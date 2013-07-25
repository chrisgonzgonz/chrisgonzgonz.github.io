---
layout: post
title: "Setting Up a Custom Domain with Octopress / Github Pages"
date: 2013-07-24 09:04
comments: true
categories: 
---
                                             
I set up a blog with Octopress. It's great, but I'd always get really skeptical looks when I'd tell friends and family to read my stuff at [chrisgonzgonz.github.io](http://chrisgonzgonz.github.io). 

To remedy this, I bought a domain name. I had some issues getting it to play nice with my github pages site, so here's a quick n' dirty guide to setting this up:

Please note that this assumes that you've [setup an Octopress blog](http://octopress.org/docs/setup/)

1. Buy your domain name. I picked mine up from [Namecheap](https://www.namecheap.com/) so I'll use screenshots of my setup on their site.

2. Next, set up an A Record of <code> 204.232.175.78 </code> and CNAME of your github pages address, in this case <code>chrisgonzgonz.github.io</code>. This can be done from "All Host Settings" on Namecheap.

{% img center /images/namecheap1 %}

3. Finally, create a file called <code>CNAME</code> *in your blog's source folder.* This part is important- if you're not using Octopress you can put this in your blog's root. Octopress requires that this file be in source so that when you <code>rake generate</code> it can be pushed to master. In your CNAME file, save the name of your new domain:

{% img center /images/namecheap2 %}

That's it, 3 easy steps. This takes about 10 minutes to update, then when you type in codercorral.com, you'll be directed to github at 204.232.175.78, and my blog will be found via the CNAME file.

{% img center /images/namecheap4 %}

Also, Google has a cool [guide to DNS basics](http://support.google.com/a/bin/answer.py?hl=en&answer=48090#K) for those interested in learning more about A Record and CNAME.

