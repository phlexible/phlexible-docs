.. index::
   single: Templating; Creating links from phlexible fields

Creating links from phlexible fields
====================================

With phlexible link field you can create different links to external or internal pages.

Set link from link field
-------------------------

.. code-block:: jinja

	{% set link = content.value('cm_link_url') %}
	{% if link %}
	    <a href="{{ url(link) }}">Absolute link with hostname</a>
	    <a href="{{ path(link) }}">Absolute link without hostname</a>
    	{% endif %}

This example retrieves a link value from :ref:`variables_content` and uses the :ref:`extensions_url` and :ref:`extensions_path` functions to render different link paths.


Set title depending on link type
--------------------------------

.. code-block:: jinja

    {% if link %}
	{# set title depending which type is link #}
	{% set defaultTitle %}
	    {%- if link.value.type == "external" %}{{ link.value.url|replace({"http://":""}) }}<span class="hideme"> – {{ "accessibility.target-blank"|trans }}</span>{% endif %}

	    {%- if link.value.type == "internal" or link.value.type == "intrasiteroot" -%}
		{% set itemNode = tree_node(link.value.tid) %}
		{{- itemNode.node.title -}} {# get title from internal urls #}
	    {%- endif %}
	{% endset %}

	<a href="{{ url(link) }}">{{ defaultTitle }}</a>
    {% endif %}

This example uses ``link.value.type`` to determine the link type.

For external links, the url from ``link.value.url`` is used, without protocol.

For internal links the referenced node is retrieved via the :ref:`extensions_tree_node` function and the ``link.value.tid`` value, using title of the node as link title.

Set class depending on link type
--------------------------------

.. code-block:: jinja

    {% if link %}
	{% set linkClass %}
	    {%- if link.value.type == "external" or link.value.type  == "intrasiteroot" %} external{%- endif -%}
	    {%- if link.value.type == "internal" %} internal{%- endif -%}
	    {%- if link.value.type == "mailto" %} mail{%- endif -%}
	{% endset %}

	<a href="{{ url(link) }}" class="{{ linkClass }}">Link with type dependent class</a>
    {% endif %}

This example uses the ``link.value.type`` to build a type dependent class name.

Set target for external links
-----------------------------

.. code-block:: jinja

    {% if link %}

	{# set attribute target="_blank" for external urls #}
	{% set target %}
	    {%- if link.value.type  == "external" %} target="_blank"{%- endif -%}
	{% endset %}

	<a href="{{ url(link) }}" {{ target }}>Link with target</a>
    {% endif %}

This example uses the ``link.value.type`` to render a target attribute for external links.