.. _chapter_I:

Conformance Statement Sample WADO Service (Informative)
=======================================================

Disclaimer:

This document is an example DICOM Conformance Statement for a fictional
application service called EXAMPLE-WADO-SERVICE produced by a fictional
vendor called EXAMPLE-PACS-PRODUCTS.

As stated in the annex title, this document is truly informative, and
not normative. A conformance statement of an actual product might
implement additional services and options as appropriate for its
specific purpose. In addition, an actual product might implement the
services described in a different manner and, for example, with
different characteristics and/or sequencing of activities. In other
words, this conformance statement example does not intend to standardize
a particular manner that a product might implement DICOM functionality.

.. _sect_I.0:

Cover Page
----------

Company Name: EXAMPLE-PACS-PRODUCTS.

Product Name: EXAMPLE-WADO-SERVICE

Version: 1.0-rev. A.1

Internal document number: 4226-xxx-yyy-zzz rev 1

Date: YYYYMMDD

.. _sect_I.1:

Conformance Statement Overview
------------------------------

This fictional product EXAMPLE-WADO-SERVICE implements the WADO-URI
services and the WADO RS services for access to DICOM SOP Instances that
are stored on an EXAMPLE-PACS-ARCHIVE. The EXAMPLE-WADO-SERVICE is only
available as a plug in option for the EXAMPLE-PACS-ARCHIVE. All of the
networking, database, and other services are provided by the
EXAMPLE-PACS-ARCHIVE. This conformance claim refers to the conformance
claim for the EXAMPLE-PACS-ARCHIVE for all such services.

`table_title <#table_I.1-1>`__ provides an overview of the network
services supported by EXAMPLE-WADO-SERVICE.

.. table:: Network Services

   +----------------------+----------------------+----------------------+
   | Network Service      | User of Service      | Provider of Service  |
   |                      | (Client)             | (Server)             |
   +======================+======================+======================+
   | WADO - URI -         | No                   | Yes                  |
   | Retrieve Imaging     |                      |                      |
   | Document             |                      |                      |
   +----------------------+----------------------+----------------------+
   | WADO - URI -         | No                   | Yes                  |
   | Retrieve Rendered    |                      |                      |
   | Imaging Document     |                      |                      |
   +----------------------+----------------------+----------------------+
   | WADO - RS - Retrieve | No                   | Yes                  |
   | Study                |                      |                      |
   +----------------------+----------------------+----------------------+
   | WADO - RS - Retrieve | No                   | Yes                  |
   | Series               |                      |                      |
   +----------------------+----------------------+----------------------+
   | WADO - RS - Retrieve | No                   | Yes                  |
   | Instance             |                      |                      |
   +----------------------+----------------------+----------------------+
   | WADO - RS - Retrieve | No                   | Yes                  |
   | Frames               |                      |                      |
   +----------------------+----------------------+----------------------+
   | WADO - RS - Retrieve | No                   | Yes                  |
   | Bulkdata             |                      |                      |
   +----------------------+----------------------+----------------------+
   | WADO - RS - Retrieve | No                   | Yes                  |
   | Metadata             |                      |                      |
   +----------------------+----------------------+----------------------+

.. _sect_I.2:

Table of Contents
-----------------

A table of contents shall be provided to assist readers in easily
finding the needed information.

.. _sect_I.3:

Introduction
------------

.. _sect_I.3.1:

Revision History
~~~~~~~~~~~~~~~~

.. table:: Revision History

   ================ ================ ====== ======================
   Document Version Date of Issue    Author Description
   ================ ================ ====== ======================
   1.1              October 30, 2003 WG 6   Version for Final Text
   1.2              August 30, 2007  WG 6   Revised Introduction
   1.3              February 6, 2013 WG 6   WADO-RS Final Text
   ================ ================ ====== ======================

.. _sect_I.3.2:

Audience, Remarks, Terms and Definitions, Basics of DICOM Communication, Abbreviations, References
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

*See example text in*\ `Introduction <#sect_A.3>`__\ *.*

.. _sect_I.3.3:

Additional Remarks for This Example
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This document is a sample DICOM Conformance Statement created for DICOM
. It is to be used solely as an example to illustrate how to create a
DICOM Conformance Statement for an acquisition modality. The subject of
the document, EXAMPLE-WADO-SERVICE, is a fictional product.

.. _sect_I.4:

Networking
----------

.. _sect_I.4.1:

Implementation Model
~~~~~~~~~~~~~~~~~~~~

.. _sect_I.4.1.1:

Application Data Flow
^^^^^^^^^^^^^^^^^^^^^

The WADO Service Application receives WADO requests from a remote AE.
These requests may be either over the URI, WS or RS interfaces. It is
associated with the local real-world activity "Retrieve Images". It
converts these requests into internal lookup functions to find the
matching SOP Instances. It then obtains these matching SOP Instances and
composes a response back to the requesting remote AE.

.. _sect_I.4.1.2:

Functional Definition of AEs
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. _sect_I.4.1.2.1:

Functional Definition of WADO Service Application
'''''''''''''''''''''''''''''''''''''''''''''''''

The reception of a WADO request will activate the AE. An internal
request is sent to the search capabilities of the EXAMPLE-WADO-SERVICE.
This request is based upon the request parameters or the URL resource
end point from the WADO request. The response is a list of all SOP
instances stored on the EXAMPLE-PACS-ARCHIVE that match the request
parameters. If there are no matching instances, the AE will indicate
this in the WADO response. For all matching instances, the AE will
utilize the internal image transfer request to obtain a copy of each
instance. If the request was for retrieval of instances, these instances
will be returned. If the request was for retrieval of rendered
instances, then the AE will render each instance and return the rendered
results.

.. _sect_I.4.2:

AE Specifications
~~~~~~~~~~~~~~~~~

This AE complies with , specifications for RS and URI access.

.. _sect_I.4.2.1:

WADO-WS Specifications
^^^^^^^^^^^^^^^^^^^^^^

DICOM has retired the WADO-WS Service. See PS3.2-2017b. This product
still supports this service as described here.

.. _sect_I.4.2.1.1:

WADO-WS Retrieve Imaging Document Set
'''''''''''''''''''''''''''''''''''''

.. table:: WADO-WS Retrieve Imaging Document Set Specification

   +-----------------------------+---------------------------------------+
   | Parameter                   | Restrictions                          |
   +=============================+=======================================+
   | Transfer Syntaxes Supported | Any transfer syntax supported by the  |
   |                             | hosting EXAMPLE-PACS-ARCHIVE          |
   +-----------------------------+---------------------------------------+
   | SOP Class Restrictions      | Any SOP class supported by the        |
   |                             | hosting EXAMPLE-PACS-ARCHIVE          |
   +-----------------------------+---------------------------------------+
   | Size restriction            | Any size supported by the hosting     |
   |                             | EXAMPLE-PACS-ARCHIVE                  |
   +-----------------------------+---------------------------------------+
   | Anonymization               | Supports the DICOM Basic Application  |
   |                             | Level Confidentiality Profile plus    |
   |                             | the Retain Patient Characteristics    |
   |                             | option.                               |
   +-----------------------------+---------------------------------------+

.. _sect_I.4.2.1.2:

WADO-WS Retrieve Rendered Imaging Document Set
''''''''''''''''''''''''''''''''''''''''''''''

.. table:: WADO-WS Retrieve Rendered Imaging Documents Specification

   +-----------------------------+---------------------------------------+
   | Parameter                   | Restrictions                          |
   +=============================+=======================================+
   | Transfer Syntaxes Supported | Restricted to transfer syntaxes       |
   |                             | supported by the hosting              |
   |                             | EXAMPLE-PACS-ARCHIVE                  |
   +-----------------------------+---------------------------------------+
   | SOP Class Restrictions      | Restricted to SOP classes supported   |
   |                             | by the hosting EXAMPLE-PACS-ARCHIVE   |
   +-----------------------------+---------------------------------------+
   | Size restriction            | Restricted to sizes supported by the  |
   |                             | hosting EXAMPLE-PACS-ARCHIVE          |
   +-----------------------------+---------------------------------------+
   | Rendered formats available  | Supports JPEG and PDF for IMAGE IODS, |
   |                             | and PDF for non-IMAGE IODS.           |
   +-----------------------------+---------------------------------------+
   | Rows restrictions           | Must be in range 16 - 32767           |
   +-----------------------------+---------------------------------------+
   | Columns restrictions        | Must be in range 16 - 32767           |
   +-----------------------------+---------------------------------------+
   | Region restrictions         | None                                  |
   +-----------------------------+---------------------------------------+
   | Window Center restrictions  | None                                  |
   +-----------------------------+---------------------------------------+
   | Window Width restrictions   | None                                  |
   +-----------------------------+---------------------------------------+
   | Image Quality restrictions  | None                                  |
   +-----------------------------+---------------------------------------+
   | Anonymization               | Supports the DICOM Basic Application  |
   |                             | Level Confidentiality Profile plus    |
   |                             | the Retain Patient Characteristics    |
   |                             | option.                               |
   +-----------------------------+---------------------------------------+
   | Annotation restrictions     | None                                  |
   +-----------------------------+---------------------------------------+
   | Compression available       | JPEG                                  |
   +-----------------------------+---------------------------------------+
   | Other restrictions          | None                                  |
   +-----------------------------+---------------------------------------+

.. _sect_I.4.2.1.3:

WADO-WS Retrieve Imaging Document Set Metadata
''''''''''''''''''''''''''''''''''''''''''''''

Not supported

.. _sect_I.4.2.1.4:

Connection Policies
'''''''''''''''''''

.. _sect_I.4.2.1.4.1:

General
       

All standard WS connection policies apply. There are no extensions for
WS options.

.. _sect_I.4.2.1.4.2:

Number of Connections
                     

EXAMPLE-WADO-SERVICE limits the number of simultaneous WS requests.
Additional requests will be queued after the TCP connection is accepted.
When an earlier request completes, a pending request will proceed.

.. table:: Number of WS Requests Supported

   ========================================== ==================
   Maximum number of simultaneous WS requests 100 (configurable)
   ========================================== ==================

.. _sect_I.4.2.1.4.3:

Asynchronous Nature
                   

EXAMPLE-WADO-SERVICE does not support WS asynchronous response.

.. _sect_I.4.2.2:

WADO-URI Specification
^^^^^^^^^^^^^^^^^^^^^^

.. _sect_I.4.2.2.1:

WADO-URI Retrieve Imaging Document Set
''''''''''''''''''''''''''''''''''''''

.. table:: WADO-URI Retrieve Imaging Documents Specification

   +-----------------------------+---------------------------------------+
   | Parameter                   | Restrictions                          |
   +=============================+=======================================+
   | Transfer Syntaxes Supported | Restricted to transfer syntaxes       |
   |                             | supported by the hosting              |
   |                             | EXAMPLE-PACS-ARCHIVE                  |
   +-----------------------------+---------------------------------------+
   | SOP Class restrictions      | Restricted to SOP classes supported   |
   |                             | by the hosting EXAMPLE-PACS-ARCHIVE   |
   +-----------------------------+---------------------------------------+
   | Size restriction            | Restricted to sizes supported by the  |
   |                             | hosting EXAMPLE-PACS-ARCHIVE          |
   +-----------------------------+---------------------------------------+
   | Anonymization               | Supports the DICOM Basic Application  |
   |                             | Level Confidentiality Profile plus    |
   |                             | the Retain Patient Characteristics    |
   |                             | option.                               |
   +-----------------------------+---------------------------------------+

If the URI Retrieve specifies no transfer syntax that is supported by
the archive, the SOP Instance will be returned using the Implicit VR
Little Endian Transfer Syntax.

.. _sect_I.4.2.2.2:

WADO-URI Retrieve Rendered Imaging Document Set
'''''''''''''''''''''''''''''''''''''''''''''''

.. table:: WADO-URI Retrieve Rendered Imaging Documents Specification

   +-----------------------------+---------------------------------------+
   | Parameter                   | Restrictions                          |
   +=============================+=======================================+
   | Transfer Syntaxes Supported | Restricted to transfer syntaxes       |
   |                             | supported by the hosting              |
   |                             | EXAMPLE-PACS-ARCHIVE                  |
   +-----------------------------+---------------------------------------+
   | SOP Class restrictions      | Restricted to SOP classes supported   |
   |                             | by the hosting EXAMPLE-PACS-ARCHIVE   |
   +-----------------------------+---------------------------------------+
   | Size restriction            | Restricted to sizes supported by the  |
   |                             | hosting EXAMPLE-PACS-ARCHIVE          |
   +-----------------------------+---------------------------------------+
   | Rendered formats available  | Supports JPEG and PDF for IMAGE IODS, |
   |                             | and PDF for non-IMAGE IODS.           |
   +-----------------------------+---------------------------------------+
   | Rows restrictions           | Must be in range 16 - 32767           |
   +-----------------------------+---------------------------------------+
   | Columns restrictions        | Must be in range 16 - 32767           |
   +-----------------------------+---------------------------------------+
   | Region restrictions         | None                                  |
   +-----------------------------+---------------------------------------+
   | Window Center restrictions  | Whole window must be in the range of  |
   |                             | image pixel values.                   |
   +-----------------------------+---------------------------------------+
   | Window Width restrictions   | Must be greater than 4 and whole      |
   |                             | window must be in the range of image  |
   |                             | pixel values.                         |
   +-----------------------------+---------------------------------------+
   | Image Quality restrictions  | None                                  |
   +-----------------------------+---------------------------------------+
   | Anonymization               | Supports the DICOM Basic Application  |
   |                             | Level Confidentiality Profile plus    |
   |                             | the Retain Patient Characteristics    |
   |                             | option.                               |
   +-----------------------------+---------------------------------------+
   | Annotation Restrictions     | None                                  |
   +-----------------------------+---------------------------------------+
   | Compression available       | JPEG                                  |
   +-----------------------------+---------------------------------------+
   | Other restrictions          | None                                  |
   +-----------------------------+---------------------------------------+

.. _sect_I.4.2.2.3:

WADO-URI Retrieve Imaging Document Set Metadata
'''''''''''''''''''''''''''''''''''''''''''''''

Not supported.

.. _sect_I.4.2.2.4:

Connection Policies
'''''''''''''''''''

.. _sect_I.4.2.2.4.1:

General
       

All URI connections are limited to HTTP GET requests. The
EXAMPLE-WADO-SERVICE ignores all unknown HTTP header parameters.

.. _sect_I.4.2.2.4.2:

Number of Connections
                     

EXAMPLE-WADO-SERVICE limits the number of simultaneous HTTP connections.

.. table:: Number of HTTP Requests Supported

   ============================================ ==================
   Maximum number of simultaneous HTTP requests 100 (configurable)
   ============================================ ==================

.. _sect_I.4.2.2.4.3:

Asynchronous Nature
                   

EXAMPLE-WADO-SERVICE supports HTTP pipelined requests and responses.

.. _sect_I.4.2.3:

WADO-RS Specifications
^^^^^^^^^^^^^^^^^^^^^^

.. _sect_I.4.2.3.1:

WADO-RS Retrieve Study
''''''''''''''''''''''

.. table:: WADO-RS Retrieve Study

   +----------------------------------+----------------------------------+
   | **Options**                      | **Restrictions**                 |
   +==================================+==================================+
   | Data Types Supported (Accept     | Restricted to application/dicom  |
   | Type)                            | or application/octet-stream      |
   +----------------------------------+----------------------------------+
   | Transfer Syntaxes Supported      | Any Transfer Syntax supported by |
   |                                  | the hosting EXAMPLE-PACS-ARCHIVE |
   | (transfer-syntax Accept          |                                  |
   | parameter)                       |                                  |
   +----------------------------------+----------------------------------+
   | SOP Class Restrictions           | Restricted to SOP classes        |
   |                                  | supported by the hosting         |
   |                                  | EXAMPLE-PACS-ARCHIVE             |
   +----------------------------------+----------------------------------+
   | Size Restriction                 | Restricted to size supported by  |
   |                                  | the hosting EXAMPLE-PACS-ARCHIVE |
   +----------------------------------+----------------------------------+

.. _sect_I.4.2.3.2:

WADO-RS Retrieve Series
'''''''''''''''''''''''

.. table:: WADO-RS Retrieve Series

   +----------------------------------+----------------------------------+
   | **Options**                      | **Restrictions**                 |
   +==================================+==================================+
   | Data Types Supported (Accept     | Restricted to application/dicom  |
   | Type)                            | or application/octet-stream      |
   +----------------------------------+----------------------------------+
   | Transfer Syntaxes Supported      | Any Transfer Syntax supported by |
   |                                  | the hosting EXAMPLE-PACS-ARCHIVE |
   | (Transfer-syntax Accept          |                                  |
   | parameter)                       |                                  |
   +----------------------------------+----------------------------------+
   | SOP Class Restrictions           | Restricted to SOP classes        |
   |                                  | supported by the hosting         |
   |                                  | EXAMPLE-PACS-ARCHIVE             |
   +----------------------------------+----------------------------------+
   | Size Restriction                 | Restricted to size supported by  |
   |                                  | the hosting EXAMPLE-PACS-ARCHIVE |
   +----------------------------------+----------------------------------+

.. _sect_I.4.2.3.3:

WADO-RS Retrieve Instance
'''''''''''''''''''''''''

.. table:: WADO-RS Retrieve Instance

   +----------------------------------+----------------------------------+
   | **Options**                      | **Restrictions**                 |
   +==================================+==================================+
   | Data Types Supported (Accept     | Restricted to application/dicom  |
   | Type)                            | or application/octet-stream      |
   +----------------------------------+----------------------------------+
   | Transfer Syntaxes Supported      | Any Transfer Syntax supported by |
   |                                  | the hosting EXAMPLE-PACS-ARCHIVE |
   | (Transfer-syntax Accept          |                                  |
   | parameter)                       |                                  |
   +----------------------------------+----------------------------------+
   | SOP Class Restrictions           | Restricted to SOP classes        |
   |                                  | supported by the hosting         |
   |                                  | EXAMPLE-PACS-ARCHIVE             |
   +----------------------------------+----------------------------------+
   | Size Restriction                 | Restricted to size supported by  |
   |                                  | the hosting EXAMPLE-PACS-ARCHIVE |
   +----------------------------------+----------------------------------+

.. _sect_I.4.2.3.4:

WADO-RS Retrieve Frames
'''''''''''''''''''''''

.. table:: WADO-RS Retrieve Frames

   +----------------------------------+----------------------------------+
   | **Options**                      | **Restrictions**                 |
   +==================================+==================================+
   | Data Types Supported (Accept     | Restricted to                    |
   | Type)                            | application/octet-stream         |
   +----------------------------------+----------------------------------+
   | Transfer Syntaxes Supported      | Any Transfer Syntax supported by |
   |                                  | the hosting EXAMPLE-PACS-ARCHIVE |
   | (Transfer-syntax Accept          |                                  |
   | parameter)                       |                                  |
   +----------------------------------+----------------------------------+
   | SOP Class Restrictions           | Restricted to Multi-Frame Image  |
   |                                  | Objects as defined in .          |
   +----------------------------------+----------------------------------+
   | Size Restriction                 | Restricted to size supported by  |
   |                                  | the hosting EXAMPLE-PACS-ARCHIVE |
   +----------------------------------+----------------------------------+

.. _sect_I.4.2.3.5:

WADO-RS Retrieve Bulk Data
''''''''''''''''''''''''''

.. table:: WADO-RS Retrieve Bulk Data

   +----------------------------------+----------------------------------+
   | **Options**                      | **Restrictions**                 |
   +==================================+==================================+
   | Data Types Supported (Accept     | Restricted to                    |
   | Type)                            | application/octet-stream         |
   +----------------------------------+----------------------------------+
   | Transfer Syntaxes Supported      | Any Transfer Syntax supported by |
   |                                  | the hosting EXAMPLE-PACS-ARCHIVE |
   | (Transfer-syntax Accept          |                                  |
   | parameter)                       |                                  |
   +----------------------------------+----------------------------------+
   | SOP Class Restrictions           | Restricted to SOP classes        |
   |                                  | supported by the hosting         |
   |                                  | EXAMPLE-PACS-ARCHIVE             |
   +----------------------------------+----------------------------------+
   | Size Restriction                 | Restricted to size supported by  |
   |                                  | the hosting EXAMPLE-PACS-ARCHIVE |
   +----------------------------------+----------------------------------+

.. _sect_I.4.2.3.6:

WADO-RS Retrieve Metadata
'''''''''''''''''''''''''

.. table:: WADO-RS Retrieve Metadata

   +----------------------------------+----------------------------------+
   | **Options**                      | **Restrictions**                 |
   +==================================+==================================+
   | Data Types Supported (Accept     | Restricted to                    |
   | Type)                            | application/dicom+xml            |
   +----------------------------------+----------------------------------+
   | Accept-Encoding                  | Restricted to gzip, deflate, or  |
   |                                  | identity (the use of no          |
   |                                  | transformation whatsoever). See  |
   |                                  | W3C RFC 2616 Protocol Parameters |
   |                                  | Section 3.5 for more information |
   |                                  | (http://www.w3.org/Proto         |
   |                                  | cols/rfc2616/rfc2616-sec3.html). |
   +----------------------------------+----------------------------------+
   | SOP Class Restrictions           | Restricted to SOP classes        |
   |                                  | supported by the hosting         |
   |                                  | EXAMPLE-PACS-ARCHIVE             |
   +----------------------------------+----------------------------------+
   | Size Restriction                 | Restricted to size supported by  |
   |                                  | the hosting EXAMPLE-PACS-ARCHIVE |
   +----------------------------------+----------------------------------+

.. _sect_I.4.2.3.7:

Connection Policies
'''''''''''''''''''

.. _sect_I.4.2.3.7.1:

General
       

All standard RS connection policies apply. There are no extensions for
RS options.

.. _sect_I.4.2.3.7.2:

Number of Connections
                     

EXAMPLE-WADO-SERVICE limits the number of simultaneous RS requests.
Additional requests will be queued after the HTTP connection is
accepted. When an earlier request completes, a pending request will
proceed.

.. table:: Number of Rs Requests Supported

   ========================================== ==================
   Maximum number of simultaneous RS requests 100 (configurable)
   ========================================== ==================

.. _sect_I.4.2.3.7.3:

Asynchronous Nature
                   

EXAMPLE-WADO-SERVICE does not support RS asynchronous response.

.. _sect_I.4.3:

Network Interfaces
~~~~~~~~~~~~~~~~~~

.. _sect_I.4.3.1:

Physical Network Interface
^^^^^^^^^^^^^^^^^^^^^^^^^^

EXAMPLE-WADO-SERVICE uses the network interface from the hosting
EXAMPLE-PACS-ARCHIVE. See its conformance claim for details.

.. _sect_I.4.3.2:

Additional Protocols
^^^^^^^^^^^^^^^^^^^^

EXAMPLE-WADO-SERVICE uses the network services from the hosting
EXAMPLE-PACS-ARCHIVE. See its conformance claim for details.

.. _sect_I.4.3.3:

IPv4 and IPv6 Support
^^^^^^^^^^^^^^^^^^^^^

This product supports both IPv4 and IPv6 connections.

.. _sect_I.4.4:

Configuration
~~~~~~~~~~~~~

.. _sect_I.4.4.1:

HTTP URI Interface
^^^^^^^^^^^^^^^^^^

The EXAMPLE-WADO-SERVICE can be configured to respond on two ports, one
for unprotected HTTP traffic and one for TLS protected traffic. The TLS
port will refuse any connection from a system that is not recognized as
authenticated by a known authority.

.. _sect_I.4.4.2:

WS Interface
^^^^^^^^^^^^

DICOM has retired the WADO-WS Service. See PS3.2-2017b. This product
still supports this service as described here.

The EXAMPLE-WADO-SERVICE can be configured to respond on either one or
two service endpoints. Each endpoint offers both of the services.

The WSDL file to be used by clients is made available at the location
http://<servername>/EXAMPLE-WADO-SERVICE?WSDL.

.. _sect_I.4.4.3:

RS Interface
^^^^^^^^^^^^

The EXAMPLE-WADO-SERVICE can be configured to respond on two ports, one
for unprotected HTTP traffic and one for TLS protected traffic. The TLS
port will refuse any connection from a system that is not recognized as
authenticated by a known authority.

.. _sect_I.5:

Media Interchange
-----------------

Not applicable

.. _sect_I.6:

Support of Character Sets
-------------------------

All EXAMPLE-WADO-SERVICEs support Unicode UTF-8 for all Web Services
transactions. The EXAMPLE-WADO-SERVICE does not convert character sets
when returning SOP Instances using DICOM encoding. The original DICOM
encoded character sets are preserved. When a PDF encoding is returned,
character set conversion is performed and the PDF is returned with a
UTF-8 encoding. JPEG renderings, will also utilize UTF-8 encoding for
internal labels.

See conformance claim for EXAMPLE-PACS-ARCHIVE for character sets used
within the DICOM instances.

.. _sect_I.7:

Security
--------

EXAMPLE-WADO-SERVICE supports transport level security measures for all
Web Services.

The EXAMPLE-WADO-SERVICE supports the following transport level security
measures:

-  HTTP BASIC Authorization over SSL

-  Digest Authorization

-  SSL Client Certificates

The transport level security measures are the support for bi-directional
authentication using TLS connections. The EXAMPLE-WADO-SERVICE can
provide it's certificate information, and can be configured with either
a direct comparison (self-signed) certificate or a chain of trust
certificate.

The EXAMPLE-WADO-SERVICE will refuse a connection over TLS from a source
that does not have a recognized authentication. For example, a
certificate authenticated by "Big Bank Corp." will not be accepted
unless the EXAMPLE-WADO-SERVICE has been configured to accept
authentications from "Big Bank Corp." The list of acceptable
certificates for EXAMPLE-WADO-SERVICE is not shared with certificates
used by other system applications and must be maintained independently.

The EXAMPLE-WADO-SERVICE can optionally be configured to support the
following session authentication mechanisms:

-  Kerberos Local Domain Sessions

-  Shibboleth Cross Domain Sessions (using SAML2.0)

.. _sect_I.8:

Annexes
-------

.. _sect_I.8.1:

IOD Contents
~~~~~~~~~~~~

See Conformance claim for the EXAMPLE-PACS-ARCHIVE.

.. _sect_I.8.3:

Coded Terminology and Templates
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

See conformance claim for EXAMPLE-PACS-ARCHIVE

.. _sect_I.8.4:

Grayscale Image Consistency
~~~~~~~~~~~~~~~~~~~~~~~~~~~

The EXAMPLE-WADO-SERVICE assumes that the JPEG images will be displayed
with monitors calibrated to the sRGB profile when rendering images.

.. _sect_I.8.5:

Standard Extended / Specialized / Private SOP Classes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

See conformance claim for EXAMPLE-PACS-ARCHIVE

.. _sect_I.8.6:

Private Transfer Syntaxes
~~~~~~~~~~~~~~~~~~~~~~~~~

If you request a DICOM object, it will not be returned in a private
transfer syntax.

