---
layout: catpage
title: "ERROR: server failed to start"
category: tutorials
---

When you've tried to boot the server and you see ERROR: server failed to start, usually there are various other messages you can see as the server was booting. For example, if you see this:

    Exception in World_OpenUDP: unable to bind udp socket

    RESULT = 1
    ERROR:
    server failed to start

...the bit about the "socket" means that the server wasn't able to establish a connection on the internet port that SC wanted to use for client<->server communication. Usually this means you have a zombie scsynth running in the background - go to your computer's Task Manager and see if there's an instance of scsynth there, then kill it, before trying again.