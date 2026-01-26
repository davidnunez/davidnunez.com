---
id: 65ac4ceb0e7c79000119ac12
title: Applescript to import NNW smart folder into Yojimbo
feature_image:
description: Today I modified this script which facilitates Yojimbo importing from NetNewsWire
date: 2007-03-20
full-date: 2007-03-20T17:14:32.000Z
tags:
  - posts
slug: applescript-to-import-nnw-smart-folder-into-yojimbo
type: post
draft: false
status:
---

Today I modified [this script](http://samuraicoder.net/netnewswire_to_yojimbo_integration) which facilitates [Yojimbo](http://www.barebones.com/products/yojimbo/index.shtml) importing from [NetNewsWire](http://www.newsgator.com/NGOLProduct.aspx?ProdID=NetNewsWire)

I’ve set up a smart folder in [NetNewsWire](http://www.newsgator.com/NGOLProduct.aspx?ProdID=NetNewsWire) that grabs the latest 50 flagged headlines from any feed.

I needed this script because I had a [technorati](http://www.technorati.com) watch feed for dorkbot and I wanted to collect blog mentions to send around. I was just flagging articles that mentioned dorkbot-austin and wanted to export a list of bookmarks.

With this, the workflow is now:

1. Quickly scan headlines in NetNewsWire and do CMD-Shift-L to flag interesting content.
2. Run this script on the smart folder (this creates a web archive in [Yojimbo](http://www.barebones.com/products/yojimbo/index.shtml) of each of these articles and removes the flag on the headline in NetNewsWire)
3. Over time, spend a few minutes working down the list of archived articles in Yojimbo and tag/delete them further as necessary.

Potential problem: This makes it really easy to procrastinate making decisions on what to read and what to do with what I read. Following this strategy will lead to a large pile of unsorted links which I’ll very likely will never find the time to sort through.

I think [DEVONThink](http://www.devon-technologies.com/products/devonthink) does a better job of scanning and grouping incoming pieces of text.

I should probably rewrite this to send flagged content directly to DEVONThink. Then, instead of queueing up a long list of articles to read, I’ll let DEVONThink suggest articles for me to read as I do research. Anything that I think I’d want to read immediately I could tag with “@Read” or something similar.

    tell application "NetNewsWire"
        try
            set userInput to text returned of (display dialog "Enter Tag:" default answer "untagged")
            set oldDelims to AppleScript's text item delimiters
            set AppleScript's text item delimiters to {", ", ","}
            set h\_tags to text items of userInput
            set AppleScript's text item delimiters to oldDelims
            if (index of selected tab is not 0) then
                set tabnum to index of selected tab + 1
                set taburls to URLs of tabs
                set h\_URL to (get item tabnum of taburls)
                set tabtitles to titles of tabs
                set newItemTitle to (get item tabnum of tabtitles)
                tell application "Yojimbo"
                    --set newItem to make new bookmark item with properties {name:newItemTitle, location:h\_URL}
                    set newItem to make new web archive item with contents h\_URL
                    add tags h\_tags to newItem
                    set flagged of newItem to true
                    set isFlagged of h to false
                end tell
            else if exists selectedSubscription then
                repeat with h in headlines of selectedSubscription
                    set h\_URL to URL of h
                    set h\_title to title of h
                    set isFlagged of h to false
                    tell application "Yojimbo"
                        --set newItem to make new bookmark item with properties {name:h\_title, location:h\_URL}
                        set newItem to make new web archive item with contents h\_URL
                        add tags h\_tags to newItem
                        set flagged of newItem to true
                    end tell
                end repeat
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
    end tell
