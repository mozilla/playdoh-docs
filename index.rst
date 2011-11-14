=======
Playdoh
=======

**Mozilla's Playdoh** is a web application template based on Django_.

Django is a high-level Python Web framework that encourages rapid development
and clean, pragmatic design. Playdoh is simply a pre-configured Django app
that adds some essential modules and middleware to meet the following goals:

* Enhance the **security** of your application and its data
* Achieve optimal **performance** in the face of high traffic
* **Localize** content in multiple languages using `Mozilla's L10n standards`_
* Use the best tools and best practices to make development **fun and easy**

This is an open source project; patches are welcome! Feel free to fork and
contribute to this project on Github_.

All new `web development`_ projects at Mozilla (and maybe elsewhere?) are
created using Playdoh. However, Playdoh is not a framework itself. All of its
components can be installed and configured individually without using the
Playdoh template.

.. _Django: http://www.djangoproject.com/
.. _Github: https://github.com/mozilla/playdoh
.. _`web development`: http://blog.mozilla.com/webdev/
.. _`Mozilla's L10n standards`: https://wiki.mozilla.org/L10n:Home_Page

Let's Go!
---------

:doc:`Install <gettingstarted>` Playdoh now or :ref:`apply it
<upgrading-via-funfactory>` to an existing Django app.


Features
--------

Quick and dirty (and probably incomplete) feature list:

* Rich, but "cherry-pickable" features out of the box:

  * Django
  * jinja2 template engine
  * Simple database migrations
  * Full localization support
  * :doc:`logging`
  * ...

* Secure by default:

  * Stronger password hashing
  * X-Frame-Options: DENY by default
  * secure and httponly flags on cookies enabled by default
  * ...

:ref:`Full feature list <features>` (work in progress)...


Contents
--------

.. toctree::
   :maxdepth: 1

   gettingstarted
   features
   libs
   packages
   vagrant
   operations
   migrations
   l10n
   mobile
   logging
   errors
   template-context
   docs
   upgrading
   bestpractices
   troubleshooting
   monkeypatches


Indices and tables
------------------

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`
