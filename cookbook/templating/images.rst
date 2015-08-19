.. index::
   single: Templating; Working with Images

Working with Images
===================

All media files are located in phlexible media management. You can access them with fields in your element.

Examples
--------

.. _cookbook_templating_images_thumbnail:

Render an image thumbnail with alt-attribute from metadata
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: jinja

    {% set imageInfo = fileinfo(image) %}
    {% set altText   = imageInfo.meta.image.alttext %}
    <img src="{{ thumbnail_path(image, template) }}" alt="{{ altText }}" />

This example uses the :ref:`extensions_fileinfo` function to get the alt text from the meta information of the file. The image is rendered using the ``image`` and the media ``template`` via the :ref:`extensions_thumbnail_path` function.

.. _cookbook_templating_images_zoom:

Provide a zoom link if the original image is bigger than template image
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ 

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

This example uses the :ref:`extensions_mediatemplate` function to retrieve information about the media ``template``. A link to the larger original ``image`` is only rendered, if the media ``template`` width is larger than the the ``image`` width, via the :ref:`extensions_image_path` function.
