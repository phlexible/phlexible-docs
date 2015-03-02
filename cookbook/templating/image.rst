.. index::
   single: Templating; Working with Images

Working with Image
==========================

All media files are located in phlexible media management. You can access them with fields in your element.

Variables
---------

Functions
---------

``fileinfo(media)``
~~~~~~~~~~~~~~~~~~~~

``media``
    **type**: ``object``

Returns an array with following data:

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

``thumbnail_path(media, template)``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

``media``
    **type**: ``object``

``template``
    **type**: ``string``

Template for transcoding original image to defined view

``mediatemplate(template)``
~~~~~~~~~~~~~~~~~~~~~~~~~~~

``template``
    **type**: ``string``

Returns an array with template definitions for ``template``

Examples
--------

Include an image with alt-attribute from metadata
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: jinja

    {% set imageInfo = fileinfo(image) %}
    {% set altText   = imageInfo.meta.image.alttext %}
    <img src="{{ thumbnail_path(image, template) }}" alt="{{ altText }}" />

Creating an image gallery if original image is bigger than used image
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: jinja

    {% set templateWidth = mediatemplate(template).width %}
    {% set imageWidth = imageInfo.attributes['image.width'] %}
    {% if imageWidth > templateWidth %}
        <a href="{{ image_path(image) }}" class="lightbox" target="_blank" title="{{ imageInfo.meta.file.title }}">
    {% endif %}

     <img src="{{ thumbnail_path(image, template) }}" alt="{{ altText }}" />

    {% if imageWidth > templateWidth %}
            <span class="zoom">{{ "lightbox.open_lightbox"|trans }}</span>
        </a>
    {% endif %}