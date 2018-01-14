---
layout: post
title: "SuperCollider 3.9"
description: "SuperCollider 3.9 now available"
category: Releases
author: snappizz
tags: []
---

We are proud to announce the arrival of SuperCollider 3.9.0! Apologies for being so far behind schedule; we hope the improvements you'll find here will more than make up for it. In 3.9.0, determined contributors have fixed some of SuperCollider's major cross-platform compatibility demons, addressed longstanding issues in the IDE and language, and added new features and bugfixes across the board.

[The full changelog](https://github.com/supercollider/supercollider/blob/b6de49d15742380a91623f2bf19061ed81472081/CHANGELOG.md) is very long. Here are the most important changes:

- **Breaking change:** The application binary interface (ABI) for server plugins has changed. This has an important impact: **plugin binaries compiled for SuperCollider 3.8 will not work with SuperCollider 3.9** and vice versa. You will need to use a new version of sc3-plugins as well if you are upgrading SC.
- **Breaking change:** Rests in the patterns system have been restructured. Instead of using the `isRest` event property, events are considered rests if one of their properties is a `Rest` object. You must use instances of `Rest` rather than the rest class itself -- use of `Rest` instead of `Rest()` is now deprecated.
- The UnitTest quark has been incorporated into the main repository. If you already have UnitTest installed, you should uninstall it to prevent duplicate class errors.
- Support for multiple sclang clients connecting to the same server is greatly improved.
- A new UGen, `Sanitize`, replaces infinities, NaNs, and subnormals with another signal, zero by default.
- Fixed numerous instances of UGens outputting an initial sample of garbage.
- Fixed help files failing to open on Windows if the user's name contains a non-ASCII character.
- New aliases for done actions, e.g. `Done.freeSelf == 2`, are introduced for better readability. See the `Done` helpfile for details.
- Deprecated `OSCresponder`, `OSCresponderNode`, `OSCpathResponder`, `AudioIn`, and `Speech`.
- Some Linux systems had unreadable font colors in the autocomplete tooltips. This has been (finally) fixed.

You can grab the latest version from the [release page](https://github.com/supercollider/supercollider/releases/tag/Version-3.9.0). Thanks for using SuperCollider!
