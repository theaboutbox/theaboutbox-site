---
layout: post
title: "iPhone Popovers with RubyMotion"
date: 2013-06-21 08:34
comments: true
categories:
  - development
  - ios 
---
For an app that I am developing, I needed a simple 
[Popover view](http://developer.apple.com/library/ios/#documentation/WindowsViews/Conceptual/ViewControllerCatalog/Chapters/Popovers.html) 
that appears when the user taps a button. Apple does provide a
[UIPopoverController](http://developer.apple.com/library/ios/#documentation/uikit/reference/UIPopoverController_class/Reference/Reference.html)
class that shows popovers at a specific point, but it only works on the iPad. On the iPhone,
your application will crash if you try to use it. To work around this
issue, developers have [created their own controls](http://bit.ly/125z4QV).

The simplest one that I have found is called [PopoverView](https://www.cocoacontrols.com/controls/popoverview).
It is not the most powerful, but it is very easy to use. Its interface
is basically a set of static methods that display a popover view
anchored at a specific point. You can supply a UIView, or if you just
want to allow the user to select things, you can keep it really simple
and pass in an array of strings:

{% img /images/iPhone-popup-example.jpeg 322 482 %}

For example, here is a view controller that displays a button with a
popup to change its title:

{% include_code popover_controller.rb %}

See the [full example on Github](https://github.com/theaboutbox/rubymotion-iphone-popovers).
