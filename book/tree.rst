.. index::
    single: Book; Tree

Tree
====

The tree is a hierarchical collection of nodes, each nodes points to a content :doc:`element </book/elements>`.
It defines the page structure of your project. 

You can think of it as a filesystem:

.. code-block:: text

    Root [1]
    ├─ Main Navigation [2]
    |   ├─ Home [4]
    |   ├─ Career [5]
    |   └─ Contact [6]
    └─ Meta Navigation [3]
        ├─ Error 500 [7]
        ├─ Error 404 [8]
        └─ Search [9]

New nodes can created in the tree, existing nodes can be updated, copied or moved inside the tree.

Tree Manager
------------

All access to trees is done via the tree manager. 

.. code-block:: php

    $treeManager = $this->get('phlexible_tree.tree_manager');
        
Tree
----

Use the tree manager to retrieve a specific tree, either by siteroot id, or by a node id inside the tree.

.. code-block:: php

    $tree = $treeManager->getBySiterootId($siterootId);
    $tree = $treeManager->getByNodeId($nodeId);

Retrieving Nodes
----------------

Navigate through a tree:

.. code-block:: php

    // get the "Main Navigation" node from the example above
    $node = $tree->get(2);

    // get path array - tree nodes or ids
    $path   = $tree->getPath($node);
    $idPath = $tree->getIdPath($node);

    // get children of node -> 4,5,6
    $children = $tree->getChildren($node);
    $childNode = current($children);

    // get parent -> 1
    $parentNode = $tree->getParent($node);

    // different check methods
    $isChild     = $tree->isChildOf($childNode, $parentNode);  // will return true
    $isParent    = $tree->isParentOf($parentNode, $childNode); // will return true
    $isRoot      = $tree->isRoot($node);                       // will return false
    $hasChildren = $tree->hasChildren($node);                  // will return true

    $tree->getParent($parentNode);                             // will be null

    $tree->isRoot($tree->getRoot());                           // will return true

Updating Nodes
--------------

Update a node by calling ``updateNode()`` on the tree:

.. code-block:: php

    $node = $tree->get(4);
    $node->setAttribute('foo', 'bar');

    $tree->updateNode($node);

Deleting Nodes
--------------

Delete a node by calling ``delete()`` on the tree:

.. code-block:: php

    $node = $tree->get(4);
    
    $tree->delete($node, $userId);

    

