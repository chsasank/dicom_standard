.. _chapter_12:

Non-Patient Instance Service and Resources
==========================================

.. _sect_12.1:

Overview
--------

The Non-Patient Instance (NPI) Storage Service enables a user agent to
retrieve, store, and search an origin server for instances that are not
related to a patient.

An NPI Storage Service manages a collection of resources belonging to
the categories specified in `table_title <#table_12.1.1-1>`__.

All NPI Storage Service origin servers shall support the Retrieve
Capabilities, Retrieve, and Search transactions. Support for the Store
transaction is optional. All NPI Storage Service user agents support one
or more of the Retrieve Capabilities, Retrieve, Store, or Search
transactions.

.. _sect_12.1.1:

Resource Descriptions
~~~~~~~~~~~~~~~~~~~~~

An NPI Service manages resources from the same NPI Category. Target URIs
have the following templates:

::

   /{npi-name}
   /{npi-name}/{uid}

Where

::

   npi-name    = "color-palettes"
               / "defined-procedure-protocols"
               / "hanging-protocols"
               / "implant-templates"
   uid         ; is the Unique Identifier of an NPI Instance

`table_title <#table_12.1.1-1>`__ contains the templates for the NPI
Resource Categories.

.. table:: Resource Categories, URI Templates and Descriptions

   +-------------+-------------+-------------+-------------+-------------+
   | Resource    | URI         | Co          | Storage     | Information |
   | Category    | Template    | rresponding | Class       | Model       |
   |             | and         | IOD         |             |             |
   |             | Description |             |             |             |
   +=============+=============+=============+=============+=============+
   | Color       | ::          |             |             |             |
   | Palette     |             |             |             |             |
   |             |             |             |             |             |
   |             |  /color-pal |             |             |             |
   |             | ettes{/uid} |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Defined     | ::          |             |             |             |
   | Procedure   |             |             |             |             |
   | Protocol    |    /        |             |             |             |
   |             | defined-pro |             |             |             |
   |             | cedure-prot |             |             |             |
   |             | ocols{/uid} |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Hanging     | ::          |             |             |             |
   | Protocol    |             |             |             |             |
   |             |    /h       |             |             |             |
   |             | anging-prot |             |             |             |
   |             | ocols{/uid} |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Implant     | ::          |             |             |             |
   | Template    |             |             |             |             |
   |             |    /i       |             |             |             |
   |             | mplant-temp |             |             |             |
   |             | lates{/uid} |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+

The NPI SOP Classes are listed in .

.. _sect_12.1.2:

Common Query Parameters
~~~~~~~~~~~~~~~~~~~~~~~

The origin server shall support Query Parameters as required in
`table_title <#table_12.1.2-1>`__.

The user agent shall supply in the request Query Parameters as required
in `table_title <#table_12.1.2-1>`__.

.. table:: Common Query Parameters

   +----------------+------------+-------+---------+------------------+
   | Name           | Value      | Usage | Section |                  |
   +================+============+=======+=========+==================+
   | Accept         | media-type | M     | M       | `Accept Query    |
   |                |            |       |         | Parameter <#     |
   |                |            |       |         | sect_8.3.3.1>`__ |
   +----------------+------------+-------+---------+------------------+
   | Accept-Charset | charset    | O     | M       | `Character Set   |
   |                |            |       |         | Query            |
   |                |            |       |         | Parameter <#     |
   |                |            |       |         | sect_8.3.3.2>`__ |
   +----------------+------------+-------+---------+------------------+

See also `Header Fields <#sect_8.4>`__.

.. _sect_12.1.3:

Common Media Types
~~~~~~~~~~~~~~~~~~

The origin server shall support the media types listed as Default or
Required in `table_title <#table_12.1.3-1>`__ for all NPI transactions.

.. table:: Default, Required, and Optional Media Types

   +----------------------------+----------+----------------------------+
   | Media Type                 | Usage    | Section                    |
   +============================+==========+============================+
   | application/dicom          | Required | `The application/dicom     |
   |                            |          | Media                      |
   |                            |          | Type <#sect_8.7.3.1>`__    |
   +----------------------------+----------+----------------------------+
   | application/dicom+json     | Default  | `DICOM Metadata Media      |
   |                            |          | Types <#sect_8.7.3.2>`__   |
   +----------------------------+----------+----------------------------+
   | multipart/related;         | Required | `DICOM Metadata Media      |
   | ty                         |          | Types <#sect_8.7.3.2>`__   |
   | pe="application/dicom+xml" |          |                            |
   +----------------------------+----------+----------------------------+

.. _sect_12.2:

Conformance
-----------

An origin server conforming to the NPI Service shall implement the
Retrieve Capabilities Transaction (see `Request <#sect_8.9.1>`__).

The origin server shall support the transactions listed as Required in
`table_title <#table_12.2-1>`__.

.. table:: Required and Optional Transactions

   +-----------------------+----------+----------------------------+
   | Transaction           | Support  | Section                    |
   +=======================+==========+============================+
   | Retrieve Capabilities | Required | `Retrieve Capabilities     |
   |                       |          | Transaction <#sect_8.9>`__ |
   +-----------------------+----------+----------------------------+
   | Retrieve              | Required | `Retrieve                  |
   |                       |          | T                          |
   |                       |          | ransaction <#sect_12.4>`__ |
   +-----------------------+----------+----------------------------+
   | Store                 | Optional | `Store                     |
   |                       |          | T                          |
   |                       |          | ransaction <#sect_12.5>`__ |
   +-----------------------+----------+----------------------------+
   | Search                | Required | `Search                    |
   |                       |          | T                          |
   |                       |          | ransaction <#sect_12.6>`__ |
   +-----------------------+----------+----------------------------+

Implementations shall specify in their Conformance Statement (see ) and
the Retrieve Capabilities Transaction (see `Retrieve Capabilities
Transaction <#sect_8.9>`__ and `Capabilities
Description <#chapter_H>`__):

-  The implementations role: origin server, user agent, or both.

-  The supported resources (IODs) for each role.

In addition, for each supported transaction they shall specify:

-  The supported Query Parameters, including optional Attributes, if any

-  The supported DICOM Media Types

-  The supported character sets (if other than UTF-8)

.. _sect_12.3:

Transactions Overview
---------------------

The NPI Service consists of the transactions listed in
`table_title <#table_12.3-1>`__.

.. table:: NPI Service Transactions

   +----------+---------+----------+----------+----------+----------+
   | Tra      | Method  | Resource | Payload  | Des      |          |
   | nsaction |         |          |          | cription |          |
   +==========+=========+==========+==========+==========+==========+
   | Retrieve | OPTIONS | /        | N/A      | Capa     | R        |
   | Capa     |         |          |          | bilities | etrieves |
   | bilities |         |          |          | Des      | a        |
   |          |         |          |          | cription | des      |
   |          |         |          |          |          | cription |
   |          |         |          |          |          | of the   |
   |          |         |          |          |          | capa     |
   |          |         |          |          |          | bilities |
   |          |         |          |          |          | of the   |
   |          |         |          |          |          | NPI      |
   |          |         |          |          |          | Service, |
   |          |         |          |          |          | i        |
   |          |         |          |          |          | ncluding |
   |          |         |          |          |          | trans    |
   |          |         |          |          |          | actions, |
   |          |         |          |          |          | re       |
   |          |         |          |          |          | sources, |
   |          |         |          |          |          | query    |
   |          |         |          |          |          | par      |
   |          |         |          |          |          | ameters, |
   |          |         |          |          |          | etc.     |
   +----------+---------+----------+----------+----------+----------+
   | Retrieve | GET     | /        | N/A      | Instance | R        |
   |          |         | {npi-nam |          | and/or   | etrieves |
   |          |         | e}/{uid} |          | Status   | an       |
   |          |         |          |          | Report   | I        |
   |          |         |          |          |          | nstance, |
   |          |         |          |          |          | s        |
   |          |         |          |          |          | pecified |
   |          |         |          |          |          | by the   |
   |          |         |          |          |          | Target   |
   |          |         |          |          |          | Resource |
   |          |         |          |          |          | in an    |
   |          |         |          |          |          | Ac       |
   |          |         |          |          |          | ceptable |
   |          |         |          |          |          | DICOM    |
   |          |         |          |          |          | Media    |
   |          |         |          |          |          | Type.    |
   +----------+---------+----------+----------+----------+----------+
   | Store    | POST    | /        | Ins      | Status   | Stores   |
   |          |         | {npi-nam | tance(s) | Report   | one or   |
   |          |         | e}{/uid} |          |          | more     |
   |          |         |          |          |          | DICOM    |
   |          |         |          |          |          | I        |
   |          |         |          |          |          | nstances |
   |          |         |          |          |          | c        |
   |          |         |          |          |          | ontained |
   |          |         |          |          |          | in the   |
   |          |         |          |          |          | request  |
   |          |         |          |          |          | payload, |
   |          |         |          |          |          | in the   |
   |          |         |          |          |          | location |
   |          |         |          |          |          | re       |
   |          |         |          |          |          | ferenced |
   |          |         |          |          |          | by the   |
   |          |         |          |          |          | Target   |
   |          |         |          |          |          | URL.     |
   +----------+---------+----------+----------+----------+----------+
   | Search   | GET     | /{n      | N/A      | R        | Searches |
   |          |         | pi-name} |          | esult(s) | the      |
   |          |         |          |          | and/or   | Target   |
   |          |         | ?{       |          | Status   | Resource |
   |          |         | params*} |          | Report   | for      |
   |          |         |          |          |          | I        |
   |          |         |          |          |          | nstances |
   |          |         |          |          |          | that     |
   |          |         |          |          |          | match    |
   |          |         |          |          |          | the      |
   |          |         |          |          |          | search   |
   |          |         |          |          |          | pa       |
   |          |         |          |          |          | rameters |
   |          |         |          |          |          | and      |
   |          |         |          |          |          | returns  |
   |          |         |          |          |          | a list   |
   |          |         |          |          |          | of       |
   |          |         |          |          |          | matches  |
   |          |         |          |          |          | in an    |
   |          |         |          |          |          | Ac       |
   |          |         |          |          |          | ceptable |
   |          |         |          |          |          | DICOM    |
   |          |         |          |          |          | Media    |
   |          |         |          |          |          | Type.    |
   +----------+---------+----------+----------+----------+----------+

The npi-name specifies the type of resource(s) contained in the payload.

`table_title <#table_12.3-2>`__ summarizes the Target Resources
permitted for each transaction.

.. table:: Resources by Transaction

   ============= ================= ======== ===== ====== ============
   Resource      URI               Retrieve Store Search Capabilities
   ============= ================= ======== ===== ====== ============
   NPI Service   /                                       X
   All Instances /{npi-name}                X     X      
   Instance      /{npi-name}/{uid} X        X            
   ============= ================= ======== ===== ====== ============

.. _sect_12.4:

Retrieve Transaction
--------------------

The Retrieve transaction retrieves the target NPI resource in a DICOM
Media Type.

.. _sect_12.4.1:

Request
~~~~~~~

The request shall have the following syntax:

::

   GET SP /{npi-name}/{uid} SP version CRLF

::

   Accept: 1#dicom-media-type CRLF

::

   *(header-field CRLF)

::

   CRLF

.. _sect_12.4.1.1:

Target Resources
^^^^^^^^^^^^^^^^

The target URI shall reference one of the resources shown in
`table_title <#table_12.4.1-1>`__.

An origin server shall specify all supported npi-names in its
Conformance Statement and in its response to the Retrieve Capabilities
transaction.

.. table:: Retrieve Transaction Resources

   ======== ====================
   Resource URI Template
   ======== ====================
   Instance ::
            
               /{npi-name}/{uid}
   ======== ====================

.. _sect_12.4.1.2:

Query Parameters
^^^^^^^^^^^^^^^^

The user agent shall supply, and the origin server shall support, the
Common Query Parameters in `Common Query Parameters <#sect_12.1.2>`__.

.. _sect_12.4.1.3:

Request Header Fields
^^^^^^^^^^^^^^^^^^^^^

.. table:: Request Header Fields

   +--------+----------------+-------+-------------+----------------+
   | Name   | Values         | Usage | Description |                |
   +========+================+=======+=============+================+
   | Accept | 1#-di          | M     | M           | The Acceptable |
   |        | com-media-type |       |             | Media Types of |
   |        |                |       |             | the response   |
   |        |                |       |             | payload        |
   +--------+----------------+-------+-------------+----------------+

See also `Header Fields <#sect_8.4>`__.

.. _sect_12.4.1.4:

Request Payload
^^^^^^^^^^^^^^^

The request shall have no payload.

.. _sect_12.4.2:

Behavior
~~~~~~~~

The origin server shall try to locate the Target Resource and if found,
return it in an Acceptable DICOM Media Type. See `Acceptable Media
Types <#sect_8.7.5>`__.

A failure response payload may contain a Status Report describing any
failures, warnings, or other useful information.

.. _sect_12.4.3:

Response
~~~~~~~~

The response has the following syntax:

::

   version SP status-code SP reason-phrase CRLF

::

   [Content-Type: dicom-media-type CRLF]

::

   [(Content-Length: uint / Content-Encoding: encoding) CRLF]

::

   [Content-Location: url CRLF]

::

   *(header-field CRLF

::

   CRLF

::

   [payload / status-report]

.. _sect_12.4.3.1:

Status Codes
^^^^^^^^^^^^

`table_title <#table_12.4.3-1>`__ shows some common status codes
corresponding to this transaction. See also `Status Codes <#sect_8.5>`__
for additional status codes.

.. table:: Status Code Meaning

   +------------------+------------------------+------------------------+
   | Status           | Code                   | Meaning                |
   +==================+========================+========================+
   | Success          | 200 (OK)               | The instance was       |
   |                  |                        | successfully           |
   |                  |                        | retrieved.             |
   +------------------+------------------------+------------------------+
   | Failure          | 400 (Bad Request)      | There was a problem    |
   |                  |                        | with the request.      |
   +------------------+------------------------+------------------------+
   | 404 (Not Found)  | The origin server did  |                        |
   |                  | not find a current     |                        |
   |                  | representation for the |                        |
   |                  | Target Resource or is  |                        |
   |                  | not willing to         |                        |
   |                  | disclose that one      |                        |
   |                  | exists. For example,   |                        |
   |                  | an unsupported IOD, or |                        |
   |                  | Instance not on        |                        |
   |                  | server.                |                        |
   +------------------+------------------------+------------------------+
   | 406 (Unsupported | The origin server does |                        |
   |                  | not support any of the |                        |
   | Media Type)      | Acceptable Media       |                        |
   |                  | Types.                 |                        |
   +------------------+------------------------+------------------------+

.. _sect_12.4.3.2:

Response Header Fields
^^^^^^^^^^^^^^^^^^^^^^

.. table:: Response Header Fields

   +----------------+----------------+----------------+----------------+
   | Header Field   | Value          | Origin Server  | Requirements   |
   |                |                | Usage          |                |
   +================+================+================+================+
   | Content-Type   | di             | M              | The media-type |
   |                | com-media-type |                | of the         |
   |                |                |                | response       |
   |                |                |                | payload.       |
   +----------------+----------------+----------------+----------------+
   | Content-Length | uint           | C              | Shall be       |
   |                |                |                | present if no  |
   |                |                |                | content        |
   |                |                |                | encoding has   |
   |                |                |                | been applied   |
   |                |                |                | to the         |
   |                |                |                | payload.       |
   +----------------+----------------+----------------+----------------+
   | Co             | encoding       | C              | Shall be       |
   | ntent-Encoding |                |                | present if a   |
   |                |                |                | content        |
   |                |                |                | encoding has   |
   |                |                |                | been applied   |
   |                |                |                | to the         |
   |                |                |                | payload.       |
   +----------------+----------------+----------------+----------------+

See also `Header Fields <#sect_8.4>`__.

.. _sect_12.4.3.3:

Response Payload
^^^^^^^^^^^^^^^^

A success response shall have a payload containing the DICOM instance
specified by the Target Resource.

A failure response payload may contain a Status Report describing any
failures, warnings, or other useful information.

.. _sect_12.5:

Store Transaction
-----------------

This transaction requests that the origin server store the
representations of the NPIs contained in the request payload so that
they may be retrieved in the future using the SOP Instance UIDs.

.. _sect_12.5.1:

Request
~~~~~~~

The request shall have the following syntax:

::

   POST SP /{npi-name} {/uid} SP version CRLF

::

   Content-Type: dicom-media-type CRLF

::

   (Content-Length: uint / Content-Encoding: encoding) CRLF

::

   CRLF

::

   payload

.. _sect_12.5.1.1:

Target Resources
^^^^^^^^^^^^^^^^

The Target URI shall reference one of the resources shown in
`table_title <#table_12.5.1-1>`__.

An origin server shall specify all supported npi-names in its
Conformance Statement and in its response to the Retrieve Capabilities
transaction.

.. table:: Store Transaction Resources

   +---------------+-----------------------+-------------------------+
   | Resource      | URI Template          | Description             |
   +===============+=======================+=========================+
   | All Instances | ::                    | Stores representations  |
   |               |                       | of a set of Instances.  |
   |               |    /{npi-name}        |                         |
   +---------------+-----------------------+-------------------------+
   | Instance      | ::                    | Stores a representation |
   |               |                       | of a single Instance    |
   |               |    /{npi-name} {/uid} | with a UID equal to     |
   |               |                       | uid.                    |
   +---------------+-----------------------+-------------------------+

.. _sect_12.5.1.2:

Query Parameters
^^^^^^^^^^^^^^^^

The user agent shall supply, and the origin server shall support, the
Common Query Parameters in `Common Query Parameters <#sect_12.1.2>`__.

.. _sect_12.5.1.3:

Request Header Fields
^^^^^^^^^^^^^^^^^^^^^

.. table:: Request Header Fields

   +---------------+------------+-------+-------------+---------------+
   | Name          | Values     | Usage | Description |               |
   +===============+============+=======+=============+===============+
   | Content-Type  | media-type | M     | M           | The DICOM     |
   |               |            |       |             | Media Type of |
   |               |            |       |             | the request   |
   |               |            |       |             | payload.      |
   +---------------+------------+-------+-------------+---------------+
   | C             | uint       | C     | M           | Shall be      |
   | ontent-Length |            |       |             | present if a  |
   |               |            |       |             | content       |
   |               |            |       |             | encoding has  |
   |               |            |       |             | not been      |
   |               |            |       |             | applied to    |
   |               |            |       |             | the payload.  |
   +---------------+------------+-------+-------------+---------------+
   | Con           | encoding   | C     | M           | Shall be      |
   | tent-Encoding |            |       |             | present if a  |
   |               |            |       |             | content       |
   |               |            |       |             | encoding has  |
   |               |            |       |             | been applied  |
   |               |            |       |             | to the        |
   |               |            |       |             | payload.      |
   +---------------+------------+-------+-------------+---------------+

See also `Header Fields <#sect_8.4>`__.

.. _sect_12.5.1.4:

Request Payload
^^^^^^^^^^^^^^^

The request payload shall be present and shall contain one or more
representations in the DICOM Media Type specified by the Content-Type
header field of the message, or for multipart payloads the Content-Type
header field of each part.

.. _sect_12.5.2:

Behavior
~~~~~~~~

The origin server stores the representations contained in the request
payload so that they may be retrieved later using the Retrieve
transaction.

Before storing the representations, the origin server may coerce data
elements.

If any element is coerced, the Original Attribute Sequence (0400,0561)
(see ) shall be included in the stored DICOM instances. Both the
Original Attribute Sequence and the response shall describe the
modifications.

.. _sect_12.5.3:

Response
~~~~~~~~

The response shall have the following syntax:

::

   version SP status-code SP reason-phrase CRLF

::

   [Content-Type: media-type CRLF]

::

   [(Content-Length: uint / Content-Encoding: encoding) CRLF]

::

   [Content-Location: url CRLF]

::

   *(header-field CRLF)

::

   CRLF

::

   [Status Report]

.. _sect_12.5.3.1:

Status Codes
^^^^^^^^^^^^

`table_title <#table_12.5.3-1>`__ shows some common status codes
corresponding to this transaction. See also `Status Codes <#sect_8.5>`__
for additional status codes.

.. table:: Status Code Meaning

   +----------------------+----------------------+----------------------+
   | Status               | Code                 | Meaning              |
   +======================+======================+======================+
   | Success              | 200 (OK)             | The origin server    |
   |                      |                      | successfully stored  |
   |                      |                      | or created at least  |
   |                      |                      | one of the           |
   |                      |                      | representations      |
   |                      |                      | contained in the     |
   |                      |                      | request payload and  |
   |                      |                      | is returning a       |
   |                      |                      | response payload.    |
   +----------------------+----------------------+----------------------+
   | 202 (Accepted)       | The origin server    |                      |
   |                      | successfully         |                      |
   |                      | validated the        |                      |
   |                      | request message but  |                      |
   |                      | has not yet stored   |                      |
   |                      | or created the       |                      |
   |                      | representations in   |                      |
   |                      | the request payload. |                      |
   |                      | The origin server    |                      |
   |                      | may or may not have  |                      |
   |                      | validated the        |                      |
   |                      | payload.             |                      |
   |                      |                      |                      |
   |                      | The user agent can   |                      |
   |                      | use a Query or       |                      |
   |                      | Retrieve transaction |                      |
   |                      | later to determine   |                      |
   |                      | if the request has   |                      |
   |                      | completed.           |                      |
   +----------------------+----------------------+----------------------+
   | Failure              | 400 (Bad Request)    | The was a problem    |
   |                      |                      | with the request.    |
   |                      |                      | For example:         |
   |                      |                      |                      |
   |                      |                      | -  the origin server |
   |                      |                      |    did not store any |
   |                      |                      |    of the            |
   |                      |                      |    representations   |
   |                      |                      |    contained in the  |
   |                      |                      |    request payload   |
   |                      |                      |    because of errors |
   |                      |                      |    in the request    |
   |                      |                      |    message,          |
   |                      |                      |                      |
   |                      |                      | -  the request       |
   |                      |                      |    contained an      |
   |                      |                      |    invalid Query     |
   |                      |                      |    Parameter,        |
   |                      |                      |                      |
   |                      |                      | -  the request       |
   |                      |                      |    referenced an     |
   |                      |                      |    invalid instance. |
   +----------------------+----------------------+----------------------+
   | 404 (Not Found)      | The origin server    |                      |
   |                      | did not find a       |                      |
   |                      | current              |                      |
   |                      | representation for   |                      |
   |                      | the Target Resource  |                      |
   |                      | or is not willing to |                      |
   |                      | disclose that one    |                      |
   |                      | exists. For example, |                      |
   |                      | an unsupported IOD,  |                      |
   |                      | or Instance not on   |                      |
   |                      | server.              |                      |
   +----------------------+----------------------+----------------------+
   | 409 (Conflict)       | The request could    |                      |
   |                      | not be completed due |                      |
   |                      | to a conflict with   |                      |
   |                      | the current state of |                      |
   |                      | the Target Resource. |                      |
   +----------------------+----------------------+----------------------+
   | 415 (Unsupported     | The origin server    |                      |
   | Media Type)          | does not support the |                      |
   |                      | media type specified |                      |
   |                      | in the Content-Type  |                      |
   |                      | header field of the  |                      |
   |                      | request, and none of |                      |
   |                      | the representations  |                      |
   |                      | contained in the     |                      |
   |                      | request were         |                      |
   |                      | processed or stored. |                      |
   +----------------------+----------------------+----------------------+

.. _sect_12.5.3.2:

Response Header Fields
^^^^^^^^^^^^^^^^^^^^^^

.. table:: Response Header Fields

   +----------------+----------------+----------------+----------------+
   | Header Field   | Value          | Origin Server  | Requirements   |
   |                |                | Usage          |                |
   +================+================+================+================+
   | Content-Type   | di             | M              | The media type |
   |                | com-media-type |                | of the         |
   |                |                |                | response       |
   |                |                |                | payload.       |
   +----------------+----------------+----------------+----------------+
   | Content-Length | uint           | C              | Shall be       |
   |                |                |                | present if a   |
   |                |                |                | content        |
   |                |                |                | encoding has   |
   |                |                |                | not been       |
   |                |                |                | applied to the |
   |                |                |                | payload        |
   +----------------+----------------+----------------+----------------+
   | Co             | encoding       | C              | Shall be       |
   | ntent-Encoding |                |                | present if a   |
   |                |                |                | content        |
   |                |                |                | encoding has   |
   |                |                |                | been applied   |
   |                |                |                | to the payload |
   +----------------+----------------+----------------+----------------+

See also `Header Fields <#sect_8.4>`__.

.. _sect_12.5.3.3:

Response Payload
^^^^^^^^^^^^^^^^

If the origin server failed to store or modified any representations in
the request payload, the response payload shall contain a Status Report
describing any additions, modifications, or deletions to the stored
representations. The Status Report may also describe any warnings or
other useful information.

.. _sect_12.6:

Search Transaction
------------------

The Search transaction searches the collection of NPI Instances
contained in the Target Resource. The search criteria are specified in
the query parameters. Each match includes the default and requested
Attributes from the matching Instance. A successful response returns a
list describing the matching Instances.

.. _sect_12.6.1:

Request
~~~~~~~

The request shall have the following syntax:

::

   GET SP /{npi-name} {?parameter*} SP version CRLF

::

   Accept: 1#dicom-media-type CRLF

::

   *(header-field CRLF)

::

   CRLF

.. _sect_12.6.1.1:

Target Resources
^^^^^^^^^^^^^^^^

The Target URI shall reference one of the resources shown in
`table_title <#table_12.6.1-1>`__.

An origin server shall specify all supported npi-names in its
Conformance Statement and in its response to the Retrieve Capabilities
transaction.

.. table:: Search Transaction Resources

   ============= ============ =======================================
   Resource      URI Template Description
   ============= ============ =======================================
   All Instances /{npi-name}  Searches a collection of NPI Instances.
   ============= ============ =======================================

.. _sect_12.6.1.2:

Query Parameters
^^^^^^^^^^^^^^^^

The user agent shall supply, and the origin server shall support, the
Common Query Parameters in `Common Query Parameters <#sect_12.1.2>`__.

The origin server shall support Query Parameters as required in
`table_title <#table_8.3.4-1>`__.

The user agent shall supply in the request Query Parameters as required
in `table_title <#table_8.3.4-1>`__.

For each Resource Category the origin server supports, it shall support
the behaviors and matching key Attributes specified in the corresponding
sections in `table_title <#table_12.6.1-2>`__.

.. table:: NPI Resource Search Attributes

   ========================== =====================================
   Resource Category          Behaviors and Matching Key Attributes
   ========================== =====================================
   Color Palette              .
   Defined Procedure Protocol .
   Hanging Protocol           .
   Implant Template           .
   ========================== =====================================

.. _sect_12.6.1.3:

Request Header Fields
^^^^^^^^^^^^^^^^^^^^^

.. table:: Request Header Fields

   +--------+----------------+-------+-------------+----------------+
   | Name   | Values         | Usage | Description |                |
   +========+================+=======+=============+================+
   | Accept | 1#-di          | M     | M           | The Acceptable |
   |        | com-media-type |       |             | Media Types of |
   |        |                |       |             | the response   |
   |        |                |       |             | payload        |
   +--------+----------------+-------+-------------+----------------+

See also `Header Fields <#sect_8.4>`__.

.. _sect_12.6.1.4:

Request Payload
^^^^^^^^^^^^^^^

The request has no payload.

.. _sect_12.6.2:

Behavior
~~~~~~~~

The origin server shall perform the search indicated by the request,
using the matching behavior specified in `Matching
Rules <#sect_8.3.4.1.1>`__ and in the corresponding sections in
`table_title <#table_8.3.4-1>`__.

The rules for search results are specified in `Search Query
Parameters <#sect_8.3.4>`__.

.. _sect_12.6.3:

Response
~~~~~~~~

The response shall have the following syntax:

::

   version SP status-code SP reason-phrase CRLF

::

   [Content-Type: dicom-media-type CRLF]

::

   [(Content-Length: uint / Content-Encoding: encoding) CRLF]

::

   [Content-Location: url CRLF]

::

   *(header-field CRLF

::

   CRLF

::

   [payload / status-report]

.. _sect_12.6.3.1:

Status Codes
^^^^^^^^^^^^

`table_title <#table_12.6.3-1>`__ shows some common status codes
corresponding to this transaction. See also `Status Codes <#sect_8.5>`__
for additional status codes.

.. table:: Status Code Meaning

   +----------------------+----------------------+----------------------+
   | Status               | Code                 | Meaning              |
   +======================+======================+======================+
   | Success              | 200 (OK)             | The query completed  |
   |                      |                      | and any matching     |
   |                      |                      | results are returned |
   |                      |                      | in the message body. |
   +----------------------+----------------------+----------------------+
   | Failure              | 400 (Bad Request)    | The request message  |
   |                      |                      | contained an error.  |
   |                      |                      | For example, the     |
   |                      |                      | Query Parameters     |
   |                      |                      | were invalid         |
   +----------------------+----------------------+----------------------+
   | 406 (Unsupported     | The origin server    |                      |
   | Media Type)          | does not support any |                      |
   |                      | of the Acceptable    |                      |
   |                      | Media Types.         |                      |
   +----------------------+----------------------+----------------------+
   | 413 (Payload Too     | The search was too   |                      |
   | Large)               | broad, and the body  |                      |
   |                      | of the response      |                      |
   |                      | should contain a     |                      |
   |                      | Status Report with   |                      |
   |                      | additional           |                      |
   |                      | information about    |                      |
   |                      | the failure.         |                      |
   +----------------------+----------------------+----------------------+

.. _sect_12.6.3.2:

Response Header Fields
^^^^^^^^^^^^^^^^^^^^^^

.. table:: Response Header Fields

   +----------------+----------------+----------------+----------------+
   | Header Field   | Value          | Origin Server  | Requirement    |
   |                |                | Usage          |                |
   +================+================+================+================+
   | Content-Type   | di             | M              | The media type |
   |                | com-media-type |                | of the         |
   |                |                |                | response       |
   |                |                |                | payload.       |
   +----------------+----------------+----------------+----------------+
   | Content-Length | Uint           | C              | Shall be       |
   |                |                |                | present if a   |
   |                |                |                | content        |
   |                |                |                | encoding has   |
   |                |                |                | not been       |
   |                |                |                | applied to the |
   |                |                |                | payload.       |
   +----------------+----------------+----------------+----------------+
   | Co             | Encoding       | C              | Shall be       |
   | ntent-Encoding |                |                | present if a   |
   |                |                |                | content coding |
   |                |                |                | has been       |
   |                |                |                | applied to the |
   |                |                |                | payload.       |
   +----------------+----------------+----------------+----------------+

See also `Header Fields <#sect_8.4>`__.

.. _sect_12.6.3.3:

Response Payload
^^^^^^^^^^^^^^^^

A success response shall contain the search results in an Acceptable
Media Type. See `Acceptable Media Types <#sect_8.7.5>`__.

A failure response payload may contain a Status Report describing any
failures, warnings, or other useful information.

