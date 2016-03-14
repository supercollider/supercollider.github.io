---
layout: catpage
category: development
title: Building From Source on Raspberry Pi
sort_order: 3
---

Compiling SC master natively on Raspberry Pi Raspbian Jessie
==

note: this is for running headless under **jessie-lite**. see below for building scide on standard jessie.

requirements
--
* raspberry pi 2 model b (see notes for rpi1)
* sd card with [2015-11-21-raspbian-jessie-lite.img](https://www.raspberrypi.org/downloads/) or newer raspbian jessie
* router with ethernet internet connection for the rpi
* laptop connected to same network as the rpi
* optional: usb soundcard with headphones or speakers connected

step1 (hardware setup)
--
1. connect an ethernet cable from the network router to the rpi
2. insert the sd card and usb soundcard
3. last connect usb power from a 5V@1A power supply

step2 (login & preparations)
--
1. `ssh pi@raspberrypi.local`  #from your laptop, default password is raspberry
2. `sudo raspi-config`  #change password, expand file system, reboot and log in again with ssh

step3 (update the system, install required libraries & compilers)
--
1. `sudo apt-get update`
2. `sudo apt-get upgrade`
3. `sudo apt-get install alsa-base libicu-dev libasound2-dev libsamplerate0-dev libsndfile1-dev libreadline-dev libxt-dev libudev-dev libavahi-client-dev libfftw3-dev cmake git gcc-4.8 g++-4.8`

step4 (compile & install jackd (no d-bus) )
--
1. `git clone git://github.com/jackaudio/jack2 --depth 1`
2. `cd jack2`
3. `./waf configure --alsa`  #note: here we use the default gcc-4.9
4. `./waf build`
5. `sudo ./waf install`
6. `sudo ldconfig`
7. `cd ..`
8. `rm -rf jack2`
9. `sudo nano /etc/security/limits.conf`  #and add the following two lines at the end
  * `@audio - memlock 256000`
  * `@audio - rtprio 75`
10. `exit`  #and log in again to make the limits.conf settings work

step5 (compile & install sc master)
--
1. `git clone --recursive git://github.com/supercollider/supercollider`  #optionally add --depth 1 here if you only need master
2. `cd supercollider`
3. `git submodule init && git submodule update`
4. `mkdir build && cd build`
5. `export CC=/usr/bin/gcc-4.8`  #here temporarily use the older gcc-4.8
6. `export CXX=/usr/bin/g++-4.8`
7. `cmake -L -DCMAKE_BUILD_TYPE="Release" -DBUILD_TESTING=OFF -DSSE=OFF -DSSE2=OFF -DSUPERNOVA=OFF -DNOVA_SIMD=ON -DNATIVE=OFF -DSC_ED=OFF -DSC_WII=OFF -DSC_IDE=OFF -DSC_QT=OFF -DSC_EL=OFF -DSC_VIM=OFF -DCMAKE_C_FLAGS="-mtune=cortex-a7 -mfloat-abi=hard -mfpu=neon -funsafe-math-optimizations" -DCMAKE_CXX_FLAGS="-mtune=cortex-a7 -mfloat-abi=hard -mfpu=neon -funsafe-math-optimizations" ..`
8. `make -j 4`  #leave out flag j4 on single core rpi models
9. `sudo make install`
10. `sudo ldconfig`
11. `cd ../..`
12. `rm -rf supercollider`
13. `sudo mv /usr/local/share/SuperCollider/SCClassLibrary/Common/GUI /usr/local/share/SuperCollider/SCClassLibrary/scide_scqt/GUI`
14. `sudo mv /usr/local/share/SuperCollider/SCClassLibrary/JITLib/GUI /usr/local/share/SuperCollider/SCClassLibrary/scide_scqt/JITLibGUI`

step6 (start jack & sclang & test)
--
1. `jackd -P75 -dalsa -dhw:1 -p1024 -n3 -s -r44100 &`  #edit -dhw:1 to match your soundcard. usually it is 1 for usb
2. `sclang`  #should start sc and compile the class library with only 3 harmless class overwrites warnings
  * `s.boot`  #should boot the server
  * `a= {SinOsc.ar([400, 404])}.play`  #should play sound in both channels
  * `a.free`
  * `{1000000.do{2.5.sqrt}}.bench`  #benchmark: ~0.89 for rpi2, ~3.1 for rpi1
  * `a= {Mix(50.collect{RLPF.ar(SinOsc.ar)});DC.ar(0)}.play`  #benchmark
  * `s.dump`  #avgCPU should show ~19% for rpi2 and ~73% for rpi1
  * `a.free`
  * `0.exit`  #quit sclang
3. `pkill jackd`  #quit jackd

notes
--
* this also works on the original raspberry pi 1 model b but then change compiler flags to `"-mfpu=vfp -mfloat-abi=hard -march=armv6 -mtune=arm1176jzf-s"` (in two places). also create a swap file if you run out of memory and crash during compilation
* if you get `WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!` when trying to ssh, type `ssh-keygen -R raspberrypi.local` to reset
* we need to use gcc 4.8.4 instead of the raspbian default 4.9.2. something with gcc 4.9 triggers sc to generate the dreaded atIdentityHash error at startup.
* for lower latency, try with lower blocksizes when you start jackd.  try for example `-p512` and `-p128`.  tune downwards until you get dropouts and xruns (also watch cpu%).
* soundcards i’ve tried include a cheap blue 3D sound (C-Media Electronics, Inc. Audio Adapter (Planet UP-100, Genius G-Talk)) and the aureon dual usb (TerraTec Electronic GmbH Aureon Dual USB).
* lock/writeprotect the sd card if you plan to pull out the power without properly shutting down the system first. a better way is to add a shutdown command script to a gpio pin - search online for how to do that.
* if you want to use the sc3.7 branch instead of sc master (unstable), the process is the same except for the following additions:
  * in step5, after #2 `git checkout 3.7`
  * in step5, after #12 `sudo mv /usr/local/share/SuperCollider/SCClassLibrary/Common/GUI/Base/Model.sc /usr/local/share/SuperCollider/SCClassLibrary/Common/Core/`

autostart (run sc at system boot)
--
1. `nano ~/autostart.sh`  #and add the following three lines…
  * `#!/bin/bash`
  * `/usr/local/bin/jackd -P75 -dalsa -dhw:1 -p1024 -n3 -s -r44100 &`
  * `su root -c "sclang -D /home/pi/mycode.scd"`
2. `chmod +x ~/autostart.sh`
3. `sudo crontab -e`  #and add the following line to the end…
  * `@reboot /bin/bash /home/pi/autostart.sh`
4. `nano ~/mycode.scd`  #and add your code inside a s.waitForBoot. for example…
  * `s.waitForBoot{ {SinOsc.ar([400, 404], 0, 0.5)}.play }`
5. `sudo reboot`  #and the sound should start after a few seconds. log in with ssh and `sudo pkill jackd && sudo pkill sclang` to stop it.

- - -

Compiling SCIDE master natively on Raspberry Pi Raspbian Jessie
==

note: this is for building scide on standard jessie (raspbian desktop).

requirements
--
* raspberry pi 2 model b
* sd card with [2015-11-21-raspbian-jessie.img](https://www.raspberrypi.org/downloads/) or newer raspbian jessie (note: not jessie-lite)
* router with ethernet internet connection for the rpi
* screen, mouse and keyboard (although you can also do it all via ssh)
* optional: usb soundcard with headphones or speakers connected

step1 (hardware setup)
--
1. connect an ethernet cable from the network router to the rpi
2. insert the sd card and usb soundcard + screen, mouse and keyboard
3. last connect usb power from a 5V@1A power supply

step2 (update the system, install required libraries & compilers)
--

when you see the rpi desktop open the terminal and type:

1. `sudo raspi-config`  #change password, expand file system, reboot and start terminal again
2. `sudo apt-get remove --auto-remove supercollider`  #note: this will also remove sonicpi (we'll keep jackd though)
3. `sudo apt-get update`
4. `sudo apt-get upgrade`
5. `sudo apt-get install libboost-dev libjack-jackd2-dev libcwiid-dev libicu-dev libasound2-dev libsamplerate0-dev libsndfile1-dev libreadline-dev libxt-dev libudev-dev libavahi-client-dev libfftw3-dev cmake gcc-4.8 g++-4.8 qt5-default qt5-qmake qttools5-dev qttools5-dev-tools qtdeclarative5-dev libqt5webkit5-dev qtpositioning5-dev libqt5sensors5-dev`

step3 (compile and install supercollider)
--
1. `git clone --recursive git://github.com/supercollider/supercollider --depth 1`
2. `cd supercollider`
3. `git submodule init && git submodule update`
4. `mkdir build && cd build`
5. `export CC=/usr/bin/gcc-4.8`  #here temporarily use the older gcc-4.8
6. `export CXX=/usr/bin/g++-4.8`
7. `cmake -L -DCMAKE_BUILD_TYPE="Release" -DBUILD_TESTING=OFF -DSSE=OFF -DSSE2=OFF -DSUPERNOVA=OFF -DNOVA_SIMD=ON -DNATIVE=OFF -DSC_ED=OFF -DSC_WII=ON -DSC_IDE=ON -DSC_QT=ON -DSC_EL=OFF -DSC_VIM=OFF -DCMAKE_C_FLAGS="-mtune=cortex-a7 -mfloat-abi=hard -mfpu=neon -funsafe-math-optimizations" -DCMAKE_CXX_FLAGS="-mtune=cortex-a7 -mfloat-abi=hard -mfpu=neon -funsafe-math-optimizations" ..`
8. `make -j 4`
9. `sudo make install`
10. `sudo ldconfig`
11. `cd ../..`
12. `rm -rf supercollider`

step4 (start jack & sclang & test)
--

from raspbian desktop open a terminal and type:

  * `qjackctl`  #and select the usb soundcard under setup/interface.  click ok and start
  * `scide`  #in another terminal window to launch the supercollider ide

notes
--
* if you want to ssh in and run this sc version as headless, run the command `export DISPLAY=:0.0` before starting jackd.
* the cpu benchmarks for this scide version is: ~1.01 and ~25%
