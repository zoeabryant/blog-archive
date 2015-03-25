---
layout: post
title:  "Starting with an Arduino"
date:   2014-08-19 14:04:01
tags:
- arduino
- how to
---
For my birthday this week I finally got organised on ordering myself an arduino. Specifically, A [Start Arduino Kit][startkit] from [Technology Will Save Us][twsu], a London company that does some pretty cool things for tech education.

Now I can't exactly say I know much about electronics. In fact, talk of circuits, LEDs and wires gives me flashbacks to year 6, and I'm pretty sure I've taken some more science lessons since then. This doesn't to put me off, but it does intimidate me. Thankfully, I am in a place where I am surrounded by techy people who get excited about this kind of stuff too, so I was able to enlist the help of [Roi][roi], a Makers Academy coach, who could walk me through the basics.

### So what exactly is an arduino?
An [Arduino][ardof] is a **microcontroller**. It can be used to respond to its surroundings - detect light level, air pressure, if the device is being tilted. That kind of thing. It can be used to respond to input, so I could set it up with a button to create a game. There are so many [projects][projects] that can be done with it, It's difficult to know where to begin. Roi suggested we went for a cliche - making lights blink.

## Project: Making a row of LEDS blink
'Hello World' is a computer programming cliche. Making an LED blink seems to be the physical substitute. If you are going to try this yourself, I would suggest treating it like a cooking recipe and read it through before trying to follow my steps: many things will make sense later, when you know how it all joins together.

### You will need:
* Arduino (I have an UNO one)
* Breadboard
* USB A-B Cable to connect the arduino to the computer
* LEDs
* Cables. 2 per LED, and 1 extra (I have 21 wires for 10 lights, 20 short and 1 long.)
* [Arduino IDE Software][software] installed.

![My arduino stuff]({{ site.url }}/assets/post_img/2014-08/16-youwillneed.JPG)
Clockwise: Breadboard, USB cable, Arduino UNO, LEDs, Cables

### Setting up the Breadboard
In order to connect my arduinos to the LEDs, I need to make the most of my breadboard. It's basically a tool used to prototype electronics easiliy. If I didn't use a breadboard, I'd have to get the soldering iron out.

#### Understanding the breadboard layout
The layout is alien to me. The following explanation is a digest of [Wikipedia's article][breadboardwiki]!

The breadboard has **terminal strips**, which are intended to be used for the electronic components. In this case, my LED lights. The terminal strips have helpfully labelled columns and rows. These terminal strips tend to be split in two groups with a break/gap in the middle, to prevent everything overheating.

Down the sides, the breadboard has **bus strips** which handle the power input and output. Every electronic component needs to manage two flows of electricity: the power flowing in, and the power flowing out. Both need to be considered. The 'out/negative' power, is technically the 'ground' power. I like to think these strips are called the bus strips because they transport these two power flows to our arduino in the end.

#### Negative wire.
With this in mind, all of the ground flow of electricity need to be handled. I put my longest wire (the extra wire) at the top of my negative column on one of my bus strips. This will collect all of the future negative output wires into one easy to manage flow.

#### Putting in LEDs
The LED lights have a positive leg (the longer leg) and a negative leg (the shorter leg). I set the LED row up with all the positive legs facing in the same direction. Basically, with the board rotated so the bus strip is at the top, I put my LEDs in so their positive leg is on the right hand side and their negative leg is on the left hand side.

I also positioned my row of LEDs with ample space in front of and behind them, for all the rest of my wires.

My breadboard at this stage:

![LEDs and Negative wire]({{ site.url }}/assets/post_img/2014-08/16-ledsandnegative.jpg)

#### Dealing with the ground flow of power
Right now, my LEDs are not connected with my long negative wire. This is gonna change.

For every LED negative leg I plugged in a wire behind. As long as it's in the same row, I understand it should be fine. The other end of those wires I plugged into the negative/ground column on my bus strip. As long as they are plugged in the column beneath the negative wire at the top, the row does not need to line up.

All my negative LED legs are connected with my ground wire now. You'll see I used blue and green cables and alternated colours, which makes it easier to keep track of what is plugged into where.
![Negative wires]({{ site.url }}/assets/post_img/2014-08/16-negativewires.jpg)

#### Actually putting in some power
Right now, there's no negative energy to route out without positive energy.

For every LED positive leg, I plugged a wire in front. As before, as long as it's in the same row, it should be fine. I'm still using different coloured wires as it really helped with my understanding of what is going on.
![Positive wires]({{ site.url }}/assets/post_img/2014-08/16-positives.JPG)

This is actually my finished breadboard. Now I'm ready to bring in the Arduino.

### Arduino microcontrolling my breadboard
The next stage involves actually understanding the different components of my arduino. You can read short descriptions of what exactly everything is on the board itself, but I found it helpful to refer to the [Tech Will Save Us Arduino Cheatsheet][cheatsheet], which has a useful layout diagram.

![Tech Will Save Us's arduino cheatsheet]({{ site.url }}/assets/post_img/2014-08/16-arduinocheatsheet.jpg)

#### Negative to ground
My Long negative wire will be put into the Ground pin, which is labeled as GND on the row of Power pins, which are on the side of my arduino closest to the power input.

#### Positive/Power wires
My positive / power wires will go into my row of Digital pins, which are on the side nearest my USB connection point. This is where I had to start thinking about my code. The wire put into the pin labeled 1 will be referred to by that number in my code. I plugged my wires into pins 1 to 10. This is where it will be very helpful if you've organised things neatly, so it's easier to tell which LED corresponds to which number. As shown:

![Positive wires and corresponding arduino row]({{ site.url }}/assets/post_img/2014-08/16-positiverow.JPG)

#### All connected!
My set up looks like this:

![My arduino breadboard links]({{ site.url }}/assets/post_img/2014-08/16-overview.JPG)
![My arduino breadboard links -side view]({{ site.url }}/assets/post_img/2014-08/16-secondview.JPG)


### Coding!
Finally, to coding. Connect the arduino to your computer with the USB cable, and load up the Arduino IDE. Roi advised being careful about plugging and unplugging the USB cable: both in that you should hold onto the arduino to make sure the soldering doesn't come loose, and that by plugging in the arduino power surges through our breadboard set up. If anythings not right at this point, you're about to find out.

#### Setting up your code environment.
Within the arduino software, you still need to inform your programme about the environment it is going to be used in: the arduino board type and which board.

1. In the top menu, go to Tools, and then Board, and select your board type. In this case, Arduino UNO
* Now it needs to know specifically which board, ie the one that is plugged in. Tools / Serial port. Mine is set to '/dev/tty.usbmodem1421' which I believe is an OSX USB reference. If you are using a different set up, I would advice googling around.


#### Writing the blinking lights program
[My finished code][code] to make a row of lights blink in order can be seen [here][code].

My code is very much based off the example code that arduino provides.

Example code is under **File/Examples/01.Basics/Blink** The code is as follows:

{% highlight c %}
/*
  Blink
  Turns on an LED on for one second, then off for one second, repeatedly.

  This example code is in the public domain.
 */

// Pin 13 has an LED connected on most Arduino boards.
// give it a name:
int led = 13;

// the setup routine runs once when you press reset:
void setup() {
  // initialize the digital pin as an output.
  pinMode(led, OUTPUT);
}

// the loop routine runs over and over again forever:
void loop() {
  digitalWrite(led, HIGH);   // turn the LED on (HIGH is the voltage level)
  delay(1000);               // wait for a second
  digitalWrite(led, LOW);    // turn the LED off by making the voltage LOW
  delay(1000);               // wait for a second
}
{% endhighlight %}

The structure is pretty simple.

{% highlight c %}
int led = 13;
{% endhighlight %}

'int' sets up a variable to be used later on in the code. 13 corresponds to our numbered digital output pins on our arduino.

{% highlight c %}
void setup() {
  // initialize the digital pin as an output.
  pinMode(led, OUTPUT);
}
{% endhighlight %}

The setup function literally 'sets up' our program to know what to do with our variables. Basically, set our 'led' int as an OUTPUT and ensure that it looks for a pin.

{% highlight c %}
void loop() {
  ...
}
{% endhighlight %}

An important thing to remember with our arduino software is that it will always be run in a loop. Therefore, our loop function is the container for all the code that our arduino will run.

{% highlight c %}
digitalWrite(led, HIGH);   // turn the LED on (HIGH is the voltage level)
delay(1000);               // wait for a second
digitalWrite(led, LOW);    // turn the LED off by making the voltage LOW
delay(1000);               // wait for a second
{% endhighlight %}

The rest is explained in arduino's example code above, as it blinks this light on and off. I'm told it's sensible to have a short break before turning a light on and off, so as to not overload the circuit. Obviously the break can vary.

My finished code is basically the following:

{% highlight c %}
int LED01  = 1;
int LED02  = 2;
/* and so on.. */
int LED10  = 10;

void setup(){
	pinMode(LED01, OUTPUT);
	pinMode(LED02, OUTPUT);
	/* and so on.. */
	pinMode(LED10, OUTPUT);
}

void loop(){
	digitalWrite(LED01, HIGH); // 01 on
	delay(250);

	digitalWrite(LED01, LOW); // 01 off
	delay(100);
	digitalWrite(LED02, HIGH); // 02 on
	delay(250);

	/* 02 to 09 is the same block as above,
	 except with the numbers changed, obviously */

	digitalWrite(LED09, LOW); // 09 off (having been turned on in the previous code block)
	delay(100);
	digitalWrite(LED10, HIGH); // 10 on
	delay(250);

	digitalWrite(LED10, LOW); // 10 off
	delay(100); // delay before turning 01 on again at the beginning of the loop.
}
{% endhighlight %}

It's fairly self explanatory.

#### Sending our program to our Arduino
Now I got frustrated with the limitations of the Arduino IDE and had already switched to my favourite Sublime Text to handle this repetitive code. However, once finished, it's important to have the code in the arduino set up.

Mostly for these buttons:

![Verify / Upload / New / Open / Save buttons in arduino IDE]({{ site.url }}/assets/post_img/2014-08/16-IDEbuttons.png)

Verify / Upload / New / Open / Save (As explained when hovered over)

**Verify** is important to check our code will work in our Arduino UNO environment. This will check our code for errors.

**Upload** is the magic button that sends our code to our Arduino. Verify code before sending!

Press upload and you'll see your arduino light up with activity as it processes the code, before settling into the loop.

![My lit up LEDs]({{ site.url }}/assets/post_img/2014-08/16-lights.JPG)

Yay lights! At this point, I could disconnect my computer and connect an alternative power source, either from a USB plug or a power cable, and my arduino would happily continue flashing. It memorises my code.

## Conclusion
As intimidating as the breadboard set up stage was, I am proud that I remembered my electronics when remaking this project for this blog post at the weekend. I've probably  shoddily used electronic technical terms in this post, so apologies to any experts who know better! I look forward to playing with my arduino and circuits in the future, so hopefully I can look back on this post and rewrite it with more confidence.

The majority of Makers Academy was pretty amused by my sheer joy at having pulled off this project. It feels like I've broached an area of coding I didn't think I would be able to.

If you try this, let me know!

Again, massive thanks to [Roi][roi] for talking me through this process.

Advancing on my code: running [2 lights at once][code_2lights]

## Resources
Hardware: [Start Arduino Kit from Technology Will Save Us][startkit]

[Arduino layout cheatsheet][cheatsheet]

[Breadboard layout explained by Wikipedia][breadboardwiki]

Software: [Arduino IDE][software]

Initial code reference: (within Arduino IDE) File/Examples/01.Basics/Blink


[startkit]: http://www.techwillsaveus.com/shop/diy-kits/start-arduino/
[twsu]: http://www.techwillsaveus.com/
[ardof]: http://www.arduino.cc/
[roi]: https://twitter.com/roiDsign
[projects]: http://playground.arduino.cc/projects/ideas
[cheatsheet]: http://techwillsaveus.com/az/wp-content/uploads/2014/02/cheat-sheet-3.pdf
[software]: http://arduino.cc/en/main/software
[breadboardwiki]: http://en.wikipedia.org/wiki/Breadboard
[code]: https://github.com/zoeabryant/arduino-starter-blinking-lights/blob/master/Blink_10pins.ino
[code_2lights]: https://github.com/zoeabryant/arduino-starter-blinking-lights/blob/master/Blink_10pins_ex.ino