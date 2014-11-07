---
comments: true
date: 2011-06-15 17:03:48
slug: on-atoms-and-bits-the-dying-metaphor-of-the-filesystem
title: 'On atoms and bits: the dying metaphor of the filesystem'
wordpress_id: 425
categories:
- Information
- Software
---

Last week on [Twitter](http://twitter.com/Noleli/status/77805643213438976) (during Steve Jobs’s WWDC keynote) I lamented  the death of the filesystem. I want to flesh out a few of my thoughts on the subject.

I think one of the reasons I like the filesystem so much is that I’ve actually come to believe the metaphor. When I think about tags, saved searches, even searching in general, I find it uncomfortable because I want to know where the file is _actually_ located. I’m just much more comfortable with knowing where it resides “on disk”. That’s why, to me, one of the great things about having a jailbroken iPhone is that I can actually browse the file system: I just like knowing it’s there. Even MySQL databases make me uneasy because it’s really challenging to interact with it from the relatively low level of the file system. It all feels too abstract.

But now that I think about it, really, it’s a false sense of concreteness and of security. No, in fact, the file system doesn’t really exist either. But the metaphor is so powerful because it gives the impression that each file is located _somewhere_, like a bunch of atoms -- and that feels good.

Is that important? And is losing that such a bad thing? The main problems I see with most systems that don’t rely on the hierarchical filesystem is that they don’t offer any way to share files between applications. Making certain documents accessible only from within the applications they were created in is pretty standard in iOS. I [commented](http://twitter.com/Noleli/status/27989044949) a while back that Mac OS X Lion represents a shift on the desktop away from a document-centric model toward an app-centric model, but that must not come at the cost of losing the ability to easily open and operate on documents from within any application. What will that look like if it’s not the HFS?
