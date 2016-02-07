---
layout: post
title: "Are .pyc files useless?"
description: ""
category: "python"
tags: []
---
{% include JB/setup %}

Are *.pyc files useless?
=====================================================

Yes. If you're developing in Python, it's best to get rid of any and all `*.pyc` files in your local repository. Since `*.pyc` files aren't checked in with git version control, they stay around when you switch branches. That can caus problems with the unit tests working on the wrong files! If the .pyc file ends up being a newer timestamp, then the `.py` file from the branch you just checked out, python uses that one (from the last branch). 

There are two options for removing *.pyc files:

1. You can also add PYTHONDONTWRITEBYTECODE=1 to your shell environment in `~/.bashrc` so that no *.pyc files get created. However, your unit tests in your dev environment will run slower without the help of pre-compiled bytecode in the  `*.pyc` files.
2. Add a post-checkout git script in your git configuration that removed all the *.pyc files. This is one [example](http://yuji.wordpress.com/2010/10/29/git-remove-all-pyc/). Note that `*.pyc` should be in your local `.gitignore`. Save this shell script to the file `/path/to/repo/.git/hooks/post-checkout`, and make it executable:

    #! /bin/sh

    # Start from the repository root.
    cd ./$(git rev-parse --show-cdup)

    # Delete .pyc files and empty directories.
    find . -name "*.pyc" -delete
    find . -type d -empty -delete
