.. _monkeypatches:

==============
Monkey patches
==============

Unfortunately we have to rely on a set of monkey patches. These are
`loaded from funfactory
<https://github.com/mozilla/funfactory/blob/master/funfactory/monkeypatches.py>`_. 

This is still something you have to invoke from your playdoh project.
The best place to do this is from the root ``urls.py`` file. The two
lines you need are::

    from funfactory.monkeypatches import patch
    patch()
    
This should ideally happen before the ``urlpatterns`` is set up and
it's demonstrated in `the default project urls.py
<https://github.com/mozilla/playdoh/blob/master/project/urls.py#L6>`_.

.. note::

    We used to rely on ``funfactory.models`` to automatically load and
    run ``funfactory.monkeypatches.patch()`` but this is not reliable
    when running as a WSGI app.
    
Ideally all monkey patches will one day go away. Either by individual
apps getting smarter or Django getting smarter. 

The reason the monkey patches are in funfactory is because it is
assumed that all playdoh instances will need the monkey patches and
therefore it's a convenience to put this into funfactory. Most of the
monkey patches are unobtrusive meaning they are not applied unless the
relevant app is in your ``INSTALLED_APPS``.

.. note::

   Because monkey patching is evil and can cause untoward side
   effects, we log a ``debug`` message. Hopefully this will remind you
   when you get an odd traceback, to see if perhaps this monkey
   patching was to blame.
