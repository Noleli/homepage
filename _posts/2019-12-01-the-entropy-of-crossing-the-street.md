---
title: "Entropic Timer: The Information Entropy of Crossing the Street"
latex: true
d3: true
---

<link rel="stylesheet" type="text/css" href="{{site.baseurl}}/post-uploads/7-segment-display/7-segment-display.css">

<style>
#{{ page.title | slugify }} .bigDigit {
  --height: 300px;
  margin-bottom: 15px;
}

#{{ page.title | slugify }} .digit.ticking {
  --height: 200px;
  margin-bottom: 15px;
}

#{{ page.title | slugify }} .digit {
  font-family: 'Helvetica', sans-serif;
}

#{{ page.title | slugify }} .digit .abMask {
  background-color: rgba(0, 0, 0, .6);
  grid-area: 1 / 1 / 9 / 4;
}

#{{ page.title | slugify }} .digit .efMask {
  background-color: rgba(0, 0, 0, .6);
  grid-area: 1 / 3 / 9 / 6;
}

#{{ page.title | slugify }} table .rowHeader .digit {
  --height: 32px;
  vertical-align: top;
}

#{{ page.title | slugify }} .segmentDigitTable td {
  vertical-align: middle;
}

#{{ page.title | slugify }} .digitTableContainer {
  display: flex;
}

#{{ page.title | slugify }} .digitTableContainer .digit {
  --height: 200px;
}

#{{ page.title | slugify }} .digitTableContainer .digit .label {
  font-size: 18px;
}

#{{ page.title | slugify }} .digitTableContainer .digit.heatmap .segA,
#{{ page.title | slugify }} .digitTableContainer .digit.heatmap .segB {
  --off-color: rgb(204, 0, 0);
}
#{{ page.title | slugify }} .digitTableContainer .digit.heatmap .segC {
  --off-color: rgb(229.5, 0, 0);
}
#{{ page.title | slugify }} .digitTableContainer .digit.heatmap .segD,
#{{ page.title | slugify }} .digitTableContainer .digit.heatmap .segG {
  --off-color: rgb(178.5, 0, 0);
}
#{{ page.title | slugify }} .digitTableContainer .digit.heatmap .segE {
  --off-color: rgb(102, 0, 0);
}
#{{ page.title | slugify }} .digitTableContainer .digit.heatmap .segF {
  --off-color: rgb(153, 0, 0);
}

#{{ page.title | slugify }} .digitTableContainer .digit.entropyHeatmap .segA,
#{{ page.title | slugify }} .digitTableContainer .digit.entropyHeatmap .segB {
  --off-color: rgb(184.091664, 0, 0);
}
#{{ page.title | slugify }} .digitTableContainer .digit.entropyHeatmap .segC {
  --off-color: rgb(119.593876, 0, 0);
}
#{{ page.title | slugify }} .digitTableContainer .digit.entropyHeatmap .segD,
#{{ page.title | slugify }} .digitTableContainer .digit.entropyHeatmap .segG {
  --off-color: rgb(224.729179, 0, 0);
}
#{{ page.title | slugify }} .digitTableContainer .digit.entropyHeatmap .segE,
#{{ page.title | slugify }} .digitTableContainer .digit.entropyHeatmap .segF {
  --off-color: rgb(247.592402, 0, 0);
}

</style>

You know those countdown timers at crosswalks? Sometimes when crossing the street, I like to try to guess what number it's on even when I can't see the whole thing (like when approaching the intersection at an oblique angle).

[![Crosswalk signal countdown timer]({{site.baseurl}}/post-uploads/7-segment-display/signal.jpg)](https://www.flickr.com/photos/thisisbossi/3361602602/)

This got me (over)thinking: if I want to know how much time is left, is it better to see the right side of the countdown timer (approaching from the left), or the left side (approaching from the right)? In other words, does the left or right side of the display carry more information?

These timers use [seven-segment displays](https://en.wikipedia.org/wiki/Seven-segment_display). Even if you didn't know they were called seven-segment displays, you see them all over the place. They use seven separate segments, labeled A–G, to create each of the 10 digits from 0–9.

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

To form each of the ten digits, the seven segments are turned on (1) or off (0) in different combinations. Here are the standard representations of 0–9.

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

The seven segments aren't on all turned on an equal number of times over the course of the ten digits. That means seeing some segments turned on is more probable than others.

<div class="digitTableContainer">
  <div class="digit heatmap">
    <div class="segment segA"></div>
    <div class="label segA">.8</div>
    <div class="segment segB"></div>
    <div class="label segB">.8</div>
    <div class="segment segC"></div>
    <div class="label segC">.9</div>
    <div class="segment segD"></div>
    <div class="label segD">.7</div>
    <div class="segment segE"></div>
    <div class="label segE">.4</div>
    <div class="segment segF"></div>
    <div class="label segF">.6</div>
    <div class="segment segG"></div>
    <div class="label segG">.7</div>
  </div>
  <table>
    <tr><th></th><th class="num">On for how many digits?</th></tr>
    <tr><th class="rowHeader">Segment A</th><td class="num">8/10</td></tr>
    <tr><th class="rowHeader">Segment B</th><td class="num">8/10</td></tr>
    <tr><th class="rowHeader">Segment C</th><td class="num">9/10</td></tr>
    <tr><th class="rowHeader">Segment D</th><td class="num">7/10</td></tr>
    <tr><th class="rowHeader">Segment E</th><td class="num">4/10</td></tr>
    <tr><th class="rowHeader">Segment F</th><td class="num">6/10</td></tr>
    <tr><th class="rowHeader">Segment G</th><td class="num">7/10</td></tr>
  </table>
</div>

So how can we tell which of these seven segments communicates the most information?

## Information entropy

The segments that are on or off for close to half the digits contain more information than those that are either on or off for most digits.
<!-- This is both intuitive and unintuitive (at least to me). -->
This is intuitive for the same reason a fair coin toss contains more information than tossing a coin with heads on both sides: you're less certain what you're going to get, so learn more by observing the value.
<!-- But it's unintuitive because if a segment is only not used in one digit --- like how segment C is only off for the digit 2 --- then if you happen to see a segment in that rare state, you know a lot about which digit it's displaying. But since you're relatively unlikely to see it in that state, the expected amount of information is low. -->

Claude Shannon's[^1] concept of entropy from information theory is a good way to quantify this problem. Entropy, \\(H\\), is defined as

$$H(X) = -\sum_{i = 1}^{n} P(x_i)\log_bP(x_i)$$

[Oh no](https://webcomicname.com/).

Here's what's that means in the case of a seven-segment display. \\(X\\) is a random variable representing whether a segment is on or off. Since a segment can only have two states, the random variable \\(X\\)'s actual values are either on or off. \\(P\\) is the probability operator, so \\(P(x_i)\\) really means the probability that a segment is on or off. (\\(b\\) is the base of the logarithm. We're going to use 2 because we like bits.)

Let's take segment A as an example. It's on for 8 out of 10 digits, and off for 2 out of 10. That means the probability of seeing it on is 0.8, and the probability of seeing it off is 0.2. In other words (well, symbols), \\(P(x_{\mathrm{on}}) = 0.8\\) and \\(P(x_{\mathrm{off}}) = 0.2\\).

Plugging that in,

$$H(A) = -0.8 \log_2 0.8 - 0.2 \log_2 0.2 = 0.722$$

In Shannon's terms, there are **0.722 bits** of information communicated by segment A of a seven-segment display.

Doing this for all seven segments, we get these entropy values:

<div class="digitTableContainer">
  <div class="digit entropyHeatmap">
    <div class="segment segA"></div>
    <div class="label segA">.72</div>
    <div class="segment segB"></div>
    <div class="label segB">.72</div>
    <div class="segment segC"></div>
    <div class="label segC">.47</div>
    <div class="segment segD"></div>
    <div class="label segD">.88</div>
    <div class="segment segE"></div>
    <div class="label segE">.97</div>
    <div class="segment segF"></div>
    <div class="label segF">.97</div>
    <div class="segment segG"></div>
    <div class="label segG">.88</div>
  </div>
  <table>
    <tr><th></th><th class="num">Shannon entropy</th></tr>
    <tr><th class="rowHeader">Segment A</th><td class="num">0.721928</td></tr>
    <tr><th class="rowHeader">Segment B</th><td class="num">0.721928</td></tr>
    <tr><th class="rowHeader">Segment C</th><td class="num">0.468996</td></tr>
    <tr><th class="rowHeader">Segment D</th><td class="num">0.881291</td></tr>
    <tr><th class="rowHeader">Segment E</th><td class="num">0.970951</td></tr>
    <tr><th class="rowHeader">Segment F</th><td class="num">0.970951</td></tr>
    <tr><th class="rowHeader">Segment G</th><td class="num">0.881291</td></tr>
  </table>
</div>

It sure looks like segments E and F carry the most information. That makes sense because they're the closest to being on/off 50% of the time. Guess it's better to approach an intersection from the right in order to see the left-hand segments.

But wait.

When approaching an intersection, you can see *both* right segments (B and C), or *both* left segments (E and F). A pair of segments from a single display are anything but independent because they're both showing part of the same digit, so we can't just add up their entropies.

Instead, treat each pair as if it holds a single value. Taken together, two segments can take on any of four values (off--off, off--on, on--off, on--on), which is binary for 0--3.

<table class="abBinTable segmentDigitTable">
  <tr><th></th><th>Segments B &amp; C</th><th>Binary</th><th>Decimal</th></tr>
  <tr>
    <th class="rowHeader num">
      <div class="digit digZero">
        <div class="segment segA"></div>
        <div class="segment segB"></div>
        <div class="segment segC"></div>
        <div class="segment segD"></div>
        <div class="segment segE"></div>
        <div class="segment segF"></div>
        <div class="segment segG"></div>
        <div class="abMask"></div>
      </div>
    </th><td>On – On</td> <td class="num">11</td><td class="num">3</td>
  </tr>
  <tr>
    <th class="rowHeader num">
      <div class="digit digOne">
        <div class="segment segA"></div>
        <div class="segment segB"></div>
        <div class="segment segC"></div>
        <div class="segment segD"></div>
        <div class="segment segE"></div>
        <div class="segment segF"></div>
        <div class="segment segG"></div>
        <div class="abMask"></div>
      </div>
    </th><td>On – On</td> <td class="num">11</td><td class="num">3</td>
  </tr>
  <tr>
    <th class="rowHeader num">
      <div class="digit digTwo">
        <div class="segment segA"></div>
        <div class="segment segB"></div>
        <div class="segment segC"></div>
        <div class="segment segD"></div>
        <div class="segment segE"></div>
        <div class="segment segF"></div>
        <div class="segment segG"></div>
        <div class="abMask"></div>
      </div>
    </th><td>On – Off</td><td class="num">10</td><td class="num">2</td>
  </tr>
  <tr>
    <th class="rowHeader num">
      <div class="digit digThree">
        <div class="segment segA"></div>
        <div class="segment segB"></div>
        <div class="segment segC"></div>
        <div class="segment segD"></div>
        <div class="segment segE"></div>
        <div class="segment segF"></div>
        <div class="segment segG"></div>
        <div class="abMask"></div>
      </div>
    </th><td>On – On</td> <td class="num">11</td><td class="num">3</td>
  </tr>
  <tr>
    <th class="rowHeader num">
      <div class="digit digFour">
        <div class="segment segA"></div>
        <div class="segment segB"></div>
        <div class="segment segC"></div>
        <div class="segment segD"></div>
        <div class="segment segE"></div>
        <div class="segment segF"></div>
        <div class="segment segG"></div>
        <div class="abMask"></div>
      </div>
    </th><td>On – On</td> <td class="num">11</td><td class="num">3</td>
  </tr>
  <tr>
    <th class="rowHeader num">
      <div class="digit digFive">
        <div class="segment segA"></div>
        <div class="segment segB"></div>
        <div class="segment segC"></div>
        <div class="segment segD"></div>
        <div class="segment segE"></div>
        <div class="segment segF"></div>
        <div class="segment segG"></div>
        <div class="abMask"></div>
      </div>
    </th><td>Off – On</td><td class="num">01</td><td class="num">1</td>
  </tr>
  <tr>
    <th class="rowHeader num">
      <div class="digit digSix">
        <div class="segment segA"></div>
        <div class="segment segB"></div>
        <div class="segment segC"></div>
        <div class="segment segD"></div>
        <div class="segment segE"></div>
        <div class="segment segF"></div>
        <div class="segment segG"></div>
        <div class="abMask"></div>
      </div>
    </th><td>Off – On</td><td class="num">01</td><td class="num">1</td>
  </tr>
  <tr>
    <th class="rowHeader num">
      <div class="digit digSeven">
        <div class="segment segA"></div>
        <div class="segment segB"></div>
        <div class="segment segC"></div>
        <div class="segment segD"></div>
        <div class="segment segE"></div>
        <div class="segment segF"></div>
        <div class="segment segG"></div>
        <div class="abMask"></div>
      </div>
    </th><td>On – On</td> <td class="num">11</td><td class="num">3</td>
  </tr>
  <tr>
    <th class="rowHeader num">
      <div class="digit digEight">
        <div class="segment segA"></div>
        <div class="segment segB"></div>
        <div class="segment segC"></div>
        <div class="segment segD"></div>
        <div class="segment segE"></div>
        <div class="segment segF"></div>
        <div class="segment segG"></div>
        <div class="abMask"></div>
      </div>
    </th><td>On – On</td> <td class="num">11</td><td class="num">3</td>
  </tr>
  <tr>
    <th class="rowHeader num">
      <div class="digit digNine">
        <div class="segment segA"></div>
        <div class="segment segB"></div>
        <div class="segment segC"></div>
        <div class="segment segD"></div>
        <div class="segment segE"></div>
        <div class="segment segF"></div>
        <div class="segment segG"></div>
        <div class="abMask"></div>
      </div>
    </th><td>On – On</td> <td class="num">11</td><td class="num">3</td>
  </tr>
</table>

<table class="efBinTable segmentDigitTable">
  <tr><th></th><th>Segments E &amp; F</th><th>Binary</th><th>Decimal</th></tr>
  <tr>
    <th class="rowHeader num">
      <div class="digit digZero">
        <div class="segment segA"></div>
        <div class="segment segB"></div>
        <div class="segment segC"></div>
        <div class="segment segD"></div>
        <div class="segment segE"></div>
        <div class="segment segF"></div>
        <div class="segment segG"></div>
        <div class="efMask"></div>
      </div>
    </th><td>On – On</td> <td class="num">11</td><td class="num">3</td>
  </tr>
  <tr>
    <th class="rowHeader num">
      <div class="digit digOne">
        <div class="segment segA"></div>
        <div class="segment segB"></div>
        <div class="segment segC"></div>
        <div class="segment segD"></div>
        <div class="segment segE"></div>
        <div class="segment segF"></div>
        <div class="segment segG"></div>
        <div class="efMask"></div>
      </div>
    </th><td>Off – Off</td> <td class="num">00</td><td class="num">0</td>
  </tr>
  <tr>
    <th class="rowHeader num">
      <div class="digit digTwo">
        <div class="segment segA"></div>
        <div class="segment segB"></div>
        <div class="segment segC"></div>
        <div class="segment segD"></div>
        <div class="segment segE"></div>
        <div class="segment segF"></div>
        <div class="segment segG"></div>
        <div class="efMask"></div>
      </div>
    </th><td>On – Off</td><td class="num">10</td><td class="num">2</td>
  </tr>
  <tr>
    <th class="rowHeader num">
      <div class="digit digThree">
        <div class="segment segA"></div>
        <div class="segment segB"></div>
        <div class="segment segC"></div>
        <div class="segment segD"></div>
        <div class="segment segE"></div>
        <div class="segment segF"></div>
        <div class="segment segG"></div>
        <div class="efMask"></div>
      </div>
    </th><td>Off – Off</td> <td class="num">00</td><td class="num">0</td>
  </tr>
  <tr>
    <th class="rowHeader num">
      <div class="digit digFour">
        <div class="segment segA"></div>
        <div class="segment segB"></div>
        <div class="segment segC"></div>
        <div class="segment segD"></div>
        <div class="segment segE"></div>
        <div class="segment segF"></div>
        <div class="segment segG"></div>
        <div class="efMask"></div>
      </div>
    </th><td>Off – On</td> <td class="num">01</td><td class="num">1</td>
  </tr>
  <tr>
    <th class="rowHeader num">
      <div class="digit digFive">
        <div class="segment segA"></div>
        <div class="segment segB"></div>
        <div class="segment segC"></div>
        <div class="segment segD"></div>
        <div class="segment segE"></div>
        <div class="segment segF"></div>
        <div class="segment segG"></div>
        <div class="efMask"></div>
      </div>
    </th><td>Off – On</td><td class="num">01</td><td class="num">1</td>
  </tr>
  <tr>
    <th class="rowHeader num">
      <div class="digit digSix">
        <div class="segment segA"></div>
        <div class="segment segB"></div>
        <div class="segment segC"></div>
        <div class="segment segD"></div>
        <div class="segment segE"></div>
        <div class="segment segF"></div>
        <div class="segment segG"></div>
        <div class="efMask"></div>
      </div>
    </th><td>On – On</td><td class="num">11</td><td class="num">3</td>
  </tr>
  <tr>
    <th class="rowHeader num">
      <div class="digit digSeven">
        <div class="segment segA"></div>
        <div class="segment segB"></div>
        <div class="segment segC"></div>
        <div class="segment segD"></div>
        <div class="segment segE"></div>
        <div class="segment segF"></div>
        <div class="segment segG"></div>
        <div class="efMask"></div>
      </div>
    </th><td>Off – Off</td> <td class="num">00</td><td class="num">0</td>
  </tr>
  <tr>
    <th class="rowHeader num">
      <div class="digit digEight">
        <div class="segment segA"></div>
        <div class="segment segB"></div>
        <div class="segment segC"></div>
        <div class="segment segD"></div>
        <div class="segment segE"></div>
        <div class="segment segF"></div>
        <div class="segment segG"></div>
        <div class="efMask"></div>
      </div>
    </th><td>On – On</td> <td class="num">11</td><td class="num">3</td>
  </tr>
  <tr>
    <th class="rowHeader num">
      <div class="digit digNine">
        <div class="segment segA"></div>
        <div class="segment segB"></div>
        <div class="segment segC"></div>
        <div class="segment segD"></div>
        <div class="segment segE"></div>
        <div class="segment segF"></div>
        <div class="segment segG"></div>
        <div class="efMask"></div>
      </div>
    </th><td>Off – On</td> <td class="num">01</td><td class="num">1</td>
  </tr>
</table>

In this case, our random variable \\(X\\) can take on four possible values rather than just two. Taking segments E and F as an example, the joint value is 0 for 3/10 digits, 1 for 3/10 digits, 2 for 1/10 digits, and 3 for 3/10 digits. Going back to the initial definition of entropy, we get

$$H(EF) = -\tfrac{3}{10}\log_2 \tfrac{3}{10} - \tfrac{3}{10}\log_2 \tfrac{3}{10} - .1\log_2.1 - \tfrac{3}{10}\log_2 \tfrac{3}{10} = 1.90$$

So we get **1.16 bits** of information in joint segments B--C, and **1.90 bits** in joint segments E--F. So there you have it: it's still better to approach an intersection from the right.

But wait!

When was the last time you walked up to an intersection and only saw the timer on one number? If you look for at least half a second (on average), you'll see it tick down.

<div class="digit ticking">
  <div class="segment segA"></div>
  <div class="label segA">A</div>
  <div class="segment segB"></div>
  <div class="label segB">B</div>
  <div class="segment segC"></div>
  <div class="label segC">C</div>
  <div class="segment segD"></div>
  <div class="label segD">D</div>
  <div class="segment segE"></div>
  <div class="label segE">E</div>
  <div class="segment segF"></div>
  <div class="label segF">F</div>
  <div class="segment segG"></div>
  <div class="label segG">G</div>
</div>

Luckily, [Wikipedia says](https://en.wikipedia.org/wiki/Entropy_(information_theory)#Data_as_a_Markov_process) that

> For a first-order Markov source (one in which the probability of selecting a character is dependent only on the immediately preceding character), the entropy rate is:

$$H(\mathcal{S}) = -\sum_i p_i\sum_jp_i(j)\log p_i(j)$$

> where \\(i\\) is a state (certain preceding characters) and \\(p_{i}(j)\\) is the probability of \\(j\\) given \\(i\\) as the previous character.

But actually, I don't like this notation, so I'm going to rewrite it as

$$H(\mathcal{S}) = -\sum_i P(x_i)\sum_j P(x_j|x_i)\log_b P(x_j|x_i)$$

Alright, then. The probability of seeing a given state is the same as before. As for the conditional probabilities, let's go back to the 0--3 binary values and assume 0 loops back to 9[^2]. If we see segments B and C in a 1 state (off--on), the next tick it will be in a 1 state half the time, and a 3 state half the time. Going through the rest of the states and transitions, we get these transition probabilities:

![State transition probabilities]({{site.baseurl}}/post-uploads/7-segment-display/transition-probabilities.svg)

So for segments E and F, when \\(i = 0\\) and \\(j = 2\\), \\(P(x_i) = \frac{3}{10}\\) as with before, and \\(P(x_j\|x_i) = \frac{1}{3}\\) because, as those circles show, a 0 transitions to a 2 a third of the time.

Now it's just a matter of an inelegant nested `for` loop to determine that the first-order entropy rate of segments B--C is **1.00 bits**, and **1.03 bits** for segments E--F.

So, if you can manage to stare at either the left or right segments for a whole second, you're still better off looking at the left segments, but not by much.

I'll leave figuring out the entropy rates for looking at it longer as an exercise for the reader.

---

The 7-segment display CSS is on [CodePen](https://codepen.io/noleli/pen/abbeWRL?editors=1100).

[^1]: Shannon and I both got undergrad degrees in EE from the University of Michigan, but he went on to create information theory, and I went on to write this stupid blog post.

[^2]: This makes sense for the 1s place for segments B--C, but not for E--F.

<script>
class {{ page.title | slugify | capitalize | replace: "-", "" }} {
  constructor(container) {
    this.container = container;
    this.tickingDigit =  this.container.select(".digit.ticking");
    this.digitClasses = ["digZero", "digOne", "digTwo", "digThree", "digFour", "digFive", "digSix", "digSeven", "digEight", "digNine"];

    this.startTick();
  }

  tick() {
    this.digitClasses.forEach((d, i) => {
      this.tickingDigit.classed(d, this.tickIndex == i);
    });
  }

  startTick() {
      this.tickIndex = 9;
      this.tick();
      setInterval(() => {
        this.tickIndex = this.tickIndex - 1 < 0 ? 9 : this.tickIndex - 1;
        this.tick();
      }, 1000);
  }
}
let {{ page.title | slugify | replace: "-", "" }} = new {{ page.title | slugify | capitalize | replace: "-", "" }}(d3.select("#{{ page.title | slugify }}"));
</script>
