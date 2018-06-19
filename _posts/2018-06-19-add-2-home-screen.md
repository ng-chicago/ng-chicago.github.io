---
layout: post
title: "Add To Home Screen (A2HS)"
date: 2018-06-18 07:30:44 -0500
tags: [A2HS, Angular, Chrome, Firefox]
comments: true
description: "A stand alone Angular application for testing A2HS (a work in progress)."
---  
{{ page.description }} Also good for trying to figure out how different browsers handle A2HS.  
<br/>  

# A2HS Is Big #
Getting your users to add a home screen shortcut to your PWA will greatly increase the times a user visits.
Unfortunately there is currently no constancy with how different browsers handle A2HS. It is a moving target.  
<br>
#### Source Code (still in progress)  ####
[https://github.com/ng-chicago/AddToHomeScreen](https://github.com/ng-chicago/AddToHomeScreen){:target="_blank"}


#### Clear Your Browser To Test  #### 
[See How To Use It](https://github.com/ng-chicago/AddToHomeScreen/blob/master/README.md){:target="_blank"}




#### Create Your Own A2HS Button (Chrome & Edge)  #### 
In these two browsers, if your PWA meets the [criteria](https://developers.google.com/web/fundamentals/app-install-banners/#criteria){:target="_blank"}, users will be prompted to add a home screen shortcut. The prompt may not show at the best time.  
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
 

#### Listen For Install  #### 
You can listen for when the app is added to the home screen in Chrome & Edge[^1] 

    window.addEventListener('appinstalled', (evt) => {
        // if installed, hide your custom button?
        // if installed, call Google Analytics to track?
    });
  
#### Launched from Home Screen (standalone)  #### 
You can detect if your app was opened from a button on the home screen.[^2]   
Works with these mostly mobile browsers:
 * Chrome 67.0.3396.87
 * Chrome beta 68.0.3440.23
 * Firefox 60.0.2
 * <s>Firefox beta 61.0b13 - DOES NOT WORK</s>
 * Opera 46.3.2246.127744
 * Edge 42.0.0.2033
 * Desktop Chrome 67.0.3396.87
 * <s>Desktop Chrome 69.0.3464.0 canary - DOES NOT WORK</s>
    
<strong>In your CSS</strong>  

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

#### Random Notes  ####
 * -- Clearing browsing data in Edge sometimes does not stop spinning? (06/19/2018)<br><br>
 * -- If you open the app from the Chrome Desktop apps screen, it may open a standalone window, but not give focus to that window (Mac Chrome). You can access the app from the new icon in the dock.<br><br>

#### Reference Articles  ####
[Chrome 68 snack-bar ignores preventDefault()](https://developers.google.com/web/updates/2018/06/a2hs-updates){:target="_blank"}

[Google Chrome installs a WebAPK](https://developers.google.com/web/fundamentals/integration/webapks){:target="_blank"}

#### Footnotes  ####
[^1]: Edge has a second dialog to set the icon where you want on the screen. If the user selects CANCEL here, you may falsely think it was installed if only listening to the first dialog. [I'm not sure yet how to listen to the second dialog.](https://stackoverflow.com/questions/50932302/is-there-a-listener-available-for-the-2nd-add-to-home-screen-dialog-in-edge-an){:target="_blank"}
[^2]: Last tested using Android 8.1.0 on 06/18/2018.
