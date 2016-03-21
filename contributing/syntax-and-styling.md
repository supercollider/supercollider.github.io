---
layout: catpage
title: "Syntax coloring for SuperCollider"
category: contributing
sort_order: 3
---


## SuperCollider Code Blocks

In [Markdown](https://help.github.com/articles/github-flavored-markdown) indenting creates a code block:

    s = Server.local;
    y = Synth("def");

Github supports an additional style of code block where you can specify the language to colorize.  

The markup looks like this:

	```supercollider
 	s = Server.local;
 	y = Synth("def");
 	```
  
The result looks like this:
  
 ```supercollider
 s = Server.local;
 y = Synth("def");
 ```

Note: you won't see this formatted correctly when using the local Jekyll test server.
But you can see it in the preview when editing a markdown file on github.


## Adding HTML using submodules

Any folders in this repo that don't start with an underscore will be served on the web. Folders of html can be simply copied in to a folder and they will be included in the site.

git submodules can also be added.  Pushing to that submodule will result in triggering this repo to rebuild the static pages.


## Layout and Styles

The site structure is a simplified version of Jekyll Bootstrap.  That had a theme switching system, but it seemed to be broken and the author is working on a different system now. A default theme is useful only as a starting point anyway.

The layout is a simple bootstrap html wrapper and the css is (currently) a bootstrap theme customized using [Bootstrap Magic](http://pikock.github.com/bootstrap-magic/)


## Jekyll Bootstrap

[Jekyll Bootstrap](http://jekyllbootstrap.com/)

A few things are currently left in from Jekyll Bootstrap like the disqus comment include, the category and page iterators. They are not essential and they are frankly a bit confusing.

The includes for comments, analytics etc. are forked from Jekyll Bootstrap as they are the most useful and resuable part of that project. Configuration for disqus, facebook, bitly and other trendy things is in `_config.yml`
