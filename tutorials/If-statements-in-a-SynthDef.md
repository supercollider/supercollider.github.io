---
layout: catpage
title: "If statements in a SynthDef"
---

### Introduction

It's only a matter of time before a user tries to write something like
this in a SynthDef:

{% highlight javascript %}
SynthDef(\kablooie, { |x = 0|
   var signal;
   if(x > 0) {
       signal = SinOsc.ar
   } {
       signal = Saw.ar
   };
});
{% endhighlight %}

... with the disturbing result:

`ERROR: Non Boolean in test.`

"Non Boolean in test"? But *x \> 0* is a comparison, and surely should
produce a Boolean, right?

This should be the first clue that Boolean logic in the server is a very
different animal from the so-called "normal" use of conditionals on the
client side (in the language).

### What is a Boolean in the server?

In fact, there is no such thing. The server handles floating-point
numbers. It doesn't have *true* or *false* entities.

Since everything in the server is a number, the result of the comparison
must also be a number. The server follows the same convention as other
DSP environments (Max/MSP, pd etc.):

- True is represented by 1.0
- False is represented by 0.0

### Why is x \> 0 "non-Boolean" in the "test"?

This goes back to the general issue of handling operators in the server.
Math operators in a SynthDef are not calculations to do *right now*.
They *describe* calculations that will be done *in the future*, many
thousands of times.

{% highlight javascript %}
var x = 1;
x > 0
{% endhighlight %}
`--> true`


{% highlight javascript %}
SynthDef(\kablooie, { |x = 0|
   "x: ".post; x.postln;
   "(x > 0): ".post; (x > 0).postln;
});
{% endhighlight %}

`x: an OutputProxy`

`(x > 0): a BinaryOpUGen`

The precise value of *x* is unknown at the time you execute the SynthDef
code. *x* actually represents an unlimited number of values, which will
be provided to Synths using argument lists. So, it's meaningless to
determine, once and for all, whether *x \> 0* or not. *x* may be *\> 0*
now and *\< 1* a split second later. So, instead of producing a Boolean,
*x \> 0* produces a **Binary Operator UGen** that repeatedly executes
the comparison.

Going back to this:

{% highlight javascript %}
if(aBinaryOpUGen) { ... } { ... };
{% endhighlight %}

To do this, the language must know which function (true or false) to
execute. But there is no way to know which one the BinaryOpUGen will be.
So, SuperCollider throws an error.

### If you can't branch, what good is a comparison in the server?

Comparisons have a lot of uses, actually.

-   **Choosing one of two signals:** This is the closest we can get to
    *if-then-else* in the server. Both *then* and *else* must be running
    continuously. That's a requirement of how the server works: the
    number and arrangement of unit generators within a single Synth
    cannot change. Instead, you can choose *which of those signals makes
    it downstream*. One will be used and the other ignored.\
    \
    Since true is 1 and false is 0, you can use a conditional to index
    into an array using Select.

{% highlight javascript %}
Select.kr(aKrSignal > anotherKrSignal, [false_signal, true_signal]);
{% endhighlight %}

-   **Generating triggers:** A trigger occurs whenever a signal is \<=
    0, and then becomes \> 0. Extending this to comparisons, it means
    that *a trigger occurs when a comparison is false for a while, and
    then becomes true*. Comparing a signal to a threshold may then be
    used anywhere that a trigger is valid. For a simple example, take
    the case of sending a message to the language when the microphone
    input's amplitude crosses a threshold.

{% highlight javascript %}
var mic = In.ar(8, 1),
   amplitude = Amplitude.kr(mic);
SendTrig.kr(amplitude > 0.2, 0, amplitude);
{% endhighlight %}

-   **Passing or suppressing triggers:** You might need to generate
    triggers continuously, but permit the triggers to take effect only
    when a condition is met. Multiplication handles this nicely:
    *condition \* trigger*. Since the condition evaluates as 0 when
    false, the trigger will be replaced by 0 and nothing happens, as
    desired.\
    \
    For a simple case, let's refine the mic amplitude example by
    suppressing triggers that occur within 1/4 second after the
    previous.

{% highlight javascript %}
var mic = In.ar(8, 1),
   amplitude = Amplitude.kr(mic),
   trig = amplitude > 0.2,
   timer = Timer.kr(trig),  // how long since the last trigger?
   filteredTrig = (timer > 0.25) * trig;

SendTrig.kr(filteredTrig, 0, amplitude);
{% endhighlight %}

### Logical operators: And, Or, Not, Xor

Logical operators have simple arithmetic equivalents.

-   **And = multiplication:** *(x \> 0) \* (y \> 0)* means both
    conditions must be true (nonzero) for the result to be nonzero.

<!-- -->

-   **Or = addition:** *(x \> 0) + (y \> 0)* means nonzero in either
    condition is enough to make the result nonzero.\
    \
    NOTE: If both are true, then the result will be 2, not 1. In some
    cases, the 2 may not be acceptable. That can be fixed by wrapping
    the Or in another comparison -- *((x \> 0) + (y \> 0)) \> 0* --
    because 2 \> 0 evaluates to 1!

<!-- -->

-   **Not:** I prefer to negate a condition by comparing it to zero:
    *condition \<= 0*. 0 \<= 0 is 1 (i.e., not 0), and 1 \<= 0 is 0 (not
    1). If you're certain the logical expression will only ever be 0 or
    1 exactly, you can also negate by subtraction: *1 - condition*.

<!-- -->

-   **Xor:** Exclusive-or is true if one or the other condition is true,
    but not both. We can add the two conditions and compare it to 1. The
    syntax is a little bit tricky because '==' doesn't turn into a
    BinaryOpUGen automatically. We have to create the BinaryOpUGen by
    hand.

{% highlight javascript %}
BinaryOpUGen('==', (x > 0) + (y > 0), 1)
{% endhighlight %}

