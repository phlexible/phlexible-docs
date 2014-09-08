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

Miscellaneous
~~~~~~~~~~~~~

+-----------------+-------------------------------------------+
| Function Syntax | Usage                                     |
+=================+===========================================+
| ``id(prefix)``  | Generate a unique id. Prefix is optional. |
+-----------------+-------------------------------------------+

Tree
~~~~

+----------------------+--------------------------------+
| Function Syntax      | Usage                          |
+======================+================================+
| ``url(linkField)``   | Generate href for link field.  |
+----------------------+--------------------------------+
| ``url(treeNode)``    | Generate href for treeNode.    |
+----------------------+--------------------------------+
| ``url(treeContext)`` | Generate href for treeContext. |
+----------------------+--------------------------------+
| ``node(treeNode)``   | Get new treeContext.           |
+----------------------+--------------------------------+

Media
~~~~~

+---------------------------------------+----------------------------------+
| Function Syntax                       | Usage                            |
+=======================================+==================================+
| ``image(imageField)``                 | Render path to given image.      |
+---------------------------------------+----------------------------------+
| ``icon(imageField)``                  | Render path to given image icon. |
+---------------------------------------+----------------------------------+
| ``thumbnail(imageField, template)``   | Render path to given thumbnail.  |
+---------------------------------------+----------------------------------+
| ``download(fileField)``               | Render path to given file.       |
+---------------------------------------+----------------------------------+
| ``fileinfo(fileField)``               | Get file information.            |
+---------------------------------------+----------------------------------+

Filters
-------

+--------------------+--------+
| Filter Syntax      | Usage  |
+====================+========+
| ``FILTERNAME``     | ...    |
+--------------------+--------+

Tags
----

+-----------------+--------+
| Tag Syntax      | Usage  |
+=================+========+
| ``TAGNAME``     | ...    |
+-----------------+--------+

Global Variables
----------------

+----------------------+--------+
| Variable             | Usage  |
+======================+========+
| ``Global Variable``  | ...    |
+----------------------+--------+

.. _`http://twig.sensiolabs.org/documentation`: http://twig.sensiolabs.org/documentation
