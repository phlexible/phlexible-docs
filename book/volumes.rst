.. index::
    single: Volumes

Volumes
=======

Working with media files and folders is a big part of phlexible.
They are stored in the media manager of the application and have one thing
in common: The volumes!

Volume
------

A volume is a hierarchical set of folder and files, which can be accessed through the (`Volume`_) object.
To get a volume, you need to retrieve it through the volume manager.

.. code-block:: php

    $volumeManager = $this->get('phlexible_media_manager.volume_manager');
    $volume = $volumeManager->getVolumeById($siteId);

.. hint::

    The volume id can be found in ``app/config/config.yml``.

Retrieving Files
----------------

Now that you have access to a volume, you can call several methods to retrieve files:

    // find files
    $file = $volume->findFile($id);
    $file = $volume->findFileByPath('/some/path/to/file');
    $files = $volume->findFilesByFolder($folder);

There are more file related methods in the volume (`Volume`_) to help you find the file you want to retrieve.

Retrieving Folders
------------------

Same goes for folders:

    // find folders
    $folder = $volume->findFolder($id);
    $folders = $volume->findFoldersByParentFolder($parentFolder);

There are more folder related methods in the volume (`Volume`_) to help you find the folder you want to retrieve.

.. _docs-create-folder:

Creating Folders
----------------

To create a folder, call the ``createFolder()`` method on the (`Volume`_):

    $parentFolder = $volume->findFolder($parentoId);
    $folderName = 'Test Folder';
    $attributes = array();
    $userId = $this->getUser()->getId();
    $folder = $volume->createFolder($parentFolder, $folderName, $attributes, $userId);

* The ``$parentFolder`` argument is the parent folder under which the new folder will be created.
* The ``$folderName`` argument is the name of the new folder.
* The ``$attributes`` argument is a simple array with attributes that you can define for the folder. 
* The ``$userId`` argument is the creator of the folder.

Creating Files
--------------

To create a file, call the ``createFile()`` method on the (`Volume`_), with the parent folder in which the new file will created. 
Afterwards you can simply call the ``createFile()`` method::

    $folder = $volume->findFolder($folderId);
    $fileSource = new FileSource();
    $attributes = array();
    $userId = $this->getUser()->getId();

    $file = $volume->createFile($folder, $fileSource, array(), $userId);

* The ``$parentFolder`` argument is the parent folder under which the new folder will be created.
* The ``$fileSource`` argument is the source of the new file. See below for more detailled information.
* The ``$attributes`` argument is a simple array with attributes that you can define for the file. 
* The ``$userId`` argument is the creator of the folder.

The ``$fileSource`` has to be of the Interface ``FileSourceInterface``, phlexible provides the following default file sources:

- ``CreateFileSource``: Represents an empty file
- ``FilesystemFileSource``: References a file in the filesystem
- ``StreamFileSource``: References a stream
- ``UploadedFileSource``: References an uploaded file

Updating Files
--------------

Todo

Updating Folders
----------------

Todo

Deleting Files
--------------

Todo

Deleting Folders
----------------

Todo

.. _Volume: http://link-to-api.phlexible.net/Volume
