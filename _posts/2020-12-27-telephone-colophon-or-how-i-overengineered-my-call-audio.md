---
title: "Telephone colophon: Or, how I overengineered my call audio"
image: "/post-uploads/call-audio-routing/setup.png"
---

<style>
#{{ page.title | slugify }} .reaper {
    font-variant: small-caps;
}

</style>

Toward the beginning of the pandemic, a friend asked me how she could use an external vocal mic and a guitar with a pickup on [Zoom](https://zoom.us/) calls.
Sounds easy, right?

But to have the amount of control a musician really wants, it turned out to be a bit more involved.
Plus, when working from home for a microphone company, it's pretty common to use a decent mic in meetings.

This post explains the setup I've been using for my calls.

![desk with mic, headphones, and speakers]({{site.baseurl}}/post-uploads/call-audio-routing/setup.jpg)

Ingredients:

- Mic: [Shure SM57](https://www.shure.com/en-US/products/microphones/sm57)
- USB audio interface: [Behringer UMC202HD](https://www.behringer.com/product.html?modelCode=P0BJZ)
- Headphones
- [MacBook Pro](https://support.apple.com/kb/SP715?locale=en_US)
- DAW: [<span class="reaper">Reaper</span>](https://www.reaper.fm/)
- [BlackHole virtual audio driver](https://github.com/ExistentialAudio/BlackHole)
- Zoom or other video conferencing apps

The goals are:

1. Mix the mic or other inputs going into the USB interface in the DAW
2. Be able to hear/monitor the mix
3. Route the output of the DAW to a Zoom call
4. Be able to hear the far end of the call through the same headphones as monitoring the mix

## Get Blackhole

The key ingredient here is [BlackHole](https://github.com/ExistentialAudio/BlackHole), a virtual audio driver that acts as a passthrough from each input to the corresponding output[^loopback].
This actually needs two instances of BlackHole because Zoom can only send and receive from the first two channels of any audio interface.
Fortunately, they have [nice instructions](https://github.com/ExistentialAudio/BlackHole/wiki/Running-Multiple-BlackHole-Drivers) for getting that going.
I have one called BlackHole 16ch and one called BlackHole 2ch, which --- surprise --- have 16 channels and 2 channels, respectively.

The 16-channel BlackHole device will function as the Zoom speaker; the 2-channel BlackHole will be the Zoom "microphone".

## Set up an aggregate audio device

<span class="reaper">Reaper</span> will handle all of the audio routing, but since it doesn't support having different input and output devices, the first thing to do is create an [aggregate device](https://github.com/ExistentialAudio/BlackHole/wiki/Aggregate-Device) in Audio MIDI Setup.
This allows the system to treat multiple devices as a single device with all of the channels from the individual devices.
It doesn't really matter what order you add them to the aggregate device, but it should include both BlackHole devices and the audio interface.
I have the USB interface set to be the clock source, with the two BlackHole instances set for drift correction.

![audio midi setup screenshot]({{site.baseurl}}/post-uploads/call-audio-routing/audio-midi-aggregate-device.png)

## Route and mix in the DAW

Once I got the audio devices set up, I had to route everything in <span class="reaper">Reaper</span>.
The general approach is:

- The master out is going to Zoom, and my ears for monitoring  
    In other words, (almost) every track in the DAW is "normal" in the sense that what I hear is what the far end of the call hears
- The output of Zoom is *not* going to the master out, so it doesn't feed back

But before doing that, make sure <span class="reaper">Reaper</span> is set to use the aggregate device in the device preferences.

![Reaper device preferences]({{site.baseurl}}/post-uploads/call-audio-routing/reaper-device-prefs.png)

For every input I want to mix, I created a track.
Selecting the input for that track feels almost like just using the regular USB audio interface, but with a whole bunch of other channels thanks to being aggregated with BlackHole.

![Reaper input selection]({{site.baseurl}}/post-uploads/call-audio-routing/reaper-input-selection.png)

By default, <span class="reaper">Reaper</span> sends each track to the master out, but in order to hear live input, you have to arm the track and turn on record monitoring.

A fun bonus of routing through a DAW is that you can use plugins!
I use a simple NR plugin to deal with HVAC noise, and some compression.

The master out needs to go two places:

- The USB interface so you can hear in your headphones
- BlackHole, to get it into Zoom

So, from the master track's routing window, add outputs to the USB interface and the two channels of the 2-channel BlackHole interface.
The fader/mute button for the USB interface on the output routing of the master is how I adjust whether/how much of myself I want to monitor in my ears.

![master output routing]({{site.baseurl}}/post-uploads/call-audio-routing/master-routing.png)

That's it for everything I want to send to Zoom, but I still want to be able to hear the far end of the call.
I could just tell Zoom to send out to the hardware interface, but I want it in the DAW, too.
This is useful for recording a [tape sync](https://en.wikipedia.org/wiki/Phone-sync), and so you don't have to mess up your monitoring volume to change the volume of the far end.

For that, I created a special track and set its input to the 16--channel BlackHole instance.
When you set up Zoom to use a particular output device, it sends the audio to the first two channels, so I had to use channels 1 and 2.
Here's where the track becomes special: you have to make sure it doesn't send to the master out (it'll feed back if you do).
Instead, send it directly to the USB interface's out.

![zoom monitor routing]({{site.baseurl}}/post-uploads/call-audio-routing/zoom-monitor-routing-callout.png)

And that's it for the DAW.

## Set up Zoom

The basics of setting up Zoom are simple: it receives the master output of the DAW by setting its microphone to BlackHole 2ch, and setting the speaker to BlackHole 16ch sends the far end's audio to the DAW on channels 1 and 2 of BlackHole 16ch.
Since you can control the output level from the DAW, I maxed out Zoom's output and input faders and turned off the automatic gain control.

![zoom audio settings]({{site.baseurl}}/post-uploads/call-audio-routing/zoom-prefs-1.png)

That's really all you need for the basics, but Zoom has a bunch of cool [advanced audio settings](https://support.zoom.us/hc/en-us/articles/115003279466).
Under "Music and Professional Audio" you can tell Zoom to let you turn off all of its audio processing, sending "original sound".
This is great, because what's the point of having a decent mic if Zoom is going to band-limit and compress it to death?
You can also turn on stereo, but I only use that if I really need to, which is rare.
(Keep in mind that in order to actually activate these settings, you have to press "Turn on original sound" in the upper left of a call.)

![zoom advanced audio settings]({{site.baseurl}}/post-uploads/call-audio-routing/zoom-prefs-2.png)

## Bonus! Sharing system sound

Zoom can share system sound, but when using a setup like this, I don't recommend it.
Turning it on activates some sort of additional virtual audio device on the system, which can mess with things.
Remember that Zoom can only send audio out on the first two channels of a device.
Thankfully, the system isn't so limited.
To share system sound, I went back to Audio MIDI Setup and under Configure Speakers told it that for stereo out, BlackHole 16ch uses channels 3 and 4.

![Audio MIDI Setup speaker config]({{site.baseurl}}/post-uploads/call-audio-routing/audio-midi-blackhole-speakers.png)

Now I can set my system output device to BlackHole 16ch, make a new track in the DAW, set its input to BlackHole 16ch, and system sound comes in there.
So the far side of a Zoom call comes in on channels 1 and 2, and system sound on 3 and 4.

And that's it.
Happy calling!

[^loopback]: I used BlackHole because it's free and did what I needed. You can achieve the same thing much more easily with a nice UI using [Loopback](https://rogueamoeba.com/loopback/) from the excellent Rogue Amoeba.
