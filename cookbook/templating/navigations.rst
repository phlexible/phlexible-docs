.. index::
    single: Templating; Implementing Navigation

Working with Navigations
========================

.. _cookbook_templating_navigations_simple:

How to create a simple navigation
---------------------------------

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

This example retrieves the children navigation ``main`` from the :ref:`variables_navigations` twig variable, and loops over them. Each child ``item`` is a :ref:`variables_treeContext`, and is only display if it is ``viewable``.

.. _cookbook_templating_navigations_children:

How to create a recursive navigaton
-----------------------------------

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

This example retrieves the navigation ``side`` from the :ref:`variables_navigations` twig variable, and loops over the children. Each child ``item`` is a :ref:`variables_treeContext`, and is only displayed if it is ``viewable``. If the child ``item`` has ``viewableChildren``, and is ``active`` (in the path to the current node), the :ref:`cookbook_templating_navigations_simple` is included.

.. _cookbook_templating_navigations_access_check:

How to create a navigaton with access checks
--------------------------------------------

.. code-block:: jinja

    {# get all children from navigation with key `meta` #}
    {% set items = navigation.meta.children %}
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

This example retrieves the navigation ``meta`` from the :ref:`variables_navigations` twig variable, and loops over the children. Each child ``item`` is a :ref:`variables_treeContext`, and is only displayed if it is ``viewable``. If the child ``item`` has ``viewableChildren``, and access to the ``item`` is granted (``node_granted``), the :ref:`cookbook_templating_navigations_simple` is included.
