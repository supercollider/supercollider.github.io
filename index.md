---
layout: front
title: SuperCollider
tagline: Real time algorithmic music composition environment.
group: index
---

<div class="jumbotron">

    <p>SuperCollider is a platform for audio synthesis and algorithmic composition, used by musicians, artists, and researchers working with sound. It is free and open source software available for Windows, macOS, and Linux.</p>

    <p>SuperCollider features three major components:
      <ul>
        <li>scsynth, a real-time audio server, forms the core of the platform. It features 400+ unit generators ("UGens") for analysis, synthesis, and processing. Its granularity allows the fluid combination of many known and unknown audio techniques, moving between additive and subtractive synthesis, FM, granular synthesis, FFT, and physical modelling. You can write your own UGens in C++, and users have already contributed several hundred more to the sc3-plugins repository.</li>
        <li>sclang, an interpreted programming language. It is focused on sound, but not limited to any specific domain. sclang controls scsynth via Open Sound Control. You can use it for algorithmic composition and sequencing, finding new sound synthesis methods, connecting your app to external hardware including MIDI controllers, network music, writing GUIs and visual displays, or for your daily programming experiments. It has a stock of user-contributed extensions called Quarks.</li>
        <li>scide is an editor for sclang with an integrated help system.</li>
      </ul>
    </p>

    <p>SuperCollider was developed by James McCartney and originally released in 1996. In 2002, he generously released it as free software under the GNU General Public License. It is now maintained and developed by an active and enthusiastic community.</p>

    <ul class="callstoaction">
        <li><a href="/download.html">Download it now</a></li>
        <li><a href="/examples/audio-examples.html">Listen to some sounds</a></li>
    </ul>
</div>


<div class="row-fluid" class="main-page-examples">

  <h4>Examples</h4>

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
        amp: -15.dbamp,
        freq: 60,
        legato: 0.8,
        ffreq: Pseq((0..(durations.size * 4 - 1)).normalize, inf).linexp(0, 1, 100, 4000),
        dur: Pseq(durations, inf),
        bend: Pfuncn({ |x| if(x < (1/2), 0.4, 1) }, inf) <> Pkey(\dur),
    ]),
    Pbind(*[
        instrument: \hoover,
        amp: -12.dbamp,
        midinote: 74,
        dur: durations.sum * 2,
        sustain: 7,
    ])
]).play(TempoClock(210 / 60));
)
{% endhighlight %}

{% include screenshots.md %}

<ul>
  <li><a href="/examples/supercollider-code-examples.html">More examples</a></li>
  <li><a href="/examples/screenshots.html">Screen shots</a></li>
  <li><a href="/examples/audio-examples.html">Music</a></li>
</ul>

</div>


<div class="row-fluid" id="features">
  <h4>Features</h4>

  <span class="span4">
      <h6>Language - sclang</h6>
      <ul>
        <li>Single inheritance object-oriented and functional language</li>
        <li>Similar to Smalltalk or Ruby with syntax similar to C or Javascript</li>
        <li>Dynamically typed</li>
        <li>Constant time message lookup and real time garbage collection</li>
        <li>Functions as first class objects</li>
        <li>Closures are lexical, and scope is both lexical and dynamic</li>
        <li>Coroutines</li>
        <li>List comprehensions</li>
        <li>Partial application (explicit currying)</li>
        <li>Tail call optimization</li>
        <li>Class extensions</li>
        <li>Embedded subsystems for composing patterns and signal graphs</li>
        <li>Quarks package manager for code sharing</li>
        <li>Interactive programming and Live Coding</li>
    </ul>
  </span>
  <span class="span4">
      <h6>Server - scsynth</h6>
      <ul>
        <li>High quality accurate and efficient audio engine</li>
        <li>Fully adjustable sample rate (192k+) and block size</li>
        <li>32 bit float signal chain</li>
        <li>Sampling buffers use 64 bit float</li>
        <li>Fast and fluid control rate modulation</li>
        <li><a href="http://doc.sccode.org/Reference/Server-Command-Reference.html">Communicates via Open Sound Control</a> - TCP/UDP network communication</li>
        <li><a href="http://doc.sccode.org/Browse.html#UGens">Hundreds of UGens (unit generators)</a></li>
        <li>Simple ANSI C plugin API</li>
        <li>Hundreds more community contributed UGens</li>
        <li>Supports any number of input and output channels, ideal for <a href="http://www.beast.bham.ac.uk/">massively multichannel setups</a></li>
        <li>Multi-processor support using the Supernova server implementation</li>
      </ul>
  </span>
  <span class="span3">
      <h6>IDE / Application</h6>
      <ul>
        <li>Qt based cross platform Integrated Development Environment</li>
        <li>REPL for "select and call" interactive programming</li>
        <li>Qt powered GUI framework for building rich interfaces</li>
      </ul>
  </span>
</div>

<div id="download">{% include download.md %}</div>


<div class="row-fluid">
  <div class="span6">
    <h4>Mailing list</h4>
    <p>The community is very active and helpful, the center of activity.  Please do drop by.</p>
    <p><a href="http://www.birmingham.ac.uk/facilities/BEAST/research/supercollider/mailinglist.aspx">mailing list info</a></p>
    <p><a href="https://join.slack.com/t/scsynth/shared_invite/enQtMjk0MzA0NzgyOTkyLTYwNjdmYjFmNWY4NGIyZWM2YWY1NzZhMjM3MWQ0MmEwZTZkZDExOTRjMWI2NjBiMGQ1NTg1NDQyZjExNWFjZGM">Join us on Slack</a></p>
    <h4><a href="/contributing/index.html">Contributing</a></h4>
    <ul>
      <li><a href="https://github.com/supercollider/supercollider/issues">Github issue tracker</a></li>
      <li><a href="/contributing/index.html">Contribution guidelines</a></li>
      <li><a href="/community/code-of-conduct.html">Code of Conduct</a></li>
    </ul>
    <h4><a href="/development/repository.html">Developers</a></h4>
    <ul>
      <li><a href="/development/repository.html">Resources for SuperCollider development</a></li>
    </ul>
    <h4>Tutorials</h4>
    <ul>
      <li><a href="http://doc.sccode.org/Tutorials/Getting-Started/00-Getting-Started-With-SC.html">Getting started</a></li>
      <li><a href="/tutorials/">Tutorials list</a></li>
    </ul>
    <h4>Resources</h4>
      <ul>
        <li><a href="/pages.html">Wiki</a></li>
        <li><a href="http://supercollider.sourceforge.net/wiki/">(old) wiki</a></li>
        <li><a href="http://swiki.hfbk-hamburg.de/MusicTechnology/6">(really old) swiki</a></li>
      </ul>
  </div>

  <div class="span6">

    <h4>News and announcements</h4>
    <p>{% for post in site.posts limit: 7 %}
           <h6><a href="{{ post.url }}">{{ post.title }}</a></h6>
         {% endfor %}
        <a href="/archive.html">more...</a></p>


    <div class="book">
    <h4>The SuperCollider book on MIT Press</h4>
    <a href="https://mitpress.mit.edu/books/supercollider-book"><img src="/images/MIT-supercollider-book.jpg" alt="MIT SuperCollider Book" width="60%" height="auto"/></a>
    <blockquote>The SuperCollider Book is the essential reference to this powerful and flexible language, offering students and professionals a collection of tutorials, essays, and projects. With contributions from top academics, artists, and technologists that cover topics at levels from the introductory to the specialized, it is a valuable sourcebook both for beginners and for advanced users.</blockquote>
    <a href="http://supercolliderbook.net/">supercolliderbook.net</a>
    </div>
  </div>
</div>

<hr />

<div class="row-fluid">
  <div class="span6">
    <h4>Online</h4>
    <ul>
      <li><a href="http://sccode.org/">sccode.org</a> — collaborative coding</li>
      <li><a href="/community/blogs-and-sites.html">Blogs and sites</a></li>
      <li><a href="https://twitter.com/search?q=supercollider+play">SC tweets - tunes under 140 chars</a></li>
      <li><a href="https://soundcloud.com/groups/supercollider">Soundcloud</a></li>
      <li><a href="http://rosettacode.org/wiki/Category:SuperCollider">Rosetta Code</a></li>
      <li> Facebook Groups
        <ul>
          <li><a href="https://www.facebook.com/groups/supercollider/">SuperCollider (english-spoken)</a></li>
          <li><a href="https://www.facebook.com/groups/653670444775977/">SC Women</a></li>
          <li><a href="https://www.facebook.com/groups/770853403048489/">SuperCollider Italia</a></li>
          <li><a href="https://www.facebook.com/groups/109527502188/">SuperColliderMX</a></li>
          <li><a href="https://www.facebook.com/groups/630981953617449/">SuperColliderBR</a></li>
          <li><a href="https://www.facebook.com/groups/336468226443169/">SuperCollider Slovenija</a></li>
        </ul>
      </li>
      <li><a href="http://flickr.com/groups/supercollider/pool/">flickr</a></li>
      <li><a href="http://www.vimeo.com/tag:supercollider">Vimeo</a></li>
      <li><a href="http://www.youtube.com/view_play_list?p=B813D0BDF50705D9">YouTube</a></li>
      <li><a href="https://lists.skylined.org/mailman/listinfo/supercollider">SuperCollider Slovenija mailing list</a></li>
    </ul>
  </div>

  <div class="span6">
    <h4>Other scsynth clients</h4>
    <p>SuperCollider language is the reference spec, but there are many other client languages that use the scsynth server.</p>
    <ul>
    <li><a href="http://overtone.github.io/">Overtone</a> (Clojure)</li>
    <li><a href="http://www.sciss.de/scalaCollider/">Scalacollider</a> (Scala)</li>
    <li><a href="https://github.com/maca/scruby">scruby</a> (Ruby)</li>
    <li><a href="http://hackage.haskell.org/package/hsc3">hsc3</a>,<a href="https://github.com/kaoskorobase/hsc3-server">hsc3-server</a>,<a href="https://hackage.haskell.org/package/vivid">vivid</a> (Haskell)</li>
    <li><a href="https://github.com/crucialfelix/supercolliderjs">supercollider.js</a> (JavaScript)</li>
    <li><a href="https://github.com/sonoro1234/Lua2SC">Lua2SC</a> (lua)</li>
    </ul>
  </div>
</div>

{% comment %}
the cliche fork me ribbon
<a href="https://github.com/you"><img style="position: absolute; top: 0; right: 0; border: 0;" src="https://s3.amazonaws.com/github/ribbons/forkme_right_darkblue_121621.png" alt="Fork us on GitHub"></a>
{% endcomment %}
