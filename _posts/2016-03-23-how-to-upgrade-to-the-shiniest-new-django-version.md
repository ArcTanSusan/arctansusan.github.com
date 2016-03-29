---
layout: post
title: "How to Upgrade To The Shiniest New Django Version"
description: ""
category: ""
tags: []
---
{% include JB/setup %}

Intro
--------------

Hi, I'm Susan. I work at Cisco in San Francisco, CA. I used to work at a small cloud computing startup Piston and then they got acquired by Cisco. I know python web apis, web development, and I currently work with the openstack horizon project on the Cisco team.

In 2014, I've worked on an open source Django project called OpenHatch located at openhatch.org, it's a project that helps users find open source projects. I upgraded OpenHatch from 1.3 to 1.4 and then from 1.4 to 1.5. Much of this advice is drawn from experiences on upgrading OpenHatch.org.


Why Should I Upgrade To Newer Django Version?
-----------------------------------------------------------------------------------
New versions of the Django project are released on a time-cycle of every 8 months. Upgrading your current Django project to the next release of the Django project is a necessary and inevitable chore. You know you'll get the newest security and bug fixes, and new improved features in the new release. The longer you stay in an earlier version of Django as time marches on, the more you incur technical debt, and the more difficult and time consuming to complete future upgrades will be. It's easier to go to Django 1.7 when you're already running Django 1.6, and much harder to get there if you're running a much older version like 1.3. Running an older version of Django is technical debt that can only accumulate as new feature versions are released once every 8 months. 


Semantic Versioning
-----------------------------------
Let's review semantic versioning. The first integer is the major, the second integer is the minor, and the third integer is the patch. The major version A gets incremented when your project adds a backwards-incompatible feature, the minor version B gets incremented when your projects adds a new backwards-compatible feature, the patch version C gets incremented when your project adds sercutiy updates or feature improvements. Patch releases are 100% backwards-compatible with the previous patch release, so you should always upgrade to the latest patch release.

The full document at www.semver.org goes into full detail on best practices on naming the version of the software you work on and it's a document that  communicates those rules that people have been using for a while.

Django Doesn't Follow Semantic Versioning
-----------------------------------------------------------------------------------
The django community doesn't follow the semantics versioning. Especially for the major version number. If the semantics versioning is followed, Django 1.7 would technically be Django 2.0, because it IS backwards-incompatible with all the versions that came before it. Django develops instead opted to follow version 1.9 with 2.0. This effectively means that the major release number is simply an extension of the minor release number. A.B as the major number. Contrary to what the semantic versioning rules say, the Django project's minor numbers may be double digits. Django version 1.4.15 currently exists and is a valid release identifier.


When is the Right Time to Upgrade?
-----------------------------------------------------------------------------------
The best time to upgrade is when your project's Django version is no longer supported. In other words, it has passed the deadline for extended support. For example, Django 1.6 has been end of life for several months and no longer receives security updates as of April 1, 2015. You should always upgrade to the latest point release e.g. 1.8.4 to 1.8.5, to make sure you have the latest bug and security fixes. These point releases are backwards compatible.

You can't do an upgrade without tests of some kind to confirm that the site still works after the upgrade. Running the test suite shows you which test errors to fix. Helpful deprecation warnings from the new Django version will come up when you run unit tests. If you don’t have a test suite, then now would be a good time to start writing unit tests. Integration or functional tests will take longer to run, while unit tests will give you faster results regarding if a specific feature works as expected. You don't need 100% test coverage, but the more unit tests you have, the more confident you will feel about working through the upgrade process.

We can look at the official release schedules to know when is the right time to upgrade.


Supported Versions Chart
-----------------------------------------------------------------------------------
If your project's Django version is 1.8 or below as shown in the red, the timeline here says it's about time to upgrade that version to at least 1.8 or above. 

The release notes for the version you're upgrading to and the deprecation timeline become essential reading materials. For sites that go to production with a specific deployment method, a lot of planning may need to take place before the actual upgrade work can begin.

Feature releases or major releases will happen roughly every eight months. Each feature release contains new features and improvements to existing features. The core Django team guarantees support for two major releases of Django at a time. Certain feature releases will be designated as long-term support (LTS) releases. These releases will get security and data loss fixes applied for a guaranteed period of time, typically three years. 1.8 and 1.9 are the two latest stable releases and continue to have long-term support for another 1-2 years from now.


Future Release Plan
-----------------------------------------------------------------------------------
The official release plan for upcoming Django versions cover versions 1.9 to 3.0. After the release date for that version, the django community supports it for another 8 months. That includes security fixes, data loss bugs, crashing bugs, and regressions from older Django versions. Then after mainstream support, there's an extra 8 months of extended life support that includes security fixes and data loss bugs. You may begin the upgrade process as soon as the release candidate for the newest version is released.


Why is upgrading a Django project a difficult thing to do?
-------------------------------------------------------------------------------------------------
A lot of folks think that doing an upgrade to a newer version of Django is very difficult and tricky. Well, it is. The work involved in doing an upgrade is different for each project that it's hard to make predictions on how long or and how much effort this work will take. Having to handle a lot of unknown quantities can be intimidating. You're not sure which, if any, tests will break, or what UI features will no longer work.

I did upgrade from 1.6 to 1.7 in one afternoon on a small web project that with a dozen Python package dependencies. That web app worked fine locally, all the tests pass.

In 2014, I've worked on an open source Django project called OpenHatch located at openhatch.org, it's an open source project that helps users find open source projects. I upgraded OpenHatch from 1.3 to 1.4 and then from 1.4 to 1.5.8. The changes covered a large amount of the codebase. Each upgrade to the next minor release involved adding and deleting a lot lines of code (4,000+ lines) across a lot of code in the openhatch code base and 3rd party Django libraries. It took me about 4 weeks to go from a completely broken Django app to a functional app, including days where I was stumped on how to proceed next, and even after I resolved the test errors, I submtted the large pull request on github, I received a lot of code review feedback I got  from other contributors.


What does the end product look like?
-----------------------------------------------------------------------------------
These are pull requests I've made to the openhatch repo. I did an upgrade from 1.3 to 1.4, and then another upgrade from 1.4 to 1.5.

The openhatch codebase uses dozens of 3rd party django libraries, some of which are compatible to the target Django release version, some of which are not and may require patching or upgrades themselves. The openhatch codebase vendors all of  the dependency libraries in the directory labeled "vendor/". A full copy of that library ships with the openhatch repo. Every time a contributor adds a new package, they have to make the same changes in the "vendor/" directory. There are commits here that are "add newer version of library Z", which has is the full library with all its source code.

For these pull requests, I'm using the pull request & branch method to make changes to the repo. The downside with making these big changes that cover lots of files is that when other contributors make commits to the upstream master branch, you have to rebase to get their commits. Merge conflicts may happen.


OMG Django Upgrades
-----------------------------------------------------
This is most people's reactions to doing Django upgrades. It can be a long tedious process.


What is the Step Zero?
-----------------------------------------------------------------------------------
The upgrading step itself is very easy. Assuming you're in a virtualenv, you pip uninstall your current Django and then you install the next Django version with pip install. The next step is to make the codebase support this new version of Django, which is what 99% of the upgrading work entails.


What NOT to do
-----------------------------------------------------------------------------------

Don't skip over more than 1 release. If you try to jump several releases, you may call Django APIs which no longer exist and you’ll miss the deprecation warnings that existed only in the releases you jumped over.

Upgrading to the next minor release is more manage-able than trying to work through severa releases at once. It's easier to pinpoint the root cause of issues as they come up when you do an upgrade from 1.4 to 1.5 than going directly from 1.4 to 1.9. You'll be confused on which version the errors are comng from and you'll miss out on the deprecation warnings from the next release. 
Depreciation warnings are removed after 2 versions. In 1.5, you'll see a warning that feature X is removed in 1.7. Then in 1.6, you'll see another warning that feature X is removed in 1.7 Then, when you're using 1.7, there won't be any deprecation warnings.

 
What is Step 1?
-----------------------------------------------------------------------------------
After you do this, run the tests. 3 outcomes can happen: your entire test suite fails to start. Some of your tests fail. If your codebase is small and relies on very few Django or Python dependencies, you may be lucky to see that all the tests pass. Then, you'll have to check if the test coverage is good. If you'e that lucky developer with comprehensive automated test suite that all pass, then your work is almost all done. Most likely, you'lll find that not all tests pass.


What if all tests pass on first run?
--------------------------------------------------------
I've been trying to find an occasion to use this image.


What's next if tests fail?
-----------------------------------------------------------------------------------
The rest of the challenge is fixing the failing tests. If that happens, run one test and see what fails. 


What does success look like?
-----------------------------------------------------------------------------------
This is a checklist of things to look for to know when you're all done with a Django upgrade. Breaking a big task into smaller tasks helps to keep focused.

All tests pass, including unit tests, and functional tests. The UI also works from clicking through the site locally. The deployment script works on staging and the UI shows up and works as expected. The deployment script works on production and the UI shows up and works as expected. During any of these steps, you might get errors with log messages that will tell you what you need to fix. Then you go fix errors, and go to the next step in this checklist.

1. All tests pass with no errors or deprecation warnings
2. UI works locally 
3. Deployment works on staging
4. UI works on staging
5. Deployment works on production
6. UI works on production


What's the entire process?
-----------------------------------------------------------------------------------
When you're doing an upgrade, you'll eventually go through all these steps. If you're stuck on how to handle an error caused by the Django upgrade, this checklist is useful. 
The first step is to run the tests. If your tests don't run at all, the problem is likely an import error. Any changes that you make on the codebase should be confirmed with a test.  If the test fails, y`ou'll see depreaction warnings that will direct you to the release notes. You fix the code, and run the 

1. Run existing unit tests. Unit tests help you identify which parts are broken during the upgrade process. 
2. Read the deprecation warnings. Then read the release notes. Finally, fix the code.
3. Run existing unit tests. Confirm that fewer tests fail.
4. If there are templates and a UI, check the UI functionaltiy on the browser. Click through the site and confirm that all works.

Then rinse and repeat, testing and re-testing different parts of the whole app thoroughly until all the tests pass 100%, and the UI all works.

What are The Challenges?
-------------------------------------------
Lots of dependencies may break
-------------------------------------------------
Some third party dependencies may not work or may require upgrades, breaking your app. The test error will tell you when you need to upgade the library dependency. In the worst case, some 3rd party Django libraries may not support the version of Django you're upgrading to. Then, you'lll have to patch up that library to make it compatible. You're doing good for the rest of the community if you decide to upstream those changes to the library maintainers, too.

The OpenHatch repo has a large number of python and django dependencies, as listed. I ran into an error message about library X, and that'll tell me that I have to update that library. So I did that, and I realized that when you vendor dependencies, I have to add in hundreds of files from the dependency to the OpenHatch codebase when that library needs an upgrade. For projects that don't vendor libraries, updating the requirements.txt and doing a pip install in the virtualenv is sufficient.

Lots of release notes
----------------------------------
There are a lot of release notes to read for the version you're upgrading to. I personally would not recommend reading the entire document from start to finish. I would run the unit tests and if one fails, its error message will direct you to a specific part of the release notes to read.


Some are simple changes
----------------------------------------
This is an example of a commit I made. The relrease notes state that AdminMediaHandler needs to be removed and replaced with StaticFilesHandler. When I made this change, the test error disappeared. I saw a different test error appear. Generally, when you get a different test error, that's means you're doing something right.


Some are simple changes
----------------------------------------
Django 1.5 supports execute_from_command_line instead of the execute_manager. This is a straightforward one-time change in the manage.py. This is one of the big reasons why manage.py test or manage.py runserver would not run.


Some are simple changes
----------------------------------------
This commit shows another syntax change where all mentions of "direct_to_template()" needs to be replaced with the generic template view class in urls.py. Each of these changes are separate commits to indicate one change that fixes this type of test errors.


Lots of Repetitions
--------------------------------------
Django 1.5 requires that the url referenes in the template be in quotes. This screenshot shows one of those changes on one template. The actual commit affects hundreds of files in the openhatch codebase. I wrote a bash script to automate these string replacements.


Takeways
--------------------------------------
Doing an upgrade is a big project. Do this for one version at a time at about once every 8 months. Without unit tests to tell you to what extent the project is functional  nd set off helpful deprecation warning, doing a successful upgrade is nearly impossible. Fixing one unit test at a time with a new commit is a good strategy. The release notes will tell you how to fix the test. Going through a checklist of smaller tasks is useful. I've also taken notes of various error messages and how I resolved them; in case I get stuck on a test error, I can check my notes to see what I've tried previously.

A talk does not fully encapsulatae the experience of doing a Django upgrade. To really understand what it's like to go through an upgrade, it's not from a talk, but from real experience.

Announcement: Django Upgrade Open Space this weekend
------------------------------------------------------------------------------------------------------------------
I'm hosting an open space on Saturday morning and also Sunday morning where folks can go to a table and get help on upgrading their personal Django projects. Anyone who has a Django project they want to upgrade their own projects are invited and welcome to join. I'm looking for mentors who have ever done an upgrade before. I'll be there to help. Would anyone else be interested in attending an open space devoted to people working on upgrading their projects?

References
------------------------------------------
I've made use of these blog posts to prepare my talk. If you're interested in reading more on this topic, here's a list of relevant blog posts:
http://andrewsforge.com/article/upgrading-django-to-17/part-4-upgrade-strategies/

