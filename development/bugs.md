---
layout: catpage
title: "Submitting, triaging, and fixing bugs"
category: contributing
sort_order: 1
---


# SuperCollider Bug Workflow

This document provides an overview of how bugs are tracked in SuperCollider. Use this as a quick reference for what to do when creating or triaging bugs.

- **[Bug workflow](#bug-workflow)**
    - **[Submitting a bug](#submitting-a-bug)**
    - **[Triaging a bug](#triaging-a-bug)**
    - **[Fixing a bug](#fixing-a-bug)**
    - **[Merging a pull request](#merging-a-pull-request)**
    - **[Closing a bug](#closing-a-bug)**
- **[Labels](#labels)**
- **[Milestones and versions](#milestones-and-versions)**


# Bug workflow

The best thing to make sure bugs get attention, get fixed appropriately, and get moved into a release, is to provide as much information as possible. Labels, repro steps, testing implications, assignments all ensure that a bug gets sorted and acted on appropriately. A bug should generally flow through each of these stages before being closed:

**(new bug) → (triage) → (fix → pull request → merge) → (verify and close)**

+ All issues labeled "bug" can be found with this query: [is:issue is:open label:bug](https://github.com/supercollider/supercollider/issues?q=is%3Aissue+is%3Aopen+label%3Abug)
+ Untriaged bugs can be found with this query: [is:issue is:open label:bug  -label:triaged](https://github.com/supercollider/supercollider/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+label%3Abug+-label%3Atriaged)
+ Triaged bugs can be found with this query: [is:issue is:open label:bug label:triaged](https://github.com/supercollider/supercollider/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+label%3Abug+label%3Atriaged)


## Submitting a bug

New bugs can be created on the [SuperCollider issues page](https://github.com/supercollider/supercollider/issues). Here's what to do:

1. **Check for existing issues.**
The bug you're seeing may already exist. Spend a moment searching the issues database for what you're seeing. If it already exists, add a comment noting that it's affecting you also, with any additional information that seems useful. If it's a closed bug, check a newer build/version to see if you still see the problem. If it doesn't look like it's been filed yet....
2. **Create a new issue and add a ["bug"](https://github.com/supercollider/supercollider/labels/bug) label.**
If you don't mark it bug, it's not a bug. If you're seeing a crash or hang, you can flag it with ["crash"](https://github.com/supercollider/supercollider/labels/crash).
3.  **Document the steps to reproduce**. 
Writing good repro steps means writing as if you were talking to a grandparent. Be clear and explicit, write numbered steps - anyone looking at the bug should be able to follow your steps, and immediately see the same result you're seeing. If you can provide code that will reproduce the issue, do it. Paste crash reports. Make note of quarks or external tools that may be relevent. Link to external files if required.
4. **Document the result, and what you expected**.
Not everyone has the same expectations when it comes to how software works. Describe the result you got, the result you expected, and why it's problematic.
5. **Describe your environment**.
Mention the version/build of SuperCollider (check the About menu item), your operating system version, the Quarks you have installed, and anything else that might be related to the bug. More info is always better.
6. **Add additional labels (optional)**.
If you're a core dev or familiar with tracking issues in SuperCollider, add a "comp:" label, or any others as appropriate (see [labels](#labels) below). Do NOT add an OS label unless you're SURE it's a single-OS issue - in general, SuperCollider bugs are assumed to affect all OS's unless it can be proven otherwise.
7. **Submit**
8. **Watch for updates**.
Depending on your GitHub settings, you should get an email if there's any action on the bug you wrote. Bugs will be marked with the [triaged](https://github.com/supercollider/supercollider/labels/traiged) label once a core SC dev has looked at it. **When your bug is fixed, you will generally be asked to retest and close it yourself.** You have the final say as to whether the bug can be closed or not - if you get a notification to this effect, please try and retest as soon as possible!

## Triaging a bug
Triaging a bug means checking for duplicates, labeling a new bug appropriately, and assigning / moving to a milestone if appropriate. Triaged bugs should be confirmed, and are ready for a developer to start working on. Generally, core SC developers will triage bugs - however, help is welcome! We ask that you read this page carefully, and ask for approval on the  sc-dev first, before moving bugs around.

1. **Check the issue database for duplicates**. If you see one:
     1. **Make a note** in the existing bug, linking to the new one.
     2. **Close** the new bug, and label it ["duplicate"](https://github.com/supercollider/supercollider/labels/duplicate).
1. **Make sure there's enough information.** If a bug doesn't have enough information, ask the submitter for more - but *don't* mark it triaged.
2. **Reproduce the bug** if it's reasonable to do so. 
    1. **If you *can* repro**, add any additional information you gather in the process. In particular, try to narrow down the scope of the bug (i.e. turn "it crashes when I run this SynthDef" into "it crashes when I run this UGen").
    2. **If you *can't* repro**, mark the bug as "cannot reproduce" - from there, use good judgement. If it feels like a significant issue, continue triaging and have a developer look at it anyway (add a comment to this effect). If more information would be helpful, or you think it may be fixed in a newer build, go back to the submitter for info, but *don't* mark "triaged".
3. **Add labels**.
At this point, the bug should be labeled **triaged**. Mark it with a **comp** label pointing to the application area, and any other labels that are appropriate (see [labels](#labels)).
4. **Add a milestone, if appropriate**.
Milestone indicates the release that the bug should be fixed for. In general, new bugs should be added to the "future" milestone - they will be moved out of the "future" when they're actively being worked on, or as decisions get made about what goes into a particular release. 
    1. **The triager can assign a milestone if they see fit** (though this is not necessary). In particular, if it's a crash or severe bug, adding to the next milestone is appropriate.
    2. Be aware: if a release is currently in progress, things that can be added to that milestone may be locked down. Pay attention to the sc-dev list for emails related to this.

# Fixing a bug
Bug fixes should be done in a separate branch - either one in the SuperCollider repo with a "topic/" prefix, or on a fork in your own repo - and then submitted via a pull request.

1. **Branch from master** (see [pull request suggested workflow](/contributing/index.html#pull-request-suggested-workflow) and [git cheat sheet](/development/git-cheat-sheet.html)). Keep that branch free from changes unrelated to the bug. It's MUCH easier to merge small branches than it is to tease heterogeneous changes apart from each other.
2. **Assign yourself to the issue if you're working on it** - this prevents duplicate work. You can do this from the issue page on github.
4. **Write detailed commit messages** - Please review the [commit message guidelines](/development/commit-message.html). Leave *detailed* commit descriptions. It takes time to investigate and gather context on a bug, so it's worth spending a few minutes capturing that information in the commit message - for others and for yourself.
5. **If you have code you've been using to test, consider making a unit test**. You probably have sclang code you've been using to test your change already - create a new unit test with that code. New unit tests should be added to the [CommonTests](https://github.com/supercollider-quarks/CommonTests) quark for now.
6. **When fixed, create a pull request on github**. If you want the change merged immediately, set the milestone to the next upcoming version. Tag the bug that it's fixing ("#1234" with the issue number will tag) in a comment. If your pull request doesn't build, you will be emailed by travis-ci and the PR will be marked red - it's YOUR responsibility to make sure your PR builds on all platforms. If you need help with platform build issues, it's usually easy to find someone on sc-dev to triage.

Some additional notes:

- **Use travis-ci on your local repo**. This requires a travis account, and adding travis as a service in your github repo settings. From there, the travis.yml should take care of the rest. This will build and test automatically on linux and osx for every commit, and ensure you're not breaking anything as you're working.
- **Create new issues for larger work**. It's acceptable to add a spot fix to an area of the code that's a mess, but make sure to add an issue for the larger cleanup / refactoring work, even if you're not going to do it right away.

# Merging a pull request
Pull requests are generally merged by core SC developers, when it's travis-ci build is clean, all oustanding discussions have been resolved, and it's appropriate for the current milestone. The guidelines for merging a pull request are:

1. **READ THE CODE**. The most important thing is to simply look at the code changes. Even if you don't have  domain expertise, reading changes line-by-line WILL catch bugs. If you review a PR, comment to that effect - this ensures each PR has had enough eyes on it.
1. **Allow at least 1 week for comment** before merging. Be active about asking for comments.
2. Where possible, **allow commenters with concerns to do the final merge**. Call this out explicitly - i.e. `"@jesse, I fixed the issue you mentioned, please merge if acceptable"`. 
3. **Give due dilligence to platform issues**. Any change to platform-related code, or areas that might be impacted by compiler differences, should be *actively* vetted on each OS. Please ask for help on sc-dev or in the PR.
4. **Ensure changes are documented**. If the commit entails a behavior change, make sure there there's a corresponding change to an SC helpfile.
5. **Ensure changes match [style guidelines](/development/code-style-cpp.html)**. SuperCollider has not historically had firm style guidelines, so changes to a file should always match the style *in that file*, in terms of indents, variable naming, bracket usage, etc. Functional changes should *not* be mixed in with large-scale aesthetic changes (meaning: fixing badly formatted code en-masse is good, but don't do it in the same commit as a one-line bug fix).
5. **Ensure the correct milestone**. If the PR involves an API change, i.e. changes the way an existing call behaves, it should NOT be merged into a patch release (i.e. the 1 in "3.7.1") - move the PR to the next minor-version release.
6. **Don't be afraid to ask for changes to a PR**, whether the change is major or very minor. It should be assumed that *every* PR will require at least one or two revisions before merge. Be positive and helpful. Even simple changes can represent a large investment on the part of the requester - it's important to be respectful of that.

## Closing a bug
After a bugfix pull request has been merged, a bug should only be closed when it has been verified against a build produced from master.

1. **Comment on the bug, and include a link to the travis build that contains the fix**.
2. **It is best practice to allow the person who submitted the bug a chance to close it** - this is especially critical for bugs that are complex to reproduce, intermittent, or configuration-specific. This is not always possible, so use your best judgement.


# Labels
Please be judicious about creating new labels - it's always better to find an existing label that fits. Every issue should have one of these two labels: 

- **bug** for application misbehavior, or 
- **enhancement** for any request that describes new behavior or functionality.

## bug-related labels
- **triaged**: use this for bugs that have been verified, and are ready for a developer to look at and fix.
- **cannot reproduce**: use this label when you triage a bug and do not see the behavior it describes. This is generally a request for more information/investigation from the person submitting, so make sure to comment accordingly.
- **crash**: for any bug related to a crash or hang
- **severe**: for non-crashing bugs that otherwise have a severe impact
- **performance**: for any bug related to performance / audio drop-outs / launch time / etc.
- **known issue**/**wont fix**: use this when closing a bug that is **not fixed**. This is often appropriate for platform issues, Qt issues, or bugs that reflect limitations of SuperCollider itself. "known issue" labels should be documented in the README.
- **add unit test**: use for bugs that are good candidates for a unit test

## general labels
- **duplicate**: use this when *closing* an issue that is duplicated elsewhere
- **low hanging fruit**: use this for bugs or enhancements that are simple, require little context, or where you can fully describe a solution but aren't going to fix at the time. Most documentation / string change issues, for example, should qualify as LHF.
- **api change**: for enhancements that add new API's, or change existing API behavior (this *especially* includes sclang and ClassLib changes). Anything with this label should end up in the next minor-version or major-version release, and *never* a patch release. When closing an issue with this label, verify that the change has been documented.
- **comp: xxxxxx**: comp tags reflect the area of SuperCollider that this bug or enhancement affects
- **env: xxxxxx**: for bugs/enhancements that pertain to a specific work environment (i.e. the IDE)
- **os: xxxxxxx**: for bugs/enhancements that affect *only* this OS - in general, issues are assumed to affect all OS's unless this label is present.


# Milestones and versions
The current SuperCollider milestone is 3.7.0. 

SuperCollider milestones should follow the [semantic versioning standard](http://semver.org): **major.minor.patch**

**Major version** differences reflect large-scale differences, where no backwards/forwards compatibility is expected. These are exceedingly rare in SuperCollider history.

**Minor version** differences can have new functionality, but should remain backwards compatible with code from previous minor versions (i.e. code written in 3.5 should work the same in 3.6). Historically, this requirement has been VERY soft in the SuperCollider universe - however, it should be considered a best practice, and only breached in very exceptional cases.

**Patch version** differences represent bug fixes that leave the application functionally/behaviorally unchanged. New API's should not be introduced in patch versions.

**prerelease versions** will be postfixed with -alphaN or betaN, i.e. 3.7.0-alpha0, 3.7.0-beta12.






