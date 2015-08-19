.. index::
    single: Book; Introduction

Introduction to phlexible
=========================

phlexible is a cms solution for PHP, based on the Symfony2 framework.


Leveraging Symfony2 Bundles
---------------------------

If you prefer to build your very custom system step by step and from scratch, you can integrate the standalone Symfony2 bundles. For the installation instructions, please refer to the appropriate bundle documentation.

Concepts
--------

Element Types
~~~~~~~~~~~~~

phlexible uses dynamic content structures to save the data of your website. The prototypes of these content structures are called Element Types, and can be created and modified via the GUI.

Each Element Type represents a hierarchical structure of fields, and each field can be configured in various way, including repeat for containers, validation for fields and labels.
These Element Types fulfill 2 tasks, at first they define the data structure for content, and at second the define the look of the edit masks for the content.

Elements
~~~~~~~~

Elements are concrete data objects, that are bound to an Element Type, and store the data that a user externs on the data masks.
The data can have multiple languages, and is completely versioned.

Nodes
~~~~~

Nodes define the structure of your web page, each node is bound to a concrete Element, and has a full publish lifecycle with online states and publication history.

