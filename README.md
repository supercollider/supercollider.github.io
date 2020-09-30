supercollider.github.io
=======================

Front pages for supercollider

Usage
--------
1]
Clone this repository:

    git clone git://github.com/supercollider/supercollider.github.io.git
    cd supercollider.github.io
2]
To view these pages locally, you must install `jekyll` using the Ruby Gem package manager.

*You will need Ruby Gems of course.*

3]
First, install the standard `bundler` gem which reads Gemfiles and installs isolated gems for a project:

    gem install bundler
    
4]    
then from the supercollider.github.io directory run:

    bundle install
    
 5]   
which will use the Gemfile found in that directory and will install an isolated copy of github-pages in that directory.

6]
Now run `Jekyll`:

    jekyll serve --watch
7]
or:

    jekyll help
  8]  
Then, in your browser:

    http://localhost:4000
