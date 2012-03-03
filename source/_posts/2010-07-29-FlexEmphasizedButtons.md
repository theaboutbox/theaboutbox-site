---
layout: post
title: Skinning Emphasized Buttons in Flex
date: 2010-07-29 16:52
comments: true
categories: flex development howto
---
Recently on a new Flex 4 project, I needed to apply a dark theme to all
the components in the application. It has been a great opportunity to learn
the new FXG skinning introduced in Flex 4. I have been a big fan of
Degrafa for a while, and fortunately for the simpler tasks FXG is not all
that much different.

Everything went along swimmingly until it became time to create a dark
button theme. Here is the login window when the application starts:

<img src="http://idisk.me.com/cameron.pope/Public/Pictures/Skitch/LoginScreenInactive-20100729-122252.jpg" alt="LoginScreenInactive"/>

Then, as soon as you focus on a form element, the button takes on a completely
different look and feel, one that is not defined in the skin, and cannot be
styled via CSS on the button:

<img src="http://idisk.me.com/cameron.pope/Public/Pictures/Skitch/LoginWindowEnabled-20100729-122354.jpg" alt="LoginWindowEnabled"/>

It took me a while to find the answer, but what happens, is when a user focuses
on a form element, the 'Default Button' for the window becomes 'enabled'. I
first thought I could define an 'enabled' state on the button skin to fix the
problem, but that is not possible. Instead, you need to define style rules
for the enabled state and create an entirely new skin.

<pre><code class="language-css">
.button
{
	color: #000;	
	skin-class: ClassReference("styles.ButtonSkin");
	accent-color: #000000;
}

.button.emphasized
{
	skin-class: ClassReference("styles.ButtonSkinEmphasized");
}
</code></pre>

I hope this saves someone out there some trouble!
