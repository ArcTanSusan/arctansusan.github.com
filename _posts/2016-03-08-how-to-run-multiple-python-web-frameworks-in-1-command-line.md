---
layout: post
title: "How to Run Multiple Python Web Frameworks in 1 Command Line"
description: ""
category: ""
tags: []
---
{% include JB/setup %}

How do I Run Multiple Python Web Frameworks in 1 Command Line?
==============================================================================

When you want to run a flask app locally, you run `python hello_flask.py` and open the browser to localhost:5000. When you want to run a pyramid app locally, you run `python hello_pyramid.py` and open the browser to localhost:8000. When you want to run a Django app locally, you run `python manage.py runserver` and go to localhost:8080. Each app is on a different port on the localhost domain. 

If you have information on the Flask app that which the Django app needs, it's tricky to get these two web frameworks to talk to each other on different ports via Ajax requests. You'll run into a problem called cross origin resource sharing, which can be fixed on the server side only. For example, requesting https://foo.bar/target from http://foo.bar/source would not work. Requesting http://sub.foo.bar from http://foo.bar also would not work. The most common error you'll see is "Request header field Access-Control-Allow-Origin is not allowed by Access-Control-Allow-Headers." This is a security restriction that prevents requests being made from one origin to another either via different ports or domains or http procotols.

A way around this issue is to run the python-powered frameworks as a single application. This is a well-documented feature of the python WSGI module here on the [Flask application documentation](http://flask.pocoo.org/docs/0.10/patterns/appdispatch/#combining-applications). This is straight from the doc:

    from werkzeug.wsgi import DispatcherMiddleware
    from frontend_app import application as frontend
    from backend_app import application as backend

    application = DispatcherMiddleware(frontend, {
        '/backend':     backend
    })

This werkzeug module has a class called DispatcherMiddleware. More info here from this screenshot:

![DispatcherMiddleware](/images/DispatcherMiddleware.png)

The exercise is left to the reader to investigate how werkzeug's class DispatcherMiddleware is implemented underneath the hood.

Now, we can run a number of applications from using this example. Below is a `sample hello_pyramid_flask_django.py` combined app.

    from werkzeug.serving import run_simple
    from werkzeug.wsgi import DispatcherMiddleware

    import hello_pyramid
    import hello_flask
    from hello_django.mysite.myapp import wsgi as hello_django

    application = DispatcherMiddleware(hello_pyramid.app, {
        '/flask':     hello_flask.app,
        '/django':  hello_django.application
    })

    if __name__ == '__main__':
        run_simple('localhost', 4000, application,
            use_reloader=True, use_debugger=True, use_evalex=True)

You can put in any number of web frameworks in the second dictionary argument when creating the DispatcherMiddleware object. Run `python sample hello_pyramid_flask_django.py` and go to the localhost:4000 to see the application. The Flask app's url endpoints should be available on /flask, the pyramid app's url endpoints are at root `/`, and the Django app's url endpoints are at /django.

For the full source code, you can clone [this repo](https://github.com/ArcTanSusan/wsgi_lightnng_talk) that contains a basic hello world pyramid, flask, and django app.
