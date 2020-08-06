.. _chapter_H:

DICOM Conformance Statement Medication-System-Gateway (Informative)
===================================================================

Disclaimer:

This document is an example DICOM Conformance Statement for a fictional
device called EXAMPLE-MEDICATION-SYSTEM-GATEWAY, which is a networked
computer system used to provide radiology systems with access to a
pharmacy system and a medication administration record system.

As stated in the annex title, this document is truly informative, and
not normative. A conformance statement of an actual product might
implement additional services and options as appropriate for its
specific purpose. In addition, an actual product might implement the
services described in a different manner and, for example, with
different characteristics and/or sequencing of activities. In other
words, this conformance statement example does not intend to standardize
a particular manner that a product might implement DICOM functionality.

.. _sect_H.0:

Cover Page
----------

Company Name: EXAMPLE-GATEWAY-PRODUCTS.

Product Name: EXAMPLE-MEDICATION-SYSTEM-GATEWAY

Version: 1.0-rev. A.1

Internal document number: 4226-xxx-yyy-zzz rev 1

Date: YYYYMMDD

.. _sect_H.1:

Conformance Statement Overview
------------------------------

The EXAMPLE-MEDICATION-SYSTEM-GATEWAY is a networked computer system
used to provide radiology systems with access to a pharmacy system and a
medication administration record system. It allows imaging modalities
systems and departmental information systems to retrieve information
about drugs and contrast agents, to verify that administration of a drug
or contrast agent to a particular patient is allowed, and to record the
administration of a drug or contrast agent to a patient.

.. table:: Network Services

   +----------------------+----------------------+----------------------+
   | SOP Classes          | User of Service      | Provider of Service  |
   |                      | (SCU)                | (SCP)                |
   +======================+======================+======================+
   | **Workflow           |                      |                      |
   | Management**         |                      |                      |
   +----------------------+----------------------+----------------------+
   | Substance            | No                   | Yes                  |
   | Administration       |                      |                      |
   | Logging              |                      |                      |
   +----------------------+----------------------+----------------------+
   | Query/Retrieve       |                      |                      |
   +----------------------+----------------------+----------------------+
   | Product              | No                   | Yes                  |
   | Characteristics      |                      |                      |
   | Query                |                      |                      |
   +----------------------+----------------------+----------------------+
   | Substance Approval   | No                   | Yes                  |
   | Query                |                      |                      |
   +----------------------+----------------------+----------------------+

.. _sect_H.2:

Table of Contents
-----------------

A table of contents shall be provided to assist readers in easily
finding the needed information.

.. _sect_H.3:

Introduction
------------

.. _sect_H.3.1:

Revision History
~~~~~~~~~~~~~~~~

.. table:: Revision History

   ================ ================ ========= ======================
   Document Version Date             Author    Description
   ================ ================ ========= ======================
   1.1              October 30, 2006 DICOM WG6 Version for Final Text
   1.2              August 30, 2007  WG 6      Revised Introduction
   ================ ================ ========= ======================

.. _sect_H.3.2:

Audience,Remarks,Terms and Definitions, Basics of DICOM Communication, Abbreviations, References
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

*See example text in*\ `Introduction <#sect_A.3>`__\ *.*

.. _sect_H.3.3:

Additional Remarks for This Example
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The EXAMPLE-MEDICATION-SYSTEM-GATEWAY relies on the associated, but
independent, Pharmacy and Medication Administration Record Systems to
fulfill the medical application functions implicit in the DICOM services
supported. In particular, these functions are part of a critical patient
safety workflow. However, those patient safety functions are not
specified by DICOM, and they are not fully described by this Conformance
Statement. Please see the product specifications of the Pharmacy and
Medication Administration Record Systems for full details on the
clinical decision support and records management features of those
systems.

This document is a sample DICOM Conformance Statement created for DICOM
. It is to be used solely as an example to illustrate how to create a
DICOM Conformance Statement for a server supporting the DICOM Substance
Administration Information Services. The subject of the document,
EXAMPLE-MEDICATION-SYSTEM-GATEWAY, is a fictional product.

.. _sect_H.4:

Networking
----------

.. _sect_H.4.1:

Implementation Model
~~~~~~~~~~~~~~~~~~~~

.. _sect_H.4.1.1:

Application Data Flow
^^^^^^^^^^^^^^^^^^^^^

The division of EXAMPLE-MEDICATION-SYSTEM-GATEWAY into the separate
DICOM Application Entities represents their independent logical
functionality.

By default all of the defined Application Entities have different AE
Titles. However, EXAMPLE-MEDICATION-SYSTEM-GATEWAY can be configured so
that the PHARMACY-SCP AE and MAR-SCP AE share the same Application
Entity Title.

.. _sect_H.4.1.2:

Functional Definition of AEs
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. _sect_H.4.1.2.1:

Functional Definition of PHARMACY-SCP Application Entity
''''''''''''''''''''''''''''''''''''''''''''''''''''''''

The PHARMACY-SCP AE handles incoming external queries for pharmacy (drug
and contrast agent) product data, and also handles requests for approval
of administration of pharmacy product. The PHARMACY-SCP AE handles
queries by translating the standard DICOM queries to the non-standard
interface of the Pharmacy Information System and the Patient
Registration System.

The PHARMACY-SCP AE waits for another application to connect at the
presentation address configured for its Application Entity Title.
PHARMACY-SCP AE will accept Associations with Presentation Contexts for
SOP Classes of the DICOM Substance Administration Information Service
Class, and Verification Service Class. It will handle query requests on
these Presentation Contexts and respond with values corresponding to the
information provided by the Pharmacy Information System.

.. _sect_H.4.1.2.2:

Functional Definition of MAR-SCP Application Entity
'''''''''''''''''''''''''''''''''''''''''''''''''''

The MAR-SCP AE receives incoming DICOM notifications of drug or contrast
agent administration, and adds them to the Medication Administration
Record System database.

The MAR-SCP AE waits for another application to connect at the
presentation address configured for its Application Entity Title. The
MAR-SCP AE will accept Associations with Presentation Contexts for SOP
Classes of the Substance Administration Logging and Verification SOP
Classes. Any drug or contrast agent administration images notifications
received on such Presentation Contexts will be added to the Medication
Administration Record System database.

.. _sect_H.4.1.3:

Sequencing of Real-World Activities
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

There are no sequencing constraints across the
EXAMPLE-MEDICATION-SYSTEM-GATEWAY Application Entities. Each query or
notification is handled independently.

.. _sect_H.4.2:

AE Specifications
~~~~~~~~~~~~~~~~~

.. _sect_H.4.2.1:

PHARMACY-SCP Application Entity Specification
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. _sect_H.4.2.1.1:

SOP Classes
'''''''''''

The PHARMACY-SCP AE provides Standard Conformance to the following DICOM
SOP Classes:

.. table:: SOP Classes for PHARMACY-SCP AE

   ============================= ====================== ======= =======
   **SOP Class Name**            **SOP Class UID**      **SCU** **SCP**
   ============================= ====================== ======= =======
   Verification                  1.2.840.10008.1.1      No      Yes
   Product Characteristics Query 1.2.840.10008.5.1.4.41 No      Yes
   Substance Approval Query      1.2.840.10008.5.1.4.42 No      Yes
   ============================= ====================== ======= =======

.. _sect_H.4.2.1.2:

Association Policies
''''''''''''''''''''

.. _sect_H.4.2.1.2.1:

General
       

The PHARMACY-SCP AE will never initiate Associations; it only accepts
Association Requests from external DICOM AEs. The PHARMACY-SCP AE will
accept Associations for Verification (C-ECHO) and Query (C-FIND)
requests.

The DICOM standard Application Context Name for DICOM is always
accepted:

.. table:: DICOM Application Context for PHARMACY-SCP AE

   ======================== =====================
   Application Context Name 1.2.840.10008.3.1.1.1
   ======================== =====================

.. _sect_H.4.2.1.2.2:

Number of Associations
                      

The PHARMACY-SCP AE can support multiple simultaneous Associations. Each
time the PHARMACY-SCP AE receives an Association, a child process will
be spawned to process the Verification or Query request. The maximum
number of child processes, and thus the maximum number of simultaneous
Associations that can be processed, is set by configuration. The default
maximum is 10 in total.

.. table:: Number of Simultaneous Associations as a SCP for PHARMACY-SCP
AE

   =========================================== =================
   Maximum number of simultaneous Associations 10 (Configurable)
   =========================================== =================

.. _sect_H.4.2.1.2.3:

Asynchronous Nature
                   

The PHARMACY-SCP AE does not support asynchronous communication
(multiple outstanding transactions over a single Association). All
Association requests must be completed and acknowledged before a new
operation can be initiated.

.. table:: Asynchronous Nature as a SCP for PHARMACY-SCP AE

   +----------------------------------------------+----------------------+
   | Maximum number of outstanding asynchronous   | 1 (Not Configurable) |
   | transactions                                 |                      |
   +----------------------------------------------+----------------------+

.. _sect_H.4.2.1.2.4:

Implementation Identifying Information
                                      

The implementation information for the Application Entity is:

.. table:: DICOM Implementation Class and Version for PHARMACY-SCP AE

   =========================== ======================
   Implementation Class UID    1.840.xxxxxxx.yyy.etc…
   Implementation Version Name EX_VERS_01
   =========================== ======================

Note that all EXAMPLE-MEDICATION-SYSTEM-GATEWAY AEs use the same
Implementation Class UID and Implementation Version Name. This Version
Name is updated with each new release of the product software, as the
different AE versions are never released independently.

.. _sect_H.4.2.1.3:

Association Initiation Policy
'''''''''''''''''''''''''''''

The PHARMACY-SCP AE does not initiate Associations.

.. _sect_H.4.2.1.4:

Association Acceptance Policy
'''''''''''''''''''''''''''''

.. _sect_H.4.2.1.4.1:

Activity - Handling Query Requests
                                  

.. _sect_H.4.2.1.4.1.1:

Description and Sequencing of Activity
                                      

The PHARMACY-SCP AE accepts Associations only if they have valid
Presentation Contexts. If none of the requested Presentation Contexts
are accepted then the Association Request itself is rejected. It can be
configured to only accept Associations with certain hosts (using TCP/IP
address) and/or Application Entity Titles.

The following sequencing applies to the PHARMACY-SCP AE for handling
queries (C-FIND-Requests) :

1. Peer AE opens an Association with the PHARMACY-SCP AE.

2. Peer AE sends a C-FIND-RQ Message

3. If the query is for a Substance Administration Approval, PHARMACY-SCP
   AE requests basic patient demographic data (e.g., name, sex) from the
   Patient Registration System

4. PHARMACY-SCP AE translates the query into a request for the Pharmacy
   Information System (for either Product Information or for Substance
   Administration Approval), which responds with the requested data (or
   an indication of no matching data for the query).

5. If matching information is provided, PHARMACY-SCP AE returns a
   C-FIND-RSP Message to the peer AE with the matching information.

6. A final C-FIND-RSP is sent indicating that the matching is complete.

7. Peer AE closes the Association. Note that the peer AE does not have
   to close the Association immediately. Further C-FIND Requests can be
   sent over the Association before it is closed.

The PHARMACY-SCP AE may reject Association attempts as shown in the
table below. The Result, Source and Reason/Diag columns represent the
values returned in the corresponding fields of an ASSOCIATE-RJ PDU (see
). The following abbreviations are used in the Source column:

a. 1 - DICOM UL service-user

b. 2 - DICOM UL service-provider (ASCE related function)

c. 3 - DICOM UL service-provider (Presentation related function)

.. table:: Association Rejection Reasons

   +------------------+--------+------------------+------------------+
   | Result           | Source | Reason/Diag      | Explanation      |
   +==================+========+==================+==================+
   | 2 -              | c      | 2 -              | The              |
   | re               |        | loca             | (configurable)   |
   | jected-transient |        | l-limit-exceeded | maximum number   |
   |                  |        |                  | of simultaneous  |
   |                  |        |                  | Associations has |
   |                  |        |                  | been reached. An |
   |                  |        |                  | Association      |
   |                  |        |                  | request with the |
   |                  |        |                  | same parameters  |
   |                  |        |                  | may succeed at a |
   |                  |        |                  | later time.      |
   +------------------+--------+------------------+------------------+
   | 2 -              | c      | 1 -              | No Associations  |
   | re               |        | temp             | can be accepted  |
   | jected-transient |        | orary-congestion | at this time due |
   |                  |        |                  | to the real-time |
   |                  |        |                  | requirements of  |
   |                  |        |                  | higher priority  |
   |                  |        |                  | activities or    |
   |                  |        |                  | because          |
   |                  |        |                  | insufficient     |
   |                  |        |                  | resources are    |
   |                  |        |                  | available (e.g., |
   |                  |        |                  | memory,          |
   |                  |        |                  | processes,       |
   |                  |        |                  | threads). An     |
   |                  |        |                  | Association      |
   |                  |        |                  | request with the |
   |                  |        |                  | same parameters  |
   |                  |        |                  | may succeed at a |
   |                  |        |                  | later time.      |
   +------------------+--------+------------------+------------------+
   | 1 -              | a      | 2 -              | The Association  |
   | re               |        | applic           | request          |
   | jected-permanent |        | ation-context-na | contained an     |
   |                  |        | me-not-supported | unsupported      |
   |                  |        |                  | Application      |
   |                  |        |                  | Context Name. An |
   |                  |        |                  | association      |
   |                  |        |                  | request with the |
   |                  |        |                  | same parameters  |
   |                  |        |                  | will not succeed |
   |                  |        |                  | at a later time. |
   +------------------+--------+------------------+------------------+
   | 1 -              | a      | 7 -              | The Association  |
   | re               |        | called-AE-titl   | request          |
   | jected-permanent |        | e-not-recognized | contained an     |
   |                  |        |                  | unrecognized     |
   |                  |        |                  | Called AE Title. |
   |                  |        |                  | An Association   |
   |                  |        |                  | request with the |
   |                  |        |                  | same parameters  |
   |                  |        |                  | will not succeed |
   |                  |        |                  | at a later time  |
   |                  |        |                  | unless           |
   |                  |        |                  | configuration    |
   |                  |        |                  | changes are      |
   |                  |        |                  | made. This       |
   |                  |        |                  | rejection reason |
   |                  |        |                  | normally occurs  |
   |                  |        |                  | when the         |
   |                  |        |                  | Association      |
   |                  |        |                  | initiator is     |
   |                  |        |                  | incorrectly      |
   |                  |        |                  | configured and   |
   |                  |        |                  | attempts to      |
   |                  |        |                  | address the      |
   |                  |        |                  | Association      |
   |                  |        |                  | acceptor using   |
   |                  |        |                  | the wrong AE     |
   |                  |        |                  | Title.           |
   +------------------+--------+------------------+------------------+
   | 1 -              | a      | 3 -              | The Association  |
   | re               |        | calling-AE-titl  | request          |
   | jected-permanent |        | e-not-recognized | contained an     |
   |                  |        |                  | unrecognized     |
   |                  |        |                  | Calling AE       |
   |                  |        |                  | Title. An        |
   |                  |        |                  | Association      |
   |                  |        |                  | request with the |
   |                  |        |                  | same parameters  |
   |                  |        |                  | will not succeed |
   |                  |        |                  | at a later time  |
   |                  |        |                  | unless           |
   |                  |        |                  | configuration    |
   |                  |        |                  | changes are      |
   |                  |        |                  | made. This       |
   |                  |        |                  | rejection reason |
   |                  |        |                  | normally occurs  |
   |                  |        |                  | when the         |
   |                  |        |                  | Association      |
   |                  |        |                  | acceptor has not |
   |                  |        |                  | been configured  |
   |                  |        |                  | to recognize the |
   |                  |        |                  | AE Title of the  |
   |                  |        |                  | Association      |
   |                  |        |                  | initiator.       |
   +------------------+--------+------------------+------------------+
   | 1 -              | b      | 1 -              | The Association  |
   | re               |        | no-reason-given  | request could    |
   | jected-permanent |        |                  | not be parsed.   |
   |                  |        |                  | An Association   |
   |                  |        |                  | request with the |
   |                  |        |                  | same format will |
   |                  |        |                  | not succeed at a |
   |                  |        |                  | later time.      |
   +------------------+--------+------------------+------------------+

The PHARMACY-SCP AE will close the Association under the exceptional
circumstances listed in `table_title <#table_H.4.2-7>`__.

.. table:: PHARMACY-SCP AE Communication Failure Behavior

   +----------------------------------+----------------------------------+
   | Exception                        | Behavior                         |
   +==================================+==================================+
   | Timeout expiry for an expected   | The Association is aborted by    |
   | DICOM Message Request (DIMSE     | issuing a DICOM A-ABORT.         |
   | level timeout). I.e. The         |                                  |
   | PHARMACY-SCP AE is waiting for   | Error message is output to the   |
   | the next C-FIND Request on an    | Service Audit Trail.             |
   | open Association but the timer   |                                  |
   | expires.                         |                                  |
   +----------------------------------+----------------------------------+
   | Timeout expiry for an expected   | The Association is aborted by    |
   | DICOM PDU or TCP/IP packet       | issuing a DICOM A-ABORT.         |
   | (Low-level timeout). I.e. The    |                                  |
   | PHARMACY-SCP AE is waiting for   | Error message is output to the   |
   | the next message PDU but the     | Service Audit Trail.             |
   | timer expires.                   |                                  |
   +----------------------------------+----------------------------------+
   | Association aborted by the SCU   | Error message is output to the   |
   | or the network layers indicate   | Service Audit Trail.             |
   | communication loss (i.e.,        |                                  |
   | low-level TCP/IP socket closure) |                                  |
   +----------------------------------+----------------------------------+

.. _sect_H.4.2.1.4.1.2:

Accepted Presentation Contexts
                              

The PHARMACY-SCP AE will accept Presentation Contexts as shown in
`table_title <#table_H.4.2-8>`__.

.. table:: Accepted Presentation Contexts By the PHARMACY-SCP AE

   +------------+------------+------------+------------+-----+------+
   | Pr         |            |            |            |     |      |
   | esentation |            |            |            |     |      |
   | Context    |            |            |            |     |      |
   | Table      |            |            |            |     |      |
   +============+============+============+============+=====+======+
   | Ve         | 1.2.840    | DICOM      | 1.2.840    | SCP | None |
   | rification | .10008.1.1 | Implicit   | .10008.1.2 |     |      |
   |            |            | VR Little  |            |     |      |
   |            |            | Endian     |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | Product    | 1.         | DICOM      | 1.2.840    | SCP | None |
   | Chara      | 2.840.1000 | Implicit   | .10008.1.2 |     |      |
   | cteristics | 8.5.1.4.41 | VR Little  |            |     |      |
   | Query      |            | Endian     |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | DICOM      | 1.2.840.1  |            |            |     |      |
   | Explicit   | 0008.1.2.1 |            |            |     |      |
   | VR Little  |            |            |            |     |      |
   | Endian     |            |            |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | Substance  | 1.         | DICOM      | 1.2.840    | SCP | None |
   | Approval   | 2.840.1000 | Implicit   | .10008.1.2 |     |      |
   | Query      | 8.5.1.4.42 | VR Little  |            |     |      |
   |            |            | Endian     |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | DICOM      | 1.2.840.1  |            |            |     |      |
   | Explicit   | 0008.1.2.1 |            |            |     |      |
   | VR Little  |            |            |            |     |      |
   | Endian     |            |            |            |     |      |
   +------------+------------+------------+------------+-----+------+

.. _sect_H.4.2.1.4.1.3:

SOP Specific Conformance for Verification SOP Class
                                                   

The PHARMACY -SCP AE provides standard conformance to the Verification
SOP Class as an SCP.

.. _sect_H.4.2.1.4.1.4:

SOP Specific Conformance for Product Characteristics Query SOP Class
                                                                    

The PHARMACY-SCP AE supports the Return Key Attributes shown in Tables
H.4.2-9 and H.4.2-10. Only those attributes requested in the query
identifier are returned. Note that queries about devices are not
supported.

.. table:: Return Key Attributes Supported for Product Characteristics
Query

   +--------------------------+-------------+--------------------------+
   | Product Package          | (0044,0001) | Returned with query      |
   | Identifier               |             | match value              |
   +==========================+=============+==========================+
   | Product Type Code        | (0044,0007) | RxNorm coded type of     |
   | Sequence                 |             | drug                     |
   +--------------------------+-------------+--------------------------+
   | Manufacturer             | (0008,0070) |                          |
   +--------------------------+-------------+--------------------------+
   | Product Name             | (0044,0008) |                          |
   +--------------------------+-------------+--------------------------+
   | Product Description      | (0044,0009) |                          |
   +--------------------------+-------------+--------------------------+
   | Product Lot Identifier   | (0044,000A) |                          |
   +--------------------------+-------------+--------------------------+
   | Product Expiration       | (0044,000B) |                          |
   | DateTime                 |             |                          |
   +--------------------------+-------------+--------------------------+
   | Product Parameter        | (0044,0013) | See                      |
   | Sequence                 |             | `table_ti                |
   |                          |             | tle <#table_H.4.2-10>`__ |
   |                          |             | for parameters supported |
   +--------------------------+-------------+--------------------------+
   | Pertinent Documents      | (0038,0100) | Zero or one item         |
   | Sequence                 |             | returned                 |
   +--------------------------+-------------+--------------------------+
   | >Retrieve URI            | (0040,E010) |                          |
   +--------------------------+-------------+--------------------------+

.. table:: Product Parameter Sequence Item Concepts Supported

   +----------------------------------------------------------------------+
   | **Concept Name Code Sequence (0040,A043)**                           |
   +======================================================================+
   | `(118565006, SCT, "Volume") <http://snomed.info/id/118565006>`__     |
   +----------------------------------------------------------------------+
   | `(127489000, SCT, "Active                                            |
   | Ingredient") <http://snomed.info/id/127489000>`__                    |
   +----------------------------------------------------------------------+

Only the ASCII (DICOM Default) character set is supported by the
Pharmacy Information System; Specific Character Set (0008,0005) is not
used.

.. _sect_H.4.2.1.4.1.5:

SOP Specific Conformance for Substance Approval Query SOP Class
                                                               

The PHARMACY-SCP AE supports the Matching Key Attributes shown in
`table_title <#table_H.4.2-11>`__. It can be configured to match on
Patient ID, or on Admission ID, or on a combination of Patient ID and
Issuer of Patient ID, or on a combination of Admission ID and Issuer of
Admission ID. As required by the SOP Class, one of Patient ID or
Admission ID must be present in the query, as must Product Package
Identifier and Administration Route Code Sequence. Note, however, that
the Pharmacy Information System does not support verification of
administration route. Also note that queries about devices are not
supported.

.. table:: Matching Key Attributes Supported for Substance Approval
Query

   ================================== ===========
   Patient ID                         (0010,0020)
   Issuer of Patient ID               (0010,0021)
   Admission ID                       (0038,0010)
   Issuer of Admission ID             (0038,0011)
   Product Package Identifier         (0044,0001)
   Administration Route Code Sequence (0054,0302)
   >Code Value                        (0008,0100)
   >Coding Scheme Designator          (0008,0102)
   ================================== ===========

The PHARMACY-SCP AE supports the Return Key Attributes shown in
`table_title <#table_H.4.2-12>`__. Only those attributes requested in
the query identifier are returned.

.. table:: Return Key Attributes Supported for Substance Approval Query

   +--------------------------+-------------+--------------------------+
   | Patient's Name           | (0010,0010) | Obtained from Patient    |
   |                          |             | Registration System      |
   +==========================+=============+==========================+
   | Patient ID               | (0010,0020) | Obtained from Patient    |
   |                          |             | Registration System if   |
   |                          |             | AE configured for        |
   |                          |             | Admission ID matching,   |
   |                          |             | or Admission ID + Issuer |
   |                          |             | of Admission ID matching |
   +--------------------------+-------------+--------------------------+
   | Issuer of Patient ID     | (0010,0021) | Returned only if AE      |
   |                          |             | configured for Patient   |
   |                          |             | ID + Issuer of Patient   |
   |                          |             | ID matching              |
   +--------------------------+-------------+--------------------------+
   | Patient's Birth Date     | (0010,0030) | Obtained from Patient    |
   |                          |             | Registration System      |
   +--------------------------+-------------+--------------------------+
   | Patient's Sex            | (0010,0040) | Obtained from Patient    |
   |                          |             | Registration System      |
   +--------------------------+-------------+--------------------------+
   | Admission ID             | (0038,0010) | Returned only if AE      |
   |                          |             | configured for Admission |
   |                          |             | ID matching, or          |
   |                          |             | Admission ID + Issuer of |
   |                          |             | Admission ID matching    |
   +--------------------------+-------------+--------------------------+
   | Issuer of Admission ID   | (0038,0011) | Returned only if AE      |
   |                          |             | configured for Admission |
   |                          |             | ID + Issuer of Admission |
   |                          |             | ID matching              |
   +--------------------------+-------------+--------------------------+
   | Product Package          | (0044,0001) | Returned with query      |
   | Identifier               |             | match value              |
   +--------------------------+-------------+--------------------------+
   | Administration Route     | (0054,0302) | Returned with query      |
   | Code Sequence            |             | match value              |
   +--------------------------+-------------+--------------------------+
   | Substance Administration | (0044,0002) | Obtained from Pharmacy   |
   | Approval                 |             | Information System       |
   +--------------------------+-------------+--------------------------+
   | Approval Status Further  | (0044,0003) | Obtained from Pharmacy   |
   | Description              |             | Information System       |
   +--------------------------+-------------+--------------------------+
   | Approval Status DateTime | (0044,0004) |                          |
   +--------------------------+-------------+--------------------------+

Specific Character Set (0008,0005) is returned with value ISO_IR 192 if
the Patient Registration System provides non-ASCII Unicode characters in
Patient Name.

.. _sect_H.4.2.1.4.1.6:

PHARMACY-SCP AE C-FIND Response Behavior
                                        

The PHARMACY-SCP AE supports the C-FIND Response Status return values
and behavior shown in `table_title <#table_H.4.2-13>`__.

.. table:: PHARMACY-SCP AE C-FIND Response Status Return Behavior

   +----------------+----------------+----------------+----------------+
   | Service Status | Further        | Error Code     | Behavior       |
   |                | Meaning        |                |                |
   +================+================+================+================+
   | Success        | Success        | 0000           | Matching is    |
   |                |                |                | complete. No   |
   |                |                |                | final          |
   |                |                |                | identifier is  |
   |                |                |                | supplied.      |
   +----------------+----------------+----------------+----------------+
   | Failure        | Out of         | A700           | System reached |
   |                | Resources      |                | the limit in   |
   |                |                |                | memory usage   |
   |                |                |                | for queuing    |
   |                |                |                | requests to    |
   |                |                |                | the Pharmacy   |
   |                |                |                | Information    |
   |                |                |                | System.        |
   |                |                |                |                |
   |                |                |                | Error message  |
   |                |                |                | is output to   |
   |                |                |                | as an alert to |
   |                |                |                | the Service    |
   |                |                |                | Audit Trail.   |
   +----------------+----------------+----------------+----------------+
   | Identifier     | A900           | The C-FIND     |                |
   | does not match |                | query          |                |
   | SOP Class      |                | identifier     |                |
   |                |                | contains       |                |
   |                |                | invalid        |                |
   |                |                | Elements or    |                |
   |                |                | values, or is  |                |
   |                |                | missing        |                |
   |                |                | mandatory      |                |
   |                |                | Elements or    |                |
   |                |                | values for the |                |
   |                |                | specified SOP  |                |
   |                |                | Class.         |                |
   |                |                |                |                |
   |                |                | Error message  |                |
   |                |                | is output to   |                |
   |                |                | the Service    |                |
   |                |                | Audit Trail.   |                |
   +----------------+----------------+----------------+----------------+
   | Unable to      | C001           | The AE is      |                |
   | process        |                | unable to      |                |
   |                |                | establish a    |                |
   |                |                | session with   |                |
   |                |                | the Pharmacy   |                |
   |                |                | Information    |                |
   |                |                | System.        |                |
   |                |                |                |                |
   |                |                | Error message  |                |
   |                |                | is output to   |                |
   |                |                | the Service    |                |
   |                |                | Audit Trail.   |                |
   +----------------+----------------+----------------+----------------+
   | Unable to      | C002           | The AE is      |                |
   | process        |                | unable to      |                |
   |                |                | establish a    |                |
   |                |                | session with   |                |
   |                |                | the Patient    |                |
   |                |                | Registration   |                |
   |                |                | System.        |                |
   |                |                |                |                |
   |                |                | Error message  |                |
   |                |                | is output to   |                |
   |                |                | the Service    |                |
   |                |                | Audit Trail.   |                |
   +----------------+----------------+----------------+----------------+
   | Unable to      | C110           | The AE is      |                |
   | process        |                | unable to      |                |
   |                |                | identify the   |                |
   |                |                | Patient.       |                |
   |                |                |                |                |
   |                |                | Error message  |                |
   |                |                | is output to   |                |
   |                |                | the Service    |                |
   |                |                | Audit Trail.   |                |
   +----------------+----------------+----------------+----------------+
   | Unable to      | C120           | The AE is      |                |
   | process        |                | unable to      |                |
   |                |                | identify the   |                |
   |                |                | Product.       |                |
   |                |                |                |                |
   |                |                | Error message  |                |
   |                |                | is output to   |                |
   |                |                | the Service    |                |
   |                |                | Audit Trail.   |                |
   +----------------+----------------+----------------+----------------+
   | Cancel         | Matching       | FE00           | The C-FIND SCU |
   |                | terminated due |                | sent a Cancel  |
   |                | to Cancel      |                | Request. This  |
   |                | Request        |                | has been       |
   |                |                |                | acknowledged   |
   |                |                |                | and the search |
   |                |                |                | for matches    |
   |                |                |                | has been       |
   |                |                |                | halted.        |
   +----------------+----------------+----------------+----------------+
   | Pending        | Matches are    | FF00           | Indicates that |
   |                | continuing and |                | the successful |
   |                | current match  |                | match is       |
   |                | is supplied.   |                | returned and a |
   |                |                |                | further        |
   |                |                |                | response       |
   |                |                |                | (0000) is      |
   |                |                |                | forthcoming.   |
   |                |                |                | This status    |
   |                |                |                | code is        |
   |                |                |                | returned if    |
   |                |                |                | all Optional   |
   |                |                |                | keys in the    |
   |                |                |                | query          |
   |                |                |                | identifier are |
   |                |                |                | actually       |
   |                |                |                | supported.     |
   +----------------+----------------+----------------+----------------+
   | Matches are    | FF01           | Indicates that |                |
   | continuing but |                | the successful |                |
   | one or more    |                | match is       |                |
   | Optional Keys  |                | returned and a |                |
   | were not       |                | further        |                |
   | supported.     |                | response       |                |
   |                |                | (0000) is      |                |
   |                |                | forthcoming.   |                |
   |                |                | This status    |                |
   |                |                | code is        |                |
   |                |                | returned if    |                |
   |                |                | there are      |                |
   |                |                | Optional keys  |                |
   |                |                | in the query   |                |
   |                |                | identifier     |                |
   |                |                | that are not   |                |
   |                |                | supported.     |                |
   +----------------+----------------+----------------+----------------+

.. _sect_H.4.2.2:

MAR-SCP Application Entity Specification
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. _sect_H.4.2.2.1:

SOP Classes
'''''''''''

The MAR-SCP AE provides Standard Conformance to the following DICOM SOP
Classes:

.. table:: SOP Classes for MAR-SCP AE

   ================================ ================== === ===
   SOP Class Name                   SOP Class UID      SCU SCP
   ================================ ================== === ===
   Verification                     1.2.840.10008.1.1  No  Yes
   Substance Administration Logging 1.2.840.10008.1.42 No  Yes
   ================================ ================== === ===

.. _sect_H.4.2.2.2:

Association Policies
''''''''''''''''''''

.. _sect_H.4.2.2.2.1:

General
       

The MAR-SCP AE will never initiate Associations; it only accepts
Association Requests from external DICOM AEs. The MAR-SCP AE will accept
Associations for Verification (C-ECHO) and Substance Administration
Logging (N-ACTION) requests.

The DICOM standard Application Context Name for DICOM is always accepted
and proposed:

.. table:: DICOM Application Context for MAR-SCP AE

   ======================== =====================
   Application Context Name 1.2.840.10008.3.1.1.1
   ======================== =====================

.. _sect_H.4.2.2.2.2:

Number of Associations
                      

The MAR-SCP AE can support multiple simultaneous Associations. Each time
the MAR-SCP AE receives an Association, a child process will be spawned
to process the Verification or Substance Administration Logging request.
The maximum number of child processes, and thus the maximum number of
simultaneous Associations that can be processed, is set by
configuration. The default maximum number is 10 in total.

.. table:: Number of Simultaneous Associations as an SCP for MAR-SCP AE

   +-------------------------------------------------+-------------------+
   | Maximum number of simultaneous Associations     | 10 (Configurable) |
   | requested by peer AEs                           |                   |
   +-------------------------------------------------+-------------------+

.. _sect_H.4.2.2.2.3:

Asynchronous Nature
                   

The MAR-SCP AE does not support asynchronous communication (multiple
outstanding transactions over a single Association). All Association
requests must be completed and acknowledged before a new operation can
be initiated.

.. table:: Asynchronous Nature as a SCP for MAR-SCP AE

   +----------------------------------------------+----------------------+
   | Maximum number of outstanding asynchronous   | 1 (Not Configurable) |
   | transactions                                 |                      |
   +----------------------------------------------+----------------------+

.. _sect_H.4.2.2.2.4:

Implementation Identifying Information
                                      

The implementation information for this Application Entity is:

.. table:: DICOM Implementation Class and Version for MAR-SCP AE

   =========================== ======================
   Implementation Class UID    1.840.xxxxxxx.yyy.etc…
   Implementation Version Name EX_VERS_01
   =========================== ======================

Note that all EXAMPLE-MEDICATION-SYSTEM-GATEWAY AEs use the same
Implementation Class UID and Implementation Version Name. This Version
Name is updated with each new release of the product software, as the
different AE versions are never released independently.

.. _sect_H.4.2.2.3:

Association Initiation Policy
'''''''''''''''''''''''''''''

The MAR-SCP AE does not initiate Associations.

.. _sect_H.4.2.2.4:

Association Acceptance Policy
'''''''''''''''''''''''''''''

.. _sect_H.4.2.2.4.1:

Activity - Handling Substance Administration Logging Requests
                                                             

.. _sect_H.4.2.2.4.1.1:

Description and Sequencing of Activity
                                      

The MAR-SCP AE accepts Associations only if they have valid Presentation
Contexts. If none of the requested Presentation Contexts are accepted
then the Association Request itself is rejected. It can be configured to
only accept Associations with certain hosts (using TCP/IP address)
and/or Application Entity Titles.

The following sequencing applies to the MAR-SCP AE for handling
Substance Administration Logging Requests (N-ACTION) :

1. Peer AE opens an Association with the MAR-SCP AE.

2. Peer AE sends N-ACTION-RQ to request logging of a substance
   administration event.

3. If the request does not include the Patient ID, MAR-SCP AE requests
   the Patient ID corresponding to the Admission ID from the Patient
   Registration System

4. MAR-SCP AE translates the logging request into a database operation
   on the Medication Administration Record System database.

5. MAR-SCP AE responds with N-ACTION-RSP to indicate that it received
   and processed the request.

6. Peer AE closes the Association. Note that the peer AE does not have
   to close the Association immediately. Further N-ACTION Requests can
   be sent over the Association before it is closed.

The MAR-SCP AE may reject Association attempts as shown in the Table
below. The Result, Source and Reason/Diag columns represent the values
returned in the corresponding fields of an ASSOCIATE-RJ PDU (see ). The
following abbreviations are used in the Source column:

a. 1 - DICOM UL service-user

b. 2 - DICOM UL service-provider (ASCE related function)

c. 3 - DICOM UL service-provider (Presentation related function)

.. table:: Association Rejection Reasons

   +------------------+--------+------------------+------------------+
   | Result           | Source | Reason/Diag      | Explanation      |
   +==================+========+==================+==================+
   | 2 -              | c      | 2 -              | The              |
   | re               |        | loca             | (configurable)   |
   | jected-transient |        | l-limit-exceeded | maximum number   |
   |                  |        |                  | of simultaneous  |
   |                  |        |                  | Associations has |
   |                  |        |                  | been reached. An |
   |                  |        |                  | Association      |
   |                  |        |                  | request with the |
   |                  |        |                  | same parameters  |
   |                  |        |                  | may succeed at a |
   |                  |        |                  | later time.      |
   +------------------+--------+------------------+------------------+
   | 2 -              | c      | 1 -              | No Associations  |
   | re               |        | temp             | can be accepted  |
   | jected-transient |        | orary-congestion | at this time due |
   |                  |        |                  | to the real-time |
   |                  |        |                  | requirements of  |
   |                  |        |                  | higher priority  |
   |                  |        |                  | activities       |
   |                  |        |                  | (e.g., during    |
   |                  |        |                  | image            |
   |                  |        |                  | acquisition no   |
   |                  |        |                  | Associations     |
   |                  |        |                  | will be          |
   |                  |        |                  | accepted) or     |
   |                  |        |                  | because          |
   |                  |        |                  | insufficient     |
   |                  |        |                  | resources are    |
   |                  |        |                  | available (e.g., |
   |                  |        |                  | memory,          |
   |                  |        |                  | processes,       |
   |                  |        |                  | threads). An     |
   |                  |        |                  | Association      |
   |                  |        |                  | request with the |
   |                  |        |                  | same parameters  |
   |                  |        |                  | may succeed at a |
   |                  |        |                  | later time.      |
   +------------------+--------+------------------+------------------+
   | 1 -              | a      | 2 -              | The Association  |
   | re               |        | applic           | request          |
   | jected-permanent |        | ation-context-na | contained an     |
   |                  |        | me-not-supported | unsupported      |
   |                  |        |                  | Application      |
   |                  |        |                  | Context Name. An |
   |                  |        |                  | association      |
   |                  |        |                  | request with the |
   |                  |        |                  | same parameters  |
   |                  |        |                  | will not succeed |
   |                  |        |                  | at a later time. |
   +------------------+--------+------------------+------------------+
   | 1 -              | a      | 7 -              | The Association  |
   | re               |        | called-AE-titl   | request          |
   | jected-permanent |        | e-not-recognized | contained an     |
   |                  |        |                  | unrecognized     |
   |                  |        |                  | Called AE Title. |
   |                  |        |                  | An Association   |
   |                  |        |                  | request with the |
   |                  |        |                  | same parameters  |
   |                  |        |                  | will not succeed |
   |                  |        |                  | at a later time  |
   |                  |        |                  | unless           |
   |                  |        |                  | configuration    |
   |                  |        |                  | changes are      |
   |                  |        |                  | made. This       |
   |                  |        |                  | rejection reason |
   |                  |        |                  | normally occurs  |
   |                  |        |                  | when the         |
   |                  |        |                  | Association      |
   |                  |        |                  | initiator is     |
   |                  |        |                  | incorrectly      |
   |                  |        |                  | configured and   |
   |                  |        |                  | attempts to      |
   |                  |        |                  | address the      |
   |                  |        |                  | Association      |
   |                  |        |                  | acceptor using   |
   |                  |        |                  | the wrong AE     |
   |                  |        |                  | Title.           |
   +------------------+--------+------------------+------------------+
   | 1 -              | a      | 3 -              | The Association  |
   | re               |        | calling-AE-titl  | request          |
   | jected-permanent |        | e-not-recognized | contained an     |
   |                  |        |                  | unrecognized     |
   |                  |        |                  | Calling AE       |
   |                  |        |                  | Title. An        |
   |                  |        |                  | Association      |
   |                  |        |                  | request with the |
   |                  |        |                  | same parameters  |
   |                  |        |                  | will not succeed |
   |                  |        |                  | at a later time  |
   |                  |        |                  | unless           |
   |                  |        |                  | configuration    |
   |                  |        |                  | changes are      |
   |                  |        |                  | made. This       |
   |                  |        |                  | rejection reason |
   |                  |        |                  | normally occurs  |
   |                  |        |                  | when the         |
   |                  |        |                  | Association      |
   |                  |        |                  | acceptor has not |
   |                  |        |                  | been configured  |
   |                  |        |                  | to recognize the |
   |                  |        |                  | AE Title of the  |
   |                  |        |                  | Association      |
   |                  |        |                  | initiator.       |
   +------------------+--------+------------------+------------------+
   | 1 -              | b      | 1 -              | The Association  |
   | re               |        | no-reason-given  | request could    |
   | jected-permanent |        |                  | not be parsed.   |
   |                  |        |                  | An Association   |
   |                  |        |                  | request with the |
   |                  |        |                  | same format will |
   |                  |        |                  | not succeed at a |
   |                  |        |                  | later time.      |
   +------------------+--------+------------------+------------------+

The MAR-SCP AE will close the Association under the exceptional
circumstances listed in `table_title <#table_H.4.2-20>`__.

.. table:: PHARMACY-SCP AE Communication Failure Behavior

   +----------------------------------+----------------------------------+
   | Exception                        | Behavior                         |
   +==================================+==================================+
   | Timeout expiry for an expected   | The Association is aborted by    |
   | DICOM Message Request (DIMSE     | issuing a DICOM A-ABORT.         |
   | level timeout). I.e. The MAR-SCP |                                  |
   | AE is waiting for the next       | Error message is output to the   |
   | N-ACTION Request on an open      | Service Audit Trail.             |
   | Association but the timer        |                                  |
   | expires.                         |                                  |
   +----------------------------------+----------------------------------+
   | Timeout expiry for an expected   | The Association is aborted by    |
   | DICOM PDU or TCP/IP packet       | issuing a DICOM A-ABORT.         |
   | (Low-level timeout). I.e. The    |                                  |
   | MAR-SCP AE is waiting for the    | Error message is output to the   |
   | next message PDU but the timer   | Service Audit Trail.             |
   | expires.                         |                                  |
   +----------------------------------+----------------------------------+
   | Association aborted by the SCU   | Error message is output to the   |
   | or the network layers indicate   | Service Audit Trail.             |
   | communication loss (i.e.,        |                                  |
   | low-level TCP/IP socket closure) |                                  |
   +----------------------------------+----------------------------------+

.. _sect_H.4.2.2.4.1.2:

Accepted Presentation Contexts
                              

The MAR-SCP AE will accept Presentation Contexts as shown in
`table_title <#table_H.4.2-21>`__.

.. table:: Accepted Presentation Contexts By MAR-SCP AE

   +------------+------------+------------+------------+-----+------+
   | Pr         |            |            |            |     |      |
   | esentation |            |            |            |     |      |
   | Context    |            |            |            |     |      |
   | Table      |            |            |            |     |      |
   +============+============+============+============+=====+======+
   | Ve         | 1.2.840    | DICOM      | 1.2.840    | SCP | None |
   | rification | .10008.1.1 | Implicit   | .10008.1.2 |     |      |
   |            |            | VR Little  |            |     |      |
   |            |            | Endian     |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | Substance  | 1.2.840.   | DICOM      | 1.2.840    | SCP | None |
   | Admi       | 10008.1.42 | Implicit   | .10008.1.2 |     |      |
   | nistration |            | VR Little  |            |     |      |
   | Logging    |            | Endian     |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | DICOM      | 1.2.840.1  |            |            |     |      |
   | Explicit   | 0008.1.2.1 |            |            |     |      |
   | VR Little  |            |            |            |     |      |
   | Endian     |            |            |            |     |      |
   +------------+------------+------------+------------+-----+------+

.. _sect_H.4.2.2.4.1.3:

SOP Specific Conformance for Verification SOP Class
                                                   

The MAR-SCP AE provides standard conformance to the Verification SOP
Class as an SCP.

.. _sect_H.4.2.2.4.1.4:

SOP Specific Conformance for Substance Administration Logging SOP Classes
                                                                         

As required by the SOP Class, one of Patient ID or Admission ID must be
present in the Substance Administration Logging request. If the request
does not include the Patient ID, the MAR-SCP AE requests the Patient ID
corresponding to the Admission ID from the Patient Registration System.

The MAR-SCP AE SCP translates the attributes shown in
`table_title <#table_H.4.2-22>`__ into database fields of the Medication
Administration Record System. All other provided attributes are
converted to text strings and placed in the ClinicalNotes field of the
database.

.. table:: Attributes of Logging Request Imported to Mar Database

   ================================== ===========
   Patient ID                         (0010,0020)
   Product Package Identifier         (0044,0001)
   Product Name                       (0044,0008)
   Substance Administration DateTime  (0044,0010)
   Administration Route Code Sequence (0054,0302)
   Operator Identification Sequence   (0008,1072)
   ================================== ===========

The MAR-SCP AE supports the N-ACTION Response Status return values and
behavior shown in `table_title <#table_H.4.2-23>`__.

.. table:: MAR-SCP AE N-ACTION Response Status Return Reasons

   +----------------+----------------+----------------+----------------+
   | Service Status | Further        | Status Code    | Reason         |
   |                | Meaning        |                |                |
   +================+================+================+================+
   | Success        | Success        | 0000           | The log entry  |
   |                |                |                | was            |
   |                |                |                | successfully   |
   |                |                |                | received and   |
   |                |                |                | stored in the  |
   |                |                |                | Medication     |
   |                |                |                | Administration |
   |                |                |                | Record System  |
   |                |                |                | database.      |
   +----------------+----------------+----------------+----------------+
   | Failure        | Processing     | 0110           | The AE is      |
   |                | failure        |                | unable to      |
   |                |                |                | establish a    |
   |                |                |                | session with   |
   |                |                |                | the Medication |
   |                |                |                | Administration |
   |                |                |                | Record System  |
   |                |                |                | (Error         |
   |                |                |                | ID=C003), or   |
   |                |                |                | with the       |
   |                |                |                | Patient        |
   |                |                |                | Registration   |
   |                |                |                | System (Error  |
   |                |                |                | ID=C002).      |
   |                |                |                |                |
   |                |                |                | Error message  |
   |                |                |                | is output to   |
   |                |                |                | the Service    |
   |                |                |                | Audit Trail.   |
   +----------------+----------------+----------------+----------------+
   | Operator not   | C10E           | The AE         |                |
   | authorized to  |                | received a     |                |
   | add entry to   |                | user           |                |
   | Medication     |                | authorization  |                |
   | Administration |                | rejection from |                |
   | Record         |                | the Medication |                |
   |                |                | Administration |                |
   |                |                | Record System. |                |
   |                |                |                |                |
   |                |                | Error message  |                |
   |                |                | is output to   |                |
   |                |                | the Service    |                |
   |                |                | Audit Trail.   |                |
   +----------------+----------------+----------------+----------------+
   | Patient cannot | C110           | The AE is      |                |
   | be identified  |                | unable to      |                |
   | from Patient   |                | identify the   |                |
   | ID or          |                | Patient.       |                |
   | Admission ID   |                |                |                |
   |                |                | Error message  |                |
   |                |                | is output to   |                |
   |                |                | the Service    |                |
   |                |                | Audit Trail.   |                |
   +----------------+----------------+----------------+----------------+
   | Update of      | C111           | The Medication |                |
   | Medication     |                | Administration |                |
   | Administration |                | Record System  |                |
   | Record failed  |                | reported a     |                |
   |                |                | database       |                |
   |                |                | error.         |                |
   |                |                |                |                |
   |                |                | Error message  |                |
   |                |                | is output to   |                |
   |                |                | the Service    |                |
   |                |                | Audit Trail.   |                |
   +----------------+----------------+----------------+----------------+

.. _sect_H.4.3:

Network Interfaces
~~~~~~~~~~~~~~~~~~

.. _sect_H.4.3.1:

Physical Network Interface
^^^^^^^^^^^^^^^^^^^^^^^^^^

The EXAMPLE-MEDICATION-SYSTEM-GATEWAY supports a single network
interface. One of the following physical network interfaces will be
available depending on installed hardware options:

.. table:: Supported Physical Network Interfaces

   +-------------------+
   | Ethernet 100baseT |
   +===================+
   | Gigabit Ethernet  |
   +-------------------+

.. _sect_H.4.3.2:

Additional Protocols
^^^^^^^^^^^^^^^^^^^^

EXAMPLE-MEDICATION-SYSTEM-GATEWAY conforms to the System Management
Profiles listed in `table_title <#table_F.4.3-2>`__. All requested
transactions for the listed profiles and actors are supported. It does
not support any optional transactions.

.. table:: Supported System Management Profiles

   +-------------+-------------+-------------+-------------+-------------+
   | Profile     | Actor       | Protocols   | Optional    | Security    |
   | Name        |             | Used        | T           | Support     |
   |             |             |             | ransactions |             |
   +=============+=============+=============+=============+=============+
   | Network     | DHCP Client | DHCP        | N/A         |             |
   | Address     |             |             |             |             |
   | Management  |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | DNS Client  | DNS         | N/A         |             |             |
   +-------------+-------------+-------------+-------------+-------------+

.. _sect_H.4.3.2.1:

DHCP
''''

DHCP can be used to obtain TCP/IP network configuration information. The
network parameters obtainable via DHCP are shown in
`table_title <#table_F.4.3-3>`__. The Default Value column of the table
shows the default used if the DHCP server does not provide a value.
Values for network parameters set in the Service/Installation tool take
precedence over values obtained from the DHCP server. Support for DHCP
can be configured via the Service/Installation Tool. The
Service/Installation tool can be used to configure the machine name. If
DHCP is not in use, TCP/IP network configuration information can be
manually configured via the Service/Installation Tool.

.. table:: Supported DHCP Parameters

   =================== ============================================
   DHCP Parameter      Default Value
   =================== ============================================
   IP Address          None
   Hostname            Requested machine name
   List of NTP servers Empty list
   List of DNS servers Empty list
   Routers             Empty list
   Static routes       None
   Domain name         None
   Subnet mask         Derived from IP Address (see service manual)
   Broadcast address   Derived from IP Address (see service manual)
   Default router      None
   Time offset         Site configurable (from Time zone)
   MTU                 Network Hardware Dependent
   Auto-IP permission  No permission
   =================== ============================================

If the DHCP server refuses to renew a lease on the assigned IP address
all active DICOM Associations will be aborted.

.. _sect_H.4.3.2.2:

DNS
'''

DNS can be used for address resolution. If DHCP is not in use or the
DHCP server does not return any DNS server addresses, the identity of a
DNS server can be configured via the Service/Installation Tool. If a DNS
server is not in use, local mapping between hostname and IP address can
be manually configured via the Service/Installation Tool.

.. _sect_H.4.4:

Configuration
~~~~~~~~~~~~~

.. _sect_H.4.4.1:

AE Title/Presentation Address Mapping
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. _sect_H.4.4.1.1:

Local AE Titles
'''''''''''''''

The mapping from AE Title to TCP/IP addresses and ports is configurable
and set at the time of installation by Installation Personnel.

.. table:: Default Application Entity Characteristics

   ================== ==== ================ ===================
   Application Entity Role Default AE Title Default TCP/IP Port
   ================== ==== ================ ===================
   PHARMACY-SCP       SCP  EX_PHAR_SCP      5000
   MAR-SCP            SCP  EX_MAR_SCP       4000
   ================== ==== ================ ===================

The PHARMACY-SCP and MAR-SCP Application Entities can be configured to
have the same AE Title.

.. _sect_H.4.4.1.2:

Remote AE Title/Presentation Address Mapping
''''''''''''''''''''''''''''''''''''''''''''

The mapping of external AE Titles to TCP/IP addresses and ports is
configurable and set at the time of installation by Installation
Personnel. This mapping is necessary for resolving the IP address and
port of C-MOVE Destination Application Entities and must be correctly
configured for the PHARMACY-SCP AE to correctly function as a C-MOVE
SCP.

.. _sect_H.4.4.2:

Parameters
^^^^^^^^^^

.. table:: Configuration Parameters

   +-------------------------------------+--------------+---------------+
   | Parameter                           | Configurable | Default Value |
   +=====================================+==============+===============+
   | **General Parameters**              |              |               |
   +-------------------------------------+--------------+---------------+
   | Maximum PDU size I can receive      | Yes          | 128kbytes     |
   +-------------------------------------+--------------+---------------+
   | Maximum PDU size I can send         | Yes          | 128kbytes     |
   +-------------------------------------+--------------+---------------+
   | Time-out waiting for response to    | Yes          | 10 s          |
   | TCP/IP connect() request.           |              |               |
   | (Low-level timeout)                 |              |               |
   +-------------------------------------+--------------+---------------+
   | Time-out waiting for A-ASSOCIATE RQ | Yes          | 30 s          |
   | PDU on open TCP/IP connection.      |              |               |
   | (ARTIM timeout)                     |              |               |
   +-------------------------------------+--------------+---------------+
   | Time-out waiting for acceptance or  | Yes          | 30s           |
   | rejection response to an            |              |               |
   | Association Open Request.           |              |               |
   | (Application Level timeout)         |              |               |
   +-------------------------------------+--------------+---------------+
   | Time-out waiting for acceptance of  | Yes          | 30 s          |
   | a TCP/IP message over the network.  |              |               |
   | (Low-level timeout)                 |              |               |
   +-------------------------------------+--------------+---------------+
   | Time-out for waiting for data       | Yes          | 30 s          |
   | between TCP/IP packets. (Low-level  |              |               |
   | timeout)                            |              |               |
   +-------------------------------------+--------------+---------------+
   | **PHARMACY-SCP AE Parameters**      |              |               |
   +-------------------------------------+--------------+---------------+
   | Maximum number of simultaneous      | Yes          | 10            |
   | Associations                        |              |               |
   +-------------------------------------+--------------+---------------+
   | AE time-out waiting on an open      | Yes          | 1 minute      |
   | Association for the next message    |              |               |
   | (C-FIND-RQ, Association Close       |              |               |
   | Request. etc.) (DIMSE timeout)      |              |               |
   +-------------------------------------+--------------+---------------+
   | **MAR-SCP AE Parameters**           |              |               |
   +-------------------------------------+--------------+---------------+
   | Maximum number of simultaneous      | Yes          | 10            |
   | Associations                        |              |               |
   +-------------------------------------+--------------+---------------+
   | AE time-out waiting on an open      | Yes          | 1 minute      |
   | Association for the next Request    |              |               |
   | message (N-ACTION-RQ, Association   |              |               |
   | Close Request. etc.) (DIMSE         |              |               |
   | timeout)                            |              |               |
   +-------------------------------------+--------------+---------------+

.. _sect_H.5:

Media Interchange
-----------------

EXAMPLE-MEDICATION-SYSTEM-GATEWAY does not support Media Storage.

.. _sect_H.6:

Support of Extended Character Sets
----------------------------------

All EXAMPLE-MEDICATION-SYSTEM-GATEWAY DICOM applications support the
following:

ISO_IR 192 (Unicode)

.. _sect_H.7:

Security
--------

.. _sect_H.7.1:

Security Profiles
~~~~~~~~~~~~~~~~~

The EXAMPLE-MEDICATION-SYSTEM-GATEWAY is configurable to support the
Kerberos Identity Negotiation Association Profile.

.. _sect_H.7.2:

Association Level Security
~~~~~~~~~~~~~~~~~~~~~~~~~~

The PHARMACY-SCP AE and the MAR-SCP AE can both be configured to accept
Association Requests from only a limited list of Calling AE Titles. The
SCP AEs can have different lists. Each SCP AE can be configured to check
that the Association requestor specifies the correct Called AE Title for
the SCP.

In addition the IP address of the requestor can be checked. The SCP AEs
can be constrained to only accept Association Requests from a configured
list of IP addresses. The SCP AEs can have different lists.

