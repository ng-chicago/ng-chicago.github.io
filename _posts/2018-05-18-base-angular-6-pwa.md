---
layout: post
title: "Base Angular 6 PWA"
date: 2018-05-18 15:18:54 -0500
categories: Angular
tags: ["Angular PWA",  PWA]
comments: true
description: "Angular 6 PWA With Perfect (almost) Audit Score"
---  
{{ page.description }}  

I wanted a perfect base PWA to use as a starting point for new apps.  
By applying the few extra steps listed below, I was able to get an [almost perfect](#almost) score.  
All very simple.  

![My score]({{ "/assets/posts/2018/2018-05-18-BasePWA.png" | absolute_url }})

## Creation steps

### Create new app with CLI
    ng new BaseAngular6-PWA --routing  
    cd BaseAngular6-PWA  

### Add PWA stuff
    ng add @angular/pwa  

### Make sure it's up to date (double check)
    ng update

### Modify distribution folder in _angular.json_ (personal preference)
	old: "outputPath": "dist/BaseAngular6-PWA",  
	new: "outputPath": "dist",  

## Bump up the Lighthouse score tweaks

### Add noscript tag to _index.html_ page before closing body tag
        <noscript>JavaScript required to view site</noscript>  

### Add description meta data to _index.html_ page
        <meta name="description" content="Base Angular 6 PWA">  
        <meta name="keywords" content="Angular, PWA">  

### Add .htaccess file to root for HTTPS redirect  
[Gist File](https://gist.github.com/ng-chicago/8eeb71f749134983a83b8752a9a29905){:target="_blank"}

### Modify _angular.json_ to include new .htaccess file in build  
	"assets": [
              "src/favicon.ico",
              "src/assets",
              "src/manifest.json",
              "src/.htaccess"
            ],

### Update _manifest.json_ short_name
    "short_name": "Very Short",  

### Build Deploy & Audit Check
    ng build --prod --build-optimizer  
    cd dist  
    Push the entire folder with the tool of your choice to your website  
    Run Chrome Audit to see score

### Push to GitHub
    git status  
    git add -A  
    git commit -m "base app creation"  
    git remote add origin https://github.com/ng-chicago/AngularBasePWA.git  
    git push -u origin master  

### Notes {#almost} 
    My host does not offer HTTP2 - So I was dinged on the Best Practices number 
    Some browser Extensions will slow down things and lower scores  
        (turn them all off while testing)   
        
[GitHub Source](https://github.com/ng-chicago/AngularBasePWA){:target="_blank"}  

  
[running version @ Glitch.Me](https://angularbasepwa.glitch.me/){:target="_blank"}

