.. index::
   single: Templating; Working with Downloads

Working with File Fields
========================

All media files are located in phlexible media management. You can access them with fields in your element.

.. _cookbook_templating_downloads_link:

How to create a file download link
----------------------------------

.. code-block:: jinja

    {% set file = content.value('cm_download_file') %}
    {% set fileInfo = fileinfo(file) %}
    <a href="{{ download_path(file) }}">
        {{ title|default(fileInfo.meta.file.title)|default(fileInfo.name) }}
        <span class="meta">({{ fileInfo.mediaType|upper }}, {{ fileInfo.size|readable_size }})</span>
    </a>

This example retrieves a ``file`` value from :ref:`variables_content` and renderes a link via the :ref:`extensions_download_path` function. Information about ``file`` is retrieved via the :ref:`extensions_fileinfo` function. The title is rendered either from the meta title, or the file name as a fallback. Additionally the file size is rendered via the :ref:`extensions_readable_size` function.

.. _cookbook_templating_downloads_media_type_icon:

How to create a media type icon for a download link
---------------------------------------------------

.. hint::

    This examples requires that the ``brainbits/mimetype-icon-bundle`` is installed in your project.

.. code-block:: jinja

    {% import "@BrainbitsMimetypeIcon/icon.html.twig" as mediaType %}
    {% set fileInfo = fileinfo(file) %}
    …
    <a href="{{ download_path(file) }}" class="{{ mediaType.icon(fileInfo.mediaType|lower) }}">
        {{ title|default(fileInfo.meta.file.title)|default(fileInfo.name) }}
        <span class="meta">({{ fileInfo.mediaType|upper }}, {{ fileInfo.size|readable_size }})</span>
    </a>

This examples renders a media type icon, based on the media type of the given file. The media type is retrieved via the :ref:`extensions_fileinfo` function.

In the first line, the ``icon`` macro is imported into the current template. The macro is called with ``{{ mediaType.icon(fileInfo.mediaType|lower) }}"``, which returns the css class name of the media type. 

The html of the rendered example looks like this:

.. code-block:: jinja

    <a href="/media/download/06c1b233-e611-4b56-a1a4-0f16d6715394" class="icon-mimetype icon-pdf">
        Title <span class="meta">(PDF, 266 kB)</span>
    </a>

And is displayed like this:

.. image:: /images/cookbook/mimetype-icon.png
    :alt: Example, how mime type icons work

