.. index::
    single: Book; Messages

Messages
========

Messages are human readable entries that are written by most of the phlexible components.
Filters are a defined set of rules that can match messages.
Subscriptions bind filters to trigger actions for messages that match the filter, like sending out a mail, or a daily digest mail.

Message Manager
---------------

All access to messages is done via the message manager.

.. code-block:: php

    $messageManager = $this->get('phlexible_message.message_manager');
    
Filter Manager
--------------

All access to filters is done via the filter manager.

.. code-block:: php

    $filterManager = $this->get('phlexible_message.filter_manager');
    
Subscription Manager
--------------------

All access to subscriptions is done via the subscription manager.

.. code-block:: php

    $subscriptionManager = $this->get('phlexible_message.subscription_manager');
    
Message Poster
--------------

The message poster is a service that you can use to send custom messages.

.. code-block:: php

    $messagePoster = $this->get('phlexible_message.message_poster');

    $message = Message::create('My message subject', 'My message body');

    $messagePoster->post($message);
    
