---
layout: post
title: "Google Sheets As A JSON Data Source"
date: 2018-05-07 08:06:15 -0500
categories: "Data Source"
tags: ["Google Sheets",  JSON]
comments: true
description: "When you need a JSON data source that is VERY simple for users to maintain, consider using a Google Sheet."
---
{{ page.description }}  
* my toc
{:toc}  
### Google Sheets Setup ###
if you have already published sheet, [skip down to next step](#JSONUrls). 
#### Create ####
#### Publish ####

### Determining The Tabs JSON URLs  ### {#JSONUrls}
 
Spreadsheet ID
1jgwyJCeftwM8FYnOa2ISxtwRzPsatECYJxN2u7G7cDQ

--// the published spreadsheet (uneditable)
--// may take 5 minutes to show updates
https://docs.google.com/spreadsheets/d/1jgwyJCeftwM8FYnOa2ISxtwRzPsatECYJxN2u7G7cDQ/pubhtml

--// the modified date - will be updated if anything changed on any tab
feed.updated.$t      e.g."2013-01-16T21:41:33.980Z"

--// 01 get the list of all tabs as json
https://spreadsheets.google.com/feeds/worksheets/1jgwyJCeftwM8FYnOa2ISxtwRzPsatECYJxN2u7G7cDQ/public/full?alt=

--// 02 IF SUCCESSFUL, check last update date
If the date for this tab has not changed from what we saved last, we COULD used cached data

--// 03 loop through the list for each tab
https://spreadsheets.google.com/feeds/list/1jgwyJCeftwM8FYnOa2ISxtwRzPsatECYJxN2u7G7cDQ/od6/public/full?alt=json

Notes:
01. When tabs are moved or renamed, they retain the same ID (GOOD)
02. There does seem to be a date when the spreadsheet was last modified??

--// public google sheet (old v1)
https://docs.google.com/spreadsheets/d/1NTsK79KXNVPOjCz3TGnFvoNgwvJj8b7Jcs9gtnmoBZ0/pubhtml

--// public json (one tab)
--// change number before public to get each sheet (1-6)
https://spreadsheets.google.com/feeds/list/1jgwyJCeftwM8FYnOa2ISxtwRzPsatECYJxN2u7G7cDQ/1/public/values?alt=json

--// public json all the tabs
--// loop through this to get the data for each individual tab
https://spreadsheets.google.com/feeds/worksheets/1jgwyJCeftwM8FYnOa2ISxtwRzPsatECYJxN2u7G7cDQ/public/full?alt=json



----------------- spreadsheet JSON Values START
Open Google URL in Firefox to get formatted JSON
Note: attributes are all lower case


