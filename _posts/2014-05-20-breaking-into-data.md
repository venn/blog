---
layout: post
title: Breaking into Data
author: zach
comments: true
---

Recently someone I used to work with at 500px reached out to meet for coffee.

> I want to get into data.

The allure of web applications had started waning, and he was looking for something more esoteric and challenging. We talked for about an hour and a half, and by the end of it I'd emailed him several links for him to follow up on. Only now, almost a month later, did I realize that this information could be useful to more than the one person I shared it with.

## Pick a direction

*Data Science* is an awkward title. The field is based on programming, but it has many influences depending on where you specialize. Visualizations / charting (design), predictive analytics (statistics), machine learning (statistics & computer science), analytics / report writing (business accounting), data warehousing (database administration), multi-objective optimization (economics / systems design engineering).

And in most of these sub-specialties we have the general data munging that removes the Zuckerbergs and matches *Zoë Keating, San Francisco, California* with *Zoe Keating, SF, CA* (this is literally half of what we do).

## Disregard certifications, acquire data

No one really gives a shit if you're certified. No one worth working for anyway.

The best way to get into data is start and finish projects that are similar to the type of work you want to tackle at your ideal day job. [Here](http://www.quora.com/Where-can-I-find-large-datasets-open-to-the-public?share=1) is a big list of open datasets that you can peruse to get inspiration. Also, try to stick to Python for backend programming and JavaScript for visualizations; there are alternatives, but unless you're angling to work at a hedge fund, this is what the market wants right now and for the foreseeable future.

Don't think that you need the perfect open dataset, sometimes the right non-open dataset is just as easy to acquire. For example, if you want to analyze and optimize, say, startup growth metrics, you can read up on it then convince some local startups to let them give you a crack at analyzing their data. Anonymized reports on startup growth from real startups look a whole lot better on a portfolio than nothing at all. Furthermore, if you do a really stunning job, you may not even need to interview at all; a startup may give you an offer on the spot.

> But what startup is just going to give me their data?!

Most of them. They wish they had someone looking at their data.

> What about other sub-fields?

Creating visualizations is an easy way to start. Take something that is already visualized poorly, and revisualize it. Contact the original user and get them to use your version instead. Checkout [orange](http://orange.biolab.si/), [iPython](http://en.wikipedia.org/wiki/IPython), and [d3](http://d3js.org/). Of course Excel works great. Stay away from pie charts and infographics that lack substance. If you want to make something truly amazing, consider learning photoshop or illustrator and do the charts and graphics by hand after rendering them somewhere else. If it isn't beautiful, you're wasting your life.

Data warehousing is a bit trickier. Your best bet would be to find a number of separate data sources that really should be combined then combine them and build out an API for anyone to use. Examples here are hard because it is highly situationally dependant, but perhaps write a scraper that consumes multiple municipalities and provinces voting data in your country and provide a uniform API for people to query. Whatever you do, be sure to read [The Data Warehouse Toolkit](http://www.amazon.com/The-Data-Warehouse-Toolkit-Dimensional/dp/1118530802/ref=sr_1_2), I did and it changed how I looked at organizing data for reporting (thrilling stuff, I know). I will warn you that data warehousing is extremely boring, but extremely easy and pays well with incredible job security. Be the [Beamter](http://en.wikipedia.org/wiki/Beamter) of the tech world.

Predictive analytics: sports, stocks / options / derivatives, elections. Also, [Kaggle competitions to a limited extent](http://www.kaggle.com/). If you really want to own this field it will take more work than the others, but it is the easiest way to become a millionaire by the time you're 27, you'll just have to work for a soul crushing hedge fund or private equity firm "making book".

Machine learning: Tons of possibilities here. Classifiers, search, recommendation engines, image analyzers, chatbots, so many possibilities. Start by getting up to speed on some of the basics [here](http://homepages.inf.ed.ac.uk/vlavrenk/iaml.html). Check out a couple cool libraries [here](http://scikit-learn.org/stable/), [here](http://radimrehurek.com/gensim/), [here](http://scikit-image.org/), and even [here](http://orange.biolab.si/). Read papers coming out of Google / Facebook / U of Toronto / MIT / Stanford / Italian Universities. It will be hard at first, but if you already have a background in science, engineering, or math, you'll be ok. Next, hit up some open data sets and try to think of what people want to know or find that they currently can't. That is essentially what machine learning is. Also, be sure you understand [ROC](http://en.wikipedia.org/wiki/Receiver_operating_characteristic) curves, because they are probably what you'll want to make sure that your predictor is operating optimally (this is how you iterate on a ML project). Be sure to hit up [Kaggle](http://www.kaggle.com/competitions) and try your hand at some of the competitions or just analyze Wikipedia and build a website classifier. Pro-tip: don't crawl Wikipedia, there are tarballs available for data hackers.

Multi-objective optimization: I've only used these in the construction industry, so my exposure to them is quite narrow. I understand that economics and government / environmental policy is involved here too; perhaps investigate a pollution angle? If anyone has suggestions here, I'd appreciate them.

## Finish

Finishing is the hardest thing in the world, but once you get a couple polished things out there and start telling people about them success will start snowballing.

If this post inspired you to start, finish, and polish something, please let me know, and I'll be sure to feature your work here. If you have any questions or are looking for more specific advice please reach out, I love talking to interesting people.
