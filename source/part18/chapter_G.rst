.. _chapter_G:

WADL JSON Representation
========================

.. _sect_G.1:

Introduction
------------

While the WADL specification only specifies an XML encoding for the WADL
payload, the data structure can easily be represented using JSON.
Additionally, conversion from XML to JSON and vice-versa can be done in
a lossless manner.

.. _sect_G.2:

XML Elements
------------

The JSON encoding of WADL XML elements depends on whether the element
is:

-  a "doc" element

-  an element that is unique within a particular parent element (e.g.,
   "request")

-  an element that can be repeated within a particular parent element
   (e.g., "param")

.. _sect_G.2.1:

Doc Elements
~~~~~~~~~~~~

A "doc" element is represented as an array of objects, where each object
may contain:

-  a "@xml:lang" string

-  a "@title" string

-  a "value" string

Example:

::

   "doc": [ 
           {
               "@xml:lang": "en",
               "value": "Granular cell tumor"
           },
           {
               "@xml:lang": "ja",
               "value": "顆粒細胞腫"
           },
           {
               "@xml:lang": "fr",
               "value": "Tumeur à cellules granuleuses"
           }
   ]

.. _sect_G.2.2:

Unique Elements
~~~~~~~~~~~~~~~

All unique WADL XML elements are represented as an object whose name is
the name of the XML element and where each member may contain:

-  a "@{attribute}" string for each XML attribute of the name
   {attribute}

-  a child object for each child element that must be unique

-  a child array for each child element that may not be unique

Example:

::

   "request": {
               "param": [ ... ],
               "representation": [ ... ]
   }

.. _sect_G.2.3:

Repeatable Elements
~~~~~~~~~~~~~~~~~~~

All repeatable WADL XML elements are represented as an array of objects
whose name is the name of the XML element and where each may contain:

-  a "@{attribute}" string for each XML attribute of the name
   {attribute}

-  a child object for each child element that must be unique

-  a child array for each child element that may not be unique

Example:

::

   "param": [ 
           {
               "@name": "Accept",
               "@style": "header"
           },
           {
               "@name": "Cache-control",
               "@style": "header"
           }
       ]

