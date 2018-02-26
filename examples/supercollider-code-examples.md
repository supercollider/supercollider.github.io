---
layout: catpage
title: "Code examples"
description: ""
category: "examples"
sort_order: 2
---


A babbling brook by [James McCartney 2007](http://www.listarc.bham.ac.uk/lists/sc-users-2007/msg02698.html).

```supercollider
{ ({RHPF.ar(OnePole.ar(BrownNoise.ar, 0.99), LPF.ar(BrownNoise.ar, 14)
* 400 + 500, 0.03, 0.003)}!2)
+ ({RHPF.ar(OnePole.ar(BrownNoise.ar, 0.99), LPF.ar(BrownNoise.ar, 20)
* 800 + 1000, 0.03, 0.005)}!2) }.play
```

more to come...
