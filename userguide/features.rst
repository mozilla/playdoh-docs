.. _features:

========
Features
========

This is a **work in progress** feature list of Playdoh.

For a list of useful libraries (bundled with playdoh or not), check out
:ref:`libraries <libs>`.


The base: Django
================

At the time of writing, Playdoh is based on `Django 1.4.5 <http://djangoproject.com>`_.

Enhancements:

* `jinja2 <http://jinja.pocoo.org/>`_ instead of Django's built-in templating
  system
* some helper utils called `jingo <https://github.com/jbalogh/jingo/>`_ to tie
  it into Django.


Scalability
===========
Playdoh's enhancements to raise django apps' scalability:

* `jingo-minify <https://github.com/jsocol/jingo-minify>`_ for bundling and
  minifying CSS and JS assets.


Security
========
*"Secure by default"* policy. Security enhancements applied:

* ``X-Frame-Options: Deny`` (part of commonware_) set on all responses unless
  opted out per response.
* `Stronger password hashing <https://github.com/fwenzel/django-sha2>`_ for
  Django's built-in auth system. Default: *sha512*. Recommendation:
  *bcrypt + HMAC*.
* ``secure=True`` and ``httponly=True`` :ref:`enabled by default <cookies>`
  on all cookies set through django's cookie facility, opt-out possible by
  cookie. (part of commonware_).
* Greatly reduced the need for the use of :ref:`|safe <safe>` in templates,
  to minimize opportunities for XSS vulnerabilities. The ``|fe()`` helper is
  part of `jingo <https://github.com/jbalogh/jingo/>`_, and django_safeforms is
  a `nugget <https://github.com/mozilla/nuggets/>`_.
* `bleach <https://github.com/jsocol/bleach/>`_ library bundled for
  secure-by-default, but heavily customizable HTML sanitization of user input.
* Used `django-session-csrf <https://github.com/mozilla/django-session-csrf>`_
  to replace Django's built-in, cookie-based CSRF method with a common,
  session-based method. This mitigates the risk of cookie forging attacks.

.. _commonware: https://github.com/jsocol/commonware


Localization
============
Advanced Localization (L10n) tool chain, focusing on localizable web apps by
default.

Tools and enhancements:

* *jinja2*'s integrated L10n extension based on `Babel <http://babel.edgewall.org/>`_.
* Enhanced string extraction tools and template tags through `tower
  <https://github.com/clouserw/tower>`_.
* `LocaleURLMiddleware <https://github.com/mozilla/playdoh/blob/base/apps/commons/middleware.py>`_,
  detecting user's preferred content locale and sticking it into the URL:
  example.com/*en-US*/stuff.


Testing
=======
Django's built-in test framework. Enhancements:

* `django-nose <https://github.com/jbalogh/django-nose>`_, a test runner that
  uses nose.

