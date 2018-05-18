---
layout: post
title: "Angular Update 5.2.9 to 6.0.1"
date:  2018-05-18 11:44:28 -0500
categories: Angular
tags: [Angular]
comments: true
description: "Q: How hard is an upgrade to Angular 6?"
---  
{{ page.description }}  

A: Almost painless.

Just a few import changes for RxJs really.

I had the luxury of time and it was a simple app (< 20 components), so I generated a new application with the cli and copy/pasted in the code one component at a time.  
Yes, I realize this was not necessary, but I wanted to start clean and refresh myself on all of the components I added to the original app over a period of months.

After each component was done I tested it with the chrome audit tools to see the effect of each component.

It's nice to start fresh.