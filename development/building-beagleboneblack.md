---
layout: catpage
category: development
title: Building From Source on BeagleBone Black
sort_order: 3
---

Compiling SC natively on Beaglebone Black Debian Stretch
==
note: this is for compiling and running supercollider (sclang+scsynth) including the sc3-plugins under **debian stretch**. it does not include qt nor the ide. for compiling the full scide adapt the instructions found [here](http://supercollider.github.io/development/building-raspberrypi).

the instructions here are meant for SuperCollider version 3.10 and higher; for instructions on building previous versions please see older versions of this page or ask on the mailing list.

requirements
--
* beaglebone black (or any of the variants green, blue, industrial, pocket...)
* sd card with [stretch iot](http://beagleboard.org/latest-images) or [stretch console](https://elinux.org/Beagleboard:BeagleBoneBlack_Debian#Stretch_Snapshot_console). the console version is minimal and recommended. the instructions also work under the [stretch lxqt](http://beagleboard.org/latest-images) desktop version.
* router with ethernet internet connection for the bbb
* laptop connected to same network as the bbb
* usb soundcard with headphones or speakers connected

step1 (hardware setup)
--
1. connect an ethernet cable from the network router to the bbb
2. insert the sd card and usb soundcard
3. last connect usb power from a 5V@1A power supply

step2 (update the system, install required libraries)
--
1. `ssh debian@beaglebone`  #from your laptop, default password is `temppwd`
2. `sudo passwd debian`  #change password
3. `sudo /opt/scripts/tools/grow_partition.sh`  #expand file system. skip if you are running on the emmc
4. `sudo reboot`  #and log in again with ssh
5. `sudo apt-get update`
6. `sudo apt-get upgrade`
7. `sudo apt-get dist-upgrade`
8. `sudo apt-get install libsamplerate0-dev libsndfile1-dev libasound2-dev libavahi-client-dev libreadline-dev libfftw3-dev libudev-dev cmake git build-essential python-dev alsa-utils cpufrequtils`

step3 (compile & install jackd (no d-bus) )
--
1. `git clone git://github.com/jackaudio/jack2 --depth 1`
2. `cd jack2`
3. `./waf configure --alsa --libdir=/usr/lib/arm-linux-gnueabihf/`
4. `./waf build`
5. `sudo ./waf install`
6. `sudo ldconfig`
7. `cd ..`
8. `rm -rf jack2`
9. `sudo sh -c "echo @audio - memlock 256000 >> /etc/security/limits.conf"`
10. `sudo sh -c "echo @audio - rtprio 75 >> /etc/security/limits.conf"`
11. `echo jackd -P75 -p16 -dalsa -dhw:1 -r44100 -p1024 -n3 > ~/.jackdrc`
12. `exit` #and ssh in again to make the limits.conf settings work

the `-dhw:1` above is normally the usb soundcard. `sudo aplay -l` will list available devices. use `nano ~/.jackdrc` to edit jack settings.

step4 (compile & install supercollider)
--
1. `git clone --recursive git://github.com/supercollider/supercollider`
2. `cd supercollider`
3. `git checkout 3.10`  #use latest version 3.10.x on branch 3.10
4. `git submodule init && git submodule update`
5. `mkdir build && cd build`
6. `cmake -L -DCMAKE_BUILD_TYPE="Release" -DBUILD_TESTING=OFF -DSUPERNOVA=OFF -DNATIVE=ON -DSC_IDE=OFF -DNO_X11=ON -DSC_QT=OFF -DSC_ED=OFF -DSC_EL=OFF -DSC_VIM=ON ..`
7. `make`
8. `sudo make install`
9. `sudo ldconfig`

startup
--
* `sclang`

when you boot the server jack should start automatically with the settings in ~/.jackdrc

**done!** see below for sc3-plugins, autostart, benchmarks and notes

- - -

sc3-plugins
==
how to compile and install [sc3-plugins](https://github.com/supercollider/sc3-plugins).
1. `cd ~`
2. `git clone --recursive https://github.com/supercollider/sc3-plugins.git`
3. `cd sc3-plugins`
4. `git checkout 3.10`
5. `git submodule init && git submodule update`
6. `mkdir build && cd build`
7. `cmake -L -DCMAKE_BUILD_TYPE="Release" -DSUPERNOVA=OFF -DNATIVE=ON -DSC_PATH=../../supercollider/ ..`
8. `make`
9. `sudo make install`

autostart
==
how to automatically run supercollider code at system boot.
1. `nano ~/autostart.sh`  #and add the following lines (ctrl+o, ctrl+x to save and exit)...
        
        #!/bin/bash
        export PATH=/usr/local/bin:$PATH
        sleep 5
        sclang mycode.scd
        
2. `chmod +x ~/autostart.sh`
3. `crontab -e`  #and add the following line to the end...
        
        @reboot cd /home/debian && ./autostart.sh
        
4. `nano ~/mycode.scd`  #and add your code inside a waitForBoot. for example...
        
        s.waitForBoot{ {SinOsc.ar([400, 404])}.play }
        
5. `sudo reboot`  #the sound should start after a few seconds
6. log in with ssh and `pkill jackd; pkill sclang; pkill scsynth` to stop the sound

benchmarks
==
these are rough benchmark tests. the server should be booted and jackd running with settings: `-P75 -p1024 -n3 -r44100`
also make sure to power the bbb through the barrel jack (else the cpu is capped at 300mhz - check with `cpufreq-info`). also for comparison it is important to set cpu scaling to 'performance' with...
* `sudo cpufreq-set --governor performance`

start sclang and type...
        
        s.boot
        {1000000.do{2.5.sqrt}}.bench //~2.0 on a bb-black, ~2.6 with lxqt on a bb-black
        a= {Mix(50.collect{RLPF.ar(SinOsc.ar)});DC.ar(0)}.play
        s.avgCPU //run a few times. ~47% on a bb-black
        a.free

note: the cpu scaling mode 'ondemand' seem to work quite good on the bbb and will save battery without loosing much in performance.

notes
==
additional information.
* an easy way to burn the img.xy file (no need to unpack) to a sd card is to use [etcher](http://etcher.io).
* type `alsamixer` in terminal and then F6. adjust the mic and speaker volume with the arrow keys, esc key exits.
* if you get `WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!` when trying to ssh in, type `ssh-keygen -R beaglebone` to reset.
* for lower latency, set a lower blocksize for jackd. try for example `-p512` or `-p128`. tune downwards until you get dropouts and xruns (also watch cpu%).
* usb soundcards i’ve tried include the cheap blue 3D sound (C-Media Electronics, Inc. Audio Adapter (Planet UP-100, Genius G-Talk)) and the aureon dual usb (TerraTec Electronic GmbH Aureon Dual USB).
* to avoid sd card corruption one should always shut down the system properly and not just pull out the 5v power. when running headless you can either ssh in and type `sudo halt -p`, use a gpio pin with a button + python script, or set up an osc command from within sc that turns off the bbb. see [here](https://github.com/blacksound/VTM/wiki/Raspberry-Pi-Instructions#shutdown-for-raspberry-pi)
* to quit sclang after starting via the commandline use `0.exit`
