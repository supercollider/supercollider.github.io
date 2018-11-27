---
layout: post
title: "SuperCollider 3.10.0"
description: "SuperCollider 3.10.0 now available"
category: Releases
author: brianlheim
tags: []
---

We are proud to announce the release of SuperCollider 3.10! It's been an arduous process; we've come
a long way, and we'll continue to polish things up in backward-compatible 3.10.x patch releases. We
hope you enjoy the countless new features and fixes contributed by our fantastic development
community.

Some of the more notable changes in this version include:

- Major UI updates to the IDE, including a better default theme and new built-in themes such as
  Solarized Light and Dark
- SerialPort is now available on Windows
- The Supernova server is now available in the release package for macOS
- Breaking change: Float:asString now always produces a decimal point, so 3.0.asString is now "3.0"
  instead of "3".
- Lots (100+) of new math functions are available in sclang
- Menu GUI components are available in sclang
- Fixed high CPU usage by sclang when built without Qt
- Fixes for file path encoding issues on Windows
- The web view backend used in the IDE help browser and WebView class changed from QWebKit to
  QWebEngine, which means the project now builds with Qt >= 5.7
- The project now supports building with Windows Visual Studio >= 2015

Check out "News in 3.10" in the IDE or the [full changelog](https://github.com/supercollider/supercollider/blob/Version-3.10.0/CHANGELOG.md)
for more information.  You can grab the latest version from the [release page](https://github.com/supercollider/supercollider/releases/tag/Version-3.10.0).

Thanks for using SuperCollider!
