---
title: "Quantified cantillation III: sequences"
---

> [First post]({% post_url 2015-04-12-quantified-cantillation %})  
> [Second post]({% post_url 2015-04-17-quantified-cantillation-ii-word-counts %})

Earlier this year I published a couple of [blog]({% post_url 2015-04-12-quantified-cantillation %}) [posts]({% post_url 2015-04-17-quantified-cantillation-ii-word-counts %}) with some descriptive statistics of *[trop](https://en.wikipedia.org/wiki/Cantillation)* in the Torah. One of the biggest shortcomings of those posts was that they didn't deal with the order of *trop* at all. This is a pretty big shortcoming when you consider that many *trop* come in pairs/groups, or that certain *trop* frequently or necessarily follow certain other *trop*. So, this time around I created an interactive tool I'm calling (for lack of creativity) the [Trop Sequence Explorer](http://quantifiedcantillation.nl/). If you haven't [checked it out](http://quantifiedcantillation.nl/) yet, I'd suggest playing around with it a bit; it'll give you context for the rest of this post.

Basically, it shows each *trop* listed in order from most to least common. When you click one, it shows you all *trop* that can follow it and how often each one occurs in that sequence. In other words, it shows transition probabilities to each *trop* conditional on all *trop* that come before it in a sequence. There's also a graph at the bottom that shows how often the selected sequence occurs in each *perek* of the Torah. Clicking a bar in the graph shows the text of the *p'sukim* in that *perek* that contain the current sequence.

<!-- As with before, as far as I know this has no scholarly value, but it seemed like an interesting thing to do. -->

[![Trop Explorer screenshot]({{site.baseurl}}/post-uploads/trop/sequenceexplorer/screenshot.png)](http://quantifiedcantillation.nl/)

What follows is a bit of the thought process that went into its creation, some issues I ran into, and some interesting observations. Feel free to jump to the section that's most interesting to you.

## The Jewish Nerd section

Back in the fall, I was *gabbai*ing and noticed two *tevir*s in a row. "How often does that happen?", I wondered. Seven times, it turns out. It's pretty well known that a *zarka* has to be followed by a *segol* or a *munakh segol*, but it turns out that the latter is actually more common (by a 13-point margin).

Beyond the factoids, there are other fun things to come across. Parallel sentence structures often have parallel *trop*, even when the *trop* itself is not that common. In *B'midbar* 26, *gadol* is used at a much higher rate than normal, mostly on names in a genealogy; it really pops out in the bar graph.

![Gadol in B'midbar 26]({{site.baseurl}}/post-uploads/trop/sequenceexplorer/gadol-bmidbar26.png)

One of the most surprising things for me, though, is how relatively unique each *pasuk* is. Once you get more than three or four levels deep in the tree, there are surprisingly few *p'sukim* that match that sequence. This is even true for seemingly common sequences. A *pasuk* that is *merkha tipkha etnakhta merkha tipkha sof pasuk* only happens 43 times in the entire Torah.

As I was creating the Sequence Explorer, I encountered some challenges and needed to make some decisions about how it used *trop* data. One question several people have raised is: Why are there ever *trop* following a *sof pasuk*? Shouldn't a *sof pasuk*, by definition, be the end of a *pasuk*? The answer is that there are two sets of *trop* used for the 10 Commandments, the *takhtonim*, which are used for private study, and the *elyonim*, which are used for public readings. I chose to use the *elyonim* because I wanted to examine how *trop* are read out loud. The problem is that the two sets of *trop* also have different *pasuk* divisions. Even though I used the *elyon* *trop*, I had to use the *takhton* *pasuk* divisions, because the *takhton* divisions seem to be more standard, and are the ones returned by the [Sefaria](http://www.sefaria.org/) API, which is what I used to pull the in actual *pasuk* text when you click on a *perek*'s bar in the bar graph. Perhaps at some point I'll add a setting so people can explore both versions.

Many authorities consider *munakh legarmeh* a separate *trop*. I decided not to count it separately for two reasons. The simple technical reason is that there is not a different Unicode character for it (distinct from *munakh*), so I would have to detect it based on context. The other is that, by definition, the *munakh legarmeh* is a *munakh* that precedes another *munakh*. Since that's exactly the type of data this app shows, it felt both redundant and somewhat circular to distinguish a *trop* by what follows it. If you click the *munakh*, the number of *munakh*s that follow it should be equal to the number of *munakh legarmeh*s.

Seeing sequences also helped me find issues in the data that I couldn't see otherwise. For example, I found a couple instances where the data showed four *pashta*s in a row, but this wasn't really the case. *Trop* typically indicate where the stress should fall in a word, but some *trop* must be placed at either the beginning or the end of a word regardless of stress. To help readers, many sources, including --- I found out --- the [Tanach.us](http://tanach.us/) data source I used, put such *trop* on a word twice: once in the required position, and once where the stress falls. I cleaned out those doublings by searching for any word with two *trop* on it, and if the two *trop* were the same, I deleted one of them. Hopefully there was no collateral damage from that.

Another oddity was that there were ten *tsinnorit*s and one *geresh mukdam*. This was odd because [those *trop* aren't used in the Torah](https://en.wikipedia.org/wiki/Cantillation#Names_in_different_traditions), even if their lookalikes, *zarka* and *geresh* are. It seems like they were used for [typesetting reasons](http://tanach.us/Pages/Coding.xml) --- their placement on a word is slightly different --- so I just lumped them in with their respective lookalikes.

There were also a number of *p'sukim* with no *sof pasuk*. I'm not sure exactly why, but I fixed them. Being able to see the bar graph across the bottom was hugely helpful in seeing that this was an issue.

Speaking of the bar graph at the bottom, aggregating by *perek* is somewhat arbitrary. At some point I would like to try aggregating in other ways, such as by *parshah*.

## The Design Nerd section

I knew pretty early on that I wanted to do some sort of [Markov chain](https://en.wikipedia.org/wiki/Markov_chain)--like visualization of transition probabilities, but I set the idea aside to do real work, which, fortunately, happened to involve learning [D3](http://d3js.org/). When I turned my attention back to this, I realized two things:

1. Pairwise transition probabilities aren't that interesting in isolation; sequences are much more interesting. (In other words, you need memory in your Markov chain.)

2. As in the previous posts, we have the complete dataset. Descriptively exploring that is very different from wanting to make predictions or generate new sequences, which is a more typical use of Markov chains.

So, I settled on the basics of a design, but without a few key features. The original idea was a tree, where each level would show the conditional probability of going to a particular trop given all those that had come before it. The plan was just to show simple squares with a *trop* symbol, its name, conditional probability, and conditional count. And, there was no bar graph at the bottom to show where a given sequence occurred.

![Original whiteboard sketch (or what's left of it)]({{site.baseurl}}/post-uploads/trop/sequenceexplorer/whiteboard.jpg)

It wasn't until I was sketching out the visual design for the squares --- well after I had it actually working --- that I came up with the idea of shading them in, making them into a histogram of sorts. Since they seem to follow something not entirely unlike a [Poisson distribution](https://en.wikipedia.org/wiki/Poisson_distribution), I thought about log-weighting them, but decided it would be more straightforward not to since I'm also showing raw counts.

Once I could play with building sequence trees, I pretty quickly wanted to know where in the Torah those sequences were. And so, the bar graph at the bottom was born. For most of the time I was building it, clicking a bar would just open that *perek* on Sefaria. Using the Sefaria API to pull in the text of the actual *p'sukim* was one of the last features to go in.

## The Programming Nerd section

<!-- I encountered two main challenges when building this: deciding how to structure the data, and the challenges of working right-to-left. -->

When I first started thinking about how to implement this, my intuition was to have the data structure match the tree structure of the interface. It felt elegant, and it seemed like a good idea at the time. I wrote a recursive function (after fighting with mutable container objects in Python) to go through the *trop* strings and build a giant JSON file shaped like this:


~~~
[{
  "name": "munakh",
  "count": 5456,
  "children": [
    {
     "name": "revii",
     "count": 1410,
     "children": […]
     },
     {
     "name": "katan",
     "count": 4350,
     "children": […]
     }
     …
  ]}
  …
]
~~~

Well, that turned out to be 8.6&nbsp;MB --- way too big to download as part of a web app. A similar file that listed which *prakim* had which sequences was over two *gigabytes*. I wrote most of the UI (locally) with these two files. Thankfully, I finally realized that I could just download a 760&nbsp;kB list of raw trop strings and search for sequences on demand in the browser. And *that*, folks, is why I'm in [HCI](https://en.wikipedia.org/wiki/Human%E2%80%93computer_interaction), not real computer science. Derp.

Finally, D3 was great to work with. Being able to define a simple linear scale like this

~~~
var x = d3.scale.linear()
    .domain([0, width])
    .range([width, 0]);
~~~

even made it easy to work right-to-left when SVG objects have their origins in the upper left-hand corner.

<!-- The second issue was working in right-to-left. Most of the time it was actually really straightforward. It was just a matter of using the CSS `direction: rtl` declaration and reversing the bar graph's *x* scale `range()` function. Where it was trickier was in creating transition animations for the sequence tree. SVG coordinates always have their origin in the upper left-hand corner, so if the SVG object is changing width, . When clicking a *trop* to drill down a level, I made the entire SVG object wider. With no animation, this means just recomputing every object's *x* position, but to animate it, you have to keep track of where its parent was in  -->

## Future work

I'm a grad student, so how can I resist a Future Work section? There are a number of features I'd like to add at some point. As I hinted at earlier in this post, it would be nice to be able to aggregate the bar graph by *parshah* instead of just *perek*. Combining other aggregations, like *sefer*, with the ability to limit sequence queries to certain parts of the text would open the door to adding the rest of the *Tanakh*. (The Emet books would be outta control!) And color coding disjunctive and conjunctive *trop* would be a nice way to see more structure in sequences. If you want to take a stab at any of these things, have a look at the [issues](https://github.com/Noleli/trop-analysis/issues) list for this project on [GitHub](https://github.com/Noleli/trop-analysis).

And if you've made it this far without actually using the app, [go play with it now](http://quantifiedcantillation.nl/)!
