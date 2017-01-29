---
layout: catpage
title: Code for GUI sampler
category: gui-design-project
sort_order: 4
---

The full set of elements that are needed can be seen on this screenshot: [GUI ELEMENTS](http://www.flickr.com/photos/55063999@N03/5110498719/in/pool-1575422@N22/)

Here is the (most recent and up to date) code to generate that.

    (
    w = SCWindow("SC Window", Rect(400, 64, 650, 750)).front;

    w.view.decorator = FlowLayout(w.view.bounds);

    SCStaticText(w, Rect(0, 0, 100, 20)).string_("Button").background_(Color.white);

    w.view.decorator.shift(4,0);

    a = SCButton(w, Rect(20,20, 60, 20)).states_([["on",Color.black,Color.clear],["off",Color.black,Color.clear]]).action_({arg butt; butt.value.postln;});

    w.view.decorator.nextLine; w.view.decorator.shift(0,4);

    SCStaticText(w, Rect(0, 0, 60, 20)).string_("Slider").background_(Color.white);

    w.view.decorator.shift(4,0);

    b = SCSlider(w, Rect(20, 50, 60, 20)).action_({arg sl; sl.value.postln; });

    w.view.decorator.shift(4,0);

    e = SCSlider(w, Rect(90, 20, 20, 60)).value_(0.5).action_({arg sl; sl.value.postln; });

    w.view.decorator.nextLine; w.view.decorator.shift(0,4);

    SCStaticText(w, Rect(0, 0, 60, 20)).string_("2DSlider").background_(Color.white);

    w.view.decorator.shift(4,0);

    c = SC2DSlider(w, Rect(20, 80, 60, 60)).x_(0.2).y_(0.7).action_({arg sl; [\x, sl.x.value, \y, sl.y.value].postln; });

    w.view.decorator.nextLine; w.view.decorator.shift(0,4);

    SCStaticText(w, Rect(0, 0, 100, 20)).string_("RangeSlider").background_(Color.white);

    w.view.decorator.shift(4,0);

    d = SCRangeSlider(w, Rect(20, 150, 60, 20)).lo_(0.2).hi_(0.7).action_({arg sl; [\lo, sl.lo.value, \hi, sl.hi.value].postln; });

    w.view.decorator.nextLine; w.view.decorator.shift(0,4);

    SCStaticText(w, Rect(0, 0, 100, 20)).string_("NumberBox").background_(Color.white);

    w.view.decorator.shift(4,0);

    f = SCNumberBox(w, Rect(130, 20, 100, 20)).value_(67.92).action_({ arg numb; numb.value.postln; });

    w.view.decorator.nextLine; w.view.decorator.shift(0,4);

    SCStaticText(w, Rect(0, 0, 100, 20)).string_("StaticText").background_(Color.white);

    w.view.decorator.shift(4,0);

    g = SCStaticText(w, Rect(130, 50, 100, 20)).string_("some text").background_(Color.white);

    w.view.decorator.nextLine; w.view.decorator.shift(0,4);

    SCStaticText(w, Rect(0, 0, 100, 20)).string_("TextView").background_(Color.white);

    w.view.decorator.shift(4,0);

    g = SCTextView(w, Rect(0, 0, 400, 80)).background_(Color.white);
    g.hasVerticalScroller_(true).hasHorizontalScroller_(true).autohidesScrollers_(true);
    g.string_("To be, or not to be--that is the question:
    Whether 'tis nobler in the mind to suffer
    The slings and arrows of outrageous fortune
    Or to take arms against a sea of troubles
    And by opposing end them. To die, to sleep--
    No more--and by a sleep to say we end
    The heartache, and the thousand natural shocks
    That flesh is heir to. 'Tis a consummation
    Devoutly to be wished. To die, to sleep--
    To sleep--perchance to dream: ay, there's the rub,
    For in that sleep of death what dreams may come
    When we have shuffled off this mortal coil,
    Must give us pause. There's the respect
    That makes calamity of so long life.
    ");

    w.view.decorator.nextLine; w.view.decorator.shift(0,4);

    SCStaticText(w, Rect(0, 0, 100, 20)).string_("ListView").background_(Color.white);

    w.view.decorator.shift(4,0);

    h = SCListView(w,Rect(130, 80, 100, 50)).items_(["aaa","bbb", "ccc", "ddd", "eee", "fff"]).action_({ arg sbs; [sbs.value, sbs.item].postln; });

    w.view.decorator.nextLine; w.view.decorator.shift(0,4);

    SCStaticText(w, Rect(0, 0, 100, 20)).string_("MultiSliderView").background_(Color.white);

    w.view.decorator.shift(4,0);

    i = SCMultiSliderView(w, Rect(130, 150, 100, 50)).isFilled_(true).action_({arg xb; ("index: " ++ xb.index ++" value: " ++ xb.currentvalue).postln}).value_([0.1, 0.2, 0.3, 0.1, 0.2, 0.3, 0.1, 0.2, 0.3]);

    w.view.decorator.nextLine; w.view.decorator.shift(0,4);

    SCStaticText(w, Rect(0, 0, 100, 20)).string_("PopUpMenu").background_(Color.white);

    w.view.decorator.shift(4,0);

    j = SCPopUpMenu(w, Rect(20, 178, 100, 20)).items_(["one", "two", "three", "four", "five"]).action_({ arg sbs; sbs.value.postln; });

    w.view.decorator.nextLine; w.view.decorator.shift(0,4);

    SCStaticText(w, Rect(0, 0, 100, 20)).string_("EnvelopeView").background_(Color.white);

    w.view.decorator.shift(4,0);

    k = SCEnvelopeView(w, Rect(20, 220, 400, 80)).drawLines_(true).selectionColor_(Color.red).drawRects_(true).action_({arg b; [b.index,b.value].postln}) .thumbSize_(5).value_([[0.0, 0.1, 0.5, 1.0],[0.1,1.0,0.8,0.0]]);

    w.view.decorator.nextLine; w.view.decorator.shift(0,4);

    SCStaticText(w, Rect(0, 0, 100, 20)).string_("LevelIndicator").background_(Color.white);

    w.view.decorator.shift(4,0);

    l = SCLevelIndicator(w, Rect(270, 10, 20, 60)) .drawsPeak_(true).peakLevel_(0.6).value_(0.8);

    w.view.decorator.nextLine; w.view.decorator.shift(0,4);

    SCStaticText(w, Rect(0, 0, 100, 20)).string_("Knob").background_(Color.white);

    w.view.decorator.shift(4,0);

    n = SCKnob(w, Rect(270, 190, 40, 40)).value_(0.5).action_({arg sl; sl.value.postln; });

    w.view.decorator.nextLine; w.view.decorator.shift(0,4);

    SCStaticText(w, Rect(0, 0, 100, 20)).string_("SoundFileView").background_(Color.white);

    w.view.decorator.shift(4,0);

    q = SCSoundFileView(w, Rect(20,20, 400, 60));

    x = SoundFile.new;

    x.openRead("sounds/a11wlk01.wav");

    q.soundfile = x;

    q.read(0, x.numFrames);

    q.setSelection (0,  [ 10000, 70000 ]);
    )
