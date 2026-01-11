---
id: 65ac4ceb0e7c79000119ac02
title: Applescript to import articles into devonthink pro and del.icio.us from incoming NetNewsWire RSS streams
feature_image:
description: The applescript in this post will take the currently selected headline or tabbed article in NetNewsWire, prompt the user for tags about the…
date: 2007-07-31
full-date: 2007-08-01T02:50:03.000Z
tags:
  - posts
slug: applescript-to-import-articles-into-devonthink-pro-and-del-icio-us-from-incoming-netnewswire-rss-streams
type: post
draft: true
---

The applescript in this post will take the currently selected headline or tabbed article in NetNewsWire, prompt the user for tags about the article, and then create an HTML copy of the article in DEVONThink in a sub group.

If the first tag is not the word “private” then the link is also posted, via [cocoalicious](http://www.scifihifi.com/cocoalicious/), to my [del.icio.us account](http://del.icio.us/davidnunez).

This was based on my [prior script](http://davidnunezdev.wpengine.com/2007/03/24/applescript-that-archives-netnewswire-post-to-devonthink-pro/) and [Ethan’s](http://web.archive.org/web/20080509071046/http://blackrimglasses.com/archives/2007/07/16/answer-to-infooverload/) attempt to deal with info overload.

It attaches the referral URL to the DEVONThink record, so when it creates the archive, it will actually fetch the article from the original source (ex. del.icio.us posts get the original article)

Since DEVONThink doesn’t really do tags, I’ve co-opted the comments field for this purpose.

This is attached to a Quicksilver trigger (CMD-CTR-OPTION-/).

Here is the workflow:

* SCAN: Quickly scan headlines in NetNewsWire and hit return when I see a headline that seems interesting. This opens the page in the background in a tab in NNW
* READ: Go down list of articles, skim them, do CMD-CTR-OPTION-/ for those I’d like to possibly include in future research to invoke my script. \* In the prompt that appears, type a few keywords/tags that describe the content and hit “return”
* REVIEW: Later on, when doing research or work around a topic, I can use DEVONThink’s smart searching features confidently knowing that it will dig up at least some interesting connections between articles I saved.

Things to do:

* add a growl notification saying “successful import”
* write a looping script that will handle the few hundred articles marked as “flagged” in NNW by archiving them. What would the tags be here?

set destination\_group\_location to "/url/delicious/"

tell application "NetNewsWire"
    set userInput to text returned of (display dialog "Enter Tag:" default answer "untagged")

    set h\_tags to userInput
    
    set AppleScript's text item delimiters to space
    set h\_tags to h\_tags's text items
    set AppleScript's text item delimiters to {""}--> restore delimiters'
    
    try
        if (index of selected tab is not 0) then
            set tabnum to index of selected tab + 1
            set taburls to URLs of tabs
            set h\_URL to (get item tabnum of taburls)
            set tabtitles to titles of tabs
            set h\_title to (get item tabnum of tabtitles)
            set h\_mdate to get current date
            set h\_when to current date
            
        else if exists selectedHeadline then
            set h\_URL to URL of selectedHeadline
            set h\_title to title of selectedHeadline
            set h\_mdate to get current date
            if exists date published of selectedHeadline then
                set h\_when to date published of selectedHeadline
            else
                set h\_when to date arrived of this\_headline
            end if
        else
            error "No headline is selected."
        end if
    on error error\_message number error\_number
        if the error\_number is not -128 then
            try
                display alert "NetNewsWire" message error\_message as warning
            on error number error\_number
                if error\_number is -1708 then display dialog error\_message buttons {"OK"} default button 1
            end try
        end if
    end try
    
    tell application "DEVONthink Pro"
        if item 1 of h\_tags is "private" then
            set destination\_group\_location to destination\_group\_location & item 2 of h\_tags
        else
            set destination\_group\_location to destination\_group\_location & item 1 of h\_tags
        end if
        
        if not (exists record at destination\_group\_location) then
            set destination\_group to create location destination\_group\_location
        else
            set destination\_group to get record at destination\_group\_location in current database
        end if
        
        set archive to create record with {name:h\_title, type:html, creation date:h\_when, modification date:h\_mdate, URL:h\_URL, comment:userInput} in destination\_group
        set source of archive to download markup from h\_URL
        
    end tell
    
    tell application "Cocoalicious"
        if item 1 of h\_tags is not "private" then
            make new post with properties {description:h\_title, url:h\_URL, tag string:userInput}
        end if
    end tell
    
end tell
