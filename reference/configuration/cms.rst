.. index::
    single: Configuration reference; PhlexibleCms

PhlexibleCmsBundle Configuration ("phlexible_cms")
==================================================

This reference document is a work in progress. It should be accurate, but
all options are not yet fully covered.

The PhlexibleCmsBundle contains most of the "base" cms functionality
and can be configured under the ``phlexible_gui`` key in your application configuration.
This includes settings related to frontend languages and more.

Configuration
-------------

* `languages`_
    * `default`_
    * `available`_

languages
~~~~~~~~~

default
.......

    **type**: ``string`` **default**: ``de``

This specifies the default frontend language.

available
.........

    **type**: ``string`` **default**: ``de,en``

This specifies the available frontend languages.


Full default Configuration
--------------------------

.. configuration-block::

    .. code-block:: yaml

        phlexible_cms:
            languages:     # Required
                default:   en
                available: en
