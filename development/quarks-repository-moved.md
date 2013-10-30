---
layout: catpage
category: development
title: Quarks Repository has moved
sort_order: 9
---

Quarks is the name of the SuperCollider package management system. It is implemented using SVN and they are hosted on SourceForge.  SourceForge recently changed the URLs of their SVN repositories which unfortunately broke older versions of SuperCollider.

Its easy to fix:

<div><strong>Note:</strong> If you have installed SuperCollider from the binary downloads on Sourceforge you will have to execute the following steps to make updating quarks via SVN work again:
    <ol>
        <li>In a terminal navigate to your userAppSupportDir resp. the directory containing the sources of your quarks.
        On a mac:
        {% highlight bash %}
        $ cd ~/Library/Application\ Support/SuperCollider/quarks 
        {% endhighlight %}
        On Linux:
        {% highlight bash %}
        $ cd ~/.local/share/SuperCollider/quarks
        {% endhighlight %}
        On Windows:
        ( path and explanation needed here )
        </li>
        <li>
        Issue the switch statement. It has to be done in one line or \ has to be set before a line-brake: 
        {% highlight bash %}
        $ svn switch --relocate \
            https://quarks.svn.sourceforge.net/svnroot/quarks/ \
            https://svn.code.sf.net/p/quarks/code 
        {% endhighlight %}
        </li>
    </ol>
</div>
