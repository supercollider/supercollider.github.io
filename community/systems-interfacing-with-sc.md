---
layout: catpage
title: "Systems interfacing with SC"
description: ""
category: "community"
sort_order: 5
---


There are various ways to use SC with other applications. By sending
[Open Sound Control OSC] network messages to the SC Server one can
control sound processes from other clients.

To send osc messages from the shell (terminal) see [sendOSC][].

Clients Using SC Server
-----------------------

-   Scheme
    -   [rsc3][] is an [r6rs scheme][] supercollider client.
-   Haskell
    -   [hsc3][] is a [haskell][] supercollider client.
    -   [Vivid][] is a haskell supercollider client.
    -   [Tidal][] is a pattern live coding language built on Haskell, controlling a backend written in SuperCollider.
-   SmallTalk
    -   A squeak OSC-Client by Marcus Gälli, which works with SC:
        [OSC-Client][]
-   Perl
    -   Alex McLean's article [“Hacking Perl in Nightclubs”][]
-   Impromptu
    -   SCIMP, an SC Server library for Impromptu (Scheme) [Impromptu
        Libraries][]
-   Python
    -   scosc, python OSC for supercollider:
        [<http://www.patrickkidd.com/>][]
    -   SC 0.3.1, python client for SuperCollider
        [<https://pypi.python.org/pypi/SC/0.3.1>][]
    -   [Supriya][]
-   Q
    -   Albert Graef lets his Q functional programming language for
        multimedia applications talk specially to SC3 through OSC:
        <http://q-lang.sourceforge.net/>
-   Pure
    -   Pure is the successor to Q: <http://purelang.bitbucket.org/>
    -   OSC is already [implemented][], but the SC3 interface needs to
        be ported from [Q][] to Pure
-   Java
    -   JCollider duplicates some of SCLang's client side representation
        classes to simplify the building of Java based clients (project
        is beta state): <http://www.sciss.de/jcollider>
-   Processing
    -   [P5_SC][] is a [Processing][] client for SC Synth. It
        replicates the main classes of SC-lang, e.g., Bus, Group,
        Buffer, Bus, etc.
-   CommonMusic
    -   See documentation: <http://commonmusic.sourceforge.net/cm2/doc/dict/supercollider-topic.html>
-   ML
    -   [smlsc3][] is a [Standard ML][] supercollider client.
-   Scala
    -   Scala provides type safety, and at the same time offers
        compactness that makes UGen graph creation look very close to
        their sclang equivalents.
        <http://github.com/Sciss/ScalaCollider>
-   Clojure
    -   [Overtone][] is a [Clojure][] based musical generation and
        manipulation system for live-coding and more.
-   Lua
    - [Lua2SC][] is a Lua client with ide, debugging...
-   Ruby
    - [Sonic Pi][] is a very popular live coding synth with SuperCollider as a server.

  [sendOSC]: http://archive.cnmat.berkeley.edu/OpenSoundControl/clients/sendOSC.html
  [rsc3]: http://slavepianos.org/rd/?t=rsc3
  [r6rs scheme]: http://www.r6rs.org/
  [hsc3]: http://www.slavepianos.org/rd/?t=hsc3
  [haskell]: http://www.haskell.org
  [OSC-Client]: http://map1.squeakfoundation.org/sm/accountbyid/13fa7a75-1e76-471e-8f42-b676f4d8e373/package/61f807be-83a3-4944-bfa1-686ddac7153c
  [“Hacking Perl in Nightclubs”]: http://www.perl.com/pub/a/2004/08/31/livecode.html
  [Impromptu Libraries]: http://impromptu.moso.com.au/libs.html
  [<http://www.patrickkidd.com/>]: http://www.patrickkidd.com/
  [<https://pypi.python.org/pypi/SC/0.3.1>]: http://pypi.python.org/pypi/SC/0.2
  [here]: http://jonathansaggau.com/sc/sclangEmacsPySCLang.rtf
  [implemented]: http://code.google.com/p/pure-lang/wiki/Addons#pure-liblo
  [Q]: http://q-lang.sourceforge.net/addons.html
  [P5_SC]: http://www.erase.net/projects/processing-sc/
  [Processing]: http://processing.org/
  [Page at sourceforge]: http://commonmusic.sourceforge.net/doc/cm.html
  [smlsc3]: http://www.slavepianos.org/rd/?t=smlsc3
  [Standard ML]: http://standardml.org/
  [Overtone]: http://github.com/overtone/overtone
  [Clojure]: http://clojure.org/
  [Lua2SC]: https://github.com/sonoro1234/Lua2SC
  [Vivid]: http://www.vivid-synth.com/
  [Tidal]: http://tidalcycles.org/
  [Sonic Pi]: http://sonic-pi.net/
  [Supriya]: https://github.com/josiah-wolf-oberholtzer/supriya

Editors
-------

-   [scvim][] VIM scripts for supercollider
-   Emacs - sc.el is included with the standard SuperCollider distribution
-   [Supercollider Atom](https://atom.io/packages/supercollider) Super Collider IDE for Atom
-   [Sublime Text](https://github.com/geoffroymontel/supercollider-package-for-sublime-text) Sublime Text
-   [supercollider-tmbundle](http://github.com/rfwatson/supercollider-tmbundle) TextMate
-   [sced](http://artfwo.googlepages.com/sced) a gedit plugin
-   [scate](http://github.com/jleben/Scate) a Kate plugin
-   [scfront](http://aug.ment.org/scfront) a Tcl/Tk frontend


GUI
---

-   [SwingOSC][] is an OpenSoundControl (OSC) server intended for
    scripting Java. It was written before SC had cross-platform unification
    of GUI, and is now no longer maintained.
-   [SCUM][] is an OpenSoundControl (OSC) GUI server based on FLTK.

Other Systems
-------------

-   [faust][] a functional language for real-time audio processing,
    which can compile DSP expressions to C++ SuperCollider plugin code
    (as well as to other formats).
-   [OpenObject][] a [quark][] for easily controlling synths with
    external applications (like Max, Pure Data, Processing, or
    openFrameworks) using OSC
-   [OctaveSC][] a class to interface with the free powerful math
    package [GNU Octave][] (GNU clone of MATLAB).
-   [vst2osc][]: sending osc messages from any VST-compatible
    application
-   [SuperColliderAU][]: AudioUnits wrapper for scsynth, now part of SuperCollider.
-   [javaosc][] a library for talking the Open Sound Control (OSC)
    protocol in Java.
-   communication from Cocoa with sc
    <http://www.illposed.com/software/objcosc.html>
-   a java based system for creation of spatialisation data:
    <http://sourceforge.net/projects/meloncillo/>
-   a java based sound editor using scsynth:
    <http://www.sciss.de/eisenkraut>
-   a soundfile segmentor that comes with supercollider classes:
    [Meapsoft][]
-   open sound control library for lisp [cl-osc][]

Hardware Connections
--------------------

-   [lemur-tutorial for supercollider][]
-   iPod Touch and iPhone OSC clients: [mrmr][] (open source,
    multi-user, server configured), [oscemote][] (auto-connect, UI
    customizable via html/css)
-   Chimaera documentation: direct conection via UDP/TCP to SuperCollider server [chimaera][]

  [scvim]: http://www.x37v.info/scvim/
  [sced]: http://artfwo.googlepages.com/sced
  [scate]: http://github.com/jleben/Scate
  [scfront]: http://aug.ment.org/scfront
  [supercollider-tmbundle]: http://github.com/rfwatson/supercollider-tmbundle/tree/master
  [SwingOSC]: http://sourceforge.net/projects/swingosc
  [SCVamp]: http://the3rd2nd.com/SCVamp/
  [SCUM]: SCUM "wikilink"
  [faust]: http://faust.grame.fr/
  [OpenObject]: http://www.fredrikolofsson.com/f0blog/?q=node/401
  [quark]: http://quarks.sourceforge.net/
  [OctaveSC]: http://www.sonification.de/projects/sc3/index.shtml
  [GNU Octave]: http://www.octave.org/
  [vst2osc]: http://peter1island.com/technicalStuff/audio-plugin/vst2osc-rtas2osc.php
  [SuperColliderAU]: http://doc.sccode.org/Guides/SuperColliderAU.html
  [javaosc]: http://www.illposed.com/software/javaosc.html
  [Meapsoft]: http://labrosa.ee.columbia.edu/meapsoft/docs.php
  [cl-osc]: http://fo.am/darcs/osc/
  [lemur-tutorial for supercollider]: http://www.jazzmutant.com/workshop_tutorialslist.php?id=supercollider
  [mrmr]: http://poly.share.dj/projects/#mrmr
  [oscemote]: http://lux.vu/blog/oscemote/
  [chimaera]: http://open-music-kontrollers.ch/chimaera/usage/#supercollider
