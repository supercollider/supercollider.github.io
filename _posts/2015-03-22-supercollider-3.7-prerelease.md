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
