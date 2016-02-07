---
layout: post
title: "How to run other people's Github pull requests locally"
description: "In an open source world far far away, a contributor makes a pull request on the upstream master repo of a project. You're
a core committer or collaborator with your own fork of the upstream repo. How do you run this new pull request locally? This is a short guide
on how to check out pull requests locally and painlessly."
category: "git"
---
{% include JB/setup %}

I was very recently made a core committer to the open source OpenHatch.org Django website. Since Spring 2013, I've been contributing
code to OpenHatch.org, mostly on the UI/UX side and in some amounts of Python. One of the responsibilites as a core committer is that
I get to review the code of other contributors and when appropriate, approve their pull requests to be merged into the upstream repository.
I have full push access to the code repository.

This article is about how to go about checking out someone else's pull request locally. This is an epecially useful skill regardless of whether
or not you have push access to the upstream repository. Reading and reviewing other people's code is a common and helpful thing to do
in software development.

Github Support wrote [this excellent guide](https://help.github.com/articles/checking-out-pull-requests-locally) on how to check out
pull requests locally. Read through this Github article carefully before proceeding with the rest of this post.

First of all, what is a pull request? In the Github world, a pull requests is a technically a branch from someone else's fork of the upstream
repository and the branch represents one or more commits that the contributor wants to merge into the upstream repository. The
Github Support guide was written for the project leaders in mind, rather than for the contributor-who-was-granted-push-access to
the upstream repo. In the article, the "origin" actually refers to the upstream master repository. So, if you have a fork
of an upstream repo, what do you need to do for your git configuration setup? Below are my step-by-step modifications:


Modifying your Git Configuration
=====================

Open your `.git/config` file in your editor and locate the section for your GitHub upstream remote. It should look something like this:

    [remote "upstream"]
        url = https://github.com/openhatch/oh-mainline.git
        fetch = +refs/heads/*:refs/remotes/upstream/*

We're going to add an extra line to this section so that it now looks like this:

    [remote "upstream"]
        url = https://github.com/openhatch/oh-mainline.git
        fetch = +refs/heads/*:refs/remotes/upstream/*
        fetch = +refs/pull/*/head:refs/pull/upstream/*

We told Git that we would like to fetch remote references of the upstream repo that match the pattern `refs/pull/*/head` and write them
as local references that match the pattern `refs/pull/origin/*`.

Now we can fetch all the pull requests from the upstream repo:

    git fetch upstream

Depending on the number of pull requests, you'll get a stream of info in your terminal about pull requests that are now rewritten locally
in the format of `refs/pull/upstream/<PR_number>`, which is what you've specified in the git config.


Checking out a particular pull request
=========================

You should now be able to check out a pull request in your local repo as follows:

    git checkout -b 999 pull/upstream/999

Now you can test this person's branch by running a local server or running a test suite to make sure all the tests pass.
