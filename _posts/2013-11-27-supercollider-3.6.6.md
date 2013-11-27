---
layout: post
title: "SuperCollider 3.6.6"
description: ""
category: Releases
tags: []
---
{% include JB/setup %}

SuperCollider 3.6.6 is now available!

Since 3.6.5, there are many small bugfixes, so this is a recommended update. Notably, the Quarks system is updated to avoid a couple of recent issues. (Full changelog below.)

{% include download.md %}

{% comment %}
when later versions come out then these historical links might be useful.
for now just show current downloads

### Downloads ###

# Mac OS X (Universal Build):

http://sourceforge.net/projects/supercollider/files/Mac%20OS%20X/3.6/SuperCollider-3.6.6-OSX.dmg/download

# Windows (32 bit):

http://sourceforge.net/projects/supercollider/files/Windows/3.6/SuperCollider-3.6.6-win32.exe/download

# Sources:

http://sourceforge.net/projects/supercollider/files/Source/3.6/SuperCollider-3.6.6-Source.tar.bz2/download
http://sourceforge.net/projects/supercollider/files/Source/3.6/SuperCollider-3.6.6-Source-linux.tar.bz2/download

{% endcomment %}


### Changes since 3.6.5 ###

Bruno Ruviaro (1):
      help: changed .send(s) for .add in SynthDef example

Dan Stowell (13):
      linux: install 2 more files needed in dev headers: SCVersion.txt, SC_PlugIn.hpp
      Actually enable memory-checking code when in debug mode
      enable memory-checks only on special flag, not general debug
      class library: curvelin is now inverse of lincurve (UGen implementation)
      cmake: simplify qt-free build via SC_QT=False - fixes #959
      help doc: update to match the new syntax error output (thanks numb101). Fixes #981
      bump version number to 3.6.6
      fix outdated svn url in windows readme (thanks @bagong)
      Add warning about Mac OSX Mavericks (App Nap), thanks bagong
      On mac, remember to bundle README_OS_X.txt
      Import Rainer's rewritten OSX readme (from 315e60)
      update cmake for moved readme

Eirik Arthur Blekesaune (1):
      Pproto typo fix

Jakob Leben (6):
      scide: when saving document, automatically append ".scd" extension
      qtcollider: QUserView, QWindow: do refresh when "drawingEnabled==false"
      server: PortAudio: scale CPU load data to represent percentage
      scide: never close a session with unsaved documents
      Add win-rc-files for sclang and scide and and add icons to execs
      sclang: allow Windows path separator in code filename argument

James Harkins (14):
      Classlib: Pspawn resolved a function --> pattern prematurely
      Change "global variable" references where "environment variables" are meant
      MP tutorial 10: Fix typos in an example (one causing syntax error)
      platform: standalone's modifyStartup needs to initialize openPorts
      Library: Psync's cleanup was incorrect and could yield a redundant rest
      Library: Avoid redundant releases for rests in PmonoArticStream
      Library/PmonoArtic: Fix the case of a rest as the first event
      classlib (quarks): Defer svn path checking until needed; try{} the check
      Class library: Fix TempoClock CmdPeriod cleanup
      Class lib: PmonoStream: Fix cleanup bug (was adding cleanups for rests)
      Classlib: Pconst: Make sure Pconst returns the right inval
      Help: Process help: Document the important 'nowExecutingPath' method
      Help: String/Literal: Document escape character properly
      Classlib: Rest: Return a proper compileString for Rest instances

Julian Rohrhuber (9):
      class library: copy list before implictly removing items from it
      help: add a note about precision to Integer
      help: add a note about precision to Integer
      class library: when setting the bus, NodeProxy only rebuilds if really needed.
      class library: curvelin is now a proper inverse of lincurve (fix by james harkins).
      help: array.move
      examples: making ear training application compatible with QT
      class library: plot warns if Buffer is not allocated
      class library: plot now draws correct domain spec values

Michael Zacherl (1):
      HPF.schelp: Warning about frequencies close to 0.

Miguel Negrao (1):
      linux readme: qt5 limitation

Tim Blechmann (8):
      Revert "class library: jitlib - Avoiding sync problems with free/play"
      jitlib: explicitly take server latency into account
      plugins: fix substraction of kr - ar signals
      plugins: DiskIO ugens - remove limitation of channel count
      class library: fix curvelin
      plugins: FFT - clip window type to avoid crash
      plugins: FFT - fix invalid use of memcpy
      sclang: win32/msvc compile fixes

Yvan Volochine (2):
      Quarks: use new sf.net repo url
      boost: fix build error with recent versions of glibc

bagong (1):
      Minor enhancements after first rewrite

redFrik (1):
      midi type - fix for sending sysex

rs (18):
      Add Thumbs.db to ignored files
      For Windows install supernova to SuperCollider folder
      Add two icon-files for sclang and scide resource files
      Simplify Win-installer (remove options and comment out gedit related code)
      Register installer in Add-/Remove programs and remove registration on uninstall
      Associate filetypes sc scd and schelp with SC and attach cube icon
      Add Startmenu item (and try to remove it on uninstall)
      Brand installer, add welcome screens and use default texts where possible
      Small additions to Windows Readme
      Cleanup: remove unnecessary pseudo variable declarations
      Cleanup: remove defunct code after consultation with author
      Add QtCreator's CMakeLists.txt.user to ignored files
      RelPath cleanup a: move platform specific icons to platform/windows/Resources
      RelPath cleanup b: Make sc_cube.ico available to nsis install script
      RelPath cleanup c: change confusing semantics of var SC_SRC_DIR
      RelPath cleanup d: Adjust the NSIS script (and forgotten scide.rs) to preceding changes
      Add info about installing Quarks to Readme
      Enhance Quarks section in Windows readme

