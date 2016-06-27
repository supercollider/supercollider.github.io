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

Gratefully accepted at [github/supercollider](https://github.com/supercollider/supercollider).

Please don't put un-related commits in a single pull request.  Separate by functionality or issue.  Try not to change spacing or needlessly rearrange things if they don't have anything to do with the issue you are fixing.  Save rearrangement for a separate commit.

### Pull Request suggested workflow:
Assuming your clone of `supercollider/supercollider` repository is at `~/dev/sc`:

    # - fork `supercollider` repository on Github
    # - let your local clone know about your fork:
    (~/dev/sc) % git remote add REMOTE_NAME git@github.com:GITHUB_USER/supercollider
    # - be sure that your local clone `master` branch is up-to-date:
    (~/dev/sc) % git pull origin master
    # - create a new branch for your changes:
    (~/dev/sc) % git checkout -b SOME_GREAT_IMPROVEMENT
    # - write some code...
    # - commit and push your changes to your fork's new branch:
    (~/dev/sc) % git commit -a
    (~/dev/sc) % git push REMOTE_NAME SOME_GREAT_IMPROVEMENT
    # - go on your github fork page and submit a PR from that branch

## Coding guidelines

- [Coding guidelines](/development/code-style-cpp.html)
- [Commit message format](/development/commit-message.html)

