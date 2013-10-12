---
layout: post
title: "SuperCollider 3.3 released"
description: ""
category: releases
author: dan
tags: []
---
<p>We are pleased to announce that <strong>SuperCollider 3.3</strong> is now released.</p>
<p>Visit <a href="http://supercollider.sourceforge.net/downloads">the SuperCollider downloads page</a> to get binary or source-code downloads for your platform.</p>
<p>There are many changes since 3.2 (see <a title="SuperCollider 3.3 changelog" href="http://supercollider.svn.sourceforge.net/viewvc/supercollider/tags/3.3/build/ChangeLog">the changelog</a> for full detail) but here are some headlines:</p>
<ul>
<li><strong>GUI system updates</strong>: easier syntax, plus a major update of GUI documentation, as well as extra features such as modal sheets, SCLevelIndicator, and menu item manipulation</li>
<li><strong>New UGens</strong> added:
<ul>
<li>BEQSuite filter UGens (popular set of nice-sounding filters)</li>
<li>PartConv (efficient frequency-domain convolution)</li>
<li>SendReply (sends arrays from server to the language client)</li>
<li>VDiskIn (like DiskIn but with variable rate)</li>
<li>LFGauss</li>
</ul>
</li>
<li>Buffer recording/playback UGens used to be limited to 16-channel; now they can handle <strong>massively multi-channel</strong> audio</li>
<li><strong>SCImage</strong> for manipulating bitmap image objects (mac only)</li>
<li><strong>LocalBuf framework</strong> allows synths to create/free their own &#8220;private&#8221; buffers, simplifying buffer management in many situations</li>
<li>Various behind-the-scenes <strong>efficiency improvements</strong>, for a sleeker audio server that can do more on a given machine</li>
</ul>
<p> </p>
<p>(Note: the Windows build of 3.3 is still in alpha stages and so is not yet a &#8220;stable&#8221; release&#8230; watch this space)</p>
