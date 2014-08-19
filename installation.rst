.. index::
single: Installation

Installing and Configuring phlexible 1.0
========================================

The goal of this chapter is to get you up and running with a working phlexible 1.0 application
built on top of Symfony2.


Installing phlexible 1.0
------------------------
.. tip::

    First, check that you have installed the Symfony2 Standard Distribution. See
    `http://symfony.com/doc/current/book/installation.html`_ for details.

After Symfony2 is installed, you can add phlexible 1.0 by adding several bundles to your ``composer.json`` file.

Step 1: Add Composer repository
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Before you can use the phlexible package or any of its bundles, you have to add
the `phlexible Composer Repository`_. Paste the following into your ``composer.json``:

.. code-block:: json

    {
        "repositories": [
            {
                "type": "composer",
                "url": "https://packages.brainbits.net/phlexible-bundles/"
            }
        ]
    }

Step 2: Adding libraries
~~~~~~~~~~~~~~~~~~~~~~~~

phlexible 1.0 itself is a library and depends on a number of external libraries which you have to add
before you can start. Open your ``composer.json`` and add the following:

.. code-block:: json

    {
        ...,
        "require": {
            ...,

            "nelmio/api-doc-bundle": "~2.5",
            "alchemy/zippy": "~0.2",
            "jms/cg": "dev-master",
            "cocur/slugify": "~0.8",
            "phansys/getid3": "v2.0.0-BETA1",

            "phlexible/phlexible": "dev-master",
            "brainbits/toolkit": "dev-master"
        }
    }


Step 3: Updating Vendors
~~~~~~~~~~~~~~~~~~~~~~~~

To download all necassary libraries - including phlexible itself - you have to update your vendors.

.. code-block:: bash

    $ php composer.phar update

Step 4: Enable phlexible
~~~~~~~~~~~~~~~~~~~~~~~~

At this point, the necassary bundles are installed in your ``vendor/`` directory and
the autoloader recognizes its classes. The only thing you need to do now is register
the needed bundles in ``AppKernel``::

    // app/AppKernel.php

    // ...
    class AppKernel extends Kernel
    {
        // ...

        public function registerBundles()
        {
            $bundles = array(
                // ...,

                new Igorw\FileServeBundle\IgorwFileServeBundle(),

                new Nelmio\ApiDocBundle\NelmioApiDocBundle(),

                new Symfony\Cmf\Bundle\RoutingBundle\CmfRoutingBundle(),

                // phlexible.core
                new Phlexible\Bundle\GuiBundle\PhlexibleGuiBundle(),
                new Phlexible\Bundle\SecurityBundle\PhlexibleSecurityBundle(),
                new Phlexible\Bundle\MessageBundle\PhlexibleMessageBundle(),
                new Phlexible\Bundle\QueueBundle\PhlexibleQueueBundle(),
                new Phlexible\Bundle\UserBundle\PhlexibleUserBundle(),
                new Phlexible\Bundle\ProblemBundle\PhlexibleProblemBundle(),
                new Phlexible\Bundle\CacheBundle\PhlexibleCacheBundle(),
                new Phlexible\Bundle\DashboardBundle\PhlexibleDashboardBundle(),
                new Phlexible\Bundle\SearchBundle\PhlexibleSearchBundle(),
                new Phlexible\Bundle\AccessControlBundle\PhlexibleAccessControlBundle(),
                new Phlexible\Bundle\DataSourceBundle\PhlexibleDataSourceBundle(),
                new Phlexible\Bundle\TemplateBundle\PhlexibleTemplateBundle(),
                new Phlexible\Bundle\TranslationBundle\PhlexibleTranslationBundle(),

                // phlexible.media
                new Phlexible\Bundle\MediaAssetBundle\PhlexibleMediaAssetBundle(),
                new Phlexible\Bundle\MediaExtractorBundle\PhlexibleMediaExtractorBundle(),
                new Phlexible\Bundle\MediaTemplateBundle\PhlexibleMediaTemplateBundle(),
                new Phlexible\Bundle\MediaCacheBundle\PhlexibleMediaCacheBundle(),
                new Phlexible\Bundle\MediaSiteBundle\PhlexibleMediaSiteBundle(),
                new Phlexible\Bundle\MediaManagerBundle\PhlexibleMediaManagerBundle(),
                new Phlexible\Bundle\DocumenttypeBundle\PhlexibleDocumenttypeBundle(),
                new Phlexible\Bundle\MetaSetBundle\PhlexibleMetaSetBundle(),
                new Phlexible\Bundle\MediaToolBundle\PhlexibleMediaToolBundle(),

                // phlexible.cms
                new Phlexible\Bundle\CmsBundle\PhlexibleCmsBundle(),
                new Phlexible\Bundle\SiterootBundle\PhlexibleSiterootBundle(),
                new Phlexible\Bundle\ContentchannelBundle\PhlexibleContentchannelBundle(),
                new Phlexible\Bundle\ElementtypeBundle\PhlexibleElementtypeBundle(),
                new Phlexible\Bundle\ElementBundle\PhlexibleElementBundle(),
                new Phlexible\Bundle\TeaserBundle\PhlexibleTeaserBundle(),
                new Phlexible\Bundle\TreeBundle\PhlexibleTreeBundle(),
                new Phlexible\Bundle\FrontendBundle\PhlexibleFrontendBundle(),
                new Phlexible\Bundle\FrontendMediaBundle\PhlexibleFrontendMediaBundle(),
                new Phlexible\Bundle\ElementRendererBundle\PhlexibleElementRendererBundle(),
                new Phlexible\Bundle\FrontendAssetBundle\PhlexibleFrontendAssetBundle(),
                new Phlexible\Bundle\TaskBundle\PhlexibleTaskBundle(),
                new Phlexible\Bundle\TwigRendererBundle\PhlexibleTwigRendererBundle(),
            );
        }
    }

Configuration and Setup
~~~~~~~~~~~~~~~~~~~~~~~

At this point, all of the needed third-party libraries now live in the ``vendor/``
directory. You also have a default application setup in ``app/`` and some
sample code inside the ``src/`` directory.

.. _`http://symfony.com/doc/current/book/installation.html`: http://symfony.com/doc/current/book/installation.html
.. _`phlexible Composer Repository`: https://packages.brainbits.net/phlexible-bundles/
