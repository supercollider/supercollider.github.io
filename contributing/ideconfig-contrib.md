---
layout: catpage
category: contributing
title: Setting up the IDE for easy contribution of sc-help and class library changes.
sort_order: 2
---

In order to simplify changing class files or help files and then contributing back the changes, it's easier to work directly with the git class library and schelp files tracked by git instead of the ones in the installation folder. To do this we can use the LanguageConfig feature:

In the IDE go to edit, preferences, interpreter then set the following options:

## OSX:

include paths:
* /Users/yourusername/...fill in your dev directory.../supercollider/SCClassLibrary

exclude paths:
* /Users/yourusername/...fill in your dev directory.../supercollider/build/Install/SuperCollider/SuperCollider.app/Contents/Resources/SCClassLibrary

## Linux:

include paths:
* /home/yourusername/...fill in your dev directory.../supercollider/SCClassLibrary

exclude paths:
* /usr/local/share/SuperCollider/SCClassLibrary/


