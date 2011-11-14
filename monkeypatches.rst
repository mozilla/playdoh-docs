.. _monkeypatches:

==============
Monkey patches
==============

Unfortunately we have to rely on a set of monkey patches. These are
`loaded from funfactory
<https://github.com/mozilla/funfactory/blob/master/funfactory/monkeypatches.py>`_. 

This works because the first installed app is always
``funfactory`` and the first thing Django does after configuring itself
(i.e. ``django.conf.settings`` is a module) is to load the
``models.py`` file from every installed app. 

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
