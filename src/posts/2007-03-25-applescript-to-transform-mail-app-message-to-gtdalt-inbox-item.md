---
id: 65ac4ceb0e7c79000119ac0e
title: Applescript to transform mail.app message to GTDAlt inbox item
feature_image:
description: I’m currently using GTDAlt in TextMate as my GTD processing system. It’s a text based system, so it’s upgradable, portable, etc.
date: 2007-03-25
full-date: 2007-03-25T17:56:00.000Z
tags:
  - posts
slug: applescript-to-transform-mail-app-message-to-gtdalt-inbox-item
type: post
draft: false
status:
---

I’m currently using [GTDAlt](http://skiadas.dcostanet.net/afterthought/2006/06/25/details-on-the-gtdalt-bundle/) in [TextMate](http://macromates.com/) as my GTD processing system. It’s a text based system, so it’s upgradable, portable, etc.

Through the [TextMate](http://macromates.com/) bundle framework, you get some nice collating of contexts, etc.

[GTDAlt](http://skiadas.dcostanet.net/afterthought/2006/06/25/details-on-the-gtdalt-bundle/) does rely on some proprietary syntax, but it’s pretty basic and easily parsable.

There is rudimentary support for iterating through items in an inbox.txt file to generate GTD items.

I created an applescript which will take the selected message in Mail.app and create a properly formated item, using the subject and message: url (you must have [MailTags](http://www.indev.ca/MailTags.html) installed so the message: protocol is recognized).

This means I’ll get action items with links to specific messages in my GTD system.

I partner this with a [Mail Act-On](http://www.indev.ca/MailActOn.html) rule… so when I hit ctrl-1, a [GTDAlt](http://skiadas.dcostanet.net/afterthought/2006/06/25/details-on-the-gtdalt-bundle/) item gets created, the message is tagged “@action”, and it’s sent to my one archive folder in one step.

In true GTD fashion, this should only be used for messages that take longer than 2 minutes to respond to. In reality, I need to get better at firing off quick responses to things (or liberally using the delete key). Otherwise, it’s likely I’ll use this to just procrastinate email items away into a black hole.

[Download the script](https://davidnunez.com/assets/2007/3/26/Mail_to_TMGTD.scpt)
