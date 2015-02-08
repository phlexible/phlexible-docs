.. index::
   single: Architecture

Architecture Overview
=====================

Before we dive separately into every phlexible concept, you need to have an overview of how our main application is structured.
You already know that phlexible is built from components and Symfony2 bundles, which are integration layers with the framework.

All bundles share the conventions for naming things and the same way of data persistence. phlexible, by default, uses Doctrine ORM for managing all entities.

For deeper understanding of how Doctrine works, please refer to the `excellent documentation on their official website <http://doctrine-orm.readthedocs.org/en/latest/>`_.
