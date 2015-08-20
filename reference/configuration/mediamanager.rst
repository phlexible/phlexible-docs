.. index::
    single: Configuration reference; PhlexibleMediaManagerBundle

phlexible_media_manager Configuration
=====================================

This reference document is a work in progress. It should be accurate, but
all options are not yet fully covered.

The PhlexibleMediaManagerBundle contains media related functionality
and can be configured under the ``phlexible_media_manager`` key in your application configuration.

Configuration
-------------

* `metaset_mapping`_

* `volumes`_

* `portlet`_
    * `style`_
    * `num_items`_
    
* `files`_
    * `view`_
    * `num_files`_
    
* `upload`_
    * `enable_upload_sort`_
    * `disable_flash`_
    
* `delete_policy`_

metaset_mapping
~~~~~~~~~~~~~~~

volumes
~~~~~~~

portlet
~~~~~~~

style
.....

    **type**: ``string`` **default**: ``large``

num_items
.........

    **type**: ``integer`` **default**: ``10``

files
~~~~~

view
....

    **type**: ``string`` **default**: ``tile``

num_files
.........

    **type**: ``integer`` **default**: ``10``

upload
~~~~~~

enable_upload_sort
..................

    **type**: ``boolean`` **default**: ``false``

disable_flash
.............

    **type**: ``boolean`` **default**: ``false``

delete_policy
~~~~~~~~~~~~~

    **type**: ``string`` **default**: ``hide_old``

Full default Configuration
--------------------------

.. configuration-block::

    .. code-block:: yaml

        phlexible_media_manager:
            metaset_mapping:
                # Prototype
                metaset:
                    category:       ~
                    name:           ~
            volumes:
                # Prototype
                name:
                    id:             ~
                    driver:         phlexible_media_manager.driver.doctrine
                    root_dir:       ~
                    quota:          ~
            portlet:
                style:              large
                num_items:          10
            files:
                view:               tile
                num_files:          10
            upload:
                enable_upload_sort: false
                disable_flash:      false
            delete_policy:          hide_old
