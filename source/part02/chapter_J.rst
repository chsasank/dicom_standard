.. _chapter_J:

Conformance Statement Sample STOW Service (Informative)
=======================================================

Disclaimer:

This document is an example DICOM Conformance Statement for a fictional
application service called EXAMPLE-STOW-SERVICE produced by a fictional
vendor called EXAMPLE-PACS-PRODUCTS.

As stated in the annex title, this document is truly informative, and
not normative. A conformance statement of an actual product might
implement additional services and options as appropriate for its
specific purpose. In addition, an actual product might implement the
services described in a different manner and, for example, with
different characteristics and/or sequencing of activities. In other
words, this conformance statement example does not intend to standardize
a particular manner that a product might implement DICOM functionality.

.. _sect_J.0:

Cover Page
----------

Company Name: EXAMPLE-PACS-PRODUCTS-VENDOR

Product Name: EXAMPLE-STOW-SERVICE

Version: 1.0-rev. A.1

Internal document number: 1024-1960-xx-yy-zz rev 1

Date: YYYYMMDD

.. _sect_J.1:

Conformance Statement Overview
------------------------------

This fictional product EXAMPLE-STOW-SERVICE implements the STOW-RS
services for storing DICOM SOP Instances into an EXAMPLE-PACS-ARCHIVE.
The EXAMPLE-STOW-SERVICE is only available as a plug in option for the
EXAMPLE-PACS-ARCHIVE. All of the networking, database, and other
services are provided by the EXAMPLE-PACS-ARCHIVE. This conformance
claim refers to the conformance claim for the EXAMPLE-PACS-ARCHIVE for
all such services.

`table_title <#table_J.1-1>`__ provides an overview of the network
services supported by EXAMPLE-STOW-SERVICE.

.. table:: Network Services

   +----------------------+----------------------+----------------------+
   | **Network Service**  | **User of Service    | **Provider of        |
   |                      | (Client)**           | Service (Server)**   |
   +======================+======================+======================+
   | **STorage Over the   |                      |                      |
   | Web (STOW)**         |                      |                      |
   +----------------------+----------------------+----------------------+
   | STOW-RS - Store      | No                   | Yes                  |
   | Instances            |                      |                      |
   +----------------------+----------------------+----------------------+

.. _sect_J.2:

Table of Contents
-----------------

A table of contents shall be provided to assist readers in easily
finding the needed information.

.. _sect_J.3:

Introduction
------------

.. _sect_J.3.1:

Revision History
~~~~~~~~~~~~~~~~

.. table:: Revision History

   +-----------------+-----------------+------------+-----------------+
   | **Document      | **Date of       | **Author** | **Description** |
   | Version**       | Issue**         |            |                 |
   +=================+=================+============+=================+
   | 1.1             | November 16     | LCS        | Version for     |
   |                 | :sup:`th`, 2012 |            | Final Text      |
   +-----------------+-----------------+------------+-----------------+
   | 1.2             | February 8      | LCS        | Revised         |
   |                 | :sup:`th`, 2013 |            | Introduction    |
   +-----------------+-----------------+------------+-----------------+
   | 1.3             | May 16          | SAR        | Incorporated    |
   |                 | :sup:`th`, 2013 |            | CP-71           |
   +-----------------+-----------------+------------+-----------------+

.. _sect_J.3.2:

Audience, Remarks, Terms and Definitions, Basics of DICOM Communication, Abbreviations, References
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

*See example text in*\ `Introduction <#sect_A.3>`__\ *.*

.. _sect_J.3.3:

Additional Remarks for This Example
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This document is a sample DICOM Conformance Statement created for DICOM
. It is to be used solely as an example to illustrate how to create a
DICOM Conformance Statement for a DICOM Service Class Provider (SCP).
The subject of the document, EXAMPLE-STOW-SERVICE, is a fictional
product.

.. _sect_J.4:

Networking
----------

.. _sect_J.4.1:

Implementation Model
~~~~~~~~~~~~~~~~~~~~

.. _sect_J.4.1.1:

Application Data Flow
^^^^^^^^^^^^^^^^^^^^^

Example STOW Service

The STOW-RS Service Application receives STOW requests from a remote AE.
These requests are HTTP POST requests. It is associated with the local
real-world activity "Store Instances". It converts these requests into
internal functions to store the given SOP Instances. It returns a
summary HTTP status line, including a status code and an associated
textual phase, followed by an XML message indicating success, warning,
or failure for each instance to the requesting remote AE.

.. _sect_J.4.1.2:

Functional Definition of AEs
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. _sect_J.4.1.2.1:

Functional Definition of STOW Service Application
'''''''''''''''''''''''''''''''''''''''''''''''''

The reception of a STOW-RS POST request will activate the STOW-RS
Service. The storage request is based upon the accept headers in the
STOW-RS POST request. The response includes an HTTP status line,
including a status-code and its associated textual phrase, followed by
an XML message indicating success, warning, or failure for each instance
stored by the STOW-RS service.

.. _sect_J.4.2:

AE Specifications
~~~~~~~~~~~~~~~~~

This AE complies with , specification for STOW-RS storage.

.. _sect_J.4.2.1:

STOW-RS Specifications
^^^^^^^^^^^^^^^^^^^^^^

.. _sect_J.4.2.1.1:

STOW-RS Store Instance
''''''''''''''''''''''

.. table:: STOW-RS Store Instances Specification

   +----------------------------------+----------------------------------+
   | **Category**                     | **Restrictions**                 |
   +==================================+==================================+
   | Media Types Supported (Accept    | Restricted to application/dicom  |
   | header)                          | or application/dicom+xml         |
   +----------------------------------+----------------------------------+
   | Transfer Syntaxes Supported      | Any Transfer Syntax supported by |
   |                                  | the hosting EXAMPLE-PACS-ARCHIVE |
   | (Media Type parameter)           |                                  |
   +----------------------------------+----------------------------------+
   | SOP Class Restrictions           | Restricted to SOP classes        |
   |                                  | supported by the hosting         |
   |                                  | EXAMPLE-PACS-ARCHIVE             |
   +----------------------------------+----------------------------------+
   | Size restriction                 | Restricted to size supported by  |
   |                                  | the hosting EXAMPLE-PACS-ARCHIVE |
   +----------------------------------+----------------------------------+

.. _sect_J.4.2.2.4:

Connection Policies
'''''''''''''''''''

.. _sect_J.4.2.2.4.1:

General
       

All standard RS connection policies apply. There are no extensions for
RS options.

.. _sect_J.4.2.2.4.2:

Number of Connections
                     

EXAMPLE-STOW-SERVICE limits the number of simultaneous RS requests.
Additional requests will be queued after the HTTP connection is
accepted. When an earlier request completes, a pending request will
proceed.

.. table:: Number of HTTP Requests Supported

   ========================================== ==================
   Maximum number of simultaneous RS requests 100 (configurable)
   ========================================== ==================

.. _sect_J.4.2.2.4.3:

Asynchronous Nature
                   

EXAMPLE-STOW-SERVICE does not support RS asynchronous response.

.. _sect_J.4.2.2.4.4:

SOP Specific Conformance for SOP Class(Es)
                                          

The EXAMPLE-STOW-SERVICE response message header contains status codes
indicating success, warning, or failure as shown in the "HTTP Standard
Response Codes" below. No additional status codes are used.

.. table:: HTTP Standard Response Codes

   +----------------+--------------------+------------------------------+
   | Service Status | HTTP Status Code   | STOW-RS Description          |
   +================+====================+==============================+
   | Failure        | 400 - Bad Request  | This indicates that the      |
   |                |                    | STOW-RS Service was unable   |
   |                |                    | to store any instances due   |
   |                |                    | to bad syntax.               |
   +----------------+--------------------+------------------------------+
   |                | 401 - Unauthorized | This indicates that the      |
   |                |                    | STOW-RS Service refused to   |
   |                |                    | create or append any         |
   |                |                    | instances because the client |
   |                |                    | is not authenticated.        |
   +----------------+--------------------+------------------------------+
   |                | 403 - Forbidden    | This indicates that the      |
   |                |                    | STOW-RS Service understood   |
   |                |                    | the request, but is refusing |
   |                |                    | to fulfill it (e.g., an      |
   |                |                    | authenticated user with      |
   |                |                    | insufficient privileges).    |
   +----------------+--------------------+------------------------------+
   |                | 409 - Conflict     | This indicates that the      |
   |                |                    | STOW-RS Service request was  |
   |                |                    | formed correctly but the     |
   |                |                    | service was unable to store  |
   |                |                    | any instances due to a       |
   |                |                    | conflict in the request      |
   |                |                    | (e.g., unsupported SOP Class |
   |                |                    | or Study Instance UID        |
   |                |                    | mismatch).                   |
   |                |                    |                              |
   |                |                    | This may also be used to     |
   |                |                    | indicate that a STOW-RS      |
   |                |                    | Service was unable to store  |
   |                |                    | any instances for a mixture  |
   |                |                    | of reasons.                  |
   |                |                    |                              |
   |                |                    | Additional information       |
   |                |                    | regarding the instance       |
   |                |                    | errors can be found in the   |
   |                |                    | XML response message body.   |
   +----------------+--------------------+------------------------------+
   |                | 503 - Busy         | This indicates that the      |
   |                |                    | STOW-RS Service was unable   |
   |                |                    | to store any instances       |
   |                |                    | because it was out of        |
   |                |                    | resources.                   |
   +----------------+--------------------+------------------------------+
   | Warning        | 202 - Accepted     | This indicates that the      |
   |                |                    | STOW-RS Service stored some  |
   |                |                    | of the instances but         |
   |                |                    | warnings or failures exist   |
   |                |                    | for others.                  |
   |                |                    |                              |
   |                |                    | Additional information       |
   |                |                    | regarding this error can be  |
   |                |                    | found in the XML response    |
   |                |                    | message body.                |
   +----------------+--------------------+------------------------------+
   |                |                    |                              |
   +----------------+--------------------+------------------------------+
   |                |                    |                              |
   +----------------+--------------------+------------------------------+
   | Success        | 200 - OK           | This indicates that the      |
   |                |                    | STOW-RS Service successfully |
   |                |                    | stored all the instances.    |
   +----------------+--------------------+------------------------------+

The EXAMPLE-STOW-SERVICE response message body ( XML Store Instances
Response Module) contains the DICOM status codes for individual SOP
Instances indicating success, warning, or failure as defined below. No
additional status codes are used.

For the following semantics the associated value are used for the
Warning Reason (0008,1196):

B000
   Coercion of Data Elements

   The STOW-RS Service modified one or more data elements during storage
   of the instance.

B006
   Elements Discarded

   The STOW-RS Service discarded some data elements during storage of
   the instance.

B007
   Data Set does not match SOP Class

   The STOW-RS Service stored the instance despite the Data Set not
   matching the constraints of the SOP Class.

Additional codes may be used for the Warning Reason (0008,1196) to
address the semantics of other issues.

In the event that multiple codes may apply, the single most appropriate
code is used.

For the following semantics the associated value are used for the
Failure Reason (0008,1197).

A700
   Refused out of Resources

   The STOW-RS Service did not store the instance because it was out of
   memory.

A710
   Refused out of Resources

   The STOW-RS Service did not store the instance because it was out of
   storage space.

A900
   Error: Data Set does not match SOP Class

   The STOW-RS Service did not store the instance because the SOP Class
   of an element in the Referenced SOP Instance Sequence did not
   correspond to the SOP class registered for this SOP Instance at the
   STOW-RS Service.

C000
   Error: Cannot understand

   The STOW-RS Service did not store the instance because it cannot
   understand certain Data Elements.

C122
   Referenced Transfer Syntax not supported

   The STOW-RS Service did not store the instance because it does not
   support the requested Transfer Syntax for the instance.

0110
   Processing failure

   The STOW-RS Service did not store the instance because of a general
   failure in processing the operation.

0122
   Referenced SOP Class not supported

   The STOW-RS Service did not store the instance because it does not
   support the requested SOP Class.

Additional codes may be used for the Failure Reason (0008,1197) to
address the semantics of other errors.

In the event that multiple codes may apply, the single most appropriate
code shall be used.

.. _sect_J.4.3:

Network Interfaces
~~~~~~~~~~~~~~~~~~

.. _sect_J.4.3.1:

Physical Network Interface
^^^^^^^^^^^^^^^^^^^^^^^^^^

EXAMPLE-STOW-SERVICE uses the network interface from the hosting
EXAMPLE-PACS-ARCHIVE. See its conformance claim for details.

.. _sect_J.4.3.2:

Additional Protocols
^^^^^^^^^^^^^^^^^^^^

EXAMPLE-STOW-SERVICE uses the network services from the hosting
EXAMPLE-PACS-ARCHIVE. See its conformance claim for details.

.. _sect_J.4.3.3:

IPv4 and IPv6 Support
^^^^^^^^^^^^^^^^^^^^^

This product supports both IPv4 and IPv6 connections.

.. _sect_J.4.4:

Configuration
~~~~~~~~~~~~~

.. _sect_J.4.4.1:

STOW-RS Interface
^^^^^^^^^^^^^^^^^

The EXAMPLE-STOW-SERVICE is configured to respond to TLS protected
traffic. The TLS port will refuse any connection from a system that is
not recognized as authenticated by a known authority.

.. _sect_J.5:

Media Interchange
-----------------

Not applicable

.. _sect_J.6:

Support of Character Sets
-------------------------

All EXAMPLE-STOW-SERVICEs support Unicode UTF-8 for all RS transactions.

The EXAMPLE-STOW-SERVICE does not convert character sets when storing
binary Instances. The original DICOM encoded character sets are
preserved.

.. _sect_J.7:

Security
--------

The EXAMPLE-STOW-SERVICE supports the following transport level security
measures:

-  HTTP BASIC Authorization over SSL

-  Digest Authorization

-  SSL Client Certificates

The transport level security measures support bi-directional
authentication using TLS connections. The EXAMPLE-STOW-SERVICE can
provide its certificate information, and can be configured with either a
direct comparison (self-signed) certificate or a chain of trust
certificates.

The EXAMPLE-STOW-SERVICE will refuse a connection over TLS from a source
that does not have a recognized authentication. For example, a
certificate authenticated by "Big Hospital Provider" will not be
accepted unless the EXAMPLE-STOW-SERVICE has been configured to accept
authentications from "Big Hospital Provider". The list of acceptable
certificates for EXAMPLE-STOW-SERVICE is not shared with certificates
used by other system applications and must be maintained independently.

The EXAMPLE-STOW-SERVICE can optionally be configured to use the
following session authentication mechanisms:

-  Kerberos Local Domain Sessions

-  Shibboleth Cross Domain Sessions (using SAML2.0)

-  OAuth 2.0 complying with IHE ITI Internet User Authentication (IUA)

.. _sect_J.8:

Annexes
-------

.. _sect_J.8.1:

IOD Contents
~~~~~~~~~~~~

See conformance claim for the EXAMPLE-PACS-ARCHIVE.

.. _sect_J.8.2:

Data Dictionary of Private Attributes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

No data dictionary for private attributes is provided. Private
attributes are stored as received without modification.

.. _sect_J.8.3:

Coded Terminology and Templates
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

See conformance claim for EXAMPLE-PACS-ARCHIVE.

.. _sect_J.8.4:

Standard Extended / Specialized / Private SOP Classes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

See conformance claim for EXAMPLE-PACS-ARCHIVE.

.. _sect_J.8.5:

Private Transfer Syntaxes
~~~~~~~~~~~~~~~~~~~~~~~~~

Private transfer syntaxes are not supported.

