---
layout: catpage
title: "supercollider.github.io [this site]"
category: contributing
sort_order: 2
---


The pages hosted at [https://supercollider.github.io](https://supercollider.github.io) are built using github's Jekyll system.  Page and posts are simple markdown documents and github generates these to static pages whenever changes are pushed.

The content, being simple markdown, is portable and can be moved to whatever trendy system comes along next.

This repo is at [https://github.com/supercollider/supercollider.github.io](https://github.com/supercollider/supercollider.github.io)


#### Fixing a typo or editing something small

You can edit and create files directly on github. Here's how to quickly edit a page:

**Step 0:** Create a github account if you don't have one (github.com)

**Step 1:** From the page you want to edit, click on the edit link at the very bottom, "edit this page" (scroll down to see it; it is small)

**Step 2:** Sign in with your github account (name and password)

**Step 3:** You'll see the contents of the page in an editable window. Do your editing there.

**Step 4:** Click "Preview" at the top of the editing window to see how your proposed changes will look like. If anything doesn't look right, click on "Code" again and fix the errors.

**Step 5:** When you are ready, scroll down to the bottom of the page and propose the file change (green button). You may add an optional description if you like.

For this kind of small edits, there is no need to mess with jekyll or clone the repository.

See also [Syntax and styling](syntax-and-styling.html)


#### Working with Jekyll and a checked out repo


Jekyll can render to html `_sites` but this content is not checked into git and github does not need it to be rendered.  They will render using their own Jekyll anytime you push to the repo.

- [Jekyll](http://jekyllrb.com/)
- [Github Flavored Markdown](https://help.github.com/articles/github-flavored-markdown)

Check out this repository, install gem and jekyll (plenty of help online) and start up the server to view changes in preview mode.

    jekyll --server --auto


#### Adding news posts and pages

A post is a page that has a publish date and appears in the dated archives. It also appears in the RSS/Atom feed and in the latest news on the front page.

A page is a wiki page, simple document.

A page or post must have this YAML front matter at the top:

    ---
    layout: page
    title: "Building from source"
    published: true
    category: development
    sort_order: 3
    ---

Pages go in `category-name/page-name.md` and should always have the category set in the header variables to be the same as the folder it is in.  Otherwise it doesn't show up in the page index.

Posts (announcements and news with dates) go in `_posts` and must include a date in the file name: `YYYY-MM-DD-title-goes-here.md`.

Easiest is to use the rake tasks to generate a stub for a new page.  This sets the date format for posts correctly.

Use the rake tasks from the command line:

    # list tasks
    rake -T

    # create a new post
    rake post title="a new title"

    # create a page
    rake page name="category/post-name.md"

For pages you can also just create markdown files inside folders.

    category/post-name.md

will result in

    http://supercollider.github.io/category/post-name/

Be sure to set some YAML front matter (the variables) at the top of your page if its a markdown file.  See https://github.com/mojombo/jekyll/wiki/YAML-Front-Matter

Linking to other pages.  github only ?   category / post-name

#### Gotcha

Jekyll seems to kill iframes reducing them to a single `<iframe />` so put a word in the tag: `<iframe ...>invisible words</iframe>` to fool it.

Internal links are relative to the current document and should use the .html form, eg.:

    See [Syntax styling and markdown](syntax-and-styling.html)


#### Publishing

Simply push to this [repo](https://github.com/supercollider/supercollider.github.io) and github will regenerate the site.


