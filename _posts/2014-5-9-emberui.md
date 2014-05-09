---
layout: post
type: draft
title: EmberUI
subtitle: Nine months after we first wrote about it, liftoff!
author: jaco
---

EmberUI has been a labor of love and it is finally ready to see the light of day. Please use it, fork it, patch it. We especially need help ironing out bugs in Windows and Linux.

We have tried to set a new standard of quality with EmberUI. Throughout the design and build process we have been governed by one rule: the user experience trumps all. No matter how small the detail was, if it made it the act of using a component better then it had to go in. It is, after all, the small details that create the elusive “native” feeling.

<div class="image-wide">
  <a href="http://jsbin.com/zuric"><img src="/public/images/posts/2014-09-emberui.png" /></a>
</div>

Play around with a live version on the [EmberUI website](http://emberui.com) or [JS Bin Sanbox](http://jsbin.com/zuric)

## Key Features

EmberUI is a polished product that you really need to use to appreciate, but here’s some of the things we are most proud of:

**Error handling.** Form elements are smartly validated as the user uses them and errors are displayed inline. Combine with a library such as [ember-validations](https://github.com/dockyard/ember-validations) and get all your error handling done with almost no work. 

**Customization.** EmberUI was built to look great right out of the box. Obviously each application has unique requirements so customization is paramount. Everything can be changed or extended to fit your product: component sizes, aesthetic styles, animations. Everything, and with a nice API to boot!

**Animations.** The EmberUI philosophy is that anything that changes visually needs to be animated. We use a combination of CSS and JS animations and transitions to achieve a very fluid experience on desktop and mobile.

**Keyboard support.** You can use all the components using purely a keyboard. We paid special attention to the experience of tabbing through the components and making sure focus is always where you expect it to be.


## The road to 1.0.0

When we release 1.0 we will lock down the API, but before we get there, there are a few things that has to happen first.

**More components and mixins.** Adding a masked input, custom scrollbars, Stripe, and possible a validations library is in the cards. We want to make sure once we hit 1.0 that the component library covers all the basics of building a modern application.

**Better mobile support.** While most components will work just fine on mobile right now, we want to really push the mobile experience forward and make the components feel like native mobile components. For example, the select window should consume the entire viewport on mobile.

**More polish.** There are a few known issues that needs to be addressed. The biggest one is how we disable page scrolling when a modal is open. Right now is causes the content to shift around on Windows which is not acceptable. We also need full keyboard support which the calendar components do not yet support.

**Full WAI-ARIA support.** This is a larger goal and very important to ensure that EmberUI can be used by everybody. When 1.0 is released we need full [WAI-ARIA](http://www.w3.org/TR/wai-aria-practices/) support for all components.


## How can you help

This biggest thing right now is to get people using EmberUI so we can get feedback on the API. Once 1.0 hits the API will be locked down, but until then we want to make sure we create the best possible interface. 

Code refactoring would also be appreciated. Our goal was to get a working version first, and then iterate on it after that to improve it. Take a look at the [repository](https://github.com/emberui/emberui) and please send us pull requests.

Take a look at the project [README](https://github.com/emberui/emberui#pull-requests) for more about how to send us a pull request and syntax conventions.  


###### Links

[EmberUI Website](http://emberui.com)  
[Github Repo](https://github.com/emberui/emberui)  
[JS Bin Sandbox](http://emberjs.jsbin.com/zuric)  
