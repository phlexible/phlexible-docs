.. index::
    single: Book; Users

Users
=====

The PhlexibleUserBundle incorporates the `FOSUSerBundle`_ and extends it with additional functionality like groups, providing a complete user management system.

User Manager
------------

All access to users is done via the user manager.

.. code-block:: php

    $userManager = $this->get('phlexible_user.user_manager');
        
Retrieving Users
----------------

To fetch a user by id, use the ``find()`` method on the user manager:

.. code-block:: php

    // find user by id
    $user = $userManager->find($id);

The user manager also provides additional methods for finding users:

.. code-block:: php

    // find users by criteria
    $users = $userManager->findBy(array('enabled' => 0));

    // find a user by criteria
    $user = $userManager->findOneBy(array('email' => 'john.doe@example.com'));

    // find all users
    $users = $userManager->findAll();

Updating Users
--------------

To update an user, call the ``updateUser()`` method on the user manager:

.. code-block:: php

    // for an existing user
    $user = $userManager->find(1);

    // ... or for a new user
    $user = new \Phlexible\Bundle\UserBundle\Entity\User();

    $user->setFirstname('John');
    $user->setLastname('Doe');

    // update user
    $userManager->updateUser($user);

Deleting Users
--------------

To delete an user, call the ``deleteUser()`` method on the user manager:

.. code-block:: php

    $user = $userManager->find(1);

    // delete user
    $userManager->deleteUser($user);

Group Manager
-------------

All access to groups is done via the group manager.

.. code-block:: php

    $groupManager = $this->get('phlexible_user.group_manager');
        
Retrieving Groups
-----------------

To fetch a group by id, use the ``find()`` method on the group manager:

.. code-block:: php

    // find group by id
    $group = $groupManager->find($id);

The group manager also provides additional methods for finding groups:

.. code-block:: php

    // find groups by criteria
    $groups = $groupManager->findBy(array('name' => 'testgroup'));

    // find a group by criteria
    $group = $groupManager->findOneBy(array('name' => 'testgroup'));

    // find all groups
    $groups = $groupManager->findAll();

Updating Groups
---------------

To update a group, call the ``updateGroup()`` method on the group manager:

.. code-block:: php

    // for an existing group
    $group = $groupManager->find(1);

    // ... or for a new group
    $group = new \Phlexible\Bundle\UserBundle\Entity\Group();

    $group->setName('testgroup');

    // update group
    $groupManager->updateGroup($group);

Deleting Groups
---------------

To delete a group, call the ``deleteGroup()`` method on the group manager:

.. code-block:: php

    $group = $groupManager->find(1);

    // delete group
    $groupManager->deleteGroup($group);

.. _`FOSUSerBundle`: https://github.com/FriendsOfSymfony/FOSUserBundle
.. _`Query Builder`: http://docs.doctrine-project.org/projects/doctrine-orm/en/latest/reference/query-builder.html
