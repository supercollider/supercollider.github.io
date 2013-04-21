---
layout: post
title: "SuperCollider 3.6.4"
description: ""
category: Releases
tags: []
---
{% include JB/setup %}

## SuperCollider 3.6.4 is released!

The release brings a bunch of small enhancements and important bugfixes to the
new IDE, steadily advancing its quality. Thanks to involvement of testers on
Mac OS X, some issues with key bindings specific to the platform have been
fixed. Moreover, the IDE on Mac OS X now uses a common global menu bar for all
its windows (including detached docklets).

There is also several bugfixes to the standard SC class library and core server
functionality, and improvements of documentation.

Enjoy SuperCollider 3.6.4!

{% include download.md %}

{% comment %}
when later versions come out then these historical links might be useful.
for now just show current downloads


### Downloads ###

# Mac OS X (Universal Build):

http://sourceforge.net/projects/supercollider/files/Mac%20OS%20X/3.6/SuperCollider-3.6.4-OSX-universal.dmg/download
Old IDE:
http://sourceforge.net/projects/supercollider/files/Mac%20OS%20X/3.6/SuperCollider-3.6.4-OSX-universal-no-ide.dmg/download

# Windows (32 bit):

http://sourceforge.net/projects/supercollider/files/Windows/3.6/SuperCollider-3.6.4-win32.exe/download

# Sources:

http://sourceforge.net/projects/supercollider/files/Source/3.6/SuperCollider-3.6.4-Source.tar.bz2/download
http://sourceforge.net/projects/supercollider/files/Source/3.6/SuperCollider-3.6.4-Source-linux.tar.bz2/download

{% endcomment %}


### Changes since 3.6.3 ###

Dan Stowell (1):
- SinOsc and Osc: note phase issue beyond +-8pi. Fixes #815     (cherry
     picked from commit 492954548083283d18fcc0f6bf391534d437deb8)

Jakob Leben (34):
- sclang: fix Char:-isUpper/isLower
- qtcollider: add QListView:-selectionAction
- qtcollider: add QListView:-selection setter
- scide: remove credits for kiberpipa
- help: GUI - improve documentation of alignment options
- help: add guide on creating standalone applications
- sc ide: show impl/ref lookup dialogs even when no text under cursor
- sc class library: ClassBrowser: fix search with empty query string
- sc ide: interpreter: post notification on quit or crash
- qtcollider: pass exit code up to SC_TerminalClient
- sc ide: fix and improve region detection
- sc ide: sc editor: add action to select pair of brackets enclosing cursor
- sc ide: sc editor: update bracket match highlight after applying settings
- qtcollider: QTextView: increase 'selectedString' compatibility, fix docs
- qtcollider: envelope view: fix drawing of quadratic and cubic curves
- sc ide: help browser: delegate docklet focus to webpage view
- sc ide: docklet: when focusing, also activate window
- sc ide: fix auto-indenting closing brackets on certain locales
- sc ide: ensure dock widgets within screen bounds when first undocked
- qtcollider: QTextView: set 'enterInterpretsSelection' to true by default
- scide: config dialog: preserve font when toggling "show only monospaced"
- scide: select line in code on triple click
- scide: ensure last active window activated after open/save file dialog
- scide: on startup, remove invalid file paths from "recent documents" list
- scide: improve default paths in open/save dialogs
- scide: save document dialog: always allow saving with any extension
- scide: editor: highlight unmatched brackets just like mismatched ones
- qtcollider: StackLayout: fix crash when removing contained widget
- qtcollider: do not allow reparenting layouts, to avoid crashing
- scide: fix closing tool panels on Escape
- scide: impl/ref lookup: close dialog when opening documentation for class
- Revert "Revert "scide: on Mac, make one global menu to share by all windows""
- scide: prevent erroneous overriding of shortcuts on Mac OS
- bump version to 3.6.4

James Harkins (2):
- Library: Bugfix for PmonoArtic inside other patterns w/cleanup
- Library: Fix Pfset passing child cleanups up to its parent(s)

Tim Blechmann (10):
- Help: fix rlpf help file
- plugins: DemandEnv - fix shape polling
- plugins: GrainBuf - catch both inf and NaN phase arguments
- scsynth: prevent possible buffer overflow
- cmake build system: fix x11 include paths
- class library: Bus - fix get method for multi-channel busses
- class library: Server.scope - remove limitation to 16 channels
- plugins: LocalOut - don't crash server if LocalIn is missing
- sclang: prevent buffer overflow
- scide: link with librt

Victor Bombi (1):
- supernova: CMakeLists.txt must set include dirs for fftw3f

attejensen (1):
- Update MIDI.schelp
