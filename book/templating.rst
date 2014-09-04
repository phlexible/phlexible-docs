.. index::
    single: Templating

Creating and Using Templates
============================

When a controller needs to generate HTML, CSS or any other content,
it hands the work off to the templating engine. phlexible uses `Twig`_
by default and so you benefit from its power.

Twig
----

Twig defines three types of special syntax:

* ``{{ ... }}``: "Says something": prints a variable or the result of an
  expression to the template;

* ``{% ... %}``: "Does something": a **tag** that controls the logic of the
  template; it is used to execute statements such as for-loops for example.

* ``{# ... #}``: "Comment something": it's the equivalent of the PHP
  ``/* comment */`` syntax. It's used to add single or multi-line comments.
  The content of the comments isn't included in the rendered pages.

Twig also contains **filters**, which modify content before being rendered.
The following makes the ``title`` variable all uppercase before rendering
it:

.. code-block:: jinja

    {{ title|upper }}

Twig comes with a list of `tags`_ and `filters`_ that are available
by default. You can `add your own extensions`_ to Twig as needed.

Create Template
---------------

// TODO

Template Inheritance
--------------------

// TODO

.. _`Twig`: http://twig.sensiolabs.org
.. _`tags`: http://twig.sensiolabs.org/doc/tags/index.html
.. _`filters`: http://twig.sensiolabs.org/doc/filters/index.html
.. _`add your own extensions`: http://twig.sensiolabs.org/doc/advanced.html#creating-an-extension
