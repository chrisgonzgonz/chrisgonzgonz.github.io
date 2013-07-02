---
layout: post
title: "Smart-Kegs"
date: 2013-07-01 23:07
comments: true
categories: 
---
Kegs Should Refill Themselves
------------------------------
We have smart phones and smart cars, why not Smart-Kegs (patent pending)? [Jordán](http://jgtr.github.io/), [Joe](http://weatherlightus.tumblr.com/) and I would like to present to you... Keg Kong! The solution to a tapped keg on a Friday afternoon at The Flatiron School. Keg Kong will re-order himself before the class gets to the bottom of the barrel, and we'll be able to track usage statistics along the way.

{% img center http://i411.photobucket.com/albums/pp199/hccllc2008/1105081524.jpg %}

You can find our team's initial plan in Joe's [post](http://weatherlightus.tumblr.com/post/53232311824/and-the-beer-must-flow). Since then, we've amassed the hardware (raspberry pi, arduino, flow meter), we've programmed the pi/arduino, and we've begun our initial tests.

##Working with hardware is hard...

The last week has taught me to appreciate the beautiful error messages that Ruby, Sinatra, and almost anything software related have to offer. We've been unable to find much documentation on our second-hand flow meter so we've been having fun figuring out how to wire everything together.

A Beautiful and Informative Ruby Error Message:
{% img center http://snag.gy/5EbK3.jpg %}

Jordán Tackling a Flow Meter to Arduino Error Message:
{% img center http://snag.gy/Ie968.jpg %}

##Working with hardware is rewarding...

Our team has spent some evenings working on transmitting an electrical pulse from the flow meter to the arduino to the raspberry pi. We've hypothesized as to why a process may or may not be working and we've broken problems down into ever-smaller components. I'll cover the issues we had and our next steps in a second, but let me just say, I have never high-fived so hard over such incremental progress. 
{% img center http://www.corepower.com/blog/wp-content/uploads/Victory-2.jpg %}

##Working with hardware is rewarding...
Issues so far:
<li>there seemed to be a lack of documentation for related flow meter projects in general, and related projects written in Ruby specifically (we aim to fix this)</li>
<li>correctly connecting flow meter -> arduino -> raspberry pi</li>
<li>capturing flow meter readings</li>
<li>shipping flow meter data to raspberry pi for analysis</li>

The first 3 items on this list were taken care of by sorting out the wiring via guess and check and isolated pulse readings on the arduino. After that, raspberry pi can consume the arduino's output via loops on each machine (arduino printing, pi listening). These loops are not synchronized, so although we are able to pass packets of data along this chain, some packets get cut off.

                                Ruby Loop (Listening):
{%img center http://snag.gy/wl86E.jpg%} 

                              Arduino Loop (Printing):
{%img center http://snag.gy/mzcBe.jpg%}

##2 possible solutions for this data integrity problem:
<li>install a data-logging shield onto the arduino to store data and send in complete packets to be parsed at a later time</li>
<li>install a WiFi shield that connects the arduino wirelessly, and we can send TCP packets to the raspberry pi which we can set up to always be listening via sockets.</li>

More to come as the saga continues!




