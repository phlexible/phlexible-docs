.. index::
    single: Book; Media Templates

Media Templates
===============

Media Template Manager
----------------------

All access to media templates is done via the media template manager.

.. code-block:: php

    $templateManager = $this->get('phlexible_media_template.media_template_manager');
        
Retrieving Media Templates
--------------------------

To fetch a media template by id, use the ``find()`` method on the media template manager:

.. code-block:: php

    // find media template by id
    $template = $templateManager->find($id);

The media template manager also provides additional methods for finding media templates:

.. code-block:: php

    // find media templates by criteria
    $templates = $templateManager->findBy(array('type' => 'image'));

    // find a media template by criteria
    $template = $templateManager->findOneBy(array('name' => 'my_media_template'));

    // find all media templates
    $templates = $templateManager->findAll();

Updating Media Templates
------------------------

To update a media template, call the ``updateTemplate()`` method on the media template manager:

.. code-block:: php

    // for an existing template
    $template = $templateManager->find(1);

    // ... or for a new template
    $template = new \Phlexible\Component\MediaTemplateBundle\Entity\ImageTemplate();

    $template->setWidth(100);
    $template->setMethod('crop');

    // update template
    $templateManager->updateTemplate($template);

Deleting Media Templates
------------------------

To delete a media template, call the ``deleteTemplate()`` method on the media template manager:

.. code-block:: php

    $template = $templateManager->find(1);

    // delete template
    $templateManager->deleteTemplate($template);
