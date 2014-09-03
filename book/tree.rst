.. index::
    single: Tree

Tree
====

The tree is one of the most important things in phlexible. It holds each :doc:`element </book/elements>`
and defines the project structure. You can think of it as a filesystem:

.. code-block:: text

    Root
    ├─ Main Navigation
        ├─ Home
        ├─ Career
        └─ Contact
    └─ Meta Navigation
        ├─ Error 500
        ├─ Error 404
        └─ Search

Each node represents an element in phlexible. You can create, copy or move nodes
in the tree and even create instances of nodes at another point in the tree.

Create Node
-----------

To create a new node in the tree, you can
