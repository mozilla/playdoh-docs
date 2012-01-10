============
Installation
============


Requirements
------------

You need `Python`_ 2.6, `git`_, virtualenv_, and a Unix like OS.

.. _`Python`: http://python.org/
.. _`git`: http://git-scm.com/

Starting a project based on playdoh
-----------------------------------

Install the funfactory module
`from PyPI <http://pypi.python.org/pypi/funfactory>`_
or `from source <https://github.com/mozilla/funfactory>`_
with a package manager like `pip`_::

    pip install funfactory

This will install a command line script that you can use to create a new
Playdoh app. Check out ``funfactory --help`` or install an app like this::

    funfactory --python=python2.6 --pkg=yourapp

The automatic install process goes like this:

1. Clone the `Playdoh git repository`_
2. Create a custom ``yourapp`` package
3. Create a `virtualenv`_
4. Install/compile all requirements
5. Create a local settings file in ``yourapp/settings/local.py``

.. seealso::

    :doc:`Installing everything automatically in a Vagrant VM <vagrant>`

The Playdoh project layout uses a vendor library, i.e. a subdirectory ``vendor``
that contains all pure Python libraries required. In addition, a few C based
libraries (such as Jinja2, bcrypt, etc) get built by the installer. For more
information on vendor libraries, read :ref:`packages`.

.. _`Playdoh git repository`: https://github.com/mozilla/playdoh
.. _virtualenv: http://pypi.python.org/pypi/virtualenv
.. _pip: http://www.pip-installer.org/
.. _`PyPI`: http://pypi.python.org/pypi

Configuration
-------------

By default the funfactory installer configures your app to use a `MySQL`_
database named ``playdoh_app``. You'll need to create the database manually::

    mysql -u root -e 'create database playdoh_app;'

Synchronize tables and initial data::

    ./manage.py syncdb

Start the development server::

    ./manage.py runserver 0.0.0.0:8000

You can now view the dev server at http://localhost:8000/ -- hooray!

If you start adding pieces that should go back into playdoh, you will probably
want to patch `funfactory`_, which is the core of Playdoh.

.. _funfactory: https://github.com/mozilla/funfactory
.. _`MySQL`: http://www.mysql.com/


Upgrading
---------

There is a :doc:`whole section <upgrading>` on that!
