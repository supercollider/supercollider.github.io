---
layout: post
title: "SuperCollider 3.9.3"
description: "SuperCollider 3.9.3 now available"
category: Releases
author: brianlheim
tags: []
---

This is a bugfix release with no breaking changes. 3.9 users are advised to upgrade if possible.

Contributors to this release: brianlheim, mneilsen, patrickdupuis, telephon

- It is now possible to build the project using a system install of yaml-cpp. Previously the `SYSTEM_YAMLCPP` CMake option was broken ([#3557](https://github.com/supercollider/supercollider/pulls/3557)).
- Improvements to documentation on writing and designing classes ([#3605](https://github.com/supercollider/supercollider/pulls/3605)).
- Fixed a regression from 3.8 to 3.9 that prevented the tilde character from being expanded to the user's home directory during class library compilation ([#3646](https://github.com/supercollider/supercollider/pulls/3646)).
- Fixed an issue with handling of ranges in `RangeSlider:setSpan` and `:setDeviation` ([#3620](https://github.com/supercollider/supercollider/pulls/3620)).
- Fixed a regression in `Score`'s multichannel expansion from 3.9.1 to 3.9.2 ([#3608](https://github.com/supercollider/supercollider/pulls/3608)).

You can download SuperCollider 3.9.3 from [the release page](https://github.com/supercollider/supercollider/releases/tag/Version-3.9.3).
