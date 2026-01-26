---
id: 65ac4ceb0e7c79000119abe5
title: Quix - useful tweak for web workflow
feature_image:
description: I learned about Quix today. It’s a bookmarklet-driven shortcut tool for web browsing and has LOTS of potential for shortcuts and helpful…
date: 2012-01-24
full-date: 2012-01-24T17:23:29.000Z
tags:
  - posts
slug: quix-useful-tweak-for-web-workflow
type: post
draft: false
---

I learned about [Quix](http://www.quixapp.com/) today. It’s a bookmarklet-driven shortcut tool for web browsing and has LOTS of potential for shortcuts and helpful information processing workflow due to its built-in and custom command features.

Here’s an example of my custom quix.txt configuration file. I expect this will evolve rapidly over time ~(and I’ll eventually get this into github or something)~(Done!)

[David’s quix.txt](https://gist.github.com/1683139)

I use Chrome as my primary browser. Unlike safari, it does not allow for keyboard shortcuts for bookmarks or bookmark (ex. if you press cmd-1 while in Safari, the browser launches the first bookmark in the bookmark bar.

To hack this into Chrome (without using one of the clunky extensions available for this purpose), you use the Mac OS X System Preferences > Keyboard > Keyboard Shortcuts.

#### Instructions to set keyboard shortcut for bookmarks in Chrome

```
1. Go to System Preferences > Keyboard > Keyboard Shortcuts. Select Application Shortcuts and click + to add a new shortcut. Pick Google Chrome exact name for the Quix bookmarklet.  
2. I choose ctrl-1, which works pretty well since I use the caps lock key as a second control modifier. You should see the keyboard short right in Chrome’s Bookmarks menu  
3. Just ctrl-1 your way to productivity. An added benefit over the extension route is that the shortcut works even if the omnibar has focus.
```

(via [Keyboard Shortcuts for Bookmarklet on Google Chrome – 5typos.net](http://5typos.net/post/6611916064/keyboard-shortcuts-for-bookmarklet-on-google-chrome))

So the workflow becomes:

1. bang on ctrl-1
2. type mt
3. bang on cmd-c to copy the already highlighted markdown-formatted link into clipboard

Fast and no mouse required!

Remarkably, quix works on all browsers that support JavaScript bookmarklets — even safari on iOS devices!

### Updates

* 2012-01-26: changed link to github gist
