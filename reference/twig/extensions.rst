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

.. _extensions_id:

id
~~

.. code-block:: jinja

    {{ id(prefix) }}

``prefix``
    **type**: ``string`` **default**: ``""``
    
Generate a unique id. Prefix is optional.

.. _extensions_path:

path
~~~~

.. code-block:: jinja

    {{ path(name, parameters, relative) }}

``name``
    **type**: ``LinkField`` | ``TreeNode`` | ``ContentTextContext`` | ``int`` | ``string``
``parameters``
    **type**: ``array`` **default**: ``[]``
``relative``
    **type**: ``boolean`` **default**: ``false``

Returns the relative URL (without the scheme and host) for the given route. If
``relative`` is enabled, it'll create a path relative to the current path.
``name`` can be a Link Field, Tree Node, Tree Context, TID, or a route name.

.. _extensions_url:

url
~~~

.. code-block:: jinja

    {{ url(name, parameters, schemeRelative) }}

``name``
    **type**: ``LinkField`` | ``TreeNode`` | ``ContentTextContext`` | ``int`` | ``string``
``parameters``
    **type**: ``array`` **default**: ``[]``
``schemeRelative``
    **type**: ``boolean`` **default**: ``false``
    
Returns the absolute URL (with scheme and host) for the given route. If
``schemeRelative`` is enabled, it'll create a scheme-relative URL.
``name`` can be a Link Field, Tree Node, Tree Context, TID, or a route name.

.. _extensions_element:

element
~~~~~~~

.. code-block:: jinja

    {{ element(identifier) }}

``identifier``
    **type**: ``int`` | ``TreeNode`` | ``ContentTreeContext``
    
Returns a reference to a content element.
Identifier can be a plain eid, a Tree Node, or a Tree Context.

.. _extensions_special_tid:

special_tid
~~~~~~~~~~~

.. code-block:: jinja

    {{ special_tid(name) }}

``name``
    **type**: ``string``

Returns the tid of a special tid from the current siteroot.
An invalid special tid will return null.

.. _extensions_tree_node:

tree_node
~~~~~~~~~

.. code-block:: jinja

    {{ tree_node(id) }}

``id``
    **type**: ``int``

Returns a reference to a tree node.
ID is a tid.

.. _extensions_node_granted:

node_granted
~~~~~~~~~~~~

.. code-block:: jinja

    {{ node_granted(node) }}

``node``
    **type**: ``TreeNode``

Returns ``true`` if user has access to the given node.

.. _extensions_page_title:

page_title
~~~~~~~~~~

.. code-block:: jinja

    {{ page_title(patternName, language, treeNode) }}

``patternName``
    **type**: ``string`` **default**: "default"
``language``
    **type**: ``string`` **default**: Locale from current request
``treeNode```
    **type**: ``TreeNode`` | ``ContentTreeContext`` **default**: Current Tree Node
    
Create a page title, with a configured pattern identifier by ``patternName``.
Will fall back to default page title, if pattern is not found.

.. _extensions_page_title_pattern:

page_title_pattern
~~~~~~~~~~~~~~~~~~

.. code-block:: jinja

    {{ page_title_pattern(pattern, language, treeNode) }}

``pattern``
    **type**: ``string``
``language``
    **type**: ``string`` **default**: Locale from current request
``treeNode```
    **type**: ``TreeNode`` | ``ContentTreeContext`` **default**: Current Tree Node
    
Create a page title, with the provided ``pattern``.

.. _extensions_image_path:

image_path
~~~~~~~~~~

.. code-block:: jinja

    {{ image_path(imageField) }}
    
``imageField``
    **type**: ``ImageField``
    
Returns a relative URL (without the schema and host) for the image provided by the given image field.

.. _extensions_image_url:

image_url
~~~~~~~~~

.. code-block:: jinja

    {{ image_url(imageField) }}
    
``imageField``
    **type**: ``ImageField``
    
Returns ab absolute URL (with the schema and host) for the image provided by the given image field.

.. _extensions_icon_path:

icon_path
~~~~~~~~~

.. code-block:: jinja

    {{ icon_path(imageField, size) }}
    
``imageField``
    **type**: ``ImageField``
``size``
    **type**: ``int`` **default**: ``16``
    
Returns a relative URL (without the schema and host) for the media type icon provided by the given image field.
Valid sizes are 16, 32, 48, 256

.. _extensions_icon_url:

icon_url
~~~~~~~~

.. code-block:: jinja

    {{ icon_url(imageField, size) }}
    
``imageField``
    **type**: ``ImageField``
``size``
    **type**: ``int`` **default**: ``16``
    
Returns an absolute URL (with the schema and host) for the media type icon provided by the given image field.

.. _extensions_thumbnail_path:

thumbnail_path
~~~~~~~~~~~~~~

.. code-block:: jinja

    {{ thumbnail_path(imageField, template) }}
    
``imageField``
    **type**: ``ImageField``
``template``
    **type**: ``string``
    
Returns a relative URL (without the schema and host) for a thumbnail created for the given image field and template.

.. _extensions_tumbnail_url:

thumbnail_url
~~~~~~~~~~~~~

.. code-block:: jinja

    {{ thumbnail_url(imageField, template) }}
    
``imageField``
    **type**: ``ImageField``
``template``
    **type**: ``string``
    
Returns an absolute URL (with the schema and host) for a thumbnail created for the given image field and template.

.. _extensions_download_path:

download_path
~~~~~~~~~~~~~

.. code-block:: jinja

    {{ download_path(fileField) }}
    
``fileField``
    **type**: ``FileField``
    
Returns a relative download URL (without the schema and host) for the file provided by the given file field.

.. _extensions_download_url:

download_url
~~~~~~~~~~~~

.. code-block:: jinja

    {{ download_url(fileField) }}
    
``fileField``
    **type**: ``FileField``
    
Returns an absolute download URL (with the schema and host) for the file provided by the given file field.

.. _extensions_fileinfo:

fileinfo
~~~~~~~~

.. code-block:: jinja

    {{ fileinfo(fileField) }}
    
``fileField``
    **type**: ``FileField``

Returns an array with information about the file provided by the given file field.

.. code-block:: jinja

    [
        'name'          => $file->getName(),  // String
        'mimetype'      => $file->getMimeType(), // String
        'mediaCategory' => $file->getMediaCategory(), // String
        'mediaType'     => $file->getMediaType(), // String
        'size'          => $file->getSize(), // String
        'attributes'    => $file->getAttributes(), // Array
        'createdAt'     => $file->getCreatedAt(), // String
        'modifiedAt'    => $file->getModifiedAt(), // String
        'meta'          => [], // Array
    ]

.. _extensions_mediatemplate:

mediatemplate
~~~~~~~~~~~~~

.. code-block:: jinja

    {{ mediatemplate(name) }}
    
``name``
    **type**: ``string``
    
Returns an array with information about the media template identified by ``name``

Filters
-------

.. _extensions_age:

age
~~~ 

.. code-block:: jinja

    {{ date|age(diffDate) }}

``diffDate``
    **type**: ``DateTime`` **default**: ``null``
    
Create a human readable age.
If ``diffDate`` is provided, age is calculated from the given date, not the current date.

.. _extensions_nl2p:

nl2p
~~~~~

.. code-block:: jinja

    {{ text|nl2p }}
    
Convert newlines to p-tags.

.. _extensions_readable_size:

readable_size
~~~~~~~~~~~~~

.. code-block:: jinja

    {{ number|readable_size(decimals, binarySuffix) }}
    
``decimals``
    **type**: ``int`` **default**: ``0``
``binarySuffix``
    **type**: ``bool`` **default**: ``false``
    
Transform a file size to a human readable file size.

.. _extensions_truncate_html:

truncate_html
~~~~~~~~~~~~~

.. code-block:: jinja

    {{ truncate_html(text, length, suffix) }}

``text``
    **type**: ``string``
``length``
    **type**: ``int``
``suffix``
    **type**: ``string`` **default**: "&hellip;"
    
Truncate text to given length, preserving html tags.


Global Variables
----------------

.. _extensions_project:

project
~~~~~~~

The ``project`` variable is available everywhere and gives access to project settings.

The available attributes are:

* ``project.title``
* ``project.url``
* ``project.version``

.. _`http://twig.sensiolabs.org/documentation`: http://twig.sensiolabs.org/documentation
