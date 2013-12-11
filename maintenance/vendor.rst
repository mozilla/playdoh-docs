.. _maintenance-vendor:

===============================
Maintaining libs in playdoh-lib
===============================

.. contents::
   :local:


Adding a new library via git submodules
---------------------------------------

To add a library via git submodules, you must first know the git url
to clone. Once you know that, then you do:

1. ``git submodule add <GIT-URL> src/<REPO>``
2. Add a line to ``vendor.pth``. Note that this file is sorted
   alphabetically.
3. ``git commit vendor.pth .gitmodules src/<REPO>``


Updating a library via git submodules
-------------------------------------

To update a library via git submodules:

1. ``cd src/<REPO>``
2. ``git fetch --all -p``
3. ``git checkout <REVISH>``
4. ``cd ..``
5. Do a ``git log --oneline <FROM>..<TO>`` for the library and
   copy/paste that output into the commit message so that playdoh-lib
   users can see from the playdoh-lib log what's changed.
6. ``git commit -a``


Adding a new library via pip
----------------------------

From the playdoh-lib root::

    pip install -I --install-option="--home=`pwd`" <LIB>

where ``LIB`` is any pip-happy library spec.

After you do this, make sure that any scripts that get added to
``bin/`` have a header like this::

    #!/usr/bin/env python

Then ``git add`` all the new files and commit.


Updating a library via pip
--------------------------

First, delete the library files::

    cd lib/python/
    git rm -rf <LIB>

Note the ``git`` part. This removes all the files from the git
repository.

After you do that, follow the instructions in **Adding a library via
pip** to add the update.


Dealing with binary dependencies
--------------------------------

Binary dependencies can't be checked into playdoh-lib
repository. Instead, they require a change in the funfactory
repository.

Add a line to ``funfactory/funfactory/requirements/compiled.txt``.


Dealing with source dependencies
--------------------------------

When you install/upgrade a library via git submodules, you have to
make sure the minimum required versions of dependencies are all
accounted for in either git submodules or ``lib/``.

When you install/upgrade a library via pip, it'll install the
dependencies for you into ``lib/``.
