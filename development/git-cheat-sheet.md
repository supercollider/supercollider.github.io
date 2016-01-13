---
layout: catpage
category: development
title: Cheat Sheet for Git
sort_order: 4
---

# Understanding git and GitHub#

You are here, because you wish to contribute. Welcome!

However, you may be wondering how so many people can smoothly collaborate on such a complex project such as SuperCollider (SC) and how contributions can get properly synced among the many participating contributors. Tools are needed, which allow version control and support collaboration.

This is where git comes in handy. There are [two basic approaches](https://help.github.com/articles/types-of-collaborative-development-models/) for using git. With SuperCollider we use the "Fork & pull" model. This means for you working typically with a copy of the master project files, a so-called [fork](https://help.github.com/articles/about-forks/), which may confuse or irritate you, notably when coming from svn. 

In general understanding for any tool how things work in principle means having a clear user model. It does not mean to understand every technical detail and should not require you to become a guru before being able to use a tool. A good user model allows to deduce tool behavior merely by logic and should be fully consistent throughout. Unfortunately, this is not necessarily the case with git. Therefore following may be helpful to you.

## The user model ##

Git uses its own terminology. A few key terms and concepts need to be understood always.

First there are typically three so-called repositories (*repository* or short *repo*), data storing places:

- **upstream repository** is the remote master project *repository*, reachable via URL [https://github.com/supercollider/supercollider](https://github.com/supercollider/supercollider), maintained by the community. It contains all project files. The *upstream repo* is hosted by [GitHub](http://GitHub.com).

- **origin** is also a *repository* and is your personal remote copy of the project, a so-called [fork](https://help.github.com/articles/about-forks/) at GitHub, reachable via URL https://github.com/*YOURGitHubUSERID*/supercollider. It is made once by clicking button ’fork’ at the *upstream repo* while you are logged in as GitHub user *YOURGitHubUSERID*. Note this can be done only using a browser, neither the command line tool '[git](http://gitref.org)' nor the application ‘[GitHub Desktop](https://desktop.github.com)’ can fork. Your fork has many advantages. E.g. it keeps all your contributions separate from the *upstream repo* and allows you to make freely changes without disturbing anyone. Your fork is not private, it is visible to everyone logged in to GitHub and may contain specific discussions. Note, despite being separate, the fork can be easily updated/synced to the latest development state. Again the *origin repo* is hosted by [GitHub](http://GitHub.com).

- **local** is the local git *repository* stored anywhere on your machine, a directory, e.g. ../*MYGitHubProjects*/supercollider, containing all project files plus the hidden directory ‘.git’ and other auxiliary files needed therein for git to work. This local copy must be created by cloning once the remote origin, i.e. your personal fork *origin*, not the *upstream*, to the local machine. All files here can be freely edited with tools of your choice, git will take care of the rest, i.e. detect changes by watching all files residing in your *local* repo on your machine.

In addition there are **branches** within above 3 repos. Each repo contains at least one branch, the **default branch**, called **Master**. Branches serve separate development from the main branch, e.g. to try new things out first before they are released (deployed) to others. Whether to create or not to create a branch depends on the given circumstances. Generally you make first a branch before you start editing. Only in case of a very small change, e.g. fix a typo, may be no need to create a branch and you would then make such a change directly within the master branch of the local repo. In most cases, for sure for any substantive change, e.g. an entire subproject such as a complex new feature, you should first create a branch (locally).

Then it is important that local edits need to be committed locally to become effective, then pushed to the origin, not the upstream (!), and then be announced and proposed to the community by pull requests. The core team of the project will then revise the pull requests and eventually merge the edits from your fork origin (remember it is public) into the upstream. Once that is done and you have synced your local repo (fetched and merged all latest edits) you can then update your local files to the latest development and sync back to your fork origin. As a result all three repositories should then contain identical project files.

All version control actions (except forking) can be done either by using the command line tool (CLT) 'git' (see next section) or application ‘GitHub Desktop’ (if available for your platform). In addition you need a browser to access the remote repos.

We do not recommend to follow the GitHub tutorials (!), they are misleading and are rarely helpful unless you are already very familiar with git concepts. For the CLT based 'git' command technique gain a quick overview with «[git - the simple guide - no deep shit!](http://rogerdudler.github.io/git-guide/)». Otherwise read on. For using ‘GitHub Desktop’ use this tutorial «[GitHub Desktop User Guides](https://help.github.com/desktop/guides/)». As of this writing we do not recommend to follow the help prominently offered by ‘GitHub Desktop’, i.e. the popup window, since it points only to GitHub Flow and from there on to CLT based techniques. The ‘GitHub Desktop’ tutorial is also available from the application itself, but only if you avoid using menu command "Help -> Tutorial" and use "Help -> GitHub Desktop Help" instead.

That's all folks!


# Working hints #

## Setup things ##

First, you need to setup things. There are two cases: You use a personal GitHub account or you don't.

#### Contributor with a personal GitHub account ####

For most cases it is recommended you work with the **origin repository**. To this end you need your personal GitHub account, which will give you a unique user ID, i.e. *YOURGitHubUSERID*. Once you have that sign in at [GitHub](http://GitHub.com) with your GitHub user ID, i.e. *YOURGitHubUSERID*. Then go to the *upstream repository* at GitHub, i.e. visit [https://github.com/supercollider/supercollider](https://github.com/supercollider/supercollider). There create your fork at GitHub by pressing button 'Fork' (near the top right corner). As a result the *origin repository* will be created at a new site with following URL **https://github.com/*YOURGitHubUSERID*/supercollider**.

In a 2nd step, again to be done only once, clone the *origin repository* to your local machine. This gets you the latest sources. This will also allow you to push changes back to the GitHub repository. There are three ways to accomplish that. CLT based means use 'git' and do:

    ``git clone --recursive git@github.com:supercollider/supercollider.git``

The `--recursive` flag is required to also download all the *submodules* as needed by SC.

Alternatively use application ‘GitHub Desktop’ assuming you are correctly logged in to your GitHub account with this application. Click on the + on the top left corner and select tab 'clone' and choose then the wanted repository. Having previously forked the *upstream repository* to your personal *origin repository* allows you to select "supercollider" (also assumed you have never done that before). The third technique is to use the browser. While visiting your *origin repository* click the 'clone' button (left of 'Download ZIP'). 

Whichever technique you use, you should get an exact copy of all project files on your local machine, i.e. your *local repository* properly inited, in which you can now start editing at your heart's content. There is no need to create first explicitly the *local repository* e.g. by calling ``git init`` (as suggested by some tutorials).

Subsequent working hints focus on the CLT based technique using command '[git](http://gitref.org)'.

#### Contributor without a personal GitHub account ####

If you don’t have a GitHub account, e.g. because you don’t intend to push changes (so will instead be contributing via patches or pull-requests), then use read-only access:

    ``git clone --recursive git://github.com/supercollider/supercollider.git``

The `--recursive` flag is required to also download all the *submodules* as needed by SC.

Subsequent working hints focus on the CLT based technique using command '[git](http://gitref.org)'.
 
## Update local repository ##

Considering that you have not been changing your local repository by yourself, you can update it with:

    git pull
    git submodule update

Many reported build problems are due to out-of-date submodules, so make sure to not skip the last step.

If you are going to do any development work, keep reading for more details...

### Updating and rebasing

The `git pull` command downloads *commits* from the online to the local repository. If you are doing any development work, it is best to always use it with the `--rebase` flag:

    git pull --rebase

The `--rebase` flag tells git to first put your new commits off the commit stack, and then stack them up on top of the just-downloaded commits. If the downloaded commits were stacked on top of yours, the history of your repository would not be a linear continuation of the history of the online repository anymore, which would prevent you from being able to push your commits online.

You could define a git command *alias* to help you with this - a short custom command that will substitute the longer command:

    git config alias.up pull --rebase

This will make `git up` equivalent to `git pull --rebase`.

### Updating submodules

Submodules are git repositories within other git repositories; the main SuperCollider repository uses several submodules. Submodules are not automatically updated within your local copy when you `git pull`, so now and then you need to update them manually using:

    git submodule update

How to know precisely when submodules need to be updated? Your local copy of submodules is out of sync when:
* the `git status` command shows directories that correspond to submodules as modified
* the `git diff` command will show changes related to these directories, in the form:
    `Subproject commit <commit ID>`

When you see any of these signs, it's time to update submodules. This may happen even whenever changing [branches](#branches), as different branches may use different versions of submodules.

Submodules are referenced in their hosting module by their URL. At some point the URL itself may be changed, and you will have to update it with:

    git submodule sync

In case you get a submodule stuck in a state you don't understand, it's handy to know that you can always delete the submodules and re-fetch them, for example:

    rm -rf external_libraries/nova-tt
    git submodule update

### Pulling from different sources

With git, it's also possible to pull changes from different clones of the same repository. For instance, you might have two or three computers that you use at different times. You can synchronize those clones over a local network without touching github!

The easy way:

    git pull https://johnny.com/repo.git johnnys-branchname # get his changes

check that everything is okay

    git pull --rebase # update master from github
    git push

The hard way:

    git checkout -b merge-johnnys-changes
    git pull https://johnny.com/repo.git johnnys-branchname # get his changes

check that everything is okay, then push changes back to github.

    git checkout master
    git pull --rebase # update master from github
    git rebase master  merge-johnnys-changes # put johny’s changes on top of latest changes from github
    git checkout master
    git merge merge-johnnys-changes
    git push

taken from [here](http://people.gnome.org/~federico/misc/git-cheat-sheet.txt)

## Commit + Push ##

Unlike in SVN, publishing changes is a two-step process in git:

- `Commit` the changes. The changes are now "permanent" in your local clone of the repository.
- `Push` the new commits into the public repository.

This has the advantage over SVN that you can manipulate the changes after committing but before pushing. If you made a mistake with some commits, you can `git reset` them, erasing them from your local repository. Then you can recommit before pushing.

Highly recommended: Set your global git configuration so that `git push` with no arguments will push only the current branch. Otherwise, if you forget to say `git push origin [branch]`, git will helpfully push all commits from all branches, including ones that you forgot about and didn't intend to make public. Once changes are pushed to the public repository, they can't be erased -- only reverted. Doing this will help to avoid headache-inducing mistakes.

    git config --global push.default upstream

If you're using an older version of git, substitute "tracking" for "upstream."

    git config --global push.default tracking

## Branches ##
Another really helpful way to save you from yourself is to work in a local branch that doesn't exist in the public repository. If you are new to git, you `will` make mistakes. If you make mistakes in a published branch, such as "master," and you accidentally push those mistakes, it may take some effort to clean up. But if you work in a branch that exists only on your local machine, you can do anything you want with it, and then selectively move specific commits into a public branch.

With a local-only branch, the worst case (completely messing up the branch) is that you delete the local branch and re-create it, with no impact on the origin.

The "-b" option to `git checkout` creates a new branch from an existing one.

    git checkout master -b my_master # now you have your own disconnected branch of master

... work work work, commit stuff, blah blah...

    git log # take note of the commit IDs, which are 32 digit hexadecimal strings

    git checkout master # switch back to the real master branch
    git cherry-pick [ID] # repeat for each ID
    git cherry -v # doublecheck what will actually be pushed
    git push origin master

    git checkout my_master # safe again

`git cherry-pick` is a bit inconvenient for large numbers of commits. In that case, it would be better to use a "topic branch." See below, "Using a separate branch for work on a feature."

## A common git workflow for development work on SuperCollider ##

Make sure you've done the "git clone" stuff above, then...

### Simple work on your main (master) branch ###

Hack on existing files, create new files...

Display and check uncommitted changes:

    git diff master

Stage changed and new files (mark them for inclusion in the next commit):

    git add file1 file2 file3

Check which changed files are staged and which not:

    git status

Commit the staged changes and additions:

    git commit -m "This commit does this and that..."

Repeat the above procedure for as many separate commits as you want.

Update your local repository with latest commits in the public repository:

    git pull --rebase
    git submodule update

Check what you will be pushing:

    git log origin/master..

Push it:

    git push

### Using a separate branch for work on a feature ###

Sometimes you want to work on several unrelated features during the same period of time and you want to be able to switch between your work on one or another. You can do this by using several branches within your local repository. Each branch allows you to store your work on a feature in form of commits on top of the commit history at the time the branch was created. By default, each repository contains one branch named master, but you can create new ones (and even rename any of them later, including master).

Create a new branch named "my_new_feature" containing all the commits in the current branch:

	git checkout -b my_new_feature

By the way `git checkout branch_name` switches between branches. 'git status' will tell you which branch you are currently on.

Now start coding your changes, and commit them into your feature branch with 'git add' and 'git commit' as explained in the previous section.

While you are coding your new feature you might need to update the branch with latest changes from the remote (public) repository, to keep up with other developments. The safest way to do this is to update your master branch and then rebase commits introduced by your feature branch on top of the master. Be sure to have all local changes committed before doing this:

	git checkout master
	git pull --rebase
	git rebase master my_new_feature

When you are ready to push the work on the feature to the public repository, first do the above three steps to synchronize your local repository with the public one, then check what you are going to push with 'git log origin/master..' and do the following:

    git checkout master
    git merge my_new_feature
    git push

This will merge the additional commits of your feature branch into the master and push them public. For additional details about rebase, see (4).

##Common git commands##

upstream - the github repository.

fetch and merge changes from upstream:

    git pull

commit all local changes:

    git commit -a -m “message”

commit changes in specific files:

    git add <files…>

    git commit -m “message”

get patch files for last N commits

    git format-patch -N

get patch files for all commits that are in your current branch but not in upstream:

    git format-patch origin/master

undo (delete) all current non-commited changes (Watch out !):

    git reset --hard HEAD

undo last commit, but leave the changes in the working tree

    git reset --soft HEAD^1

undo (delete) all commits since last time one was pulled from upstream (Watch out !). This should be done while in the master branch:

    git reset --hard origin/master

undo all commits since the last time one was pulled from upstream but leave the changes in the working tree. This should be done while in the master branch:

    git reset --soft origin/master

show uncommited local changes:

    git diff [file]

discard local changes instead of commiting them:

    git checkout — <file>

add interactively

    git add -i

To revert local commits, revert will create another commit that undoes the commit provided. Unlike reset the history is not erased.

    git revert <commit ID>

show changes compared to upstream:

    git diff origin/master    # only diff

    git show origin/master..  # log and diff

    git log origin/master..   # only log

show latest log in upstream:

    git log origin/master

see status of changes:

    git status
    
## Problems with submodule state update ##

When switching branches and doing a submodule update (in SC: nova-simd and nova-tt"), git sometimes messes up the submodule status without you having touched it. 

It will post something like:

    On branch master
    Changes not staged for commit:
      (use "git add <file>..." to update what will be committed)
      (use "git checkout -- <file>..." to discard changes in working directory)
      (commit or discard the untracked or modified content in submodules)
    modified:   external_libraries/nova-tt (untracked content)


This can be remedied by deleting the file and updatind the submodules again (given you haven't consciously made any changes, of course, which you'd lose!):
    
    rm -r external_libraries/nova-tt
    git submodule init
    git submodule update
    

## Testing mailing list patches ##

To try out emailed patches (created with git send-mail) copy all the content of the original mail message in a file, e.g. patch.mbox, and remove all the empty/white-spaces lines from the beginning of that file. If the patch is a series of mails copy all in order in the same file (the subject has an order tag `[PATCH 0/N]`, `[PATCH 1/N]`, ..., `[PATCH N/N]`).

Note: in gmail go to the option "show original" and copy the plain text message.

Create a branch to try the patch

    git checkout -b solve_problem_patch

Apply and merge the patch with am (apply mailbox)

    git am -3 patch.mbox

After testing it the branch can be erased (be careful any change will be lost)

    git branch -D solve_problem_patch

Note: this workflow is useful just to try a patch and discard changes for other solutions check the Resources.


## Testing pull-requests ##

Using Github pull-requests to contribute to sc is strongly encouraged. A single line addition to the git configuration in your local SuperCollider repo will allow you to treat pull-requests just like any other remote branch. To add this line, change to the source folder of your local sc-repository and edit the file:

    .git/config

The entry describing access to the Github repository will likely look like this (you might have to adjust the remote name):

    [remote "origin"]  
        url = https://github.com/supercollider/supercollider.git  
        fetch = +refs/heads/*:refs/remotes/origin/*

Add this line:

    fetch = +refs/pull/*/head:refs/remotes/origin/pr/*

To get:

    [remote "origin"]
        url = https://github.com/supercollider/supercollider.git  
        fetch = +refs/heads/*:refs/remotes/origin/*  
        fetch = +refs/pull/*/head:refs/remotes/origin/pr/*  

Assuming your `git pull` or `git fetch` pulls from the Github repo by default, your next pull will bring in all the references to pull requests from the SuperCollider Github repo (and keep updating them with each pull/fetch). From now on the pull requests behave like the other remote branches from the SC repo. In order to merge one, you just need to know it's number and preceed that with `origin/pr/` (replace `origin` with your remote-name), like so:

    git merge origin/pr/1372

Just remember that merged branches will not be updated by pulling any more. So if after a pull you notice the pull request you are testing has been modified, you need to repeat the merge to get the latest changes.


## Resources ##

- [Git Reference](http://gitref.org)
- [Git Book](http://book.git-scm.com/)
- [Pro Git Book](http://progit.org/book/)
- [Visual Git Tutorial](http://www.ralfebert.de/blog/tools/visual_git_tutorial_1/)
- [Rebasing](http://jbowes.wordpress.com/2007/01/26/git-rebase-keeping-your-branches-current/)
- [My Git Workflow](http://osteele.com/archives/2008/05/my-git-workflow)


contributed by:  Miguel Negrão, Jakob Leben, Jonatan Liljedahl, James Harkins, Andreas Fischlin
