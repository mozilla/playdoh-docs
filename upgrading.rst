.. _upgrading-playdoh:

=================
Upgrading Playdoh
=================

Upgrading your app to the latest version of playdoh means you'll share the
latest features.

Depending on the state of your app you'll want to choose one of the following
upgrade paths:

.. contents::
    :local:


.. _upgrading-via-funfactory:

Funfactorifying any Project
---------------------------

Any app, even if it's not originally a playdoh fork can be "Funfacorified".

#. Remove ``apps/commons`` if it came from playdoh.
#. Add ``funfactory`` to the vendor library.
#. Change manage.py to match playdoh's manage.py.
#. In ``settings.py`` add to the top::

    from funfactory.settings_base import *

#. In ``settings.py`` change::

        INSTALLED_APPS = (...)

   to::

        INSTALLED_APPS = list(INSTALLED_APPS) + [ ... ]

   Do the same for any other lists which have been customized.

   You can remove any entries in ``INSTALLED_APPS`` from your ``settings.py``
   if they are already in ``funfactory.settings_base.py``.

#. You can remove any redundant settings in ``settings.py`` if they appear in
   ``funfactory.settings_base.py``.


Manual upgrade
--------------

All of Playdoh's core changes are encapsulated in the funfactory_ module
which is a git submodule in the vendor directory.  Chances are that
pulling in upstream changes will be as simple as updating this module
in your vendor lib.  There is a slight chance that some additional changes
were made so you may want to examine the latest playdoh commits.

Recently forked app
-------------------

If you have a recent fork of playdoh, you can probably safely merge changes
from the base branch of playdoh and merge it into your master.

First, make sure you have a reference to the main playdoh repo:

.. code-block:: bash

  git remote add playdoh git@github.com:mozilla/playdoh.git

1. Checkout the base branch, pull and merge with your master branch:

.. code-block:: bash

  git checkout base
  git pull playdoh base
  git checkout master
  git merge base

2. Recursively update the vendor submodules to pull in any new or updated
   third party Python modules:

.. code-block:: bash

  git submodule update --init
  pushd vendor
  git submodule sync
  git submodule update --init
  popd

3. Take a look at settings_local.py-dist to see if there are new
   settings you need in your own settings_local.py
4. Run ``pip install -r requirements/compiled.txt`` in case there are new
   requirements.

.. remove this after 1 Dec 2011

Upgrading an old Playdoh fork
-----------------------------

.. note:: Thank you for being an early adopter! Muhuhahaha.

Playdoh core was factored out of the main git repo into
the funfactory_ module as part of `Issue 29`_ which was closed on
July 20, 2011.  If you still have ``apps/commons`` in your project then you
probably cloned from the playdoh repo before this change was made.
There were a lot of changes so trying to merge with base will most likely
result in conflicts.

The best way to upgrade your app is to get a fresh clone from the current
playdoh and copy over each file one by one. Then review the diff to see that
you didn't lose any customization. Be sure to also update all vendor
submodules.

Here is an `example diff`_ of an older
app that was manually upgraded to the new funfactory-based Playdoh.
There is a `second diff`_ that updates its vendor submodule to use funfactory.
This is just an example. These diffs are already out of date with some changes
that were made to manage.py and possibly some other files.

.. _example diff: https://github.com/mozilla/affiliates/commit/5c37c222b9aebca890995dc4e5e9d20ac58f67b7
.. _second diff: https://github.com/mozilla/affiliates/commit/838e0267b07ee0419ebe4cc6d5ec0c8ac9250f2e
.. _Issue 29: https://github.com/mozilla/playdoh/issues/29
.. _funfactory: https://github.com/mozilla/funfactory


