.. _settings:

=======================
Settings Management API
=======================

Funfactory's default settings module provides some useful helper functions that
make managing your playdoh app's settings easier.

* ``get_apps(exclude=(), append=())``

    The ``get_apps`` function returns the current INSTALLED_APPS tuple, modified
    based on the ``exclude`` and ``append`` parameters, which can be tuples or
    lists. INSTALLED_APPS originates in funfactory's ``settings_base.py`` file,
    containing the default suite of funfactory apps, but can be modified using
    this function to add or remove apps as necessary for your project.
    
    The state of the INSTALLED_APPS tuple returned by this function persists so
    that you can modify it as necessary for your app in ``settings/base.py``
    and then further modify it for your local install in ``settings/local.py``.

    Example::

        INSTALLED_APPS = get_apps(
            exclude=('cronjobs', 'djcelery'),
            append=('debug_toolbar',)
        )

* ``get_middleware(exclude=(), append=())``

    Similar to ``get_apps``, this function returns the current
    MIDDLEWARE_CLASSES tuple and persists its state through the various
    settings files.

* ``get_template_context_processors(exclude=(), append=())``

    Again, similar to ``get_apps`` but returns the current
    TEMPLATE_CONTEXT_PROCESSORS tuple and persists its state through the various
    settings files.
