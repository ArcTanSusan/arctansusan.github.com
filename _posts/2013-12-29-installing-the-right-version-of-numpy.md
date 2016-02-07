---
layout: post
title: "Installing the Right Version of Numpy"
description: ""
category: "python numpy"
---
{% include JB/setup %}

I once had trouble installing the correct version of numpy in order to get sklearn working. I found a quick solution:
On the python terminal, do the following:

    »import numpy
    »print(numpy)

This should print the location of the current numpy installation. Delete the folder where numpy is stored. Then, do a re-install of numpy with that correct version. Then, do print(numpy) again and you should see the correct location of numpy. You can also check by typing 

    »print numpy.__version__

This prints the version of numpy in your envrionment. Once the correct version of numpy is running in your environment, then importing sklearn should produce no errors.

    » import sklearn
    »

Stack OverFlow Reference: http://stackoverflow.com/questions/12436979/how-to-fix-python-numpy-pandas-installation
