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
    `Installing and Configuring Symfony`_ for details.

After Symfony2 is installed, you can add phlexible by adding several bundles to your ``composer.json`` file.

Step 1: Add Composer repository
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Before you can use the phlexible package or any of its bundles, you have to add
the `phlexible Composer Repository`_. Paste the following into your ``composer.json``:

.. code-block:: yaml

    {
        "repositories": [
            {
                "type": "composer",
                "url": "https://packages.brainbits.net/phlexible-bundles/",
                "options": {
                    "ssl": {
                        "allow_self_signed": "true"
                    }
                }
            }
        ]
    }

Step 2: Download phlexible
~~~~~~~~~~~~~~~~~~~~~~~~~~

Open a command console, enter your project directory and execute the following command to download the latest stable version of this bundle:

.. code-block:: bash

    $ composer require "phlexible/phlexible=dev-master"

This command requires you to have Composer installed globally, as explained in the `installation chapter`_ installation chapter of the Composer documentation. 

Step 3: Enable phlexible bundles
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

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
                // ...

                // required phlexible dependencies
                new Igorw\FileServeBundle\IgorwFileServeBundle(),
                new Nelmio\ApiDocBundle\NelmioApiDocBundle(),
                new FOS\UserBundle\FOSUserBundle(),
                new Puli\Extension\Symfony\PuliBundle\PuliBundle(),
                new Symfony\Cmf\Bundle\RoutingBundle\CmfRoutingBundle(),

                // phlexible.core
                new Phlexible\Bundle\GuiBundle\PhlexibleGuiBundle(),
                new Phlexible\Bundle\MessageBundle\PhlexibleMessageBundle(),
                new Phlexible\Bundle\QueueBundle\PhlexibleQueueBundle(),
                new Phlexible\Bundle\UserBundle\PhlexibleUserBundle(),
                new Phlexible\Bundle\ProblemBundle\PhlexibleProblemBundle(),
                new Phlexible\Bundle\DashboardBundle\PhlexibleDashboardBundle(),
                new Phlexible\Bundle\SearchBundle\PhlexibleSearchBundle(),
                new Phlexible\Bundle\AccessControlBundle\PhlexibleAccessControlBundle(),
                new Phlexible\Bundle\DataSourceBundle\PhlexibleDataSourceBundle(),

                // phlexible.media
                new Phlexible\Bundle\MediaCacheBundle\PhlexibleMediaCacheBundle(),
                new Phlexible\Bundle\MediaExtractorBundle\PhlexibleMediaExtractorBundle(),
                new Phlexible\Bundle\MediaManagerBundle\PhlexibleMediaManagerBundle(),
                new Phlexible\Bundle\MediaTemplateBundle\PhlexibleMediaTemplateBundle(),
                new Phlexible\Bundle\MediaToolBundle\PhlexibleMediaToolBundle(),
                new Phlexible\Bundle\MediaTypeBundle\PhlexibleMediaTypeBundle(),
                new Phlexible\Bundle\MetaSetBundle\PhlexibleMetaSetBundle(),

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
                new Phlexible\Bundle\TaskBundle\PhlexibleTaskBundle(),

                 new FOS\UserBundle\FOSUserBundle(),
            );
        }
    }

Configuration
-------------

App configuration
~~~~~~~~~~~~~~~~~

phlexible  requires some configuration to be added to app's ``app/config/config.yml`` file:

.. code-block:: yaml

    # activate translator
    framework:
        translator: { fallback: "%locale%" }

    # CMF Routing Bundle
    cmf_routing: ~

    # Igorw File Serve Bundle
    igorw_file_serve:
        factory: php # php
        #factory: sendfile # nginx
        #factory: xsendfile # apache

    # FOS User Bundle
    fos_user:
        db_driver: orm
        firewall_name: phlexible
        user_class: Phlexible\Bundle\UserBundle\Entity\User

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

    phlexible_meta_set:
        languages:
            default: de
            available: en,de

    phlexible_media_cache:
        storages:
            default:
                id: phlexible_media_cache.storage.local
                options:
                    storage_dir: /path/to/mediacache/storage/dir

    phlexible_media_manager:
        volumes:
            default:
                id: 492d88c5-dd48-4d73-b849-1cacc0a80056 # this has to be a generated id
                root_dir: /path/to/mediamanager/root/dir
                quota: 1000000000
                driver: phlexible_media_manager.driver.doctrine

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
            pdf2swf: /path/to/pdf2swf
        poppler:
            pdfinfo: /path/to/pdfinfo
            pdftotext: /path/to/pdftotext
            pdftohtml: /path/to/pdftohtml
        mime:
            file: /path/to/file
        ffmpeg:
            ffprobe: /path/to/ffprobe
            ffmpeg: /path/to/ffmpeg

Parameters
~~~~~~~~~~

Some configuration values should be defined as parameters, since they are dependending on the local environment.
Open ``app/config/parameters.yml`` and set the following values:

.. code-block:: yaml

    tool_pdf2swf: /path/to/pdf2swf
    tool_pdfinfo: /path/to/pdfinfo
    tool_pdftohtml: /path/to/pdftohtml
    tool_file: /path/to/file
    tool_ffprobe: /path/to/ffprobe
    tool_ffmpeg: /path/to/ffmpeg
    media_manager_root_dir: /path/to/project/media/files/
    media_cache_storage_dir: /path/to/project/media/frames/

After that, replace these configuration values in ``app/config/config.yml`` with the new parameters:

.. code-block:: yaml

    phlexible_media_cache:
        storages:
            default:
                options:
                    storage_dir: %media_cache_storage_dir%
    phlexible_media_manager:
        volumes:
            default:
                root_dir: %media_manager_root_dir%
    phlexible_media_tool:
        swftools:
            pdf2swf: %tool_pdf2swf%
        poppler:
            pdfinfo: %tool_pdfinfo%
            pdftotext: %tool_pdftotext%
            pdftohtml: %tool_pdftohtml%
        mime:
            file: %tool_file%
        ffmpeg:
            ffprobe: %tool_ffprobe%
            ffmpeg: %tool_ffmpeg%

Routing
~~~~~~~

To make the backend routes available, you have to add a resource to ``app/config/routing.yml``:

.. code-block:: yaml

    phlexible_frontendmedia_media:
        resource: "@PhlexibleFrontendMediaBundle/Controller/MediaController.php"
        type:     annotation

    phlexible_teaser_render:
        resource: "@PhlexibleTeaserBundle/Controller/RenderController.php"
        type:     annotation
        
    admin:
        resource: admin_routing.yml
        prefix:   /admin

After that, add a new file ``app/config/admin_routing.yml`` and add the following lines:

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

    phlexible_mediatypes:
        resource: "@PhlexibleMediaTypeBundle/Controller/"
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

    phlexible_siteroots:
        resource: "@PhlexibleSiterootBundle/Controller/"
        type:     annotation

    phlexible_tasks:
        resource: "@PhlexibleTaskBundle/Controller/"
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

        Phlexible\Bundle\UserBundle\Entity\User: sha512

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
                login_path:    fos_user_security_login
                check_path:    fos_user_security_check
            logout:
                path:     fos_user_security_logout
                target:   /
            anonymous:    true
            switch_user:
                role:     users_impersonate
            remember_me:
                key:      %secret%
                lifetime: 604800
                path:     /
                domain:   ~

Add path for backend access control:

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

    phlexible uses the `FOSUSerBundle`_ to handle user management. If you
    are familiar with this bundle, the user creation will be nothing special.

Add user
........

.. code-block:: bash

    $ php app/console fos:user:create admin admin@example.com p@ssw0rd

This command adds a user with username ``admin``, email ``admin@example.com`` and
password ``p@ssw0rd``. If any of the required arguments are not passed to the command,
an interactive prompt will ask you to enter them.

Promote User
............

To add a role to the user you just created, use the following command:

.. code-block:: bash

    $ php app/console fos:user:promote admin ROLE_SUPER_ADMIN

This command promotes the user ``admin`` with the role ``ROLE_SUPER_ADMIN``.

Step 3: Add Media Root Folder
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To work with the Mediamanager in phlexible, there has to be a root folder. That folder
can be created by executing the command:

.. code-block:: bash

    $ php app/console media-manager:init default

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

.. _`installation chapter`: https://getcomposer.org/doc/00-intro.md
.. _`Installing and Configuring Symfony`: http://symfony.com/doc/current/book/installation.html
.. _`phlexible Composer Repository`: https://packages.brainbits.net/phlexible-bundles/
.. _`standard command for creating the database schema`: http://symfony.com/doc/current/book/doctrine.html#creating-the-database-tables-schema
.. _`FOSUSerBundle`: https://github.com/FriendsOfSymfony/FOSUserBundle
