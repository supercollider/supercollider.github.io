---
layout: catpage
title: "Building from source"
published: true
category: development
---

To get the sources run this command in a terminal window:

	git clone --recursive https://github.com/supercollider/supercollider.git

Update with:

	git pull
	git submodule update

Many reported build problems are due to not updating submodules.  These are git repositories that SC depends on:

	git://github.com/timblechmann/nova-simd.git
    git://supercollider.git.sourceforge.net/gitroot/supercollider/nova-tt
    git://supercollider.git.sourceforge.net/gitroot/supercollider/boost-lockfree


See the files “README OS X”, “README LINUX”, “README WINDOWS”, “README IPHONE” which are in the “platform” folder. Those files tell you how to compile it!

See [Developer cheat sheet for git](developer-cheat-sheet-for-git.html)
