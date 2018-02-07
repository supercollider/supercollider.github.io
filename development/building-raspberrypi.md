---
layout: catpage
category: development
title: Building From Source on Raspberry Pi
sort_order: 3
---

Compiling SCIDE natively on Raspberry Pi Raspbian
==
note: this is for building the latest version of supercollider including qt gui components and the ide under **raspbian stretch with desktop**. it is the easiest way to compile sc and this version can also run headless. see below for building non-qt, non scide under **raspbian stretch lite** (more advanced).

requirements
--
* raspberry pi 2 or 3 (also rpi0 and rpi1 but note that compiling will take a _long_ time)
* sd card with [raspbian-stretch](https://www.raspberrypi.org/downloads/raspbian) (note: not stretch lite)
* router with ethernet internet connection for the rpi
* screen, mouse and keyboard (although you can also do it all via ssh)
* optional: usb soundcard with headphones or speakers connected

step1 (hardware setup)
--
1. connect an ethernet cable from the network router to the rpi
2. insert the sd card and usb soundcard. connect screen, mouse and keyboard
3. last connect usb power from a 5V@1A power supply

step2 (update the system, install required libraries)
--
from raspbian desktop open a terminal window and type...
1. `sudo raspi-config`  #change password and optionally edit hostname and enable ssh and/or vnc
2. `sudo apt-get update`
3. `sudo apt-get upgrade`
4. `sudo apt-get dist-upgrade`
5. `sudo apt-get install libjack-jackd2-dev libsndfile1-dev libasound2-dev libavahi-client-dev libreadline6-dev libfftw3-dev libxt-dev libudev-dev libcwiid-dev cmake qttools5-dev-tools libqt5webkit5-dev qtpositioning5-dev libqt5sensors5-dev`

step3 (compile and install supercollider)
--
1. `git clone --recursive git://github.com/supercollider/supercollider`
2. `cd supercollider`
3. `git checkout 3.9`  #use latest version 3.9.x on branch 3.9
4. `git submodule init && git submodule update`
5. `mkdir build && cd build`
6. `cmake -L -DCMAKE_BUILD_TYPE="Release" -DBUILD_TESTING=OFF -DSUPERNOVA=OFF -DNATIVE=ON -DSC_WII=ON -DSC_IDE=ON -DSC_QT=ON -DSC_ED=OFF -DSC_EL=OFF -DSC_VIM=ON ..`
7. `make -j 4`  #use -j4 flag only for rpi3 (quadcore)
8. `sudo make install`
9. `sudo ldconfig`
10. `mkdir -p ~/.config/SuperCollider`

step4 (set up jack)
--
1. `nano ~/.jackdrc`  #edit to look like this...
        
        /usr/bin/jackd -P75 -dalsa -dhw:0 -r44100 -p1024 -n3
        
2. press ctrl+o to save and ctrl+x to exit

the `-dhw:0` above is the internal soundcard. change this to `-dhw:1` for usb soundcards. `aplay -l` will list available devices.

another way to set up and start jack is to open a terminal and type `qjackctl`. click 'setup' to select soundcard and set periods to 3 (recommended). then start jack before scide by clicking the play icon.

startup
--
from raspbian desktop just open a terminal and type...
* `scide`

(see notes below about alsamixer volume)

headless
--
if you want to ssh in and start this sc version headless, run the following commands...
* `export DISPLAY=:0.0`
* `sclang`

**done!** see below for sc3-plugins, autostart, benchmarks and notes

- - -

Compiling SC natively on Raspberry Pi Raspbian Lite
==
note: this section is for more advanced users that want to compile and run supercollider (sclang+scsynth) under **raspbian stretch lite**. it does not include qt nor the ide.

the instructions here are meant for supercollider version 3.9.1 and higher; for instructions on building previous versions please see older versions of this page or ask on the mailing list.

requirements
--
* raspberry pi 2 or 3 (also rpi0 and rpi1 but note that compiling will take a _long_ time)
* sd card with [raspbian-stretch-lite](https://www.raspberrypi.org/downloads/raspbian)
* an empty dummy file called `ssh` on the root level of the sd card (to enable ssh)
* router with ethernet internet connection for the rpi
* laptop connected to same network as the rpi
* optional: usb soundcard with headphones or speakers connected

step1 (hardware setup)
--
1. connect an ethernet cable from the network router to the rpi
2. insert the sd card and usb soundcard
3. last connect usb power from a 5V@1A power supply

step2 (update the system, install required libraries)
--
1. `ssh pi@raspberrypi`  #from your laptop, default password is raspberry
2. `sudo raspi-config`  #change password and optionally edit hostname, set memory split to 16
3. `sudo apt-get update`
4. `sudo apt-get upgrade`
5. `sudo apt-get dist-upgrade`
6. `sudo apt-get install libsamplerate0-dev libsndfile1-dev libasound2-dev libavahi-client-dev libreadline6-dev libfftw3-dev libxt-dev libudev-dev libcwiid-dev cmake git`

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
9. `sudo nano /etc/security/limits.conf`  #and add the following lines at the end...
        
        @audio - memlock 256000
        @audio - rtprio 75
        
10. `exit`  #and ssh in again to make the limits.conf settings work
11. `nano ~/.jackdrc`  #edit to look like this...
        
        /usr/local/bin/jackd -P75 -dalsa -dhw:0 -r44100 -p1024 -n3
        
the `-dhw:0` above is the internal soundcard. change this to `-dhw:1` for usb soundcards. `aplay -l` will list available devices.

step4 (compile & install supercollider)
--
1. `git clone --recursive git://github.com/supercollider/supercollider`
2. `cd supercollider`
3. `git checkout 3.9`  #use latest version 3.9.x on branch 3.9
4. `git submodule init && git submodule update`
5. `nano lang/LangSource/SC_TerminalClient.cpp`  #TEMP FIX for 100% sclang issue - find the first line and comment it out, add the 2nd right after
        
        //mTimer.cancel();
        if (error==boost::system::errc::success) {mTimer.cancel();} else {return;}
        
6. `mkdir build && cd build`
7. `cmake -L -DCMAKE_BUILD_TYPE="Release" -DBUILD_TESTING=OFF -DSUPERNOVA=OFF -DNATIVE=ON -DSC_WII=ON -DSC_IDE=OFF -DSC_QT=OFF -DSC_ED=OFF -DSC_EL=OFF -DSC_VIM=ON ..`
8. `make -j 4`  #use -j4 flag only for rpi3 (quadcore)
9. `sudo make install`
10. `sudo ldconfig`
11. `mkdir -p ~/.config/SuperCollider`

startup
--
* `sclang`

when you boot the server jack should start automatically with the settings in `~/.jackdrc`

**done!** see below for sc3-plugins, autostart, benchmarks and notes

- - -

sc3-plugins
==
how to compile and install [sc3-plugins](https://github.com/supercollider/sc3-plugins). this applies to both the scide and lite versions above.
1. `git clone --recursive https://github.com/supercollider/sc3-plugins.git --depth 1`
2. `cd sc3-plugins`
3. `mkdir build && cd build`
4. `cmake -L -DCMAKE_BUILD_TYPE="Release" -DSUPERNOVA=OFF -DNATIVE=ON -DSC_PATH=../../supercollider/ ..`
5. `make -j 4`  #use -j4 flag only for rpi3 (quadcore)
6. `sudo make install`

autostart
==
how to automatically run supercollider code at system boot. this applies to both the scide and lite versions above.
1. `nano ~/autostart.sh`  #and add the following lines (ctrl+o, ctrl+x to save and exit)...
        
        #!/bin/bash
        PATH=/usr/local/bin:$PATH
        export DISPLAY=:0.0
        sleep 10  #can be lower (5) for rpi3
        sclang mycode.scd
        
2. `chmod +x ~/autostart.sh`
3. `crontab -e`  #and add the following line to the end...
        
        @reboot cd /home/pi && ./autostart.sh
        
4. `nano ~/mycode.scd`  #and add your code inside a waitForBoot. for example...
        
        s.waitForBoot{ {SinOsc.ar([400, 404])}.play }
        
5. `sudo reboot`  #the sound should start after a few seconds
6. log in with ssh and `killall jackd sclang scsynth` to stop the sound

benchmarks
==
these are rough benchmark tests. the server should be booted and jackd running with settings: `-P75 -p1024 -n3 -r44100`
also for comparison it is important to set cpu scaling to 'performance' with...
* `echo performance | sudo tee /sys/devices/system/cpu/cpu*/cpufreq/scaling_governor`

start sclang or scide and type...
        
        s.boot
        {1000000.do{2.5.sqrt}}.bench //~0.65 for rpi3 headless, ~0.7 for rpi3 scide, ~3.1 for rpi1 headless, ~2.3 for rpi0 headless, ~2.5 for rpi0 scide
        a= {Mix(50.collect{RLPF.ar(SinOsc.ar)});DC.ar(0)}.play
        s.avgCPU //run a few times. ~12% for rpi3, ~48% for rpi1, ~39% for rpi0
        a.free

note: with the default cpu scaling (ondemand) these benchmarks perform much worse. but 'ondemand' also saves battery life so depending on your application this might be the preferred mode.
to set 'performance' scaling mode permanently see under "Gotcha..." [here](https://raspberrypi.stackexchange.com/questions/9034/how-to-change-the-default-governor#9048)

notes
==
additional information. this applies to both the scide and lite versions above.
* an easy way to burn the zip file (no need to unpack) to a sd card is to use [etcher](http://etcher.io).
* the internal soundcard volume is by default set low (40). type `alsamixer` in terminal and adjust the pcm volume to 85 with the arrow keys, esc key exits.
* the audio quality of rpi's built-in sound is terrible. dithering helps a bit so add `-zs` to the jackd command if you are using the built-in sound.
* if the `make -j 4` build step stops or returns an error the compiler might just have run out of memory. try to reboot and run the make command again without `-j 4` or decrease the gpu memory in raspi-config under advanced (set it to 16).
* if you get `WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!` when trying to ssh in, type `ssh-keygen -R raspberrypi` to reset.
* for lower latency, set a lower blocksize for jackd. try for example `-p512` or `-p128`. tune downwards until you get dropouts and xruns (also watch cpu%).
* usb soundcards i’ve tried include the cheap blue 3D sound (C-Media Electronics, Inc. Audio Adapter (Planet UP-100, Genius G-Talk)) and the aureon dual usb (TerraTec Electronic GmbH Aureon Dual USB). there are also some [audio codec modules](http://www.fredrikolofsson.com/f0blog/?q=node/656) that work.
* to avoid sd card corruption one should always shut down the system properly and not just pull out the 5v power. when running headless you can either ssh in and type `sudo halt -p`, use a gpio pin with a button + python script, or set up an osc command from within sc that turns off the rpi. see [here](https://github.com/blacksound/VTM/wiki/Raspberry-Pi-Instructions#shutdown-for-raspberry-pi)
* for the older Raspbian Jessie system use a [previous](https://github.com/supercollider/supercollider.github.io/blob/1f578b5fa71e1acae0ce40d14bc0ef116062093d/development/building-raspberrypi.md) version of these instructions.
* to quit sclang after starting via the commandline use `0.exit`
