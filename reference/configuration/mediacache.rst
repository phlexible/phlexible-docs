.. index::
    single: Configuration reference; PhlexibleMediaCacheBundle

phlexible_media_cache Configuration
===================================

This reference document is a work in progress. It should be accurate, but
all options are not yet fully covered.

The PhlexibleMetaSetBundle contains meta data related functionality
and can be configured under the ``phlexible_media_cache`` key in your application configuration.
This includes settings related to languages and more.

Configuration
-------------

* `storages`_
	* "name"
    	* `id`_
    	* options
    		* `storage_dir`_

storages
~~~~~~~~

id
..

    **type**: ``string`` **default**: ``phlexible_media_cache.storage.local``

This specifies the container id of the storage adapter to use.

storage_dir
...........

    **type**: ``string``

This specifies the storage directory.


Full default Configuration
--------------------------

.. configuration-block::

    .. code-block:: yaml

		phlexible_media_cache:
		    immediately_cache_system_templates:  true
		    storages:                            # Required
		        # Prototype
		        name:
		            id:                          ~
		            options:                     []