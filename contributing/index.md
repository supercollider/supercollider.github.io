---
layout: catpage
title: Contributing - reporting bugs and pull requests
category: contributing
sort_order: 1
---

## Bugs and Features

For bug-reports and feature requests see: [Github issue tracker](https://github.com/supercollider/supercollider/issues)

But asking on the mailing list first is always a good idea.


## Pull requests

Gratefully accepted at [github/supercollider](https://github.com/supercollider/supercollider)

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

