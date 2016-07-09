---
layout: post
title: "SuperCollider 3.7.2"
description: "SuperCollider 3.7.2 now available"
category: Releases
author: snappizz
tags: []
---

This is old news by now, but please bear with us -- we forgot to update this website for the past few 3.7.x releases!

- 3.7.0 was released on 2016-03-13
- 3.7.1 was released on 2016-04-10
- 3.7.2 was released on 2016-06-03

Head to the [Downloads](/download) page to get 3.7.2.

3.7 is special since it marks our first release in a few years (not counting some prereleases in 2015). It's also significant since from here on, we'll be picking up the speed of 3.x versions. 3.8 is only a month or so away as of this writing.

3.7 can coexist with 3.6.6 and other SC versions. We recommend you backup your `sc_ide_conf.yaml` - settings from 3.6.6 should be forwards compatible, but using a 3.7 settings file in 3.6.6 may experience problems. This can be found in the user support folder (File > 'Open user support directory').

---

## Major changes since 3.6.6

* Cross-platform HID support using HIDAPI
* A new Quarks package management system which supports installing packages from Git or from local folders.
* JITlib has seen significant refactoring and new functionality (see the "JITLib Changes in 3.7" help file)
* IDE editor themes can now be saved/loaded.
* Many enhancements to IDE autocomplete, introspection, and workflow improvements.
* A new Download class, for easy http file download.
* GUI redirects have been removed, Qt is now the core UI toolkit in sclang
* The Image class has been resurrected.
* The Document class has been resurrected, allowing sclang interaction with IDE documents.