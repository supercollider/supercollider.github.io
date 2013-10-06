---
layout: post
title: "SuperCollider source code now at GitHub"
description: ""
category: development
author: redfrik
tags: []
---

<p>News for SuperCollider developers: we&#8217;ve decided to use Github as the main host for our source code. So today we&#8217;ve switched over. We&#8217;re using a mixture of services from Sourceforge and Github, but <a href="https://github.com/supercollider/supercollider">the official source code repository is now at Github</a>. (Note that we&#8217;re also using Github&#8217;s issue tracker, so if you have a problem with SuperCollider you can <a href="https://github.com/supercollider/supercollider/issues">report issues</a> there.)</p>
<p>If you have your own git clone of supercollider, you should update it so it points at github. Here are the appropriate terminal commands:</p>
<pre>git remote rename origin sf
git remote add origin git@github.com:supercollider/supercollider.git
git fetch origin
# The following is for 3.5 and master branches. Do it for all the ones you have:
git branch --set-upstream master origin/master
git branch --set-upstream 3.5 origin/3.5</pre>
