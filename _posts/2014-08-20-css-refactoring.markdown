---
layout: post
title:  "Organising CSS"
date:   2014-08-20 13:56:34
tags:
- css
- how to
---

This week I let other people know about the existence of this blog, and I've recieved so many positive comments from my Makers Academy folks. Thanks people, your encouragement means so much. It's that attitude which makes this place awesome.

I've also recieved requests for posts on certain topics, specifically for CSS. At Makers Academy the focus is very much on Ruby and back-end code. This suits most (including me) but it means that CSS is often put to the side. So this post on organising CSS is for [Toan][toan]. I hope it is useful.

## Keeping CSS clean
Whilst thinking about how to structure this post, it occurred to me that actually, so many of the things we have been taught about keeping Ruby Code clean are also applicable to CSS. You heard me right: we can treat CSS like any other code base when it comes to keeping things neat and tidy.

So I looked back and found my notes on 'Code Smells' from way back on Day 9 of Makers Academy. I noted the following things that constitute a code smell, or small signs of bad code.

## Code Smells
* Obscure naming
* Long blocks of code
* Repetition
* Nested control flow
* Magic numbers and constants

So here goes, code smells and how they can be found (and sorted) in CSS.

### Obscure naming
In Ruby, we have been taught to name our methods and variables descriptively. So we write 'display_posts' rather than 'posts_output/render/something else terrible and non english.'

In CSS, this means descriptive classes and ids.

So rather than '.block-3', I could call it '.user-profile-block'.

Critically, it's advised to avoid descriptive naming that suggests styling. So don't call things 'blue-block' or 'right-block' because if you change your design later, these things might not make sense. Think about what that blue signifies in your design - is it an information block? Is it used to mark out a summary paragraph? Consider the purpose and name accordingly.

### Long blocks of code
In Ruby, this meant making sure our methods don't get as long as 5 lines or more. This is more difficult in CSS, as sometimes it takes a lot of properties to get a simple effect. However, it doesn't mean we can't separate out our CSS.

First up, separating out generic code. If there is a block of CSS that you are using for lots of different things, it should be separated into a generic class of its own. This is easier with CSS preprocessors like [LESS][less] and [SASS][sass], as you can set classes that are only used by your CSS. There are ways to do this in plain 'vanilla' CSS.

For example, if you had a bunch of notice paragraph elements that basically look the same, except that the 'success' notice is green and the 'error' notice is red, it is sensible to have a '.notice' class that sets the common features first. This may be a border radius, or padding, or font size, whatever it is. Then you would have separate classes for '.success' and '.error', which set the appropriate background colour.

Separating out long blocks of code also means commenting efficiently. In many projects, I've used massive commented out headers that help break it up. I've even created Contents lists before and numbered all of my sections so they are easy to find in a search. You can separate each 'section' of code out into separate files with [@import][import], but this is generally considered to be more practical when using CSS preprocessors.

### Repetition
This is pretty similar to above. Avoiding repetition is pretty difficult in CSS, but allow me to further emphasise the idea of generic CSS.

When starting my CSS, I like to sort out the very basic things. Things that are global, things that won't matter too much if they are written over on a specific element later on. An easy example is typography. Start with the basic font set on the body tag at the top of the page, and it saves having to set it on every single bit of generic text later on. It sounds obvious, but it can make a big difference having a good CSS foundation.

Generic CSS also means that things that will appear on every page should be set pretty early on, and more specific page things later on. When going through a photoshop design in order to make a front end version, it was critical to identify the repetitive patterns, so I would know to style those in a flexible way first. Even working out which headings in the design should be a H1, H2 and H3 made a big difference in how I approached writing my CSS.

### Nested control flow
Ok, in Ruby this means pulling out if statements and loops into separate methods, basically identifying and separating different types of logic. To me, in CSS terms, this means separating out your structure from your styling.

Although starting with good markup is pretty essential, and it is true that the responsibility of HTML is structure and CSS is styling, this isn't about HTML right now. This is about the CSS that can be used for structure. CSS can be used for putting boxes in the same row, or setting a width on an element. I would consider these things that affect the position of the HTML element on the page, or the dimensions of it, to be structual things.

Separation can be as simple as just grouping them together and perhaps putting a line break between your width property and your color property. If you need to change the dimensions of your layout, either for responsive or redesign purposes, it makes sense to have it separate so you won't accidentally change something you don't mean to. At the same time if you are changing a font colour, you don't want to searching for it amongst a bunch of stuff that basically position the box on the page.

### Magic numbers and constants
CSS is full of a ton of these. You may know that that box is set to 250px because the parent box is 500px, and that hex code color you are using all over the place is an essential bit of branding, but a new person on the project won't know that.

In vanilla CSS this means commenting. Have a key at the top that sets out your generic brand colours that can be referenced back to. Then the new person doesn't have to dig around with browser tools to find the shade of grey that is used for the text. Try explaining your maths next to arbitary numbers.

With CSS preprocessors it is much easier. Just write out your constants with the built in variable functionality and just write your maths upfront. It'll vary how much you can do this, so check through the offical documents for your preprocessor of choice. These constants can be separated out into a file of their own, like '_colors.sass' to make it extra clear.


## Conclusion
So there you go, not so different from Ruby Refactoring after all. Organising CSS is a big topic, but I hope this has given you a good starting place. For more, I recommend this [smashing][smashing] article which groups together a whole bunch of different ways of organising CSS, as recommended by experts.

CSS is simply something that you get better at by breaking it and figuring out what doesn't work. Some organisational tactics work for some projects but are overblown for others. Good luck!

## Resources
[CSS @import][import] - how to use css in multiple files

[Smashing Magazine: 70 Expert Ideas For Better CSS Coding][smashing] - for more discussion on organising CSS

[Sass][sass] - CSS Preprocessor, ruby/HAML based

[LESS][less] - CSS Preprocessor, JS based

[Font sizing: px vs em vs %][ems] - advanced, may be of interest when it comes to avoiding magic numbers and keeping track of different font sizes across a site.

[toan]: http://yoshdog.github.io/
[import]: http://www.cssnewbie.com/css-import-rule/
[ems]: http://kyleschaeffer.com/development/css-font-size-em-vs-px-vs-pt-vs/
[smashing]: http://www.smashingmagazine.com/2007/05/10/70-expert-ideas-for-better-css-coding/
[sass]: http://sass-lang.com/
[less]: http://lesscss.org/