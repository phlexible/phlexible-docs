.. index::
    single: Media

Media
=====

Working with media files and folders is a big part of phlexible.
They are stored in the media manager of the application and have one thing
in common: The media site!

Media Site
----------

The media site can be seen as a root (folder) in the media manager.
It holds the files and folders and is responsible for loading the desired
data. You can use the media site manager for this kind of operations.
Simply grab it from the container::

    public function listAction()
    {
        $mediaSiteManager = $this->get('phlexible_media_site.site_manager');
        $site = $mediaSiteManager->getSiteById($siteId);
    }

.. hint::

    The site id can be found in ``app/config/config.yml``.

Loading Files
-------------

Now that you have access to the media site, you can call some helpful methods
to get files and/or folders::

    // find files
    $file = $site->findFile($id);
    $file = $site->findFileByPath('/some/path/to/file');

    // find folders
    $folder = $site->

As you can see ...
