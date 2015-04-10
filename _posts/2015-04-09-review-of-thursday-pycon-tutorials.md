---
layout: post
title: "Review of Thursday PyCon Tutorials"
description: ""
category: ""
tags: []
---
{% include JB/setup %}


Impressions of Thursday's PyCon Tutorials
===================================

The two days before PyCon begins is reserved for tutorals. I didn't attend any tutorials on Wednesday,  but I went to two intermediate level tutorials on Thursday. I was very impressed with the teaching style. The tutorial speakers Asheesh and David Beazley are veteran speakers with years of experience teaching Python to newcomers and each has over a decade of Python experience since its early days in pre Python 2.5.

I went to Asheesh Laroia's tutorial on web security. Asheesh had a team of 5 or or TAs to lead a group of 4 students to work on hands-on exercises in which students worked on a pre-built instance of a demo [Django web appllication](http://rocky-thicket-5783.herokuapp.com/) intentioanlly filled with security holes. I was impressed with the thoroughnss and the clear explanations and steps in the tutorial material. A number of exercises on the app focused on how to do cross site scripting, csrf forgery to login as another user, and SQL injection. The material was a lot to cover as you can see [here](http://petwitter.com/student-handout/static/slides.html). I've finished half of the exercises by the end of the tutorial and the depth of the explanations made me want to learn more about web security topics. Everyone worked on their own pace. For those who completed the exercises early, there were many more extra exercies to do. By far this is the most hands-on tutorial I've attended at any PyCon ever. The exercises are constructed in a way to make students try out different exploits and discover expected vulnerabilities in a guided manner. One useful point for feedback is to pause the hands-on activity for a few minutes to  then review answers every so often so that everyone is on the same page. On every seat, there was a post-it note with handwritten arrows on who to pair up with for the different exercise open-ended questions. The  handwritten post-it notes were a well-thought out plan. At the end, Asheesh briefly covered some ways in Django to prevent security holes from leaking such as using csrf tokens to hiding the `SECRET_KEY` in `settings.py`. I highly recommend viewing this tutorial and going through the exercises if you're serious about web security in a web application.

Later in the aftenroon, I went to David Beazley's talk on imports and modules. He created the talk as a part of a learning experience to dive into the depths of Python's import module. This is a quite a long but effective lecture-style format that happened over the course of 3 hours with a short coffee break halfway in between. Beazley covered the in-depth internals of the `import` module from cached imports to how to make namespace packages, and different hacks one can put on top of it. I can pip install PyPI packages if the import fails, for example. In Python 3.5,  I can monitor the number of times that `import` was called in a script. The entire slide deck is over 120 [slides](http://www.dabeaz.com/modulepackage/ModulePackage.pdf) in 9 separate sections. Beazley referenced over half a dozen PEPs in his talk and demonstrated a curiousity in using imports and inspecting its internals in unconventional ways. I've learned a great deal on sys.path and what affects the sys.path (default system paths, the default python site-packages, and outside PyPI packages in a virtualenv) and how to manipulate the sys.path. Most of the material is good FYI rather than for production use. The slide deck contains an abundant and suffucient amount of code in each slide that's runnable on a Python interpreter with Pythin 3.4 installed. For the first time, I finally understand what the __init__.py is doing to stitch together many files into 1 top-level portable module. This is definitely another must-watch tutorial for people curious about the internals workings behind the ubiquitous `import` module.

A few other random cool learnings:

1. Fun hacks you can put in the __init__.py to make it more useful such as doing PyPI package updates and path hacking.

2. The usefulness of the __all__ method in making it easier for __init__.py to gather up files into a top-level object.

3. You can create zip files and then execute zip files in Python when that directory has no __init__.py.

4. You can make any Python code available on a local web server.

5. An import executes that **entire** file, the exec module is used to do that.

6. hy force reloading a module causes zombies to spawn.

7. The difference between implicit imports vs. explicit imports (explicit relative imports are preferred over any other, stylistically)

8. `python3 -m foo.py` to run any python script, makes the python version explicit.

