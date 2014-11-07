---
title: Ideology versus the user experience
---

The open-source community taking ideological stances to the detriment of users and the user experience is harmful and counterproductive.

[Adium](http://adium.im/), a popular chat/instant messaging client for Mac which uses [libpurple](https://developer.pidgin.im/wiki/WhatIsLibpurple) as a backend, supports the [XMPP](http://xmpp.org/) chat protocol. XMPP is a standard, so any implementation should theoretically conform to that standard. But when the most widely used implementation is XMPP *compatible*, but not *compliant*, that should make developers obligated to produce software that behaves in a broadly accepted way.

Google Chat (aka Gtalk aka Gchat aka that little chat thingy in the corner of most people's email) is based on the XMPP protocol, but the way it handles statuses is different from the XMPP specification. Specifically, Google's *Idle* is XMPP's *Away*, Google's *Away* is XMPP's *Do not disturb*, and Google's invisibility simply doesn't work.

Adium's developers have taken the [stance](http://trac.adium.im/ticket/7848) that "Adium has never supported invisibility on GTalk and will not as long as libpurple does not support it. They dislike the way it works (for good reasons [#p11433](https://developer.pidgin.im/ticket/11433))."

The "good reasons" given by the libpurple team come down to developer ideology:

> Popularity and user-base have never been the sole (or even particularly major) driving factors in pidgin development (as a whole, individual developers can be motivated by anything they want to be motivated by).

> How would you present a configurable option for something like this? Where would you put it? What would you call it? "Enable shared status support and invisibility"? No one will understand that. It is exactly the conjoined nature of these two features that I dislike the most.

> The fact that Google Talk decided the choices of available statuses in the XMPP protocol were too great and "simplified" them down thereby breaking things like DND and XA is most unfortunate, but not exactly a greatly motivating factor for working around that brokenness by introducing as many side-effects as problems one removes.

To me, this is as if the web developers of ten or fifteen years ago simply decided that they didn't care if what they produced looked wrong for the *vast majority* of users because IE was wrong. Just because you don't like the way something is implemented doesn't mean you should break the user experience.

When "doing it right" and "making the user happy" are at odds, the open-source world needs to redefine "doing it right".