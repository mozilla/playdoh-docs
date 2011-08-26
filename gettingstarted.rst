Getting started
===============

.. seealso::

    :ref:`upgrading-via-funfactory`

Requirements
------------

You need Python 2.6.

To check out playdoh, run:

.. code-block:: bash

    git clone --recursive git://github.com/mozilla/playdoh.git your_project

This project is set up to use a vendor library, i.e. a subdirectory ``vendor``
that contains all pure Python libraries required by this project. The recursive
checkout will also clone these requirements.

In addition, there are compiled libraries (such as Jinja2) that you will need
to build yourself, either by installing them from ``pypi`` or by using your
favorite package manager for your OS.

For development, you can run this in a `virtualenv environment`_
using `pip`_:

.. code-block:: bash

    pip install -r requirements/compiled.txt

For more information on vendor libraries, read :ref:`packages`.

.. _virtualenv environment: http://pypi.python.org/pypi/virtualenv
.. _pip: http://www.pip-installer.org/


Starting a project based on playdoh
-----------------------------------
The default branch of playdoh is ``base``. To start a new project, you fork
playdoh and start working on your app in ``master`` (branched from base).

.. code-block:: bash

  cd your_project
  git checkout base
  git checkout -b master

If
you start adding pieces that should go back into playdoh, you can apply the
patch to base and move it upstream.
However, most of Playdoh's functionality is in a separate module called
`funfactory`_ so you may want to make changes there and submit a pull request.


Publishing your repo
--------------------

::

    git remote rename origin playdoh
    git remote add origin git@github.com:mozilla/foobar.git
    git push -u origin base

.. _funfactory: https://github.com/mozilla/funfactory

Upgrading
---------

There is a :doc:`whole section <upgrading>` on that!
