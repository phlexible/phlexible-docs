.. index::
    single: Configuration reference; PhlexibleMetaSetBundle

phlexible_meta_set Configuration
================================

This reference document is a work in progress. It should be accurate, but
all options are not yet fully covered.

The PhlexibleMetaSetBundle contains meta data related functionality
and can be configured under the ``phlexible_meta_set`` key in your application configuration.
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

This specifies the default meta set language.

available
.........

    **type**: ``string`` **default**: ``de,en``

This specifies the available meta set languages.


Full default Configuration
--------------------------

.. configuration-block::

    .. code-block:: yaml

        phlexible_meta_set:
            languages:     # Required
                default:   en
                available: en
            suggest:
                seperator: ','
