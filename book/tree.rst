.. index::
    single: Tree

Tree
====

The tree holds each :doc:`element </book/elements>`
and defines the project structure. You can think of it as a filesystem:

.. code-block:: text

    Root [1]
    ├─ Main Navigation [2]
        ├─ Home [4]
        ├─ Career [5]
        └─ Contact [6]
    └─ Meta Navigation [3]
        ├─ Error 500 [7]
        ├─ Error 404 [8]
        └─ Search [9]

Each node represents an element in phlexible. The number in the bracket
is the id of the element in the the tree. You can create, copy or move nodes
in the tree and even create instances of nodes at another point in the tree.

Navigating
----------

Load the tree and "navigate" through it::

    /**
     * Example of navigating through the tree for a given siteroot
     */
    public function navigateAction(Request $request)
    {
        $siterootId  = $request->get('siterootId');
        $treeManager = $this->get('phlexible_tree.tree_manager');
        $tree        = $treeManager->getBySiteRootId($siterootId);

        // get "Main Navigation" node (see above)
        $node = $tree->get(2);

        // get path array - tree nodes or ids
        $path   = $tree->getPath($node);
        $idPath = $tree->getIdPath($node);

        // get children of node -> 4,5,6
        $children = $tree->getChildren($node);

        // get parent -> 1
        $parent = $tree->getParent($node);

        // different check methods
        $isChild     = $tree->isChildOf($childNode, $parentNode);
        $isParent    = $tree->isParentOf($parentNode, $childNode);
        $isRoot      = $tree->isRoot($node);
        $hasChildren = $tree->hasChildren($node);
    }

