.. index::
    single: Configuration reference; PhlexibleGui

PhlexibleGuiBundle Configuration ("phlexible_gui")
==================================================

This reference document is a work in progress. It should be accurate, but
all options are not yet fully covered.

The PhlexibleGuiBundle contains most of the "base" framework functionality
and can be configured under the ``phlexible_gui`` key in your application configuration.
This includes settings related to project settings, gui languages and more.

Configuration
-------------

* `project`_
    * title
    * version
    * url
* `ext`_
    * `path`_
* `languages`_
    * `default`_
    * `available`_

project
~~~~~~~

title
.....

    **type**: ``string`` **default**: ``phlexible``

This specifies the title of your project.

version
.......

    **type**: ``string`` **default**: ``1.0.0``

This specifies the version of your project.

url
...

    **type**: ``string`` **default**: ``phlexible.net``

This specifies the url of your project.

ext
~~~

path
....

    **type**: ``string`` **default**: ``ext-2.3.0``

This specifies the path to extjs.

languages
~~~~~~~~~

default
.......

    **type**: ``string`` **default**: ``de``

This specifies the default backend language.

available
.........

    **type**: ``string`` **default**: ``de,en``

This specifies the available backend languages.


Full default Configuration
--------------------------

.. configuration-block::

    .. code-block:: yaml

        phlexible_gui:
            project:
                title:       phlexible
                version:     1.0.0-dev
                url:         phlexible.net
            ext:
                path:        ext-2.3.0
            mail:            # Required
                from_email:  ~ # Required
                from_name:   ~ # Required
            languages:       # Required
                default:     en
                available:   de
