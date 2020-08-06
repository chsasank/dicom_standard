.. _chapter_7:

Overview of DICOM Web Services (Informative)
============================================

.. _sect_7.1:

DICOM Web Service Types
-----------------------

This Part of the Standard defines DICOM Web Services. Each service
allows a user agent to interact with an origin server to manage a set of
DICOM Resources. Each DICOM Web Service operates on a set of resources
and defines a set of Transactions that operate on those resources. All
Transactions are defined in terms of HTTP request/response message
pairs.

When used in this Part of the Standard, the term HTTP refers to the
family of HTTP protocols including: HTTP/1.1, HTTPS/1.1, HTTP/2, and
HTTPS/2, as defined by the relevant IETF RFCs, but does not include
HTTP/1.0 or HTTPS/1.0. The HTTP standards are normative for all aspects
of HTTP message format and transmission.

There are two general types of DICOM Web Services: URI and RESTful. This
distinction is based on the type of web service protocol used to specify
resources and transactions.

.. _sect_7.1.1:

URI Web Service
~~~~~~~~~~~~~~~

The URI Web Service retrieves representations of its resources, those
resources being Composite SOP Instances (Instance). The URI service
defines two transactions that retrieve Instances in different media
types. All URI transactions use the query component of the URI in the
request message to specify the transaction.

The functionality of the URI Web Service Transactions is similar to, but
more limited than, the Retrieve Transaction of the Studies Web Service.

.. _sect_7.1.2:

RESTful Web Services and Resources
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Each RESTful Web Service defines the set of resources, and the
transactions that can be applied to those resources.

The defined RESTful Web Services are:

Studies Web Service
   Enables a user agent to manage Studies stored on an origin server.

Worklist Web Service
   Enables a user agent to manage the Worklist containing Workitems
   stored on an origin server.

Non-Patient Instance Web Service
   Enables a user agent to manage Non-Patient Instances, e.g., Color
   Palettes, stored on an origin server.

.. _sect_7.2:

Resources, Representations, and Target URIs
-------------------------------------------

In RESTful Web Services, a resource is an abstract object with a type,
associated data, relationships to other resources,and a set of methods
that operate on it. Resources are grouped into collections. Collections
are themselves resources as well. Each collection is unordered and
contains only one type of resource. Collections can exist globally, at
the top level of an API, but can also be contained inside a resource. In
the latter case, we refer to these collections as sub-collections.
Sub-collections usually express some kind of "contained in"
relationship.

.. _sect_7.2.1:

DICOM Restful Resources
~~~~~~~~~~~~~~~~~~~~~~~

The DICOM Resources defined in this Part of the Standard are typically
either a DICOM Web Services or DICOM Information Objects. Examples
include Studies, Series, Instances, Worklists, and Workitems.

DICOM Resources are grouped into collections and hierarchies. The
following resources are examples of collections:

============= =========================
Resource Path Contents
============= =========================
/studies      A collection of Studies.
/series       A collection of Series.
/instance     A collection of Instance.
/frames       A sequence of Frames.
============= =========================

The following resources are examples of hierarchies:

+----------------------------------+----------------------------------+
| /studies/{study}/series          | Contains a collection of Series. |
+----------------------------------+----------------------------------+
| /studies/{                       | Contains a collection of         |
| study}/series/{series}/instances | Instances.                       |
+----------------------------------+----------------------------------+
| /studies/{study}/series/{ser     | Contains a sequence of frames.   |
| ies}/instances/{instance}/frames |                                  |
+----------------------------------+----------------------------------+

A DICOM Web Service origin server manages a collection of resources.
This might not be done directly; for example, an origin server could act
as a proxy, converting RESTful requests into DIMSE requests, and DIMSE
responses into RESTful responses.

Resources are typically created and/or accessed by user agents.

.. _sect_7.2.2:

Representations
~~~~~~~~~~~~~~~

A resource is an abstract concept that is made concrete by a
representation, which is a data object encoded in an octet-stream. For
example, a DICOM Study (abstract) might be represented by a sequence of
octets encoded in DICOM Media Type. See `DICOM Media Types and Media
Types For Bulkdata <#sect_8.7.3>`__.

A media type describes the format or encoding of a representation.
Examples of media types are application/dicom, application/dicom+json,
image/jpeg, and text/html.

.. _sect_7.2.3:

Target URIs
~~~~~~~~~~~

Resources are identified by URIs. Each service defines the resources
that it manages and the format of the URIs used to reference those
resources. The format of URIs is defined using URI Templates. See
`biblioentry_title <#biblio_RFC_6570>`__.

