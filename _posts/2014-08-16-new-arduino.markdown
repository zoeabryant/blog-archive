---
layout: post
title:  "Can I play with my Arduino now?"
date:   2014-08-16 12:43:54
tags:
- arduino
- how to
---
For my birthday this week I finally got organised on ordering myself an arduino. Specifically, A [Start Arduino Kit][startkit] from [Technology Will Save Us][twsu], a London company that does some pretty cool things for tech education.

Now I can't exactly say I know much about electronics. In fact, talk of circuits, LEDs and wires gives me flashbacks to year 6, and I'm pretty sure I've taken some more science lessons since then. This wasn't enough to put me off. Thankfully, I am in a place where I am surrounded by techy people who get excited about this kind of stuff too, so I was able to enlist the help of [Roi][roi], a Makers Academy coach, who could walk me through the basics.

### So what exactly is an arduino?
An [Arduino][ardof] is a **microcontroller**. It can be used to respond to its surroundings - detect light level, if the device is being tilted, air pressure, that kind of thing. It can be used to respond to input, set it up with a button to create a game. There are so many [projects][projects] that can be done with it, I wasn't really sure where to begin. So I went for a cliche - making lights blink.

## Project: Making a row of LEDS blink
'Hello World' is a computer programming cliche. Making an LED blink seems to be the physical substitute.

### You will need:
* Arduino (I have an UNO one)
* Breadboard
* USB A-B Cable to connect the arduino to the computer
* LEDs
* Cables. 2 per LED, and 1 extra (I have 21 wires for 10 lights)
* [Arduino IDE Software][software]

### Steps
* Longest wire goes at the top of the negative column on the edge of the breadboard
* Put the LEDs in. Put them in the middle row, so there is space in the columns behind and infront of them. Longest leg faces away from the wire at the top of the negative col.
* Behind each of the shorter legs, the negative legs, put a wire in the next slot in the same row.
* These wires plug into the negative column, in any row as long as they are in the negative col.
* The rest of the wires are for the positive legs.
* Arduino in!
* Long Negative wire to GND (ground)
* USB plug in

* Tools: Board: Arduino UNO
* Tools: Serial Port: /dev/tty.usbmodem1421
* ^^ why this setting?
* Write code
* Verify, Upload


![Tech Will Save Us's arduino cheatsheet]({{ site.url }}/assets/post_img/2014-08/16-arduinocheatsheet.jpg)
[Tech Will Save Us Arduino Cheatsheet][cheatsheet]


[startkit]: http://www.techwillsaveus.com/shop/diy-kits/start-arduino/
[twsu]: http://www.techwillsaveus.com/
[ardof]: http://www.arduino.cc/
[roi]: https://twitter.com/roiDsign
[projects]: http://playground.arduino.cc/projects/ideas
[cheatsheet]: http://techwillsaveus.com/az/wp-content/uploads/2014/02/cheat-sheet-3.pdf
[software]: http://arduino.cc/en/main/software