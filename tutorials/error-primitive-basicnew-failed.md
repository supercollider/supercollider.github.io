---
layout: catpage
title: "ERROR: Primitive 'BasicNew' failed. Index not an Integer"
category: tutorials
---

If you're writing a SynthDef
----------------------------

It's quite likely that the error means you're trying to dynamically change the
number of channels inside a SynthDef, which is something you can't do -
SynthDefs need to have a fixed layout. For example, this is a simple attempt to
make pink noise over a variable number of channels:

{% highlight javascript %}
(
SynthDef(\thiswillfail, { |out=0, numChannels=2|
	Out.ar(out, {PinkNoise.ar}.dup(numChannels))
}).add
)
{% endhighlight %}

It fails because we're trying to make the number of pink noise generators
involved, actually changeable. You can't do that - when the SynthDef is
compiled, the language needs to know **exactly** how many UGens will be involved
and how they are connected. This is because a SynthDef represents an efficient
fixed-layout synth that the server can instantiate.

#### So what to do instead?

Think of SynthDefs as tiny fixed reusable components, and design your logic to
reuse them in whatever combinations are needed.

To go back to the simple example above (the pink noise generator), you could
simply do:

{% highlight javascript %}
(
SynthDef(\simplepink, { |out=0|
	Out.ar(out, PinkNoise.ar)
}).add
)
{% endhighlight %}

and create one \simplepink synth for each channel. Or you could create one
SynthDef for each number of channels you expect to use - for example if you
might use between 1 and 5 channels:

{% highlight javascript %}
(
(1..5).do{|n|
SynthDef("simplepink_%".format(n).asSymbol, { |out=0|
	Out.ar(out, {PinkNoise.ar}.dup(n))
}).add
}
)
{% endhighlight %}

Then you'd need to invoke \simplepink_4 or whatever, as appropriate.
