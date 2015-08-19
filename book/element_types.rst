.. index::
    single: Book; Element Types

Element Types
=============

Element Type Manager
--------------------

All access to element types is done via the element type manager.

.. code-block:: php

    $elementtypeManager = $this->get('phlexible_elementtype.elementtype_manager');
        
Retrieving Element Types
------------------------

To fetch an element types by id, use the ``find()`` method on the element type manager:

.. code-block:: php

    // find element type by id
    $elementtype = $elementtypeManager->find($elementtypeId);

The element type manager also provides additional methods for finding element types:

.. code-block:: php

    // find element types by criteria
    $elementtypes = $elementtypeManager->findBy(array('uniqueId' => 'my-elementtype'));

    // find a element type by criteria
    $elementtype = $elementtypeManager->findOneBy(array('type' => 'full'));

    // find all element types
    $elementtypes = $elementtypeManager->findAll();

Updating Element Types
----------------------

To update an element type, call the ``updateElementtype()`` method on the element type manager:

.. code-block:: php

    // for an existing elementtype
    $elementtype = $elementtypeManager->find(1);

    // ... or for a new elementtype
    $elementtype = new \Phlexible\Component\Elementtype\Model\Elementtype();

    $elementtype->setUniqueId('my-elementtype');

    // update elementtype
    $elementtypeManager->updateElementtype($elementtype);

Deleting Element Types
----------------------

To delete an element type, call the ``deleteElementtype()`` method on the element type manager:

.. code-block:: php

    $elementtype = $elementtypeManager->find(1);

    // delete elementtype
    $elementtypeManager->deleteElementtype($elementtype);
