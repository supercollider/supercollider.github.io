---
layout: page
title: Downloads
---

Jump to:
[Mac](#mac) - [Linux](#linux) - [Windows](#windows) - [Other Platforms](#other-platforms)

------

{% for os in site.data.downloads.os %}
## {{ os.slug }}
{% for category in os.categories %}
#### {{ category.name | capitalize }}
{{ category.start_text }}
{% for download in category.downloads %}
- [{{ download.name }}]({{ download.link }})
{% endfor %}
{{ category.end_text }}
{% endfor %}
------
{% endfor %}

## Other Platforms

SuperCollider can be used on embedded platforms, including Raspberry Pi and Beagle Bone Black.  
See the [project READMEs](https://github.com/supercollider/supercollider) for more information.

## Releases

[SuperCollider releases](https://github.com/supercollider/supercollider/releases) (including Stable Releases, Betas, and Release Candidates).

## Building From Source

Build instruction can be found on [GitHub](https://github.com/supercollider/supercollider) in the README corresponding to your Operating System.

## Plugins And Extensions

#### SC3 Plugins

[https://supercollider.github.io/sc3-plugins](https://supercollider.github.io/sc3-plugins)

The sc3-plugins are extension plugins for the SuperCollider audio synthesis server.  
These third-party plugins provide additional synthesis, analysis, and other capabilities for the sound server.

#### Quarks

[https://github.com/supercollider-quarks/quarks](https://github.com/supercollider-quarks/quarks)

Quarks are packages containing classes, extension methods, documentation and UGens.  
The integrated Quarks package system is used to download and manage these packages on your system.
