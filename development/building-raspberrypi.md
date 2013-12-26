---
layout: catpage
category: development
title: Building From Source on Raspberry Pi
sort_order: 3
---

Note
--
If you just quickly want to install and run an older version of sc, you can follow the instructions here... [sam.aaron.name/2012/11/02/supercollider-on-pi.html](http://sam.aaron.name/2012/11/02/supercollider-on-pi.html).

Compiling SC3.7alpha0 natively on Raspberry Pi Raspbian
==

The latest raspbian versions come with sc3.4.5 pre installed, but this supercollider version is old, slow and lack readline support. The 3.7 you build below will work better in many respects - it just takes time to do it.

NOTE: the whole process takes many hours.

step1 (startup)
--
1. download and transfer the latest Raspbian (as of writing [2013-12-20-wheezy-raspbian.zip](http://www.raspberrypi.org/downloads)) to a sdcard.
2. put the sdcard in the rpi (on osx try [PiFiller](http://ivanx.com/raspberrypi/)), connect an ethernet cable and 5v power.
3. figure out the IP of the rpi (on osx try [LanScan](https://itunes.apple.com/app/lanscan/id472226235)) and log in with `ssh pi@x.x.x.x`. the default password is `raspberry`.

step2 (preparation)
--
1. log in and type `sudo raspi-config`, select expand file system, set timezone, finish and reboot
2. `sudo apt-get update`
3. `sudo apt-get upgrade` # this might take a while
4. `sudo apt-get remove jackd` # remove old jack and old supercollider
5. `sudo apt-get autoremove`
6. `sudo apt-get install cmake libasound2-dev libsamplerate0-dev libsndfile1-dev libavahi-client-dev libicu-dev libreadline-dev libfftw3-dev libxt-dev`
7. `sudo ldconfig`

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
6. `sudo dd if=/dev/zero of=/swapfile bs=1MB count=512` # create a temporary swap file
7. `sudo mkswap /swapfile`
8. `sudo swapon /swapfile`
9. `CC="gcc" CXX="g++" cmake -L -DCMAKE_BUILD_TYPE="Release" -DBUILD_TESTING=OFF -DSSE=OFF -DSSE2=OFF -DSUPERNOVA=OFF -DNOVA_SIMD=ON -DNATIVE=OFF -DSC_QT=OFF -DSC_WII=OFF -DSC_ED=OFF -DSC_IDE=OFF -DSC_EL=OFF -DCMAKE_C_FLAGS="-march=armv6 -mtune=arm1176jzf-s -mfloat-abi=hard -mfpu=vfp" -DCMAKE_CXX_FLAGS="-march=armv6 -mtune=arm1176jzf-s -mfloat-abi=hard -mfpu=vfp" ..` # should add '-ffast-math -O3' here but then gcc4.6.3 fails
10. `make` # this takes a while
11. `sudo make install`
12. `cd ../..`
13. `sudo rm -r supercollider`
14. `sudo swapoff /swapfile`
15. `sudo rm /swapfile`
16. `sudo ldconfig`
17. `echo "export SC_JACK_DEFAULT_INPUTS=\"system\"" >> ~/.bashrc`
18. `echo "export SC_JACK_DEFAULT_OUTPUTS=\"system\"" >> ~/.bashrc`
19. `sudo reboot`

step5 (start jack & sclang & test sound)
--
1. `jackd -p32 -dalsa -dhw:0,0 -p1024 -n3 -s &` # built-in sound. change to -dhw:1,0 for usb sound card (see more below)
2. `scsynth -u 57110 &`
3. `sclang` # ignore the error “ERROR: No GUI scheme active” - it is harmless.
4. `s.boot;`
5. `a= {SinOsc.ar([400, 404], 0, 0.1)}.play;`
6. `s.dump;`
7. `a.free;`
8. `0.exit;`
9. `pkill jackd`

optional: step6 (low latency with realtime privileges and an usb soundcard)
--
1. `sudo pico /etc/security/limits.conf`
2. and add the following lines somewhere before it says end of file.
3.    `@audio - memlock 256000`
4.    `@audio - rtprio 99`
5.    `@audio - nice -19`
6. save and exit with ctrl+o, ctrl+x
7. `sudo halt`
8. power off the rpi and insert the sd card in your laptop.
9. `dwc_otg.speed=1` # add the following to beginning of /boot/cmdline.txt (see <http://wiki.linuxaudio.org/wiki/raspberrypi> under force usb1.1 mode)
10. eject the sd card and put it back in the rpi, make sure usb soundcard is connected and power on again.
11. log in with ssh and now you can start jack with a lower blocksize...
12. `jackd -p32 -dalsa -dhw:1,0 -p256 -n3 -s &` # uses an usb sound card and lower blocksize
13. continue like in step5.2 above

links:
--
* <http://wiki.linuxaudio.org/wiki/raspberrypi>



Compiling SC3.7alpha0 on Raspberry Pi Raspbian using OSX, a cross-compiler & DISTCC
==
NOTE: this is mainly useful for speeding up compiling. It's probably better to compile natively like above.

This assumes OSX10.8.4, homebrew and a fresh 2013-09-25-wheezy-raspbian.img on a sdcard,
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
13. `CC="distcc arm-linux-gcc" CXX="distcc arm-linux-g++" cmake -L -DCMAKE_BUILD_TYPE="Release" -DBUILD_TESTING=OFF -DSSE=OFF -DSSE2=OFF -DSUPERNOVA=OFF -DNOVA_SIMD=ON -DNATIVE=OFF -DSC_QT=OFF -DSC_WII=OFF -DSC_ED=OFF -DSC_IDE=OFF -DSC_EL=OFF -DCMAKE_C_FLAGS="-march=armv6 -mtune=arm1176jzf-s -mfloat-abi=hard -mfpu=vfp" -DCMAKE_CXX_FLAGS="-march=armv6 -mtune=arm1176jzf-s -mfloat-abi=hard -mfpu=vfp" ..` # should add '-ffast-math -O3' here but then gcc4.6.3 fails
14. check the output and make sure it says: Check for working C compiler: /usr/bin/distcc -- works
15. `make -j4`
16. `sudo make install`
17. `cd ../..`
18. `sudo rm -r supercollider`
19. `sudo ldconfig`
20. `echo "export SC_JACK_DEFAULT_INPUTS=\"system\"" >> ~/.bashrc`
21. `echo "export SC_JACK_DEFAULT_OUTPUTS=\"system\"" >> ~/.bashrc`
22. `sudo reboot`

now do step5 and step6 above.

links:
--
* <http://jeremy-nicola.info/portfolio-item/cross-compilation-distributed-compilation-for-the-raspberry-pi/>
