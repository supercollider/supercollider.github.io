# supercollider.github.io

## Local Usage

Clone this repository:

    git clone git://github.com/supercollider/supercollider.github.io.git
    cd supercollider.github.io

To view these pages locally, you must install `jekyll` using the Ruby Gem package manager.  
You will also need Ruby and Gems.

First, install the standard `bundler` gem:

    gem install bundler

and then from the supercollider.github.io directory run:

    bundle install


Now run `Jekyll`:

    bundle exec jekyll serve

And then, in your browser:

    http://127.0.0.1:4000

## Update This Website

### CSS Updates

If you wanna be sure that your CSS changes are going to be effective in the browsers you'll have to update `site_version` in `_config.yml` (css cache burst).

### Downloads

To edit the default download data **on the main page**:

- edit `_data/downloads.yml`
- edit `current_version` in `_config.yml`.

To edit data from the dedicated download page, you'll have to edit `download/index.md`.

### Code Snippets

Add a code snippet to the main page:

- edit `_data/code_snippets.yml`
- add the corresponding audio file in `assets/audio`

### Gallery

Add a project to the Gallery/Projects page:

- edit `_data/gallery.yml`
- add the corresponding image (1024x576 recommended) in `images/gallery`
