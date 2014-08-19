---
layout: post
title:  "Organising CSS"
date:   2014-08-19 20:57:42
tags:
- css
---

[Toan] asked for some advice on organising CSS/SCSS files. At Makers Academy the focus is very much on Ruby and back-end code, which suits most but it means that CSS is often put to the side. The advice that follows is from working on plenty of sites, usually amounting to massive CSS files. At the end of the day, it does come down to what suits the project and the coder's preferences, but here's a starting place. I'll start with plain 'vanilla' CSS and then talk about preprocessors such as Sass and LESS.


### Basics first.
One of the critical things to grasp about CSS is that it is **Cascading** Style Sheets. If you define something and redefine it later on, it will always take the latest version. It doesn't bother going through the file again. Simply put:

{% highlight css %}
h1 {
	color: red;
	color: blue;
}
{% endhighlight %}

Our header tag is going to be blue.

This is obviously easy to keep track of when it's in one place neatly together, but it quickly becomes difficult to keep track of things. This leads me to my first point:

### Generic things first, Specifics later

I like to start by sorting out the very basic things: like the typography on the page. Things that are global, things that won't matter too much if they are written over, or things that are intended to be written over.

This is kind of like setting up a [CSS Reset][reset]. A reset should be used to generalize the default browser CSS, or strip it out all together to create a blank starting point for your CSS. Your generic CSS should be about creating a plain starting point.

### Use comments to split up the file
Having a heading like such:

{% highlight css %}
/*
-- Globals / Typography
*/
{% endhighlight %}

Or even more overt than that, can really help to break up a file into meaningful chunks. In some projects, I have even created a table of contents, like so:

{% highlight css %}
/* -----------
// CONTENTS:
// -----------
// 01. TYPE
// 02. GLOBAL
// 03. NAVIGATION
// 04. HOME PAGE
// 05. ARCHIVE PAGE
// 06. TEXT PAGE
// 07. SHOWREEL PAGE
// 08. RESPONSIVENESS
// ----------- */
{% endhighlight %}

And had headers like this:

{% highlight css %}
/* 03. NAVIGATION */
{% endhighlight %}

So I could press cmd f and search the file for the correct numbered heading.

You can also see in that contents list how it builds up. I start with generic things (type) move onto global things that will affect every page (global and navigation) then I move onto page specific styling.

### Structure should be separate from styling.
I don't mean this in the HTML/CSS responsibility divide, although starting with good markup is pretty essential. I mean this in that CSS can be used for putting three boxes in the same row, or setting a width on a box. I would consider things that affect the position of the HTML element on the page, or the dimensions of it, to be structual things.

Separation can be as simple as just putting a line between them:
{% highlight css %}
.box {
	width: 50px;
	height: 50px;
	position: fixed;
	top: 5px;

	color: red;
	background-color: white;
	font-size: 16px;
}
{% endhighlight %}

Or, as you find you need to make more and more .box elements with similar structural properties, make the .box element about structure only and make a more specific declaration for the styling.

{% highlight css %}
.box { /* used multiple times */
	width: 50px;
	height: 50px;
	position: fixed;
	top: 5px;
}
.header .box {
	color: red;
	background-color: white;
	font-size: 16px;
}
{% endhighlight %}

### CSS should be refactored.
It's simple really. CSS is far more likely to inspire repetitive code, so we should look out for ways to make things generic in order to get rid of repetition.

[toan]: http://yoshdog.github.io/
[reset]: http://www.cssreset.com/
[vanilla]: http://www.vanillacss.com/
[normalize]: http://necolas.github.io/normalize.css/