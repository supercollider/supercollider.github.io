---
layout: catpage
category: development
title: Source Code Repository
sort_order: 1
---

SuperCollider source code is under [Git][git] source control management, and [hosted on GitHub][sc-github]

* **read-only:** <git://github.com/supercollider/supercollider.git>

    If you only want to get the latest source code, but you have no permission or intent to contribute, use the above URL.

* **read-write:** <git@github.com:supercollider/supercollider.git>

    In order to contribute, you need to have a GitHub account and be granted permission, then use the above URL.

For help with Git, see [Cheat Sheet for Git](git-cheat-sheet.html)

### The Master Branch

Main development is happening on the `develop` branch. Here, we develop everything that goes into the next *minor version* (e.g. 3.x) and beyond.

### Bugfix Branches

Shortly before the release of a new *minor version*, a branch with the name of the version is created (e.g. `3.6`). Here, we only commit changes that **fix bugs**, not new features, and that are well tested to not cause any *regressions* (retrigger already fixed bugs or create new ones). In general, all commits should first go to the `develop` branch, and then be *cherry-picked* to bugfix branches

When a *bugfix version* (e.g. 3.6.x) is released, its point on the bugfix branch is *tagged* (e.g. `Version-3.6.4`);

### Topic Branches

These are branches dedicated to development of specific features. The names of such branches start with 'topic/' followed by the topic description (where words are usually separated with '-' or '_'). For example, the `topic/supernova_osx` branch is dedicated to development of support for Mac OS X in *supernova*.

The topic branches are useful for experimental development, where it is not sure whether the development will be successful and useful enough to include it in the master branch. However, when the goal is approached successfully enough, the topic branch is *merged* into the master branch.

[sc-github]: https://github.com/supercollider/supercollider
[git]: http://git-scm.com/
