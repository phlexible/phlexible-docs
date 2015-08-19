.. index::
   single: Templating; Creating links from phlexible fields

Creating links from phlexible fields
====================================

With phlexible link field you can create different links to external or internal pages.

Variables
---------

Functions
---------

``url(node)``
~~~~~~~~~~~~~

``node``
    **type**: ``object``

Creates url from ``node``.

``tree_node(node)``
~~~~~~~~~~~~~~~~~~~

``node``
    **type**: ``object``

Returns tree node date from ``node``.

Examples
--------

Set classes, if link is external or internal
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: jinja

    {% if link %}
	{% set linkClass %}
	    {%- if link.value.type == "external" or link.value.type  == "intrasiteroot" %} external{%- endif -%}
	    {%- if link.value.type == "internal" %} internal{%- endif -%}
	    {%- if link.value.type == "mailto" %} mail{%- endif -%}
	{% endset %}

	{# set attribute target="_blank" for external urls #}
	{% set target %}
	    {%- if link.value.type == "external" or link.value.type  == "intrasiteroot" %} target="_blank"{%- endif -%}
	{% endset %}
	{# set title depending which type has link #}
	{% set defaultTitle %}
	    {%- if link.value.type == "external" %}{{ link.value.url|replace({"http://":""}) }}<span class="hideme"> – {{ "accessibility.target-blank"|trans }}</span>{% endif %}

	    {%- if link.value.type == "internal" or link.value.type == "intrasiteroot" -%}
		{% set itemNode = tree_node(link.value.tid) %}
		{{- itemNode.node.title -}} {# get title from internal urls #}
	    {%- endif %}
	{% endset %}

	<a href="{{ url(link) }}" class="{{ linkClass }}" {{ target }}>{{ defaultTitle }}</a>
    {% endif %}

``link.value.type``
    **type**: ``string`` **values**: ``"external"``, ``"internal"``, ``"intrasiteroot"``, ``"mailto"``