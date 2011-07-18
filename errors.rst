======
Errors
======

Mailing errors
--------------

You can send error tracebacks by email when server errors occur. Configure this
by setting::

   LOGGING = {
        'handlers': {
            'mail_admins': {
                'level': 'ERROR',
                'class': 'django.utils.log.AdminEmailHandler',
            }
        },
        'loggers': {
            'django.request': {
                'handlers': ['mail_admins'],
                'level': 'ERROR',
                'propagate': False,
            },
        },
    }

Arecibo
-------

Optionally, you can use `Arecibo`_ to record your errors. This can help stop an
email flood, gives you a URL for a traceback and statistics. To add-in
Arecibo, add the destination server to your `local_settings.py`.

If are developing a site for Mozilla, you can use an `existing`_ Arecibo
server, otherwise you'll need to set one up.

For example in `settings_local.py`::

    ARECIBO_SERVER_URL = 'http://amckay-arecibo.khan.mozilla.org'

The easiest way to report exceptions is to use the middleware, again in `settings_local.py`::

    MIDDLEWARE_CLASSES += 'django_arecibo.middleware.AreciboMiddlewareCelery',

Finally, please ensure `settings_test.py` is set to the default::

    ARECIBO_SERVER_URL = ''

Further information on `django_arecibo`_.

.. _django_arecibo: http://www.areciboapp.com/docs/client/django.html
.. _existing: http://readthedocs.org/docs/mozweb/en/latest/errors.html
.. _Arecibo: http://areciboapp.com
