---
layout: post
title: "SuperCollider 3.8"
description: "SuperCollider 3.8 now available"
category: Releases
author: snappizz
tags: []
---

Version 3.8 is out! For this long-delayed release (the release date we had set was June 2016!), we spent a lot of time focusing on platform stability and consistency, so this version is light on new features and heavy on bugfixes. We expect a similar situation for 3.9, since we still didn't attend to everything we wanted in time for release.

If you're already using 3.7.x, an upgrade is strongly recommended -- there's only a handful of API changes in 3.8 and most of them are unlikely to affect users.

SuperCollider still has **486 open issues** and counting, so we need all the help we can get!

Here's a selection of notable changes in this release:

## General

- Improved support for building sclang without Qt.
- scvim is back in active development.
- The -v command-line option displays the commit.
  [#2243](https://github.com/supercollider/supercollider/pull/2243)
- Improved support for building on Raspberry Pi and similar systems.
  [#2065](https://github.com/supercollider/supercollider/pull/2065)

## scsynth and supernova

- A new command-line option for scsynth, -B, allows binding to a specific address.
  [#2095](https://github.com/supercollider/supercollider/pull/2095)
- VOsc supports an audio-rate phasein argument.
  [#2140](https://github.com/supercollider/supercollider/pull/2140)
- TGrains supports numChannels set to 1.
  [#2136](https://github.com/supercollider/supercollider/pull/2136)
- The order of audio ports can be manually set using the JACK metadata API.
  [#1951](https://github.com/supercollider/supercollider/pull/1951)
- Rare explosions in Gendy1, Gendy2, and Gendy3 have been fixed.
  [#2331](https://github.com/supercollider/supercollider/pull/2331)
- DemandEnvGen overshooting problems have been fixed.
  [#2164](https://github.com/supercollider/supercollider/pull/2164)
- PartConv no longer duplicates the first section of its impulse response.
  [#2015](https://github.com/supercollider/supercollider/pull/2015)

## Language, class library, and help files

- New methods: TreeView:addChild, TreeView:insertChild, and TreeView:childAt.
  [#2260](https://github.com/supercollider/supercollider/pull/2260)
- New method: NodeProxy:trace, for debugging.
  [#2020](https://github.com/supercollider/supercollider/pull/2020)
- New methods: Function:plotAudio, Bus:plotAudio.
  [#1846](https://github.com/supercollider/supercollider/pull/1846)
- It is now easier to insert custom views, in particular subclasses of SCViewHolder, into layouts.
  [#2188](https://github.com/supercollider/supercollider/pull/2188)
- The main help file is now titled with "SuperCollider [version]" rather than "Help."
  [#1928](https://github.com/supercollider/supercollider/pull/1928)
- A Float:asStringPrec crash has been fixed.
  [#2168](https://github.com/supercollider/supercollider/pull/2168)
- NetAddr.matchLangIP has been reimplemented to fix several bugs.
  [#1972](https://github.com/supercollider/supercollider/pull/1972)
- The second argument of String:replace now defaults to an empty string.
  [#2433](https://github.com/supercollider/supercollider/pull/2433)
- The "Writing UGens" documentation has been expanded.
  [#1997](https://github.com/supercollider/supercollider/pull/1997)
- Error handling has been improved in Server:record.
  [#1580](https://github.com/supercollider/supercollider/issues/1580)
- TChoose.ar now works correctly for audio-rate inputs.
  [#1979](https://github.com/supercollider/supercollider/pull/1979)
- A crash has been fixed when using a class name as a selector.
  [#2166](https://github.com/supercollider/supercollider/pull/2166)

## IDE

- The middle mouse button now closes tabs.
  [#2083](https://github.com/supercollider/supercollider/pull/2083)
- A new menu entry, Language > Quarks, launches Quarks.gui.
  [#1867](https://github.com/supercollider/supercollider/pull/1867)

## API changes

- The default number of audio bus has been increased from 128 to 1024.
  [#2239](https://github.com/supercollider/supercollider/pull/2239)
- TGrains, GrainBuf, GrainSin, GrainFM, and GrainIn now have unified panning behavior when numChannels is 2 and the pan exceeds the range [-1, 1].
  [#2136](https://github.com/supercollider/supercollider/pull/2136)
- Several old methods have been deprecated from PathName: \*fromOS9, foldersWithoutCVS, isCVS, foldersWithoutSVN, isSVN, filesDoNoCVS, filesDoNoSVN, streamTreeNoCVS.
  [#1909](https://github.com/supercollider/supercollider/issues/1909)
- The argument "startframe" has been renamed to "startFrame" and "aSoundFile" to "soundFile" in the following methods of SoundFileView: loadFile, setData, readFile, read, readFileWithTask, readWithTask.
  [#1684](https://github.com/supercollider/supercollider/pull/1684)