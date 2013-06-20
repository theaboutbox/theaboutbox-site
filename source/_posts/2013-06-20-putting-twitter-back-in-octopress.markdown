---
layout: post
title: "Putting Twitter back in Octopress"
date: 2013-06-20 12:05
comments: true
categories:
  - development
  - blogging
  - twitter
---
I'm using [Octopress](http://octopress.org/) for blogging and with the
latest update the Twitter support went away. Why that happened is a
longer conversation, but the short of it is, that Twitter needs to make
money, so they are putting up additional roadblocks to grabbing their
data and putting it other places.

So now the only option is to embed a Twitter widget on the blog sidebar,
which is okay, but you don't get as much control. [This post](http://blog.jmac.org/blog/2013/03/30/putting-twitter-back-into-octopress/)
got me most of the way there, but it's best to keep customizations
separate so when you update Octopress they do not get stomped on.

Without further ado, here's what you need to do to get your tweets back
into your Octopress blog:

Create a new [Twitter timeline widget](https://twitter.com/settings/widgets/new)
and copy the resulting html snippet to your clipboard.

Create `source/_includes/custom/asides/twitter.html`:

{% codeblock lang:html %}
<section>
  <h1>Latest Tweets</h1>
  <!-- Paste your widget HTML snippet here -->
</section>
{% endcodeblock %}

Add `custom/asides/twitter.html` to your `config.yml` file:

{% codeblock lang:yaml %}
default_asides: [asides/recent_posts.html, custom/asides/twitter.html, asides/github.html, asides/delicious.html, asides/pinboard.html, asides/googleplus.html]
{% endcodeblock %}

(Hat Tip to [jmac](http://jmac.org) for doing most of the legwork. I
just made a few tweaks to make it a little more update-friendly)
