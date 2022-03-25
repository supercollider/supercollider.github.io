# supercollider.github.io

## Local Usage

Clone this repository:

```sh
git clone https://github.com/supercollider/supercollider.github.io.git
cd supercollider.github.io
```

This website is powered by `jekyll` so in order to view it locally you'll need
to have [Ruby](https://ruby-lang.org) and [Gems](https://rubygems.org) installed
on your computer.

Then, install `jekyll` and `bundler` gems:

```sh
gem install jekyll bundler
```

Install dependencies:

```sh
bundle install
```

Now you can run `jekyll` server:

```sh
bundle exec jekyll serve
```

And then, in your browser:

http://127.0.0.1:4000

## Update This Website

### CSS Updates

We use sass variables so changing colors can be done by editing `assets/css/_variables.scss`.
Otherwise, the main sass file is `assets/css/main.scss`.

If you wanna be sure that your CSS changes are going to be effective in the browsers you'll have to update `site_version` in `_config.yml` (css cache bust).

### Downloads

To update download links, you'll have to edit `_data/downloads.yml`.

Please keep in mind that **the *Download* section on the index page will display the first download
for each OS in the `current_version` category (order matters)**.

### Code Snippets

To add a code snippet to the main page:

- edit `_data/code_snippets.yml`
- add the corresponding audio file in `assets/audio`

### Gallery

To add a project to the Projects page:

- edit `_data/gallery.yml` with your project data (see examples below)
- if your project is represented by an image, add the corresponding image in `images/gallery`

#### Image

```yml
- title: YOUR TITLE
  type: image
  image: YOUR IMAGE
  link: YOUR LINK
  author: YOUR AUTHOR NAME
  text: |
    YOUR TEXT
```

#### Vimeo or YouTube video

```yml
- title: YOUR VIDEO TITLE
  type: vimeo (or youtube)
  id: YOUR VIDEO ID
  text: |
    YOUR TEXT
```
