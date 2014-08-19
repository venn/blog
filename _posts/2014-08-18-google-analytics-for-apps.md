---
layout: post
title: Google Analytics for mobile and web applications
author: zach
comments: true
type: draft
---

Google Analytics is still the dominant tool for web statistics for webistes across the web. Depending on the measurement methodology used, somewhere between fifty and sixty percent of the properties on the web have Google Analytics enabled.

Understanding Google Analytics requires a solid understanding of Google as a company. Google is still primarily in the business of bringing users to content and monetizing through premium access to those users. This is why Google took on Apple in the smart phone world; the web was increasingly going mobile and Apple would have a lock what content (apps, In-App Purchases, even books) users had access to.

Google Analytics is designed for the web the way that Google sees it: Primarily a place to find content to read or watch, a place to click on adds, and a place where people purchase goods and services. This is the vast majority of websites, which is why Google Analytics is structured around visitor flow, repeatable goals, and AdWords. Prior to orientating a change to a more pro-privacy angle there was also higher focus on keywords. They are still available in Google Webmaster Tools, but can't be tied together with in app events and other Google users.

Pulling all this together, what is the typical usecase that Google Analytics was designed for is an ecomerce site that needs to figure out what users are searching for, what types of users are purchasing the most, and optimizing copy, shipping rates, and translations to better match the type of users that are most likely to purchase. Also, maximizing advertising spend to the properties that have the largest margin (or *Goal Value* in Google Analytics).

But for web and mobile applications, especially for those that have some concept of a signed in user and a recurring monthly payment, Google Analytics at first blush seems unable to provide the tools that are needed to analyse user behaviour. For example, it is far more important to see how many users that signed up for a paid account a month ago pay for the second month, than it is to know which internal page a user convereted from.

While a platform like [Mixpanel](https://mixpanel.com) or even more generally [Segment.io](https://segment.io/) will certainly provide easier access to this information, they can be a bit pricey and for simple answers Google Analytics can be good enough. Other approaches involve building an in-house data dashboard, which I usually recommend against, since most companies don't realize that building an internal data dashboard is building another product that needs to be maintained. If you need custom programming, scripts that generate daily or weekly metrics emails should be more than enough for most startups with less than fifty people.

# Cohorts

Cohorts are super useful. How many users you retain from month one to month twelve impacts a number of your business' key objectives: Churn, Life Time Value (LTV), even Average Revenue Per Unit, since longer staying customers end up upgrading to larger packages.

You can set up cohorts in Google Analytics in two seperate ways. If your app is sign-in only (like say, Tinder, where the only action an unsigned up user can take is to connect his or her Facebook account) then it is pretty easy, just select *Date of First Session* under segments (click from the admin tab) and select the date range that defines the segment. Try to stick to monthly and weekly cohorts though. Unless you are first launching something really new and are really interested in fine grain adoption and retention data, I don't recommend daily cohorts, since it's too much work for samples that have too much statistical noise cohort to cohort.

If your application has a conversion event that happens after the users first session (for example, a freemium app where users can upgrade and pay a monthly fee) then you need to create an event with a label that is the date and time (best formatted using UTC, like this: 2014-11-25T13:15:30Z). Then under segments select *Sequences* and select both *Users* (not *Sessions*) and *First user interaction* and create a regex that matches your desired cohort.

You must do this for every single cohort you wish to create, which is tedious, but now you are able to look at just this cohort through all of Google Analytics, including custom reports.

# The Funnel

Google Analytics has a pretty poor experience for funnel tracking, especially across cohorts of users, where you want to find out how many free users that orginally signed up in a given month have upgraded to a paid account.

But it is possible. To accomplish this we need to create events where a user first did the desired action (for exmample, "User's First Upgrade" as an event action with an event label of the date and time). To answer your developer's question: yes, this means you'll need to store whether or not the user has done the action yet or not on your back end. I know it is yucky. I'm sorry.

Then in Google Analytics create these events as goals. Once the goals  are properly registering (Google doesn't allow you to generate goals as data in the past), we can use custom reports and our cohort segments to track the funnel for users of different cohorts, as well as track our progress over time. Keep in mind that you should be only concerned with goal completion numbers, not percentages, since the goal managment built into Google Analytics is not optimized for a traditional SaaS funnel, but more for an ecommerce site, where goals can be skipped or repeated.

Can start to experiment by optionally including some users into a beta release or split test group and measure the impact not just in the conversion from one step to another, but in the overall value of a customer or segment.

That being said, I do not believe that products should be designed by split test. I've seen too many companies get stuck on a localized maxima, instead of focusing on creating amazing experiences for their core customer base. It saps out the creativity and delight from your designers if your company is designing by committee + split test. That being said, from time to time a split test is warranted, for example I've often seen increasing prices ten fold only decreasing conversion by half, thereby five folding profit.

# Smarty Pants Segments

While cohorts and funnels should be the back bone of most SaaS app models, they arn't everything. Sometimes what we care about is customer segments, for example, free users vs paid users, or customers from a certain type of industry.

The the two tools we have to create these different segments are:

1. Custom Variables + Segments.
2. Events + Advanced Sequence Segments.

This is best illustrated by example:

Let's pretend that we're in charge of marketing at Tinder and we want to figure out better ways of engaging average looking guys that are interested only in women. There are two ways we can proceed, the first is to create a custom variables called *attractiveness*, *gender* and, *orientation* then create a segment using these custom variables and their value. If a user changes their oreintation or uploads a new photo that increases his perceived attractiveness, then we can update that user's custom variable, which will no longer include him in the segment.

There is only one problem with this approach: The free version of Google Analytics has a limit of 20 custom variables. Use them if you can, but otherwise we have to rely on another event hack:

Using a combination of include and exclude filters, exact match / does not exact match regexes, as well as fine grained step data you are able to simulate custom variables even for users that switch back and forth between categories (each of which would require specific step classification in order to prevent double inclusion into multiple sets). It is painful to set up, but once set up, it creates readibly usable segments that even someone with very little data analysis experience can use.

# Final thoughts and hacks

Keeping an organization's custom reports and segments synced is a massive waste of time. Google only lets you share 20 at once, and things can quickly get disorganized. Even something simple like sharing a dashboard that links to custom reports results in a confusing experience as some users will be able to click into the linked report, while others will not. And you will have to do this every time a user joins the company.

There is a great solution that I learned from a company I did some Analytics consulting for: Make a special user account called Analytics and just have everyone sign in there. Sure you'll have to change the password if someone is let go, but it's much less of a pain. Ideally of course Google would just fix this by enabling a mode where all users saw all the same data, but in the mean time it's probably easier this way.

Another nice hack that I love to do is to match up any internal tracking codes to visual representations right into Google Analytics by building a bookmarklet. For example, rather than just track a url or tracking code of a banner ad cohort conversion report, you can get it to appear in place at the click of a button.

As you can probably tell, Google Analytics isn't the perfect tool. On the one hand, they do allow enough power in event tracking, goal tracking, segments, and custom reports so that you can ultimately achieve your goals, but on the other the experience is hobbled and ultimately only a stop gap for internal reporting.

But for a stop gap, it sure can get stretched to the limit.
