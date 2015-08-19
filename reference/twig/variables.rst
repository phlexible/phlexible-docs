.. index::
    single: phlexible Twig variables

phlexible Twig Variables
========================

.. _variables_siteroot:

siteroot
--------
**type**: ``Phlexible\Bundle\SiterootBundle\Entity\Siteroot``

The ``siteroot`` variable contains the current siteroot.

Notable accessors are:

* ``siteroot.id`` Returns the ID of the siteroot.
* ``siteroot.title`` Returns the title of the siteroot.

.. _variables_treeNode:

treeNode
--------
**type**: ``Phlexible\Bundle\TreeBundle\ContentTree\ContentTreeNode``

The ``treeNode`` variable contains the current Node.

Notable accessors are:

* ``treeNode.id`` Returns the ID of the node.
* ``treeNode.publishedAt`` Returns the publish date of the node.

.. _variables_treeContext:

treeContext
-----------
**type**: ``Phlexible\Bundle\TreeBundle\ContentTree\ContentTreeContext``

The ``treeContext`` variable contains the current Tree Context. 

Notable accessors are:

* ``treeContext.title`` Returns the page title of the node.
* ``treeContext.viewable`` Returns ``true`` if the node is in navigation, is published and not a structure element.
* ``treeContext.viewableChildren`` Returns ``true`` if the node has at least one viewable child, i.e. that is in navigation, are published and aren't structure elements.

.. _variables_contentElement:

contentElement
--------------
**type**: ``Phlexible\Bundle\ElementBundle\ContentElement\ContentElement``

The ``contentElement`` variable contains the current Element.

Notable accessors are:

* ``contentElement.eid`` Returns the eid of the element.

.. _variables_content:

content
-------
**type**: ``Phlexible\Bundle\ElementBundle\Model\ElementStructure``

The ``content`` variable contains the content of the current node.

Notable accessors are:

* ``content.value(name)`` Returns the first value with the given ``name``.
* ``content.children(name)`` Returns children of ``name``.

.. _variables_navigations:

navigations
-----------
**type**: ``array``

The ``navigation`` variable contains an array of :ref:`variables_treeContext`, with each representing a navigation for the current node.
Each entry is of type ``TreeContext``, but provides additional context sensitive navigation information:

* ``treeContext.active`` Returns true, if this node is in the current path.

.. _variables_teasers:

teasers
-------
**type**: ``array``

The ``teasers`` variable contains an array with all layout areas and teasers of the current node.
