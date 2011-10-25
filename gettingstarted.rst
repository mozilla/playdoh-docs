.. highlight:: bash

Getting started
===============

.. seealso::

    :ref:`Applying Playdoh to an existing Django app <upgrading-via-funfactory>`

Requirements
------------

You need `Python`_ 2.6 and `git`_.

.. _`Python`: http://python.org/
.. _`git`: http://git-scm.com/

Starting a project based on playdoh
-----------------------------------

To check out playdoh, run::

    git clone --recursive git://github.com/mozilla/playdoh.git your_project

This project is set up to use a vendor library, i.e. a subdirectory ``vendor``
that contains all pure Python libraries required by this project. The
recursive checkout will also clone these requirements.

The default branch of playdoh is ``base``. To start a new project, you fork
playdoh and start working on your app in ``master``.

::

    cd your_project
    git checkout base
    git checkout -b master


.. seealso::

    :doc:`Installing everything automatically in a Vagrant VM <vagrant>`

In addition, there are compiled libraries (such as Jinja2) that you will need
to build yourself, either by installing them from `PyPI`_ or by using your
favorite package manager for your OS.

For development, you can run this in a `virtualenv environment`_
using `pip`_::

    pip install -r requirements/compiled.txt

For more information on vendor libraries, read :ref:`packages`.

.. _virtualenv environment: http://pypi.python.org/pypi/virtualenv
.. _pip: http://www.pip-installer.org/
.. _`PyPI`: http://pypi.python.org/pypi

Configuration
-------------

Once your app is set up, there are a few things you need to configure.
Create a custom settings file (git will ignore this file)::

    cp settings_local.py-dist settings_local.py

Set ``SECRET_KEY`` to any random, non-empty value. `The longer the better
<https://docs.djangoproject.com/en/dev/ref/settings/#secret-key>`_.

Out of the box Playdoh is configured for use with a `MySQL`_ database
named ``playdoh_app``.  You can change that name or switch out the backend,
otherwise you'll need to create the database::

    mysql -u root -e 'create database playdoh_app;'

Synchronize tables and initial data::

    ./manage.py syncdb

Start the development server::

    ./manage.py runserver 0.0.0.0:8000

You can now view the dev server at http://localhost:8000/ -- hooray!

If you start adding pieces that should go back into playdoh, you can apply the
patch to base and move it upstream. However, most of Playdoh's functionality
is in a separate module called `funfactory`_ so you may want to make changes
there and submit a pull request.

.. _funfactory: https://github.com/mozilla/funfactory
.. _`MySQL`: http://www.mysql.com/

Publishing your repo
--------------------

::

    git remote rename origin playdoh
    git remote add origin git@github.com:mozilla/foobar.git
    git push -u origin base


Upgrading
---------

There is a :doc:`whole section <upgrading>` on that!
