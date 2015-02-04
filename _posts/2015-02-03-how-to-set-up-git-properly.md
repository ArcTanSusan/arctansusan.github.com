---
layout: post
title: "How to Set Up Git Properly"
description: ""
category: ""
tags: []
---
{% include JB/setup %}

Here are some useful git configs that will make the experience of using git more productive and colorful. When you're getting started with a new VM
or any new local dev environment, you'll be able to make better use of git by setting up these basic config files. This is certainly not a comprehensive guide to all the various git configs. Use this as a starting point for customizing and building out your personal config files that will make your workflow better.

Aliases
---------------
Git aliases are shortcuts to typing long git commands. It’s straight forward to set up. This is an example of a global gitconfig file. Then you can start typing shorter git commands without having to remember the full version of the git command.

![Alias global git config](/images/alias_gitconfig.png)

This is a basic alias to avoid having to type out the full command `git status`, but you can imagine how useful this will be for very long git commands with lots of flag arguments.

![Alias in action](/images/git_alias_in_action.png)

Colors
---------------
Also in your global `~/.gitconfig`, you can color code the types of files in your git directory like so:

![Colors status config](/images/color_config_status.png)

I’ve color-colored the untracked, modified, and committed files to show up when I type `git status`.

![Colors in action](/images/colors_in_action.png)

Git Auto-completion
------------------------------
Eventually you’ll run into long branch names that you wish you didn’t have to type out. You can configure your `.bashrc` file to include a git-autocompletion bash script. I like to use these instructions [here](https://github.com/bobthecow/git-flow-completion/wiki/Install-Bash-git-completion). How you configure this setting is different for each operating system, so folllow the instructions for your operating system.

Once that’s done, go into a git repository, and you should be able to do tab completion when you partially type out a full git command or alias. This works with all of Git commands, remotes, repositories, and branch names.

Git Prompt
------------------------------
You can customize your command line prompt to contain useful info such as the name of your current branch, the current directory path, or whether or not you’re in a python virtualenv, and the status of the working directory. You can edit the $PS1 variable manually in the `.bashrc` to show this information or you can add a [pre-made](https://github.com/bobthecow/git-flow-completion/wiki/Install-Bash-git-completion) bash script to your $PS1 variable. I've tried a git prompt that someone else wrote and it looks like this below:

![Gitt prompt](/images/my_git_prompt.png)
