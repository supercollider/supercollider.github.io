---
layout: catpage
title: Contributing
category: contributing
sort_order: 1
---

Thank you for your interest in helping to develop SuperCollider! There are many ways you can help out:

- Answering questions from your fellow users in the [mailing list](http://new-supercollider-mailing-lists-forums-use-these.2681727.n2.nabble.com/).
- Filing bug reports and feature requests.
- Writing and maintaining documentation. Anything from typos to entire tutorials helps. Documentation contributions are done in the form of pull requests (see below). If you are using scide, there is a [useful trick](/contributing/ideconfig-contrib) to setting up your workspace for documentation edits.
- Reviewing, discussing, and testing out [proposed changes](https://github.com/supercollider/supercollider/pulls).
- Improving other auxiliary parts of SC, such as [sc3-plugins](https://github.com/supercollider/sc3-plugins), [this website](/contributing/supercollider-github-com), and the various [quarks](https://github.com/supercollider-quarks).

## Bugs and Features

Bug reports and feature requests should be filed in the [GitHub issue tracker](https://github.com/supercollider/supercollider/issues). See "[Submitting, triaging, and fixing bugs](/development/bugs.html)" for info on the full workflow for bug reports.

## New developer?

SuperCollider uses [Git](https://git-scm.com/) for source code control. Git knowledge is necessary to try out the latest developer versions and to contribute your own changes.

If you aren't familiar with Git, GitHub has [tutorials](https://guides.github.com/activities/hello-world/) for you to get started. If you encounter problems using Git, feel free to ask for help on the [sc-dev](http://new-supercollider-mailing-lists-forums-use-these.2681727.n2.nabble.com/SuperCollider-Developers-New-Use-this-f2681767.html) list.

## Pull requests

You can submit changes in the form of pull requests, gratefully accepted at [our GitHub repository](https://github.com/supercollider/supercollider).

The first step to filing a PR is to get your git environment working. First, fork supercollider/supercollider on GitHub. By convention, `origin` should point to your fork, and `upstream` to the main repository:

    git remote add origin git@github.com:YOUR_GITHUB_USERNAME/supercollider
    git remote add upstream https://github.com/supercollider/supercollider

For each pull request, you should first update your fork to match upstream (not needed, but it helps guard against conflicts):

    git checkout master # switch to master branch
    git pull upstream master # download the latest and the greatest
    git push origin master # update your fork on GitHub

To start a new branch:

    git checkout master # make sure your new branch is based off master, not something else!
    git checkout -b my-great-improvement
    # add and commit your changes
    git push origin my-great-improvement

Your changes are at the "my-great-improvement" branch on your fork of SuperCollider. Now point your browser to your SuperCollider fork and file a PR.

Here are some important guidelines for making pull requests:

- Don't put unrelated changes in the same pull request. Separate by functionality or issue.
- Try not to change whitespace or needlessly rearrange things if they don't have anything to do with the issue you are fixing. Save rearrangement for a separate commit.
- Be patient! It might take a few days for your changes to get reviewed and merged. Smaller PRs get merged faster, which is another good reason to break down your contributions into bite-sized pieces.

## Coding guidelines

- [Coding guidelines](/development/code-style-cpp.html)
- [Commit message format](/development/commit-message.html)

