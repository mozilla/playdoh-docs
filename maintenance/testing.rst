.. _maintenance-testing:

=======
Testing
=======

Testing playdoh-lib changes
---------------------------

Will tests playdoh-lib changes by pushing the updates to his github
clone, then adding that github clone to one of his projects, fetching
the changes and running the tests in his project.


Testing funfactory changes
--------------------------

funfactory has two sides:

1. **funfactory the library**

   You can add your funfactory clone as a remote to your project, get
   the changes and run your project's tests.

2. **funfactory the playdoh project builder**

   You can run the tests. funfactory uses tox and the instructions are
   in ``README.rst`` in the funfactory repository.


Depending on the changes you're making it probably makes sense to do
both of these.


Testing playdoh changes
-----------------------

To test template changes, you want to run the funfactory tests with
the ``FF_PLAYDOH_REMOTE`` and ``FF_PLAYDOH_BRANCH`` environment
settings set.

For more details, see the ``README.rst`` in the funfactory repository.

You will also probably want to create a playdoh project with your
changes and make sure they work correctly.
