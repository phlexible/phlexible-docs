.. index::
    single: phlexible Twig extensions

phlexible Twig Extensions
=========================

Twig is the default template engine for phlexible. By itself, it already contains
a lot of built-in functions, filters, tags and tests (`http://twig.sensiolabs.org/documentation`_
then scroll to the bottom).

phlexible adds more custom extension on top of Twig to integrate some components
into the Twig templates. Below is information about all the custom functions,
filters and tags.

Functions
---------

id
~~

.. code-block:: jinja

    {{ id(prefix) }}

``prefix``
    **type**: ``string``
    
Generate a unique id. Prefix is optional.

element
~~~~~~~

.. code-block:: jinja

    {{ element(identifier) }}

``identifier``
    **type**: ``int`` | ``TreeNode`` | ``ContentTreeContext``
    
Returns a reference to a content element.
Identifier can be a plain eid, a Tree Node, or a Tree Context.


path
~~~~

.. code-block:: jinja

    {{ path(name, parameters) }}

``name``
    **type**: ``LinkField`` | ``TreeNode`` | ``ContentTextContext`` | ``name``
``parameters``
    **type**: ``array`` **default**: ``[]``
    
Returns a relative URL (without the schema and host).
Name can be a Link Field, Tree Node, Tree Context, or a route name.

url
~~~

.. code-block:: jinja

    {{ url(name, parameters) }}

``name``
    **type**: ``LinkField`` | ``TreeNode`` | ``ContentTextContext`` | ``name``
``parameters``
    **type**: ``array`` **default**: ``[]``
    
Returns a absolute URL (with the schema and host).
Name can be a Link Field, Tree Node, Tree Context, or a route name.

treeNode
~~~~~~~~

.. code-block:: jinja

    {{ treeNode(id) }}

``id``
    **type**: ``int``

Returns a reference to a tree node.
ID is a tid.

imagePath
~~~~~~~~~

.. code-block:: jinja

    {{ imagePath(imageField) }}
    
``imageField``
    **type**: ``ImageField``
    
Returns a relative URL (without the schema and host) for the image provided by the given image field.

imageUrl
~~~~~~~~

.. code-block:: jinja

    {{ imageUrl(imageField) }}
    
``imageField``
    **type**: ``ImageField``
    
Returns ab absolute URL (with the schema and host) for the image provided by the given image field.

iconPath
~~~~~~~~

.. code-block:: jinja

    {{ iconPath(imageField) }}
    
``imageField``
    **type**: ``ImageField``
    
Returns a relative URL (without the schema and host) for the icon provided by the given image field.

iconUrl
~~~~~~~

.. code-block:: jinja

    {{ iconUrl(imageField) }}
    
``imageField``
    **type**: ``ImageField``
    
Returns an absolute URL (with the schema and host) for the icon provided by the given image field.

thumbnailPath
~~~~~~~~~~~~~

.. code-block:: jinja

    {{ thumbnailPath(imageField, template) }}
    
``imageField``
    **type**: ``ImageField``
``template``
    **type**: ``string``
    
Returns a relative URL (without the schema and host) for a thumbnail created for the given image field and template.

thumbnailUrl
~~~~~~~~~~~~

.. code-block:: jinja

    {{ thumbnailUrl(imageField, template) }}
    
``imageField``
    **type**: ``ImageField``
``template``
    **type**: ``string``
    
Returns an absolute URL (with the schema and host) for a thumbnail created for the given image field and template.

downloadPath
~~~~~~~~~~~~

.. code-block:: jinja

    {{ downloadPath(fileField) }}
    
``fileField``
    **type**: ``FileField``
    
Returns a relative download URL (without the schema and host) for the file provided by the given file field.

downloadUrl
~~~~~~~~~~~

.. code-block:: jinja

    {{ downloadUrl(fileField) }}
    
``fileField``
    **type**: ``FileField``
    
Returns an absolute download URL (with the schema and host) for the file provided by the given file field.

fileinfo
~~~~~~~~

.. code-block:: jinja

    {{ fileinfo(fileField) }}
    
``fileField``
    **type**: ``FileField```

Returns an array with information about the file provided by the given file field.

mediatemplate
~~~~~~~~~~~~~

.. code-block:: jinja

    {{ mediatemplate(name) }}
    
``name``
    **type**: ``string``
    
Returns an array with information about the media template identified by ``name``

Filters
-------

readable_size
~~~~~~~~~~~~~

.. code-block:: jinja

    {{ number|readable_size(decimals, binarySuffix) }}
    
``decimals``
    **type**: ``int`` **default**: ``0``
``binarySuffix``
    **type**: ``bool`` **default**: ``false``
    
Transform a file size to a human readable file size.

age
~~~ 

.. code-block:: jinja

    {{ date|age(diffDate) }}

``diffDate``
    **type**: ``Date`` **default**: ``null``
    
Create a human readable age.
If ``diffDate`` is provided, age is calculated from the given date, not the current date.

.. _`http://twig.sensiolabs.org/documentation`: http://twig.sensiolabs.org/documentation
