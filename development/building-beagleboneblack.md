---
layout: catpage
category: development
title: Building From Source on BeagleBone Black
sort_order: 3
---

Compiling SC3.7alpha0 natively on Beaglebone Black Debian
==

NOTE: the whole process takes about 1.5h.

NOTE: in step5 it is assumed there is an usb soundcard/adapter connected. It might work with hdmi audio also but this is untested.

step1 (startup)
--
1. download and transfer [debian-wheezy-7.2-armhf-3.8.13-bone30.img](http://www.armhf.com/index.php/download/) to a sdcard. NOTE: For the moment, do not use a debian version newer than 7.4.
2. put the sdcard in the bbb (on osx try [PiFiller](http://ivanx.com/raspberrypi/)), connect an ethernet cable and 5v power.
3. figure out the IP of the bbb (on osx try [LanScan](https://itunes.apple.com/app/lanscan/id472226235)) and log in with `ssh debian@x.x.x.x`. the default password is `debian`.

step2 (preparation)
--
1. `sudo dpkg-reconfigure tzdata` # set timezone
2. `sudo ntpdate pool.ntp.org` # set time
3. `sudo apt-get update`
4. `sudo apt-get upgrade`
5. `sudo apt-get install build-essential git cmake alsa-base libasound2-dev libsamplerate0-dev libsndfile1-dev libavahi-client-dev libicu-dev libreadline-dev libfftw3-dev libxt-dev` # this takes a while
6. `sudo depmod` # for alsa
7. `sudo adduser debian audio`

step3 (install jack2 from github)
--
1. `git clone git://github.com/jackaudio/jack2.git`
2. `cd jack2`
3. `./waf configure --alsa`
4. `./waf build` # this takes a while
5. `sudo ./waf install`
6. `cd ..`
7. `sudo rm -r jack2`
8. `sudo ldconfig`
9. `sudo reboot`

step4 (install sc3.7alpha0 from github and build with gcc)
--
1. `git clone --recursive git://github.com/supercollider/supercollider.git supercollider`
2. `cd supercollider`
3. `git checkout ddd8c8d75dd00263acf593b062ecbb06686a4574` # need an older version from july2013 that still can use gcc
4. `git submodule init && git submodule update`
5. `mkdir build && cd build`
6. `CC="gcc" CXX="g++" cmake -L -DCMAKE_BUILD_TYPE="Release" -DBUILD_TESTING=OFF -DSSE=OFF -DSSE2=OFF -DSUPERNOVA=OFF -DNOVA_SIMD=ON -DNATIVE=OFF -DSC_QT=OFF -DSC_WII=OFF -DSC_ED=OFF -DSC_IDE=OFF -DSC_EL=OFF -DCMAKE_C_FLAGS="-march=armv7-a -mtune=cortex-a8 -mfloat-abi=hard -mfpu=neon" -DCMAKE_CXX_FLAGS="-march=armv7-a -mtune=cortex-a8 -mfloat-abi=hard -mfpu=neon" ..` # should add '-ffast-math -O3' here but then gcc4.6.3 crashes
7. `make` # this takes a while
8. `sudo make install`
9. `cd ../..`
10. `sudo rm -r supercollider`
11. `sudo ldconfig`
12. `sudo reboot`

step5 (start jack & sclang & test sound)
--
1. `jackd -dalsa -dhw:1,0 -p128 -n3 -s &` # if distorting try with larger blocksize e.g. -p1024
2. `sclang` # ignore the error "ERROR: No GUI scheme active" - it is harmless.
3. `s.boot;`
4. `a= {SinOsc.ar([400, 404], 0, 0.1)}.play;`
5. `s.dump;`
6. `a.free;`
7. `s.quit;`
8. `0.exit;`
9. `pkill jackd`

step6 (low latency with realtime privileges)
--
1. `sudo pico /etc/security/limits.conf`
2. and add the following lines somewhere before it says end of file.
3.    `@audio - memlock 256000`
4.    `@audio - rtprio 99`
5.    `@audio - nice -19`
6. save and exit with ctrl+o, ctrl+x
7. `sudo pico /etc/ssh/sshd_config`
8. and at the bottom change to `UsePAM yes`
9. `sudo reboot`
10. done. after reboot start jack+sc again like in previous step







Compiling SC3.7alpha0 on Beaglebone Black Debian using OSX, a cross-compiler & DISTCC
==
NOTE: this is mainly useful for speeding up compiling. It's probably better to compile natively like above.

This assumes OSX10.8.4, homebrew and a fresh debian-wheezy-7.2-armhf-3.8.13-bone30.img on a sdcard,
but should also work on linux and windows if you install the cross-compiler and distcc.

step0 (osx: install compiler, distcc & start server)
--
1. install the arm-linux-gnueabihf cross-compiler. it is easiest from [www.cety.de/ctbot/arm-linux-gnueabihf.pkg](http://www.cety.de/ctbot/arm-linux-gnueabihf.pkg).
2. `export PATH=$PATH:/usr/local/arm-linux/bin`
3. `brew install distcc`
4. `distccd --daemon --allow 192.168.1.0/24 --no-detach` # edit to match root of your ip domain

then follow step1, step2 and step3 above.

step4 (install sc3.7alpha0 from github and build with distcc)
--
1. `sudo apt-get install distcc`
2. `sudo ln -s /usr/bin/gcc /usr/local/bin/arm-linux-gcc` # this to make sure the bbb cc is called the same as the osx cc
3. `sudo ln -s /usr/bin/g++ /usr/local/bin/arm-linux-g++` # this to make sure the bbb cxx is called the same as the osx cxx
4. `sudo ldconfig`
5. `git clone --recursive git://github.com/supercollider/supercollider.git supercollider`
6. `cd supercollider`
7. `git checkout ddd8c8d75dd00263acf593b062ecbb06686a4574` # need an older version from july2013 that still can use gcc
8. `git submodule init && git submodule update`
9. `mkdir build && cd build`
10. `export DISTCC_HOSTS='192.168.1.51'` # edit to match your osx computer ip
11. `export DISTCC_IO_TIMEOUT=3000`
12. `export DISTCC_SKIP_LOCAL_RETRY=1`
13. `CC="distcc arm-linux-gcc" CXX="distcc arm-linux-g++" cmake -L -DCMAKE_BUILD_TYPE="Release" -DBUILD_TESTING=OFF -DSSE=OFF -DSSE2=OFF -DSUPERNOVA=OFF -DNOVA_SIMD=ON -DNATIVE=OFF -DSC_QT=OFF -DSC_WII=OFF -DSC_ED=OFF -DSC_IDE=OFF -DSC_EL=OFF -DCMAKE_C_FLAGS="-march=armv7-a -mtune=cortex-a8 -mfloat-abi=hard -mfpu=neon" -DCMAKE_CXX_FLAGS="-march=armv7-a -mtune=cortex-a8 -mfloat-abi=hard -mfpu=neon" ..` # should add '-ffast-math -O3' here but then gcc4.6.3 crashes
14. check the output and make sure it says: Check for working C compiler: /usr/bin/distcc -- works
15. `make -j4`
16. `sudo make install`
17. `cd ../..`
18. `sudo rm -r supercollider`
19. `sudo ldconfig`
20. `sudo reboot`

now do step5 and step6 above.
