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
    **type**: ``string`` **default**: ``""``
    
Generate a unique id. Prefix is optional.

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

element
~~~~~~~

.. code-block:: jinja

    {{ element(identifier) }}

``identifier``
    **type**: ``int`` | ``TreeNode`` | ``ContentTreeContext``
    
Returns a reference to a content element.
Identifier can be a plain eid, a Tree Node, or a Tree Context.


tree_node
~~~~~~~~~

.. code-block:: jinja

    {{ tree_node(id) }}
    {{ treeNode(id) }} {# deprecated #}

``id``
    **type**: ``int``

Returns a reference to a tree node.
ID is a tid.

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

image_path
~~~~~~~~~~

.. code-block:: jinja

    {{ image_path(imageField) }}
    
``imageField``
    **type**: ``ImageField``
    
Returns a relative URL (without the schema and host) for the image provided by the given image field.

image_url
~~~~~~~~~

.. code-block:: jinja

    {{ image_url(imageField) }}
    {{ image(imageField) }} {# deprecated #}
    
``imageField``
    **type**: ``ImageField``
    
Returns ab absolute URL (with the schema and host) for the image provided by the given image field.

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

icon_url
~~~~~~~~

.. code-block:: jinja

    {{ icon_url(imageField, size) }}
    {{ icon(imageField, size) }} {# deprecated #}
    
``imageField``
    **type**: ``ImageField``
``size``
    **type**: ``int`` **default**: ``16``
    
Returns an absolute URL (with the schema and host) for the media type icon provided by the given image field.

thumbnail_path
~~~~~~~~~~~~~~

.. code-block:: jinja

    {{ thumbnail_path(imageField, template) }}
    
``imageField``
    **type**: ``ImageField``
``template``
    **type**: ``string``
    
Returns a relative URL (without the schema and host) for a thumbnail created for the given image field and template.

thumbnail_url
~~~~~~~~~~~~~

.. code-block:: jinja

    {{ thumbnail_url(imageField, template) }}
    {{ thumbnail(imageField) }} {# deprecated #}
    
``imageField``
    **type**: ``ImageField``
``template``
    **type**: ``string``
    
Returns an absolute URL (with the schema and host) for a thumbnail created for the given image field and template.

download_path
~~~~~~~~~~~~~

.. code-block:: jinja

    {{ download_path(fileField) }}
    
``fileField``
    **type**: ``FileField``
    
Returns a relative download URL (without the schema and host) for the file provided by the given file field.

download_url
~~~~~~~~~~~~

.. code-block:: jinja

    {{ download_url(fileField) }}
    {{ download(imageField) }} {# deprecated #}
    
``fileField``
    **type**: ``FileField``
    
Returns an absolute download URL (with the schema and host) for the file provided by the given file field.

fileinfo
~~~~~~~~

.. code-block:: jinja

    {{ fileinfo(fileField) }}
    
``fileField``
    **type**: ``FileField``

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

age
~~~ 

.. code-block:: jinja

    {{ date|age(diffDate) }}

``diffDate``
    **type**: ``DateTime`` **default**: ``null``
    
Create a human readable age.
If ``diffDate`` is provided, age is calculated from the given date, not the current date.

nl2p
~~~~~

.. code-block:: jinja

    {{ text|nl2p }}
    
Convert newlines to p-tags.

readable_size
~~~~~~~~~~~~~

.. code-block:: jinja

    {{ number|readable_size(decimals, binarySuffix) }}
    
``decimals``
    **type**: ``int`` **default**: ``0``
``binarySuffix``
    **type**: ``bool`` **default**: ``false``
    
Transform a file size to a human readable file size.

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

project
~~~~~~~

The ``project`` variable is available everywhere and gives access to project settings.

The available attributes are:

* ``project.title``
* ``project.url``
* ``project.version``

.. _`http://twig.sensiolabs.org/documentation`: http://twig.sensiolabs.org/documentation
