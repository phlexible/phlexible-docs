.. index::
    single: Book; Siteroots

Siteroots
=========

Siteroot Manager
----------------

All access to siteroots is done via the siteroot manager.

.. code-block:: php

    $siterootManager = $this->get('phlexible_siteroot.siteroot_manager');
        
Retrieving Siteroots
--------------------

To fetch a siteroot by id, use the ``find()`` method on the siteroot manager:

.. code-block:: php

    // find siteroot by id
    $siteroot = $siterootManager->find($siterootId);

The siteroot manager also provides additional methods for finding siteroots:

.. code-block:: php

    // find siteroots by criteria
    $siteroots = $siterootManager->findBy(array('type' => 'image'));

    // find a siteroot by criteria
    $siteroot = $siterootManager->findOneBy(array('title' => 'my_siteroot'));

    // find all siteroots
    $siteroots = $siterootManager->findAll();

Updating Siteroots
------------------

To update a siteroot, call the ``updateSiteroot()`` method on the siteroot manager:

.. code-block:: php

    // for an existing siteroot
    $siteroot = $siterootManager->find(1);

    // ... or for a new siteroot
    $siteroot = new \Phlexible\Bundle\SiterootBundle\Entity\Siteroot();

    $siteroot->setTitle('testSiteroot');

    // update siteroot
    $siterootManager->updateSiteroot($siteroot);

Deleting Siteroots
------------------

To delete a siteroot, call the ``deleteSiteroot()`` method on the siteroot manager:

.. code-block:: php

    $siteroot = $siterootManager->find(1);

    // delete siteroot
    $siterootManager->deleteSiteroot($siteroot);

Siteroots in the CLI
--------------------

Information about siteroots can be displayed via a cli command.

Display siteroot id and name of all siteroots:

.. code-block:: bash

	$ php app/console siteroot:show

Display detailled information about all siteroots:

.. code-block:: bash

	$ php app/console siteroot:show -v