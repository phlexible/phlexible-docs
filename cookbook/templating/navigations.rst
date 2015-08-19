.. index::
    single: Templating; Implementing Navigation

Implementing Navigations
========================

Examples
--------

.. _cookbook_templating_navigations_simple:

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

This example retrieves the children navigation ``main`` from the :ref:`variables_navigations` twig variable, and loops over them. Each child node is a :ref:`variables_treeContext`, and is only display if it is ``viewable``.

.. _cookbook_templating_navigations_children:

Navigaton with children
~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: jinja

    {# get all children from navigation with key `side` #}
    {% set items = navigation.side.children %}
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

This example retrieves the navigation ``side`` from the :ref:`variables_navigations` twig variable, and loops over the children. Each child ``item`` is a :ref:`variables_treeContext`, and is only display if it is ``viewable``. If the child ``item`` has ``viewableChildren``, and is ``active`` (in the path to the current node), the :ref:`cookbook_templating_navigations_simple` is included.

.. _cookbook_templating_navigations_access_check:

Navigaton with access checks
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

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

This example retrieves the navigation ``side`` from the :ref:`variables_navigations` twig variable, and loops over the children. Each child ``item`` is a :ref:`variables_treeContext`, and is only display if it is ``viewable``. If the child ``item`` has ``viewableChildren``, and access to the ``item`` is granted (``node_granted``), the :ref:`cookbook_templating_navigations_simple` is included.
