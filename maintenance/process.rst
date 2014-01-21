.. _maintenance-process:

===================
Maintenance process
===================

General process for how things change:

1. write up an issue in the `Playdoh issue tracker
   <https://github.com/mozilla/playdoh/issues>`_
2. discuss the issue until a consensus for solution is arrived at
3. do the work---make sure to add tests where possible
4. create a pull request adding a ``r?`` at the end of the description
   indicating the pull request is ready for review

5. review happens

   This can take a while and go back and forth and involve multiple
   people. At some point the pull request is approved.

6. the reviewer who ``r+`` the pull request presses the Merge button
7. for playdoh-lib changes and any non-trivial changes for the other
   repos, an email should go out to dev-webdev mailing list. See
   :ref:`contact` for details on the mailing list.
8. Victory dance!
