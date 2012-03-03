---
layout: post
title: "Newly Discovered Things That Rock"
date: 2010-11-18 16:52
comments: true
categories: apps development software
---
In the past few days I've run across a few tools that have been very, very handy.

First is [virtualhost.sh](http://code.google.com/p/virtualhost-sh/). This is a shell script that sets up virtual hosts using the Mac OS X
built-in Web server. I've been working on a [Wordpress](http://wordpress.org/) project for one of my clients, where they have a bunch of 
plugins that implements part of their Web site, but they do not provide a seamless user experience. Basically they want their customers,
when they sign up for a membership, they enter all of their information once and it creates a user with the right access, it puts the user's
information in their back-end database system, and it charges their credit card. The current experience has the user entering information on a 
bunch of different pages and a lot of stuff needs to be typed in over and over again. Not the best impression.

One of the problems developing sites locally is that a lot of sites really like to be at the root of their own domain/subdomain. Some parts
of this wordpress instance's configuration assume that. So I needed to define a virtual host for this site, and thanks to this script, it took
about five minutes to download, install the script and create the virtual host.

For Rails development, that brings me to the second awesome tool: [Passenger](http://www.modrails.com/) + [PassengerPane](https://github.com/alloy/passengerpane).

I cannot believe it has taken me so long to discover passenger for development on the mac. It's nice not to have to run `script/server` all the
time and worry about more then one app being on the same port. With Passenger on the mac, you can just set up hostfile aliases for all the apps
that are under development and just hit them in the browser. It's especially nice for some of the Flex+Rails work that I've been doing because I
can set a domain that is allowed under the production servers' `crossdomain.xml` file.

[PassengerPane](https://github.com/alloy/passengerpane) makes it super easy to define vhosts and hostfile entries for as many rails applications 
as you want.

I love it when the things that seem to be hard turn out easy!
