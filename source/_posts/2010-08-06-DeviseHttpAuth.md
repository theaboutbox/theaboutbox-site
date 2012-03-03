---
layout: post
title: Devise and HTTP Authentication
date: 2010-08-06 16:52
comments: true
categories: rails development howto ruby
---
I burned the midnight oil last night tracking down an annoying problem where user
logins with Devise worked perfectly in our development environment but stopped
working completely, with no error messages, on production. I tracked it down
to an issue where Devise and Nginx's http authentication fought with each other.

Like many stealth-mode startups, one of my clients isn't ready to show their product
to the world yet, so they have an http 'password wall' in front of their site that
asks for a username and password via http authentication.

Since this is a new project, we have started it with Rails 3, and we have gone with
[Devise](http://github.com/plataformatec/devise) to hanle the user authentication.
At first I was a little leery about how much it tries to provide by being a Rails
Engine - it ships with its own views, defines its own routes, contains its own views
and everything, but once I started working with it, it is really nice to have an
authentication solution that works out of the box, and then you can spend all of your
time adding functionality, which is quite easy.

Everything was perfect until the first time I deployed to production. Users could
register, but they could not log in. There were no error messages, and I could see
in other places in the application (like flash notices) that sessions were working
just fine. I spent hours trying to figure out why I could register but not log in
as a new users. Bringing up the console and exercising the controllers worked fine.
The models were behaving as expected. Development was perfect.

In desperation, I started reading through every newsgroup message and I stumbled
across a thread of [someone having the same problem](http://groups.google.com/group/plataformatec-devise/msg/d617c3d075f465d4)

Fortunately the solution turned out to be easy. I needed to make the following changes
in <code>config/initializers/devise.rb</code>

<pre><code class="language-ruby">
# Tell if authentication through HTTP Basic Auth is enabled. True by default.
config.http_authenticatable = false

# Set this to true to use Basic Auth for AJAX requests.  True by default.
config.http_authenticatable_on_xhr = false
</code></pre>


