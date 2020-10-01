SUPER_COLLIDER.Github.io
=======================

Front pages for supercollider

Usage
--------

Clone this repository:

    git clone git://github.com/supercollider/supercollider.github.io.git
    cd supercollider.github.io

To view these pages locally, you must install `jekyll` using the Ruby Gem package manager.  
You will need Ruby Gems of course.

First, install the standard `bundler` gem which reads Gemfiles and installs isolated gems for a project:

    gem install bundler
    
and then from the supercollider.github.io directory run:

    bundle install
    
which will use the Gemfile found in that directory and will install an isolated copy of github-pages in that directory.


Now run `Jekyll`:

    jekyll serve --watch

or:

    jekyll help
    
Then, in your browser:

    http://localhost:4000
