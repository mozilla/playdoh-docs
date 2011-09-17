================
Template Context
================

Playdoh adds some context processors that add variables to all of your
templates. These are defined in `funfactory`_. Other third party libraries
might also add some context processors; see :ref:`each library
<libs>`'s docs for more info.

``{{ LANGUAGES }}``
  Dictionary of all available languages, such as
  ``{'en-us': 'English (US)'}``.

``{{ LANG }}``
  The currently active language code, such as ``en-us``.

``{{ DIR }}``
  ``ltr`` if the activate language read lefts to right otherwise ``rtl``
  (for example: Arabic, Hebrew, etc are right to left).

``{{ request }}``
  The request object that was passed to the view function.

``{{ settings }}``
  The settings object for the current application.


.. _funfactory: https://github.com/mozilla/funfactory
