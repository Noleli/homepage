---
comments: true
date: 2009-04-27 17:32:32
slug: instant-hijack-and-digi-coreaudio-driver-are-not-friends
title: Instant Hijack and Digi CoreAudio driver are not friends
wordpress_id: 168
categories:
- audio
- Software
tags:
- Airfoil
- Audio Hijack
- CoreAudio
- Digidesign
- drivers
- Instant Hijack
- Rogue Amoeba
- solution
- troubleshooting
---

Just in case anyone else runs into the same issue…


[![digi-instant-hijack-compatibility-fail]({{site.baseurl}}/post-uploads/digi-instant-hijack-compatibility-fail.png){: .aligncenter}]({{site.baseurl}}/post-uploads/digi-instant-hijack-compatibility-fail.png)



I just spent about half an hour trying to figure out why I couldn't get the [Digi CoreAudio driver](http://www.digidesign.com/index.cfm?navid=3&langid=100&categoryid=35&itemid=23192) to work. It knew that in order to grab the audio from a given application, one needs to launch that application after the CoreAudio Manager is connected to the hardware.

This whole "re-launch the application to grab the audio" thing reminded me of [Audio Hijack/Airfoil](http://rogueamoeba.com/) without Instant Hijack installed, so it occurred to me that maybe Instant Hijack inserting itself between my applications and the Digi driver.

Turns out I was right: I uninstalled Instant Hijack (a quick and easy process, I might add), and when I logged back in, the CoreAudio manager was able to "attach clients".

I certainly can't blame either of these companies — they're both trying to do some rather unsupported stuff with system audio — but I figured I post in case anyone else runs into a similar issue.
