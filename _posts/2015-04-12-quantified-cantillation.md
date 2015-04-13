---
# title: [Data] science and religion
title: Quantified cantillation
---

When read publicly, the [Torah](https://en.wikipedia.org/wiki/Torah) is often sung using a system of [cantillation marks](https://en.wikipedia.org/wiki/Cantillation), or *trop* in Yiddish. There are many different cantillation marks, each of which has a name, a unique sound (or sounds), and comes in combination with other *trop*.

When the cycle of readings started over this year after [Simchas Torah](https://en.wikipedia.org/wiki/Simchat_Torah)[^transliteration], it seemed like there were more *telisha gedolah*s in *Bereshit* (Genesis), whereas there were more *telisha ketana*s in *D'varim* (Deuteronomy). I decided to find out whether or not this was really the case.

First, I needed a dataset. [Tanach.us](http://tanach.us) offers the entire *Tanakh* in XML form, including *trop* and vowels. I was only interested in the Torah, so I downloaded XML files for each of the five *sfarim* (books). I went through the XML and tabulated how many of each *trop* were present in each *pasuk* (sentence).

<!-- To make it easier to work with, I made an object that maps an English transliteration of each *trop* name to its respective unicode character. I then went through each of the five sfarim and tallied how many of each *trop* were in each *pasuk* (sentence). This seemed like a great opportunity to play with Pandas's MultiIndexes, so I structured the data such that each row is indexed by `(sefer, perek, pasuk)` and each column is the name of a *trop*. -->

<!-- As you might expect for count data where most *trop* don't occur every (or even most) *psukim*, the distributions of *trop* occurrence for most *trop* resemble zero-inflated Poisson distributions, although some of the more frequent *trop* look more normal, and extremely common ones like *etnakhta* or *sof pasuk* are left skewed. Because of this, after talking with my friend Zach (a Ph.D. student in Statistics), we decided to stick with a visual analysis for now. -->

<!-- ![Distributions for a common and less common trop] -->

Aggregating by *sefer* to consider my original question about the relative frequencies of *telisha gedolah*s and *telisha ketana*s, we see that my intuition was somewhat correct: while there are more *ketana*s throughout, there are more overall *ketana*s in *D'varim*.

<img src="{{site.baseurl}}/post-uploads/trop/telisha_bar.svg" alt="Telisha Ketana and Telisha Gedola by Sefer" class="svgalt svg">
<img src="{{site.baseurl}}/post-uploads/trop/telisha_bar.png" alt="Telisha Ketana and Telisha Gedola by Sefer" class="svgalt img">


However, the ratio of *telisha gedola* to *telisha ketana* is actually not substantially different in *D'varim* and *Bereshit*. So while overall counts are higher, the relative frequencies are not so different.

<img src="{{site.baseurl}}/post-uploads/trop/telisha_ratios.svg" alt="Ration of Telisha Ketana to Telisha Gedola by sefer" class="svgalt svg">
<img src="{{site.baseurl}}/post-uploads/trop/telisha_ratios.png" alt="Ration of Telisha Ketana to Telisha Gedola by sefer" class="svgalt img">

<!-- relatively more *ketana*s than *gedola*s in the middle of *Dvarim*. -->

Aggregating by *sefer* is interesting, but I wanted to see more continuous variations. Looking at a series of what for most *trop* would be zeros and ones, with an occasional two or three, isn't that useful, but [Zach](https://twitter.com/zseeskin) (a Ph.D. student in Statistics) suggested a moving average, and that worked quite nicely. We used a 500-*pasuk*-wide window, which struck a balance between detail and low-pass filtering. (I come from a signal processing background, not time-series analysis.)

As with the initial bar graph, you can really see the number of *telisha ketana*s explode in *D'varim*. But more interestingly, we can get a sense of how they track each other through the Torah.

<!-- Although I had some initial concerns about whether a mean would be meaningful for such non-normal data, it's essentially just a count of *trop* occurances in a given window normalized by the number of *psukim* in the window. -->


<img src="{{site.baseurl}}/post-uploads/trop/telisha.svg" alt="Telisha Ketana and Telisha Gedola through the Torah" class="svgalt svg">
<img src="{{site.baseurl}}/post-uploads/trop/telisha.png" alt="Telisha Ketana and Telisha Gedola through the Torah" class="svgalt img">

Seeing how different *trop* track each other is fun. There are some things that you'd expect. For example, *munakh* is often associated with *katan*, *revi'i*, and *mapakh*--*pashta*, and we see that clearly here.

<img src="{{site.baseurl}}/post-uploads/trop/common_trop.svg" alt="Common associated trop through the Torah" class="svgalt svg">
<img src="{{site.baseurl}}/post-uploads/trop/common_trop.png" alt="Common associated trop through the Torah" class="svgalt img">

Particklarly striking is the tight correlation between *zarka* and *segol*.

<img src="{{site.baseurl}}/post-uploads/trop/zarkasegol.svg" alt="Zarka and segol through the Torah" class="svgalt svg">
<img src="{{site.baseurl}}/post-uploads/trop/zarkasegol.png" alt="Zarka and segol through the Torah" class="svgalt img">

Although other combinations, though, like *darga*--*tevir* are more loosely correlated.

<img src="{{site.baseurl}}/post-uploads/trop/dargatevir.svg" alt="Darga and tevir through the Torah" class="svgalt svg">
<img src="{{site.baseurl}}/post-uploads/trop/dargatevir.png" alt="Darga and tevir through the Torah" class="svgalt img">

(For more correlations, here are the [*pasuk* by *pasuk*]({{site.baseurl}}/post-uploads/trop/rawcorr.html) and [moving window]({{site.baseurl}}/post-uploads/trop/rollingcorr.html) correlation tables.)

While these patterns are intuitive, the fact that trop --- especially common ones like *merkha* and *tipkha* --- aren't uniformly distributed across the Torah was, to me, somewhat less expected. A big reason for this is changes in sentence structure. This becomes extremely obvious when looking at *etnakhta*, which essentially functions as a comma.

<img src="{{site.baseurl}}/post-uploads/trop/etnakhta.svg" alt="Etnakhta through the Torah" class="svgalt svg">
<img src="{{site.baseurl}}/post-uploads/trop/etnakhta.png" alt="Etnakhta through the Torah" class="svgalt img">

The reason for the rather dramatic plunge toward the beginning of *B'midbar* seems to be a shift in sentence structure. Checking the text, this part of the Torah contains quite a bit of genealogy, which contains many single-phrase sentences ("So-and-so begat so-and-so"[^women]), and many occurrences of the common *pasuk* "<span dir="rtl">וידבר ה` אל־משה לאמר</span>".

Oddly, I did a bit of digging into this, and it looks like a drop in words per *pasuk* actually lags the drop in *etnakhta*s. I'm not sure why.

<img src="{{site.baseurl}}/post-uploads/trop/etnakhtawordcount.svg" alt="Etnakhta and wordcount through the Torah" class="svgalt svg">
<img src="{{site.baseurl}}/post-uploads/trop/etnakhtawordcount.png" alt="Etnakhta and wordcount through the Torah" class="svgalt img">

I could imagine running a logistic regression to see whether words per *pasuk* predicts the presense of an *etnakhta*, but I'm going to cut myself off now.

If you're interested in playing around with this yourself, everything is on [GitHub](https://github.com/Noleli/trop-analysis). If you just want to cut to the chase, here's a [CSV file]({{site.baseurl}}/post-uploads/trop/trop.csv) of the raw data. And here's an [IPython Notebook](http://nbviewer.ipython.org/github/Noleli/trop-analysis/blob/master/Trop%20analysis.ipynb).

[^women]: No wife required, incredibly.

[^transliteration]: Benjamin, please forgive my transliterations.