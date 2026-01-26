---
id: 65ac4ceb0e7c79000119abfe
title: Spam and Email System
feature_image:
description: I think I have finally nailed down a reasonable email handling / spam fighting strategy after about a year of tweaking.
date: 2007-10-31
full-date: 2007-11-01T00:44:44.000Z
tags:
  - posts
slug: spam-and-email-system
type: post
draft: false
---

I think I have finally nailed down a reasonable email handling / spam fighting strategy after about a year of tweaking.

I’m going to slowly describe my system over a series of posts. It’s pretty good, if I do say so myself.

Here are a couple of ranty things I’d like to just put out on the table, first.

I wish I had a quarter for whenever somebody says, “Oh, man, I get SOOO many email messages every day that I don’t have time to read them all, much less respond.”

It’s usually followed by some quantification, “I get over 1000 messages everyday” and _always_ includes some corollary about, “I subscribe to 100 mailing lists” and “I have 20 email addresses I check” and “that doesn’t even include SPAM!”

I’m going to carry around blue ribbons and certificates for whenever somebody says this.

What they are trying to explain to you is that they are important. And important people get lots of email. And since they are more important than you, they mask their immense fear of being discovered as disorganized or type-B or luddites with a cloud of digital detritus that enables them to defraud their families and employers by engaging ineffectively with pointless busywork rather than actually contributing to society.

Here’s the reality check:

1. Human beings can’t process thousands of messages a day.
2. Good news. Most email does not deserve your attention.
3. You will not have to act on all of the messages you receive each day.
4. Saying “I have too many pieces of email” is admitting you have poor skills at prioritizing.
5. Shut up and deal… we’re all faced with the same (or worse) email and spam barrage.
6. If you can’t deal with your avalanche of email, then you and your system are outdated and broken. Upgrade, dinosaur.
7. Will the world end or will people suffer and die if you don’t handle all your email? If so, why the hell are you talking to me instead of clearing your inbox?
8. Coping mechanisms: Hire assistants. Hit the delete key. Go read [Lifehacker](http://lifehacker.com). Streamline your system. Get in touch with yourself. Climb a mountain and meditate on what’s truly important.

So here’s me: 4000 messages daily (including SPAM, including mailing lists, including automated notices) that pass through my multiple servers hosting multiple email addresses.

The system I use filters that down to roughly 20 per day that MAY require a response or action. They all come to the one inbox.

Using some Mail.app plugins to triage, route, and deal, I can handle these in under 30 minutes.

The rest are handled by autoresponders or are filed away through a set of rules. I’ve recently implemented some steps that automagically archive older stuff into a MySQL database in the most absurdly remote, almost impossible chance I’d need to refer back to those posts some years down the line.

That beats [Pareto](http://en.wikipedia.org/wiki/Pareto_principle) 20/80 easily, and I’m going to share how I do it.

**Pre-requisites**: Go read [Merlin Mann’s inbox zero](http://www.43folders.com/izero) series for some theory. Implement and live with his system for a while. Only then should you consider my tweaks.  
You’ll need a computer running OS X using Mail.app as your primary client. You’ll have to purchase roughly $100 worth software. (ask yourself how much your time is worth before balking at that).

One other pet peeve: It’s “email messages” or “email posts” or “pieces of email” or _sometimes_ just “email.” It is NEVER CORRECT to say “emails.” This is the same as never saying, “I’m going to the post office to drop off mails.”

And yes… with my backlog of owed responses, I’m self-aware enough to recognize “Pot. Kettle. Black.” That’s why I’m projecting so strongly.

Upcoming: Mail.app baseline setup. IMAP, Inbox, Archives, and Smart Folders I Use
