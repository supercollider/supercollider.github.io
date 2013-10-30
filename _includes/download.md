<table>
    <tbody>
        <tr>
            <td width="32%" valign="top">
                <h2>
                    <img src="/images/platform_mac_os_x.gif" alt="" />
                    Mac
                </h2>
                <ul class="nodot">
                    <li>
                        <a href="http://sourceforge.net/projects/supercollider/files/Mac%20OS%20X/3.6/SuperCollider-3.6.5-OSX-universal.dmg/download"><i class="icon-download-alt">.</i> 3.6.5 installer</a>
                    </li>
                    <li>
                        <a href="http://sourceforge.net/projects/supercollider/files/Mac%20OS%20X/3.6/SuperCollider-3.6.5-OSX-universal-no-ide.dmg/download"><i class="icon-download-alt">.</i> 3.6.5 installer (old Cocoa IDE)</a>
                    </li>
                </ul>
                <p>
                    OS X 10.4, 32-bit universal build:
                </p>
                <ul class="nodot">
                    <li>
                        <a href="http://sourceforge.net/projects/supercollider/files/Mac%20OS%20X/3.4.4/SuperCollider-3.4.4_32_bit.dmg/download"><i class="icon-download-alt">.</i> SuperCollider3.4.4-10.4</a>
                    </li>
                </ul>
            </td>
            <td width="32%" valign="top">
                <h2>
                    <img src="/images/platform_linux.gif" alt="" />
                    Linux
                </h2>
                 PPA and package distributions:
                <ul>
                    <li>
                        <a href="http://launchpad.net/~supercollider/+archive/ppa"><strong>Ubuntu</strong> </a>
                    </li>
                    <li>
                        <a href="http://packages.debian.org/sid/supercollider"><strong>Debian</strong> </a>
                    </li>
                    <li>
                        <a href="http://ccrma.stanford.edu/planetccrma/software/"><strong>RedHat</strong> or <strong>Fedora</strong> packages</a>
                        provided by PlanetCCRMA
                    </li>
                </ul>
            </td>
            <td width="32%" valign="top">
                <h2>
                    <img src="/images/platform_windows.gif" alt="" />
                    Windows
                </h2>
                <ul class="nodot">
                    <li>
                        <a href="http://sourceforge.net/projects/supercollider/files/Windows/3.6/SuperCollider-3.6.5-win32.exe/download"><i class="icon-download-alt">.</i> Win 32 3.6.5 installer</a>
                    </li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>


<h4>Building from source</h4>

{% highlight bash %}
git clone --recursive git@github.com:supercollider/supercollider.git
{% endhighlight %}

<iframe src="http://ghbtns.com/github-btn.html?user=supercollider&amp;repo=supercollider&amp;type=fork&amp;count=true&amp;size=small" allowtransparency="true" frameborder="0" scrolling="0" width="156px" height="30px">fork</iframe>

<p><a href="/development/building.html"><i class="icon-hand-right">.</i> <strong>Build instructions, tips and trouble shooting</strong></a></p>

<h4>Release notes</h4>

<p><a href="http://doc.sccode.org/Guides/News-3_6.html">3.6 Release notes</a></p>

<h4>Plugins and Extensions</h4>

<ul>
    <li><a href="http://supercollider.sourceforge.net/downloads/#ext">Synthesis Plugins and Extensions</a></li>
</ul>

<h4>Quarks</h4>

<p>Quarks is the package system and extends SuperCollider with lots of interesting things for math, graphics, machine learning, networking, interface and compositional frameworks.</p>

<ul>
    <li><a href="http://quarks.sourceforge.net/">Quarks repository</a></li>
    <li><a href="http://doc.sccode.org/Guides/UsingQuarks.html">Quarks help file</a></li>
</ul>
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

