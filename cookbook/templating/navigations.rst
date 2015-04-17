.. index::
    single: Templating; Implementing Navigation

Implementing Navigations
========================

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
