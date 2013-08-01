---
layout: catpage
category: development
title: Building From Source on BeagleBone Black
sort_order: 3
---

Compiling SC3.7 on Beaglebone Black Debian using OSX, a cross-compiler & DISTCC
==

This assumes OSX10.8.4, homebrew and a fresh debian-wheezy-7.0.0-armhf-3.8.13-bone20.img on a sdcard,
but should also work on linux and windows if you install the cross-compiler and distcc.

step1 (osx: install compiler, distcc & start server)
--
1. install the arm-linux-gnueabihf cross-compiler.  it is easiest from [www.cety.de/ctbot/arm-linux-gnueabihf.pkg](http://www.cety.de/ctbot/arm-linux-gnueabihf.pkg).
2. `export PATH=$PATH:/usr/local/arm-linux/bin`
3. `brew install distcc`
4. `distccd --daemon --allow 192.168.1.0/24 --no-detach`  #edit to match root of your ip domain

step2 (bbb: preparation)
--
1. `sudo apt-get update`
2. `sudo apt-get upgrade`
3. `sudo apt-get install git build-essential distcc cmake emacs alsa-base libasound2-dev libsamplerate0-dev libsndfile1-dev libavahi-client-dev libicu-dev libreadline-dev libfftw3-dev libxt-dev`
4. `sudo ln -s /usr/bin/gcc /usr/local/bin/arm-linux-gcc`  #this to make sure the rpi cc is called the same as the osx cc
5. `sudo ln -s /usr/bin/g++ /usr/local/bin/arm-linux-g++`  #this to make sure the rpi cxx is called the same as the osx cxx
6. `sudo ldconfig`

step3 (bbb: install newest jack2 from github)
--
1. `git clone git://github.com/jackaudio/jack2.git`
2. `cd jack2`
3. `./waf configure --alsa`
4. `./waf build`
5. `sudo ./waf install`
6. `sudo ldconfig`

step4 (bbb: install newest sc from github)
--
1. `git clone --recursive git://github.com/supercollider/supercollider.git supercollider`
2. `cd supercollider`
3. `mkdir build && cd build`
4. `export DISTCC_HOSTS='192.168.1.55'`            #edit to match your osx computer ip
5. `CC="distcc arm-linux-gcc" CXX="distcc arm-linux-g++" cmake -L -DCMAKE_BUILD_TYPE=Release -DBUILD_TESTING=OFF -DSSE=OFF -DSSE2=OFF -DSUPERNOVA=OFF -DNOVA_SIMD=ON -DNATIVE=OFF -DSC_QT=OFF -DSC_WII=OFF -DSC_ED=OFF -DSC_IDE=OFF -DSC_EL=ON -DCMAKE_C_FLAGS="-march=armv7-a -mtune=cortex-a8 -mfloat-abi=hard -mfpu=neon" -DCMAKE_CXX_FLAGS="-march=armv7-a -mtune=cortex-a8 -mfloat-abi=hard -mfpu=neon" ..`
6. check the output and make sure it says: Check for working C compiler: /usr/bin/distcc -- works
7. `make -j4`
8. `sudo make install`

step5 (bbb: start jack & sclang)
--
1. `jackd -P70 -p16 -t2000 -dalsa -dhw:0,0 -p128 -n3 -r44100 -s &`     #use -dhw:1,0 if you have a usb soundcard connected
2. `export SC_JACK_DEFAULT_INPUTS="system"`
3. `export SC_JACK_DEFAULT_OUTPUTS="system"`
4. `sclang`

step6 (sc bbb: boot server & test sound)
--
1. `s.boot;`
2. `a= {SinOsc.ar*0.1}.play;`
3. `s.dump;`
4. `a.free;`
5. `s.quit;`
6. `0.exit;`

Compiling SC3.7 natively on Beaglebone Black Debian
==
you can also compile natively on the bbb itself without using distcc.  just follow the instructions above but skip the distcc part (step1, step2 lines 4-5, step4 line 4) and before compiling set up a swapfile...
1. `sudo dd if=/dev/zero of=/swapfile bs=1MB count=512`
2. `sudo mkswap /swapfile`
3. `sudo swapon /swapfile`

And last in step4 line 5 change to `CC="gcc" CXX="g++"`

