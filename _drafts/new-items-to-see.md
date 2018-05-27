---
layout: post
title: "New Items To See"
date: 2018-05-21 06:21:51 -0500
categories: category1 category2
tags: ["Two Words",  Angular]
comments: true
description: "POST SUMMARY FOR TWITTER CARD"
---  
{{ page.description }}  
* my toc
{:toc}  
### Heading ###
Blah blah blah, [skip down to next heading](#JumpHere). 
#### Sub Heading 1 ####
#### Sub Heading 2 ####

The rest of the more detailed post here

### Some Other Heading  ### {#JumpHere}

The file name
<!-- 2018-05-21-new-items-to-see.md -->




## Creation steps

### Clone My Base GitHub PWA App
    create new GitHub repository NewItemsToSee
    mkdir NewItemsToSee
    cd NewItemsToSee
    git clone https://github.com/ng-chicago/AngularBasePWA.git .    
    git remote set-url origin https://github.com/ng-chicago/NewItemsToSee.git
    git push -u origin master  

### Get Dependencies
    npm install

### Make sure it's up to date (double check)
    ng update
 

### Build Deploy & Audit Check
    ng build --prod --build-optimizer  
    cd dist  
    Push the entire folder with the tool of your choice to your website  
    Run Chrome Audit to see score

