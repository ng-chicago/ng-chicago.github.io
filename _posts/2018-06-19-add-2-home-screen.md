---
layout: post
title: "Add To Home Screen (A2HS)"
date: 2018-06-18 07:30:44 -0500
tags: [A2HS, Angular, Chrome, Firefox]
comments: true
description: "A stand alone Angular application for testing A2HS (a work in progress)."
---  
{{ page.description }} For trying to figure out how different browsers handle A2HS.  

Updated Jun 20, 2018
{:.post-meta}

# A2HS for PWAs Is Big #
Getting users to add a home screen shortcut to your [PWA](https://developers.google.com/web/progressive-web-apps/){:target="_blank"} will greatly increase it's use. Since PWAs are relatively new, there is no constancy with how different browsers handle A2HS. It is a moving target.  
<br>
**[Chrome](https://developers.google.com/web/fundamentals/app-install-banners/){:target="_blank"}** and **[Edge](https://blogs.windows.com/msedgedev/2018/02/06/welcoming-progressive-web-apps-edge-windows-10/#0eVsoxrHYlso6vcS.97){:target="_blank"}** have implemented prompts to ask the user if they would like to A2HS. These are great, but they may not display at a good time for the user. As with many random prompts, I would guess they are quickly dismissed. You can add logic to add a button to your app to let the user control the A2HS prompt.  
<br>
**[FireFox](https://developer.mozilla.org/en-US/Apps/Progressive/Add_to_home_screen){:target="_blank"}** adds a A2HS icon/button to the browser address bar for qualifying PWAs. I would guess that almost all users do not know what that icon does. Currently this icon shows even if it has already been used


#### Source Code (still in progress)  ####
[https://github.com/ng-chicago/AddToHomeScreen](https://github.com/ng-chicago/AddToHomeScreen){:target="_blank"}

#### Working Example  ####
[Running on Glitch](https://a2hs.glitch.me/){:target="_blank"}

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
 

#### Manual A2HS  #### 
The browsers below do NOT prompt the user to A2HS, but they do offer a manual option that will then open your PWA in a standalone screen.
 * Opera - Three dots > Home Screen (available for all websites)
 * Firefox - home icon with a plus (+) icon inside it in address bar (qualifying PWA websites only)


#### Listen For Install  #### 
You can listen for when the app is added to the home screen in Chrome & Edge[^2] 

    window.addEventListener('appinstalled', (evt) => {
        // if installed, hide your custom button?
        // if installed, call Google Analytics to track?
    });
  
#### Launched from Home Screen (standalone)  #### 
You can detect if your app was opened from a button on the home screen.[^3]   
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
 * Test what happens if prompt is placed in local storage

#### Random Notes  ####
 * -- Clearing browsing data in Edge sometimes does not stop spinning? (06/19/2018)<br><br>
 * -- If you open the app from the Chrome Desktop apps screen, it may open a standalone window, but not give focus to that window (Mac Chrome). You can access the app from the new icon in the dock.<br><br>
 * -- The Prompt could be shown multiple times after rejection in desktop Chrome. It CANNOT be shown after rejection in mobile Chrome, Edge.
 * -- If you open a PWA site in the twitter "browser" window, and even then "open in browser" it may not properly prompt A2HS. Looks like you may have to open the site directly in the browser?

#### Reference Articles  ####
[Chrome 68 snack-bar ignores preventDefault()](https://developers.google.com/web/updates/2018/06/a2hs-updates){:target="_blank"}

[Google Chrome installs a WebAPK](https://developers.google.com/web/fundamentals/integration/webapks){:target="_blank"}

#### Footnotes  ####

[^1]: There are TWO versions of the Lighthouse audit tool: The one built into the developer tools AND a [Chrome extension](https://chrome.google.com/webstore/detail/lighthouse/blipmdconlkpinefehnmjammfjpmpbjk){:target="_blank"} which usually has more recent features.

[^2]: Edge has a second dialog to set the icon where you want on the screen. If the user selects CANCEL here, you may falsely think it was installed if only listening to the first dialog. [I'm not sure yet how to listen to the second dialog.](https://stackoverflow.com/questions/50932302/is-there-a-listener-available-for-the-2nd-add-to-home-screen-dialog-in-edge-an){:target="_blank"}

[^3]: Last tested using Android 8.1.0 on 06/20/2018.




