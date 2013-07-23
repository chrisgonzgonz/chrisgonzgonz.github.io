---
layout: post
title: "Smart-Kegs Part II"
date: 2013-07-22 00:38
comments: true
categories:
published: false 
---
It's Alive!!!
-------------
KegKong lives! In [Smart-Kegs Part I](http://chrisgonzgonz.github.io/blog/2013/07/01/smart-kegs-part-i/) we left off with the flowmeter and arduino sending incomplete readings to the raspberry pi with no database persistance. I thought we'd end up taking care of this data integrity problem with either a data-logging shield or a wifi shield. Instead, the fix that brought us to a minimum viable product was actually a lot simpler- we took advantage of a delimiter with ruby's **gets** method, in this case "\r\n" which is the same as "null." 

{% img center /images/delimiter1 %}

Using this and the arduino's serial caching abilities, we made sure to only get complete data and keep out null values.

Great! Next we needed an interface to show off our data. Our weapon of choice here is a Sinatra application with Activerecord. We built two models, keg and measurements. Keg keeps track of vital keg data like type of beer, maximum volume, and whether or not a refill email has been sent. Measurements allows us to capture the volume of each pull in pulses, the change in volume in gallons, and the id of the keg that each measurement belongs to. Keg id is necessary as we will create a new keg to reset each time the beer runs out.

A keg object can check its own volume by subtracting the sum of its measurements from its max volume, and it can send an email requesting reinforcements using the Gmail Sender gem

{% img center /images/kk_folders %}



