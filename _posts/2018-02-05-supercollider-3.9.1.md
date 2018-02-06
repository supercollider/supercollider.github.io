---
layout: post
title: "SuperCollider 3.9.1"
description: "SuperCollider 3.9.1 now available"
category: Releases
author: snappizz
tags: []
---

This is a bugfix release with no breaking changes. 3.9 users are advised to upgrade if possible.

Contributors to this release: antonhornquist, aspiers, brianlheim, cappelnord, florian-grond, gusano, jamshark70, patrickdupuis, redFrik, shimpe, telephon

- supernova only looked for plugins in a `plugins/` subfolder of the provided extensions directory. This has been fixed to be consistent with scsynth ([#3433](https://github.com/supercollider/supercollider/pull/3433)).
- Fixed `Index`, `IndexL`, `FoldIndex`, `WrapIndex`, `IndexInBetween`, and `DetectIndex` incorrectly downsampling audio-rate index arguments ([#3436](https://github.com/supercollider/supercollider/pull/3436)).
- The GUI class library folders were installed even when building sclang without Qt, resulting in unbound primitives. This has been fixed ([#3456](https://github.com/supercollider/supercollider/pull/3456)).
- Some default class library directories had to be manually created. sclang will now create them for you if they don't exist ([#3469](https://github.com/supercollider/supercollider/pull/3469)).
- Fixed a Routine not being properly terminated when running `CmdPeriod.run` (or hitting an equivalent shortcut) when a `Server:plotTree` window is open ([#3423](https://github.com/supercollider/supercollider/pull/3423)).
- Fixed `LevelIndicator:style_` doing nothing and printing the warning `Qt: WARNING: Do not know how to use an instance of class 'Meta_QLevelIndicatorStyle'` ([#3398](https://github.com/supercollider/supercollider/pull/3398)).
- Fixed `Git.checkForGit` returning `nil` ([#3445](https://github.com/supercollider/supercollider/issues/3445)).
- The SynthDef compiler optimizes `a + b.neg` to `a - b`, but other UGens that depend on `b.neg` would also be incorrectly removed in some cases. This has been fixed ([#3437](https://github.com/supercollider/supercollider/pull/3437)).
- In 3.9.0, the `group` key broke in the "grain" event type. This has been fixed ([#3483](https://github.com/supercollider/supercollider/pull/3483)).
- New IDE themes have been introduced for the editor and post window: Solarized, Solarized Dark, and Dracula ([#3412](https://github.com/supercollider/supercollider/pull/3412), [#3410](https://github.com/supercollider/supercollider/pull/3410)).
- Set the default font in the IDE for macOS to Monaco, instead of the rather silly non-monospace font that has been the SC default for over a decade ([#3404](https://github.com/supercollider/supercollider/pull/3404)).
- Fixed duplicate SCIDE icons in GNOME, and fixed the SCIDE icon looking wrong ([#3380](https://github.com/supercollider/supercollider/pull/3380)).
- Fixed SCDoc breaking with page titles containing a single quote character ([#3301](https://github.com/supercollider/supercollider/pull/3301)).
- Fixed an error due to lack of input sanitization when trying to open help (Cmd+D/Ctrl+D) or references (Cmd+U/Ctrl+U) on text containing a double quote character ([#3277](https://github.com/supercollider/supercollider/pull/3277)).

You can download SuperCollider 3.9.1 from [the release page](https://github.com/supercollider/supercollider/releases/tag/Version-3.9.1).
