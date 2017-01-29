---
layout: catpage
title: GUI Design Project
category: gui-design-project
sort_order: 1
---

*N.B. The SuperCollider GUI project from 2011 has been abandoned.
We will eventually want to revive this, but as of January 2017, there
are much higher-priority issues facing development. These pages are
archived for historical purposes.*

The SuperCollider development community invites graphic designers and UI
specialists to create a unique and elegant look for its GUI controls
(buttons, sliders, knobs, etc.) Visual coherency of the interface
elements is essential for making a good first impression for any Open
Source project and for day to day work an elegant and uniform look makes
for an inspiring environment.

SuperCollider is a programming language and development environment for
real-time audio synthesis and algorithmic composition. Originally
released in 1996, it is now a widely used open source project that runs
on Mac, Linux, Windows, iOS and Android. It is renowned for its audio
quality, flexibility and efficiency. It is widely used by composers,
musicians, improvisers and media artists as well as by researchers. It
is taught in many universities, and is used in numerous research
projects, galleries, concerts and clubs.

However it must be admitted that SuperCollider does not have the sexiest
knobs.

Current State of GUI
--------------------

So far SuperCollider has a reputation for being primarily a text based
language without a substantial GUI, and there have been many interesting
works done that treat code as an art-form in itself and revel in the use
of pure code as an interface.

There does exist a full compliment of standard GUI controls (buttons,
sliders, knobs, etc.), but these lack the finesse and visual appeal that
inspire artists. GUI interfaces can be written in SuperCollider code to
create standard controls (knobs, buttons, faders etc.) and on a custom
canvas (like Processing, HTML5 Canvas etc). These interfaces are used in
building small applications, performance instruments, for use in
installations, and for creating experimental software that are works of
art in themselves. There also exist larger applications and specialized
libraries that automatically compose GUIs.

The environment has up until now used GUI controls that required
separate implementations for different OS, so now a true cross platform
GUI is being constructed using the Qt (pronounced "Qute") application
framework. The implementation will give it a uniform look across all
platforms (no native widgets) and will give SuperCollider an instantly
recognized and distinctive look.

Call for Designs
--------------------

For this new implementation the development community invites graphic
designers and UI specialists to submit designs for the standard
elements. The full set of elements that are needed can be seen on this
screenshot: [GUI
ELEMENTS](http://www.flickr.com/photos/55063999@N03/5110498719/in/pool-1575422@N22/).
View the [SuperCollider code to generate these
elements](gui-code).
Besides the elements in the screenshot, a check box, a radio button and
a tabbed view should also be provided.

Entries to this call should be submitted to the [SuperCollider GUI
Flicker group](http://www.flickr.com/groups/supercollidergui/pool/)
where members of the SuperCollider community will be able to view and
discuss the pros and cons of the design. The development community also
invites any interested party to make contact via
**supercollidergui@gmail.com** and welcomes advice regarding the project
from anyone experienced with designing a complete and coherent GUI.

While the designer is invited to be free and create, a few guidelines
have been established: [SuperCollider GUI Design
Guidelines](guidelines)

License: since SuperCollider is open-source (GPL) software, the designs
will need to be licensed accordingly - GPL v2 or later.

Proposals
---------

- [Ben de Silva's proposal](bens-proposal.md)
- [Jon Ovander's proposal](jons-proposal.jpg)
