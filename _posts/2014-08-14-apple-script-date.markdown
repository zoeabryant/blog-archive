---
layout: post
title:  "Creating a keyboard shortcut to write the current date and time"
date:   2014-08-14 18:10:12
tags:
- apple mac
- keyboard shortcuts
- how to
---

I've only just started using Jekyll to create this blog today. I'm still getting used to quite a few things about this set up. One thing that got to me is the date format that Jekyll requires every post to have. It looks as follows:

**date: 2014-08-14 17:28:17**

That's a pretty intense format, and not something I can easily write off the top of my head. Googling around, it appears I am not the only one with this problem.

This post from [Andy Taylor][andytaylor] walks you through the process of creating an Service with AppleScript in the Automator app. Basically, write a mini programme in a mac friendly format that can be assigned to a keyboard shortcut. Andy's blog post pointed me in the right direction, but I found that his code didn't work - it was written 2 years ago. It just means I had to work a bit harder!


#### Getting the date in terminal (Command Line/Shell/Bash/what have you)
I looked at Andy's AppleScript and realised that all he was really trying to do was run a shell script. Which meant that I should start figuring out how to get what I wanted in bash.

Which meant that if I want to be able to write the date in Jekyll's format I should start with knowing how to do it in bash.

Back to google. I found this article on [how to format date and time][unixdate] very useful. After playing around for a bit I settled on this shell command:

{% highlight bash %}
date +'%Y-%m-%d %T'
{% endhighlight %}

All this basically says is

**Run:** date

**format:** +'..'

**%Y** for 2014 (%y returns 14)

**%m** for 08

**%d** for 14

**%T** for the time, to the millisecond

Each of these values is separated by a - or a space, just to format.

This gets my desired date time format: 2014-08-14 17:43:55

#### Making an Automator Service
Getting the date and time in bash is all very well but I need to package this up in a format that my macbook will understand. This is where Andy's article really came in handy. Let me run through the process I took.

1. Open up the Automator.app. I just searched for it, the icon is a robot.

* You want to create a **Service**, so make your document type a Service.

* On the left hand side you should see your library, which contains a bunch of preformatted action types to use. On the right should be your workflow area, with a prompt to build your workflow.

* Setup your workflow to recieve ** text ** in ** any application **. You're looking at the box above your workflow area which has a few dropdown boxes to select your options from.

* You want to make sure that whatever your code outputs (in this case, the Date and Time) replaces the text that you have highlighted. Check the box for **Output replaces selected text**

* Right, now you have set up you need to create your workflow. This finished script will work like this: you will be able to highlight a bit of text, press your keyboard shortcut, and replace that text with your current date and time. So first things first, you need to make sure your Service can **Get Specified Text**. You can do this by using the action types that are in the library Automator has. Search for 'Get Specified text' and drag the action over to your workflow.

* Next, you need to do something with that text. Specifically, run an AppleScript that will run the date shell command. Search for **Run AppleScript** action and drag that into the workflow.

* The Run AppleScript action helpfully put in the basic code.
I replaced it with the following:

{% highlight AppleScript %}
on run {input, parameters}

	return do shell script "date +'%Y-%m-%d %T '"

end run
{% endhighlight %}

All that says it when this AppleScript is run, return the output of this shell command.

Press the run button to see if it works. You will need to open out the 'results' tab at the bottom of your Run AppleScript block. All being well, you should see the date and time formatted as desired.

Save this Service to ~/Library/Services. It should automatically position you to save there, just save it as something helpful.

This is a screenshot of my finished AppleScript Service:

![my AppleScript Service]({{ site.url }}/assets/post_img/2014-08/14-apple-script-date.png)

#### Assigning a keyboard shortcut to my Service
1. Open the Settings menu and select Keyboard Settings, Shortcuts
2. Find your created Service in the Services menu. It should be under the 'Text' menu. It's a loong list...
3. Activate it by checking the checkbox, then double click on 'add shortcut'
4. Just press what you want the shortcut to be. Mine is ⌃⇧⌘T (ctrl shift cmd T). It's a little long winded. I wanted Shift so I know I have to highlight text, T for time and ctrl and cmd so I can make it as unique as possible to avoid conflict with Sublime Text keyboard shortcuts.
5. Give it a go! 2014-08-14 18:05:34

### Conclusion
It's incredibly satisfying. 2014-08-14 18:06:11 . After the initial set up I was very concerned it wasn't working, but I just needed to make sure I was always selecting text and that I was pressing the right buttons. I was also put off by the occasional delay before the date is outputted.

I would like to tweak this code some more, see if I can refactor my Automator Service down to its most basic functionality, or set it up so that I don't have to highlight any text. As it stands I am pretty happy! For my first try at writing AppleScript, it wasn't so bad. Real Experts: let me know what I can do to improve my process here.

### Resources
[andytaylor]: http://andytaylor.me/2012/11/10/creating-an-osx-service-to-insert-the-current-date-and-time/
[Andy Taylor Blog][andytaylor]

[unixdate]: http://www.cyberciti.biz/faq/linux-unix-formatting-dates-for-display/
[Unix Date format reference][unixdate]

Macbook Pro running OS X Mavericks.