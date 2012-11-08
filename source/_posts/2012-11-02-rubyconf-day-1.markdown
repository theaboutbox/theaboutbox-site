---
layout: post
title: "RubyConf Wrap-Up"
date: 2012-11-02 12:16
comments: true
categories: 
---
Since RubyConf was in Denver this year, it would have been crazy not to
go. Last time I went to RubyConf, it was 2009, and it's amazing how much
the community has changed since then.

I remember listening to a presentation on some exotic Erlang-based
message-passing system, and the speaker, from Github, referred to Java
programmers as 'Drones'. Perhaps the Ruby community was still in phase
where most of the members where 'enterprise refugees' and we were
determined to burn down everything Enterprise, and remake it in a more
Agile, more Flexible image.

Three years passes. There have been a few major Rails releases. There
are a lot of people now who have these giant 'Monorail' applications,
and now they are looking for solutions for some of these scaling
problems, and if there is one thing the Enterprise knows, it's how to
operate at scale. It's as if all of us hippies cut our hair, went to
college, started families and are getting some real jobs. We need to
look to the Enterprise for wisdom, while hopefully avoiding some of
the mistakes the previous generation made. Almost every talk gushed
on the awesomeness of JRuby and the JVM, about which I totally agree. Many talks talked about breaking
apart large apps into services, and ways of structuring multi-machine
architectures, so it's still possible to test quickly and deploy
quickly.

There was also a focus on monitoring, gathering data and using it to
track usage patterns and find problems.

Here is a round-up of some of the awesome things that I discovered.

* [T, the command-line twitter client](https://github.com/sferik/t) - A
  twitter client with truly deep karate searching through twitter
  streams.

* [Gitnesse, running Cucumber Features from a Git Wiki](https://github.com/hybridgroup/gitnesse)
  Part of the "sell" for Cucumber is that you write feature descriptions
  English, so stakeholders can understand or write the stories. If
  that's the goal, why are we keeping the stories in the same place
  as the source code? Wouldn't a wiki be better?

* [Activesupport notifications](http://api.rubyonrails.org/classes/ActiveSupport/Notifications.html)
  The most important feature of Rails that I didn't know anything about.
  A really powerful way to log lots of events, which can then be
  captured, aggregated and presented by other tools.

* [Metriks](https://github.com/eric/metriks) - A lot of people sung the
  praises of Metriks as a means of capturing metrics from an application
  for publication to another piece of software, such as graphite or
  statsd.

* [Metriksd](https://github.com/eric/metriksd) - A server that can
  capture and aggregate metrics

* [Graphite](http://graphite.wikidot.com/) - Front-end and back-end
  system to store time-series data

* [d3.js](http://d3js.org/) - Javascript library to visualize data

* [Cube](https://github.com/square/cube) [Cubism](https://github.com/square/cubism/) - Projects from Square that collect and present
  time-series data.

* [System-metrics](http://nearinfinity.github.com/system-metrics/) - A
  lo-fi system for collecting metrics

* [Issue Triage](http://issuetriage.heroku.com) - A system Heroku put
  together to help triage bugs and issues in open source projects

* [mRuby](https://github.com/mruby/mruby) - Minimalistic subset of ruby
  designed to run on a very low size and memory footprint

* [MobiRuby](http://mobiruby.org/) - Runtime for iOS devices based on
  MobiRuby

* [@iDoHaiku](https://twitter.com/IDoHaiku) - Neural network that
  creates a new haiku every day.

* [metro](https://github.com/burtlo/metro) - Taking the Rails approach
  to developing 2d games with [Gosu](https://github.com/jlnr/gosu/wiki/Ruby-Tutorial)
