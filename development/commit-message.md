---
layout: catpage
category: development
title: Commit Message Format
sort_order: 4
---

Git commit messages should consists of a one-line title, followed by an empty line, followed by the message body:

    title

    first line of body
    second line of body
    third line of body

This makes the message most expressive and comprehensible, while also supporting many git functions and graphical clients that treat the first line differently than the rest of the message.

### Title

Message titles should have the following form:

``component: sub-component: short description of changes``

Great titles are short (**70 characters** or less), so as to fit in one line in most constrained circumstances.

The description of changes should be written in [**imperative mood**][wkp-imperative], e.g. `fix bug` instead of `fixed bug`.

A good example of a title is:

``sc class library: ClassBrowser: fix search with empty query string``

Look at previous commits in the repository for inspiration.

### Body

The message body should describe the changes in details, and explain motivations behind them. The body is not always needed if the changes are few, and the title explains them enough.

The body should have manual line breaks at around **70 character**.

[wkp-imperative]: http://en.wikipedia.org/wiki/Imperative_mood
