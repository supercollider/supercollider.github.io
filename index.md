---
layout: front
title: SuperCollider
tagline: Real-time algorithmic music composition environment.
group: index
---

SuperCollider is a platform for audio synthesis and algorithmic composition, used by musicians, artists, and researchers working with sound. It is free and open source software available for Windows, macOS, and Linux.

SuperCollider features three major components:

- **scsynth**, a real-time audio server, forms the core of the platform. It features 400+ unit generators ("UGens") for analysis, synthesis, and processing. Its granularity allows the fluid combination of many known and unknown audio techniques, moving between additive and subtractive synthesis, FM, granular synthesis, FFT, and physical modeling. You can write your own UGens in C++, and users have already contributed several hundred more to the sc3-plugins repository.

- **sclang**, an interpreted programming language. It is focused on sound, but not limited to any specific domain. sclang controls scsynth via Open Sound Control. You can use it for algorithmic composition and sequencing, finding new sound synthesis methods, connecting your app to external hardware including MIDI controllers, network music, writing GUIs and visual displays, or for your daily programming experiments. It has a stock of user-contributed extensions called Quarks.

- **scide** is an editor for sclang with an integrated help system.


SuperCollider was developed by James McCartney and originally released in 1996. In 2002, he generously released it as free software under the GNU General Public License. It is now maintained and developed by an active and enthusiastic community.


---


### Examples

- [Code examples](/examples/supercollider-code-examples.html)

<div class="row-fluid main-page-examples">

{% highlight javascript %}
// modulate a sine frequency and a noise amplitude with another sine
// whose frequency depends on the horizontal mouse pointer position
{
        var x = SinOsc.ar(MouseX.kr(1, 100));
        SinOsc.ar(300 * x + 800, 0, 0.1)
        +
        PinkNoise.ar(0.1 * x + 0.1)
}.play;
{% endhighlight %}


{% highlight javascript %}
// 60Hz Gabber Rave 1995
Server.default.boot;

(
SynthDef(\gabberkick, {
    var snd, freq, high, lfo;
    freq = \freq.kr(440) * (Env.perc(0.001, 0.08, curve: -1).ar * 48 * \bend.kr(1)).midiratio;
    snd = Saw.ar(freq);
    snd = (snd * 100).tanh + ((snd.sign - snd) * -8.dbamp);
    high = HPF.ar(snd, 300);
    lfo = SinOsc.ar(8, [0, 0.5pi]).range(0, 0.01);
    high = high.dup(2) + (DelayC.ar(high, 0.01, lfo) * -2.dbamp);
    snd = LPF.ar(snd, 100).dup(2) + high;
    snd = RLPF.ar(snd, 7000, 2);
    snd = BPeakEQ.ar(snd, \ffreq.kr(3000) * XLine.kr(1, 0.8, 0.3), 0.5, 15);
    snd = snd * Env.asr(0.001, 1, 0.05).ar(2, \gate.kr(1));
    Out.ar(\out.kr(0), snd * \amp.kr(0.1));
}).add;

SynthDef(\hoover, {
    var snd, freq, bw, delay, decay;
    freq = \freq.kr(440);
    freq = freq * Env([-5, 6, 0], [0.1, 1.7], [\lin, -4]).kr.midiratio;
    bw = 1.035;
    snd = { DelayN.ar(Saw.ar(freq * ExpRand(bw, 1 / bw)) + Saw.ar(freq * 0.5 * ExpRand(bw, 1 / bw)), 0.01, Rand(0, 0.01)) }.dup(20);
    snd = (Splay.ar(snd) * 3).atan;
    snd = snd * Env.asr(0.01, 1.0, 1.0).kr(0, \gate.kr(1));
    snd = FreeVerb2.ar(snd[0], snd[1], 0.3, 0.9);
    snd = snd * Env.asr(0, 1.0, 4, 6).kr(2, \gate.kr(1));
    Out.ar(\out.kr(0), snd * \amp.kr(0.1));
}).add;
)

(
var durations;
durations = [1, 1, 1, 1, 3/4, 1/4, 1/2, 3/4, 1/4, 1/2];
Ppar([
    Pbind(*[
        instrument: \gabberkick,
        amp: -23.dbamp,
        freq: 60,
        legato: 0.8,
        ffreq: Pseq((0..(durations.size * 4 - 1)).normalize, inf).linexp(0, 1, 100, 4000),
        dur: Pseq(durations, inf),
        bend: Pfuncn({ |x| if(x < (1/2), 0.4, 1) }, inf) <> Pkey(\dur),
    ]),
    Pbind(*[
        instrument: \hoover,
        amp: -20.dbamp,
        midinote: 74,
        dur: durations.sum * 2,
        sustain: 7,
    ])
]).play(TempoClock(210 / 60));
)
{% endhighlight %}

</div>


---


### Features


#### Language - sclang

  - Single inheritance object-oriented and functional language
  - Similar to Smalltalk or Ruby with syntax similar to C or Javascript
  - Dynamically typed
  - Constant time message lookup and real-time garbage collection
  - Functions as first-class objects
  - Closures are lexical, and scope is both lexical and dynamic
  - Coroutines
  - List comprehensions
  - Partial application (explicit currying)
  - Tail call optimization
  - Class extensions
  - Embedded subsystems for composing patterns and signal graphs
  - Quarks package manager for code sharing
  - Interactive programming and Live Coding



#### Server - scsynth

  - High quality accurate and efficient audio engine
  - Fully adjustable sample rate (192k+) and block size
  - 32-bit float signal chain
  - Sampling buffers use 64-bit float
  - Fast and fluid control rate modulation
  - [Communicates via Open Sound Control](http://doc.sccode.org/Reference/Server-Command-Reference) - TCP/UDP network communication
  - [Hundreds of UGens (unit generators)](http://doc.sccode.org/Browse.html#UGens)
  - Simple ANSI C plugin API
  - Hundreds more community contributed UGens
  - Supports any number of input and output channels, ideal for [large multichannel setups](http://www.beast.bham.ac.uk/)
  - Multi-processor support using the Supernova server implementation



#### IDE / Application

- Qt-based cross-platform Integrated Development Environment
- REPL for "select and call" interactive programming
- Qt powered GUI framework for building rich interfaces


#### External Systems
- [Systems that interface with SuperCollider](community/systems-interfacing-with-sc.md)


---


### Download
{% include download.md %}


---


### Community

#### Mailing list
The community is very active and helpful, the center of activity.  Please do drop by.

- [mailing lists](http://www.birmingham.ac.uk/facilities/BEAST/research/supercollider/mailinglist.aspx)
- [Join us on Slack](https://join.slack.com/t/scsynth/shared_invite/enQtMjk0MzA0NzgyOTkyLTYwNjdmYjFmNWY4NGIyZWM2YWY1NzZhMjM3MWQ0MmEwZTZkZDExOTRjMWI2NjBiMGQ1NTg1NDQyZjExNWFjZGM)


#### Contributing

- [Github issue tracker](https://github.com/supercollider/supercollider/issues)
- [Contribution guidelines](/contributing/index)
- [Code of Conduct](/community/code-of-conduct)


#### Developers

- [Source Code](/development/repository)

#### Tutorials

- [Getting started](http://doc.sccode.org/Tutorials/Getting-Started/00-Getting-Started-With-SC.html)
- [Tutorials list](/tutorials/)

#### Resources

- [Wiki](/pages)
- [(old) wiki](http://supercollider.sourceforge.net/wiki/)
- [(really old) swiki](http://swiki.hfbk-hamburg.de/MusicTechnology/6)


#### News and announcements

<p>
{% for post in site.posts limit: 4 %}
           <h6><a href="{{ post.url }}">{{ post.title }}</a></h6>
         {% endfor %}
        <a href="/archive.html">more...</a>

</p>


#### The SuperCollider Book on MIT Press

<a href="https://mitpress.mit.edu/books/supercollider-book"><img src="/images/MIT-supercollider-book.jpg" alt="MIT SuperCollider Book" width="35%" height="auto"/></a>
<blockquote>The SuperCollider Book is the essential reference to this powerful and flexible language, offering students and professionals a collection of tutorials, essays, and projects. With contributions from top academics, artists, and technologists that cover topics at levels from the introductory to the specialized, it is a valuable sourcebook both for beginners and for advanced users.</blockquote>
<a href="https://mitpress.mit.edu/books/supercollider-book">The SuperCollider Book</a>

#### Online

- [sccode.org](http://sccode.org/)
- [Blogs and sites](/community/blogs-and-sites)
- [SC tweets - tunes under 140 chars](https://twitter.com/search?q=supercollider+play)
- [Rosetta Code](http://rosettacode.org/wiki/Category:SuperCollider)
-  Facebook Groups
    - [SuperCollider (english-spoken)](https://www.facebook.com/groups/supercollider/)
    - [SC Women](https://www.facebook.com/groups/653670444775977/)
    - [SuperCollider Italia](https://www.facebook.com/groups/770853403048489/)
    - [SuperCollider Mexico](https://www.facebook.com/groups/109527502188/)
    - [SuperColliderBR](https://www.facebook.com/groups/630981953617449/)
    - [SuperCollider Slovenija](https://www.facebook.com/groups/336468226443169/)
- [SuperCollider Slovenija mailing list](https://lists.skylined.org/mailman/listinfo/supercollider)
