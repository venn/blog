---
layout: post
title: It's probably not a race condition
author: zach
comments: true
---

I came across an interesting little problem a month or two ago. I was working on a crypto-currency project that needed to transmit data in the form of JSON. One down side of using JSON, however, is that binary information needs to be character encoded.

Most crypto-currencies use Base58 encoding, which is like Base64 encoding, without difficult to distinguish characters: 0, O, I, and l. (Fun aside, Base58 encoding is the only encoding where "1" does not equal 1, it equals 0 because it is the first number.) It is useful because it stops humans from misreading wallet addresses or transaction ids.

Rather than confuse people by including both Base64 and Base58 encoding, I decided to just stick with Base58 encoding for everything, even parts of that humans shouldn't normally need to read like cryptographic signatures and encrypted messages.

I was writing the project in Ruby so to convert the binary chunk into a Base58 encoding I'd written:

~~~ ruby
Base58.encode(binary_blob.unpack("H*").inject(&:+).to_i(16))
~~~

Which basically reads as: Take the binary blob, represent it as Base16 characters, append all those characters together, convert them to an integer, then convert that integer into a Base58 encoded string.

To decrypt I'd:

~~~ ruby
[Base58.decode(base58_string).to_s(16)].pack("H*")
~~~

I should have been able to go straight from binary to Base58, but the library I was using required integer input.

My tests passed, and everything worked great, so I went on to start implementing an unrelated portion of the crypto-currency.

But every now and then (around 5% of the time) my tests, which verified that signatures and encrypted chunks would Base58 encode and properly propagate to and from the blockchain, would fail.

Then I'd immediately re-run them and they'd pass. So naturally I thought "race condition" and moved on. My code worked just fine a second later so it couldn't possibly be anything else. I always thought that Rspec would do the right thing and run tests in parallel, since tests are supposed to have no side effects. Also my tests were pretty slow, because certain operations are not possible with less than 1024 bit keys in Ruby's OpenSSL due to security concerns, so to speed things up I used variables that were shared from spec to spec, instead of the normal:

~~~ ruby
let(:signed_blob) = { long_running_process }
~~~

So I figured it was possible I was inadvertently opening the door to a race condition somewhere. I should note at this point that when I mentioned this to Justin, he shook his head and informed me that it probably wasn't a race condition and told me that Rspec does not run things in parallel by default.

I continue on letting these tests randomly fail until I started the file-upload code, which splits large files into smaller chunks then puts them back together. When those started failing I knew the problem wasn't OpenSSL. With a now reliably failing test I started diving into where my code was breaking down.

The problem with debugging binary data stuff is that you can't just "see" what you are doing. Printing it to the terminal will just flood you with a whitespace and unreadable characters. Frustrated, I finally decided I was going to compare binary to binary before and after. To do this I changed my hex based packing code to binary:

~~~ ruby
binary_blob.unpack("b*")
~~~

and

~~~ ruby
Base58.decode(base58_string).to_i(2)
~~~

so I could print the actual ones and zeros to compare them bit by bit (Achievement Unlocked - *Literally Bit by Bit!*).

I discovered problem quite quickly. When you have binary data that starts with "0001111" and you represent it as an integer it is equivalent to "1111" since leading zeros are meaningless on a number line. But without those leading integers, it wont' reassemble the same data.

I was losing all my leading zeros! The fix was really easy, just add one bit at the start and encode it. When decoding it, ignore the first bit.

It also explains why my initial build was failing roughly 5% of the time, since I was representing the binary data as a hexadecimal encoding before converting it into an integer 1/16 of the time the first hexadecimal number was a "0".

Heisenbugs are hard, but next time I encounter one I'm going to resist thinking *race condition*.
