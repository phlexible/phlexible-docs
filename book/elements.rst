.. index::
    single: Elements

Elements
========

One of the most common tasks in phlexible is working with elements.
Elements manage the content and they are defined by their elementtypes.

Create Element
--------------

To create an element, get the elementtype and call the ``createElement()``
method. Finally add it to the :doc:`tree </book/tree>`::

    /**
     * Create an Element
     */
    public function createAction(Request $request)
    {
        $elementService = $this->get('phlexible_element.element_service');

        // load element source
        $elementSource = $this->elementService->findElementSource($elementtypeId);

        // create element
        $element = $elementService->createElement($elementSource, $masterLanguage, $userId);

        // add element to tree
        $node = $tree->create(
            $parentElementId,
            $afterElementId,
            'element',
            $element->getEid(),
            array(),
            $userId
        );

        // ... return ResultResponse
    }

.. note::

    After doing this, you have an **empty** node (with no data) in your tree.
    See :ref:`Save Element Data <docs-save-element-data>` on how to add data.

.. _docs-save-element-data:

Create Element Version
----------------------

Create or load an element and add a new version by calling ``createElementVersion()`` on 
the element service::

    public function saveAction(Request $request)
    {
        // get needed data from request
        $values   = $request->request->all();
        $language = $request->get('language');

        $elementService = $this->get('phlexible_element.element_service');

        // find element
        $element = $elementService->findElement(123);

        // create new element structure
        $elementStructure = new ElementStructure();
        // ... set values to elementStructure

        // create new element version
        $elementVersion = $elementService->createElementVersion(
            $element,
            $elementStructure,
            $language,
            $userId,
            'element comment'
        );

        // ... return ResultResponse
    }

