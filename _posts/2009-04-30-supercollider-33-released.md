---
layout: post
title: "SuperCollider 3.3 released"
description: ""
category: releases
author: dan
tags: []
---
We are pleased to announce that **SuperCollider 3.3** is now released.

Visit [the SuperCollider downloads page](http://supercollider.sourceforge.net/downloads) to get binary or source-code downloads for your platform.

There are many changes since 3.2 (see [the changelog](http://supercollider.svn.sourceforge.net/viewvc/supercollider/tags/3.3/build/ChangeLog) for full detail) but here are some headlines:

* **GUI system updates**: easier syntax, plus a major update of GUI documentation, as well as extra features such as modal sheets, SCLevelIndicator, and menu item manipulation
* **New UGens** added:
     * BEQSuite filter UGens (popular set of nice-sounding filters)
     * PartConv (efficient frequency-domain convolution)
     * SendReply (sends arrays from server to the language client)
     * VDiskIn (like DiskIn but with variable rate)
     * LFGauss
* Buffer recording/playback UGens used to be limited to 16-channel; now they can handle **massively multi-channel** audio
* **SCImage** for manipulating bitmap image objects (mac only)
* **LocalBuf framework** allows synths to create/free their own "private" buffers, simplifying buffer management in many situations
* Various behind-the-scenes **efficiency improvements**, for a sleeker audio server that can do more on a given machine

(Note: the Windows build of 3.3 is still in alpha stages and so is not yet a "stable" release - watch this space)
