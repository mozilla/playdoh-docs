==========================
Support for Mobile Devices
==========================

Playdoh enables you to create Django apps that run on mobile devices using the
`django-mobility`_ middleware which negotiates between user agents. In your
templates, you can check if you're in mobile like this::

  {% if request.MOBILE %}
    {{ _('This text is only visible on mobile devices.') }}
  {% endif %}

In your views module you can use the mobility decorator to toggle between
templates:

.. code-block:: python

  from mobility.decorators import mobile_template

  @mobile_template('examples/{mobile/}home.html')
  def home(request, template=None):
      # ...
      return jingo.render(request, template, data)

See the `django-mobility`_ documentation for more details about setting
up your backend.

For frontend mobile strategies like media queries and other alternatives,
check out `Approaches to Mobile Web Development`_ followed by `Part 2
(Separate Sites)`_ and `Part 3 (Responsive Design)`_.

.. _`django-mobility`: https://github.com/jbalogh/django-mobility
.. _`Approaches to Mobile Web Development`: http://blog.mozilla.com/webdev/2011/05/04/approaches-to-mobile-web-development-part-1-what-is-mobile-friendliness/
.. _`Part 2 (Separate Sites)`: http://blog.mozilla.com/webdev/2011/05/13/approaches-to-mobile-web-development-part-2-separate-sites/
.. _`Part 3 (Responsive Design)`: http://blog.mozilla.com/webdev/2011/05/27/approaches-to-mobile-web-development-part-3-responsive-design/
