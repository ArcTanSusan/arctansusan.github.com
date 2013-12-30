---
layout: post
title: "How to Install CTags Plugin In Sublime Text"
description: ""
category: ""
tags: ["sublime text","ctags"]
---
{% include JB/setup %}


If you're working on a codebase that has more than a hundred lines of code, you should find tools that help you navigate large codebases. There's the
global search function on every text editor. That can be useful for looking up text in the code.

An even better tool is to get inside the initial function declarations. So, I use Sublime Text with CTags installed. CTags will make working in a very large
codebase a lot easier. It allows you to see where function definitions are. It's an essential tool if you're using Sublime Text.

Install CTags using the Sublime’s package installer. To install CTag, type SHIFT+COMMAND+P and then “install package” in the pop-up search
bar. A pop-up menu should appear and you can type in “Ctags”. Press enter to install CTags plugin. Now you have the Sublime package CTags installed.

In your command terminal, `cd` into your current project, and now type the following to generate ctags, which are `.tags`:

```ctags -R -f .tags```

If that above command produces an error message of the following:

```ctags: illegal option — R usage: ctags [-BFadtuwvx] [-f tags file] file …```

Then, do `brew install ctags` on the terminal, and type in the following:

```alias ctags=”`brew —prefix`/bin/ctags”```

The default key bindings should now work. See https://github.com/SublimeText/CTags for more information.

For more help on installing CTags if you’re on a MacOX, see these blogs:
http://gmarik.info/blog/2010/10/08/ctags-on-OSX
http://mattpolito.info/post/1648956809/ctags-got-you-down