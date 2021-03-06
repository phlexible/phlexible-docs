.. index::
    single: Configuration reference; PhlexibleCmsBundle

phlexible_cms Configuration
===========================

This reference document is a work in progress. It should be accurate, but
all options are not yet fully covered.

The PhlexibleCmsBundle contains most of the "base" cms functionality
and can be configured under the ``phlexible_gui`` key in your application configuration.
This includes settings related to languages and more.

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
