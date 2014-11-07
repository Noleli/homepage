---
comments: true
date: 2011-06-21 07:52:59
slug: aesthetics-math-and-music
title: Aesthetics, math, and music
wordpress_id: 428
categories:
- Music
latex: true
---

I’ve been talking a lot lately with a [couple](http://twitter.com/#!/salliballi21) [friends](http://www.caitholman.com/) about what imbues music with emotion, why certain chords and intervals are more pleasant sounding than others, whether expectations about resolutions  are learned or somehow innate (e.g. I–IV–V7 seems to naturally want to only go to one place: I), and other similar questions. I’ve been saying that a lot of it has to do with the mathematics of music, so the relationship between aesthetics and mathematics was already on my mind when the post about the golden ratio and Apple’s iCloud icon [made its way around Twitter](http://alanvanroemburg.tumblr.com/post/6550997276/apple-icloud-icon-golden-ratio-alan-van-roemburg) the other day, and only made me more excited about that relationship.

[![icloud golden ratio]({{site.baseurl}}/post-uploads/icloud-golden-ratio.png){: .aligncenter}](http://alanvanroemburg.tumblr.com/post/6550997276/apple-icloud-icon-golden-ratio-alan-van-roemburg)

So with that motivation, here is a brief primer on the mathematics of music, particularly as it relates to intervals and tuning. It is adapted partially from a 2004 post I made to the AppleNova forum, and partially from some demos I put together (unassigned, of course) for a Physics of Music class I took in fall 2005.

Any interval between notes can be (in theory) defined is a ratio between frequencies, and intervals that have traditionally been considered consonant are part of the natural harmonic series, and therefore have low-integer ratios.

The harmonic series turns up in a couple places in music/audio. In audio, harmonics occur in all natural (i.e. non-synthesized) sounds. It’s the relative weighting of each of the harmonics that give each sound its unique timbre. I’m not really going to be talking about the harmonic/spectral breakdown of individual notes in this post, though. I’m just focusing on the relationship between notes and other notes — what I’m calling the harmonic series in music as opposed to in audio.

The [harmonic series](http://en.wikipedia.org/wiki/Harmonic_series_(mathematics)) is defined as \\(\frac{1}{1}, \frac{1}{2}, \frac{1}{3}, \dots, \frac{1}{n}\\). (Mathematicians, ever wonder why the harmonic series was called that? This is why.)

This makes the theoretical definition of the larger intervals easy. Taking A440 as an example:


<table>
	<tr><th>Degree</th><th><em>n</em></th><th>Frequency (Hz)</th></tr>
	<tr><td>Root</td><td>0</td><td>\(440\times 1 = 440\)</td></tr>
	<tr><td>Octave</td><td>1</td><td>\(440\times \left(1 + \frac{1}{1} \right) = 880\)</td></tr>
	<tr><td>5th</td><td>2</td><td>\(440\times \left(1 + \frac{1}{2} \right) = 660\)</td></tr>
	<tr><td>4th</td><td>3</td><td>\(440\times \left(1 + \frac{1}{3} \right) = 586\frac{2}{3}\)</td></tr>
	<tr><td>Major 3rd</td><td>4</td><td>\(440\times \left(1 + \frac{1}{4} \right) = 550\)</td></tr>
	<tr><td>Minor 3rd</td><td>5</td><td>\(440\times \left(1 + \frac{1}{5} \right) = 528\)</td></tr>
</table>


That’s where it stops working, though. Closer intervals don’t neatly obey the harmonic series. But you know something else about intervals that are not in the harmonic series? They’re perceived as dissonant. Interesting, eh?

Now, the reason I said that these are the frequencies of the notes _in theory_ is because that’s not how western music is actually tuned. The system outlined above is called [just intonation](http://en.wikipedia.org/wiki/Just_intonation); however, this system has several drawbacks, including the inability to be played equally in tune in any key, and intervals other than those listed above being constructed from large integer frequency ratios from much higher in the harmonic series.

Beginning in the late 16th century, a competing intonation system (that was much more difficult to obtain mathematically back in the day), [equal temperament](http://en.wikipedia.org/wiki/Equal_temperament), began to gain favor in Europe. (In fact, J.S. Bach’s [Well-Tempered Clavier](http://en.wikipedia.org/wiki/Well-Tempered_Clavier) was written in order to demonstrate equal temperament’s ability to be played in tune in all twelve major and minor keys.)

Equal temperament is based on the twelfth root of 2, \\(\sqrt[12]{2}\\), or, if you remember your root, fraction, and log identities, \\(2^\frac{1}{12}\\).

Again taking A440 as an example:



<table>
	<tr><th>Degree</th><th><em>n</em></th><th>Frequency (Hz)</th></tr>
	<tr><td>Root</td><td>0</td><td>440</td></tr>
	<tr><td>Half step</td><td>1</td><td>\(440 \times 2^\frac{1}{12} = 466.16\)</td></tr>
	<tr><td>Whole step</td><td>2</td><td>\(440 \times 2^\frac{2}{12} = 493.88\)</td></tr>
	<tr><td>Minor 3rd</td><td>3</td><td>\(440 \times 2^\frac{3}{12} = 523.25\)</td></tr>
	<tr><td>Major 3rd</td><td>4</td><td>\(440 \times 2^\frac{4}{12} = 554.37\)</td></tr>
	<tr><td>4th</td><td>5</td><td>\(440 \times 2^\frac{5}{12} = 587.33\)</td></tr>
	<tr><td>Tritone</td><td>6</td><td>\(440 \times 2^\frac{6}{12} = 622.25\)</td></tr>
	<tr><td>5th</td><td>7</td><td>\(440 \times 2^\frac{7}{12} = 659.26\)</td></tr>
	<tr><td>Minor 6th</td><td>8</td><td>\(440 \times 2^\frac{8}{12} = 698.46\)</td></tr>
	<tr><td>Major 6th</td><td>9</td><td>\(440 \times 2^\frac{9}{12} = 739.99\)</td></tr>
	<tr><td>Flat 7</td><td>10</td><td>\(440 \times 2^\frac{10}{12} = 783.99\)</td></tr>
	<tr><td>7th</td><td>11</td><td>\(440 \times 2^\frac{11}{12} = 830.61\)</td></tr>
	<tr><td>Octave</td><td>12</td><td>\(440 \times 2^\frac{12}{12} = 880\)</td></tr>
</table>



How different do these look and sound? These are two A major chords (of sine waves), one in just intonation, the other in equal temperament. (Excuse the JPEG compression artifacts. I made these in 2005 before PNG really caught on, and I don’t have access to MATLAB anymore.)

![A Major - Just Intonation]({{site.baseurl}}/post-uploads/A-Major-Just.jpg){: .aligncenter}



> [Listen to it!]({{site.baseurl}}/post-uploads/intonation/AMajorChordJust.wav)
>
> <audio src="{{site.baseurl}}/post-uploads/intonation/AMajorChordJust.wav" controls="controls"></audio>




![A Major - Equal Temperament]({{site.baseurl}}/post-uploads/A-Major-Equal.png){: .aligncenter}


> [Listen to it!]({{site.baseurl}}/post-uploads/intonation/AMajorChordEqual.wav)
>
> <audio src="{{site.baseurl}}/post-uploads/intonation/AMajorChordEqual.wav" controls="controls"></audio>




What you’ll notice is that the chord in equal temperament has imperfections and asymmetries that the just intonation one doesn’t. While this doesn’t have much impact because these are sine waves, you can imagine that when played on real instruments, the interactions between the upper harmonics would be much more complex in equal temperament.

When you listen to them, listen for the “[beats](http://en.wikipedia.org/wiki/Beat_(acoustics))” in equal  and notice how the are absent in just intonation, resulting in a more pure sound.

And for your listening pleasure, a C major scale with each note played in [Pythagorean](http://en.wikipedia.org/wiki/Pythagorean_tuning), just, and equal tunings.



> [Listen to it!]({{site.baseurl}}/post-uploads/intonation/CMajorComparisonScale.wav)
>
> <audio src="{{site.baseurl}}/post-uploads/intonation/CMajorComparisonScale.wav" controls="controls"></audio>




Here’s a [zip file]({{site.baseurl}}/post-uploads/intonation/IntervalExamples.zip) of all the sounds, graphs, and the MATLAB code to generate it. I haven’t looked at it in six years, but I assume it does something useful.
