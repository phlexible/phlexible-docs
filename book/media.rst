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

Loading Files/Folders
---------------------

Now that you have access to the media site, you can call some helpful methods
to get files and/or folders::

    // find files
    $file = $site->findFile($id);
    $file = $site->findFileByPath('/some/path/to/file');
    // ...

    // find folders
    $folder = $site->findFolder($id);
    $folder = $site->findFolderByFileId($fileId);
    // ...

There are more methods in the media site (`Site`_) to help you find the object you need.

.. _docs-create-folder:

Create Folder
-------------

Creating a folder is very simple::

    $parentFolder = $site->findFolder($parentId);
    $folder = $site->createFolder($parentFolder, 'Folder Name', new AttributeBag(), $userId);

The ``AttributeBag`` can contain an array of attributes that you can define by yourself. They are
stored serialized in the database. The ``userId`` is the creator of the folder.

Create File
-----------

To create a file, you have to find or :ref:`create a folder <docs-create-folder>` where the file will be put
into. Afterwards you can simply call the ``createFile()`` method::

    // find folder
    $folder = $site->findFolder($folderId);

    // or create folder ... see above

    $file = $site->createFile($folder, $fileSource, new AttributeBag(), $userId);

The ``fileSource`` has to be one of the following:

- ``CreateFileSource``: Creates an empty file
- ``FilesystemFileSource``: Creates file from filesystem
- ``StreamFileSource``: Creates a file stream
- ``UploadedFileSource``: Creates file source from uploaded file

Just like the ``AttributeBag`` for the folder creation, you can define an array
with file attributes by yourself. The ``userId`` is the creator of the file.

.. _Site: http://link-to-api.phlexible.net/Site
