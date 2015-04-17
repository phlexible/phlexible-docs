.. index::
   single: Templating; Working with Images

Working with Images
===================

All media files are located in phlexible media management. You can access them with fields in your element.

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