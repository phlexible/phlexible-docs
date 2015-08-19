.. index::
   single: Templating; Working with Image Fields

Working with Image Fields
=========================

All media files are located in phlexible media management. You can access them with fields in your element.

.. _cookbook_templating_images_thumbnail:

How to create an image thumbnail
--------------------------------

.. code-block:: jinja

    {% set image = content.value('cm_gallery_image') %}
    <img src="{{ thumbnail_path(image, "teaser_image") }}" />

This example retrieves an ``image`` value from :ref:`variables_content` and uses the :ref:`extensions_thumbnail_path` function create a thumbnail link using ``image`` and the ``"teaser_image"`` media template.

.. _cookbook_templating_images_alt:

How to create an image thumbnail with alt-attribute from metadata
-----------------------------------------------------------------

.. code-block:: jinja

    {% set imageInfo = fileinfo(image) %}
    {% set altText   = imageInfo.meta.image.alttext %}
    <img src="{{ thumbnail_path(image, "teaser_image") }}" alt="{{ altText }}" />

This example uses the :ref:`extensions_fileinfo` function to get the alt text from the meta information of the file. 

.. _cookbook_templating_images_zoom:

How to provide a zoom link for larger images
--------------------------------------------

.. code-block:: jinja

    {% set templateWidth = mediatemplate(template).width %}
    {% set imageWidth = imageInfo.attributes['image.width'] %}
    {% if imageWidth > templateWidth %}
        <a href="{{ image_path(image) }}" class="lightbox" target="_blank" title="{{ imageInfo.meta.file.title }}">
    {% endif %}

     <img src="{{ thumbnail_path(image, "teaser_image") }}" alt="{{ altText }}" />

    {% if imageWidth > templateWidth %}
            <span class="zoom">{{ "lightbox.open_lightbox"|trans }}</span>
        </a>
    {% endif %}

This example uses the :ref:`extensions_mediatemplate` function to retrieve information about the media ``template``. A link to the larger original ``image`` is only rendered, if the media ``template`` width is larger than the the ``image`` width, via the :ref:`extensions_image_path` function.
