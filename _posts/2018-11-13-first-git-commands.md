---
layout: post
title: The Six Commands You NEED To Know To Work With Git
date: 2018-11-13
author: Thomas Rayner
comments: true
categories: [learning, git]
---

So let me say first, there are WAY more than 6 git commands you should know if you're working with a project that uses git. However, when you're first getting started, there are 6 git commands that you can't get away without knowing. Here they are.

This "guide" assumes that you're working with GitHub or Azure DevOps Repos or something and are creating your repos through the web-based GUI they offer, or the repos are already created. You're on your own there.

## This is not a replacement for learning git. This is just a cheat sheet for beginners.

First, you need to `clone` the repo. This takes a copy of what's in source control and puts it on your local system.

```
git clone https://github.com/thomasrayner/git-demo.git
```

If you've already cloned the repository before, and just want to retrieve new changes, you can `pull` them.

```
git pull
```

Next, you should probably be doing your work in a separate branch in order to avoid stepping on the toes of your coworkers. You need to `checkout` a new branch (`-b` to create it). You can also use `checkout` to move between branches on your local system.

```
git checkout -b new-branch

# or if you wanted to move from a branch you created back to the master branch
git checkout master
```

Now, make your changes. The demo repository I'm using to validate these commands is empty, so I'm just going to add something to a readme file using PowerShell. This is _not_ one of the commands you need to learn.

```powershell
"Just a little somethin' somethin'" | Out-File ".\readme.md"
```

You can check your `status` now (and at any point). This will even tell you which git commands you probably want next.

```
git status

# returns something like this
On branch new-branch

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        readme.md

nothing added to commit but untracked files present (use "git add" to track)
```

Next, to stage our changes, we'll use `add` like `status` suggested. Flags and parameters in git are case sensitive, and I'm using the `-A` flag to stage **A**ll my unstaged changes.

```
git add -A
```

Once my change is staged, I need to `commit` it. `-m` is the parameter for a commit message, otherwise you'll be prompted for one. These messages are critical for tracking changes to files and projects, so make them good.

```
git commit -m "Added readme.md"
```

Once the change is commited, it's time to `push` it back to GitHub (or Azure DevOps, or whatever else you're using).

```
git push
```

But wait, if you haven't pushed since creating your branch, you'll get an error! Mine looked like this.

```
fatal: The current branch new-branch has no upstream branch.
To push the current branch and set the remote as upstream, use

    git push --set-upstream origin new-branch
```

Git very helpfully shares the command that we need to use the first time we push a new branch. You don't need to do this every time, but when you perform a `git checkout -b <branch name>` then the first time you push it back to your source control, you need to include the `--set-upstream origin <branch name>` bit. After your source control knows about the branch, you can just do the normal `git push` command.

Now, you can go to GitHub or Azure DevOps and make a pull request to get the changes from your branch pulled into master.

That's it. At the very least, you need to know `clone`, `pull`, `checkout`, `status`, `commit` and `push` if you're going to work with git. Again, this is no replacement for more thorough learning and practice. There are a couple great courses on Pluralsight (click the link for my courses at the top of the page and search for "git") and other text-based resources available for you when you're ready to learn more. Until then, try not to get into too much trouble!
