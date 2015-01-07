---
layout: catpage
title: "User FAQ"
category: tutorials
---



This is the beginning of a FAQ for SuperCollider users. Eventually this
will be moved into the main documentation, but the wiki is a better
place to encourage community contributions.

Language (client) issues
------------------------

#### Calling gui primitives from a SystemClock routine

When calling gui primitives from a SystemClock routine will cause an
error:

e.g.

{% highlight javascript %}
SystemClock.sched(0,{ Window.new.front })
{% endhighlight %}

`
ERROR: Primitive '_SCView_New' failed.
Operation cannot be called from this Process. Try using AppClock instead of SystemClock.
`

To avoid this issue use the AppClock,

{% highlight javascript %}
AppClock.sched(0,{ Window.new.front })
{% endhighlight %}

or the defer method:

{% highlight javascript %}
SystemClock.sched(0,{ { Window.new.front }.defer })
{% endhighlight %}

#### Binary operations order

Because of the way SuperCollider evaluates expressions, the usual order
of execution of mathematical expressions is not respected. In
SuperCollider everything is an object, and evaluation happens from left
to right, so

{% highlight javascript %}
5 + 3 * 2
{% endhighlight %}

will evaluate as (5 + 3 ) \* 2.

This happens because the expression becomes:

{% highlight javascript %}
5.performBinaryOpOnSimpleNumber('+',3).performBinaryOpOnSimpleNumber('*',2) 
{% endhighlight %}

Therefore, in algebraic expressions parenthesis must be used when left
to right orders is not what is desired:

{% highlight javascript %}
5 + (3 * 2)
{% endhighlight %}


SynthDef Issues
---------------

#### Using “If” Statements inside a SynthDef

This is covered on the page [If statements in a SynthDef][]

#### ERROR: SynthDef not found

Sending a SynthDef to the server requires a little bit of time, which
means that running a block of code with both SynthDef definitions and
instances of those SynthDefs won't be guaranteed to work unless this
slight delay is accounted for. There are two main ways to do this:

First way: put the SynthDefs and the main code in a Task and put some
kind of .wait time between them.


{% highlight javascript %}
Task({
	(put your SynthDefs here)
	0.2.wait;
	(put the rest of your code here)
}).play;
{% endhighlight %}

Second way: use .sync:


{% highlight javascript %}
Routine({
	(put your SynthDefs here)
	s.sync; // assuming that 's' is the server
	(put the rest of your code here)
}).play
{% endhighlight %}

### FAILURE /s\_new alloc failed, increase server's memory allocation (e.g. via ServerOptions)

**What it means:** While initializing the unit generators in a new Synth
node, the server ran out of real-time memory.

**Solution:** Increase the amount of real-time memory available to the
server. This size is set, as the error message says, in the
*ServerOptions* object associated with the server. It is a server
startup option; you must quit the server and reboot it, or the new
setting will not take effect.

{% highlight javascript %}
myServer.quit;
myServer.options.memSize = 65536;  // e.g., could be different for you
myServer.boot;
{% endhighlight %}

*myServer.options.memSize* is given in KB. The default is 8192KB, or
8MB.

**What it *really* means:** Many unit generators require internal memory
buffers, such as delay lines, comb filters, allpass delays, some FFT
manipulators, reverb units etc. These internal buffers are not allocated
directly from the operating system, but rather from a “real-time memory
pool.” This is because direct allocation from the OS, by functions such
as *malloc()*, is not real-time safe. The OS may take too long to return
the new block, causing glitches in the audio. To solve this problem, the
server allocates a chunk of memory when it starts up and parcels it out
to unit generators as needed.

If you use a large number of delays, the server may run out of real-time
memory. The default 8192KB setting can support 47.55 seconds of delay at
a sampling rate of 44.1 kHz. This goes away quickly when using lots of
synths with multiple channels of delay.

**Alternate solution:** For delay units, you may use preallocated delay
buffers -- Buffer.alloc() -- and the “Buf” delay units: BufDelayN,
BufDelayL, BufDelayC, BufCombL etc. Buffer.alloc does not use the
real-time pool and is not subject to the memSize limitation. This
approach will not help with FFT units.



**Helpfile reference:**

-   ServerOptions

### “Array arguments”

Sometimes, you need to send an array to a series of Control inputs in a
SynthDef (often called “array arguments”).

{% highlight javascript %}
Synth(\xyz, [freqs: [300, 400, 500]]);
{% endhighlight %}

There are two primary ways to do this:

-   Supply a literal array -- \#[1, 2, 3] -- as the default for the
    argument name in the function. This is discussed in SynthDef's help
        file.

{% highlight javascript %}
SynthDef(\xyz, { |freqs = #[1, 2, 3]|
   ...
})
{% endhighlight %}

-   Or, use NamedControl. This is the only way to do it if you want to
    construct the array's size dynamically, or based on a variable. See
        NamedControl help.

{% highlight javascript %}
SynthDef(\xyz, {
   var freqs = NamedControl.kr(\freqs, #[1, 2, 3]);
   ...
});
{% endhighlight %}

#### Why does it have to be a literal array?

The reason comes from the process of building a SynthDef:

1.  First, look at the function arguments to figure out what the Control
    inputs should be.
2.  Then create Control units (usually just one, if they're all normal
    arguments without prefixes or special rates). Each channel is
    represented by an OutputProxy.
3.  Then run the SynthDef function, passing the output proxies to the
    arguments.
4.  Then sort the UGens into the right order, etc. etc.

To do steps \#1 and \#2, the SynthDef builder has to know the size of an
array argument *before* running the function. That's possible only if
it's a literal array: \#[1, 2, 3, 4, 5]. Any other array notation
creates the array *while running the function* (step \#3). But then it's
too late -- the SynthDef builder already created a non-array control
channel for it!

{% highlight javascript %}
SynthDef(\notArray, { arg a = (1..5);
   a.debug(“a is”);
});
{% endhighlight %}
`a is: an OutputProxy`

{% highlight javascript %}
SynthDef(\array, { arg a = #[1, 2, 3, 4, 5];
   a.debug(“a is”);
});
{% endhighlight %}
`a is: [ an OutputProxy, an OutputProxy, an OutputProxy, an OutputProxy, an OutputProxy ]`

(Note, if 'a' printed as [ 1, 2, 3, 4, 5 ], then you wouldn't be able to
change the values in a Synth using .set!)


Server issues
-------------

### How to trigger a function from the server

The first and most important point: **Functions are client-side only.**
The server doesn't know what functions are, doesn't understand them and
has no way to execute them. **Only the client can execute a function.**

Therefore, if you want a function to execute when something happens in
the server, the only way is for the server to tell the client to take
the action.

The server can communicate messages back to the client using one of two
unit generators: *SendTrig* and *SendReply*. *SendTrig* is simpler and
less flexible (it can send only a '/tr' message, and only one data
value). *SendReply* allows you to name the message anything you like,
and can send arrays with the message. We'll use SendReply here because
of its greater flexibility.

Within the language, you also need an object to receive the message and
act on it. Usually this is *OSCresponderNode* or *OSCpathResponder*. In
this example, *OSCpathResponder* filters messages not just on the name
'/bleep' but also on the synth's ID. This way, you could have multiple
triggering synths, with a different responder and a different action per
synth.

{% highlight javascript %}
(
a = {
   var trig = Dust.kr(8),
   decay = Decay2.kr(trig, 0.01, 0.1),
   sig = SinOsc.ar(TExpRand.kr(200, 600, trig), 0, 0.1) * decay;
   SendReply.kr(trig, '/bleep', trig);
   sig ! 2
}.play;

o = OSCpathResponder(s.addr, ['/bleep', a.nodeID], { |time, thisResponder, msg|
   msg.postln;
}).add;
)

a.free; o.remove;
{% endhighlight %}

**Helpfile references:**

-   SendTrig, SendReply
-   OSCresponderNode, OSCpathResponder, OSCresponder, OSC\_communication

### Exception in World\_OpenUDP: unable to bind udp socket

Sometime when booting the server one gets a message.

` Exception in World_OpenUDP: unable to bind udp socket `.

This is usually caused by an instance of scsynth that as hanged but has
not released the osc port, perhaps because it SuperCollider crashed. To
fix this, just hit the “k” button in the server window to kill all
scsynth processes, and then boot again.

Other issues
------------

### error while loading shared libraries: libsclang.so: cannot open shared object file

This usually happens after building on Linux and it means that your
system is unaware of newly installed shared libraries. Running ldconfig
(as root) solves the problem:

`# /sbin/ldconfig`
