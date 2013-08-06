---
layout: post
title: "Scraping Wikipedia Using Nokogiri and Google Search"
date: 2013-08-05 19:55
comments: true
categories: 
---
The Problem:
------------
I needed to write a method for an application that would take a famous programmer's name and scrape the related Wikipedia page for relevant resources, the most important of which would be a picture.

Nokogiri can scrape a page when passed a url, but how could I ensure that the name passed would translate directly into a valid url? Or even that the name would be spelled correctly? As it turns out, Google can do the heavy lifting and point us directly to the desired page for scrapin'.

The Solution:
-------------
The solution is what I'll call a 'double-scrape'. The first thing I did was create my query string by substituting blank spaces in the programmer's name for '+' and adding '+wikipedia' to the end of the query, all to ensure that the first result would be the wikipedia page related to the programmer's name.

Next we get the Google search result page for this query string, which Nokogiri scrapes to turn the first result in the list (which should be the Wikipedia article) into the url for the programmer's wikipedia page. Scrape n' repeat.

{% img center /images/noko1 %}

Postscript
----------
While I'm still testing this solution out, I have to say it seems pretty robust. The evidence lies in our seed data, where one Programmer of the Day was listed as 'Cookie Monster.'

{% img center /images/noko2 %}