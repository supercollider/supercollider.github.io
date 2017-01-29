---
layout: catpage
title: GUI Design Guidelines
category: gui-design-project
sort_order: 2
---

While the designer is invited to be free and create, a few guidelines
have been established:

Stylistic requirements
----------------------

-   Elegant, minimal, precise, readable, high contrast
-   No mad chrome, spaceship controls, excessive fake 3D, or that fake
    car radio look you see on Windows MP3 players.
-   We wish to avoid the currently popular totally flat 2D style that
    has become very common in Audio software: Ableton, TouchOSC, Reaktor
-   A slight 3D/raised look would be ideal, giving some sense of
    tactile controls.
-   OS neutral : not referencing or emulating the look of any of the
    operating systems (Cocoa/Aqua/Vista/XP)
-   Default design of the controls should be color-neutral (apart from
    minor elements like focus banding, selected text)
-   The controls will be style-able by users (colors, font, dimensions)
    so the design should not rely on strong primary colors.
-   The above implies that edge detail, elegant 3D (drop shadows,
    fading), and proportion are the primary aspects to be designed (but
    then again we aren't experts in this)
-   Note that sliders, buttons and knobs are size-able so the design
    needs to be implementable in a way that the edges can stretch

Suggestions, ideas to play with and aesthetic opinions
------------------------------------------------------

-   We associate ourselves stylistically more with projects like
    Processing and Max/PD than with commercial music software
-   The science-lab look of precision is a fetish we are fond of, but we
    want to look pretty too
-   More than one Slider(Fader) class may exist. One with calibration
    markings on them would be great
-   Programmers may add custom bitmaps as backgrounds to Sliders
    and Knobs. (If this doesn't fit with the design then a separate Slider/Knob
    class can be made that does and whose chrome won't conflict and also allows
    a bitmap for the handle)

Discussion
----------

A thread with discussion within the development community about the
project can be read
[here](http://www.listarc.bham.ac.uk/lists/sc-dev/thrd194.html#19324)
Advice and opinions on the project gratefully accepted. Feel free to
directly email anybody on the development list involved in the
discussion.

[Other Applications (to envy or
avoid)](other-applications)

[Example screenshots showing the current SuperCollider GUI can be found
on the Wikipedia](http://en.wikipedia.org/wiki/SuperCollider)
