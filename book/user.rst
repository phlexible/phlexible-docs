.. index::
    single: Media

User
====

This article focuses on how to handle user data in phlexible. The PhlexibleUserBundle
extends the `FOSUSerBundle`_ and additionally brings group handling to work with.

Fetching User Object
--------------------

Fetching a user object from the database is very easy. For example, suppose
you've configured a route to load a specific ``User`` based on its ``id`` value::

    public function loadAction($id)
    {
        $user = $this->get('phlexible_user.user_manager')->find($id);

        // ... do something with the user object
    }

As you can see, phlexible ships with a user manager. Once you have the
user manager, you have access to all sorts of helpful methods::

    $userManager = $this->get('phlexible_user.user_manager');

    // query by the primary key (usually "id")
    $user = $userManager->find($id);

    // find a user by username
    $user = $userManager->findByUsername('john.doe');

    // find a user by criteria
    $user = $userManager->findOneBy(array('email' => 'john.doe@example.com'));

    // find all users
    $users = $userManager->findAll();

    // find a group of users based on criteria
    $users = $userManager->findBy(array('enabled' => 1));

    // get logged in users
    $users = $userManager->findLoggedInUsers();

.. note::

    Of course, you can also issue complex queries. Just use the
    Doctrine `Query Builder`_ for that.

Creating/Updating User Object
-----------------------------

To create or update a user, you need to fetch (for updating) or instantiate (for creating)
a user object and call the desired setters. After that, you can call the ``updateUser()``
method to save your changes::

    // for editing
    $user = $userManager->find(1);

    // for creating
    $user = $userManager->create();

    // example -> change firstname & lastname
    $user->setFirstname('John');
    $user->setLastname('Doe');

    // ...

    // save changes
    $userManager->updateUser($user);

Deleting User Object
--------------------

Deleting a user involves just three steps:

#. fetching object of user that will be deleted
#. fetching object of user that is successor
#. call deleteUser()

.. code-block:: php

    $deleteUser = $userManager->find(1);
    $successor = $userManager->find(2);

    $userManager->deleteUser($deleteUser, $successor);

.. _`FOSUSerBundle`: https://github.com/FriendsOfSymfony/FOSUserBundle
.. _`Query Builder`: http://docs.doctrine-project.org/projects/doctrine-orm/en/latest/reference/query-builder.html
