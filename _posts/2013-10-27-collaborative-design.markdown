---
title: Collaborative design
---

Having talked about it a bit with a few people, my friend [Cory](http://corykaufman.com/) recently[^2] sent me [an essay](http://www106.pair.com/rhp/free-software-ui.html) from way back in 2002 by [Havoc Pennington](http://ometer.com/) on why free software often has poorly designed UI.

One of his points is that “designers can’t submit code patches.” I have long felt this was a major problem facing not just UI designers in OSS, but any designers working collaboratively.

Basically, the reason a relatively hierarchically flat collaborative style works so well for software is that it’s atomic. Code is made up of functions and objects, which in turn are made up of lines, which in turn are made up of characters. The way most languages are designed, lines make the perfect atomic unit for versioning, making version management tools like Git work so well for large teams. When someone makes a change to someone else’s code, it’s really easy to see exactly what the change was.

That makes it really easy for someone who’s never contributed to a project before to fix bugs and make small changes. UI design[^1] is different. Like any kind of design, it requires big-picture vision. And that is exactly what top-down organizational structures or solo designers are good at.

Is this just a matter of tools that are inadequate for the task of distributed design, or is this really a fundamental aspect of design that makes it poorly suited to large, distributed teams?

[^2]: Apparently I started this post on April 27, 2011 despite not getting around to finishing it till now.

[^1]: UI design is distinct from UI implementation. Nudging something a few pixels, slightly modifying the behavior of UI elements, etc., is UI implementation, and is something that is at least somewhat atomic.