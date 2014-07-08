---
layout: post
title: Designing for the color blind
author: jaco
comments: true
---

Color blindess affects 7 to 10 percent of the male population. It is a large enough demographic that you should be spending some some time making sure that your designs are still usable by those affected.

The most common types of color blindness are *protanopia* (can't see red) and *deuteranopia* (can't see green). About one third of the color-blind are completely blind to red or green. The rest generally having a milder form of color blindness.

What can you do to improve your designs? There are a few basic things you can do:

##### Pay attention to your link color

Blue is the safest color. If you make your link color red or green, or event just tint it, you need to underline it as well or people may not realize it is a link. Take a look at this screenshot from CrunchBase. It is not clear at all that you can click on the names of people.

<a href="http://www.crunchbase.com/organization/blablacar"><img src="/public/images/posts/2014-07-08/crunchbase.jpg" width="100%" /></a>

With Invision their primary call to actions, normally in pink, fall completely flat and fades into the background. The signup button in the top right corner is practically invisible.

<a href="http://www.invisionapp.com"><img src="/public/images/posts/2014-07-08/invision.jpg" width="100%" /></a>

Google, on the other hand, is largely unaffected. The primary link color stays the same, and the url in green underneath turns gray and matches the  link to its right.

<img src="/public/images/posts/2014-07-08/google.png" width="100%" />


##### Don't depend on red and green to indicate status or error state

Red and green may as well be the same color, so don't depend on it. Look at the Devices tab in Google Chrome. Which port is forwarding correctly and which is failing?

<img src="/public/images/posts/2014-07-08/chrome.png" width="100%" />

If you want to use red and green make sure to combine them with a label or icon so color is not the only indication of what is going on.


##### Be careful when using color legends

Frequently chart legends depend on the user matching the color of a bar or line with a color swatch next to a label. Colors like purple and blue will become earily similar when viewed by a color-blind person.

<a href="https://mixpanel.com/segmentation/"><img src="/public/images/posts/2014-07-08/mixpanel.jpg" width="100%" /></a>

##### Unsure? Simulate color-blindiness in Photoshop

Photoshop provides a built in way to preview what designs look like to somebody with protanopia or deuteranopia. Simply turn on proof colors with &#8984;Y and go to View > Proof Setup and select the color blindness type you want to simulate.
