---
layout: post
title: "BEASTmulch multichannel system released"
description: ""
category: releases
author: dan
tags: []
---
Scott Wilson today announced the release of the BEASTmulch system, developed as part of an AHRC-funded research project exploring approaches to large-scale multichannel electroacoustic composition and presentation.

Downloads at: http://www.beast.bham.ac.uk/research/mulch.shtml

For more information: beastmulch-info@contacts.bham.ac.uk

BEASTmulch System

BEASTmulch System is a software tool for the presentation of electroacoustic music over multichannel systems. Designed primarily with a classic "live diffusion" model in mind, it is nevertheless flexible enough to be adapted for a number of purposes, and can support input and output configurations of arbitrary complexity (i.e. live inputs, soundfiles with varying numbers of channels, etc.).

The software has numerous features (e.g. realtime reconfigurable routing, channel processing, automation, etc.), incorporates various standard and non-standard spatialisation techniques (VBAP, ambisonics, etc.), and adapts easily to both small and large (i.e. > 100 loudspeakers) systems.

BEASTmulch System is the software component of the BEAST concert system.

System Requirements: Mac OSX 10.4 - 10.5 (10.6 compatibility forthcoming)

**BEASTmulchLib**

BEASTmulchLib is a SuperCollider class library designed for use in the creation, processing and presentation of complex multichannel signal chains. Objects include sources, matrix routers and mixers, and sound processors and spatialisers. The latter are based on a simple user-extensible plugin architecture. Many classes have elegant GUI representations.

The library also includes classes which represent a variety of different controllers, including MIDI controllers, GUI Faders, EtherSense, etc., and provides support for controller automation (i.e automated mixing and diffusion).

It supports a number of common spatialisation techniques, such as Ambisonics, and includes SC ports of Ville Pullki's Vector Base Amplitude Panning (VBAP), and the Loris analysis resynthesis method. It also supports some idiosyncratic techniques, such as Spatial Swarm Granulation, and provides utility classes for Speaker Array balancing and visualisation.

N.B. Currently the library is not fully cross-platform: GUI classes and UGens are OSX only.

