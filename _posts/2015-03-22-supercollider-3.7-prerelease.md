---
layout: post
title: "SuperCollider 3.7 prerelease"
description: "SuperCollider 3.7 prerelease builds are now available"
category: Releases
author: scztt
tags: []
---

# SuperCollider 3.7

SuperCollider 3.7.0 prerelease builds are now available. These will be released regularly until the application is considered stable and a release candidate is declared.

This release has been in continuous use during it's development, so it is considered stable enough for day-to-day use. It should be backwards compatibly with any code from 3.6.6. 

3.7 can coexist with 3.6.6 and other SC versions. We recommend you backup your `sc_ide_conf.yaml` - settings from 3.6.6 should be forwards compatible, but using a 3.7 settings file in 3.6.6 is not supported (though it may partially work). This can be found in the user support folder (File > 'Open user support directory').

**Builds available:**

- [alpha1](#alpha1)
- [alpha0](#alpha0)

---

## How can I help?

### Report bugs
Read the **[bug submission guidelines](/development/bugs.html#submitting-a-bug)**! 
Bugs can be submitted:

- From the application, via **Help > Report a bug...**
- From the [github issues page](https://github.com/supercollider/supercollider/issues/new?labels=bug&body=Bug%20description%3A%0A%0ASteps%20to%20reproduce%3A%0A1.%0A2.%0A3.%0A%0AActual%20result%3A%0A%0AExpected%20result%3A%0A)
- Without a GitHub account, from the [GitReports page](https://gitreports.com/issue/supercollider/supercollider)

Please run existing SC projects and report any significant failures or unexpected behaviors. This is also a chance to report long-standing issues that have not been addressed in 3.7. 

If you have access to uncommon hardware setups, or OS distributions, your testing is especially important! Please take a moment to smoke-test with your specialized linux distro or custom HID-based device and report back! 

### Help triage bugs 
SuperCollider currently has **345 open issues**, many of which are years old - as we beta test 3.7, we expect that number to increase. We need help dealing with new bugs, and sorting through old bugs and features (many of which may already be fixed). This is also a good chance to advocate for getting your (least) favorite bugs fixed.  Please read the **[bug triage guidelines](/development/bugs.html#triaging-a-bug)** and **ask on sc-users or sc-dev** if you would like to contribute to this process.

### Fix an easy bug
Simple-to-fix bugs and documentation / string issues are marked with the **[low hanging fruit](https://github.com/supercollider/supercollider/issues?q=is%3Aopen+label%3A%22low+hanging+fruit%22+label%3Abug)** label in the issues database. If you haven't contributed a pull request to SuperCollider before, or need an excuse to build locally, these are a good place to start.


### Write / review documentation
SuperCollider's documentation is always a work in progress. Classes in need of documentation can be found in the Help docklet, via Browse > Undocumented Classes). Or, walk through your own code, look up help on the Classes and Methods you're using, and document the ones that don't currently have documentation. 

---
## alpha1
*Windows builds are still in progress. Much progress has been made, but a few core issues have to be fixed before a working alpha build can be made available.*

### Downloads

[**Mac OS X (64-bit)**](https://github.com/supercollider/supercollider/releases/download/Version-3.7.0-alpha1/SuperCollider-Mac.zip)

**Windows (64 bit)** (not available yet) 

[**Source.zip**](https://github.com/supercollider/supercollider/archive/Version-3.7.0-alpha1.zip)

[**Source.tar.gz**](https://github.com/supercollider/supercollider/archive/Version-3.7.0-alpha1.tar.gz)

### Fixes since alpha0
- WebView closes after displaying scrollbar [1489](https://github.com/supercollider/supercollider/issues/1489)
- Plugin unload fixes [1473](https://github.com/supercollider/supercollider/issues/1473)
- Quarks windows path error bug [1451](https://github.com/supercollider/supercollider/issues/1451)
- Quarks conflicts with case insensitive file systems [1429](https://github.com/supercollider/supercollider/issues/1429)
- LanguageConfig.current problems (incorrect return value) [1369](https://github.com/supercollider/supercollider/issues/1369)
- installing local quark does not install it's dependencies [1378](https://github.com/supercollider/supercollider/issues/1378)
- quarks always go into default lang config file [1400](https://github.com/supercollider/supercollider/issues/1400)
- dependencies specified with git url and refspec not working [1377](https://github.com/supercollider/supercollider/issues/1377)
- canceling git checkout [1376](https://github.com/supercollider/supercollider/issues/1376)
- if sclang_config.yaml doesn't exist prior to install of Quark, include-path is not written [1362](https://github.com/supercollider/supercollider/issues/1362)
- Quarks install on Windows fails in parseQuarkName [1346](https://github.com/supercollider/supercollider/issues/1346)
- Error on interpreter startup [1448](https://github.com/supercollider/supercollider/issues/1448)
- Switching a session causes the IDE to segfault [1430](https://github.com/supercollider/supercollider/issues/1430)
- findRegexp does not compile escaped character sequences correctly [1411](https://github.com/supercollider/supercollider/issues/1411)
- Preferences/Editor/Fonts&Colors/Color:Current Line: sample text display doesn't update to the color selected in Text [1403](https://github.com/supercollider/supercollider/issues/1403)
- Remove cURL dependency in Quarks [1389](https://github.com/supercollider/supercollider/issues/1389)
- Add a way to update quarks (git pull or delete folder and clone again) [1386](https://github.com/supercollider/supercollider/issues/1386)
- GridLayout spanning bug [1383](https://github.com/supercollider/supercollider/issues/1383)
- fix DiskOut (last sample block not written) [1382](https://github.com/supercollider/supercollider/pull/1382)
- Server Gui volume bug [1370](https://github.com/supercollider/supercollider/issues/1370)
- default key for "trigger autocomplete" cmd-space conflicts with spotlight  [1365](https://github.com/supercollider/supercollider/issues/1365)
- addition of SimpleController::removeAt [1328](https://github.com/supercollider/supercollider/issues/1328)
- IDE passes wrong Document modifiers to mouseDownAction [952](https://github.com/supercollider/supercollider/issues/952)
- Wrongly reported external document changes [758](https://github.com/supercollider/supercollider/issues/758)
- Editing plotter with domainSpec bug [264](https://github.com/supercollider/supercollider/issues/264)
- MIDIFunc.noteOn does not work with floats [325](https://github.com/supercollider/supercollider/issues/325)
- sclang / scserver: print version with -V [1458(https://github.com/supercollider/supercollider/pull/1458)
- CoreMIDI crash fix [1147](https://github.com/supercollider/supercollider/pull/1147)

In addition, [crucialfelix](https://github.com/crucialfelix) committed numerous smaller cleanups and fixes for the new Quarks system.

## alpha0
*There are still build issues being sorted on Windows - these should be available in future prerelease iterations.*

### Downloads

[**Mac OS X (64-bit)**](https://github.com/supercollider/supercollider/releases/download/Version-3.7.0-alpha0/SuperCollider-Mac.zip)

**Windows (64 bit)** (not available yet) 

[**Source.zip**](https://github.com/supercollider/supercollider/archive/Version-3.7.0-alpha0.zip)

[**Source.tar.gz**](https://github.com/supercollider/supercollider/archive/Version-3.7.0-alpha0.tar.gz)

### Changes since 3.6.6
*3.7 spans roughly 2500 new commits, so the release notes represent only a high level overview. These will be expanded over time.*

**Features**

* Cross-platform HID support using HIDAPI
* A new Quarks package management system which supports installing packages from Git or from local folders.
* JITlib has seen significant refactoring and new functionality (see the "JITLib Changes in 3.7" help file)
* IDE editor themes can now be saved/loaded.
* Many enhancements to IDE autocomplete, introspection, and workflow improvements.
* A new Download class, for easy http file download.
* GUI redirects have been removed, Qt is now the core UI toolkit in sclang
* The Image class has been resurrected.
* The Document class has been resurrected, allowing sclang interaction with IDE documents.
*  ...

**Fixes**

A non-definitive list of issues fixed in 3.7 is available [here](https://github.com/supercollider/supercollider/issues?page=4&q=is%3Aissue+is%3Aclosed+label%3Abug+closed%3A%3E2013-11-27)
