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

### The Main Branch

SuperCollider's `main` branch is its stable branch. This branch contains only SuperCollider releases. The `main` branch can be considered stable production-ready code.

### The Development Branch

Main development is happening on the `develop` branch. Here, we develop everything that goes into the next *minor version* (e.g. 3.x) and beyond.

### Release Branches

Shortly before the release of a new *minor version*, a branch with the name of the version is created (e.g. `3.6`). Here, we only commit changes that **fix bugs**, not new features, and that are well tested to not cause any *regressions* (retrigger already fixed bugs or create new ones). In general, all commits should first go to the `develop` branch, and then be *cherry-picked* to release branches.

Before a new *patch version* (e.g. 3.6.x) is released, a branch with the name of the version is also created (e.g. `3.6.4`).

When a new *minor version* is released, its release branch is merged into `main`. When a new *patch version* is released, its branch is merged into `develop` and `main`.

### Topic Branches

These are branches dedicated to development of specific features. The names of such branches start with 'topic/' followed by the topic description (where words are usually separated with '-' or '_'). For example, the `topic/supernova_osx` branch is dedicated to development of support for Mac OS X in *supernova*.

The topic branches are meant as a way for others to test and review your work. A topic branch should be clean, free of any changes unrelated to the topic at hand. When work contained in a topic branch is considered ready for review, a pull request is created against the `develop` branch. After successful reviewing and testing by the community, the topic branch is *merged* into `develop`.

[sc-github]: https://github.com/supercollider/supercollider
[git]: http://git-scm.com/
