.. index::
    single: Elements

Elements
========

One of the most common tasks in phlexible is working with elements.
Elements manage the content and they are defined by their elementtypes.

Create Element
--------------

To create an element, you need to now the elementtype and have to create
a new version for your element. Finally add it to the :doc:`tree </book/tree>`::

    /**
     * Create an Element
     */
    public function createAction(Request $request)
    {
        // load elementtype and elementtype version
        $elementService     = $this->get('phlexible_element.element_service');
        $elementtype        = $elementService->getElementtypeService()->findElementtype($elementtypeId);
        $elementtypeVersion = $elementService->getElementtypeService()->findLatestElementtypeVersion($elementtype);

        $element = $elementService->createElement($elementtypeVersion, $masterLanguage, $userId);

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

Save Element Data
-----------------

After you created an element, save the data by doing::

    public function saveAction(Request $request)
    {
        $dataSaver      = $this->get('phlexible_element.data_saver');
        $elementVersion = $saver->save($request, $this->getUser());

        // ... return ResultResponse
    }

Delete Element
--------------

Delete an element by calling::

    public function deleteAction(Request $request)
    {
        $treeManager = $this->get('phlexible_tree.tree_manager');

        $siterootId  = $request->get('siterootId');
        $tree        = $treeManager->getBySiteRootId($siterootId);
        $node        = $tree->get($id);

        $tree->delete($node, $userId);

        // ... return ResultResponse
    }

