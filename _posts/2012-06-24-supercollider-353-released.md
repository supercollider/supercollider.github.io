---
layout: post
title: "SuperCollider 3.5.3 released"
description: ""
category: releases
author: redfrik
tags: []
---
<p>we have a new 3.5.3 bugfix release:</p>
<p>source tarballs:<br />
http://sourceforge.net/projects/supercollider/files/Source/3.5.3/SuperCollider-3.5.3-Source.tar.bz2<br />
http://sourceforge.net/projects/supercollider/files/Source/3.5.3/SuperCollider-3.5.3-Source-linux.tar.bz2</p>
<p>osx installer:<br />
http://sourceforge.net/projects/supercollider/files/Mac%20OS%20X/3.5.3/SuperCollider-3.5.3-OSX.dmg</p>
<p>win32 installer:<br />
http://sourceforge.net/projects/supercollider/files/Windows/3.5.3/SuperCollider-3.5.3-win32.exe</p>
<p>ubuntu debs (due to launchpad packaging hell currently one commit before<br />
3.5.3):<br />
https://launchpad.net/~supercollider/+archive/ppa</p>
<p>cheers, tim</p>
<p>changes since 3.5.2:<br />
Dan Stowell (6):<br />
LocalIn helpfile fix, thanks Bruno Ruviaro<br />
Fix scvim regsitry file for updated filename (thanks Carlo Capocasa)<br />
version number to 3.5.3<br />
Server helpfile: see-also reference docs<br />
SCVim.sc should not be executable<br />
cmake build system: use system boost libraries if available</p>
<p>Jakob Leben (1):<br />
cmake: fix Boost Thread linking on Windows</p>
<p>James Harkins (10):<br />
EnvGen_next_ak_nova: Hardcoded blocksize=64, change to<br />
inNumSamples<br />
Per Scott W., initSiblings is not needed<br />
Reinstate Mix.ar and Mix.kr, with rate checks<br />
Fix crossplatform fail: Scale.directory shouldn&#8217;t always depend<br />
on Document<br />
ListPatterns: offset.value omitted (inval) as an argument<br />
Fix PbindProxy:storeArgs - should NOT call &#8220;source&#8221; on keys in<br />
the array!<br />
Scale:degreeToRatio should handle degrees outside of one<br />
octave&#8217;s range<br />
More meaningful error message for too many selectors<br />
Explain the limitation on the number of selectors in one<br />
FunctionDef<br />
Correct spelling error</p>
<p>Jonatan Liljedahl (3):<br />
Methods.html: auto-redirect to Search if method not found<br />
SCDoc: fix detection of old format class docs<br />
Mix.ar was un-deprecated, so remove the deprecated method</p>
<p>Joshua Parmenter (2):<br />
fix scroll view problem for OS X 10.7.4<br />
update SC_DirUtils to look at the name of the app bundle on osx</p>
<p>Julian Rohrhuber (14):<br />
fix bugs due to wrong usage of partial application<br />
PV_BinShift helpfile improved<br />
PV_Diffuser helpfile improved<br />
reformat statement for readability (no change of functionality)<br />
helpfile improvements<br />
improve array helpfile<br />
add note to the loop argument of DiskIn (thanks Stefan).<br />
improve helpfile<br />
some helpfile improvements<br />
improve helpfile<br />
improve helpfile<br />
improve and simplify FFT overview helpfile: fix some errors in<br />
examples.<br />
improve and simplify IFFT helpfile.<br />
improve and simplify FFT helpfile, mention that hopsize must be<br />
larger than 0.0</p>
<p>Tim Blechmann (11):<br />
external libraries: update nova-tt (gcc 4.7 fix)<br />
supernova: correctly implement replace semantics for /s_new<br />
Help: Function.scope is not limited to OSX anymore<br />
cmake build system: locate server plugins on freebsd<br />
server: add support for RF64<br />
cmake build system: ensure boost include path for scsynth<br />
cmake build system: set boost library path<br />
cmake build system: link scapp with correct version of<br />
libboost_thread<br />
cmake build system: minor cleanup<br />
supernova: fix asynchronous commands for empty reply address<br />
common: fix non-apple builds</p>

					
