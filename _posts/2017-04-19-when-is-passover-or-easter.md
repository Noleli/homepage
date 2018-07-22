---
title: When is Passover (or Easter)?
---

A few weeks ago, [@iamreddave](https://twitter.com/iamreddave/status/846124447312609280) tweeted a plot of Easter dates since 1600. I thought it was a very cool looking pattern, with very clear cyclicality.

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">What date is Easter Sunday? Picture of the April dates for 500 years <a href="https://t.co/A10AHJv8j5">pic.twitter.com/A10AHJv8j5</a></p>&mdash; iamreddave (@iamreddave) <a href="https://twitter.com/iamreddave/status/846124447312609280">March 26, 2017</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

Being Jewish, I immediately thought of the calendrical connection between Easter and Passover. Specifically, since Easter is usually around Passover, does the 19-year cycles of Hebrew leap years play a role in when Easter falls?

Very briefly (and approximately), a solar year is aligned with the seasons (because a year is one orbit of the earth around the sun), but the [Hebrew calendar](https://en.wikipedia.org/wiki/Hebrew_calendar) is based on a lunar calendar in which a month is determined by one cycle through the phases of the moon. The solar year is approximately 365 days, while 12 lunar months are approximately 354 days, or 11 days shorter. If the Hebrew calendar were a pure lunar calendar, over time the months would drift around the year. To make up for this shortfall, a 30-day leap month is added to the Hebrew calendar every two to three years, seven times in a 19-year cycle (years 3, 6, 8, 11, 14, 17, and 19). (30 days × 7 years ≈ 11 days × 19 years. Hey, I said this explanation is approximate.)

<!-- d3 window size 655 x 537 to copy svg figures -->

To see the effect of Hebrew leap years on Easter dates, I recreated iamreddave's graph, but with larger points for leap years and points colored by position in the 19-year cycle.

> Interact with these graphs at [https://projects.noahliebman.net/pesach-easter/](https://projects.noahliebman.net/pesach-easter/)

![Easter dates]({{site.baseurl}}/post-uploads/easterpesach_easter.svg)

What jumps out to me is that all of the late Easter dates are Hebrew leap years, which is what you'd expect when an additional month has recently been inserted, but all of the *early* Easter dates are also Hebrew leap years.

Passover, on the other hand, always occurs late in a leap year, as you'd expect:

![Passover dates]({{site.baseurl}}/post-uploads/easterpesach_pesach.svg)

Toggling between the two, it looks like it's years with the latest Passovers that get leap-year--early Easters.

![Animating between Easter and Passover]({{site.baseurl}}/post-uploads/easterpesach_animated.gif)

Zoom in a bit and you'll find that the early Easter dates are always years 8, 11, and 19 of the 19-year cycle:

![Easter, zoomed in on about 20 years]({{site.baseurl}}/post-uploads/easterpesach_zoomed.svg)

I thought maybe this happens because the Christian 19-year cycle is shifted by three years from the Jewish cycle (2014 was the first year of the Christian cycle, while 2017/5777 is the first year of the Jewish cycle), but this isn't the case. Here's what seems to be happening:

Easter is ([by definition](http://www.whydomath.org/Reading_Room_Material/ian_stewart/2000_03.html)) the first Sunday after the full moon after the vernal (in the northern hemisphere) equinox. Typically, that's the full moon of Nissan (the Hebrew month which contains Passover), but in those three years the leap month pushes Passover so late that it's a full month later than the equinox. In other words, in those years the new moon that marks the start of Nissan is at least ~14 days *after* the equinox, which puts a full moon very shortly after the equinox, which is still in Adar II (the month before Nissan).

Shout out to the [Hebcal](https://www.hebcal.com/) team for their amazing tools!

> Interact with these graphs at [https://projects.noahliebman.net/pesach-easter/](https://projects.noahliebman.net/pesach-easter/)
