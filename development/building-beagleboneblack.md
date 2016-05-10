---
layout: catpage
category: development
title: Building From Source on BeagleBone Black
sort_order: 3
---

Compiling SC master natively on Beaglebone Black Debian Jessie
==

NOTE: the whole process takes about 1.5h.

requirements
--
* beaglebone black
* sd card with [bone-debian-8.3-console-armhf-2016-01-31-2gb.img](http://elinux.org/Beagleboard:BeagleBoneBlack_Debian) or newer jessie
* router with ethernet internet connection for the bbb
* laptop connected to same network as the bbb
* optional: usb soundcard with headphones or speakers connected

step1 (hardware setup)
--
1. connect an ethernet cable from the network router to the bbb
2. insert the sd card and usb soundcard
3. last connect usb power from a 5V@1A power supply

step2 (login & preparations)
--
1. `ssh debian@beaglebone.box`  #from your laptop, default password is temppwd
2. `sudo passwd debian`  #change password
3. `sudo /opt/scripts/tools/grow_partition.sh`  #expand file system
4. `sudo reboot`  #and log in again with ssh

step3 (update the system, install required libraries & compilers)
--
1. `sudo apt-get update`
2. `sudo apt-get upgrade`
3. `sudo apt-get install python-dev alsa-base libicu-dev libasound2-dev libsamplerate0-dev libsndfile1-dev libreadline-dev libxt-dev libudev-dev libavahi-client-dev libfftw3-dev cmake git gcc-4.8 g++-4.8`

step4 (compile & install jackd (no d-bus) )
--
1. `git clone git://github.com/jackaudio/jack2.git --depth 1`
2. `cd jack2`
3. `export CC=/usr/bin/gcc-4.8`
4. `export CXX=/usr/bin/g++-4.8`
5. `./waf configure --alsa`
6. `./waf build`
7. `sudo ./waf install`
8. `sudo ldconfig`
9. `cd ..`
10. `rm -rf jack2`
11. `sudo nano /etc/security/limits.conf`  #and add the following two lines at the end
  * `@audio - memlock 256000`
  * `@audio - rtprio 75`
12. `sudo nano /etc/ssh/sshd_config`  #at the bottom change to UsePAM yes
13. `sudo reboot`  #and log in again to make the limits and sshd settings work

step5 (compile & install sc master)
--
1. `git clone --recursive git://github.com/supercollider/supercollider.git supercollider`
2. `cd supercollider`
3. `git submodule init && git submodule update`
4. `mkdir build && cd build`
5. `export CC=/usr/bin/gcc-4.8`
6. `export CXX=/usr/bin/g++-4.8`
7. `cmake -L -DCMAKE_BUILD_TYPE="Release" -DBUILD_TESTING=OFF -DSUPERNOVA=OFF -DNOVA_SIMD=ON -DNATIVE=OFF -DSC_ED=OFF -DSC_WII=OFF -DSC_IDE=OFF -DSC_QT=OFF -DSC_EL=OFF -DSC_VIM=OFF -DCMAKE_C_FLAGS="-march=armv7-a -mtune=cortex-a8 -mfloat-abi=hard -mfpu=neon" -DCMAKE_CXX_FLAGS="-march=armv7-a -mtune=cortex-a8 -mfloat-abi=hard -mfpu=neon" ..`
8. `make`
9. `sudo make install`
10. `sudo ldconfig`
11. `cd ../..`
12. `rm -r supercollider`
13. `sudo mv /usr/local/share/SuperCollider/SCClassLibrary/Common/GUI /usr/local/share/SuperCollider/SCClassLibrary/scide_scqt/GUI`
14. `sudo mv /usr/local/share/SuperCollider/SCClassLibrary/JITLib/GUI /usr/local/share/SuperCollider/SCClassLibrary/scide_scqt/JITLibGUI`

step6 (start jack & sclang & test)
--
1. `jackd -P75 -dalsa -dhw:1 -p1024 -n3 -s -r44100 &`  #edit -dhw:1 to match your soundcard. usually it is 1 for usb
2. `sclang`  #should start sc and compile the class library with only 3 harmless class overwrites warnings
  * `s.boot`  #should boot the server
  * `a= {SinOsc.ar([400, 404])}.play`  #should play sound in both channels
  * `a.free`
  * `{1000000.do{2.5.sqrt}}.bench`  #benchmark: ~0.68 for bbb
  * `a= {Mix(50.collect{RLPF.ar(SinOsc.ar)});DC.ar(0)}.play`  #benchmark
  * `s.avgCPU`  #should show ~44%
  * `a.free`
  * `0.exit`  #quit sclang
4. `pkill jackd`  #quit jackd

notes
--
* if you get `WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!` when trying to ssh, type `ssh-keygen -R beaglebone.box` to reset
* if you get `perl: warning: Setting locale failed`. either ignore it or run the commands: `sudo apt-get install locales` and `sudo dpkg-reconfigure locales` and set en_US.UTF-8 UTF-8 twice
* we need to use gcc 4.8.4 instead of the default 4.9.2. something with gcc-4.9 triggers sc to generate the dreaded atIdentityHash error at startup.
* for lower latency, try with lower blocksizes when you start jackd.try for example `-p512` and `-p128`. tune downwards until you get dropouts and xruns (also watch cpu%)
* soundcards i’ve tried include a cheap blue 3D sound (C-Media Electronics, Inc. Audio Adapter (Planet UP-100, Genius G-Talk)) and the aureon dual usb (TerraTec Electronic GmbH Aureon Dual USB).
* lock/writeprotect the sd card if you plan to pull out the power without properly shutting down the system first. a better way is to add a shutdown command script to a gpio pin - search online for how to do that.
* if you want to use the sc3.7 branch instead of sc master (unstable), the process is the same except for the following additions: in step5, after #2 `git checkout 3.7`, in step5, after #12 `sudo mv /usr/local/share/SuperCollider/SCClassLibrary/Common/GUI/Base/Model.sc /usr/local/share/SuperCollider/SCClassLibrary/Common/Core/`

autostart (run sc at system boot)
--
1. `nano ~/autostart.sh`  #and add the following three lines...
  * `#!/bin/bash`
  * `/usr/local/bin/jackd -P75 -dalsa -dhw:1 -p1024 -n3 -s -r44100 &`
  * `su root -c "sclang -D /home/debian/mycode.scd"`
2. `chmod +x ~/autostart.sh`
3. `sudo crontab -e`  #and add the following line to the end...
  * `@reboot /bin/bash /home/debian/autostart.sh`
4. `nano ~/mycode.scd`  #and add your code inside a s.waitForBoot. for example...
  * `s.waitForBoot{ {SinOsc.ar([400, 404], 0, 0.5)}.play }`
5. `sudo reboot`  #and the sound should start after a few seconds. log in with ssh and `sudo pkill jackd && sudo pkill sclang` to stop it.



- - -

wheezy (older system)
==

here we use [bone-debian-7.9-console-armhf-2015-11-03-2gb.img](http://elinux.org/Beagleboard:BeagleBoneBlack_Debian)

for older debian wheezy the process is similar except you will need to install gcc-4.7, cmake 2.8.12 and build the 3.7 branch instead of master.

so for wheezy step3 and step5 are different and there are minor changes in step4. the rest is the same as for jessie above.

step3 (update the system, install required libraries & compilers for wheezy)
--
1. `sudo apt-get update`
2. `sudo apt-get upgrade`
3. `sudo apt-get install python-dev alsa-base libicu-dev libasound2-dev libsamplerate0-dev libsndfile1-dev libreadline-dev libxt-dev libudev-dev libavahi-client-dev libfftw3-dev cmake git gcc-4.7 g++-4.7 build-essential`
4. `wget http://www.cmake.org/files/v2.8/cmake-2.8.12.1.tar.gz`
5. `tar xvf cmake-2.8.12.1.tar.gz`
6. `cd cmake-2.8.12.1`
7. `export CC=/usr/bin/gcc-4.7`
8. `export CXX=/usr/bin/g++-4.7`
9. `cmake . && make`

then in step4, #3 and #4 should read...

* `export CC=/usr/bin/gcc-4.7`
* `export CXX=/usr/bin/g++-4.7`

step5 (compile & install sc 3.7)
--
1. `git clone --recursive git://github.com/supercollider/supercollider.git supercollider`
2. `cd supercollider`
3. `git checkout 3.7`
4. `git submodule init && git submodule update`
5. `mkdir build && cd build`
6. `export CC=/usr/bin/gcc-4.7`
7. `export CXX=/usr/bin/g++-4.7`
8. `~/cmake-2.8.12.1/bin/cmake -L -DCMAKE_BUILD_TYPE="Release" -DBUILD_TESTING=OFF -DSUPERNOVA=OFF -DNOVA_SIMD=ON -DNATIVE=OFF -DSC_ED=OFF -DSC_WII=OFF -DSC_IDE=OFF -DSC_QT=OFF -DSC_EL=OFF -DSC_VIM=OFF -DCMAKE_C_FLAGS="-march=armv7-a -mtune=cortex-a8 -mfloat-abi=hard -mfpu=neon" -DCMAKE_CXX_FLAGS="-march=armv7-a -mtune=cortex-a8 -mfloat-abi=hard -mfpu=neon" ..`
9. `make`
10. `sudo make install`
11. `sudo ldconfig`
12. `cd ../..`
13. `rm -r supercollider`
14. `sudo mv /usr/local/share/SuperCollider/SCClassLibrary/Common/GUI/Base/Model.sc /usr/local/share/SuperCollider/SCClassLibrary/Common/Core/`
15. `sudo mv /usr/local/share/SuperCollider/SCClassLibrary/Common/GUI /usr/local/share/SuperCollider/SCClassLibrary/scide_scqt/GUI`
16. `sudo mv /usr/local/share/SuperCollider/SCClassLibrary/JITLib/GUI /usr/local/share/SuperCollider/SCClassLibrary/scide_scqt/JITLibGUI`
