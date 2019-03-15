---
layout: post
title: "Web Push Notifications - Part 1"
date: 2019-03-20 07:30:44 -0500
tags: [Angular, Chrome, Firefox, 'Push API']
comments: true
description: "Adding push notifications to an Angular PWA."  
---  
{{ page.description }} Creating Opt-In Push Notifications.  

Last Updated March 20, 2019
{:.post-meta}

# Most notification requests are ANNOYING #
Getting users to add a home screen shortcut to your [PWA](https://developers.google.com/web/progressive-web-apps/){:target="_blank"} will greatly increase it's use. Since PWAs are relatively new, there is no constancy with how different browsers handle A2HS. It is a moving target.  
<br>
**[Chrome](https://developers.google.com/web/fundamentals/app-install-banners/){:target="_blank"}** and **[Edge](https://blogs.windows.com/msedgedev/2018/02/06/welcoming-progressive-web-apps-edge-windows-10/#0eVsoxrHYlso6vcS.97){:target="_blank"}** have implemented prompts to ask the user if they would like to A2HS. These are great, but they may not display at a good time for the user. As with many random prompts, I would guess they are quickly dismissed. You can add logic to add a button to your app to let the user control the A2HS prompt.  
<br>
**[FireFox](https://developer.mozilla.org/en-US/Apps/Progressive/Add_to_home_screen){:target="_blank"}** adds a A2HS icon/button to the browser address bar for qualifying PWAs. Currently this icon shows even if it has already been used. 


<br>
**[Push api vs Web Notifications.](https://stackoverflow.com/questions/34844561/difference-between-notifications-api-and-push-api-from-web-perspective){:target="_blank"}** 






#### Source Code (still in progress)  ####
[https://github.com/ng-chicago/AddToHomeScreen](https://github.com/ng-chicago/AddToHomeScreen){:target="_blank"}

#### Working Example  ####
[Running on Glitch (https://a2hs.glitch.me/)](https://a2hs.glitch.me/){:target="_blank"}  
If you type manually, make sure to include http**s**://

#### Functionality (Chrome & Edge)  ####

 * -- Prevents browser from displaying A2HS dialog when all criteria are met.
 * -- Displays user controlled button to open browser A2HS dialog.
 * -- Displays debug section if A2HS prompt was intercepted & saved. This makes mobile device testing easier.


#### Will My PWA Generate an A2HS Prompt?  ####
You can use the one of the Chrome Lighthouse audit tools [^1] to tell you if the prompt will be shown for your PWA.  
 * > Run the **Progressive Web App** audit
 * > Under Passed Audits, you should see **[User can be prompted to Install the Web App]( https://developers.google.com/web/tools/lighthouse/audits/install-prompt){:target="_blank"}**
 * > If you see the above message AND you have cleared out previous installs AND browser cache for your website, you will get the prompt in browsers that support it.
 * > **Note**: Some browsers may have an engagement heuristic that requires you visit the site for a period of time before the prompt shows.
 * > Here are the [Chrome criteria](https://developers.google.com/web/fundamentals/app-install-banners/#criteria){:target="_blank"}
 
 

#### Create Your Own A2HS Button (Chrome & Edge)  #### 
In these two browsers, if your PWA meets the, users will be prompted to add a home screen shortcut. The prompt may not show at the best time.  
You can:  
 * Listen for the prompt and stop it before it shows  
 * Save it and show a button to let the user control the timing of the prompt  
 * Show saved prompt (only once) when the user clicks on the button  

---
    window.addEventListener('beforeinstallprompt', (e) => {    
        // show your custom button
        
        // Prevent Chrome 67 and earlier from automatically showing the prompt
        // no matter what, the snack-bar shows in 68 (beta 06/16/2018 11:05 AM)
        e.preventDefault();
        
        // Save the prompt so it can be displayed when the user wants
        this.deferredPrompt = e;    
    }); 


#### Manual A2HS iOS & Safari (Sample code working) #### 
There is no prompt for A2HS, but there is a manual option.  
When added to the Home Screen:  
 * iOS 11+ will open PWA as a Standalone window.  
 * Earlier versions of iOS & Safari will most likely open in the normal Safari window.
 * iOS 9 or earlier versions may not show the A2HS button

Most users probably do not know it is there, but you can add instructions for when users are in iOS Safari.


1. Share button
       <img height="22" alt="Share Button Image" src="data:image/svg+xml;base64,PHN2ZyBpZD0iTGF5ZXJfMiIgZGF0YS1uYW1lPSJMYXllciAyIiB4bWxucz0iaHR0cDovL3d3dy5
   3My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyMC44OCAyNy4yNSI+PGRlZnM+PHN0eWxlPi
   5jbHMtMXtmaWxsOm5vbmU7c3Ryb2tlOiMyMzFmMjA7fTwvc3R5bGU+PC9kZWZzPjx0aXRsZT5TY
   WZhcmlfU2hhcmU8L3RpdGxlPjxwb2x5bGluZSBjbGFzcz0iY2xzLTEiIHBvaW50cz0iMTMuMTMg
   OCAyMC4zOCA4IDIwLjM4IDI2Ljc1IDAuNSAyNi43NSAwLjUgOCA3LjUgOCIvPjxsaW5lIGNsYXN
   zPSJjbHMtMSIgeDE9IjEwLjQ0IiB5MT0iMTciIHgyPSIxMC40NCIvPjxsaW5lIGNsYXNzPSJjbH
   MtMSIgeDE9IjEwLjQ4IiB5MT0iMC4zOCIgeDI9IjE1LjI4IiB5Mj0iNS4xOCIvPjxsaW5lIGNsY
   XNzPSJjbHMtMSIgeDE9IjEwLjQ0IiB5MT0iMC4zOCIgeDI9IjUuNjQiIHkyPSI1LjE4Ii8+PC9z
   dmc+"> at the (top or bottom) of the browser 
2. Scroll (if needed) to find the Add to Home Screen button
       <img height="22" alt="Add to Home Screen button Image" src="data:image/svg+xml;base64,PHN2ZyBpZD0iTGF5ZXJfMiIgZGF0YS1uYW1lPSJMYXllciAyIiB4bWxucz0iaHR0cDovL3d3dy5
   3My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAzNSAzNSI+PHRpdGxlPlNhZmFyaV9BMkhTPC
   90aXRsZT48cmVjdCB3aWR0aD0iMzUiIGhlaWdodD0iMzUiIHJ4PSI4IiByeT0iOCIgc3R5bGU9I
   mZpbGw6IzhmOGY4ZiIvPjxsaW5lIHgxPSIyNC43NSIgeTE9IjE3LjUiIHgyPSIxMC4yNSIgeTI9
   IjE3LjUiIHN0eWxlPSJmaWxsOm5vbmU7c3Ryb2tlOiNmZmY7c3Ryb2tlLXdpZHRoOjJweCIvPjx
   saW5lIHgxPSIxNy41IiB5MT0iMTAuMjUiIHgyPSIxNy41IiB5Mj0iMjQuNzUiIHN0eWxlPSJmaW
   xsOm5vbmU7c3Ryb2tlOiNmZmY7c3Ryb2tlLXdpZHRoOjJweCIvPjwvc3ZnPg==">  
   
**Show these instructions if:**
 * Safari & iOS & Not Standalone
 * Users of older versions (< 13% ) will still see this message even if they installed.  
 iOS 10 (8.04%) iOS 11 (86.74%) as of: 07/05/2018

**Note**  
You will need to add Icons for iOS
It currently does not use the Manifest Icons

        <!-- place this in a head section -->
        <link rel="apple-touch-icon" href="/assets/touch-icon-iphone.png">
        <link rel="apple-touch-icon" sizes="152x152" href="/assets/touch-icon-ipad.png">
        <link rel="apple-touch-icon" sizes="180x180" href="/assets/touch-icon-iphone-retina.png">
        <link rel="apple-touch-icon" sizes="167x167" href="touch-icon-ipad-retina.png">

And images for the iOS standalone splash screens
If you do not add these, a plain white screen will be shown until the load is complete

        <!-- place this in a head section -->
          <meta name="apple-mobile-web-app-capable" content="yes">
          <meta name="apple-mobile-web-app-status-bar-style" content="#ffffff">
          <meta name="apple-mobile-web-app-title" content="A2HS Test">
          <link rel="apple-touch-startup-image" href="assets/splash/apple_splash_640.png" media="(device-width: 320px) and (device-height: 568px) and (-webkit-device-pixel-ratio: 2) and (orientation: portrait)">
          <link rel="apple-touch-startup-image" href="assets/splash/apple_splash_750.png" media="(device-width: 375px) and (device-height: 667px) and (-webkit-device-pixel-ratio: 2) and (orientation: portrait)">
          <link rel="apple-touch-startup-image" href="assets/splash/apple_splash_1242.png" media="(device-width: 414px) and (device-height: 736px) and (-webkit-device-pixel-ratio: 3) and (orientation: portrait)">
          <link rel="apple-touch-startup-image" href="assets/splash/apple_splash_1125.png" media="(device-width: 375px) and (device-height: 812px) and (-webkit-device-pixel-ratio: 3) and (orientation: portrait)">
          <link rel="apple-touch-startup-image" href="assets/splash/apple_splash_1536.png" media="(min-device-width: 768px) and (max-device-width: 1024px) and (-webkit-min-device-pixel-ratio: 2) and (orientation: portrait)">
          <link rel="apple-touch-startup-image" href="assets/splash/apple_splash_1668.png" media="(min-device-width: 834px) and (max-device-width: 834px) and (-webkit-min-device-pixel-ratio: 2) and (orientation: portrait)">
          <link rel="apple-touch-startup-image" href="assets/splash/apple_splash_2048.png" media="(min-device-width: 1024px) and (max-device-width: 1024px) and (-webkit-min-device-pixel-ratio: 2) and (orientation: portrait)">


#### Listen For Install  #### 
You can listen for when the app is added to the home screen in Chrome & Edge[^2] 

    window.addEventListener('appinstalled', (evt) => {
        // if installed, hide your custom button?
        // if installed, call Google Analytics to track?
    });
  
#### Standalone Detection (see grid below)  #### 
    
**In your CSS**  

        @media all and (display-mode: standalone) {
          body {
            background-color: yellow;
            border: 1px solid black;
          }
        }

<strong>In your code</strong>  

        if (window.matchMedia('(display-mode: standalone)').matches) {
          // do things here
          // e.g. call Google Analytics to track standalone use 
        }


#### Next Steps  #### 
 * Add logic to detect browser & version?
 * Test what happens if prompt is placed in local storage

#### Random Notes ####
 * -- Clearing browsing data in Edge sometimes does not stop spinning? (06/19/2018)<br><br>
 * -- If you open the app from the Chrome Desktop apps screen, it may open a standalone window, but not give focus to that window (Mac Chrome). You can access the app from the new icon in the dock.<br><br>
 * -- The Prompt could be shown multiple times after rejection in desktop Chrome. It CANNOT be shown after rejection in mobile Chrome, Edge.<br><br>
 * -- If you open a PWA site in the twitter "browser" window, and even then "open in browser" (chrome), it may not properly prompt A2HS. Looks like you may have to open the site directly in the browser?
  * -- Depending on the version of Desktop Chrome you are using, you may need to turn on A2HS Here (chrome://flags/#enable-desktop-pwas)
 

 
#### Goofiness ####
  * If you FIRST install the WebAPK with Chrome, the prompt will NOT be shown in Edge. They will be fixing this soon.
 

#### Reference Articles I Like  ####
[Chrome 68 snack-bar ignores preventDefault()](https://developers.google.com/web/updates/2018/06/a2hs-updates){:target="_blank"}  

[Google Chrome installs a WebAPK](https://developers.google.com/web/fundamentals/integration/webapks){:target="_blank"}  

[PWAs on iOS](https://www.netguru.co/codestories/few-tips-that-will-make-your-pwa-on-ios-feel-like-native){:target="_blank"}  

[iOS Splash Screens - This works (mostly?)](https://medium.com/@applification/progressive-web-app-splash-screens-80340b45d210){:target="_blank"}  

[Progressive Web App Splash Screens](https://medium.com/@applification/progressive-web-app-splash-screens-80340b45d210){:target="_blank"}  



#### A2HS OS & Browser Combos Coded/Tested So Far ####

| Combo         | A2HS Type   | Notes  | Standalone  |
| ------------- |:-------------|:-----|:-----|
| Android 8.10<br>Chrome 67 | Prompt Intercepted<br>Custom btn shown | WebApk Installed | Detected<br>Custom btn hidden | 
| Android 8.10<br>Chrome 68 (beta) | Prompt Intercepted<br>Custom btn shown | WebApk Installed<br>[See temp snack-bar note here](https://developers.google.com/web/updates/2018/06/a2hs-updates){:target="_blank"}  | Detected<br>Custom btn  hidden | 
| Android 8.10<br>Edge 42 | Prompt Intercepted<br>Custom btn shown | Shortcut added | Detected<br>Custom btn hidden | 
| iOS 11.4<br>Safari<br>(simulator)    | Manual how to shown     | Shortcut added<br>[Extra work needed for iOS icons & Splash Screens](https://www.netguru.co/codestories/few-tips-that-will-make-your-pwa-on-ios-feel-like-native){:target="_blank"} | Detected<br>How to  hidden |   
| iOS 9.3.5<br>Safari<br>(iPod)     | Manual how to shown | Shortcut added |  &#10060;Semi-standalone?<br>Not detected,<br>not Safari<br>How to hidden |  
| iOS 9.3.5<br>Chrome 63<br>(iPod)     | Manual how to shown     | &#10060;No A2HS option available | n/a |   
| Android 8.10<br>Firefox 61     | Manual how to shown     | Shortcut added |  &#10060;No standalone<br> &#10060;How to shows |   
| Android 8.10<br>Firefox 62 (beta)     | Manual how to shown     | Shortcut added | Detected<br>How to  hidden |  
| Android 8.10<br>Opera 43 | &#10060;**Need to add<br>how to code** | Shortcut added | Detected<br>How to  hidden |  


#### To Do - Add code to show these instructions.  #### 
 * Opera - Three dots > Home Screen (available for all websites)
 * Firefox -"home" icon with a plus (+) icon inside it in address bar (qualifying PWA websites only)



#### Footnotes  ####

[^1]: There are TWO versions of the Lighthouse audit tool: The one built into the developer tools AND a [Chrome extension](https://chrome.google.com/webstore/detail/lighthouse/blipmdconlkpinefehnmjammfjpmpbjk){:target="_blank"} which usually has the more recent features.

[^2]: Edge has a second dialog to set the icon where you want on the screen. If the user selects CANCEL here, you may falsely think it was installed if only listening to the first dialog. [I'm not sure yet how to listen to the second dialog.](https://stackoverflow.com/questions/50932302/is-there-a-listener-available-for-the-2nd-add-to-home-screen-dialog-in-edge-an){:target="_blank"}

[^3]: Last tested using Android 8.1.0 on 06/20/2018.


## App Creation steps  ## 
#### Clone an existing blank PWA  ####  
I'm using an empty base verified Angular 7 PWA so I don't have to repeat the same basic steps again.  

**At GitHub Site**  
Create new empty repository *WebNotificationsPart1*

**In Terminal Window (mac)**

    mkdir WebNotificationsPart1
    cd WebNotificationsPart1
    git clone https://github.com/ng-chicago/AngularBasePWA.git .
    git remote set-url origin https://github.com/ng-chicago/WebNotificationsPart1.git
    git push -u origin master
    npm install

**Just in case, run** 

    ng update
