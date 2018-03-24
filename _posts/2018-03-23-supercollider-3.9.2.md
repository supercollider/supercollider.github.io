---
layout: post
title: "SuperCollider 3.9.2"
description: "SuperCollider 3.9.2 now available"
category: Releases
author: brianlheim
tags: []
---

This is a bugfix release with no breaking changes. 3.9 users are advised to upgrade if possible.

Contributors to this release: adcxyz, brianlheim, davidgranstrom, jamshark70, patrickdupuis, snappizz, telephon, vivid-synth

- Improvements to various documentation pages ([#3587](https://github.com/supercollider/supercollider/pull/3587), [#3526](https://github.com/supercollider/supercollider/pull/3526))
- Fixed CMake configuration errors that prevented successfully building on Windows when the project path contains spaces ([#3525](https://github.com/supercollider/supercollider/pull/3525)).
- Fixed PSinGrain growing in amplitude after it was supposed to finish ([#3494](https://github.com/supercollider/supercollider/pull/3494)).
- sclang now creates a configuration directory on startup, rather than waiting for it to be created by another action. This step is skipped if sclang is run as a standalone (-a) or if a language config file is specified with the -l option ([#3577](https://github.com/supercollider/supercollider/pull/3577)).
- `SequenceableCollection:unixCmd` now allows respects `PATH` instead of strictly requiring the executable path ([#3501](https://github.com/supercollider/supercollider/pull/3501)).
- A new method, `Platform:killProcessByID`, was added ([#3499](https://github.com/supercollider/supercollider/pull/3499)).
- `LanguageConfig:store` throws an error if it fails to write ([#3577](https://github.com/supercollider/supercollider/pull/3577)).
- Fixed an off-by-one error in a warning message for `Server:clientID_` ([#3487](https://github.com/supercollider/supercollider/pull/3487)).
- `Event:isRest` now returns true if the event's `\isRest` entry is `true`. This usage was backported from 3.8 and is deprecated ([#3521](https://github.com/supercollider/supercollider/pull/3521)).
- `Server` now tries to recover in the case of a lost connection between client and server ([#3486](https://github.com/supercollider/supercollider/pull/3486)).
- Fixed an error when producing a `Score` containing an `Event` with a multichannel `timingOffset` ([#3544](https://github.com/supercollider/supercollider/pull/3544)).
- The help browser table of contents popout no longer has redundant "table of contents" text ([#3576](https://github.com/supercollider/supercollider/pull/3576)).

You can download SuperCollider 3.9.2 from [the release page](https://github.com/supercollider/supercollider/releases/tag/Version-3.9.2).
