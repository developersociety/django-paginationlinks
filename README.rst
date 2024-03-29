Django Pagination Links
=======================

Small package for creating a list of page links from a Django paginator object,
similar in style to the Django admin - showing the start and end pages, but
only showing a limited list of pages in the middle.

Deprecated
----------

As of Django 3.2 - the Paginator class now supports
`elided page ranges <https://docs.djangoproject.com/en/3.2/releases/3.2/#pagination>`_.

Installation
------------

Using pip_:

.. _pip: https://pip.pypa.io/

.. code-block:: console

    $ pip install django-paginationlinks


Edit your Django project's settings module, and add ``paginationlinks``:

.. code-block:: python

    INSTALLED_APPS = [
        # ...
        'paginationlinks',
    ]

Usage
-----

Load the template tag:

.. code-block::

    {% load pagination_links %}

Typical usage, which shows 1 page on each end, and 1 on each side of the current page:

.. code-block::

    {% get_pagination_links paginator page_obj as pagination_links %}

However the number of pages on each side can be customised, as well as how many pages at the end -
both are optional arguments:

.. code-block::

    {% get_pagination_links paginator page_obj on_each_side=1 on_ends=2 as pagination_links %}

A more fully featured example for a site:

.. code-block::

    {% load pagination_links %}

    {% if page_obj.has_other_pages %}
        {% get_pagination_links paginator page_obj as pagination_links %}
        <ul>
            {% for page_num in pagination_links %}
                {% if page_num.is_current %}
                    <li class="current">{{ page_num.number }}</li>
                {% elif page_num.is_filler %}
                    <li class="filler">—</li>
                {% else %}
                    <li><a href="?page={{ page_num.number }}">{{ page_num.number }}</a></li>
                {% endif %}
            {% endfor %}
        </ul>
    {% endif %}
