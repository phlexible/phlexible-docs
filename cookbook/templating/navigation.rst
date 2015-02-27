.. index::
    single: Templating; Implementing Navigation

Implementing Navigation
=======================

Variables
---------

``navigation``
    **type**: ``array``

Contains all navigation keys from siteroot.

``node.node.title``
    **type**: ``string``

Navigation title from node.

``node.active``
    **type**: ``boolean``

``true`` if node is active

Functions
---------

``node.viewable()``
    **type**: ``boolean``

``true`` if navigation item is in navigation, is published and not structure element~


``node.viewableChildren()``
    **types**: ``boolean``

``true`` if node children are in navigation, are published and aren't structure elements

``node_granted(node)``

``true`` if user is authenticated for node


Examples
--------

Simple navigation
~~~~~~~~~~~~~~~~~

.. code-block:: jinja

    {# get all children from navigation with key `main` #}
    {% set items = navigation.main.children %}
    {% if items %}
        <ul>
            {% for item in items %}
                {% if item.viewable %}
                    <li>
                        <a href="{{ url(item) }}">{{ item.node.title|escape }}</a>
                    </li
                {% endif %}
            {% endfor %}
        </ul>
    {% endif %}

Simple navigaton with children
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: jinja

    {# get all children from navigation with key `main` #}
    {% set items = navigation.main.children %}
    {% if items %}
        <ul>
            {% for item in items %}
                {% if item.viewable %}
                    <li>
                        <a href="{{ url(item) }}">{{ item.node.title|escape }}</a>
                        {% if item.viewableChildren and item.active %}
                            {% include "::navigation/simple.html.twig" with {items: item.children} %}
                        {% endif %}
                    </li>
                {% endif %}
            {% endfor %}
        </ul>
    {% endif %}

Simple navigaton with children and role model
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: jinja

    {# get all children from navigation with key `main` #}
    {% set items = navigation.main.children %}
    {% if items %}
        <ul>
            {% for item in items %}
                {% if item.viewable and node_granted(item) %}
                    <li>
                        <a href="{{ url(item) }}">{{ item.node.title|escape }}</a>
                        {% if item.viewableChildren and node_granted(item.children) %}
                            {% include "::navigation/simple.html.twig" with {items: item.children} %}
                        {% endif %}
                    </li>
                {% endif %}
            {% endfor %}
        </ul>
    {% endif %}
