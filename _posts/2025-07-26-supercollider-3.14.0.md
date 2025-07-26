---
layout: post
title: "SuperCollider 3.14.0"
description: "SuperCollider 3.14.0 now available"
category: Releases
author: dyfer
tags: []
---

We are pleased to announce the release of SuperCollider 3.14.0! The release is available here: https://github.com/supercollider/supercollider/releases/tag/Version-3.14.0

This version has a number of changes since SC 3.13. Highlights include:

- Sclang functions now support collecting arbitrary keyword arguments via `{ |...args, kwargs| kwargs }`
- The initialization sample of multiple UGens was fixed
- Documentation can now also be themed like the IDE
- Due to updated bundled boost libraries on macOS and Windows, FluCoMa UGens which were working under SuperCollider 3.13 are not compatible anymore with 3.14! Go to https://github.com/flucoma/flucoma-sc to check for compatible version.
  - This does not apply to other extensions - e.g. sc3-plugins version 3.13 will still work with SuperCollider 3.14, as the plugin interface was not changed
- Even though these are not as much of user-facing changes, there were countless structural upgrades: we migrated to Qt6, added and improved tests, updated 3rd-party libraries, updated the build system for most recent build tools, and adapted a new organizational structure for development

A big thank you to all developers for your contributions!
