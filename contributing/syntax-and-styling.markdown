---
layout: catpage
title: "Syntax coloring for SuperCollider"
category: contributing
---

## Markdown syntax

- [Github Flavored Markdown](https://help.github.com/articles/github-flavored-markdown)


## SuperCollider Code Blocks

In Markdown indenting creates a code block:

    s = Server.local;
    y = Synth("def");

Github supports an additional style of code block.  If support for SuperCollider is ever added to Pygments then it can display code blocks correctly.

The markup would look like this:

	```supercollider
	s = Server.local;
	y = Synth("def");
	```

The result looks like this:

```supercollider
s = Server.local;
y = Synth("def");
```

Note: you won't see this formatted correctly using the local Jekyll test server.

## Adding SuperCollider syntax coloring support

Jekyll has built in Pygment support for syntax coloring.

SuperCollider looks kinda like Javascript so its possible to get approximate syntax coloring by using `{ %  highlight javascript % }` 

{% highlight javascript %}
s = Server.local;
y = Synth("def");
{
  Saw.ar(440);
}.play
{% endhighlight %}

It would be possible to implement Pygments support and submit that to github.

It would also be possible to add SuperCollider support to Highlight.js and then include that js on the page and use it for syntax highlighting.


## Adding HTML using submodules

Any folders in this repo that don't start with an underscore will be served on the web. Folders of html can be simply copied in to a folder and they will be included in the site.

git submodules can also be added.  Pushing to that submodule will result in triggering this repo to rebuild the static pages.


## Layout and Styles

The site structure is a simplified version of Jekyll Bootstrap.  That had a theme switching system, but it seemed to be broken and the author is working on a different system now. A default theme is useful only as a starting point anyway.

The layout is a simple bootstrap html wrapper and the css is (currently) a bootstrap theme customized using [Bootstrap Magic](http://pikock.github.com/bootstrap-magic/)


## Jekyll Bootstrap

[Jekyll Bootstrap](http://jekyllbootstrap.com/)

A few things are currently left in from Jekyll Bootstrap like the disqus comment include, the category and page iterators.  They are not essential and they are frankly a bit confusing.

The includes for comments, analytics etc. are forked from Jekyll Bootstrap as they are the most useful and resuable part of that project. Configuration for disqus, facebook, bitly and other trendy things is in `_config.yml`



