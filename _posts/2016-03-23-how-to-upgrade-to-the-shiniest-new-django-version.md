---
layout: post
title: "How to Upgrade To The Shiniest New Django Version"
description: ""
category: ""
tags: []
---
{% include JB/setup %}

Have you done Django upgrades before or are looking to do so in the near future? A lot of folks think that doing an upgrade to a newer version of Django is tricky. Well, it is.


Semantic Versioning
-----------------------------------
Let's review semantic versioning for your projects. The first integer is the major, the second is theb minor, and the third is the patch. The major version gets incremented when your project adds an backwards-incampatible feature, the minor version gets incremented when your projects adds a new backwards-compatible feature, the patch version gets incremented when your projects adds sercutiy updates or feature improvements. Reading the full document at semver.org is a good start to get familiar with the best practice in how to name the version of the software you work on.
Projects that don't comply with semantic versioning will have version numbers that are essentially useless for dependency management. 

1.6 is the feature release version number. Each version will be mostly backwards compatible with the previous release. Exceptions to this rule are listed in the release notes. The patch release version number, which is incremented for bugfix and security releases. These releases will be 100% backwards-compatible with the previous patch release
 

Why Should I Upgrade To Newer Django Version?
-----------------------------------------------------------------------------------
New versions of the Django project are released on a time- cycle of every 8-9 months. Upgrading your current Django project to the next release of the Django project is a necessary chore. You know you'll get the newest security and bug fixes, latest features, and get improved re-factored code in that new release. The longer you stay in an earlier version of Django, the more you incur technical debt, and the more difficult and time consuming your future upgrades will be. Running an older version of Django is an exampe of incurring technical debt that can only accumulate as new feature versions are released once every 8 months.

Two year ago, I've worked on an open source Django project called OpenHatch located at openhatch.org. I upgraded OpenHatch from 1.3 to 1.4 and then from 1.4 to 1.5.8. Doing an upgrade from one minor release to the next minor release covered a large amount of the codebase. Each upgrade to the next minor release involved adding and deleting a lot lines of code (4,000+ lines) across a lot of code in the openhatch code base and also in its 3rd party Django libraries. The openhatch codebase uses dozens of 3rd party django libraries, some of which are compatible to the target Django release version, some of which are not and may require patching or upgrades themselves. The openhatch codebase vendors all of its dependency libraries. Every time someone does a pip install or pip install a new package, they have to make the same changes in the vendor/ directory. I'll go over how to resolve django library problems with that later.


When is the Right Time to Upgrade?
-----------------------------------------------------------------------------------
The best time to upgrade is when your project's Django version is no longer supported. Django 1.6 has been end of life for several months and no longer receives security updates. You should always upgrade to the latest point release e.g. 1.8.4 to 1.8.5, to make sure you have the latest bug and security fixes. These point releases are backwards compatible wherever possible. f your project's Django version is 1.8 or below as shown in the red, the timeline here says it's about time to upgrade that version to at least 1.8 or above. 

You can't do an upgrade without tests of some kind to test that the site still works after the upgrade. Running the test suite shows you which test errors to fix and the associated deprecation warnings from the new Django version. If you don’t have a test suite then now would be a good time to start writing unit tests. Integration or functional tests will take longer to run, while unit tests will give you faster results on if a specific feature works as expected. You don't need 100% coverage, but the more unit tests you have, the more confident you will feel about working through the upgrade.


About the Django Release Plans and Terminology
-----------------------------------------------------------------------------------
Let's go over some Django's release plan.

Feature releases or major releases will happen roughly every eight months. These releases will contain new features and improvements to existing features.

Patch releases (A.B.C, etc.) will be issued as needed, to fix bugs and/or security issues. These releases will be 100% compatible with the associated feature release, unless this is impossible for security reasons or to prevent data loss. So the answer to "should I upgrade to the latest patch release?” will always be "yes."

Certain feature releases will be designated as long-term support (LTS) releases. These releases will get security and data loss fixes applied for a guaranteed period of time, typically three years.
1.8 and 1.9 are the two latest stable releases and continue to have long-term support for another 1-2 years.

Future Release Plan
-----------------------------------------------------------------------------------
The official release plan for upcoming Django versions cover versions 1.9 to 3.0. After the release date for that version, the django community supports it for another 8 months. That includes security fixes, data loss bugs, crashing bugs, and regressions from older Django versions. Then after mainstream support, there's an extra 8 months of extended life support that includes security fixes and data loss bugs.

You may begin the upgrade process as soon as the release candidate for the newest version is released, but you should wait until the full release to deploy to your production server. You'll be able to deal with your dependencies early on and potentially even deal with deprecated features before any others.


What is the First Step?
-----------------------------------------------------------------------------------
The upgrading step itself is very easy. Assuming you're in a virtualenv, you pip uninstall your current Django and then you install the next Django version with pip install. The next step is to make the codebase support this new version of Django, which is what 99% of the upgrading work is about.

After you do this, run the tests. If your codebase is small and last very few Django or Python dependencies, you may be lucky to see that all the tests pass. If you'e that lucky developer, then your work is almost all done. If your tests fail, you're likely seeing A LOT of test failures and errors. If that happens, run one test and see what fails. 

You'lll find that not all tests  pass. The rest of the challenge is fixing the failing tests.



What NOT to do
-----------------------------------------------------------------------------------

Don't skip over more than 1 release. If you try to jump two releases, you may call Django APIs which no longer exist and you’ll miss the deprecation warnings that existed only in the releases you jumped over. Each version has a few big features and a few things which were changed and deprecated.

Upgrading to the next minor release is more manage-able than trying to work through severa releases at once. It's easier to pinpoint the root cause of issues as they come up when you do an upgrade from 1.4 to 1.5 than going directly from 1.4 to 1.9. You'll be confused on if the errors are coming from 1.5 or 1.6 or 1.7 and you'll miss out on the deprecation warnings from the next minor release.

So, for example, if we decided to start the deprecation of a function in Django 4.2:

Django 4.2 will contain a backwards-compatible replica of the function which will raise a RemovedInDjango51Warning. This warning is silent by default; you can turn on display of these warnings with the -Wd option of Python.
Django 5.0 (the version that follows 4.2) will still contain the backwards-compatible replica. This warning becomes loud by default and will likely be quite annoying.
Django 5.1 will remove the feature outright.

What did I Learn from This Experience?
-----------------------------------------------------------------------------------
I've learned a lot about good software practices from doing a Django upgrade. Below is a brief summary of the resources I used when I was doing Django ugprades. If you're doing an upgrade, you'll eventually go through all these steps. If you're stuck on how to handle an error caused by the Django upgrade, this checklist is useful. 

1. Run existing unit tests. Unit tests help you identify which parts are broken during the upgrade process. 
2. Read the deprecation warnings. Then read the release notes. Finally, fix the code.
3. Run existing unit tests. Confirm that fewer tests fail.
4. If there are templates and a UI, check the UI functionaltiy on the browser.

Then rinse and repeat starting at the unit tests again until al the tests pass 100%. 

The Challenges
-----------------------------------------------------------------------------------
You will have to retest the whole app thoroughly. Some third party dependencies may not work or may require upgrades, breaking your app.

For upgrades to Django 1.7+, you will lose all previous South migrations.

3rd party django libraries
------------------------------------------

In the worst case, some 3rd party Django libraries may not support the version of Django you're upgrading to. Then you'lll have to patch up that library to make it compatible and it's a good thing to upstream those changes to the library maintainers, too.



Some are simple changes
----------------------------------------

Release notes: "The django.core.servers.basehttp.AdminMediaHandler will be removed. In its place use django.contrib.staticfiles.handlers.StaticFilesHandler."



References
------------------------------------------
I've made use of these blog posts to prepare my talk. If you're interested in reading more on this topic, here's a list of relevant blog posts:
http://andrewsforge.com/article/upgrading-django-to-17/part-4-upgrade-strategies/

