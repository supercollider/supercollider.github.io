---
layout: post
title: "SuperCollider 3.6.5"
description: ""
category: Releases
tags: []
---

Due to a silly but important bug that sneaked into SuperCollider 3.6.4 and made
a simple "{SinOsc.ar}.scope" fail with an error, we have decided to do the next
bugfix release early. We took the opportunity to include a couple other
improvements as well.

So, here is SuperCollider 3.6.5.

Thanks to the community for quick feedback and contributions!

### Downloads ###

# Mac OS X (Universal Build):

http://sourceforge.net/projects/supercollider/files/Mac%20OS%20X/3.6/SuperCollider-3.6.5-OSX-universal.dmg/download
Old IDE:
http://sourceforge.net/projects/supercollider/files/Mac%20OS%20X/3.6/SuperCollider-3.6.5-OSX-universal-no-ide.dmg/download

# Windows (32 bit):

http://sourceforge.net/projects/supercollider/files/Windows/3.6/SuperCollider-3.6.5-win32.exe/download

# Sources:

http://sourceforge.net/projects/supercollider/files/Source/3.6/SuperCollider-3.6.5-Source.tar.bz2/download
http://sourceforge.net/projects/supercollider/files/Source/3.6/SuperCollider-3.6.5-Source-linux.tar.bz2/download


### Changes since 3.6.4 ###

Jakob Leben (10):
- sc class library: fix regression in Server:-scope
- scide: add "reset font size" action to post window and help browser
- scide: autocompletion: order methods by class hierarchy when class is known
- documentation: improve info on logical time, clocks and threads
- documentation: more info on threads, clocks and time
- sclang: PyrThread: ensure slot type safety
- documentation: clarify the functioning of Thread and Routine
- streamline README.txt
- documentation: improve thisFunction and thisFunctionDef
- bump version to 3.6.5

Julian Rohrhuber (3):
- sc class library: replacing the source of a node proxy led to hanging patterns
- sc class library: NodeProxy:cleanNodeMapnow works even if no settings are present
- fix typo /  removing the implication that ansi-C isn't appropriate

Michael Zacherl (5):
- In.schelp: replaced AudioIn w/ SoundIn in reference, added loudness warning in example section
- Knob.schelp: repositioned text in mouseOverAction example
- Klang.schelp: changed 'filter' to 'oscillator' in methods section
- DynKlang.schelp: changed 'filter' to 'oscillator' in methods section
- README.txt: reworked and simplified with focus on SC IDE and version 3.6

vividsnow (2):
- scdoc: Pseg: duration pattern in beats not seconds
- scdoc: add thisFunctionDef/thisFunction
