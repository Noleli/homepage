---
title: "Entropic Timer: The Entropy of Crossing the Street"
latex: true
d3: true
---

<link rel="stylesheet" type="text/css" href="{{site.baseurl}}/post-uploads/7-segment-display/7-segment-display.css">

<style>
#{{ page.title | slugify }} .bigDigit {
  --height: 300px;
  font-family: 'Helvetica', sans-serif;
  margin-bottom: 15px;
}

#{{ page.title | slugify }} table .rowHeader .digit {
  --height: 32px;
  vertical-align: top;
}
</style>

As a pedestrian, I'm a fan of those countdown timers that tell you how much time is left when crossing the street. To help make sure crossing signs are visible in bright sun, they usually have a hood that shields the display itself. This has the effect of obscuring part of the display when approaching an intersection at an oblique angle.

This got me thinking: if I want to know how much time is left, is it better to see the right side of the countdown timer (approaching from the left), or the left side (approaching from the right)? In other words, does the left or right side of the display contain more information?

These timers use [seven-segment displays](tk). Even if you didn't know they were called seven-segment displays, you see them all over the place. They use seven separate segments, labeled A–G, to create each of the 10 digits from 0–10.

<div class="digit bigDigit">
  <div class="segment segA on"></div>
  <div class="label segA">A</div>
  <div class="segment segB on"></div>
  <div class="label segB">B</div>
  <div class="segment segC on"></div>
  <div class="label segC">C</div>
  <div class="segment segD on"></div>
  <div class="label segD">D</div>
  <div class="segment segE on"></div>
  <div class="label segE">E</div>
  <div class="segment segF on"></div>
  <div class="label segF">F</div>
  <div class="segment segG on"></div>
  <div class="label segG">G</div>
</div>

To form each of the ten digits, the seven segments are turned on or off in different combinations. Here are the standard representations of 0–10.

<table class="segmentDigitTable">
    <tr><td></td><th>A</th><th>B</th><th>C</th><th>D</th><th>E</th><th>F</th><th>G</th></tr>
    <tr>
        <th class="rowHeader">
            <div class="digit digZero">
              <div class="segment segA"></div>
              <div class="segment segB"></div>
              <div class="segment segC"></div>
              <div class="segment segD"></div>
              <div class="segment segE"></div>
              <div class="segment segF"></div>
              <div class="segment segG"></div>
            </div>
        </th>
        <td>1</td><td>1</td><td>1</td><td>1</td><td>1</td><td>1</td><td>0</td></tr>
    <tr>
        <th class="rowHeader">
            <div class="digit digOne">
              <div class="segment segA"></div>
              <div class="segment segB"></div>
              <div class="segment segC"></div>
              <div class="segment segD"></div>
              <div class="segment segE"></div>
              <div class="segment segF"></div>
              <div class="segment segG"></div>
            </div>
        </th>
        <td>0</td><td>1</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td></tr>
    <tr>
        <th class="rowHeader">
            <div class="digit digTwo">
              <div class="segment segA"></div>
              <div class="segment segB"></div>
              <div class="segment segC"></div>
              <div class="segment segD"></div>
              <div class="segment segE"></div>
              <div class="segment segF"></div>
              <div class="segment segG"></div>
            </div>
        </th>
        <td>1</td><td>1</td><td>0</td><td>1</td><td>1</td><td>0</td><td>1</td></tr>
    <tr>
        <th class="rowHeader">
            <div class="digit digThree">
              <div class="segment segA"></div>
              <div class="segment segB"></div>
              <div class="segment segC"></div>
              <div class="segment segD"></div>
              <div class="segment segE"></div>
              <div class="segment segF"></div>
              <div class="segment segG"></div>
            </div>
        </th>
        <td>1</td><td>1</td><td>1</td><td>1</td><td>0</td><td>0</td><td>1</td></tr>
    <tr>
        <th class="rowHeader">
            <div class="digit digFour">
              <div class="segment segA"></div>
              <div class="segment segB"></div>
              <div class="segment segC"></div>
              <div class="segment segD"></div>
              <div class="segment segE"></div>
              <div class="segment segF"></div>
              <div class="segment segG"></div>
            </div>
        </th>
        <td>0</td><td>1</td><td>1</td><td>0</td><td>0</td><td>1</td><td>1</td></tr>
    <tr>
        <th class="rowHeader">
            <div class="digit digFive">
              <div class="segment segA"></div>
              <div class="segment segB"></div>
              <div class="segment segC"></div>
              <div class="segment segD"></div>
              <div class="segment segE"></div>
              <div class="segment segF"></div>
              <div class="segment segG"></div>
            </div>
            </th>
        <td>1</td><td>0</td><td>1</td><td>1</td><td>0</td><td>1</td><td>1</td></tr>
    <tr>
        <th class="rowHeader">
            <div class="digit digSix">
              <div class="segment segA"></div>
              <div class="segment segB"></div>
              <div class="segment segC"></div>
              <div class="segment segD"></div>
              <div class="segment segE"></div>
              <div class="segment segF"></div>
              <div class="segment segG"></div>
            </div>
        </th>
        <td>1</td><td>0</td><td>1</td><td>1</td><td>1</td><td>1</td><td>1</td></tr>
    <tr>
        <th class="rowHeader">
            <div class="digit digSeven">
              <div class="segment segA"></div>
              <div class="segment segB"></div>
              <div class="segment segC"></div>
              <div class="segment segD"></div>
              <div class="segment segE"></div>
              <div class="segment segF"></div>
              <div class="segment segG"></div>
            </div>
        </th>
        <td>1</td><td>1</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td></tr>
    <tr>
        <th class="rowHeader">
            <div class="digit digEight">
              <div class="segment segA"></div>
              <div class="segment segB"></div>
              <div class="segment segC"></div>
              <div class="segment segD"></div>
              <div class="segment segE"></div>
              <div class="segment segF"></div>
              <div class="segment segG"></div>
            </div>
        </th>
        <td>1</td><td>1</td><td>1</td><td>1</td><td>1</td><td>1</td><td>1</td></tr>
    <tr>
        <th class="rowHeader">
            <div class="digit digNine">
              <div class="segment segA"></div>
              <div class="segment segB"></div>
              <div class="segment segC"></div>
              <div class="segment segD"></div>
              <div class="segment segE"></div>
              <div class="segment segF"></div>
              <div class="segment segG"></div>
            </div>
        </th>
        <td>1</td><td>1</td><td>1</td><td>1</td><td>0</td><td>1</td><td>1</td></tr>
</table>

There are \\(2^7 = 128\\) possible combinations of seven segments, only ten of which are our standard digits. Therefore, the seven segments aren't on all turned on an equal number of times over the course of the ten digits.

TK - sum of above table with a heatmap of segments

How can we tell which of these seven segments communicates the most information?

## Information entropy

The segments that are on or off for close to half the digits contain more information than those that are either on or off for most digits. This is both intuitive and unintuitive (at least to me). It's intuitive for the same reason a fair coin toss contains more information than tossing a coin with heads on both sides: you're less certain what you're going to get, so learn more by observing the value. But it's unintuitive because if a segment is only not used in one digit --- like how segment C is only off for the digit 2 --- then if you happen to see a segment in that rare state, you know a lot about which digit it's displaying. But since you're relatively unlikely to see it in that state, the expected amount of information is low.

Claude Shannon's[^1] concept of entropy from information theory is a good way to quantify this problem. Entropy, \\(H\\), is defined as

$$H(X) = -\sum_{i = 1}^{n} P(x_i)\log_bP(x_i)$$

Oh no.

Here's what's that means in the case of a seven-segment display. \\(X\\) is a random variable representing whether a segment is on or off. Since a segment can only have two states, the random variable \\(X\\)'s actual values are either on or off. \\(P\\) is the probability operator, so \\(P(x_i)\\) really means the probability that a segment is on or off. (\\(b\\) is the base of the logarithm. We're going to use 2 because we like bits.)

Let's take segment A as an example. It's on for 8 out of 10 digits, and off for 2 out of 10. That means the probability of seeing it on is 0.8, and the probability of seeing it off is 0.2. In other words (well, symbols), \\(P(x_{\mathrm{on}}) = 0.8\\) and \\(P(x_{\mathrm{off}}) = 0.2\\).

Plugging that in,

$$H(A) = -0.8\log_2 0.8 - 0.2\log_2 0.2 = 0.722$$

In Shannon's terms, there are **0.722 bits** of information communicated by segment A of a seven-segment display.

Doing this for all seven segments, we get these entropy values:

TK - table of entropy values with heatmap

It sure looks like segments E and F carry the most information. That's expected because they're the closest to being on/off 50% of the time. Guess it's better to approach an intersection from the right in order to see the left-hand segments.

But wait.

When approaching an intersection, you can see *both* right segments (B and C), or *both* left segments (E and F). Entropy is additive between independent events, but a pair of segments from a single display are anything but independent.

Instead, treat each pair as if it holds a single value. Taken together, two segments can take on any of four values (off--off, off--on, on--off, on--on), which is binary for 0--3.

TK - table of digit, BC bin_seq, EF bin_seq

Working out the entropy for these, we get **1.16 bits** of information in joint segments B--C, and **1.90 bits** in joint segments E--F. So there you have it: it's still better to approach an intersection from the right.

But wait!

When was the last time you walked up to an intersection and only saw the timer on one number? If you look for at least half a second (on average), you'll see it count down. Luckily, [Wikipedia says](https://en.wikipedia.org/wiki/Entropy_(information_theory)#Data_as_a_Markov_process) that

> For a first-order Markov source (one in which the probability of selecting a character is dependent only on the immediately preceding character), the entropy rate is:

$$H(\mathcal{S}) = -\sum_i p_i\sum_jp_i(j)\log p_i(j)$$

> where \\(i\\) is a state (certain preceding characters) and \\(p_{i}(j)\\) is the probability of \\(j\\) given \\(i\\) as the previous character.

Alright, cool. Going back to the 0--3 binary sequence values, and defining previous values by assuming 0 loops back to 9 (which makes sense for the 1s place for segments B--C, but not for E--F), we get the following counts for segments B--C:

TK - table of value_given_prev for B--C

Now it's just a matter of an inelegant nested `for` loop to determine that the first-order entropy rate of segments B--C is **1.00 bits**, and **1.03 bits** for segments E--F.

So, if you can manage to stare at either the left or right segments for a whole second, you're still better off looking at the left segments, but not by much.

I'll leave figuring out the entropy rates for looking at it longer as an exercise for the reader.

[^1]: Shannon and I both got undergrad degrees in EE from the University of Michigan, but he went on to create information theory, and I went on to write this stupid blog post.

<script>
class {{ page.title | slugify | capitalize | replace: "-", "" }} {
  constructor(container) {
    this.container = container;
    this.segmentDigitTable =  this.container.select(".segmentDigitTable");
  }
}
let {{ page.title | slugify | replace: "-", "" }} = new {{ page.title | slugify | capitalize | replace: "-", "" }}(d3.select("#{{ page.title | slugify }}"));
</script>
