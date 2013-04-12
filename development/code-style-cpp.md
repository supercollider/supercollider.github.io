---
layout: development
title: C++ Code Style
---


Some quick notes about what to consider when contributing to SuperCollider's code base. The following really only applies to the C/C++ sources of scsynth and sclang (somebody please add notes for SC sources!).

### Indentation

* Older code uses tabs for indentaion.
* Newer code often uses 4 spaces (sometimes only 2 spaces).

When modifying existing code, always make sure you use the same indentation style as the rest of the file.


### Identifiers

In general identifiers are in camel case (with some exceptions, see below):

    double thisIsAVariable;
    double andThisIsAnother;

Global variables are often prefixed with g:

    InterfaceTable* gInterfaceTable;

Constants are prefixed with k:

    kNode_Info

Functions operating on a certain structure type are often prefixed with the name of that type, followed by an underscore:

    World* World_New(WorldOptions *inOptions);
    void   Node_SendTrigger(Node* inNode, int triggerID, float value);

Classes of general utility and used in both scsynth and sclang are sometimes prefixed with SC_.

    class SC_SyncCondition;

Method names more often than not begin with an upper case character.

    GetReplyFunc();
    CallNextStage();

Class and struct members are usually prefixed with m followed by an upper case character, or `m_` followed by a lower case character, the rest of the identifier being in camel case:

    size_t mOffset;
    double m_prevInput;


### Conventions particular to sclang

Structures in sclang are often prefixed with Pyr:

    PyrSlot;
    PyrClass;


### Notes for UGen writers

The naming for UGens has fairly strict conventions, because SC's macros connect the function/struct names with the names used by a user. A UGen usually has a struct associated with it, which should take the same name as the corresponding sclang class (which implies it begins with a capital letter).

    struct SinOsc : Unit { ... };

In general the associated methods' names should begin with that name too: the constructor must take that name followed by _Ctor and the destructor (if used) must take that name followed by _Dtor.

    void SinOsc_Ctor(SinOsc *unit);

The DSP functions should take that name followed by `_next`, plus more text to distinguish the different DSP functions from each other as needed; e.g. audio-rate is postfixed by `_a` and control-rate is postfixed by `_k`. These postfixes might stack up for several parameter/rate combinations:

    void SinOsc_next_iak(SinOsc *unit, int inNumSamples);

Private methods within the plugin files don't have to follow strict naming but it is recommended to prefix them in a similar fashion, to identify the UGen(s) with which they belong.

