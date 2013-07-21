---
layout: catpage
category: development
title: Building From Source on Raspberry Pi
sort_order: 2
---


asdf

compiling sc3.7alpha0 on rpi using osx, a crosscompiler and distcc
------------------------------------------------------------------

(this assumes osx10.8.4, homebrew and a fresh 2013-05-25-wheezy-raspbian.img on a sdcard)

//--on osx
* download and install http://www.cety.de/ctbot/arm-linux-gnueabihf.pkg
* export PATH=$PATH:/usr/local/arm-linux/bin
* brew install distcc
* distccd --daemon --allow 192.168.1.0/24 --no-detach  #edit to match root of your ip domain

//--on rpi
* sudo apt-get update
* sudo apt-get upgrade
* sudo apt-get install cmake emacs distcc libasound2-dev libsamplerate0-dev libsndfile1-dev libavahi-client-dev libicu-dev libreadline-dev libfftw3-dev libxt-dev
* sudo ln -s /usr/bin/gcc /usr/local/bin/arm-linux-gcc
* sudo ln -s /usr/bin/g++ /usr/local/bin/arm-linux-g++
* sudo ldconfig

* git clone git://github.com/jackaudio/jack2.git
* cd jack2
* ./waf configure --alsa
* ./waf build
* sudo ./waf install
* sudo ldconfig
* sudo pico /etc/security/limits.conf
* add the following lines and do ctrl+o, ctrl+x so save and exit.
	@audio - memlock 256000
	@audio - rtprio 99
	@audio - nice -19
* sudo reboot

* git clone --recursive git://github.com/supercollider/supercollider.git supercollider
* cd supercollider
* mkdir build && cd build
* export DISTCC_HOSTS='192.168.1.55'            #edit to match your osx computer ip
* CC="distcc arm-linux-gcc" CXX="distcc arm-linux-g++" cmake -L -DCMAKE_BUILD_TYPE=Release -DBUILD_TESTING=OFF -DSSE=OFF -DSSE2=OFF -DSUPERNOVA=OFF -DNOVA_SIMD=ON -DNATIVE=OFF -DSC_QT=OFF -DSC_WII=OFF -DSC_ED=OFF -DSC_IDE=OFF -DSC_EL=ON -DCMAKE_C_FLAGS="-march=armv6 -mfpu=vfp -mfloat-abi=hard" -DCMAKE_CXX_FLAGS="-march=armv6 -mfpu=vfp -mfloat-abi=hard" ..
* shock the output and make sure it says: Check for working C compiler: /usr/bin/distcc -- works
* make -j4
* sudo make install

//--start jack and sclang
* jackd -R -p 32 -d alsa -d hw:0 -n 3 &
* export SC_JACK_DEFAULT_INPUTS="system"
* export SC_JACK_DEFAULT_OUTPUTS="system"
* sclang
sc3> s.boot;
sc3> a= {SinOsc.ar*0.1}.play
sc3> a.free
sc3> s.quit
sc3> 0.exit;

