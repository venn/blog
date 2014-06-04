---
layout: post
title: It's Probably not a Race Condition
author: zach
comments: true
type: draft
---

I came across an interesting little problem a month or two ago. I've been working on brand new, from scratch crypto-currency over the past half year that features a novel proof-of-work algorithm. I hope to provide a couple useful things from this crypto-currency, like decentralized file backup, as well as messaging that is hardened against [network timing attacks](http://en.wikipedia.org/wiki/Timing_attack), something that even Tor based communication is vulnerable to against adversaries like the NSA.

Since I want to make writing clients for the crypto-currency very easy, and I want the protocol to be easily extendable, I've decided that the data format should be JSON. One down side of using JSON, however, is that binary information needs to be character encoded.

Most crypto-currencies use Base58 encoding, which is like Base64 encoding, only it lacks difficult to distinguish characters: 0, O, I, and l. (Fun aside, Base58 encoding is the only encoding where "1" does not equal 1, it equals 0 because it is the first number.) It is useful because it stops humans from misreading wallet addresses or transaction ids.

Rather than confuse people by including both Base64 and Base58 encoding, I decided to just stick with Base58 encoding for everything, even parts of the crypto-currency that humans would never need to read like cryptographic signatures and encrypted messages; and since I'm writing the reference implementation in Ruby, that means using OpenSSL.

To convert the binary chunk into a Base58 encoding I'd just run:

`Base58.encode(binary_blob.unpack("H*").inject(&:+).to_i(16))`

Which basically reads as: Take the binary blob, represent it as Base16 characters, append all those characters together, convert them to an integer, then convert that integer into a Base58 encoded string.

To decrypt I'd:

`[Base58.decode(base58_string).to_s(16)].pack("H*")`

My tests passed, and everything worked great, so I went on to start implementing an unrelated portion of the crypto-currency.

But every now (around 10% of the time) then my tests, which verified that signatures and encrypted chunks would Base58 encode and properly propagate to and from the blockchain, would fail.

Then I'd immediately re-run them and they'd pass. So naturally I thought "race condition" and moved on. My code worked just fine a second later so it couldn't possibly be anything else (right guys, right?). Also, I fundamentally misunderstood how rspec actually worked. I always thought that it would do the right thing and run tests in parallel, since tests are supposed to have no side effects. Also my tests were pretty slow, because certain operations are not possible with less than 1024 bit keys in Ruby's OpenSSL due to security concerns, so to speed things up I used variables to speed things up, instead of the normal `let(:signed_blob) = { long_running_process }` to re-instantiate certain test variables on every test. So I figured it was possible I was causing a race condition somewhere. I should note at this point that when I mentioned this to Justin, he was like "lol, probably not a race condition homie" (I'm paraphrasing) but I disregarded his sage wisdom and pushed on.

I continue on letting these tests randomly fail until I started the file-upload code, which splits large files into smaller chunks then puts them back together. When those started failing I knew I couldn't blame OpenSSL anymore. With a now reliably failing test I started diving into where my code was breaking down.

The problem with debugging binary data stuff is that you can't just "see" what you are doing. Printing it to the terminal will just flood you with a whitespace and unreadable characters. Frustrated, I finally decided I was going to compare binary to binary before and after. To do this I changed my hex based packing code to binary `binary_blob.unpack("b*")` and `Base58.decode(base58_string).to_i(2)` so I could print the actual ones and zeros to compare them bit by bit (Achievement Unlocked - Literally Bit by Bit!).

I discovered problem quite quickly. When you have binary data that starts with "0001111" and you represent it as an integer it is equivalent to "1111" since leading zeros are meaningless on a number line. But without those leading integers, it wasn't generating the same data. I was loosing all my leading zero bits! The fix was really easy, just add one bit at the start and encode it. When decoding it, ignore the first bit.

I'm really enjoying writing this currency from scratch. I'm learning a lot about things I don't usually have to think about and it is nice to work on something that isn't ultimately served behind a web app. I'm also enjoying learning about stuff that I've never had to think about, like stream ciphers, RSA key based encryption, which SHA to use, how bcrypt isn't a one way function; but some of the most interesting things are lessons like this that you don't even know you're going to learn until you do.
