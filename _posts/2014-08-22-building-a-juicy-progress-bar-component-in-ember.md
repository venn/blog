---
layout: post
title: Building a juicy progress bar component in Ember
author: jaco
comments: true
---

Over the last week I have been working on building an image uploader for an open source project I am working on.

For this application we are making use of circular profile images. I wanted users to see how the image they are uploading would be used in the application while also showing the progress of the upload. By combining the two we get to reinforce that the bar indicated upload progress, and also allow for a very tight aesthetic.

You can see the final version below. Hit the simulate button to see it in action.


<div style="height: 300px; overflow: hidden;">
  <div style="margin-top: -50px; overflow: hidden;">
    <iframe src="http://jsbin.com/behano/14/embed?output" width="100%" height="400" style="border: none;"></iframe>
  </div>
</div>

Creating this effect is not possible in CSS as far as I know, so I decided to build it using SVG. Here is the basic SVG setup:

{% highlight html %}
<svg {{bind-attr viewBox="viewBox"}} xmlns="http://www.w3.org/2000/svg">
  <circle class="bar" {{bind-attr
    stroke-dasharray="circumference"
    stroke-dashoffset="dashOffset"
    cx="radius"
    cy="radius"
    stroke-width="strokeWidth"
    r="radiusWithoutStroke"}}
  ></circle>
</svg>
{% endhighlight %}

The user supplies a diameter which we use to size the SVG container and to draw a circle that fill it. We then make use of a dashed line for the stroke, with each dash being the length of the circle's circumference. Then, by shifting the starting point of the line we can show how much progress has been made.

~~~ JS
dashOffset: Ember.computed('diameter', 'percentage', function() {
  var percentage = this.get('percentage') * 0.01;
  var circumference = this.get('circumference');

  // We have to factor in strokeWidth here because we are using a rounded edge
  // on the stroke that makes it appear to be further along than it really is
  var strokeWidth = this.get('strokeWidth');

  return circumference - (circumference * percentage) + (strokeWidth * 2);
})
~~~

The styling itself happens via CSS, so it is very easy to customize the colors and animations.

Edit: I removed the rotate transformation from the circle itself because Firefox uses a different origin point than Chrome. Instead I apply the rotate to the div that contains the svg element. The rotate is necessary because the dash starts at the 90deg point and we want to shift it to 0deg.

~~~ CSS
.circular-progress-bar .bar {
  stroke: #1787e5;
  fill: none;
  stroke-linecap: round;
  transform-origin: center;
  transition:
    stroke-dashoffset 0.6s,
    stroke 0.6s;
}

.circular-progress-bar.is-complete {
  animation: circular-progress-bar-complete 1.3s 1;
}

.circular-progress-bar.is-complete .bar {
  stroke: #8fd713;
}

@keyframes circular-progress-bar-complete {
  0% {
    box-shadow: 0px 0px 0px 0px rgba(143, 215, 19, 0.4);
  }

  100% {
    box-shadow: 0px 0px 2px 40px rgba(143, 215, 19, 0);
  }
}
~~~

The Ember code is pretty basic since you are just doing basic math to calculate radius, circumference, and progress percentage. I haven't yet decided if this is a significant enough component to make it into [EmberUI](http://emberui.com), but it could be pretty useful if made more customizable.

You can see the full component code here: [http://jsbin.com/behano/](http://jsbin.com/behano/)
