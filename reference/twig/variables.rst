.. index::
    single: phlexible Twig variables

phlexible Twig Variables
========================

siteroot
--------
**type**: ``Phlexible\Bundle\SiterootBundle\Entity\Siteroot``

``siteroot.id``
    **returns**: ``string``

treeNode
--------
**type**: ``Phlexible\Bundle\TreeBundle\ContentTree\ContentTreeNode``

``treeNode.id``
    **returns**: ``string``

treeContext
-----------
**type**: ``Phlexible\Bundle\TreeBundle\ContentTree\ContentTreeContext``

``treeContext.title``
    **returns**: ``string``

Navigation title from node.

``treeContext.active``
    **returns**: ``boolean``

``true`` if node is active.

``treeContext.viewable``
    **returns**: ``boolean``

``true`` if node is in navigation, is published and not a structure element.

``treeContext.viewableChildren``
    **returns**: ``boolean``

``true`` if node has at least one viewable child, i.e. that is in navigation, are published and aren't structure elements.

contentElement
--------------
**type**: ``Phlexible\Bundle\ElementBundle\ContentElement\ContentElement``

content
-------
**type**: ``Phlexible\Bundle\ElementBundle\Model\ElementStructure``

The content of the current node.

``content.findValue(name)``
    
    **returns**: ``boolean``

specialTids
-----------
**type**: ``array``

An array that contains all special tids from current siteroot.

navigation
----------
**type**: ``array``

An array that contains all navigations for the current node.

teasers
-------
**type**: ``array``

An array that contains all teasers for the current node.