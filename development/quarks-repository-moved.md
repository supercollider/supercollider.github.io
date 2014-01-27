---
layout: catpage
category: development
title: Quarks Repository has moved
sort_order: 9
---

Quarks is the name of the SuperCollider package management system. It is implemented using SVN and they are hosted on SourceForge.  SourceForge recently changed the URLs of their SVN repositories which unfortunately broke older versions of SuperCollider.

Its easy to fix:

If you are a new user or have never installed quarks on your current system see below. Otherwise, if you've been using quarks and they've stopped working:

**Note:** If you have installed SuperCollider from the binary downloads on Sourceforge you will have to execute the following steps to make updating quarks via SVN work again:

<ol>
<li>
In a terminal navigate to your userAppSupportDir resp. the directory containing the sources of your quarks.
    <ul>
        <li>
        On a mac:
        {% highlight bash %}$ cd ~/Library/Application\Support/SuperCollider/quarks{% endhighlight %}
        </li>
        <li>
        On Linux:
        {% highlight bash %}$ cd ~/.local/share/SuperCollider/quarks{% endhighlight %}            
        </li>
        <li>
        On Windows: 
        <ol>
            <li>
            Find your path by by executing the following command in SuperCollider: {% highlight c %}Platform.userAppSupportDir;{% endhighlight %}            
            </li>
            <li>
            Then cd to that directory, followed by \quarks
            </li>
        </ol>
        </li>
    </ul>
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

If quarks are new to your system:

<ol>
<li>
In a terminal navigate to your userAppSupportDir resp. If you find the directory does not exist, you will need to create it.
    <ul>
        <li>
            On a mac:
            <ol>
                <li>
                    {% highlight bash %}$ cd ~/Library/Application\ Support/SuperCollider/quarks{% endhighlight %}
                </li>
                
                <li>
                   If it says No such File or Directory, then:
                </li>
               
                <li>
                   {% highlight bash %}$ mkdir ~/Library/Application\ Support/SuperCollider/quarks{% endhighlight %}
                </li>
           </ol>
        </li>
        <li>
            On Linux:
            <ol>
                <li>
                    {% highlight bash %}$ cd ~/.local/share/SuperCollider/quarks{% endhighlight %}
                </li>
                <li>
                    If it says No such File or Directory, then: 
                </li>
                <li>
                    {% highlight bash %}$ mkdir ~/.local/share/SuperCollider/quarks{% endhighlight %}
                </li>
            </ol>            
        </li>
        <li>
            On Windows:
            <ol>
                <li>
                    Find your path by by executing the following command in SuperCollider:
                </li>
                <li>
                    {% highlight bash %}Platform.userAppSupportDir{% endhighlight %}
                </li>
                <li>
                    Then cd to that directory.
                </li>
                <li> Then
                    {% highlight bash %}$ cd quarks{% endhighlight %}
                </li>
                <li>
                    If the directory is not found, then:
                </li>
                <li>
                    {% highlight bash %}$ mkdir quarks{% endhighlight %}
                </li>
            </ol>
        </li>
    </ul>

</li>

<li>
Do an initial Quark checkout:

{% highlight bash %}
$ svn checkout svn://svn.code.sf.net/p/quarks/code/ quarks
{% endhighlight %}
</li>
</ol>