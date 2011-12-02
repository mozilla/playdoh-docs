======
Errors
======

Mailing errors
--------------

By default ``log_settings.py`` mails out errors to anybody listed in ``settings.ADMINS``.

Arecibo
-------

Optionally, you can use `Arecibo`_ to record your errors. This can help stop an
email flood, gives you a URL for a traceback and statistics. To add-in
Arecibo, add the destination server to your `settings/local.py`.

If are developing a site for Mozilla, you can use an `existing`_ Arecibo
server, otherwise you'll need to set one up.

For example in `settings/local.py`::

    ARECIBO_SERVER_URL = 'http://amckay-arecibo.khan.mozilla.org'

Finally, please ensure `settings_test.py` is set to the default::

    ARECIBO_SERVER_URL = ''

``log_settings.py`` will use ``funfactory.log.AreciboHandler`` if Celery is setup to ping Arecibo.

.. seealso:: Further information on `django_arecibo`_.

.. _django_arecibo: http://www.areciboapp.com/docs/client/django.html
.. _existing: http://readthedocs.org/docs/mozweb/en/latest/errors.html
.. _Arecibo: http://areciboapp.com
