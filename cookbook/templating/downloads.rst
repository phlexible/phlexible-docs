.. index::
   single: Templating; Working with Downloads

Working with Downloads
======================

All media files are located in phlexible media management. You can access them with fields in your element.

Examples
--------

Create link to download file
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: jinja

    <a href="{{ download_path(file) }}">
        {{ title|default(fileInfo.meta.file.title)|default(fileInfo.name) }}
        <span class="meta">({{ fileInfo.mediaType|upper }}, {{ fileInfo.size|readable_size }})</span>
    </a>

Add Mimetype Icon to your download link
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. Please check if ``brainbits/mimetype-icon-bundle`` is installed in your project

.. code-block:: jinja

    {% import "@BrainbitsMimetypeIcon/icon.html.twig" as icon %}
    {% set fileInfo = fileinfo(file) %}
    …
    <a href="{{ download_path(file) }}" class="{{ icon.icon(fileInfo.mediaType|lower) }}">
        {{ title|default(fileInfo.meta.file.title)|default(fileInfo.name) }}
        <span class="meta">({{ fileInfo.mediaType|upper }}, {{ fileInfo.size|readable_size }})</span>
    </a>

You have to import this macro in your template with ``{% import "@BrainbitsMimetypeIcon/icon.html.twig" as icon %}`` before you can call your macro. With ``class="{{ icon.icon(fileInfo.mediaType|lower) }}"`` do you add class names for using icons. The example above would compile following line and Layout:

.. image:: /images/cookbook/mimetype-icon.png
    :align: right
    :alt: Example, how mime type icons work

.. code-block:: jinja

    <a href="/media/download/06c1b233-e611-4b56-a1a4-0f16d6715394" class="icon-mimetype icon-pdf">Title <span class="meta">(PDF, 266 kB)</span></a>
