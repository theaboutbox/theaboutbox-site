---
layout: post
title: "Devops Lite"
date: 2013-06-20 10:58
comments: true
categories:
  - devops
  - development
---
I've been hearing some great things about [Gitlab](http://gitlab.org/)
to handle source control in those cases where clients want to run Git,
but are not in a position to have a Github account or a hosted version
of Github, or perhaps for a huge number of private side-projects. Interestingly, 
it also as a CI server.

I just ran across [Dokku](http://progrium.com/blog/2013/06/19/dokku-the-smallest-paas-implementation-youve-ever-seen/),
a "mini-heroku" that accepts git push requests and deploys them.

I think one could do something very, very interesting with Dokku plus
[Knife Solo](http://matschaffer.github.io/knife-solo/) to spin up
servers and provision them.
