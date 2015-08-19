.. index::
   single: Book; Architecture

Architecture Overview
=====================

Before we dive separately into every phlexible part, you need to have an overview of how our main application is structured.
You already know that phlexible is built from phlexible bundles and Symfony2 bundles, which are integration layers with the framework.

All bundles share the conventions for naming things and the same way of data persistence. 
Bundles providing data persistance provide a persistance manager interface, that defines the contract for persisting data objects.
phlexible, by default, provides persistance managers that use the doctrine ORM.
You can create custom persistance managers by implementing the respective interfaces.

For deeper understanding of how Doctrine works, please refer to the `excellent documentation on their official website <http://doctrine-orm.readthedocs.org/en/latest/>`_.
