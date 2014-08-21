.. index::
    single: Installation

Installing and Configuring phlexible
====================================

The goal of this chapter is to get you up and running with a working phlexible application
built on top of Symfony2.


Installing phlexible
--------------------
.. tip::

    First, check that you have installed the Symfony2 Standard Distribution. See
    `http://symfony.com/doc/current/book/installation.html`_ for details.

After Symfony2 is installed, you can add phlexible by adding several bundles to your ``composer.json`` file.

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

phlexible itself is a library and depends on a number of external libraries which you have to add
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

To download all necessary libraries - including phlexible itself - you have to update your vendors.

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
                new Phlexible\Bundle\DashboardBundle\PhlexibleDashboardBundle(),
                new Phlexible\Bundle\SearchBundle\PhlexibleSearchBundle(),
                new Phlexible\Bundle\AccessControlBundle\PhlexibleAccessControlBundle(),
                new Phlexible\Bundle\DataSourceBundle\PhlexibleDataSourceBundle(),

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

Configuration
-------------

App configuration
~~~~~~~~~~~~~~~~~

phlexible  requires some configuration to be added to app's ``app/config/config.yml`` file:

.. code-block:: yaml

    # CMF Routing Bundle
    cmf_routing: ~

    # Igorw File Serve Bundle
    igorw_file_serve:
        factory: php # php
        #factory: sendfile # nginx
        #factory: xsendfile # apache

    phlexible_gui:
        project:
            title:   Your Project Title
            version: 1.0.0
            url:     project.dev
        languages:
            default:   en
            available: en,de
        mail:
            from_name:  John Doe
            from_email: john.doe@example.com

    phlexible_cms:
        languages:
            default: de
            available: en,de

    phlexible_message:
        use_log_handler: false
        audit_entities: false

    phlexible_meta_set:
        languages:
            default: de
            available: en,de

    phlexible_media_cache:
        storages:
            default:
                id: phlexible_media_cache.storage.local
                options:
                    storage_dir: %media_cache_storage_dir%

    phlexible_media_site:
        sites:
            default:
                id: 492d88c5-dd48-4d73-b849-1cacc0a80056 # this has to be a generated id
                root_dir: %media_manager_root_dir%
                quota: 1000000000
                driver: phlexible_media_manager.site_default

    phlexible_siteroot:
        overrides:
            48ef589f-2ddc-4cb6-9a54-7e0dc0a8005b:
                navigation:
                    0:
                        url: project.dev
                        path: ~
                        language: ~
                        default: 1
                        type: element
                        target: 1062

    phlexible_media_tool:
        swftools:
            pdf2swf: %tool_pdf2swf%
            swfdump: %tool_swfdump%
            swfcombine: %tool_swfcombine%

        pdftotext:
            pdftotext: %tool_pdftotext%
            pdfinfo: %tool_pdfinfo%

        mime:
            file: %tool_file%

        imagemagick:
            identify: %tool_identify%
            convert: %tool_convert%
            mogrify: %tool_mogrify%

        ffmpeg:
            ffprobe: %tool_ffprobe%
            ffmpeg: %tool_ffmpeg%~

Parameters
~~~~~~~~~~

As you can see in the previous section, there are some parameters to be set.
Open ``app/config/parameters.yml`` and set the following values:

.. code-block:: yaml

    tool_identify: /path/to/identify
    tool_convert: /path/to/convert
    tool_mogrify: /path/to/mogrify
    tool_ffprobe: /path/to/ffprobe
    tool_ffmpeg: /path/to/ffmpeg
    tool_pdf2swf: /path/to/pdf2swf
    tool_swfdump: /path/to/swfdump
    tool_swfcombine: /path/to/swfcombine
    tool_pdftotext: /path/to/pdftotext
    tool_pdfinfo: /path/to/pdfinfo
    tool_file: /path/to/file
    media_manager_root_dir: /path/to/project/media/files/
    media_cache_storage_dir: /path/to/project/media/frames/

Routing
~~~~~~~

To make the backend routes available, you have to add a resource to ``app/config/routing.yml``:

.. code-block:: yaml

    admin:
        resource: admin_routing.yml
        prefix:   /admin

After that, you have to add a new file ``app/config/admin_routing.yml`` and add the following lines:

.. code-block:: yaml

    phlexible_accesscontrol:
        resource: "@PhlexibleAccessControlBundle/Controller/"
        type:     annotation

    phlexible_contentchannels:
        resource: "@PhlexibleContentchannelBundle/Controller/"
        type:     annotation

    phlexible_dashboard:
        resource: "@PhlexibleDashboardBundle/Controller/"
        type:     annotation

    phlexible_datasources:
        resource: "@PhlexibleDataSourceBundle/Controller/"
        type:     annotation

    phlexible_documenttypes:
        resource: "@PhlexibleDocumenttypeBundle/Controller/"
        type:     annotation

    phlexible_elements:
        resource: "@PhlexibleElementBundle/Controller/"
        type:     annotation

    phlexible_elementtypes:
        resource: "@PhlexibleElementtypeBundle/Controller/"
        type:     annotation

    phlexible_frontend_preview:
        resource: "@PhlexibleFrontendBundle/Controller/PreviewController.php"
        type:     annotation

    phlexible_frontendmedia_folder:
        resource: "@PhlexibleFrontendMediaBundle/Controller/FolderController.php"
        type:     annotation

    phlexible_gui:
        resource: "@PhlexibleGuiBundle/Controller/"
        type:     annotation

    phlexible_mediamanager:
        resource: "@PhlexibleMediaManagerBundle/Controller/"
        type:     annotation

    phlexible_mediatemplates:
        resource: "@PhlexibleMediaTemplateBundle/Controller/"
        type:     annotation

    phlexible_messages:
        resource: "@PhlexibleMessageBundle/Controller/"
        type:     annotation

    phlexible_metasets:
        resource: "@PhlexibleMetaSetBundle/Controller/"
        type:     annotation

    phlexible_problems:
        resource: "@PhlexibleProblemBundle/Controller/"
        type:     annotation

    phlexible_queue:
        resource: "@PhlexibleQueueBundle/Controller/"
        type:     annotation

    phlexible_search:
        resource: "@PhlexibleSearchBundle/Controller/"
        type:     annotation

    phlexible_security:
        resource: "@PhlexibleSecurityBundle/Controller/"
        type:     annotation

    phlexible_siteroots:
        resource: "@PhlexibleSiterootBundle/Controller/"
        type:     annotation

    phlexible_tasks:
        resource: "@PhlexibleTaskBundle/Controller/"
        type:     annotation

    phlexible_teasers_catch:
        resource: "@PhlexibleTeaserBundle/Controller/CatchController.php"
        type:     annotation

    phlexible_teasers_layout:
        resource: "@PhlexibleTeaserBundle/Controller/LayoutController.php"
        type:     annotation

    phlexible_tree:
        resource: "@PhlexibleTreeBundle/Controller/"
        type:     annotation

    phlexible_users:
        resource: "@PhlexibleUserBundle/Controller/"
        type:     annotation

Security
~~~~~~~~

Add a new provider, encoder and firewall configuration to ``app/config/security.yml``:

.. code-block:: yaml

    providers:
        ...

        phlexible_user:
            id: phlexible_user.user_manager

    encoders:
        ...

        Phlexible\Bundle\UserBundle\Entity\User:
            algorithm: md5
            encode_as_base64: false
            iterations: 1

    firewalls:
        ...

        phlexible_login:
            pattern:   ^/admin/login$
            anonymous: true

        phlexible:
            pattern:    ^/admin
            form_login:
                provider:      phlexible_user
                csrf_provider: form.csrf_provider
                login_path:    security_login
                check_path:    security_check
            logout:
                path:     security_logout
                target:   /
            anonymous:    true
            switch_user:
                role:     users_impersonate
            remember_me:
                key:      %secret%
                lifetime: 604800
                path:     /
                domain:   ~

Add path' for backend access control:

.. code-block:: yaml

    access_control:
        - { path: ^/admin/security/login$, roles: IS_AUTHENTICATED_ANONYMOUSLY }
        - { path: ^/admin/security/asset, roles: IS_AUTHENTICATED_ANONYMOUSLY }
        - { path: ^/admin/security/reset, roles: IS_AUTHENTICATED_ANONYMOUSLY }
        - { path: ^/admin, roles: login }

Setup
-----

After you finished the general configuration, there are some further setup steps to make phlexible work.

Step 1: Create Database Schema
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

phlexible  brings some database tables which you can install by executing the following command:

.. code-block:: bash

    $ php app/console doctrine:schema:update --force

.. note::

    You need to be in your project root to execute the command. It's the doctrine `standard
    command for creating the database schema`_ in Symfony2.

.. _docs-add-backend-user:

Step 2: Add Backend User
~~~~~~~~~~~~~~~~~~~~~~~~

Now that the database is set up, you have to add a backend user and add
a role to this user.

.. hint::

    phlexible  uses the `FOSUSerBundle`_ to handle user management. If you
    are familiar with this bundle, the user creation will be nothing special.

Add user
........

.. code-block:: bash

    $ php app/console fos:user:create testuser test@example.com p@ssw0rd

This command adds a user with username ``testuser``, email ``test@example.com`` and
password ``p@ssw0rd``. If any of the required arguments are not passed to the command,
an interactive prompt will ask you to enter them.

Promote User
............

To add a role to the user you just created, use the following command:

.. code-block:: bash

    $ php app/console fos:user:promote testuser SUPERADMIN

This command promotes the user ``testuser`` with the role ``SUPERADMIN``.
Another role you can use at this point is ``DEVELOPER``.

Step 3: Add Media Root Folder
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To work with the Mediamanager in phlexible, there has to be a root folder. That folder
can be created by executing the command:

.. code-block:: bash

    $ php app/console media-manager:init

Finish Installation
-------------------

When everything is configured and set up, open your browser and request the backend
by typing in the following url:

.. code-block:: text

    http://project.dev/app_dev.php/admin

phlexible  will prompt you for your username and password that you have set
:ref:`earlier in the setup <docs-add-backend-user>`.

Beginning Development
---------------------

Now that you have a fully-functional phlexible application, you can begin development!

Be sure to also check out the :doc:`Cookbook </cookbook/index>` which contains a wide variety
about solving problems with phlexible.

.. _`http://symfony.com/doc/current/book/installation.html`: http://symfony.com/doc/current/book/installation.html
.. _`phlexible Composer Repository`: https://packages.brainbits.net/phlexible-bundles/
.. _`standard command for creating the database schema`: http://symfony.com/doc/current/book/doctrine.html#creating-the-database-tables-schema
.. _`FOSUSerBundle`: https://github.com/FriendsOfSymfony/FOSUserBundle
