.. _chapter_K:

Conformance Statement Sample QIDO-RS Provider (Informative)
===========================================================

Disclaimer:

This document is an example DICOM Conformance Statement for a fictional
application service called EXAMPLE-QIDO-SERVICE produced by a fictional
vendor called EXAMPLE-PACS-PRODUCTS.

As stated in the annex title, this document is truly informative, and
not normative. A conformance statement of an actual product might
implement additional services and options as appropriate for its
specific purpose. In addition, an actual product might implement the
services described in a different manner and, for example, with
different characteristics and/or sequencing of activities. In other
words, this conformance statement example does not intend to standardize
a particular manner that a product might implement DICOM functionality.

.. _sect_K.0:

Cover Page
----------

Company Name: EXAMPLE-PACS-PRODUCTS

Product Name: EXAMPLE-QIDO-SERVICE

Version: 1.0-rev. A.1

Internal document number: 1024-xxx-yyy-zzz rev 1

Date: YYYYMMDD

.. _sect_K.1:

Conformance Statement Overview
------------------------------

This fictional product EXAMPLE-QIDO-SERVICE implements QIDO-RS, which
allow the client to search for studies, series or SOP instances stored
in an EXAMPLE-PACS-ARCHIVE. The EXAMPLE- QIDO-SERVICE is only available
as a plug in option for the EXAMPLE-PACS-ARCHIVE. All of the networking,
database, and other services are provided by the EXAMPLE-PACS-ARCHIVE.
This conformance claim refers to the conformance claim for the
EXAMPLE-PACS-ARCHIVE for all such services.

`table_title <#table_K.1-1>`__ provides an overview of the network
services supported by EXAMPLE-QIDO-SERVICE.

.. table:: Network Services

   +----------------------+----------------------+----------------------+
   | **Network Service**  | **User of Service    | **Provider of        |
   |                      | (Client)**           | Service (Server)**   |
   +======================+======================+======================+
   | **Query by ID for    |                      |                      |
   | DICOM Objects        |                      |                      |
   | (QIDO)**             |                      |                      |
   +----------------------+----------------------+----------------------+
   | QIDO-RS - Search for | No                   | Yes                  |
   | Studies              |                      |                      |
   +----------------------+----------------------+----------------------+
   | QIDO-RS - Search for | No                   | Yes                  |
   | Series               |                      |                      |
   +----------------------+----------------------+----------------------+
   | QIDO-RS - Search for | No                   | Yes                  |
   | Instances            |                      |                      |
   +----------------------+----------------------+----------------------+

.. _sect_K.2:

Table of Contents
-----------------

A table of contents shall be provided to assist readers in easily
finding the needed information.

.. _sect_K.3:

Introduction
------------

.. _sect_K.3.1:

Revision History
~~~~~~~~~~~~~~~~

.. table:: Revision History

   ==================== ================= ========== ======================
   **Document Version** **Date of Issue** **Author** **Description**
   ==================== ================= ========== ======================
   1.1                  October 24, 2011  WG-27      Version for Final Text
   1.2                  March 26, 2013    WG-27      Revised Introduction
   ==================== ================= ========== ======================

.. _sect_K.3.2:

Audience, Remarks, Terms and Definitions, Basics of DICOM Communication, Abbreviations, References
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

*See example text in*\ `Introduction <#sect_A.3>`__\ *.*

.. _sect_K.3.3:

Additional Remarks for This Example
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This document is a sample DICOM Conformance Statement created for DICOM
. It is to be used solely as an example to illustrate how to create a
DICOM Conformance Statement for a DICOM Service Class Provider (SCP).
The subject of the document, EXAMPLE-QIDO-SERVICE, is a fictional
product.

.. _sect_K.4:

Networking
----------

.. _sect_K.4.1:

Implementation Model
~~~~~~~~~~~~~~~~~~~~

.. _sect_K.4.1.1:

Application Data Flow
^^^^^^^^^^^^^^^^^^^^^

The QIDO-RS Provider Application receives QIDO requests from a remote
AE. These requests are HTTP GET requests. It is associated with the
local real-world activity "Query Remote Device". It uses the request to
select matching Studies, Series or Instances. It then returns a set of
matching Studies, Series or Instances or a response code indicating
warning or failure back to the requesting device.

.. _sect_K.4.1.2:

Functional Definition of AEs
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. _sect_K.4.1.2.1:

Functional Definition of QIDO Service Application
'''''''''''''''''''''''''''''''''''''''''''''''''

The reception of a QIDO-RS GET request will activate the QIDO-RS
Provider. An internal query request is sent to the search capabilities
of the associated PACS or Vendor Neutral Archive (VNA). The search
result is based upon the URL of the QIDO-RS GET request. The response is
a status code indicating the success, warning, or failure of the search
along with any matching results stored in the Remote PACS or VNA.

.. _sect_K.4.2:

AE Specifications
~~~~~~~~~~~~~~~~~

This AE complies with , specification for QIDO-RS.

.. _sect_K.4.2.1:

QIDO-RS Specifications
^^^^^^^^^^^^^^^^^^^^^^

.. _sect_K.4.2.1.1:

QIDO-RS Search for Studies
''''''''''''''''''''''''''

.. table:: QIDO-RS Search for Studies Specification

   +----------------------------+----------------------------------------+
   | **Parameter**              | **Restrictions**                       |
   +============================+========================================+
   | Media Types                | Restricted to "multipart/related;      |
   |                            | type=application/dicom+xml" or         |
   |                            | "application/dicom+json"               |
   +----------------------------+----------------------------------------+
   | Matching Attributes        | See `table_title <#table_K.4.2-1a>`__  |
   +----------------------------+----------------------------------------+
   | Return Attributes          | See `table_title <#table_K.4.2-1a>`__  |
   +----------------------------+----------------------------------------+
   | Limit and Offset supported | Yes                                    |
   +----------------------------+----------------------------------------+
   | Person Name Matching       | Literal, case insensitive. Section     |
   |                            | `Extended                              |
   |                            | Negotiation <#sect_K.4.2.2>`__.        |
   +----------------------------+----------------------------------------+

.. table:: QIDO-RS Study Attribute Matching

   ============================== ======== =================
   Keyword                        Tag      Types of Matching
   ============================== ======== =================
   **STUDY Level**                         
   StudyDate                      00080020 S,*,U,R
   StudyTime                      00080030 S,*,U,R
   AccessionNumber                00080050 S,*,U
   ModalitiesInStudy              00080061 S,*,U
   ReferringPhysiciansName        00080090 S,*,U
   StudyDescription               00081030 S,*,U
   PhysicianOfRecord              00081048 U
   PatientsName                   00100010 S,*,U
   PatientID                      00100020 S,*,U
   PatientBirthDate               00100030 NONE
   PatientSex                     00100040 NONE
   StudyInstanceUID               0020000D UNIQUE
   StudyID                        00200010 S,*,U
   NumberOfStudyRelatedSeries     00201206 NONE
   NumberOfStudyRelatedInstances  00201208 NONE
   RetrieveURL                    00081190 NONE
   **Common to all query levels**          
   InstanceAvailability           00080056 S,*,U
   SpecificCharacterSet           00080005 NONE
   RetrieveURL                    00081190 NONE
   ============================== ======== =================

Types of Matching (see ) :

"S" indicates the identifier attribute uses Single Value Matching

"L" indicates UID List Matching

"U" indicates Universal Matching.

.. note::

   If only Universal Matching is supported for an attribute then that
   attribute can only be passed as an "includefield" query key

"*" indicates wild card matching

"R" indicates Range Matching

"SEQUENCE" indicates Sequence Matching

"NONE" indicates that no matching is supported, but that values for this
Element requested will be returned with all requests

"UNIQUE" indicates that this is the Unique Key for that query level, in
which case Universal Matching or Single Value Matching is used depending
on the query level (see ).

.. _sect_K.4.2.1.2:

QIDO-RS Search for Series
'''''''''''''''''''''''''

.. table:: QIDO-RS Search for Series Specification

   +------------------------------+--------------------------------------+
   | **Parameter**                | **Restrictions**                     |
   +==============================+======================================+
   | Media Types                  | Restricted to "multipart/related;    |
   |                              | type=application/dicom+xml" or       |
   |                              | "application/dicom+json"             |
   +------------------------------+--------------------------------------+
   | Matching Attributes          | See                                  |
   |                              | `table_title <#table_K.4.2-2a>`__    |
   +------------------------------+--------------------------------------+
   | Return Attributes            | See                                  |
   |                              | `table_title <#table_K.4.2-2a>`__    |
   +------------------------------+--------------------------------------+
   | Limit and Offset supported   | Yes                                  |
   +------------------------------+--------------------------------------+
   | Relational Queries Supported | No                                   |
   +------------------------------+--------------------------------------+

.. table:: QIDO-RS Series Attribute Matching

   =============================== ======== =================
   Keyword                         Tag      Types of Matching
   =============================== ======== =================
   **SERIES Level**                         
   Modality                        00080060 S,*,U
   SeriesDescription               0008103E NONE
   SeriesInstanceUID               0020000E UNIQUE
   SeriesNumber                    00200011 S,*,U
   NumberOfSeriesRelatedInstances  00201209 NONE
   PerformedProcedureStepStartDate 00400244 S,*,U,R
   PerformedProcedureStepStartTime 00400245 S,*,U,R
   RequestAttributeSequence        00400275 SEQUENCE
   >ScheduledProcedureStepID       00400009 S,*,U
   >RequestedProcedureID           00401001 S,*,U
   **Common to all query levels**           
   InstanceAvailability            00080056 S,*,U
   SpecificCharacterSet            00080005 NONE
   RetrieveURL                     00081190 NONE
   =============================== ======== =================

Types of matching: Section `QIDO-RS Search for
Studies <#sect_K.4.2.1.1>`__.

.. _sect_K.4.2.1.3:

QIDO-RS Search for Instances
''''''''''''''''''''''''''''

.. table:: QIDO-RS Search for Instances Specification

   +------------------------------+--------------------------------------+
   | **Parameter**                | **Restrictions**                     |
   +==============================+======================================+
   | Media Types                  | Restricted to "multipart/related;    |
   |                              | type=application/dicom+xml" or       |
   |                              | "application/dicom+json"             |
   +------------------------------+--------------------------------------+
   | Matching Attributes          | See                                  |
   |                              | `table_title <#table_K.4.2-3a>`__    |
   +------------------------------+--------------------------------------+
   | Return Attributes            | See                                  |
   |                              | `table_title <#table_K.4.2-3a>`__    |
   +------------------------------+--------------------------------------+
   | Limit and Offset supported   | Yes                                  |
   +------------------------------+--------------------------------------+
   | Relational Queries Supported | Series-level, only                   |
   +------------------------------+--------------------------------------+

.. table:: QIDO-RS Instance Attribute Matching

   =============================== ======== =================
   Keyword                         Tag      Types of Matching
   =============================== ======== =================
   **SERIES Level**                         
   Modality                        00080060 S,*,U
   SeriesDescription               0008103E NONE
   SeriesInstanceUID               0020000E UNIQUE
   SeriesNumber                    00200011 S,*,U
   NumberOfSeriesRelatedInstances  00201209 NONE
   PerformedProcedureStepStartDate 00400244 S,*,U,R
   PerformedProcedureStepStartTime 00400245 S,*,U,R
   RequestAttributeSequence        00400275 SEQUENCE
   >ScheduledProcedureStepID       00400009 S,*,U
   >RequestedProcedureID           00401001 S,*,U
   **COMPOSITE INSTANCE Level**             
   SOPClassUID                     00080016 L
   SOPInstanceUID                  00080018 UNIQUE
   InstanceNumber                  00200013 S,*,U
   Rows                            00280010 NONE
   Columns                         00280011 NONE
   BitsAllocated                   00280100 NONE
   NumberOfFrames                  00280008 NONE
   **Common to all query levels**           
   InstanceAvailability            00080056 S,*,U
   SpecificCharacterSet            00080005 NONE
   RetrieveURL                     00081190 NONE
   =============================== ======== =================

Types of matching: Section `QIDO-RS Search for
Studies <#sect_K.4.2.1.1>`__.

.. _sect_K.4.2.1.4:

Connection Policies
'''''''''''''''''''

.. _sect_K.4.2.1.4.1:

General
       

All standard RS connection policies apply. There are no extensions for
RS options.

.. _sect_K.4.2.1.4.2:

Number of Connections
                     

EXAMPLE-QIDO-SERVICE limits the number of simultaneous RS requests.
Additional requests will be queued after the HTTP connection is
accepted. When an earlier request completes, a pending request will
proceed.

.. table:: Number of HTTP Requests Supported

   ========================================== ==================
   Maximum number of simultaneous RS requests 100 (configurable)
   ========================================== ==================

.. _sect_K.4.2.1.4.3:

Asynchronous Nature
                   

EXAMPLE-QIDO-SERVICE does not support RS asynchronous response.

.. _sect_K.4.2.1.4.4:

Response Status
               

The EXAMPLE-QIDO-SERVICE shall provide a response message header
containing the appropriate status code indicating success, warning, or
failure as shown in `table_title <#table_K.4.2-5>`__.

.. table:: HTTP Standard Response Codes

   +----------+--------------------------+----------------------------+
   | **Code** | **Name**                 | **Description**            |
   +==========+==========================+============================+
   | Success  |                          |                            |
   +----------+--------------------------+----------------------------+
   | 200      | OK                       | The query completed and    |
   |          |                          | any matching results are   |
   |          |                          | returned in the message    |
   |          |                          | body.                      |
   +----------+--------------------------+----------------------------+
   | Failure  |                          |                            |
   +----------+--------------------------+----------------------------+
   | 400      | Bad Request              | This indicates that the    |
   |          |                          | QIDO-RS Provider was       |
   |          |                          | unable to fulfill it       |
   |          |                          | because it cannot          |
   |          |                          | understand the query       |
   |          |                          | component.                 |
   +----------+--------------------------+----------------------------+
   | 401      | Unauthorized             | This indicates that the    |
   |          |                          | QIDO-RS Provider refused   |
   |          |                          | to fulfill it because the  |
   |          |                          | client is not authorized.  |
   +----------+--------------------------+----------------------------+
   | 403      | Forbidden                | This indicates that the    |
   |          |                          | QIDO-RS Provider           |
   |          |                          | understood the request,    |
   |          |                          | but is refusing to fulfill |
   |          |                          | it (e.g., no single        |
   |          |                          | patient specified, an      |
   |          |                          | authorized user with       |
   |          |                          | insufficient privileges,   |
   |          |                          | etc.).                     |
   +----------+--------------------------+----------------------------+
   | 413      | Request entity too large | This indicates that the    |
   |          |                          | query was too broad and a  |
   |          |                          | narrower query or paging   |
   |          |                          | should be requested. This  |
   |          |                          | code will be returned for  |
   |          |                          | queries that do not        |
   |          |                          | specify PatientID.         |
   +----------+--------------------------+----------------------------+
   | 503      | Busy                     | Service is unavailable.    |
   +----------+--------------------------+----------------------------+

.. _sect_K.4.2.2:

Extended Negotiation
^^^^^^^^^^^^^^^^^^^^

EXAMPLE-QIDO-SERVICE does not support the "fuzzymatching" query key.

EXAMPLE-QIDO-SERVICE will perform case insensitive matching for PN VR
attributes but will not perform other forms of fuzzy matching. This
applies to the following attributes:

-  Referring Physician's Name (0008,0090)

-  Physician(s) of Record (0008,1048)

-  Patient's Name (0010,0010)

.. _sect_K.4.3:

Network Interfaces
~~~~~~~~~~~~~~~~~~

.. _sect_K.4.3.1:

Physical Network Interface
^^^^^^^^^^^^^^^^^^^^^^^^^^

EXAMPLE-QIDO-SERVICE uses the network interface from the hosting
EXAMPLE-PACS-ARCHIVE. See its conformance claim for details.

.. _sect_K.4.3.2:

Additional Protocols
^^^^^^^^^^^^^^^^^^^^

EXAMPLE-QIDO-SERVICE uses the network services from the hosting
EXAMPLE-PACS-ARCHIVE. See its conformance claim for details.

.. _sect_K.4.3.3:

IPv4 and IPv6 Support
^^^^^^^^^^^^^^^^^^^^^

This product supports both IPv4 and IPv6 connections.

.. _sect_K.4.4:

Configuration
~~~~~~~~~~~~~

.. _sect_K.4.4.1:

QIDO-RS Interface
^^^^^^^^^^^^^^^^^

The EXAMPLE-QIDO-SERVICE can be configured to respond on one port for
TLS protected traffic. The TLS port will refuse any connection from a
system that is not recognized as authenticated by a known authority.

.. _sect_K.5:

Media Interchange
-----------------

Not applicable

.. _sect_K.6:

Support of Character Sets
-------------------------

EXAMPLE-QIDO-SERVICE supports Unicode UTF-8 for all RS transactions.

See conformance claim for EXAMPLE-PACS-ARCHIVE for character sets used
within the DICOM instances.

.. _sect_K.7:

Security
--------

The EXAMPLE-QIDO-SERVICE supports the following transport level security
measures:

-  HTTP BASIC Authorization over SSL

-  Digest Authorization

-  SSL Client Certificates

The transport level security measures support bi-directional
authentication using TLS connections. The EXAMPLE-QIDO-SERVICE can
provide its certificate information, and can be configured with either a
direct comparison (self-signed) certificate or a chain of trust
certificate.

The EXAMPLE-QIDO-SERVICE will refuse a connection over TLS from a source
that does not have a recognized authentication. For example, a
certificate authenticated by "Big Hospital Provider." will not be
accepted unless the EXAMPLE-QIDO-SERVICE has been configured to accept
authentications from "Big Hospital Provider." The list of acceptable
certificates for EXAMPLE-QIDO-SERVICE is not shared with certificates
used by other system applications and must be maintained independently.

The EXAMPLE-QIDO-SERVICE can optionally be configured to use the
following session authentication mechanisms:

-  Kerberos Local Domain Sessions

-  Shibboleth Cross Domain Sessions (using SAML2.0)

-  OAuth 2.0 complying with IHE ITI Internet User Authentication (IUA)
   Profile

