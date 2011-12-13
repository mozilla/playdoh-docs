.. _bestpractices:

==============
Best Practices
==============

This page lists several best practices for writing secure web applications
with playdoh.


.. _safe:

``|safe`` considered harmful
----------------------------

Using something like ``mystring|safe`` in a template will prevent Jinja2 from
auto-escaping it. Sadly, this requires us to be really sure that ``mystring``
is not raw, user-entered data. Otherwise we introduce an XSS vulnerability.

We have therefore eliminated the need for ``|safe`` for localized strings. This
works::

    {{ _('Hello <strong>world</strong>!') }}


String interpolation
~~~~~~~~~~~~~~~~~~~~

When you *interpolate* data into such a string, however, the resulting output
will lose its "safeness" and be escaped again. To mark the *localized part*
of an interpolated string as safe, do not use ``|f(...)|safe``. The data could
be unsafe. Instead, use the helper ``|fe(...)``. It will escape all its
arguments before doing string interpolation, then return HTML that's safe to
use::

    {{ _('Welcome back, <strong>{username}</strong>!')|fe(username=user.display_name) }}

``|f(...)|safe`` is to be considered unsafe and **should not pass code
review**.

If you interpolate into a base string that does *not contain HTML*, you may
keep on using ``|f(...)`` without ``|safe``, of course, as the auto-escaping
won't harm anything::

    {{ _('Author name: {author}')|f(author=user.display_name) }}


Form fields
~~~~~~~~~~~

Jinja2, unlike Django templates, by default does not consider Django forms
"safe" to display. Thus, you'd use something like ``{{ form.myfield|safe }}``.

In order to minimize the use of ``|safe`` (and thus possible unsafe uses of
it), playdoh monkey-patches the Django forms framework so that form fields'
HTML representations are considered safe by Jinja2 as well. Therefore, the
following works as expected::

    {{ form.myfield }}


.. _cookies:

Mmmmh, Cookies
--------------

Django's default way of setting a cookie is set_cookie_ on the HTTP response.
Unfortunately, both **secure** cookies (i.e., HTTPS-only) and **httponly**
(i.e., cookies not readable by JavaScript, if the browser supports it) are
disabled by default.

To be secure by default, we use commonware's ``cookies`` app. It makes secure
and httponly cookies the default, unless specifically requested otherwise.

To disable either of these patches, set ``COOKIES_SECURE = False`` or
``COOKIES_HTTPONLY = False`` in ``settings.py``.

You can exempt any cookie by passing ``secure=False`` or ``httponly=False`` to
the ``set_cookie`` call, respectively::

    response.set_cookie('hello', value='world', secure=False, httponly=False)

.. _set_cookie: http://docs.djangoproject.com/en/dev/ref/request-response/#django.http.HttpResponse.set_cookie


Content Security Policy (CSP) compliance
----------------------------------------

**Content Security Policy** is a web-security-related `proposal`_ put forward
by Mozilla Security. It is currently a `W3C working draft`_.

Its primary goal is to **mitigate cross-site scripting (XSS) risk** by
enforcing certain policies on a web site.

While the proposal is still subject to change there are certain best practices
that should be implemented today, because they prepare web applications for
CSP compliance and should already be considered standard practices, even if a
project does not enforce CSP yet:

.. _proposal: https://wiki.mozilla.org/Security/CSP
.. _W3C working draft: https://dvcs.w3.org/hg/content-security-policy/raw-file/tip/csp-specification.dev.html

Avoid inline CSS and JS
~~~~~~~~~~~~~~~~~~~~~~~

Avoid the use of inline CSS and JavaScript inside your HTML documents. This
includes:

Replace the following methods of writing **CSS** with a separate file:

* ``<style>`` elements
* ``style`` attributes on HTML elements

Replace the following methods of writing **JavaScript** with a separate file:

* ``<script>`` elements that wrap inline code
* ``javascript:`` URIs
* event-handling HTML attributes (like ``onclick``)

Do not create code from strings
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In JavaScript, never create **code from strings**, including calls to:

* ``eval()``
* ``new Function()`` constructor
* ``setTimeout()`` called with a non-callable argument
* ``setInterval()`` called with a non-callable argument


CSRF-protect your forms
-----------------------

Django comes with a built-in, cookie-based `CSRF protection
<https://docs.djangoproject.com/en/dev/ref/contrib/csrf/>`_ facility. Sadly,
the integrity of cookies can be compromised under certain circumstances
(through Flash, or across subdomains on the same domain), so we replaced the
CSRF method with a session-based method (as is common across web frameworks).

To CSRF-protect a form for logged-in users, just add this to your template,
inside the ``<form>`` tag::

    {{ csrf() }}

To make this work for anonymous users, with a light-weight session stored in
Django's cache, decorate a view with ``@anonymous_csrf``:

.. code-block:: python

    from session_csrf import anonymous_csrf

    @anonymous_csrf
    def login(request):
        ...

If a form is supposed to be CSRF-protected for logged-in users, but not for
anonymous users, use the ``@anonymous_csrf_exempt`` decorator:

.. code-block:: python

    from session_csrf import anonymous_csrf_exempt

    @anonymous_csrf_exempt
    def protected_in_another_way(request):
        ...

Finally, to disable CSRF protection on a form altogether (if you know what
you're doing!), Django's ``csrf_exempt`` decorator still works as expected.

To learn more about this method, refer to the
`django-session-csrf README <https://github.com/mozilla/django-session-csrf#readme>`_.


CEF (Common Event Format) logging
---------------------------------

Playdoh is set up for `Common Event Format (CEF) <http://pypi.python.org/pypi/cef>`_
logging. CEF is a unified logging format for security-relevant events and
can be used by `ArcSight <http://www.arcsight.com/solutions/solutions-cef/>`_
and similar applications.

For example, to log a user resetting their password, you would do something
like this:

.. code-block:: python

    import logging
    from funfactory.log import log_cef

    def pw_reset(request, user):
        log_cef('Password Reset', logging.INFO, request, username=user.username,
                signature='PASSWORDRESET', msg='User requested password reset')

For more information about logging and suggestions on what kinds of events to
log, refer to the `Mozilla Security Wiki <https://wiki.mozilla.org/Security/Users_and_Logs>`_.
