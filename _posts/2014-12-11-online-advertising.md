---
layout: post
title: Online advertising and the future of web browsing
author: zach
comments: true
type: draft
---

For a long time I resisted installing an online ad blocker. I felt that doing so would both make me a net drain on content producing websites, and would warp my view of how websites look and work. I also thought that it was bad enough that I had to trust established companies like Google, Apple, and Canonical to not steal my passwords while browsing the internet, but by enabling a third party browser plugin I was trusting developers of significantly less repute.

What changed my mind over the summer were four things coming together all at once:

1.  Youtube ads got longer, more frequent, and more distracting. I just wanted to put on some music in the background and get some work done, but instead I was interrupted every two to three minutes. My workaround was to put on longer mixes, but Google changed the way ads work, interrupting longer videos every fifteen minutes with ads.

    Furthermore, video ads are the worst type because they don't solve a problem. Unlike search ads which are occasionally helpful and generally ignorable if you're not interested in the content, video ads pit user against advertiser.

2.  A friend figured out a way of getting people's real names and work positions when they visited his website. After he told me about it I wrote a crawler[^1] to see if any companies had also figured this out and were using this hack to build sales lists. I set the crawler loose on every company with a domain on AngelList and Crunchbase. I didn't find anyone doing it, but I was only scanning links one deeper than the homepage.

    While the method we'd figured out no longer works, it lead me to realize how much data bleeds between companies.[^2] I had to accept that a large portion of my browsing history was in the hands of advertisers and social media companies and furthermore that these companies could also know my name, age, and occupation.[^3]

3.  I realized that almost all of the non-video content I consume is produced by people that do not rely on advertising as their primary form of income. They either create it for free or use it as a lead generator, like this blog which helps drives leads to our Toronto digital services agency.

    In the case of video, I think a new business model will emerge in the future. Intrusive ads like video, audio, or even flashing banner ads are not sustainable. They reduce focus, waste time, and create un-intelligent communities.

4.  I learned about [malvertising](https://en.wikipedia.org/wiki/Malvertising) and I realized that it was more likely that I'd get owned by an exploit sent through an advert than I woudl get owned by having an unscrupulous developer at Adblock Plus lift my password. Furthermore I realized that enough developers over at Google or Canonical used an ad blocker that I've already lost if they can't be trusted.

Now that I've made the switch to blocking ads I can't see how I ever lived without it. The internet is just better. Even in places where I wouldn't have minded the ads pages just load faster. Fonts and colors for sites look more cohesive, since another site's random branding isn't barging its way in. I'll never go back.

[Almost 10%](http://techcrunch.com/2012/05/18/clarityray-ad-blockers/) of web traffic by humans is ad blocked, and that was back in 2012. I believe that soon adblockers will be adopted by the majority of people going on the web.

I also think that there is an opportunity for a new browser.[^5] One that ships with ad and tracker blocking by default. One that randomly requests websites to give web browsers plausible deniability for people monitoring unencrypted web requests. One that integrates VPNs and possibly even Tor[^4] in a really user friendly way. For example, if content is blocked by a region the browser should automatically make the request from a computer in a region that is not blocked or forging X-Forwarded-For ips to look like they come in a country where the content is not blocked. It could even make money by selling a freemium on-demand proxy service.

A company like Apple could make it - completely eviscerating Google in the process - but it might drum up anti-trust complaints and meddling from national governments that want to protect their ability to censor the internet. So ultimately I think it will be based off of an open source engine like WebKit and built by a startup.

[^1]: My first startup (in 2009) was a web crawler that crawled the web and recorded online advertising. It failed because search re-targeting was taking off and to get accurate data you needed to get it on a per-user basis though some kind of browser plugin.

[^2]: I'd always known this in an abstract way, but I'd figured it would be too hard to tie it all together across different domains.

[^3]: Note that this is not configured out of the box with Adblock Plus, you need to go [here](https://adblockplus.org/en/features) to enable it. Also I recommend enabling full ad protection (ie, don't allow nice ads) and enabling the blocking of social media share buttons. The reason for this is that there is no way to host these from another domain and prove that you aren't using them to track people.

    This is especially important if you're logged into your Facebook or Twitter account as it provides a way for those companies to tie your browsing history with your real name. Furthermore using an incognito browser is not enough, since there are methods of fuzzy matching that activity back to your account.

[^4]: I generally don't advise people to use Tor. It is *way* too easy to make a mistake and you may draw unwanted attention to yourself. The (often) false sense of security it gives you will often cause you to make mistakes.

[^5]: While writing this blog post I came across [Maxthon](https://en.wikipedia.org/wiki/Maxthon) a Chinese-made web browser, which ships with ad blockers by default. It is interesting, but I would be very wary of installing Chinese made software. Maxthon also has an office in SF, so maybe they are worth taking a risk on.
