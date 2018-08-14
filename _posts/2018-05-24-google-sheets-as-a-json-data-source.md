---
layout: post
title: "Google Sheets as a JSON data source"
date: 2018-05-24 08:06:15 -0500
categories: "Data Source"
tags: ["Google Sheets",  JSON]
comments: true
description: "When you need a read-only JSON data source that is very simple for users to maintain, consider using a Google Sheet."
---
{{ page.description }} It's not very obvious that you can get JSON from a sheet, but it can be done in 4 steps.  
<br/>
### 1. Get the ID of your sheet  
The long number seen in the URL <ins>while you are editing</ins>  
e.g.  
_https://docs.google.com/spreadsheets/d/**1bPW98SzQ5SRsincyVGdP3ctM8ey3oSpncnyo9ASFUDM**/edit#gid=0_  
yourSheetID = _**1bPW98SzQ5SRsincyVGdP3ctM8ey3oSpncnyo9ASFUDM**_  
(this is the ID for my sheet, not yours)  
<br/>
### 2. Publish your sheet as a web page  
    File > Publish to the web...  
    
The default options are fine.
<div style="border: 1px solid black; margin-left: 60px; width: 455px;"  markdown="1">
![screenshot]({{ "/assets/posts/2018/2018-05-24-PublishToWeb.png" | absolute_url }}){:height="400 px"}
</div>
Check the [link created when published](https://docs.google.com/spreadsheets/d/e/2PACX-1vSVEF9lRqjxyXbTqQ4rmXJSJK9mrTZ5UnEcCVnTcGAa7g-vPjmkSPQCMWWMY6JNBMD8U8db4VEN7i1-/pubhtml){:target="_blank"} to view your sheet as read-only.  
<br/>
### 3. Get the ID(s) for the desired tab(s)
Manually build a URL with the following pieces
https://spreadsheets.google.com/feeds/worksheets/{yourSheetID}/public/full?alt=json  
That will give you [JSON like this](https://spreadsheets.google.com/feeds/worksheets/1bPW98SzQ5SRsincyVGdP3ctM8ey3oSpncnyo9ASFUDM/public/full?alt=json){:target="_blank"} which contains an ID for each tab in your sheet

The ID for each of the tabs can be found after the final slash in these values  

        feed.entry[0].id.$t
        feed.entry[1].id.$t
        feed.entry[3].id.$t
        etc.
        the IDs for my 4 tabs
            omyavzt (Dogs)
            o9ws5hl (Cats)
            od6 (AllOthers)
            o97vx72 (Notes)

<div style="border: 1px solid black; margin-left: 60px; width: 455px;"  markdown="1">
![screenshot]({{ "/assets/posts/2018/2018-05-24-FirefoxJSON.png" | absolute_url }}){:height="400 px"}
</div>
Tip: The JSON will be formatted pretty if you view it in FireFox.  
<br/>
### 4. A JSON link <ins>for EACH tab</ins>
Manually build a URL with the following pieces
https://spreadsheets.google.com/feeds/list/{yourSheetID}/{yourTabID}/public/full?alt=json  
That will give you [JSON like this](https://spreadsheets.google.com/feeds/list/1bPW98SzQ5SRsincyVGdP3ctM8ey3oSpncnyo9ASFUDM/omyavzt/public/full?alt=json){:target="_blank"} for the Dogs tab which contains the data in one tab.  
[Cats tab](https://spreadsheets.google.com/feeds/list/1bPW98SzQ5SRsincyVGdP3ctM8ey3oSpncnyo9ASFUDM/o9ws5hl/public/full?alt=json){:target="_blank"}  
[AllOthers tab](https://spreadsheets.google.com/feeds/list/1bPW98SzQ5SRsincyVGdP3ctM8ey3oSpncnyo9ASFUDM/od6/public/full?alt=json){:target="_blank"}  
<br/><br/>
### Notes
1. It may take up to 5 minutes to see published changes made in the sheet. Usually happens in a few seconds.   
2. The IDs for the sheet & tabs never changes. Even if they are renamed.  
3. Somehow it's smart enough to know the first row is the header.  
        (I used: *view > freeze > 1 row* on the first row )  
4. Any data under the first empty row will not show in the JSON.  
5. feed.entry will always contain a record for each row in your tab.  
6. If the user renames a header, that MAY cause issues if you go after attributes by name.  
7. JSON attributes are all lower case & case sensitive. No matter what case you use in your sheet.  
8. The email you use to log into Google will be exposed in the JSON.  
9. If you will be using this source for high volume, I do not know if there are use limits.

<!-- Sheet edited in Firefox Developer Edition logged in as Demos@ng-Chicago.com -->
<!-- https://docs.google.com/spreadsheets/d/1bPW98SzQ5SRsincyVGdP3ctM8ey3oSpncnyo9ASFUDM/edit#gid=0 -->


