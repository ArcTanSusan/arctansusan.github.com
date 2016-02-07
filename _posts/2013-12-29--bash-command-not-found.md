---
layout: post
title: "Command Not Found"
description: ""
category: "django"
---
{% include JB/setup %}

Do you ever get this error where you try to call a python module?

```django-admin.py startproject name_of_app
    -bash: django-admin.py Command not found```

This problem arises because django-admin.py file not being included properly in the PYTHON path in the .profile. I’m sure you’ll find other guides that talk about how to include the correct path to django-admin.py into the PYTHON path. However, I’m here to present a much hackier temporary solution.

The simplest get-it-to-work-asap solution is to find the files where the django-admin.py is located. This is where the `find` unix command comes in handy.

```sudo find / -name django-admin.py```

You will see that the output is a bunch of file paths where django-admin.py, the command not found, is located. Pick one of the file paths and then run
the following:

```/path/to/file/django-admin.py startproject name_of_app```

And now you have created a Django app. Congrats.
