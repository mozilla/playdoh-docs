.. _upgrading-playdoh:

=================
Upgrading Playdoh
=================

Upgrading your app to the latest version of playdoh means you'll share the
latest features. Depending on the state of your app you'll want to choose one of
the following upgrade paths:

.. contents::
    :local:


.. _upgrading-via-funfactory:

Funfactorifying any Project
---------------------------

Applying Playdoh to an existing Django app is a little different than
:doc:`starting an app from scratch <installation>`.  Here's how it works:

#. Add `funfactory`_ to the `vendor <packages>`:ref: library. If you don't have
   a vendor submodule, take a look at how the :doc:`installer <installation>`
   sets that up. If you like, you can simply install `funfactory from PyPI`_
   into a virtualenv.
#. Funfactory expects you to have a top level Python module named ``yourapp`` or
   whatever. This is a directory with an ``__init__.py`` file and all its
   submodules will be your various Django apps.
#. Change manage.py to match playdohs manage.py. Specifically, it needs to do
   some setup and calls ``funfactory.manage.setup_environ(...)`` for that.
#. In ``yourapp/settings/__init__.py`` add to the top::

    from funfactory.settings_base import *

#. In ``yourapp/settings/__init__.py`` change::

        INSTALLED_APPS = (...)

   to::

        INSTALLED_APPS = list(INSTALLED_APPS) + [ ... ]

   Do the same for any other lists which have been customized.
   This will ensure that you inherit the default funfactory settings.

   You can remove any entries in ``INSTALLED_APPS`` from your ``settings.py``
   if they are already in ``funfactory.settings_base.py``.

#. You can remove any redundant settings in ``settings.py`` if they appear in
   ``funfactory.settings_base``.

.. _`funfactory from PyPI`: http://pypi.python.org/pypi/funfactory

.. _manual-upgrae:


Mind those monkey patches
-------------------------

As of April 2012, every playdoh project needs to invoke the collected
monkey patches in funfactory. By doing this explicitly in each
project (as opposed to relying on ``funfactory/model.py`` to do it
automatically) we make sure monkey patches are safely executed both
when running ``runserver`` and when running as a WSGI app.

See the :ref:`Monkey patches <monkeypatches>` documentation for the
lines you need to add to your root urls.py if you don't already have
them.

Manual upgrade
--------------

All of Playdohs core is encapsulated by the funfactory_ module which is a git
submodule in the vendor directory or a python package installed in a virtualenv
if you choose. You can upgrade your app by upgrading that module.

Recently forked app
-------------------

If you have a recent fork of playdoh, you can probably safely merge changes
from the master branch of playdoh.

.. note::

   "Recently" is subjective.  Generally if you've made any commits, you're probably better off doing a
   :ref:`manual-upgrade`.

First, make sure you have a reference to the main playdoh repo:

.. code-block:: bash

  git remote add playdoh git@github.com:mozilla/playdoh.git

1. pull and merge with your master branch:

.. code-block:: bash

  git checkout master
  git pull playdoh master

2. Recursively update the vendor submodules to pull in any new or updated
   third party Python modules:

.. code-block:: bash

  git submodule update --init
  pushd vendor
  git submodule sync
  git submodule update --init
  popd

3. Take a look at ``project/settings/local.py-dist`` to see if there are new
   settings you need in your own ``yourapp/settings/local.py``
4. Run ``pip install -r requirements/compiled.txt`` in case there are new
   requirements.

.. remove this after 1 Aug 2012

Upgrading an old Playdoh fork
-----------------------------

.. note:: Thank you for being an early adopter! Muhuhahaha.

The Playdoh apps layout was majorly refactored in Jan 2012 as part of
`Pull 67`_. Instead of having a directory called ``apps`` that contains separate
Python modules there is now one top level package called ``project`` or whatever
you choose to name it. For each individual Django app therein, you'll now refer
to it as a submodule, like ``project.users``, ``project.payments``, etc. It's
also no longer possible to run your root directory as a Python module. That is,
the ``__init__.py`` file was removed.

.. _Pull 67: https://github.com/mozilla/playdoh/pull/67
.. _funfactory: https://github.com/mozilla/funfactory


