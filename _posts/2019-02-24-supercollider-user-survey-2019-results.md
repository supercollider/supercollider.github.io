---
layout: post
title: "SuperCollider User Survey 2019 Results"
description: ""
category: survey
author: brian
tags: [survey]
---

At long last, we are happy to share these results from the 2019 SuperCollider survey! In total, we
had 253 responses from friends of the SuperCollider project around the world. We're incredibly
thankful to everyone who gave their time and energy to respond so thoughtfully; these results will
be invaluable in guiding future development work and in informing community discussion. Based on the
enthusiasm we've seen, we certainly hope to do this again next year!

Here are a few of the top takeaways from this year's results:

- **Platforms**: a plurality of users work on macOS; Linux is the second most popular desktop OS,
  followed by Windows. Embedded platforms such as Raspberry Pi, BELA, and BeagleBone are also
  popular, with about as many users reporting that they use Raspberry Pi as Windows.

- **Version**: about two-thirds of users are already on 3.10, the latest release at the time of the
  survey. This number is very important to us as developers, as it indicates how confident users
  feel in moving to new versions. We're hoping to see this percentage rise in the next survey.

- **Client**: sclang is the most popular way to interact with scsynth by a large margin; TidalCycles and
  Sonic Pi also seem quite popular.

- **Features**: we provided a list of possible features and improvements we'd like to implement across
  the codebase; of those given, the top two most-demanded were quality pitch, formant, and time
  manipulation UGens, and (2) improvements to compiler warnings and error messages.  This gives us a
  very clear idea of what projects to tackle next.

- **Development focus**: when asked where the most development effort should go, votes were practically
  split in a three-way tie between documentation, sclang, and UGens, with scsynth a close fourth.

Below, we present aggregated data for each survey question. In the next few weeks you might see more
posts from some of the developers sharing their thoughts on the survey. We're very excited to see
what the community thinks of these results!

At the end of this post, you'll find the data in these charts presented as text tables for easy
access.

# Results

### Question 1

![Chart 01-How long have you used SuperCollider?](/images/survey2019_charts/01_supercollider_years_used.svg)

### Question 2

![Chart 02-Which best describes your level of proficiency?](/images/survey2019_charts/02_supercollider_proficiency.svg)

### Question 3

![Chart 03-As a user, I think of SuperCollider as](/images/survey2019_charts/03_user_thinks.svg)

### Question 4

![Chart 04-What are the platforms on which you use SuperCollider?](/images/survey2019_charts/04_supercollider_platforms.svg)

### Question 5

![Chart 05-What version(s) of SuperCollider do you currently use?](/images/survey2019_charts/05_supercollider_versions.svg)

### Question 6

Note: Quarks with fewer than five mentions are not included in this list.

![Chart 06-What quarks do you use, if any?](/images/survey2019_charts/06_quarks_used.svg)

### Question 7

![Chart 07-Which clients do you use?](/images/survey2019_charts/07_supercollider_clients.svg)

### Question 8

![Chart 08-Have you heard of supernova?](/images/survey2019_charts/08_heard_supernova.svg)

### Question 9

These responses were difficult to categorize; answers that had fewer than four mentions are not
included here. Hopefully, this chart gives a good sense of the broad range of uses people have found
for SuperCollider.

![Chart 09-What do you use SuperCollider for?](/images/survey2019_charts/09_supercollider_uses.svg)

### Question 10

This list is the top twenty most frequent answers we received; in total there
were over 180 unique tools mentioned in response to this question!

![Chart 10-What other tools do you use?](/images/survey2019_charts/10_other_tools.svg)

### Question 11

These are the top ten most frequent answers we received.

![Chart 11-What are the biggest pain points you have encountered while using SuperCollider?](/images/survey2019_charts/11_supercollider_pain_points.svg)

### Question 12

Responses with fewer than four answers are not included here.

![Chart 12-What resources have been useful to you in learning SuperCollider?](/images/survey2019_charts/12_what_resources_learning.svg)

### Question 13: How would you describe your experience learning SuperCollider?

This question was very personal, and the responses were difficult to place in any sort of
categorization. We have decided to keep them private, but future posts from the development team
may reflect on them.

### Question 14: How has your experience been interacting with the SuperCollider community?

The responses to this question were difficult to categorize. We hope you find this word cloud
informative, or at least amusing.

![Community Experience Word Cloud](/images/survey2019_charts/14_community_word_cloud.png)

### Question 15

![Chart 15-Where do you discuss SuperCollider?](/images/survey2019_charts/15_discuss_supercollider.svg)

### Questions 16-41: Development project ideas

The methodology for calculating these scores was:

- "I would love this" = 3 pts
- "I would use this" = 2 pts
- "I want this" = 1 pt
- "Don't care" / no response = 0 pts

![Chart 16-Development project ideas](/images/survey2019_charts/16_new_features.svg)

### Question 42: Suggestion box: Any features you want to see?

We received a great variety of answers to this question, and it would be too difficult to try to
boil them down to some aggregated format. Some of the more popular ones were:

- make it possible to use scsynth as a VST plugin
- add a specific UGen, or more UGens related to a particular topic
- make it easier to visualize the state of the server
- improve GUI objects and make writing GUI code easier
- improve MIDI support
- improve the IDE with a variety of new features

### Question 43

![Chart 43-Where you would like to see the most development effort go in the future?](/images/survey2019_charts/43_development_effort.svg)

### Question 44

![Chart 44-I use SuperCollider as a](/images/survey2019_charts/44_use_supercollider_as.svg)

### Question 45

![Chart 45-How do you identify your gender?](/images/survey2019_charts/45_gender.svg)

# Text charts

## 1. How long have you used SuperCollider?

| Duration           | Count | %     |
|--------------------|-------|-------|
| more than 10 years | 64    | 25.9% |
| 6 to 10 years      | 56    | 22.7% |
| 4 or 5 years       | 37    | 15.0% |
| 2 or 3 years       | 49    | 19.8% |
| 1 year or less     | 41    | 16.6% |

## 2. Which best describes your level of proficiency?

| Level                                                                                                              | Count | %     |
|--------------------------------------------------------------------------------------------------------------------|-------|-------|
| I am new to SuperCollider and learning how to build basic things.                                                  | 27    | 10.9% |
| I'm comfortable with basic features of SC, and learning how to put them to use in medium-sized project.            | 58    | 23.5% |
| I have completed small projects and can often help myself or other people. I'm learning to build complex projects. | 69    | 27.9% |
| I have built complex, large-scale projects in SC, and feel comfortable helping myself and others.                  | 93    | 37.7% |

## 3. As a user, I think of SuperCollider as...

| Adjective  | Count |
|------------|-------|
| powerful   | 240   |
| fun        | 187   |
| difficult  | 113   |
| dependable | 105   |
| a toy      | 24    |
| unstable   | 18    |

## 4. What are the platforms on which you use SuperCollider?

| Platform     | Count |
|--------------|-------|
| macOS        | 179   |
| Linux        | 108   |
| Raspberry Pi | 64    |
| Windows      | 57    |
| BELA         | 21    |
| BeagleBone   | 10    |
| Prynth       | 5     |
| Norns        | 2     |
| FreeBSD      | 1     |

## 5. What version(s) of SuperCollider do you currently use?

| Version                         | Count |
|---------------------------------|-------|
| Unreleased development versions | 31    |
| 3.10                            | 164   |
| 3.9                             | 90    |
| 3.8                             | 18    |
| 3.7                             | 10    |
| 3.5, 3.6                        | 18    |
| 3.4 or older SC3                | 6     |
| SC2 or SC1                      | 1     |

## 6. What quarks do you use, if any?


| Quark Name       | Count |
|------------------|-------|
| wslib            | 39    |
| mathlib          | 24    |
| atk              | 17    |
| superdirt        | 16    |
| bjorklund        | 16    |
| xml              | 14    |
| ctk              | 13    |
| modality         | 13    |
| cruciallib       | 12    |
| feedback         | 10    |
| arduino          | 10    |
| ddw              | 10    |
| jitlibextensions | 10    |
| miscellaneouslib | 10    |
| batlib           | 9     |
| wavesets         | 8     |
| vowel            | 7     |
| adclib           | 7     |
| jitlib           | 6     |
| filelog          | 6     |
| utopia           | 5     |
| tabbedview       | 5     |
| safetynet        | 5     |

## 7. Which client(s) do you use?

| Client                   | Count |
|--------------------------|-------|
| sclang                   | 233   |
| TidalCycles              | 41    |
| Sonic Pi                 | 18    |
| Overtone                 | 6     |
| ScalaCollider            | 3     |
| cl-collider              | 3     |
| custom client / OSC only | 3     |
| FoxDot                   | 2     |
| Monome Norns             | 1     |
| supercollider.js         | 1     |

## 8. Have you heard of supernova?

| Response                                           | Count | %     |
|----------------------------------------------------|-------|-------|
| I have heard of it, but never used it              | 146   | 59.1% |
| I have never heard of it                           | 37    | 15.0% |
| I use it occasionally, depending on the task       | 33    | 13.4% |
| I tried it, but I don't plan on coming back to it  | 16    | 6.5%  |
| I can't use it because it's not supported on my OS | 9     | 3.6%  |
| It's my default synthesis engine                   | 6     | 2.4%  |

## 9. What do you use SuperCollider for?

| Response                                      | Count |
|-----------------------------------------------|-------|
| composition/music/projects                    | 120   |
| sound design/sound synthesis                  | 75    |
| improvisation/live electronics                | 46    |
| algorithmic composition                       | 38    |
| performance                                   | 37    |
| live coding                                   | 35    |
| installations                                 | 35    |
| instruments                                   | 31    |
| teach                                         | 28    |
| prototyping ideas/prototyping DSP/experiments | 27    |
| DSP/effects                                   | 26    |
| acousmatic composition                        | 25    |
| interface with other tools                    | 25    |
| learning                                      | 19    |
| as a general programming language             | 17    |
| interactive system                            | 16    |
| research                                      | 12    |
| fixed media                                   | 10    |
| data sonification                             | 7     |
| music production                              | 6     |
| visuals                                       | 6     |
| sound analysis                                | 4     |
| making apps                                   | 4     |
| dance pieces                                  | 4     |
| sound art                                     | 4     |

## 10. What other tools do you use?

| Response        | Count |
|-----------------|-------|
| Reaper          | 57    |
| Max/MSP         | 53    |
| Ableton Live    | 39    |
| hardware synths | 33    |
| Logic           | 30    |
| Pure Data       | 26    |
| Python          | 25    |
| Audacity        | 24    |
| Processing      | 20    |
| Ardour          | 16    |
| openFrameworks  | 16    |
| Arduino         | 15    |
| TidalCycles     | 12    |
| Pro Tools       | 10    |
| Bitwig Studio   | 9     |
| Renoise         | 7     |
| Jitter          | 6     |
| Csound          | 5     |
| Lilypond        | 5     |
| OpenMusic       | 5     |

## 11. What are the biggest pain points you have encountered while using SuperCollider?

| Response                                                     | Count |
|--------------------------------------------------------------|-------|
| documentation is outdated/missing/unclear                    | 30    |
| error messages from sclang are difficult to understand       | 22    |
| difficult to understand sclang/server separation             | 18    |
| debugging in sclang is difficult                             | 17    |
| sclang syntax is difficult                                   | 15    |
| tutorials/introductory material are missing/difficult to use | 13    |
| IDE is missing features I want                               | 11    |
| sclang has too many ways to do things                        | 8     |
| making GUIs is difficult                                     | 7     |
| sclang has no dynamic class loading                          | 7     |

## 12. What resources have been useful to you in learning SuperCollider?

| Resource                                               | Count |
|--------------------------------------------------------|-------|
| project documentation, tutorials, and guides           | 163   |
| mailing list                                           | 79    |
| Eli Fieldsteel tutorials                               | 70    |
| The SuperCollider Book (Wilson/Cottle/Collins)         | 69    |
| classroom education                                    | 30    |
| forum                                                  | 24    |
| sccode.org                                             | 23    |
| YouTube videos                                         | 21    |
| Nick Collins tutorial                                  | 18    |
| internet                                               | 17    |
| A Gentle Introduction to SuperCollider (Bruno Ruviaro) | 15    |
| friends and colleagues                                 | 13    |
| reading code                                           | 13    |
| Introduction to SuperCollider (Andrea Valle)           | 13    |
| Slack                                                  | 11    |
| GitHub                                                 | 10    |
| workshops                                              | 10    |
| Computer Music with Examples in SC 3 (Cottle)          | 9     |
| Facebook group                                         | 6     |
| meetups                                                | 4     |

## 13. How would you describe your experience learning SuperCollider?

See note above.

## 14. How has your experience been interacting with the SuperCollider community?

See note above.

## 15. Where do you discuss SuperCollider?

| Venue                                   | Count |
|-----------------------------------------|-------|
| sc-users mailing list                   | 143   |
| Facebook group(s)                       | 94    |
| scsynth.org Discourse forum             | 81    |
| sccode.org                              | 72    |
| GitHub issue tracker                    | 48    |
| sc-dev mailing list                     | 47    |
| Slack                                   | 38    |
| I don't participate in the SC community | 31    |
| colleagues/friends                      | 13    |
| lines forum (https://llllllll.co/)      | 9     |
| talk.lurk.org                           | 9     |
| local meetups                           | 8     |
| r/supercollider subreddit               | 5     |
| classmates/teachers/students            | 3     |
| concerts/events                         | 2     |
| workshops                               | 1     |
| Twitter                                 | 1     |
| IRC                                     | 1     |
| Discord                                 | 1     |

## 16.-41. Development project ideas

See note on methodology above.

| Idea                                                                                                    | Score |
|---------------------------------------------------------------------------------------------------------|-------|
| \[UGens\] Quality pitch/formant/time manipulation                                                       | 535   |
| \[sclang\] More and better compiler warnings and error messages                                         | 523   |
| \[sclang\] A debugger that can support breakpoints and step through code interactively                  | 462   |
| \[UGens\] More reverbs                                                                                  | 458   |
| \[UGens\] More virtual analog filters                                                                   | 446   |
| \[UGens\] Physical models of instruments                                                                | 416   |
| \[UGens\] More compressors                                                                              | 402   |
| \[IDE\] Metering panels (volume meter, spectrograph, etc.) integrated into the main window              | 387   |
| \[UGens\] Antialiased distortion                                                                        | 377   |
| \[IDE\] Better autocomplete                                                                             | 377   |
| \[scsynth\] scsynth as a VST guest                                                                      | 376   |
| \[scsynth\] scsynth as a VST host                                                                       | 370   |
| \[scsynth\] Efficient single-sample feedback                                                            | 369   |
| \[sclang\] Being able to load or reload class files without restarting sclang ("dynamic class loading") | 353   |
| \[IDE\] More control over indentation                                                                   | 323   |
| \[IDE\] Multiline cursor/block selection mode                                                           | 315   |
| \[scsynth\] Oversampling in the UGen graph                                                              | 313   |
| \[IDE\] Support for macros or snippets                                                                  | 311   |
| \[sclang\] Being able to easily write and use C++ code in sclang ("language plugins")                   | 296   |
| \[IDE\] Code folding                                                                                    | 288   |
| \[sclang\] Better looking GUI components                                                                | 279   |
| \[scsynth\] scsynth in the browser via WebAssembly                                                      | 268   |
| \[IDE\] Refactoring tools                                                                               | 253   |
| \[sclang\] A namespace language feature                                                                 | 250   |
| \[IDE\] Custom syntax highlighting support                                                              | 238   |
| \[sclang\] Support for Ableton Link                                                                     | 214   |

## 42. Suggestion box

See note above.

## 43. Where you would like to see the most development effort go in the future?

| Component                     | Count |
|-------------------------------|-------|
| tutorials and documentation   | 123   |
| sclang (language)             | 118   |
| UGens                         | 116   |
| scsynth (server)              | 101   |
| IDE                           | 82    |
| interfaces with other tools   | 76    |
| supernova (server)            | 48    |
| stability                     | 3     |
| standalone support            | 2     |
| MIDI                          | 1     |
| embedded system support       | 1     |
| language interoperability     | 1     |
| OSC visualization             | 1     |
| mailing list / forum          | 1     |
| easier to create UGens        | 1     |
| support for older OS's        | 1     |
| SuperCollider project concept | 1     |
| video tutorials               | 1     |
| sample-accurate timing        | 1     |
| graphic/musical notation      | 1     |

## 44. I use SuperCollider as a(n) ________.

| Response         | Count |
|------------------|-------|
| Artist           | 234   |
| Researcher       | 86    |
| Teacher/Educator | 82    |
| Student          | 52    |
| Hobbyist         | 7     |
| Developer        | 2     |
| Game developer   | 1     |
| Music producer   | 1     |
| Sound designer   | 1     |

## 45. How do you identify your gender?

| Response              | Count | %      |
|-----------------------|-------|--------|
| male                  | 210   | 85.02% |
| prefer not to respond | 15    | 6.07%  |
| female                | 13    | 5.26%  |
| nonbinary             | 9     | 3.64%  |

