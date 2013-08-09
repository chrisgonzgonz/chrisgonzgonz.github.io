---
layout: post
title: "Smart-Kegs Part II"
date: 2013-08-09 07:43
comments: true
categories: 
---
It's Alive!!! (Locally)
-------------
KegKong lives! In [Smart-Kegs Part I](http://chrisgonzgonz.github.io/blog/2013/07/01/smart-kegs-part-i/) we left off with our flowmeter and arduino sending incomplete readings to the raspberry pi with no database persistance. I thought we'd take care of this data integrity problem with either a data-logging shield or a wifi shield. Instead, the fix that brought us to a minimum viable product was actually a lot simpler- we took advantage of a delimiter with ruby's **gets** method, in this case "\r\n" which is the same as **null**. 

{% img left /images/delimiter1 %}
{% img right /images/kk_folders %}

Using this and the arduino's serial caching abilities, we made sure to only transfer only complete data to the raspberry pi and remove null values.

Great! Next we needed an interface to show off our data. Our weapon of choice here is a light-weight Sinatra application with Activerecord. We built two models, keg and measurements. Keg keeps track of vital keg data like type of beer, maximum volume, and whether or not a refill request has been sent. Measurements allows us to capture the volume of each pull in pulses, the corresponding change in volume in gallons, and the id of the keg that each measurement belongs to. The measurement/keg id relationship is necessary as we will create a new keg in order to "reset" each time the beer runs out.

A keg object can check its own volume by subtracting the sum of its measurements from its max volume, and it can send an email requesting reinforcements using the Gmail Sender gem.

{% img center /images/kegkong2_1 %}

Here I'll leave you with KegKong fully functioning locally. In **Smart-Kegs Part III**, I'll go over all the fun we had with deployment to Heroku, changing our scripted method of persistance and migrating our SQLite database to PostgreSQL.

{% img center /images/kegkong2_2 %}
{% img center /images/kegkong2_reset %}





