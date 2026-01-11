---
id: 65ac4ceb0e7c79000119ac04
title: Converting from Mephisto to Wordpress
feature_image:
description: Finished pulling in old entries to wordpress.
date: 2007-07-21
full-date: 2007-07-21T11:28:11.000Z
tags:
  - posts
slug: converting-from-mephisto-to-wordpress
type: post
draft: true
status:
---

Finished pulling in old entries to wordpress.

1. adjust controllers/feed\_controller so that the article limit is greater than number of articles
2. clear cached feed in settings
3. in CLI, execute “curl <http://yoururl.com/feed/> > feed.xml” (atom)
4. use an xml / xsl editor on feed.xml to apply the Atom2RSS xsl sheet found here [http://atom.geekhood.net/](http://atom.geekhood.net/)
5. Use RSS import on wordpress

Issues: Tags / Categories get all mixed up. Pages and comments do not import
