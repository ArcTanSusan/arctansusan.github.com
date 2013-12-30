---
layout: post
title: "How to apply a patch attached to a ticket in a FOSS project."
description: ""
category: ""
tags: ["git","open source"]
---
{% include JB/setup %}

Sometimes, contributors to an open-source project are kind enough to attach patches to a ticket.
You’re working on a ticket that already contains a patch, which is a diff of the development branch against the upstream master branch.

What do you do with the tickets that already have patches attached to them? As part of the regular workflow, you create a new git branch, usually named after the ticket name, before you start working on that development branch. After you have your new local git branch, the next step is to apply the existing patch(es). Here's one workflow of how to apply a patch:

Steps to take when applying a patch:
1. Create an empty .patch file.

```
» Touch file.patch
```

2. Download the patch directly from the url link into that empty patch file you’ve created. I'm usong a django patch as an example.

```
» curl https://code.djangoproject.com/raw-attachment/ticket/99999/my_patch.diff > file.patch
```

3. cd into the directory where the patch refers to. Use git to apply the patch.

```
» git am file.patch.
```

See this guide for additional reference: http://ariejan.net/2009/10/26/how-to-create-and-apply-a-patch-with-git/

Did you get any errors when you run that above command? If not, then you have now successfully applied an existing patch.

There’s a chance that the patch may not apply 100% correctly. Sadly, that means you’ll have to manually apply those patches. This unfortunate situation
is usually true for very old patches. Then, git gets confused on which line numbers to apply the patches to. That is especially true when the upstream master
codebase has been dramatically updated or if the pach has aged considerably. As a result, there may be hunks that do not get applied cleanly into the
existing codebase.
