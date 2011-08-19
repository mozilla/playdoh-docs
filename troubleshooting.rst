===============
Troubleshooting
===============

Python namespace collisions
---------------------------

When naming your top-level project (i.e., the directory you're checking
your code out into), keep in mind that this will **become a Python module**,
so name it accordingly and don't use spaces or funny characters.

Make sure that your project directory is called **differently than**:

* any Python builtin (``code``, ``email``, ...)
* any module on your Python path (such as ``nose``, ``celery``, ``redis``)
* any app inside your ``apps`` directory.

It is a good idea to give your project a concise code name that's somewhat
unique to avoid such namespace problems.
