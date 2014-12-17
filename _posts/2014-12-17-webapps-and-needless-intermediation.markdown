---
title: Web apps and needless intermediation
---

Histories of computing, computing culture, and the politics of computers often make this basic claim: the very purpose of the Personal Computer was so individuals could benefit from computation without having to rely on corporate- or government-controlled mainframes. But it's pretty clear to me that we've come full circle and are over-reliant on remote servers. The founders of the PC movement would probably say that we've lost our way. (Lazyweb: can someone dig up a quote of Woz saying so?)

Of course it's not black and white, but we've gone overboard. I see this from two directions:

1. **Web apps**. I like to give friends on Twitter a hard time because I strongly believe in native apps over web apps. This is partially because of the superior performance and user experience, but in large part it's because there is simply no reason for most apps to not run on my computer. A word processor or text editor does not need to run on someone else's computers (which makes me both reliant and vulnerable). Nor does it need to run in a web browser, which, twenty-some years on, is still not particularly well suited to applications. Google's vision of dumb terminal Chromebooks takes this needless remote execution to its (il)logical extreme.

2. **(Needless?) intermediation**. In addition to needless remote code execution in an inferior UI framework and runtime environment, why should my IMs or video calls go through Google or Skype servers between me and their destination? I'm reading [The Master Switch](http://www.amazon.com/The-Master-Switch-Information-Empires/dp/0307390993) by [Tim Wu](http://timwu.org/), and one of his points is that the underlying architecture of the internet is helping it resist the corporate forces that have brought about consolidation in other information industries.

	That architecture, it seems to me, is one in which every machine on the network can access any other machine on the network. But that no longer seems to be the case. AIM used to have a feature called [Direct Connect](https://trac.adium.im/wiki/ServiceFeatures); years before Google Docs, [SubEthaEdit](http://www.codingmonkeys.de/subethaedit/) allowed for collaborative editing directly between computers. So why is that not how we communicate now? It was finicky, and we (rightfully) like things that Just Work™. It was finicky because most of us don't have public/external IP addresses. That meant having to route network traffic through [IP masquerading NATs](https://en.wikipedia.org/wiki/Network_address_translation, and getting a two-way route is hard.	(Even Skype's so-called [P2P protocol](https://en.wikipedia.org/wiki/Skype_protocol) uses "supernodes", which are located in Skype/Microsoft datacenters, as intermediaries betweened NATed/firewalled clients.)

	So because most end users do not have public IP addresses, it's more reliable to have most traffic routed through a server. This breaks the very property of the internet that makes it so unique. Perhaps this is a natural stage of development in the network, because we're running out of IPv4 addresses. Maybe with IPv6, everyone can have a public IP, and we'll be able to collaboratively edit documents peer-to-peer, from my text editor to yours.

To conclude, the words of the inimitable [@SwiftOnSecurity](https://twitter.com/SwiftOnSecurity):

<blockquote class="twitter-tweet" lang="en"><p>The Cloud should be renamed Mainframes for Millennials</p>&mdash; InfoSec Taylor Swift (@SwiftOnSecurity) <a href="https://twitter.com/SwiftOnSecurity/status/534478342267740160">November 17, 2014</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>