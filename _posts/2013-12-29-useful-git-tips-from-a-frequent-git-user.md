---
layout: post
title: "Useful Git Tips From a Frequent Git User"
description: ""
category: ""
tags: ["git","gitub","workflow","productivity"]
---
{% include JB/setup %}

If you’re working on open-source projects created anytime in the past 5 to 7 years, there is a very high chance you’ll have to learn the version control system known as Git and the code storage and review site known as Github.

I've been working with git version control very frequently at both my workplace and on open-source projects. Here are some useful things I’ve learned about git.

1. Everything on git is reversible. Every mistake can be reversed. Don’t be afraid of making mistakes. The intention of the technology behind git is to encourage branching and experimentation. Branches can easily be deleted, merged into other branches, pushed to a remote origin on Github, copied, cherry-picked.

Let’s say you make a commit and push a large number of files. Then you realize that the commit you’ve just made contains a file that should not belong there.You need to discard 1 or more files from that commit. Use `git reset —soft HEAD^` to place the most-recently committed files back into the staging area. Optional: If you want to be more specific about the commit, replace the term `HEAD^` with the hash-code of the specific commit that you want to bring into the staging area.

Do `git status` to see the changed files in the staging area. Then do `git reset HEAD file_name`, where `file_name` is the path to the file name that you want to leave out of the commit. Then, add all the new changes into the staging area by typing `git add .` and commit the new change.

What happens when you realize that you want to permanently un-do the changes that you’ve made since your last commit? Do a `git reset —hard` and you’re back in your previous commit.

There are other ways to un-do commits you’ve done a while back. Git commands such as`git reset —hard commit-hash`, `git reset —soft commit-hash`, `git reflog`, `git revert commit-hash` helps to reverse or un-do changes in the staging area and commit history. No commit is permament when you use git; every commit is reversible.

2. You can re-write history. Interactive rebasing, or the proces of squashing or editing commits, allows you to clean up the git history on your local branch. Instead of having a dozen commits and a dozen commit messages that go with them, you can rebase the last 12 commits, and squash them all into one clean commit with one descriptive commit message. I highly recommend this git process if you’re working on a large project. A single pull request that contains 1 cleaned-up commit instead of 6 separate commits to resolve a ticket will look a lot cleaner in the commit history.

3. You can make branches and do cool stuff with them. Like merging branches or making branches out of other branches. Or cherrypicking commits onto
from one branch to other branches. The git workflow encourages experimentation of different versions of code. Branches are useful for publishing. You can publish branches to Github for code-review with other people. Github keeps a record of diffs, or comparisons, between various branches, which is very useful for doing code reviews.
