===============
Troubleshooting
===============

"Could not import settings"
---------------------------

Example::

    Error: Could not import settings 'code.settings_local' (Is it on
    sys.path?): No module named settings_local

This is caused by namespace problems in Python's sys path.

Make sure that your project directory is called differently than:

* any Python builtin (``code``, ``email``, ...)
* any module on your Python path (such as ``testapp``, which is used by
  django-nose)
* any app inside your ``apps`` directory (such as ``commons``, which is
  used by playdoh).

It is a good idea to give your project a concise code name that's somewhat
unique to avoid such namespace problems.
