---
layout: catpage
category: development
title: Quarks Repository has moved
sort_order: 9
---

Quarks is the name of the SuperCollider package management system. It is implemented using SVN and they are hosted on SourceForge.  SourceForge recently changed the URLs of their SVN repositories which unfortunately broke older versions of SuperCollider.

Its easy to fix:

If you are a new user or have never installed quarks on your current system see below. Otherwise, if you've been using quarks and they've stopped working:

<div><strong>Note:</strong> If you have installed SuperCollider from the binary downloads on Sourceforge you will have to execute the following steps to make updating quarks via SVN work again:
    <ol>
        <li>In a terminal navigate to your userAppSupportDir resp. the directory containing the sources of your quarks.
        On a mac:
        `cd ~/Library/Application\ Support/SuperCollider/quarks`
        On Linux:
        `cd ~/.local/share/SuperCollider/quarks`
        On Windows:
        <ol>
        <li>Find your path by by executing the following command in SuperCollider:
        
            `Platform.userAppSupportDir;`
        
        <li>Then cd to that directory, followed by \quarks
        </li>
        </ol>
        </li>
        <li>
        Issue the switch statement. It has to be done in one line: 
        `svn switch --relocate https://quarks.svn.sourceforge.net/svnroot/quarks/  https://svn.code.sf.net/p/quarks/code`
        </li>
    </ol>
</div>
<div>If quarks are new to your system:
   <ol>
        <li>In a terminal navigate to your `Platform.userAppSupportDir;`. If you find the directory does not exist, you will need to create it.
        On a mac:
        <ol>
        <li>
        `cd ~/Library/Application\ Support/SuperCollider/quarks`
        <li>If it says No such File or Directory, then:
        <li>
        ` mkdir ~/Library/Application\ Support/SuperCollider/quarks`
        </li></ol>
        On Linux:
        <ol>
        <li>
        `cd ~/.local/share/SuperCollider/quarks`
        <li>If it says No such File or Directory, then:
        <li>
        `mkdir ~/.local/share/SuperCollider/quarks`
        </li></ol>
        On Windows:
        <ol>
        <li>Find your path by by executing the following command in SuperCollider:
        <li>
        `Platform.userAppSupportDir`
        <li>Then cd to that directory.
        <li>Then
        `cd quarks`
        <li>If the directory is not found, then:
        <li>
        `mkdir quarks`
        </li></ol>
       
        </li>
        <li>
        Do an initial Quark checkout:
        `svn checkout svn://svn.code.sf.net/p/quarks/code/ quarks`
         </li>
    </ol>
</div>
       
