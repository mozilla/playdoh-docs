.. _logging:

=======
Logging
=======

Logging is a great way to track what is going on with your app.

This makes it easier for other developers to debug what's going on without
resorting to ``print`` statements or ``pdb`` calls.  It also makes it easier to
diagnose failures in production.

Playdoh supports logging out of the box.

.. note::

   This is similar to `Django Logging`_, but we make it easier to setup loggers
   and handlers.

.. _Django Logging: https://docs.djangoproject.com/en/dev/topics/logging/


How to log
----------

Logging is provided via `commonware`_.

Within our webapps we typically use a small namespace prefix for logging::

    m: mozillians
    k: kitsune
    i: input
    z: zamboni

When we log in our app we can do the following::

    import commonware.log

    log = commonware.log.getLogger('i.myapp')


    def my_view(request):
        log.info('%s got here' % request.user)
        pass

Anytime someone goes to `myapp.views.my_view` a log entry at level `INFO` will
be made.

In development this shows up as standard output.

.. _commonware: https://github.com/jsocol/commonware


Silence Logging
---------------

Sometimes logging can be noisy::

    elasticsearch: DEBUG: Search disabled for <function add_to_index at 0x102e58848>.

Commonware as configured in playdoh, allows you to configure logging via
a ``dict`` in your `settings` (preferrably `settings_local.py`)::

    error = dict(level=logging.ERROR)
    info = dict(level=logging.INFO)

    LOGGING = {
        'loggers': {
            'product_details': error,
            'nose.plugins.manager': error,
            'django.db.backends': error,
            'elasticsearch': info,
        },
    }

This configuration says:

* Only tell me if there are errors with any logs in the `product_details`,
  `nose.plugins.manager` and `django.db.backends` namespace
* Only tell me if there are `INFO`, `WARNING` or `ERROR` messages with
  ElasticSearch.
