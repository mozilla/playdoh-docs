===============
Troubleshooting
===============

Python namespace collisions
---------------------------

When naming your top-level project (i.e., the directory you're checking
your code out into), keep in mind that this will **become a Python module**,
so name it accordingly and don't use spaces or funny characters.

Make sure that your project directory is called **differently than**:

* any Python builtin (``code``, ``email``, ...)
* any module on your Python path (such as ``nose``, ``celery``, ``redis``)
* any app inside your ``apps`` directory.

It is a good idea to give your project a concise code name that's somewhat
unique to avoid such namespace problems.

Sessions not persisting after authentication?
---------------------------------------------

Be sure to double check your settings file(s) for anything that might not
work with localhost (but will work in production). For example, make sure
that if you require SESSION_COOKIE_SECURE to be set to True in production,
set it to False in development (localhost). Or else your sessions will 
never work properly.

CSRF issues?
------------

A common problem is that ``{{ csrf() }}`` returns an empty string in your 
templates.

By default playdoh uses ``session_csrf`` instead of Django's default CSRF 
framework. One common mistake when going from standard Django CSRF to 
``session_csrf`` is that you now need to decorate all your view functions
that expect anonymous users to use it (e.g. the login view). For example::

    from session_csrf import anonymous_csrf
    ...
    
    @anonymous_csrf
    def login(request):
        ...

Note that ``session_csrf`` is switched on by default in ``funfactory``. 
Therefore, you need to make sure your settings are set up correctly. 
These are the things you need to have in your settings:

* A working cache backend (e.g. ``CACHES`` also known as ``CACHE_BACKEND``)

* As part of a working cache backend, make sure memcached (or whatever you are
  using for caching) is running on your machine

* In ``TEMPLATE_CONTEXT_PROCESSORS`` make sure it contains 
  ``session_csrf.context_processor``

* In ``MIDDLEWARE_CLASSES`` make sure it contains ``session_csrf.CsrfMiddleware``

.. seealso::

   * https://github.com/mozilla/django-session-csrf/blob/master/session_csrf/__init__.py
   * https://github.com/django/django/blob/master/django/template/defaulttags.py#L40