============
Installation
============


Requirements
------------

You need `Python`_ 2.6 or 2.7, `MySQL`_, `git`_, virtualenv_, and a Unix like
OS.

.. _`Python`: http://python.org/
.. _`git`: http://git-scm.com/

Starting a project based on playdoh
-----------------------------------

The secret to what makes playdoh fun is
the `funfactory <https://github.com/mozilla/funfactory>`_ module.
When you install funfactory
`from PyPI <http://pypi.python.org/pypi/funfactory>`_
or `from source <https://github.com/mozilla/funfactory>`_ you
get a command line script that you can use to start a new playdoh project.
Install funfactory with a package manager like `pip`_::

    pip install funfactory

You'll now have the Playdoh installer script.
Read through ``funfactory --help`` or start a new project like this::

    funfactory --python=python2.6 --pkg=yourapp

The automatic install process goes like this:

1. Clone the `Playdoh git repository`_
2. Create a custom ``yourapp`` package
3. Create a `virtualenv`_ named ``yourapp`` (if not already in a virtualenv)
4. Install/compile all requirements
5. Create a local settings file in ``yourapp/settings/local.py``
   and fill in some settings.

.. note::

   If a virtualenv needs to be created and you have
   ``virtualenvwrapper`` installed, the created virtualenv  will go in
   your ``WORKON_HOME`` directory. Otherwise the virtualenv will be
   installed in ``.virtualenv``.

.. seealso::

    :doc:`Installing everything automatically in a Vagrant VM <vagrant>`

The Playdoh project layout uses a vendor library, i.e. a subdirectory ``vendor``
that contains all pure Python libraries required. In addition, a few C based
libraries (such as MySQL-python, bcrypt, etc) get built by the installer. For more
information on vendor libraries, read :ref:`packages`.

Configuration
-------------

By default the funfactory installer configures your app to use a `MySQL`_
database named ``playdoh_app``. You'll need to create the database manually::

    mysql -u root -e 'create database playdoh_app;'

If you need to adjust any settings for the database connection,
edit ``yourproject/settings/local.py``.
Synchronize tables and initial data::

    ./manage.py syncdb

Start the development server::

    ./manage.py runserver 0.0.0.0:8000

You can now view the dev server at http://localhost:8000/ -- hooray!

If you start adding pieces that should go back into playdoh, you will probably
want to patch `funfactory`_, which is the core of Playdoh.

.. _funfactory: https://github.com/mozilla/funfactory
.. _`MySQL`: http://www.mysql.com/

Installing a project by hand
----------------------------

The installer script automates everything you'd need to do by hand but it's
simple to do it yourself. Here's what you would do:

1. Clone the `Playdoh git repository`_ into ``customproject``.
2. cd into that directory and rename ``project`` to ``customproject``
   (this is the actual Python module).
3. Edit setup.py so the module name is ``customproject``
4. Copy ``customproject/settings/local.py-dist`` to
   ``customproject/settings/local.py``.
5. Edit ``local.py``:

   - Fill in your DB credentials
   - Enter a secret key
   - Enter an HMAC key for bcrypt password hashing

6. Create a `virtualenv`_ (if not already in one)
7. Run ``pip install -r requirements/compiled.txt``

Then you should be ready to run syncdb and start up the server::

    ./manage.py syncdb
    ./manage.py runserver 0.0.0.0:8000


Upgrading
---------

There is a :doc:`whole section <upgrading>` on that!

.. _`Playdoh git repository`: https://github.com/mozilla/playdoh
.. _virtualenv: http://pypi.python.org/pypi/virtualenv
.. _pip: http://www.pip-installer.org/
.. _`PyPI`: http://pypi.python.org/pypi
