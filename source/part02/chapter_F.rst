.. _chapter_F:

DICOM Conformance Statement Query-Retrieve-Server (Informative)
===============================================================

Disclaimer:

This document is an example DICOM Conformance Statement for a fictional
device called EXAMPLE-QUERY-RETRIEVE-SERVER, which is a self-contained
networked computer system used for archiving diagnostic medical images.

As stated in the annex title, this document is truly informative, and
not normative. A conformance statement of an actual product might
implement additional services and options as appropriate for its
specific purpose. In addition, an actual product might implement the
services described in a different manner and, for example, with
different characteristics and/or sequencing of activities. In other
words, this conformance statement example does not intend to standardize
a particular manner that a product might implement DICOM functionality.

.. _sect_F.0:

Cover Page
----------

Company Name: EXAMPLE-ARCHIVING-PRODUCTS.

Product Name: SAMPLE QUERY-RETRIEVE-SERVER

Version: 1.0-rev. A.1

Internal document number: 4226-xxx-yyy-zzz rev 1

Date: YYYYMMDD

.. _sect_F.1:

Conformance Statement Overview
------------------------------

The EXAMPLE-QUERY-RETRIEVE-SERVER is a self-contained networked computer
system used for archiving diagnostic medical images. It allows external
systems to send images to it for permanent storage, retrieve information
about such images, and retrieve the images themselves. The system
conforms to the DICOM standard to allow the sharing of medical
information with other digital imaging systems.

.. table:: Network Services

   +----------------------+----------------------+----------------------+
   | SOP Classes          | User of Service      | Provider of Service  |
   |                      | (SCU)                | (SCP)                |
   +======================+======================+======================+
   | Transfer             |                      |                      |
   +----------------------+----------------------+----------------------+
   | US Image Storage     | Yes                  | Yes                  |
   | (Retired)            |                      |                      |
   +----------------------+----------------------+----------------------+
   | US Image Storage     | Yes                  | Yes                  |
   +----------------------+----------------------+----------------------+
   | US Multi-frame       | Yes                  | Yes                  |
   | Storage (Retired)    |                      |                      |
   +----------------------+----------------------+----------------------+
   | US Multi-frame       | Yes                  | Yes                  |
   | Storage              |                      |                      |
   +----------------------+----------------------+----------------------+
   | Computed Radiography | Yes                  | Yes                  |
   | Image Storage        |                      |                      |
   +----------------------+----------------------+----------------------+
   | CT Image Storage     | Yes                  | Yes                  |
   +----------------------+----------------------+----------------------+
   | MR Image Storage     | Yes                  | Yes                  |
   +----------------------+----------------------+----------------------+
   | Secondary Capture    | Yes                  | Yes                  |
   | Image Storage        |                      |                      |
   +----------------------+----------------------+----------------------+
   | Storage Commitment   |                      |                      |
   +----------------------+----------------------+----------------------+
   | Storage Commitment   | No                   | Yes                  |
   | Push Model           |                      |                      |
   +----------------------+----------------------+----------------------+
   | Query/Retrieve       |                      |                      |
   +----------------------+----------------------+----------------------+
   | Patient Root Q/R -   | No                   | Yes                  |
   | FIND                 |                      |                      |
   +----------------------+----------------------+----------------------+
   | Patient Root Q/R -   | No                   | Yes                  |
   | MOVE                 |                      |                      |
   +----------------------+----------------------+----------------------+
   | Study Root Q/R -     | No                   | Yes                  |
   | FIND                 |                      |                      |
   +----------------------+----------------------+----------------------+
   | Study Root Q/R -     | No                   | Yes                  |
   | MOVE                 |                      |                      |
   +----------------------+----------------------+----------------------+

.. note::

   Relational Queries are not supported either as an SCU or SCP.

.. _sect_F.2:

Table of Contents
-----------------

A table of contents shall be provided to assist readers in easily
finding the needed information.

.. _sect_F.3:

Introduction
------------

.. _sect_F.3.1:

Revision History
~~~~~~~~~~~~~~~~

.. table:: Revision History

   ================ ================ ========= ======================
   Document Version Date             Author    Description
   ================ ================ ========= ======================
   1.1              October 30, 2003 DICOM WG6 Version for Final Text
   1.2              August 30, 2007  WG 6      Revised Introduction
   ================ ================ ========= ======================

.. _sect_F.3.2:

Audience, Remarks, Terms and Definitions, Basics of DICOM Communication, Abbreviations, References
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

*See example text in*\ `Introduction <#sect_A.3>`__\ *.*

.. _sect_F.3.3:

Additional Remarks for This Example
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This document is a sample DICOM Conformance Statement created for DICOM
. It is to be used solely as an example to illustrate how to create a
DICOM Conformance Statement for an image storage system supporting DICOM
images. The subject of the document, EXAMPLE-QUERY-RETRIEVE-SERVER, is a
fictional product.

.. _sect_F.4:

Networking
----------

.. _sect_F.4.1:

Implementation Model
~~~~~~~~~~~~~~~~~~~~

.. _sect_F.4.1.1:

Application Data Flow
^^^^^^^^^^^^^^^^^^^^^

The division of EXAMPLE-QUERY-RETRIEVE-SERVER into the separate DICOM
Application Entities represents a somewhat arbitrary partitioning of
functionality. For the purpose of this document they are organized in
this manner so as to detail their independent logical functionality.

By default all of the defined Application Entities have different AE
Titles. However, EXAMPLE-QUERY-RETRIEVE-SERVER can be configured so that
the QUERY-RETRIEVE-SCP AE and STORAGE-SCU AE share the same Application
Entity Title. However, the QUERY-RETRIEVE-SCP AE and STORAGE-SCP AE must
have separate Application Entity Titles.

The Application Entities detailed in the Application Data Flow Diagram
are all Windows NT applications.

-  The STORAGE-SCU AE can send Composite SOP Instances. It handles
   requests from the QUERY-RETRIEVE-SCP AE to transmit Images to a
   specific DICOM destination. The STORAGE-SCU AE functions as a C-STORE
   SCU. (Note that in this example Conformance Statement this
   STORAGE-SCU AE does not allow a Local User to request that images be
   sent to a Remote AE. If a 'real' AE does allow this then this should
   be mentioned here and in the other appropriate areas of the
   Conformance Statement).

-  The QUERY-RETRIEVE-SCP AE can handle incoming query and retrieve
   requests. It can handle external queries for Patient, Study, Series,
   and Image data, and also handle Image retrieval requests. The
   QUERY-RETRIEVE-SCP AE handles retrieval requests by issuing a command
   to the STORAGE-SCU AE to send the requested Images to the destination
   specified by the Remote AE. The QUERY-RETRIEVE-SCP AE functions as an
   SCP for C-FIND and C-MOVE requests.

-  The STORAGE-SCP AE can receive incoming DICOM images and add them to
   the EXAMPLE-QUERY-RETRIEVE-SERVER database. It can respond to
   external Storage and Verification Requests as a Service Class
   Provider (SCP) for C-STORE and C-ECHO requests. The STORAGE-SCP AE
   can also handle Storage Commitment Push Model Requests. It can thus
   be used to query whether the EXAMPLE-QUERY-RETRIEVE-SERVER will
   confirm ownership and responsibility for specific Composite SOP
   Instances. The STORAGE-SCP AE currently only supports image type
   Composite SOP Instances.

.. _sect_F.4.1.2:

Functional Definition of AEs
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. _sect_F.4.1.2.1:

Functional Definition of STORAGE-SCU Application Entity
'''''''''''''''''''''''''''''''''''''''''''''''''''''''

The STORAGE-SCU AE can be invoked by the QUERY-RETRIEVE-SCP AE to
trigger the transfer of specific images to a remote destination AE. The
STORAGE-SCU AE must be correctly configured with the host and port
number of any external DICOM AEs that are to be C-MOVE retrieval
destinations. The Presentation Contexts to use are determined from the
headers of the DICOM files to be transferred. Some conversion of the
DICOM image objects is possible if the original Presentation Context is
not supported by the remote destination AE or if compression is
preferred.

.. _sect_F.4.1.2.2:

Functional Definition of QUERY-RETRIEVE-SCP Application Entity
''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''

The QUERY-RETRIEVE-SCP AE waits for another application to connect at
the presentation address configured for its Application Entity Title.
When another application connects, QUERY-RETRIEVE-SCP AE expects it to
be a DICOM application. QUERY-RETRIEVE-SCP AE will accept Associations
with Presentation Contexts for SOP Classes of the DICOM Query-Retrieve
Service Class, and Verification Service Class. It will handle query and
retrieve requests on these Presentation Contexts and respond with data
objects with values corresponding to the contents of the
EXAMPLE-QUERY-RETRIEVE-SERVER database. For C-MOVE requests the
destination for the image objects is determined from the Destination AE
Title contained in the C-MOVE request. When a retrieval request is
received, the QUERY-RETRIEVE-SCP AE issues a command to the STORAGE-SCU
AE to send the specified images to the C-MOVE Destination AE.

.. _sect_F.4.1.2.3:

Functional Definition of STORAGE-SCP Application Entity
'''''''''''''''''''''''''''''''''''''''''''''''''''''''

The STORAGE-SCP AE waits for another application to connect at the
presentation address configured for its Application Entity Title. When
another application connects, the STORAGE-SCP AE expects it to be a
DICOM application. The STORAGE-SCP AE will accept Associations with
Presentation Contexts for SOP Classes of the Verification, Storage, and
Storage Commitment Service Classes. Any images received on such
Presentation Contexts will be added to the EXAMPLE-QUERY-RETRIEVE-SERVER
database. If a Storage Commitment Push Model N-ACTION Request is
received then the STORAGE-COMMITMENT-SCP AE will immediately check if
the referenced Composite SOP Instances are in the
EXAMPLE-QUERY-RETRIEVE-SERVER database and return an N-EVENT-REPORT
Notification. It will never 'cache' Storage Commitment Push Model
Requests and wait for Composite SOP Instances to be received at a later
time.

.. _sect_F.4.1.3:

Sequencing of Real-World Activities
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The only sequencing constraint that exists across all the
EXAMPLE-QUERY-RETRIEVE-SERVER Application Entities is the fact that a
Composite SOP Instance must be received by the STORAGE-SCP AE before
Storage Commitment Push Model or Query-Retrieve Requests related to this
SOP Instance can be successfully handled:

Note that the only constraint is for the Composite SOP Instance to be
received prior to the other events. For example, it is not necessary for
the Storage Commitment Push Model Request to be received prior to
receiving Query or Retrieval Requests related to the SOP Instance.

.. _sect_F.4.2:

AE Specifications
~~~~~~~~~~~~~~~~~

.. _sect_F.4.2.1:

STORAGE-SCU Application Entity Specification
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. _sect_F.4.2.1.1:

SOP Classes
'''''''''''

The STORAGE-SCU AE provides Standard Conformance to the following DICOM
SOP Classes:

.. table:: SOP Classes for STORAGE-SCU AE

   ================================== =========================== === ===
   SOP Class Name                     SOP Class UID               SCU SCP
   ================================== =========================== === ===
   Verification                       1.2.840.10008.1.1           Yes No
   US Image Storage (Retired)         1.2.840.10008.5.1.4.1.1.6   Yes No
   US Image Storage                   1.2.840.10008.5.1.4.1.1.6.1 Yes No
   US Multi-frame Storage (Retired)   1.2.840.10008.5.1.4.1.1.3   Yes No
   US Multi-frame Storage             1.2.840.10008.5.1.4.1.1.3.1 Yes No
   Computed Radiography Image Storage 1.2.840.10008.5.1.4.1.1.1   Yes No
   CT Image Storage                   1.2.840.10008.5.1.4.1.1.2   Yes No
   MR Image Storage                   1.2.840.10008.5.1.4.1.1.4   Yes No
   Secondary Capture Image Storage    1.2.840.10008.5.1.4.1.1.7   Yes No
   ================================== =========================== === ===

STORAGE-SCU AE can be configured to use the retired US Image objects (US
Image Storage, 1.2.840.10008.5.1.4.1.1.6, and US Multi-frame Storage,
1.2.840.10008.5.1.4.1.1.3) rather than the current US SOP Classes for
ultrasound images or vice-versa, making any necessary changes to make
the transformed image objects conformant to the corresponding SOP Class.
This is only done if the external Storage SCP AE does not support the
SOP Instance's original SOP Class.

By altering the configuration it is possible to support additional or
fewer SOP Classes.

.. _sect_F.4.2.1.2:

Association Establishment Policies
''''''''''''''''''''''''''''''''''

.. _sect_F.4.2.1.2.1:

General
       

The STORAGE-SCU AE can only form Associations when requested to do so by
the QUERY-RETRIEVE-SCP AE. The STORAGE-SCU AE can only request the
opening of an Association. It cannot accept requests to open
Associations from external Application Entities.

The DICOM standard Application Context Name for DICOM is always
proposed:

.. table:: DICOM Application Context for STORAGE-SCU AE

   ======================== =====================
   Application Context Name 1.2.840.10008.3.1.1.1
   ======================== =====================

.. _sect_F.4.2.1.2.2:

Number of Associations
                      

The maximum number of simultaneous Associations is configurable, but is
usually limited to a maximum of 10. This configuration largely depends
on whether relatively quick response to multiple simultaneous C-MOVE
Destination AEs is required or maximum throughput performance is
required. If the latter is the case, then no simultaneous Associations
are permitted, in order to reduce disk thrashing and thus maximize
throughput. The STORAGE-SCU AE can initiate simultaneous Associations to
a given external C-MOVE Destination AE up to the maximum number
configured. There is no separate limit on the maximum number permitted
to the same C-MOVE Destination AE.

If the first attempt to open an Association fails then the STORAGE-SCU
AE will reschedule the task to attempt it again after a configurable
time delay. The number of times to reattempt Association establishment
is configurable, with the default being zero.

.. table:: Number of Associations as a SCU for STORAGE-SCU AE

   =========================================== =================
   Maximum number of simultaneous Associations 10 (Configurable)
   =========================================== =================

.. _sect_F.4.2.1.2.3:

Asynchronous Nature
                   

The STORAGE-SCU AE does not support asynchronous communication (multiple
outstanding transactions over a single Association). All Association
requests must be completed and acknowledged before a new operation can
be initiated.

.. table:: Asynchronous Nature as a SCU for STORAGE-SCU AE

   +----------------------------------------------+----------------------+
   | Maximum number of outstanding asynchronous   | 1 (Not Configurable) |
   | transactions                                 |                      |
   +----------------------------------------------+----------------------+

.. _sect_F.4.2.1.2.4:

Implementation Identifying Information
                                      

.. table:: DICOM Implementation Class and Version for STORAGE-SCU AE

   =========================== ======================
   Implementation Class UID    1.840.xxxxxxx.yyy.etc…
   Implementation Version Name EX_VERS_01
   =========================== ======================

Note that the STORAGE-SCU AE and QUERY-RETRIEVE-SCP AE use the same
Implementation Class UID. All EXAMPLE-QUERY-RETRIEVE-SERVER AEs use the
same Implementation Version Name. This Version Name is updated with each
new release of the product software, as the different AE versions are
never released independently.

.. _sect_F.4.2.1.3:

Association Initiation Policy
'''''''''''''''''''''''''''''

.. _sect_F.4.2.1.3.1:

Activity - Send Images Requested By an External Peer AE
                                                       

.. _sect_F.4.2.1.3.1.1:

Description and Sequencing of Activity
                                      

The STORAGE-SCU AE will initiate a new Association when the
QUERY-RETRIEVE-SCP AE invokes the STORAGE-SCU AE to transmit images. The
QUERY-RETRIEVE-SCP AE will issue such a command whenever it receives a
valid C-MOVE Request. An Association Request is sent to the specified
C-MOVE Destination AE and upon successful negotiation of the required
Presentation Context the image transfer is started. In all cases an
attempt will be made to transmit all the indicated images in a single
Association, but this may not always be possible. The Association will
be released when all the images have been sent. If an error occurs
during transmission over an open Association then the image transfer is
halted. The STORAGE-SCU AE will not attempt to independently retry the
image export.

Note that the STORAGE-SCU AE does not support the unsolicited sending of
SOP Instances using the DICOM Storage Service Class. It will only send
SOP Instances in response to a C-MOVE Request from a peer AE.

The following sequencing constraints illustrated in
`figure_title <#figure_F.4.2-1>`__ apply to the STORAGE-SCU AE:

1. Peer AE requests retrieval of Study, Series, or Images from
   QUERY-RETRIEVE-SCP AE (C-MOVE-RQ).

2. QUERY-RETRIEVE-SCP AE signals STORAGE-SCU AE to send the image
   Composite SOP Instances indicated in the C-MOVE-RQ to the C-MOVE
   Destination AE.

3. STORAGE-SCU AE opens a new Association with the indicated C-MOVE
   Destination AE.

4. STORAGE-SCU AE sends the indicated Composite SOP Instances.

5. STORAGE-SCU AE closes the Association.

6. The Verification Service is only supported as a utility function for
   Service staff. It is used only as a diagnostic tool.

.. _sect_F.4.2.1.3.1.2:

Proposed Presentation Contexts
                              

STORAGE-SCU AE will propose Presentation Contexts as shown in the
following table:

.. table:: Proposed Presentation Contexts By the STORAGE-SCU AE

   +------------+------------+------------+------------+-----+------+
   | Pr         |            |            |            |     |      |
   | esentation |            |            |            |     |      |
   | Context    |            |            |            |     |      |
   | Table      |            |            |            |     |      |
   +============+============+============+============+=====+======+
   | Name       | UID        | Name       | UID        |     |      |
   +------------+------------+------------+------------+-----+------+
   | Ve         | 1.2.840    | DICOM      | 1.2.840    | SCU | None |
   | rification | .10008.1.1 | Implicit   | .10008.1.2 |     |      |
   |            |            | VR Little  |            |     |      |
   |            |            | Endian     |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | US Image   | 1.2.8      | DICOM      | 1.2.840    | SCU | None |
   | Storage    | 40.10008.5 | Implicit   | .10008.1.2 |     |      |
   |            | .1.4.1.1.6 | VR Little  |            |     |      |
   | (Retired)  |            | Endian     |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | US Image   | 1.2.8      | DICOM      | 1.2.840.1  | SCU | None |
   | Storage    | 40.10008.5 | Explicit   | 0008.1.2.1 |     |      |
   |            | .1.4.1.1.6 | VR Little  |            |     |      |
   | (Retired)  |            | Endian     |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | US Image   | 1.2.8      | DICOM      | 1.         | SCU | None |
   | Storage    | 40.10008.5 | Explicit   | 2.840.1000 |     |      |
   |            | .1.4.1.1.6 | JPEG       | 8.1.2.4.50 |     |      |
   | (Retired)  |            | baseline   |            |     |      |
   |            |            | lossy      |            |     |      |
   |            |            | c          |            |     |      |
   |            |            | ompression |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | US Image   | 1.2.840    | DICOM      | 1.2.840    | SCU | None |
   | Storage    | .10008.5.1 | Implicit   | .10008.1.2 |     |      |
   |            | .4.1.1.6.1 | VR Little  |            |     |      |
   |            |            | Endian     |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | US Image   | 1.2.840    | DICOM      | 1.2.840.1  | SCU | None |
   | Storage    | .10008.5.1 | Explicit   | 0008.1.2.1 |     |      |
   |            | .4.1.1.6.1 | VR Little  |            |     |      |
   |            |            | Endian     |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | US Image   | 1.2.840    | DICOM      | 1.         | SCU | None |
   | Storage    | .10008.5.1 | Explicit   | 2.840.1000 |     |      |
   |            | .4.1.1.6.1 | JPEG       | 8.1.2.4.50 |     |      |
   |            |            | baseline   |            |     |      |
   |            |            | lossy      |            |     |      |
   |            |            | c          |            |     |      |
   |            |            | ompression |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | US         | 1.2.8      | DICOM      | 1.2.840    | SCU | None |
   | M          | 40.10008.5 | Implicit   | .10008.1.2 |     |      |
   | ulti-frame | .1.4.1.1.3 | VR Little  |            |     |      |
   | Storage    |            | Endian     |            |     |      |
   | (Retired)  |            |            |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | US         | 1.2.8      | DICOM      | 1.2.840.1  | SCU | None |
   | M          | 40.10008.5 | Explicit   | 0008.1.2.1 |     |      |
   | ulti-frame | .1.4.1.1.3 | VR Little  |            |     |      |
   | Storage    |            | Endian     |            |     |      |
   | (Retired)  |            |            |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | US         | 1.2.8      | DICOM      | 1.         | SCU | None |
   | M          | 40.10008.5 | Explicit   | 2.840.1000 |     |      |
   | ulti-frame | .1.4.1.1.3 | JPEG       | 8.1.2.4.50 |     |      |
   | Storage    |            | baseline   |            |     |      |
   | (Retired)  |            | lossy      |            |     |      |
   |            |            | c          |            |     |      |
   |            |            | ompression |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | US         | 1.2.840    | DICOM      | 1.2.840    | SCU | None |
   | M          | .10008.5.1 | Implicit   | .10008.1.2 |     |      |
   | ulti-frame | .4.1.1.3.1 | VR Little  |            |     |      |
   | Storage    |            | Endian     |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | US         | 1.2.840    | DICOM      | 1.2.840.1  | SCU | None |
   | M          | .10008.5.1 | Explicit   | 0008.1.2.1 |     |      |
   | ulti-frame | .4.1.1.3.1 | VR Little  |            |     |      |
   | Storage    |            | Endian     |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | US         | 1.2.840    | DICOM      | 1.         | SCU | None |
   | M          | .10008.5.1 | Explicit   | 2.840.1000 |     |      |
   | ulti-frame | .4.1.1.3.1 | JPEG       | 8.1.2.4.50 |     |      |
   | Storage    |            | baseline   |            |     |      |
   |            |            | lossy      |            |     |      |
   |            |            | c          |            |     |      |
   |            |            | ompression |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | Computer   | 1.2.8      | DICOM      | 1.2.840    | SCU | None |
   | R          | 40.10008.5 | Implicit   | .10008.1.2 |     |      |
   | adiography | .1.4.1.1.1 | VR Little  |            |     |      |
   | Image      |            | Endian     |            |     |      |
   | Storage    |            |            |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | Computer   | 1.2.8      | DICOM      | 1.2.840.1  | SCU | None |
   | R          | 40.10008.5 | Explicit   | 0008.1.2.1 |     |      |
   | adiography | .1.4.1.1.1 | VR Little  |            |     |      |
   | Image      |            | Endian     |            |     |      |
   | Storage    |            |            |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | CT Image   | 1.2.8      | DICOM      | 1.2.840    | SCU | None |
   | Storage    | 40.10008.5 | Implicit   | .10008.1.2 |     |      |
   |            | .1.4.1.1.2 | VR Little  |            |     |      |
   |            |            | Endian     |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | CT Image   | 1.2.8      | DICOM      | 1.2.840.1  | SCU | None |
   | Storage    | 40.10008.5 | Explicit   | 0008.1.2.1 |     |      |
   |            | .1.4.1.1.2 | VR Little  |            |     |      |
   |            |            | Endian     |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | MR Image   | 1.2.8      | DICOM      | 1.2.840    | SCU | None |
   | Storage    | 40.10008.5 | Implicit   | .10008.1.2 |     |      |
   |            | .1.4.1.1.4 | VR Little  |            |     |      |
   |            |            | Endian     |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | MR Image   | 1.2.8      | DICOM      | 1.2.840.1  | SCU | None |
   | Storage    | 40.10008.5 | Explicit   | 0008.1.2.1 |     |      |
   |            | .1.4.1.1.4 | VR Little  |            |     |      |
   |            |            | Endian     |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | Secondary  | 1.2.8      | DICOM      | 1.2.840    | SCU | None |
   | Capture    | 40.10008.5 | Implicit   | .10008.1.2 |     |      |
   | Image      | .1.4.1.1.7 | VR Little  |            |     |      |
   | Storage    |            | Endian     |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | Secondary  | 1.2.8      | DICOM      | 1.2.840.1  | SCU | None |
   | Capture    | 40.10008.5 | Explicit   | 0008.1.2.1 |     |      |
   | Image      | .1.4.1.1.7 | VR Little  |            |     |      |
   | Storage    |            | Endian     |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | Secondary  | 1.2.8      | DICOM      | 1.         | SCU | None |
   | Capture    | 40.10008.5 | Explicit   | 2.840.1000 |     |      |
   | Image      | .1.4.1.1.7 | JPEG       | 8.1.2.4.50 |     |      |
   | Storage    |            | baseline   |            |     |      |
   |            |            | lossy      |            |     |      |
   |            |            | c          |            |     |      |
   |            |            | ompression |            |     |      |
   +------------+------------+------------+------------+-----+------+

.. note::

   The SOP Classes and Transfer Syntaxes that the STORAGE-SCU AE
   proposes, as listed above, represent the default behavior. The
   STORAGE-SCU AE can be configured to propose a subset of these
   contexts or additional Presentation Contexts. Also, the default
   Behavior is to propose just a single Transfer Syntax per Presentation
   Context. However, this can be altered so that every proposed
   Presentation Context has a unique SOP Class and one or more Transfer
   Syntaxes. That is, the default behavior is to determine the Transfer
   Syntaxes the SCP can accept as opposed to which it prefers.

.. _sect_F.4.2.1.3.1.3:

SOP Specific Conformance for Verification SOP Class
                                                   

Standard conformance is provided to the DICOM Verification Service Class
as an SCU. The Verification Service as an SCU is actually only supported
as a diagnostic service tool for network communication issues.

.. _sect_F.4.2.1.3.1.4:

SOP Specific Conformance for Image SOP Classes
                                              

Composite DICOM SOP Instances are maintained as DICOM Part 10 compliant
files in the EXAMPLE-QUERY-RETRIEVE-SERVER database. The entire set of
tags received with the image will be saved in
EXAMPLE-QUERY-RETRIEVE-SERVER; this includes all Private and SOP
Extended Elements. When a SOP Instance is selected for export from
EXAMPLE-QUERY-RETRIEVE-SERVER, its content will be exported as it was
originally received except for a few possible exceptions. Some of the
Patient demographic and Study information Elements whose values can have
been altered due to changes administered on
EXAMPLE-QUERY-RETRIEVE-SERVER or changes to the state of the image data
due to compression can be altered when the SOP Instance is exported.

The Patient demographic and Study information can be entered or altered
by several means: manually, or from HL7 messaging,. The replacement
behavior depends on which specific DICOM and HL7 services are supported.
Also, this behavior is configurable. Values can be altered without
changing the SOP Instance UID unless otherwise noted. Refer to the Annex
for the specific details of which Elements can have their values altered
at time of export.

The EXAMPLE-QUERY-RETRIEVE-SERVER creates files called Service Logs that
can be used to monitor their status and diagnose any problems that may
arise. If any error occurs during DICOM communication then appropriate
messages are always output to these Service Logs. In addition, error
messages may be output as alerts to the User Interface in certain cases.

The STORAGE-SCU AE will exhibit the following Behavior according to the
Status Code value returned in a C-STORE Response from a destination
C-STORE SCP:

.. table:: STORAGE-SCU AE C-STORE Response Status Handling Behavior

   +----------------+----------------+----------------+----------------+
   | Service Status | Further        | Error Code     | Behavior       |
   |                | Meaning        |                |                |
   +================+================+================+================+
   | Success        | Success        | 0000           | The SCP has    |
   |                |                |                | successfully   |
   |                |                |                | stored the     |
   |                |                |                | exported SOP   |
   |                |                |                | Instance. A    |
   |                |                |                | message is     |
   |                |                |                | sent to the    |
   |                |                |                | QUER           |
   |                |                |                | Y-RETRIEVE-SCP |
   |                |                |                | AE indicating  |
   |                |                |                | successful     |
   |                |                |                | export. The    |
   |                |                |                | QUER           |
   |                |                |                | Y-RETRIEVE-SCP |
   |                |                |                | AE will send   |
   |                |                |                | the            |
   |                |                |                | appropriate    |
   |                |                |                | PENDING or     |
   |                |                |                | SUCCESS Status |
   |                |                |                | in the C-MOVE  |
   |                |                |                | Response.      |
   |                |                |                |                |
   |                |                |                | Success        |
   |                |                |                | indication     |
   |                |                |                | message is     |
   |                |                |                | output to the  |
   |                |                |                | Service Logs.  |
   |                |                |                |                |
   |                |                |                | No message is  |
   |                |                |                | posted to the  |
   |                |                |                | User           |
   |                |                |                | Interface.     |
   +----------------+----------------+----------------+----------------+
   | Refused        | Out of         | A700 -A7FF     | This is        |
   |                | Resources      |                | treated as a   |
   |                |                |                | permanent      |
   |                |                |                | Failure. A     |
   |                |                |                | message is     |
   |                |                |                | sent to the    |
   |                |                |                | QUER           |
   |                |                |                | Y-RETRIEVE-SCP |
   |                |                |                | AE indicating  |
   |                |                |                | an export      |
   |                |                |                | failure and    |
   |                |                |                | the            |
   |                |                |                | Association is |
   |                |                |                | released. The  |
   |                |                |                | QUER           |
   |                |                |                | Y-RETRIEVE-SCP |
   |                |                |                | AE will send   |
   |                |                |                | an appropriate |
   |                |                |                | Status in the  |
   |                |                |                | C-MOVE         |
   |                |                |                | Response.      |
   |                |                |                |                |
   |                |                |                | Error          |
   |                |                |                | indication     |
   |                |                |                | message is     |
   |                |                |                | output to the  |
   |                |                |                | Service Logs.  |
   |                |                |                |                |
   |                |                |                | No message is  |
   |                |                |                | posted to the  |
   |                |                |                | User           |
   |                |                |                | Interface.     |
   +----------------+----------------+----------------+----------------+
   | Error          | Data Set does  | A900 -A9FF     | This is        |
   |                | not match SOP  |                | treated as a   |
   |                | Class          |                | permanent      |
   |                |                |                | Failure. A     |
   |                |                |                | message is     |
   |                |                |                | sent to the    |
   |                |                |                | QUER           |
   |                |                |                | Y-RETRIEVE-SCP |
   |                |                |                | AE indicating  |
   |                |                |                | an export      |
   |                |                |                | failure and    |
   |                |                |                | the            |
   |                |                |                | Association is |
   |                |                |                | released. The  |
   |                |                |                | QUER           |
   |                |                |                | Y-RETRIEVE-SCP |
   |                |                |                | AE will send   |
   |                |                |                | an appropriate |
   |                |                |                | Status in the  |
   |                |                |                | C-MOVE         |
   |                |                |                | Response.      |
   |                |                |                |                |
   |                |                |                | Error          |
   |                |                |                | indication     |
   |                |                |                | message is     |
   |                |                |                | output to the  |
   |                |                |                | Service Logs.  |
   |                |                |                |                |
   |                |                |                | No message is  |
   |                |                |                | posted to the  |
   |                |                |                | User           |
   |                |                |                | Interface.     |
   +----------------+----------------+----------------+----------------+
   | Error          | Cannot         | C000 -CFFF     | This is        |
   |                | Understand     |                | treated as a   |
   |                |                |                | permanent      |
   |                |                |                | Failure. A     |
   |                |                |                | message is     |
   |                |                |                | sent to the    |
   |                |                |                | QUER           |
   |                |                |                | Y-RETRIEVE-SCP |
   |                |                |                | AE indicating  |
   |                |                |                | an export      |
   |                |                |                | failure and    |
   |                |                |                | the            |
   |                |                |                | Association is |
   |                |                |                | released. The  |
   |                |                |                | QUER           |
   |                |                |                | Y-RETRIEVE-SCP |
   |                |                |                | AE will send   |
   |                |                |                | an appropriate |
   |                |                |                | Status in the  |
   |                |                |                | C-MOVE         |
   |                |                |                | Response.      |
   |                |                |                |                |
   |                |                |                | Error          |
   |                |                |                | indication     |
   |                |                |                | message is     |
   |                |                |                | output to the  |
   |                |                |                | Service Logs.  |
   |                |                |                |                |
   |                |                |                | No message is  |
   |                |                |                | posted to the  |
   |                |                |                | User           |
   |                |                |                | Interface.     |
   +----------------+----------------+----------------+----------------+
   | Warning        | Coercion of    | B000           | Image          |
   |                | Data Elements  |                | transmission   |
   |                |                |                | is considered  |
   |                |                |                | successful. A  |
   |                |                |                | message is     |
   |                |                |                | sent to the    |
   |                |                |                | QUER           |
   |                |                |                | Y-RETRIEVE-SCP |
   |                |                |                | AE indicating  |
   |                |                |                | successful     |
   |                |                |                | export. The    |
   |                |                |                | QUER           |
   |                |                |                | Y-RETRIEVE-SCP |
   |                |                |                | AE will send   |
   |                |                |                | the            |
   |                |                |                | appropriate    |
   |                |                |                | PENDING or     |
   |                |                |                | SUCCESS Status |
   |                |                |                | in the C-MOVE  |
   |                |                |                | Response.      |
   |                |                |                |                |
   |                |                |                | Warning        |
   |                |                |                | indication     |
   |                |                |                | message is     |
   |                |                |                | output to the  |
   |                |                |                | Service Logs.  |
   |                |                |                |                |
   |                |                |                | No message is  |
   |                |                |                | posted to the  |
   |                |                |                | User           |
   |                |                |                | Interface.     |
   +----------------+----------------+----------------+----------------+
   | Warning        | Data Set does  | B007           | Image          |
   |                | not match SOP  |                | transmission   |
   |                | Class          |                | is considered  |
   |                |                |                | successful. A  |
   |                |                |                | message is     |
   |                |                |                | sent to the    |
   |                |                |                | QUER           |
   |                |                |                | Y-RETRIEVE-SCP |
   |                |                |                | AE indicating  |
   |                |                |                | successful     |
   |                |                |                | export. The    |
   |                |                |                | QUER           |
   |                |                |                | Y-RETRIEVE-SCP |
   |                |                |                | AE will send   |
   |                |                |                | the            |
   |                |                |                | appropriate    |
   |                |                |                | PENDING or     |
   |                |                |                | SUCCESS Status |
   |                |                |                | in the C-MOVE  |
   |                |                |                | Response.      |
   |                |                |                |                |
   |                |                |                | Warning        |
   |                |                |                | indication     |
   |                |                |                | message is     |
   |                |                |                | output to the  |
   |                |                |                | Service Logs.  |
   |                |                |                |                |
   |                |                |                | No message is  |
   |                |                |                | posted to the  |
   |                |                |                | User           |
   |                |                |                | Interface.     |
   +----------------+----------------+----------------+----------------+
   | Warning        | Elements       | B006           | Image          |
   |                | Discarded      |                | transmission   |
   |                |                |                | is considered  |
   |                |                |                | successful. A  |
   |                |                |                | message is     |
   |                |                |                | sent to the    |
   |                |                |                | QUER           |
   |                |                |                | Y-RETRIEVE-SCP |
   |                |                |                | AE indicating  |
   |                |                |                | successful     |
   |                |                |                | export. The    |
   |                |                |                | QUER           |
   |                |                |                | Y-RETRIEVE-SCP |
   |                |                |                | AE will send   |
   |                |                |                | the            |
   |                |                |                | appropriate    |
   |                |                |                | PENDING or     |
   |                |                |                | SUCCESS Status |
   |                |                |                | in the C-MOVE  |
   |                |                |                | Response.      |
   |                |                |                |                |
   |                |                |                | Warning        |
   |                |                |                | indication     |
   |                |                |                | message is     |
   |                |                |                | output to the  |
   |                |                |                | Service Logs.  |
   |                |                |                |                |
   |                |                |                | No message is  |
   |                |                |                | posted to the  |
   |                |                |                | User           |
   |                |                |                | Interface.     |
   +----------------+----------------+----------------+----------------+
   | Warning        | Attribute List | 0107           | Image          |
   |                | Error          |                | transmission   |
   |                |                |                | is considered  |
   |                |                |                | successful. A  |
   |                |                |                | message is     |
   |                |                |                | sent to the    |
   |                |                |                | QUER           |
   |                |                |                | Y-RETRIEVE-SCP |
   |                |                |                | AE indicating  |
   |                |                |                | successful     |
   |                |                |                | export. The    |
   |                |                |                | QUER           |
   |                |                |                | Y-RETRIEVE-SCP |
   |                |                |                | AE will send   |
   |                |                |                | the            |
   |                |                |                | appropriate    |
   |                |                |                | PENDING or     |
   |                |                |                | SUCCESS Status |
   |                |                |                | in the C-MOVE  |
   |                |                |                | Response.      |
   |                |                |                |                |
   |                |                |                | Warning        |
   |                |                |                | indication     |
   |                |                |                | message is     |
   |                |                |                | output to the  |
   |                |                |                | Service Logs.  |
   |                |                |                |                |
   |                |                |                | No message is  |
   |                |                |                | posted to the  |
   |                |                |                | User           |
   |                |                |                | Interface.     |
   +----------------+----------------+----------------+----------------+
   | Warning        | Attribute      | 0116           | Image          |
   |                | Value Out of   |                | transmission   |
   |                | Range          |                | is considered  |
   |                |                |                | successful. A  |
   |                |                |                | message is     |
   |                |                |                | sent to the    |
   |                |                |                | QUER           |
   |                |                |                | Y-RETRIEVE-SCP |
   |                |                |                | AE indicating  |
   |                |                |                | successful     |
   |                |                |                | export. The    |
   |                |                |                | QUER           |
   |                |                |                | Y-RETRIEVE-SCP |
   |                |                |                | AE will send   |
   |                |                |                | the            |
   |                |                |                | appropriate    |
   |                |                |                | PENDING or     |
   |                |                |                | SUCCESS Status |
   |                |                |                | in the C-MOVE  |
   |                |                |                | Response.      |
   |                |                |                |                |
   |                |                |                | Warning        |
   |                |                |                | indication     |
   |                |                |                | message is     |
   |                |                |                | output to the  |
   |                |                |                | Service Logs.  |
   |                |                |                |                |
   |                |                |                | No message is  |
   |                |                |                | posted to the  |
   |                |                |                | User           |
   |                |                |                | Interface.     |
   +----------------+----------------+----------------+----------------+
   | \*             | \*             | Any other      | This is        |
   |                |                | status code.   | treated as a   |
   |                |                |                | permanent      |
   |                |                |                | Failure. A     |
   |                |                |                | message is     |
   |                |                |                | sent to the    |
   |                |                |                | QUER           |
   |                |                |                | Y-RETRIEVE-SCP |
   |                |                |                | AE indicating  |
   |                |                |                | an export      |
   |                |                |                | failure and    |
   |                |                |                | the            |
   |                |                |                | Association is |
   |                |                |                | released. The  |
   |                |                |                | QUER           |
   |                |                |                | Y-RETRIEVE-SCP |
   |                |                |                | AE will send   |
   |                |                |                | an appropriate |
   |                |                |                | Status in the  |
   |                |                |                | C-MOVE         |
   |                |                |                | Response.      |
   |                |                |                |                |
   |                |                |                | Error          |
   |                |                |                | indication     |
   |                |                |                | message is     |
   |                |                |                | output to the  |
   |                |                |                | Service Logs.  |
   |                |                |                |                |
   |                |                |                | No message is  |
   |                |                |                | posted to the  |
   |                |                |                | User           |
   |                |                |                | Interface.     |
   +----------------+----------------+----------------+----------------+

All Status Codes indicating an error or refusal are treated as a
permanent failure. The STORAGE-SCU AE never automatically resends images
when an error Status Code is returned in a C-STORE Response. For
specific behavior regarding Status Code values returned in C-MOVE
Responses, refer to the Services Supported as an SCP by the
QUERY-RETRIEVE-SCP AE.

.. table:: STORAGE-SCU AE Communication Failure Behavior

   +----------------------------------+----------------------------------+
   | Exception                        | Behavior                         |
   +==================================+==================================+
   | Timeout expiry for an expected   | The Association is aborted using |
   | DICOM Message Response (DIMSE    | a DICOM A-ABORT and a message is |
   | level timeout).                  | sent to the QUERY-RETRIEVE-SCP   |
   |                                  | AE indicating an export failure. |
   |                                  | The QUERY-RETRIEVE-SCP AE will   |
   |                                  | send an appropriate Status in    |
   |                                  | the C-MOVE Response.             |
   |                                  |                                  |
   |                                  | Error indication message is      |
   |                                  | output to the Service Logs.      |
   |                                  |                                  |
   |                                  | No message is posted to the User |
   |                                  | Interface.                       |
   +----------------------------------+----------------------------------+
   | Timeout expiry for an expected   | The Association is aborted using |
   | DICOM PDU or TCP/IP packet       | a DICOM A-ABORT and a message is |
   | (Low-level timeout).             | sent to the QUERY-RETRIEVE-SCP   |
   |                                  | AE indicating an export failure. |
   |                                  | The QUERY-RETRIEVE-SCP AE will   |
   |                                  | send an appropriate Status in    |
   |                                  | the C-MOVE Response.             |
   |                                  |                                  |
   |                                  | Error indication message is      |
   |                                  | output to the Service Logs.      |
   |                                  |                                  |
   |                                  | No message is posted to the User |
   |                                  | Interface.                       |
   +----------------------------------+----------------------------------+
   | Association A-ABORTed by the SCP | A message is sent to the         |
   | or the network layers indicate   | QUERY-RETRIEVE-SCP AE indicating |
   | communication loss (i.e.,        | an export failure. The           |
   | low-level TCP/IP socket closure) | QUERY-RETRIEVE-SCP AE will send  |
   |                                  | an appropriate Status in the     |
   |                                  | C-MOVE Response.                 |
   |                                  |                                  |
   |                                  | Error indication message is      |
   |                                  | output to the Service Logs.      |
   |                                  |                                  |
   |                                  | No message is posted to the User |
   |                                  | Interface.                       |
   +----------------------------------+----------------------------------+

.. _sect_F.4.2.1.4:

Association Acceptance Policy
'''''''''''''''''''''''''''''

The STORAGE-SCU AE does not accept Associations.

.. _sect_F.4.2.2:

QUERY-RETRIEVE-SCP Application Entity Specification
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. _sect_F.4.2.2.1:

SOP Classes
'''''''''''

The QUERY-RETRIEVE-SCP AE provides Standard Conformance to the following
DICOM SOP Classes:

.. table:: SOP Classes for QUERY-RETRIEVE-SCP AE

   +---------------------------+---------------------------+-----+-----+
   | SOP Class Name            | SOP Class UID             | SCU | SCP |
   +===========================+===========================+=====+=====+
   | Patient Root Q/R          | 1.                        | No  | Yes |
   | Information Model - FIND  | 2.840.10008.5.1.4.1.2.1.1 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | Patient Root Q/R          | 1.                        | No  | Yes |
   | Information Model - MOVE  | 2.840.10008.5.1.4.1.2.1.2 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | Study Root Q/R            | 1.                        | No  | Yes |
   | Information Model - FIND  | 2.840.10008.5.1.4.1.2.2.1 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | Study Root Q/R            | 1.                        | No  | Yes |
   | Information Model - MOVE  | 2.840.10008.5.1.4.1.2.2.2 |     |     |
   +---------------------------+---------------------------+-----+-----+

.. _sect_F.4.2.2.2:

Association Policies
''''''''''''''''''''

.. _sect_F.4.2.2.2.1:

General
       

The QUERY-RETRIEVE-SCP AE will never initiate Associations; it only
accepts Association Requests from external DICOM AEs. The
QUERY-RETRIEVE-SCP AE will accept Associations for Verification, C-FIND,
and C-MOVE requests. In the case of a C-MOVE request, the
QUERY-RETRIEVE-SCP AE will issue a command to the STORAGE-SCU AE to
initiate an Association with the Destination DICOM AE to send images as
specified by the originator of the C-MOVE Request.

The DICOM standard Application Context Name for DICOM is always
accepted:

.. table:: DICOM Application Context for QUERY-RETRIEVE-SCP AE

   ======================== =====================
   Application Context Name 1.2.840.10008.3.1.1.1
   ======================== =====================

.. _sect_F.4.2.2.2.2:

Number of Associations
                      

The QUERY-RETRIEVE-SCP AE can support multiple simultaneous
Associations. Each time the QUERY-RETRIEVE-SCP AE receives an
Association, a child process will be spawned to process the
Verification, Query, or Retrieval request. The maximum number of child
processes, and thus the maximum number of simultaneous Associations that
can be processed, is set by configuration. The default maximum is 10 in
total. The maximum number of simultaneous Associations can be either an
absolute number or a maximum number for each requesting external
Application Entity. The latter flexibility can be useful if
communication with one external AE is unreliable and one does not wish
'hung' connections with this AE to prevent Associations with other
client AEs.

.. table:: Number of Simultaneous Associations as a SCP for
QUERY-RETRIEVE-SCP AE

   =========================================== =================
   Maximum number of simultaneous Associations 10 (Configurable)
   =========================================== =================

.. _sect_F.4.2.2.2.3:

Asynchronous Nature
                   

The QUERY-RETRIEVE-SCP AE does not support asynchronous communication
(multiple outstanding transactions over a single Association). All
Association requests must be completed and acknowledged before a new
operation can be initiated.

.. table:: Asynchronous Nature as a SCP for QUERY-RETRIEVE-SCP AE

   +----------------------------------------------+----------------------+
   | Maximum number of outstanding asynchronous   | 1 (Not Configurable) |
   | transactions                                 |                      |
   +----------------------------------------------+----------------------+

.. _sect_F.4.2.2.2.4:

Implementation Identifying Information
                                      

The implementation information for the Application Entity is:

.. table:: DICOM Implementation Class and Version for QUERY-RETRIEVE-SCP
AE

   =========================== ======================
   Implementation Class UID    1.840.xxxxxxx.yyy.etc…
   Implementation Version Name EX_VERS_01
   =========================== ======================

Note that the STORAGE-SCU AE, and QUERY-RETRIEVE-SCP AE use the same
Implementation Class UID. All EXAMPLE-QUERY-RETRIEVE-SERVER AEs use the
same Implementation Version Name. This Version Name is updated with each
new release of the product software, as the different AE versions are
never released independently.

.. _sect_F.4.2.2.3:

Association Initiation Policy
'''''''''''''''''''''''''''''

The QUERY-RETRIEVE-SCP AE does not initiate Associations.

.. _sect_F.4.2.2.4:

Association Acceptance Policy
'''''''''''''''''''''''''''''

.. _sect_F.4.2.2.4.1:

Activity - Handling Query and Retrieval Requests
                                                

.. _sect_F.4.2.2.4.1.1:

Description and Sequencing of Activity
                                      

The QUERY-RETRIEVE-SCP AE accepts Associations only if they have valid
Presentation Contexts. If none of the requested Presentation Contexts
are accepted then the Association Request itself is rejected. It can be
configured to only accept Associations with certain hosts (using TCP/IP
address) and/or Application Entity Titles.

If QUERY-RETRIEVE-SCP AE receives a query (C-FIND) request then the
response(s) will be sent over the same Association used to send the
C-FIND-Request.

If QUERY-RETRIEVE-SCP AE receives a retrieval (C-MOVE) request then the
responses will be sent over the same Association used to send the
C-MOVE-Request. The QUERY-RETRIEVE-SCP AE will notify the STORAGE-SCU to
send the requested SOP Instances to the C-MOVE Destination. The
STORAGE-SCU AE notifies the QUERY-RETRIEVE-SCP AE of the success or
failure of each attempt to send a Composite SOP Instance to the peer
C-MOVE Destination AE. The QUERY-RETRIEVE-SCP AE then sends a C-MOVE
Response indicating this status after each attempt. Once the STORAGE-SCU
AE has finished attempting to transfer all the requested SOP Instances,
the QUERY-RETRIEVE-SCP AE sends a final C-MOVE Response indicating the
overall status of the attempted retrieval.

The following sequencing constraints illustrated in
`figure_title <#figure_F.4.2-2>`__ apply to the QUERY-RETRIEVE-SCP AE
for handling queries (C-FIND-Requests) :

1. Peer AE opens an Association with the QUERY-RETRIEVE-SCP AE.

2. Peer AE sends a C-FIND-RQ Message

3. QUERY-RETRIEVE-SCP AE returns a C-FIND-RSP Message to the peer AE
   with matching information. A C-FIND-RSP is sent for each entity
   matching the identifier specified in the C-FIND-RQ. A final
   C-FIND-RSP is sent indicating that the matching is complete.

4. Peer AE closes the Association. Note that the peer AE does not have
   to close the Association immediately. Further C-FIND or C-MOVE
   Requests can be sent over the Association before it is closed.

The following sequencing constraints illustrated in
`figure_title <#figure_F.4.2-2>`__ apply to the QUERY-RETRIEVE-SCP AE
for handling retrievals (C-MOVE-Requests) :

1. Peer AE opens an Association with the QUERY-RETRIEVE-SCP AE.

2. Peer AE sends a C-MOVE-RQ Message

3. QUERY-RETRIEVE-SCP AE notifies the STORAGE-SCU AE to send the
   Composite SOP Instances to the peer C-MOVE Destination AE as
   indicated in the C-MOVE-RQ.

4. After attempting to send a SOP Instance, the STORAGE-SCU AE indicates
   to the QUERY-RETRIEVE-SCP AE whether the transfer succeeded or
   failed. The QUERY-RETRIEVE-SCP AE then returns a C-MOVE-RSP
   indicating this success or failure.

5. Once the STORAGE-SCU AE has completed all attempts to transfer the
   SOP Instances to the C-MOVE Destination AE, or the first failure
   occurred, the QUERY-RETRIEVE-SCP AE sends a final C-MOVE-RSP
   indicating the overall success or failure of the retrieval.

6. Peer AE closes the Association. Note that the peer AE does not have
   to close the Association immediately. Further C-FIND or C-MOVE
   Requests can be sent over the Association before it is closed.

The QUERY-RETRIEVE-SCP AE may reject Association attempts as shown in
the table below. The Result, Source and Reason/Diag columns represent
the values returned in the corresponding fields of an ASSOCIATE-RJ PDU
(see ). The following abbreviations are used in the Source column:

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

.. _sect_F.4.2.2.4.1.2:

Accepted Presentation Contexts
                              

QUERY-RETRIEVE-SCP AE will accept Presentation Contexts as shown in the
following table:

.. table:: Accepted Presentation Contexts By the QUERY-RETRIEVE-SCP AE

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
   | Patient    | 1.2.840    | DICOM      | 1.2.840    | SCP | None |
   | Root Q/R   | .10008.5.1 | Implicit   | .10008.1.2 |     |      |
   | I          | .4.1.2.1.1 | VR Little  |            |     |      |
   | nformation |            | Endian     |            |     |      |
   | Model -    |            |            |            |     |      |
   | FIND       |            |            |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | Patient    | 1.2.840    | DICOM      | 1.2.840    | SCP | None |
   | Root Q/R   | .10008.5.1 | Implicit   | .10008.1.2 |     |      |
   | I          | .4.1.2.1.2 | VR Little  |            |     |      |
   | nformation |            | Endian     |            |     |      |
   | Model -    |            |            |            |     |      |
   | MOVE       |            |            |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | Study Root | 1.2.840    | DICOM      | 1.2.840    | SCP | None |
   | Q/R        | .10008.5.1 | Implicit   | .10008.1.2 |     |      |
   | I          | .4.1.2.2.1 | VR Little  |            |     |      |
   | nformation |            | Endian     |            |     |      |
   | Model -    |            |            |            |     |      |
   | FIND       |            |            |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | Study Root | 1.2.840    | DICOM      | 1.2.840    | SCP | None |
   | Q/R        | .10008.5.1 | Implicit   | .10008.1.2 |     |      |
   | I          | .4.1.2.2.2 | VR Little  |            |     |      |
   | nformation |            | Endian     |            |     |      |
   | Model -    |            |            |            |     |      |
   | MOVE       |            |            |            |     |      |
   +------------+------------+------------+------------+-----+------+

.. _sect_F.4.2.2.4.1.3:

SOP Specific Conformance for Query SOP Classes
                                              

The QUERY-RETRIEVE-SCP AE supports hierarchical queries and not
relational queries. There are no attributes always returned by default.
Only those attributes requested in the query identifier are returned.
Query responses always return values from the
EXAMPLE-QUERY-RETRIEVE-SERVER database. Exported SOP Instances are
always updated with the latest values in the database prior to export.
Thus, a change in Patient demographic information will be contained in
both the C-FIND Responses and any Composite SOP Instances exported to a
C-MOVE Destination AE.

Patient Root Information Model

All required search keys on each of the four levels (Patient, Study,
Series, and Image) are supported. However, the Patient ID (0010,0020)
key must have at least a partial value if the Patient's Name (0010,0010)
is not present in a Patient Level query.

Study Root Information Model

All the required search keys on each of the three levels (Study, Series,
and Image) are supported. If no partial values are specified for Study
attributes then either the Patient ID (0010,0020) key or the Patient's
Name (0010,0010) must have at least a partial value specified.

.. table:: Patient Root C-FIND SCP Supported Elements

   ========================== ========= == =================
   Level Name                 Tag       VR Types of Matching
                                           
   Attribute Name                          
   ========================== ========= == =================
   SOP Common                              
   Specific Character Set     0008,0005 CS NONE
   Patient Level                           
   Patient's Name             0010,0010 PN S,*,U
                                           
   Patient ID                 0010,0020 LO S,*,U
                                           
   Patient's Birth Date       0010,0030 DA S,U
                                           
   Patient's Sex              0010,0040 CS S,U
                                           
   Other Patient IDs          0010,1000 LO NONE
                                           
   Other Patient Names        0010,1001 PN NONE
   Study Level                             
   Study Date                 0008,0020 DA S,R,U
                                           
   Study Time                 0008,0030 TM R,U
                                           
   Accession Number           0008,0050 SH S,*,U
                                           
   Study ID                   0020,0010 SH S,*,U
                                           
   Study Instance UID         0020,000D UI S,U,L
                                           
   Referring Physician's Name 0008,0090 PN S,*,U
                                           
   Study Description          0008,1030 LO S,*,U
   Series Level                            
   Modality                   0008,0060 CS S,U
                                           
   Series Number              0020,0011 IS S,*,U
                                           
   Series Instance UID        0020,000E UI S,U,L
                                           
   Operator's Name            0008,1070 PN NONE
   Image Level                             
   Instance Number            0020,0013 IS S,*,U
                                           
   SOP Instance UID           0008,0018 UI S,U,L
   ========================== ========= == =================

.. table:: Study Root C-FIND SCP Supported Elements

   ========================== ========= == =================
   Level Name                 Tag       VR Types of Matching
                                           
   Attribute Name                          
   ========================== ========= == =================
   SOP Common                              
   Specific Character Set     0008,0005 CS NONE
   Study Level                             
   Patient's Name             0010,0010 PN S,*,U
                                           
   Patient ID                 0010,0020 LO S,*,U
                                           
   Patient's Birth Date       0010,0030 DA S,U
                                           
   Patient's Sex              0010,0040 CS S,U
                                           
   Other Patient IDs          0010,1000 LO NONE
                                           
   Other Patient Names        0010,1001 PN NONE
                                           
   Study Date                 0008,0020 DA S,R,U
                                           
   Study Time                 0008,0030 TM R,U
                                           
   Accession Number           0008,0050 SH S,*,U
                                           
   Study ID                   0020,0010 SH S,*,U
                                           
   Study Instance UID         0020,000D UI S,U,L
                                           
   Referring Physician's Name 0008,0090 PN S,*,U
                                           
   Study Description          0008,1030 LO S,*,U
   Series Level                            
   Modality                   0008,0060 CS S,U
                                           
   Series Number              0020,0011 IS S,*,U
                                           
   Series Instance UID        0020,000E UI S,U,L
                                           
   Operator's Name            0008,1070 PN NONE
   Image Level                             
   Instance Number            0020,0013 IS S,*,U
                                           
   SOP Instance UID           0008,0018 UI S,U,L
   ========================== ========= == =================

The tables should be read as follows:

Attribute Name: Attributes supported for returned C-FIND Responses.

Tag: Appropriate DICOM tag for this attribute.

VR: Appropriate DICOM VR for this attribute.

Types of Matching: The types of Matching supported by the C-FIND SCP. A
"S" indicates the identifier attribute can specify Single Value
Matching, a "R" will indicate Range Matching, a "*" will denote wild
card matching, an 'U' will indicate universal matching, and 'L' will
indicate that UID lists are supported for matching. "NONE" indicates
that no matching is supported, but that values for this Element in the
database can be returned.

.. table:: QUERY-RETRIEVE-SCP AE C-FIND Response Status Return Behavior

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
   | Refused        | Out of         | A700           | System reached |
   |                | Resources      |                | the limit in   |
   |                |                |                | disk space or  |
   |                |                |                | memory usage.  |
   |                |                |                |                |
   |                |                |                | Error message  |
   |                |                |                | is output to   |
   |                |                |                | as an alert to |
   |                |                |                | the User       |
   |                |                |                | Interface, and |
   |                |                |                | to the Service |
   |                |                |                | Log.           |
   +----------------+----------------+----------------+----------------+
   | Failed         | Identifier     | A900           | The C-FIND     |
   |                | does not match |                | query          |
   |                | SOP Class      |                | identifier     |
   |                |                |                | contains       |
   |                |                |                | invalid        |
   |                |                |                | Elements or    |
   |                |                |                | values, or is  |
   |                |                |                | missing        |
   |                |                |                | mandatory      |
   |                |                |                | Elements or    |
   |                |                |                | values for the |
   |                |                |                | specified SOP  |
   |                |                |                | Class.         |
   |                |                |                |                |
   |                |                |                | Error message  |
   |                |                |                | is output to   |
   |                |                |                | the Service    |
   |                |                |                | Log.           |
   +----------------+----------------+----------------+----------------+
   | Unable to      | C001           | The C-FIND     |                |
   | process        |                | query          |                |
   |                |                | identifier is  |                |
   |                |                | valid for the  |                |
   |                |                | specified SOP  |                |
   |                |                | Class but      |                |
   |                |                | cannot be used |                |
   |                |                | to query the   |                |
   |                |                | database. For  |                |
   |                |                | example, this  |                |
   |                |                | can occur if a |                |
   |                |                | Patient Level  |                |
   |                |                | query is       |                |
   |                |                | issued but the |                |
   |                |                | identifier has |                |
   |                |                | only empty     |                |
   |                |                | values for     |                |
   |                |                | both the       |                |
   |                |                | Patient ID and |                |
   |                |                | the Patient    |                |
   |                |                | Name.          |                |
   |                |                |                |                |
   |                |                | Error message  |                |
   |                |                | is output to   |                |
   |                |                | the Service    |                |
   |                |                | Log.           |                |
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
   |                | continuing and |                | the search for |
   |                | current match  |                | further        |
   |                | is supplied.   |                | matches is     |
   |                |                |                | continuing.    |
   |                |                |                | This is        |
   |                |                |                | returned when  |
   |                |                |                | each           |
   |                |                |                | successful     |
   |                |                |                | match is       |
   |                |                |                | returned and   |
   |                |                |                | when further   |
   |                |                |                | matches are    |
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
   | continuing but |                | the search for |                |
   | one or more    |                | further        |                |
   | Optional Keys  |                | matches is     |                |
   | were not       |                | continuing.    |                |
   | supported.     |                | This is        |                |
   |                |                | returned when  |                |
   |                |                | each           |                |
   |                |                | successful     |                |
   |                |                | match is       |                |
   |                |                | returned and   |                |
   |                |                | when further   |                |
   |                |                | matches are    |                |
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

.. _sect_F.4.2.2.4.1.4:

SOP Specific Conformance for Retrieval SOP Classes
                                                  

The QUERY-RETRIEVE-SCP AE will convey to the STORAGE-SCU AE that an
Association with a DICOM Application Entity named by the external C-MOVE
SCU (through a MOVE Destination AE Title) should be established. It will
also convey to the STORAGE-SCU AE to perform C-STORE operations on
specific images requested by the external C-MOVE SCU. One or more of the
Image Storage Presentation Contexts listed in
`table_title <#table_F.4.2-6>`__ will be negotiated.

The QUERY-RETRIEVE-SCP AE can support lists of UIDs in the C-MOVE
Request at the Study, Series, and Image Levels. The list of UIDs must be
at the Level of the C-MOVE Request however. For example, if the C-MOVE
Request is for Series Level retrieval but the identifier contains a list
of Study UIDs then the C-MOVE Request will be rejected, and the A900
Failed Status Code will be returned in the C-MOVE Response.

An initial C-MOVE Response is always sent after confirming that the
C-MOVE Request itself can be processed. After this, the
QUERY-RETRIEVE-SCP AE will return a response to the C-MOVE SCU after the
STORAGE-SCU AE has attempted to send each image. This response reports
the number of remaining SOP Instances to transfer, and the number
transferred having a successful, failed, or warning status. If the
Composite SOP Instances must be retrieved from long-term archive prior
to export there may be quite a long delay between the first C-MOVE
Response and the next one after the attempt to export the first image.
The maximum length of time for this delay will depend on the particular
type of archive used but typically varies between 3 and 10 minutes.

.. table:: QUERY-RETRIEVE-SCP AE C-MOVE Response Status Return Behavior

   +----------------+----------------+----------------+----------------+
   | Service Status | Further        | Error Code     | Behavior       |
   |                | Meaning        |                |                |
   +================+================+================+================+
   | Success        | Sub-operations | 0000           | All the        |
   |                | complete - No  |                | Composite SOP  |
   |                | Failures       |                | Instances have |
   |                |                |                | been           |
   |                |                |                | successfully   |
   |                |                |                | sent to the    |
   |                |                |                | C-MOVE         |
   |                |                |                | Destination    |
   |                |                |                | AE.            |
   +----------------+----------------+----------------+----------------+
   | Refused        | Out of         | A701           | Number of      |
   |                | Resources -    |                | matches cannot |
   |                | Unable to      |                | be determined  |
   |                | calculate      |                | due to system  |
   |                | number of      |                | failure.       |
   |                | matches        |                | Returned if    |
   |                |                |                | the server's   |
   |                |                |                | database is    |
   |                |                |                | not            |
   |                |                |                | functioning so |
   |                |                |                | the search for |
   |                |                |                | matches to the |
   |                |                |                | C-MOVE Request |
   |                |                |                | cannot be      |
   |                |                |                | found.         |
   |                |                |                |                |
   |                |                |                | Error message  |
   |                |                |                | is output as   |
   |                |                |                | an alert on    |
   |                |                |                | the User       |
   |                |                |                | Interface, and |
   |                |                |                | to the Service |
   |                |                |                | Log.           |
   +----------------+----------------+----------------+----------------+
   | Out of         | A702           | C-STORE        |                |
   | Resources -    |                | sub-operations |                |
   | Unable to      |                | cannot be      |                |
   | perform        |                | performed due  |                |
   | sub-operations |                | to failure to  |                |
   |                |                | access         |                |
   |                |                | Composite SOP  |                |
   |                |                | Instances in   |                |
   |                |                | archive, or    |                |
   |                |                | failure of a   |                |
   |                |                | C-STORE        |                |
   |                |                | Request. For   |                |
   |                |                | example, this  |                |
   |                |                | Status will be |                |
   |                |                | returned if    |                |
   |                |                | the required   |                |
   |                |                | SOP Instances  |                |
   |                |                | are determined |                |
   |                |                | to be off-line |                |
   |                |                | (i.e., the MO  |                |
   |                |                | media has been |                |
   |                |                | removed from   |                |
   |                |                | the archive    |                |
   |                |                | jukebox).      |                |
   |                |                |                |                |
   |                |                | Error message  |                |
   |                |                | is output as   |                |
   |                |                | an alert on    |                |
   |                |                | the User       |                |
   |                |                | Interface, and |                |
   |                |                | to the Service |                |
   |                |                | Log.           |                |
   +----------------+----------------+----------------+----------------+
   | Move           | A801           | The            |                |
   | destination    |                | Destination    |                |
   | unknown        |                | Application    |                |
   |                |                | Entity named   |                |
   |                |                | in the C-MOVE  |                |
   |                |                | Request is     |                |
   |                |                | unknown to     |                |
   |                |                | Query-Retrieve |                |
   |                |                | SCP AE.        |                |
   |                |                |                |                |
   |                |                | Error message  |                |
   |                |                | is output to   |                |
   |                |                | the Service    |                |
   |                |                | Log.           |                |
   +----------------+----------------+----------------+----------------+
   | Failed         | Identifier     | A900           | The C-MOVE     |
   |                | does not match |                | identifier     |
   |                | SOP Class      |                | contains       |
   |                |                |                | invalid        |
   |                |                |                | Elements or    |
   |                |                |                | values, or is  |
   |                |                |                | missing        |
   |                |                |                | mandatory      |
   |                |                |                | Elements or    |
   |                |                |                | values for the |
   |                |                |                | specified SOP  |
   |                |                |                | Class or       |
   |                |                |                | retrieval      |
   |                |                |                | level.         |
   |                |                |                |                |
   |                |                |                | Error message  |
   |                |                |                | is output to   |
   |                |                |                | the Service    |
   |                |                |                | Log.           |
   +----------------+----------------+----------------+----------------+
   | Cancel         | Matching       | FE00           | The C-MOVE SCU |
   |                | terminated due |                | sent a Cancel  |
   |                | to Cancel      |                | Request. This  |
   |                | Request        |                | has been       |
   |                |                |                | acknowledged   |
   |                |                |                | and the export |
   |                |                |                | of Composite   |
   |                |                |                | SOP Instances  |
   |                |                |                | to the C-MOVE  |
   |                |                |                | Destination AE |
   |                |                |                | has been       |
   |                |                |                | halted.        |
   +----------------+----------------+----------------+----------------+
   | Pending        | Sub-operations | FF00           | A Response     |
   |                | are continuing |                | with this      |
   |                |                |                | Status Code is |
   |                |                |                | sent every     |
   |                |                |                | time a         |
   |                |                |                | Composite SOP  |
   |                |                |                | Instance has   |
   |                |                |                | been           |
   |                |                |                | successfully   |
   |                |                |                | sent to the    |
   |                |                |                | C-MOVE         |
   |                |                |                | Destination    |
   |                |                |                | AE.            |
   +----------------+----------------+----------------+----------------+

Note that the Warning Status, B000 (Sub-operations complete - One or
more Failures) is never returned. If a failure occurs during export to
the C-MOVE Destination AE by the STORAGE-SCU AE then the entire task is
aborted. Thus any remaining matches are not exported.

.. table:: QUERY-RETRIEVE-SCP AE Communication Failure Behavior

   +----------------------------------+----------------------------------+
   | Exception                        | Behavior                         |
   +==================================+==================================+
   | Timeout expiry for an expected   | The Association is aborted by    |
   | DICOM Message Request (DIMSE     | issuing a DICOM A-ABORT.         |
   | level timeout). I.e. The         |                                  |
   | QUERY-RETRIEVE-SCP AE is waiting | Error message is output to the   |
   | for the next C-FIND or C-MOVE    | Service Log. If the STORAGE-SCU  |
   | Request on an open Association   | AE is still exporting Composite  |
   | but the timer expires.           | SOP Instances as a result of an  |
   |                                  | earlier C-MOVE Request received  |
   |                                  | on this Association, it will     |
   |                                  | continue attempting to complete  |
   |                                  | the entire C-MOVE Request.       |
   +----------------------------------+----------------------------------+
   | Timeout expiry for an expected   | The Association is aborted by    |
   | DICOM PDU or TCP/IP packet       | issuing a DICOM A-ABORT.         |
   | (Low-level timeout). I.e. The    |                                  |
   | QUERY-RETRIEVE-SCP AE is waiting | Error message is output to the   |
   | for the next message PDU but the | Service Log. If the STORAGE-SCU  |
   | timer expires.                   | AE is still exporting Composite  |
   |                                  | SOP Instances as a result of an  |
   |                                  | earlier C-MOVE Request received  |
   |                                  | on this Association, it will     |
   |                                  | continue attempting to complete  |
   |                                  | the entire C-MOVE Request.       |
   +----------------------------------+----------------------------------+
   | Association aborted by the SCU   | Error message is output to the   |
   | or the network layers indicate   | Service Log. If the STORAGE-SCU  |
   | communication loss (i.e.,        | AE is still exporting Composite  |
   | low-level TCP/IP socket closure) | SOP Instances as a result of an  |
   |                                  | earlier C-MOVE Request received  |
   |                                  | on this Association, it will     |
   |                                  | continue attempting to complete  |
   |                                  | the entire C-MOVE Request.       |
   +----------------------------------+----------------------------------+

.. _sect_F.4.2.3:

STORAGE-SCP Application Entity Specification
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. _sect_F.4.2.3.1:

SOP Classes
'''''''''''

The STORAGE-SCP AE provides Standard Conformance to the following DICOM
SOP Classes:

.. table:: SOP Classes for STORAGE-SCP AE

   ================================== =========================== === ===
   SOP Class Name                     SOP Class UID               SCU SCP
   ================================== =========================== === ===
   Verification                       1.2.840.10008.1.1           Yes Yes
   Storage Commitment Push Model      1.2.840.10008.1.20.1        No  Yes
   US Image Storage (Retired)         1.2.840.10008.5.1.4.1.1.6   No  Yes
   US Image Storage                   1.2.840.10008.5.1.4.1.1.6.1 No  Yes
   US Multi-frame Storage (Retired)   1.2.840.10008.5.1.4.1.1.3   No  Yes
   US Multi-frame Storage             1.2.840.10008.5.1.4.1.1.3.1 No  Yes
   Computed Radiography Image Storage 1.2.840.10008.5.1.4.1.1.1   No  Yes
   CT Image Storage                   1.2.840.10008.5.1.4.1.1.2   No  Yes
   MR Image Storage                   1.2.840.10008.5.1.4.1.1.4   No  Yes
   Secondary Capture Image Storage    1.2.840.10008.5.1.4.1.1.7   No  Yes
   ================================== =========================== === ===

These are the default SOP Classes supported. By altering the
configuration it is possible to support additional or fewer SOP Classes.

.. _sect_F.4.2.3.2:

Association Policies
''''''''''''''''''''

.. _sect_F.4.2.3.2.1:

General
       

The STORAGE-SCP AE can both accept and propose Association Requests. The
STORAGE-SCP AE will accept Association Requests for the Verification,
Storage, and Storage Commitment Push Model Services. It will propose
Associations only for the Storage Commitment Push Model Service.

The DICOM standard Application Context Name for DICOM is always accepted
and proposed:

.. table:: DICOM Application Context for STORAGE-SCP AE

   ======================== =====================
   Application Context Name 1.2.840.10008.3.1.1.1
   ======================== =====================

.. _sect_F.4.2.3.2.2:

Number of Associations
                      

The STORAGE-SCP AE can support multiple simultaneous Associations
requested by peer AEs. Each time the STORAGE-SCP AE receives an
Association, a child process will be spawned to process the
Verification, Storage, or Storage Commitment Push Model Service
requests. The maximum number of child processes, and thus the maximum
number of simultaneous Associations that can be processed, is set by
configuration. The default maximum number is 10 in total. This maximum
number of simultaneous Associations can be either an absolute number or
a maximum number for each requesting external Application Entity. The
latter flexibility can be useful if communication with one external AE
is unreliable and one does not wish 'hung' connections with this AE to
prevent Associations with other client AEs.

The STORAGE-SCP AE initiates one Association at a time for sending
Storage Commitment Push Model N-EVENT-REPORTs to peer AEs.

.. table:: Number of Simultaneous Associations as an SCP for STORAGE-SCP
AE

   +-------------------------------------------------+-------------------+
   | Maximum number of simultaneous Associations     | 10 (Configurable) |
   | requested by peer AEs                           |                   |
   +-------------------------------------------------+-------------------+
   | Maximum number of simultaneous Associations     | 1                 |
   | proposed by STORAGE-SCP AE                      |                   |
   +-------------------------------------------------+-------------------+

.. _sect_F.4.2.3.2.3:

Asynchronous Nature
                   

The STORAGE-SCP AE does not support asynchronous communication (multiple
outstanding transactions over a single Association). The STORAGE-SCP AE
does permit an SCU to send multiple Storage Commitment Push Model
Requests before it has sent back any N-EVENT-REPORT Notifications.
However, the STORAGE-SCP AE must send an N-ACTION Response before
permitting another N-ACTION Request to be received so the DICOM
communication itself is not truly asynchronous.

.. table:: Asynchronous Nature as a SCP for STORAGE-SCP AE

   +----------------------------------------------+----------------------+
   | Maximum number of outstanding asynchronous   | 1 (Not Configurable) |
   | transactions                                 |                      |
   +----------------------------------------------+----------------------+

There is no limit on the number of outstanding Storage Commitment Push
Model Requests that can be received and acknowledged before the
STORAGE-SCP AE has responded with the corresponding N-EVENT-REPORT
Notifications.

.. table:: Outstanding Storage Commitment Push Model Requests for
STORAGE-SCP AE

   +--------------------------------------------------+------------------+
   | Maximum number of outstanding Storage Commitment | No Maximum Limit |
   | Requests for which no N-EVENT Notification has   |                  |
   | been sent                                        |                  |
   +--------------------------------------------------+------------------+

.. _sect_F.4.2.3.2.4:

Implementation Identifying Information
                                      

The implementation information for this Application Entity is:

.. table:: DICOM Implementation Class and Version for STORAGE-SCP AE

   =========================== ======================
   Implementation Class UID    1.840.xxxxxxx.yyy.etc…
   Implementation Version Name EX_VERS_01
   =========================== ======================

Note that the STORAGE-SCP AE specifies a different Implementation Class
UID than that used by the other Application Entities. All
EXAMPLE-QUERY-RETRIEVE-SERVER AEs use the same Implementation Version
Name. This Version Name is updated with each new release of the product
software, as the different AE versions are never released independently.

.. _sect_F.4.2.3.3:

Association Initiation Policy
'''''''''''''''''''''''''''''

.. _sect_F.4.2.3.3.1:

Activity - Send Storage Commitment Notification Over New Association
                                                                    

.. _sect_F.4.2.3.3.1.1:

Description and Sequencing of Activity
                                      

The STORAGE-SCP AE will initiate a new Association if a Storage
Commitment Push Model Notification (N-EVENT-REPORT) cannot be sent back
over the original Association used to send the corresponding request. A
new Association will always be requested by the STORAGE-SCP AE in such
cases even if the peer AE requests another Association after the
original has been closed (i.e., A peer AE opens an Association and sends
some Storage requests and a Storage Commitment Push Model request.
Before the STORAGE-SCP AE can send the Storage Commitment Push Model
N-EVEN-REPORT the Association is closed. The peer AE then opens another
Association and begins to send Storage requests. In such a case the
STORAGE-SCP AE will always initiate a new Association to send the
N-EVENT-REPORT even though it could send the N-EVENT-REPORT over the new
Association opened by the peer AE).

An Association Request is sent to the peer AE that sent the Storage
Commitment Push Model request and upon successful negotiation of the
required Presentation Context the outstanding N-EVENT-REPORT is sent. If
there are multiple outstanding N-EVENT-REPORTs to be sent to a single
peer AE then the STORAGE-SCP AE will attempt to send them all over a
single Association rather than requesting a new Association for each
one. The Association will be released when all the N-EVENT-REPORTs for
the peer AE have been sent. If any type of error occurs during
transmission (either a communication failure or indicated by a Status
Code returned by the peer AE) over an open Association then the transfer
of N-EVENT-REPORTs is halted. A new Association will be opened to retry
sending outstanding N-EVENT-REPORTs. The maximum number of times the
STORAGE-SCP AE will attempt to resend an N-EVENT-REPORT is configurable,
along with the amount of time to wait between attempts to resend.

If the STORAGE-SCP AE sends a Notification request (N-EVENT-REPORT-RQ)
over the original Association opened by the peer AE but receives a
request to close the Association rather than a response to the
Notification (N-EVENT-REPORT-RSP) then this is handled in the same way
as if the request to close the Association had been received before
trying to send the Notification request. Thus, the STORAGE-SCP AE will
then open a new Association to resend the Notification request.

The STORAGE-SCP AE can be configured to always open a new Association
before sending a Storage Commitment Push Model Notifications
(N-EVENT-REPORT), in which case the sequencing illustrated in
`figure_title <#figure_F.4.2-3>`__ will always be followed.

The following sequencing constraints illustrated in
`figure_title <#figure_F.4.2-3>`__ apply to the STORAGE-SCP AE for
handling Storage Commitment Push Model Requests using a new Association:

1. Peer AE opens an Association with the STORAGE-SCP AE.

2. Peer AE requests Storage Commitment of Composite SOP Instance(s)
   (peer sends N-ACTION-RQ and STORAGE-SCP AE responds with N-ACTION-RSP
   to indicate that it received the request).

3. Peer AE closes the Association before the STORAGE-SCP AE can
   successfully send the Storage Commitment Push Model Notification
   (N-EVENT-REPORT-RQ).

4. STORAGE-SCP AE opens an Association with the peer AE.

5. STORAGE-SCP AE sends Storage Commitment Push Model Notification
   (N-EVENT-REPORT). More than one can be sent over a single Association
   if multiple Notifications are outstanding.

6. STORAGE-SCP AE closes the Association with the peer AE.

The Verification Service as an SCU is only supported as a utility
function for Service staff. It is used only as a diagnostic tool when
the STORAGE-SCP AE is failing to open new Associations to send
N-EVENT-REPORTs to peer AEs.

.. _sect_F.4.2.3.3.1.2:

Proposed Presentation Contexts
                              

STORAGE-SCP AE will propose Presentation Contexts as shown in the
following table:

.. table:: Proposed Presentation Contexts By the STORAGE-SCP AE

   +------------+------------+------------+------------+-----+------+
   | Pr         |            |            |            |     |      |
   | esentation |            |            |            |     |      |
   | Context    |            |            |            |     |      |
   | Table      |            |            |            |     |      |
   +============+============+============+============+=====+======+
   | Ve         | 1.2.840    | DICOM      | 1.2.840    | SCU | None |
   | rification | .10008.1.1 | Implicit   | .10008.1.2 |     |      |
   |            |            | VR Little  |            |     |      |
   |            |            | Endian     |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | Storage    | 1.2.840.10 | DICOM      | 1.2.840    | SCP | None |
   | Commitment | 008.1.20.1 | Implicit   | .10008.1.2 |     |      |
   | Push Model |            | VR Little  |            |     |      |
   |            |            | Endian     |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | Storage    | 1.2.840.10 | DICOM      | 1.2.840.1  | SCP | None |
   | Commitment | 008.1.20.1 | Explicit   | 0008.1.2.1 |     |      |
   | Push Model |            | VR Little  |            |     |      |
   |            |            | Endian     |            |     |      |
   +------------+------------+------------+------------+-----+------+

.. _sect_F.4.2.3.3.1.3:

SOP Specific Conformance for Storage SOP Classes
                                                

The associated Activity with the Storage Commitment Push Model service
is the communication by the STORAGE-SCP AE to peer AEs that it has
committed to permanently store Composite SOP Instances that have been
sent to it. It thus allows peer AEs to determine whether the
EXAMPLE-QUERY-RETRIEVE-SERVER has taken responsibility for the archiving
of specific SOP Instances so that they can be flushed from the peer AE
system.

The STORAGE-SCP AE will initiate a new Association to a peer AE that
sent a Storage Commitment Push Model request if the original Association
over which this was sent is no longer open. For a detailed explanation
of the SOP specific Behavior of the STORAGE-SCP AE in this case please
refer to 4.2.4.4.1.3.3, Storage Commitment Push Model as an SCP.

.. _sect_F.4.2.3.3.1.4:

SOP Specific Conformance for Verification SOP Class
                                                   

Standard conformance is provided to the DICOM Verification Service Class
as an SCU. The Verification Service as an SCU is actually only supported
as a diagnostic service tool for network communication issues. It can be
used to test whether Associations can actually be opened with a peer AE
that is issuing Storage Commitment Push Model requests (i.e., to test
whether the indicated TCP/IP port and AE Title for sending
N-EVENT-REPORT Requests to the peer AE are truly functional).

.. _sect_F.4.2.3.4:

Association Acceptance Policy
'''''''''''''''''''''''''''''

.. _sect_F.4.2.3.4.1:

Activity - Receive Images and Storage Commitment Requests
                                                         

.. _sect_F.4.2.3.4.1.1:

Description and Sequencing of Activity
                                      

The STORAGE-SCP AE accepts Associations only if they have valid
Presentation Contexts. If none of the requested Presentation Contexts
are accepted then the Association Request itself is rejected. It can be
configured to only accept Associations with certain hosts (using TCP/IP
address) and/or Application Entity Titles.

The default behavior of the STORAGE-SCP AE is to always attempt to send
a Storage Commitment Push Model Notification (N-EVENT-REPORT) over the
same Association opened by the peer AE to send the request (N-ACTION).
If the STORAGE-SCP AE receives a request to close the Association either
before sending the Notification or before receiving the corresponding
N-EVENT-REPORT-RSP then it will open a new Association to send the
Notification. Refer to `SOP Specific Conformance for Storage Commitment
SOP Class <#sect_F.4.2.3.4.1.5>`__ for the details.

The following sequencing constraints illustrated in
`figure_title <#figure_F.4.2-4>`__ apply to the STORAGE-SCP AE for
handling Storage Commitment Push Model Requests over the original
Association:

1. Peer AE opens an Association with the STORAGE-SCP AE.

2. Peer AE sends zero or more Composite SOP Instances.

3. Peer AE requests Storage Commitment of Composite SOP Instance(s)
   (peer sends N-ACTION-RQ and STORAGE-SCP AE responds with N-ACTION-RSP
   to indicate that it received the request).

4. STORAGE-SCP AE sends Storage Commitment Push Model Notification
   request (N-EVENT-REPORT-RQ) and successfully receives Notification
   response (N-EVENT-REPORT-RSP) from peer AE.

5. Peer AE closes the Association.

If the STORAGE-SCP AE receives a request to close the Association from
the peer AE before sending the Notification request (N-EVENT-REPORT-RQ)
or when expecting to receive a Notification response
(N-EVENT-REPORT-RSP) then it will open a new Association to send (or
resend) the Notification. Refer to 0 for the details. The STORAGE-SCP AE
has a configurable timeout value for the maximum amount of time that it
will wait on an open Association for a new request from a peer AE. A
peer AE can reset this timer by sending a Verification request
(C-ECHO-RQ). This can act as a useful mechanism for a peer AE to
maintain an active Association if the length of time between sending
Storage or Storage Commitment requests can be long (such as when using a
single Association to send images as they are acquired during an
ultrasound exam).

The STORAGE-SCP AE may reject Association attempts as shown in the Table
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

.. _sect_F.4.2.3.4.1.2:

Accepted Presentation Contexts
                              

The default Behavior of the STORAGE-SCP AE supports the Implicit VR
Little Endian and Explicit VR Little Endian Transfer Syntaxes for all
Associations. In addition, explicit JPEG (baseline lossy) compression
syntax is supported for the following SOP Classes: US Image, US
Multi-frame Image, US Image (retired), US Multi-frame Image (retired),
VL Image, VL Multi-frame and Secondary Capture Image Storage.

The STORAGE-SCP AE can be configured to accept a subset of these
Transfer Syntaxes, with the inclusion of Implicit VR Little Endian being
mandatory.

If multiple Transfer Syntaxes are proposed per Presentation Context then
only the most preferable Transfer Syntax is accepted. The order of
Transfer Syntax preference for the STORAGE-SCP AE is configurable. The
default preference order if multiple Transfer Syntaxes are proposed in a
single Presentation Context is: JPEG Baseline1, Little Endian Explicit,
Little Endian Implicit (if all these are proposed for a single
Presentation Context). This means that if the Implicit VR Little Endian
and Explicit VR Little Endian Transfer Syntaxes are proposed in a single
Presentation Context then the accepted Transfer Syntax will be Explicit
VR Little Endian. This order of preference is configurable.

Any of the Presentation Contexts shown in the following table are
acceptable to the STORAGE-SCP AE for receiving images.

.. table:: Accepted Presentation Contexts By STORAGE-SCP AE

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
   | Storage    | 1.2.840.10 | DICOM      | 1.2.840    | SCP | None |
   | Commitment | 008.1.20.1 | Implicit   | .10008.1.2 |     |      |
   | Push Model |            | VR Little  |            |     |      |
   |            |            | Endian     |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | Storage    | 1.2.840.10 | DICOM      | 1.2.840.1  | SCP | None |
   | Commitment | 008.1.20.1 | Explicit   | 0008.1.2.1 |     |      |
   | Push Model |            | VR Little  |            |     |      |
   |            |            | Endian     |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | US Image   | 1.2.8      | DICOM      | 1.2.840    | SCP | None |
   | Storage    | 40.10008.5 | Implicit   | .10008.1.2 |     |      |
   |            | .1.4.1.1.6 | VR Little  |            |     |      |
   | (Retired)  |            | Endian     |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | US Image   | 1.2.8      | DICOM      | 1.2.840.1  | SCP | None |
   | Storage    | 40.10008.5 | Explicit   | 0008.1.2.1 |     |      |
   |            | .1.4.1.1.6 | VR Little  |            |     |      |
   | (Retired)  |            | Endian     |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | US Image   | 1.2.8      | DICOM      | 1.         | SCP | None |
   | Storage    | 40.10008.5 | Explicit   | 2.840.1000 |     |      |
   |            | .1.4.1.1.6 | JPEG       | 8.1.2.4.50 |     |      |
   | (Retired)  |            | baseline   |            |     |      |
   |            |            | lossy      |            |     |      |
   |            |            | c          |            |     |      |
   |            |            | ompression |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | US Image   | 1.2.840    | DICOM      | 1.2.840    | SCP | None |
   | Storage    | .10008.5.1 | Implicit   | .10008.1.2 |     |      |
   |            | .4.1.1.6.1 | VR Little  |            |     |      |
   |            |            | Endian     |            |     |      |
   |            |            | (unc       |            |     |      |
   |            |            | ompressed) |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | US Image   | 1.2.840    | DICOM      | 1.2.840.1  | SCP | None |
   | Storage    | .10008.5.1 | Explicit   | 0008.1.2.1 |     |      |
   |            | .4.1.1.6.1 | VR Little  |            |     |      |
   |            |            | Endian     |            |     |      |
   |            |            | (unc       |            |     |      |
   |            |            | ompressed) |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | US Image   | 1.2.840    | DICOM      | 1.         | SCP | None |
   | Storage    | .10008.5.1 | Explicit   | 2.840.1000 |     |      |
   |            | .4.1.1.6.1 | JPEG       | 8.1.2.4.50 |     |      |
   |            |            | baseline   |            |     |      |
   |            |            | lossy      |            |     |      |
   |            |            | c          |            |     |      |
   |            |            | ompression |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | US         | 1.2.8      | DICOM      | 1.2.840    | SCP | None |
   | M          | 40.10008.5 | Implicit   | .10008.1.2 |     |      |
   | ulti-frame | .1.4.1.1.3 | VR Little  |            |     |      |
   | Storage    |            | Endian     |            |     |      |
   | (Retired)  |            |            |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | US         | 1.2.8      | DICOM      | 1.2.840.1  | SCP | None |
   | M          | 40.10008.5 | Explicit   | 0008.1.2.1 |     |      |
   | ulti-frame | .1.4.1.1.3 | VR Little  |            |     |      |
   | Storage    |            | Endian     |            |     |      |
   | (Retired)  |            |            |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | US         | 1.2.8      | DICOM      | 1.         | SCP | None |
   | M          | 40.10008.5 | Explicit   | 2.840.1000 |     |      |
   | ulti-frame | .1.4.1.1.3 | JPEG       | 8.1.2.4.50 |     |      |
   | Storage    |            | baseline   |            |     |      |
   | (Retired)  |            | lossy      |            |     |      |
   |            |            | c          |            |     |      |
   |            |            | ompression |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | US         | 1.2.840    | DICOM      | 1.2.840    | SCP | None |
   | M          | .10008.5.1 | Implicit   | .10008.1.2 |     |      |
   | ulti-frame | .4.1.1.3.1 | VR Little  |            |     |      |
   | Storage    |            | Endian     |            |     |      |
   |            |            | (unc       |            |     |      |
   |            |            | ompressed) |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | US         | 1.2.840    | DICOM      | 1.2.840.1  | SCP | None |
   | M          | .10008.5.1 | Explicit   | 0008.1.2.1 |     |      |
   | ulti-frame | .4.1.1.3.1 | VR Little  |            |     |      |
   | Storage    |            | Endian     |            |     |      |
   |            |            | (unc       |            |     |      |
   |            |            | ompressed) |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | US         | 1.2.840    | DICOM      | 1.         | SCP | None |
   | M          | .10008.5.1 | Explicit   | 2.840.1000 |     |      |
   | ulti-frame | .4.1.1.3.1 | JPEG       | 8.1.2.4.50 |     |      |
   | Storage    |            | baseline   |            |     |      |
   |            |            | lossy      |            |     |      |
   |            |            | c          |            |     |      |
   |            |            | ompression |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | Computer   | 1.2.8      | DICOM      | 1.2.840    | SCP | None |
   | R          | 40.10008.5 | Implicit   | .10008.1.2 |     |      |
   | adiography | .1.4.1.1.1 | VR Little  |            |     |      |
   | Image      |            | Endian     |            |     |      |
   | Storage    |            |            |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | Computer   | 1.2.8      | DICOM      | 1.2.840.1  | SCP | None |
   | R          | 40.10008.5 | Explicit   | 0008.1.2.1 |     |      |
   | adiography | .1.4.1.1.1 | VR Little  |            |     |      |
   | Image      |            | Endian     |            |     |      |
   | Storage    |            |            |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | CT Image   | 1.2.8      | DICOM      | 1.2.840    | SCP | None |
   | Storage    | 40.10008.5 | Implicit   | .10008.1.2 |     |      |
   |            | .1.4.1.1.2 | VR Little  |            |     |      |
   |            |            | Endian     |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | CT Image   | 1.2.8      | DICOM      | 1.2.840.1  | SCP | None |
   | Storage    | 40.10008.5 | Explicit   | 0008.1.2.1 |     |      |
   |            | .1.4.1.1.2 | VR Little  |            |     |      |
   |            |            | Endian     |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | MR Image   | 1.2.8      | DICOM      | 1.2.840    | SCP | None |
   | Storage    | 40.10008.5 | Implicit   | .10008.1.2 |     |      |
   |            | .1.4.1.1.4 | VR Little  |            |     |      |
   |            |            | Endian     |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | MR Image   | 1.2.8      | DICOM      | 1.2.840.1  | SCP | None |
   | Storage    | 40.10008.5 | Explicit   | 0008.1.2.1 |     |      |
   |            | .1.4.1.1.4 | VR Little  |            |     |      |
   |            |            | Endian     |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | NM Image   | 1.2.8      | DICOM      | 1.2.840    | SCP | None |
   | Storage    | 40.10008.5 | Implicit   | .10008.1.2 |     |      |
   | (Retired)  | .1.4.1.1.5 | VR Little  |            |     |      |
   |            |            | Endian     |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | Secondary  | 1.2.8      | DICOM      | 1.2.840    | SCP | None |
   | Capture    | 40.10008.5 | Implicit   | .10008.1.2 |     |      |
   | Image      | .1.4.1.1.7 | VR Little  |            |     |      |
   | Storage    |            | Endian     |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | Secondary  | 1.2.8      | DICOM      | 1.2.840.1  | SCP | None |
   | Capture    | 40.10008.5 | Explicit   | 0008.1.2.1 |     |      |
   | Image      | .1.4.1.1.7 | VR Little  |            |     |      |
   | Storage    |            | Endian     |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | Secondary  | 1.2.8      | DICOM      | 1.         | SCP | None |
   | Capture    | 40.10008.5 | Explicit   | 2.840.1000 |     |      |
   | Image      | .1.4.1.1.7 | JPEG lossy | 8.1.2.4.50 |     |      |
   | Storage    |            | c          |            |     |      |
   |            |            | ompression |            |     |      |
   +------------+------------+------------+------------+-----+------+

.. _sect_F.4.2.3.4.1.3:

SOP Specific Conformance for Verification SOP Class
                                                   

The STORAGE-SCP AE provides standard conformance to the Verification SOP
Class as an SCP.

.. _sect_F.4.2.3.4.1.4:

SOP Specific Conformance for Storage SOP Classes
                                                

The associated Activity with the Storage service is the storage of
medical image data received over the network on a designated hard disk.
The STORAGE-SCP AE will return a failure status if it is unable to store
the images on to the hard disk.

The STORAGE-SCP AE does not have any dependencies on the number of
Associations used to send images to it. Images belonging to more than
one Study or Series can be sent over a single or multiple Associations.
Images belonging to a single Study or Series can also be sent over
different Associations. There is no limit on either the number of SOP
Instances or the maximum amount of total SOP Instance data that can be
transferred over a single Association.

The STORAGE-SCP AE is configured to retain the original DICOM data in
DICOM Part 10 compliant file format. The STORAGE-SCP AE is Level 2
(Full) conformant as a Storage SCP. In addition, all Private and SOP
Class Extended Elements are maintained in the DICOM format files. In
addition to saving all Elements in files, a subset of the Elements are
stored in the EXAMPLE-QUERY-RETRIEVE-SERVER database to support query
and retrieval requests and also allow updating of Patient, Study, and
Series information by user input, or demographic and Study related
messages. Refer to the Annex for the list of Elements that are checked
and/or processed upon receiving a Composite SOP Instance.

The Behavior for handling duplicate SOP Instances is configurable. The
default Behavior is to assign a new SOP Instance UID to a received SOP
Instance if it conflicts with an existing SOP Instance UID. An
alternative configuration is possible that causes the original object
with the conflicting SOP Instance UID to be replaced by the new SOP
Instance. This Behavior is most commonly enabled if a Storage SCU
re-sends entire Studies or Series if a single failure occurs when
sending a group of SOP Instances.

For the purposes of image display the system supports the following
photometric interpretations: MONOCHROME1, MONOCHROME2, RGB, PALETTE
COLOR, YBR FULL 422, and YBR FULL.

It is expected that optimal Window Center and Width values are specified
in the DICOM Image Objects if they have greater than 8 bits of image
data stored per sample. If optimal Window Center and Width values are
not provided, then the EXAMPLE-QUERY-RETRIEVE-SERVER is capable of
estimating values using histogram analysis.

For multi-frame image SOP Instances sent using JPEG compression Transfer
Syntax, sending a fully specified offset table increases performance,
because the entire file does not have to be parsed to find the
individual frame offsets. However, the inclusion of an offset table is
not required for archiving or viewing of such SOP Instances.

Display of information conveyed using the DICOM Curve Module is not
supported. Graphic overlay data sent either embedded in the unused image
pixel data bits or in the separate Overlay Data Element is supported for
display. Region of Interest overlays are not yet supported.

If an image SOP Instance specifies an aspect ratio that is not
one-to-one then the image data will be automatically resized when
displayed on the system monitor so that they are always displayed in a
one-to-one aspect ratio.

The average throughput performance has been determined to be between 2
and 6 Mega Bytes per second on a 100 Megabit Ethernet network. Actual
performance will depend greatly on the performance of the C-STORE SCU,
the number of simultaneous active Associations, and the underlying
network performance.

.. table:: STORAGE-SCP AE C-STORE Response Status Return Reasons

   +----------------+----------------+----------------+----------------+
   | Service Status | Further        | Error Code     | Reason         |
   |                | Meaning        |                |                |
   +================+================+================+================+
   | Success        | Success        | 0000           | The Composite  |
   |                |                |                | SOP Instance   |
   |                |                |                | was            |
   |                |                |                | successfully   |
   |                |                |                | received,      |
   |                |                |                | verified, and  |
   |                |                |                | stored in the  |
   |                |                |                | system         |
   |                |                |                | database.      |
   +----------------+----------------+----------------+----------------+
   | Refused        | Out of         | A700           | Indicates that |
   |                | Resources      |                | there was not  |
   |                |                |                | enough disk    |
   |                |                |                | space to store |
   |                |                |                | the image.     |
   |                |                |                |                |
   |                |                |                | Error message  |
   |                |                |                | is output to   |
   |                |                |                | the Service    |
   |                |                |                | Log. The SOP   |
   |                |                |                | Instance will  |
   |                |                |                | not be saved.  |
   +----------------+----------------+----------------+----------------+
   | Error          | Data Set does  | A900           | Indicates that |
   |                | not match SOP  |                | the Data Set   |
   |                | Class          |                | does not       |
   |                |                |                | encode a valid |
   |                |                |                | instance of    |
   |                |                |                | the SOP Class  |
   |                |                |                | specified.     |
   |                |                |                | This status is |
   |                |                |                | returned if    |
   |                |                |                | the DICOM      |
   |                |                |                | Object stream  |
   |                |                |                | can be         |
   |                |                |                | successfully   |
   |                |                |                | parsed but     |
   |                |                |                | does not       |
   |                |                |                | contain values |
   |                |                |                | for one or     |
   |                |                |                | more mandatory |
   |                |                |                | Elements of    |
   |                |                |                | the SOP Class. |
   |                |                |                | The            |
   |                |                |                | STORAGE-SCP AE |
   |                |                |                | does not       |
   |                |                |                | perform a      |
   |                |                |                | comprehensive  |
   |                |                |                | check, as it   |
   |                |                |                | only checks a  |
   |                |                |                | subset of      |
   |                |                |                | required       |
   |                |                |                | Elements. In   |
   |                |                |                | addition, if   |
   |                |                |                | the SOP Class  |
   |                |                |                | is for a type  |
   |                |                |                | of image but   |
   |                |                |                | the SOP        |
   |                |                |                | Instance does  |
   |                |                |                | not contain    |
   |                |                |                | values         |
   |                |                |                | necessary for  |
   |                |                |                | its display    |
   |                |                |                | then this      |
   |                |                |                | status is      |
   |                |                |                | returned.      |
   |                |                |                |                |
   |                |                |                | Error message  |
   |                |                |                | is output to   |
   |                |                |                | the Service    |
   |                |                |                | Log. The       |
   |                |                |                | system can be  |
   |                |                |                | configured to  |
   |                |                |                | temporarily    |
   |                |                |                | save such Data |
   |                |                |                | Sets in order  |
   |                |                |                | to aid problem |
   |                |                |                | diagnosis.     |
   +----------------+----------------+----------------+----------------+
   | Cannot         | C000           | Indicates that |                |
   | understand     |                | the            |                |
   |                |                | STORAGE-SCP AE |                |
   |                |                | cannot parse   |                |
   |                |                | the Data Set   |                |
   |                |                | into Elements. |                |
   |                |                |                |                |
   |                |                | Error message  |                |
   |                |                | is output to   |                |
   |                |                | the Service    |                |
   |                |                | Log. The       |                |
   |                |                | system can be  |                |
   |                |                | configured to  |                |
   |                |                | temporarily    |                |
   |                |                | save such Data |                |
   |                |                | Sets in order  |                |
   |                |                | to aid problem |                |
   |                |                | diagnosis.     |                |
   +----------------+----------------+----------------+----------------+
   | Warning        | Coercion of    | B000           | Indicates that |
   |                | Data Elements  |                | one or more    |
   |                |                |                | Element values |
   |                |                |                | were coerced.  |
   |                |                |                | Refer to the   |
   |                |                |                | Attributes     |
   |                |                |                | defined in     |
   |                |                |                | Annex for a    |
   |                |                |                | list of those  |
   |                |                |                | that can be    |
   |                |                |                | coerced. Note  |
   |                |                |                | that return of |
   |                |                |                | this status is |
   |                |                |                | disabled by    |
   |                |                |                | default, as    |
   |                |                |                | some SCUs      |
   |                |                |                | treat it as an |
   |                |                |                | Error code     |
   |                |                |                | rather than a  |
   |                |                |                | Warning.       |
   +----------------+----------------+----------------+----------------+

.. note::

   If a failure condition does occur when handling an Association then
   all images previously received successfully over the Association are
   maintained in the EXAMPLE-QUERY-RETRIEVE-SERVER database. No
   previously successfully received images are discarded. Even if an
   image is successfully received but an error occurs transmitting the
   C-STORE Response then this final image is maintained rather than
   discarded. If the loss of an Association is detected then the
   Association is closed.

The Behavior of STORAGE-SCP AE during communication failure is
summarized in the following table:

.. table:: STORAGE-SCP AE Storage Service Communication Failure Reasons

   +----------------------------------+----------------------------------+
   | Exception                        | Reason                           |
   +==================================+==================================+
   | Timeout expiry for an expected   | The Association is aborted by    |
   | DICOM Message Request (DIMSE     | issuing a DICOM A-ABORT.         |
   | level timeout). I.e. The         |                                  |
   | STORAGE-SCP AE is waiting for    | Error message is output to the   |
   | the next C-STORE Request on an   | Service Log. If some Composite   |
   | open Association but the timer   | SOP Instances have already been  |
   | expires.                         | successfully received then they  |
   |                                  | are maintained in the database.  |
   |                                  | They are not automatically       |
   |                                  | discarded because of a later     |
   |                                  | failure.                         |
   +----------------------------------+----------------------------------+
   | Timeout expiry for an expected   | The Association is aborted by    |
   | DICOM PDU or TCP/IP packet       | issuing a DICOM A-ABORT.         |
   | (Low-level timeout). I.e. The    |                                  |
   | STORAGE-SCP AE is waiting for    | Error message is output to the   |
   | the next C-STORE Data Set PDU    | Service Log. If a C-STORE Data   |
   | but the timer expires.           | Set has not been fully received  |
   |                                  | then the data already received   |
   |                                  | is discarded. If some Composite  |
   |                                  | SOP Instances have already been  |
   |                                  | successfully received over the   |
   |                                  | Association then they are        |
   |                                  | maintained in the database.      |
   +----------------------------------+----------------------------------+
   | Association aborted by the SCU   | Error message is output to the   |
   | or the network layers indicate   | Service Log. If some Composite   |
   | communication loss (i.e.,        | SOP Instances have already been  |
   | low-level TCP/IP socket closure) | successfully received then they  |
   |                                  | are maintained in the database.  |
   |                                  | They are not automatically       |
   |                                  | discarded because of a later     |
   |                                  | failure.                         |
   +----------------------------------+----------------------------------+

.. _sect_F.4.2.3.4.1.5:

SOP Specific Conformance for Storage Commitment SOP Class
                                                         

The associated Activity with the Storage Commitment Push Model service
is the communication by the STORAGE-SCP AE to peer AEs that it has
committed to permanently store Composite SOP Instances that have been
sent to it. It thus allows peer AEs to determine whether the
EXAMPLE-QUERY-RETRIEVE-SERVER has taken responsibility for the archiving
of specific SOP Instances so that they can be flushed from the peer AE
system.

The STORAGE-SCP AE takes the list of Composite SOP Instance UIDs
specified in a Storage Commitment Push Model N-ACTION Request and checks
if they are present in the EXAMPLE-QUERY-RETRIEVE-SERVER database. As
long as the Composite SOP Instance UIDs are present in the database, the
STORAGE-SCP AE will consider those Composite SOP Instance UIDs to be
successfully archived. The STORAGE-SCP AE does not require the Composite
SOP Instances to actually be successfully written to archive media in
order to commit to responsibility for maintaining these SOP Instances.

Once the STORAGE-SCP AE has checked for the existence of the specified
Composite SOP Instances, it will then attempt to send the Notification
request (N-EVENT-REPORT-RQ). The default behavior is to attempt to send
this Notification over the same Association that was used by the peer AE
to send the original N-ACTION Request. If the Association has already
been released or Message transfer fails for some reason then the
STORAGE-SCP AE will attempt to send the N-EVENT-REPORT-RQ over a new
Association. The STORAGE-SCP AE will request a new Association with the
peer AE that made the original N-ACTION Request. The STORAGE-SCP AE can
be configured to always open a new Association in order to send the
Notification request.

The STORAGE-SCP AE will not cache Storage Commitment Push Model N-ACTION
Requests that specify Composite SOP Instances that have not yet been
transferred to the EXAMPLE-QUERY-RETRIEVE-SERVER. If a peer AE sends a
Storage Commitment Push Model N-ACTION Request before the specified
Composite SOP Instances are later sent over the same Association, the
STORAGE-SCP AE will not commit to responsibility for such SOP Instances.

The STORAGE-SCP AE does not support the optional Storage Media File-Set
ID & UID attributes in the N-ACTION.

The EXAMPLE-QUERY-RETRIEVE-SERVER never automatically deletes Composite
SOP Instances from the archive. The absolute persistence of SOP
Instances and the maximum archiving capacity for such SOP Instances is
dependent on the archiving media and capacity used by the
EXAMPLE-QUERY-RETRIEVE-SERVER and is dependent on the actual
specifications of the purchased system. It is necessary to check the
actual system specifications to determine these characteristics.

The STORAGE-SCP AE will support Storage Commitment Push Model requests
for SOP Instances of any of the Storage SOP Classes that are also
supported by the STORAGE-SCP AE:

.. table:: Supported Referenced SOP Classes in Storage Commitment Push
Model N-ACTION Requests

   +------------------------------------+
   | Supported Referenced SOP Classes   |
   +====================================+
   | US Image Storage (Retired)         |
   +------------------------------------+
   | US Image Storage                   |
   +------------------------------------+
   | US Multi-frame Storage (Retired)   |
   +------------------------------------+
   | US Multi-frame Storage             |
   +------------------------------------+
   | Computed Radiography Image Storage |
   +------------------------------------+
   | CT Image Storage                   |
   +------------------------------------+
   | MR Image Storage                   |
   +------------------------------------+
   | Secondary Capture Image Storage    |
   +------------------------------------+

The STORAGE-SCP AE will return the following Status Code values in
N-ACTION Responses:

.. table:: STORAGE-SCP AE Storage Commitment Push Model N-ACTION
Response Status Return Behavior

   +----------------+-----------------+------------+-----------------+
   | Service Status | Further Meaning | Error Code | Behavior        |
   +================+=================+============+=================+
   | Success        | Success         | 0000       | The SCP has     |
   |                |                 |            | successfully    |
   |                |                 |            | received the    |
   |                |                 |            | Storage         |
   |                |                 |            | Commitment Push |
   |                |                 |            | Model N-ACTION  |
   |                |                 |            | Request and can |
   |                |                 |            | process the     |
   |                |                 |            | commitment      |
   |                |                 |            | request for the |
   |                |                 |            | indicated SOP   |
   |                |                 |            | Instances.      |
   +----------------+-----------------+------------+-----------------+
   | Error          | Processing      | 0110       | Indicates that  |
   |                | Failure         |            | the Storage     |
   |                |                 |            | Commitment Push |
   |                |                 |            | Model N-ACTION  |
   |                |                 |            | Request cannot  |
   |                |                 |            | be parsed or    |
   |                |                 |            | fully processed |
   |                |                 |            | due to a        |
   |                |                 |            | database or     |
   |                |                 |            | system failure. |
   +----------------+-----------------+------------+-----------------+
   | Error          | Missing         | 0120       | Indicates that  |
   |                | Attribute       |            | the Storage     |
   |                |                 |            | Commitment Push |
   |                |                 |            | Model N-ACTION  |
   |                |                 |            | Request cannot  |
   |                |                 |            | be processed    |
   |                |                 |            | because a       |
   |                |                 |            | required        |
   |                |                 |            | attribute is    |
   |                |                 |            | missing from    |
   |                |                 |            | the N-ACTION    |
   |                |                 |            | Request Data    |
   |                |                 |            | Set.            |
   +----------------+-----------------+------------+-----------------+
   | Error          | Missing         | 0121       | Indicates that  |
   |                | Attribute Value |            | the Storage     |
   |                |                 |            | Commitment Push |
   |                |                 |            | Model N-ACTION  |
   |                |                 |            | Request cannot  |
   |                |                 |            | be processed    |
   |                |                 |            | because a Type  |
   |                |                 |            | 1 attribute in  |
   |                |                 |            | the N-ACTION    |
   |                |                 |            | Request Data    |
   |                |                 |            | Set does not    |
   |                |                 |            | specify a       |
   |                |                 |            | value.          |
   +----------------+-----------------+------------+-----------------+

The STORAGE-SCP AE will exhibit the following Behavior according to the
Status Code value returned in an N-EVENT-REPORT Response from a
destination Storage Commitment Push Model SCU:

.. table:: STORAGE-SCP AE N-EVENT-REPORT Response Status Handling
Behavior

   +----------------+----------------+----------------+----------------+
   | Service Status | Further        | Error Code     | Behavior       |
   |                | Meaning        |                |                |
   +================+================+================+================+
   | Success        | Success        | 0000           | The SCU has    |
   |                |                |                | successfully   |
   |                |                |                | received the   |
   |                |                |                | Storage        |
   |                |                |                | Commitment     |
   |                |                |                | Push Model     |
   |                |                |                | N-EVENT-REPORT |
   |                |                |                | Request.       |
   |                |                |                |                |
   |                |                |                | Success        |
   |                |                |                | indication     |
   |                |                |                | message is     |
   |                |                |                | output to the  |
   |                |                |                | Service Logs.  |
   |                |                |                |                |
   |                |                |                | No message is  |
   |                |                |                | posted to the  |
   |                |                |                | User           |
   |                |                |                | Interface.     |
   +----------------+----------------+----------------+----------------+
   | Warning        | Attribute List | 0107           | Transmission   |
   |                | Error          |                | of Storage     |
   |                |                |                | Commitment     |
   |                |                |                | Push Model     |
   |                |                |                | N-EVENT-REPORT |
   |                |                |                | Request is     |
   |                |                |                | considered     |
   |                |                |                | successful.    |
   |                |                |                |                |
   |                |                |                | Warning        |
   |                |                |                | indication     |
   |                |                |                | message is     |
   |                |                |                | output to the  |
   |                |                |                | Service Logs.  |
   |                |                |                |                |
   |                |                |                | No message is  |
   |                |                |                | posted to the  |
   |                |                |                | User           |
   |                |                |                | Interface.     |
   +----------------+----------------+----------------+----------------+
   | \*             | \*             | Any other      | This is        |
   |                |                | status code.   | treated as a   |
   |                |                |                | permanent      |
   |                |                |                | Failure.       |
   |                |                |                |                |
   |                |                |                | Error          |
   |                |                |                | indication     |
   |                |                |                | message is     |
   |                |                |                | output to the  |
   |                |                |                | Service Logs.  |
   |                |                |                |                |
   |                |                |                | No message is  |
   |                |                |                | posted to the  |
   |                |                |                | User           |
   |                |                |                | Interface.     |
   +----------------+----------------+----------------+----------------+

All Status Codes indicating an error or refusal are treated as a
permanent failure. The STORAGE-SCP AE can be configured to automatically
reattempt the sending of Storage Commitment Push Model N-EVENT-REPORT
Requests if an error Status Code is returned or a communication failure
occurs. The maximum number of times to attempt sending as well as the
time to wait between attempts is configurable.

.. table:: STORAGE-SCP AE Storage Commitment Push Model Communication
Failure Behavior

   +----------------------------------+----------------------------------+
   | Exception                        | Behavior                         |
   +==================================+==================================+
   | Timeout expiry for an expected   | The Association is aborted by    |
   | DICOM Message Request (DIMSE     | issuing a DICOM A-ABORT.         |
   | level timeout). I.e. The         |                                  |
   | STORAGE-SCP AE is waiting for    | If some Composite SOP Instances  |
   | the next N-ACTION Request on an  | have been successfully received  |
   | open Association but the timer   | over the same Association via    |
   | expires.                         | the Storage Service then they    |
   |                                  | are maintained in the database.  |
   |                                  | They are not automatically       |
   |                                  | discarded because of a later     |
   |                                  | Storage Commitment messaging     |
   |                                  | failure.                         |
   |                                  |                                  |
   |                                  | Any previously received Storage  |
   |                                  | Commitment Push Model N-ACTION   |
   |                                  | Requests will still be fully     |
   |                                  | processed.                       |
   |                                  |                                  |
   |                                  | Error indication message is      |
   |                                  | output to the Service Logs.      |
   |                                  |                                  |
   |                                  | No message is posted to the User |
   |                                  | Interface.                       |
   +----------------------------------+----------------------------------+
   | Timeout expiry for an expected   | The Association is aborted by    |
   | DICOM Message Response (DIMSE    | issuing a DICOM A-ABORT.         |
   | level timeout). I.e. The         |                                  |
   | STORAGE-SCP AE is waiting for    | If some Composite SOP Instances  |
   | the next N-EVENT-REPORT Response | have been successfully received  |
   | on an open Association but the   | over the same Association via    |
   | timer expires.                   | the Storage Service then they    |
   |                                  | are maintained in the database.  |
   |                                  | They are not automatically       |
   |                                  | discarded because of a later     |
   |                                  | Storage Commitment messaging     |
   |                                  | failure.                         |
   |                                  |                                  |
   |                                  | Any previously received Storage  |
   |                                  | Commitment Push Model N-ACTION   |
   |                                  | Requests will still be fully     |
   |                                  | processed.                       |
   |                                  |                                  |
   |                                  | Error indication message is      |
   |                                  | output to the Service Logs.      |
   |                                  |                                  |
   |                                  | No message is posted to the User |
   |                                  | Interface.                       |
   +----------------------------------+----------------------------------+
   | Timeout expiry for an expected   | The Association is aborted by    |
   | DICOM PDU or TCP/IP packet       | issuing a DICOM A-ABORT.         |
   | (Low-level timeout).             |                                  |
   |                                  | If some Composite SOP Instances  |
   |                                  | have been successfully received  |
   |                                  | over the same Association via    |
   |                                  | the Storage Service then they    |
   |                                  | are maintained in the database.  |
   |                                  | They are not automatically       |
   |                                  | discarded because of a later     |
   |                                  | Storage Commitment messaging     |
   |                                  | failure.                         |
   |                                  |                                  |
   |                                  | Any previously received Storage  |
   |                                  | Commitment Push Model N-ACTION   |
   |                                  | Requests will still be fully     |
   |                                  | processed.                       |
   |                                  |                                  |
   |                                  | Error indication message is      |
   |                                  | output to the Service Logs.      |
   |                                  |                                  |
   |                                  | No message is posted to the User |
   |                                  | Interface.                       |
   +----------------------------------+----------------------------------+
   | Association A-ABORTed by the SCU | The TCP/IP socket is closed.     |
   | or the network layers indicate   |                                  |
   | communication loss (i.e.,        | If some Composite SOP Instances  |
   | low-level TCP/IP socket closure) | have been successfully received  |
   |                                  | over the same Association via    |
   |                                  | the Storage Service then they    |
   |                                  | are maintained in the database.  |
   |                                  | They are not automatically       |
   |                                  | discarded because of a later     |
   |                                  | Storage Commitment messaging     |
   |                                  | failure.                         |
   |                                  |                                  |
   |                                  | Any previously received Storage  |
   |                                  | Commitment Push Model N-ACTION   |
   |                                  | Requests will still be fully     |
   |                                  | processed.                       |
   |                                  |                                  |
   |                                  | Error indication message is      |
   |                                  | output to the Service Logs.      |
   |                                  |                                  |
   |                                  | No message is posted to the User |
   |                                  | Interface.                       |
   +----------------------------------+----------------------------------+

.. _sect_F.4.3:

Network Interfaces
~~~~~~~~~~~~~~~~~~

.. _sect_F.4.3.1:

Physical Network Interface
^^^^^^^^^^^^^^^^^^^^^^^^^^

The EXAMPLE-QUERY-RETRIEVE-SERVER supports a single network interface.
One of the following physical network interfaces will be available
depending on installed hardware options:

.. table:: Supported Physical Network Interfaces

   +-------------------+
   | Ethernet 100baseT |
   +-------------------+
   | Ethernet 10baseT  |
   +-------------------+

.. _sect_F.4.3.2:

Additional Protocols
^^^^^^^^^^^^^^^^^^^^

EXAMPLE-QUERY-RETRIEVE-SERVER conforms to the System Management Profiles
listed in `table_title <#table_F.4.3-2>`__. All requested transactions
for the listed profiles and actors are supported. It does not support
any optional transactions.

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

.. _sect_F.4.3.2.1:

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

.. _sect_F.4.3.2.2:

DNS
'''

DNS can be used for address resolution. If DHCP is not in use or the
DHCP server does not return any DNS server addresses, the identity of a
DNS server can be configured via the Service/Installation Tool. If a DNS
server is not in use, local mapping between hostname and IP address can
be manually configured via the Service/Installation Tool.

.. _sect_F.4.3.3:

IPv4 and IPv6 Support
^^^^^^^^^^^^^^^^^^^^^

This product supports both IPv4 and IPv6. It does not utilize any of the
optional configuration identification or security features of IPv6.

.. _sect_F.4.4:

Configuration
~~~~~~~~~~~~~

.. _sect_F.4.4.1:

AE Title/Presentation Address Mapping
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. _sect_F.4.4.1.1:

Local AE Titles
'''''''''''''''

The mapping from AE Title to TCP/IP addresses and ports is configurable
and set at the time of installation by Installation Personnel.

.. table:: Default Application Entity Characteristics

   ================== ==== ================ ===================
   Application Entity Role Default AE Title Default TCP/IP Port
   ================== ==== ================ ===================
   STORAGE-SCU        SCU  EX_STORE_SCU     None
   STORAGE-SCP        SCP  EX_STORE_SCP     4000
   QUERY-RETRIEVE-SCP SCP  EX_QUERY_SCP     5000
   ================== ==== ================ ===================

The STORAGE-SCU and QUERY-RETRIEVE-SCP Application Entities can be
configured to have the same AE Title. The STORAGE-SCP Application Entity
must not have the same AE Title as the other two.

.. _sect_F.4.4.1.2:

Remote AE Title/Presentation Address Mapping
''''''''''''''''''''''''''''''''''''''''''''

The mapping of external AE Titles to TCP/IP addresses and ports is
configurable and set at the time of installation by Installation
Personnel. This mapping is necessary for resolving the IP address and
port of C-MOVE Destination Application Entities and must be correctly
configured for the QUERY-RETRIEVE-SCP AE to correctly function as a
C-MOVE SCP.

.. _sect_F.4.4.2:

Parameters
^^^^^^^^^^

.. table:: Configuration Parameters

   +----------------------+----------------------+----------------------+
   | Parameter            | Configurable         | Default Value        |
   +======================+======================+======================+
   | **General            |                      |                      |
   | Parameters**         |                      |                      |
   +----------------------+----------------------+----------------------+
   | Maximum PDU size I   | Yes                  | 128kbytes            |
   | can receive          |                      |                      |
   +----------------------+----------------------+----------------------+
   | Maximum PDU size I   | Yes                  | 128kbytes            |
   | can send             |                      |                      |
   +----------------------+----------------------+----------------------+
   | Time-out waiting for | Yes                  | 10 s                 |
   | response to TCP/IP   |                      |                      |
   | connect() request.   |                      |                      |
   | (Low-level timeout)  |                      |                      |
   +----------------------+----------------------+----------------------+
   | Time-out waiting for | Yes                  | 30 s                 |
   | A-ASSOCIATE RQ PDU   |                      |                      |
   | on open TCP/IP       |                      |                      |
   | connection. (ARTIM   |                      |                      |
   | timeout)             |                      |                      |
   +----------------------+----------------------+----------------------+
   | Time-out waiting for | Yes                  | 30s                  |
   | acceptance or        |                      |                      |
   | rejection response   |                      |                      |
   | to an Association    |                      |                      |
   | Open Request.        |                      |                      |
   | (Application Level   |                      |                      |
   | timeout)             |                      |                      |
   +----------------------+----------------------+----------------------+
   | Time-out waiting for | Yes                  | 30 s                 |
   | acceptance of a      |                      |                      |
   | TCP/IP message over  |                      |                      |
   | the network.         |                      |                      |
   | (Low-level timeout)  |                      |                      |
   +----------------------+----------------------+----------------------+
   | Time-out for waiting | Yes                  | 30 s                 |
   | for data between     |                      |                      |
   | TCP/IP packets.      |                      |                      |
   | (Low-level timeout)  |                      |                      |
   +----------------------+----------------------+----------------------+
   | The Windows NT       | No                   | 1,342,177 bytes      |
   | TCP/IP socket buffer |                      |                      |
   | size is set to       |                      |                      |
   | 1,342,177 bytes in   |                      |                      |
   | order to improve     |                      |                      |
   | image data           |                      |                      |
   | throughput           |                      |                      |
   | performance.         |                      |                      |
   +----------------------+----------------------+----------------------+
   | **STORAGE-SCU AE     |                      |                      |
   | Parameters**         |                      |                      |
   +----------------------+----------------------+----------------------+
   | Maximum number of    | Yes                  | 10                   |
   | simultaneous         |                      |                      |
   | Associations.        |                      |                      |
   +----------------------+----------------------+----------------------+
   | STORAGE-SCU AE       | Yes                  | 5 minutes            |
   | time-out waiting for |                      |                      |
   | a Response to a      |                      |                      |
   | C-STORE-RQ. (DIMSE   |                      |                      |
   | timeout)             |                      |                      |
   +----------------------+----------------------+----------------------+
   | STORAGE-SCU AE       | No                   | 0                    |
   | number of times a    |                      |                      |
   | failed send job to a |                      |                      |
   | C-MOVE Destination   |                      |                      |
   | is automatically     |                      |                      |
   | retried.             |                      |                      |
   +----------------------+----------------------+----------------------+
   | **STORAGE-SCP AE     |                      |                      |
   | Parameters**         |                      |                      |
   +----------------------+----------------------+----------------------+
   | Maximum PDU Size     | Yes                  | 16384                |
   +----------------------+----------------------+----------------------+
   | Maximum number of    | Yes                  | 10                   |
   | simultaneous         |                      |                      |
   | Associations         |                      |                      |
   |                      |                      |                      |
   | (Can be configured   |                      |                      |
   | to be a maximum      |                      |                      |
   | total number or a    |                      |                      |
   | maximum per external |                      |                      |
   | SCU AE)              |                      |                      |
   +----------------------+----------------------+----------------------+
   | STORAGE-SCP AE       | Yes                  | 15 minutes           |
   | time-out waiting on  |                      |                      |
   | an open Association  |                      |                      |
   | for the next Request |                      |                      |
   | message (C-STORE-RQ, |                      |                      |
   | Association Close    |                      |                      |
   | Request. etc.)       |                      |                      |
   | (DIMSE timeout)      |                      |                      |
   +----------------------+----------------------+----------------------+
   | STORAGE-SCP AE       | Yes                  | 10                   |
   | maximum number of    |                      |                      |
   | simultaneous         | .. note::            |                      |
   | Associations         |                      |                      |
   |                      |    Can be configured |                      |
   |                      |    with a maximum    |                      |
   |                      |    per external AE   |                      |
   +----------------------+----------------------+----------------------+
   | Permanent archival   | Yes                  | FALSE                |
   | of SOP Instances     |                      |                      |
   | sent by a peer AE to |                      | (Such received SOP   |
   | the STORAGE-SCP AE   |                      | Instances are not    |
   | in response to a     |                      | archived.)           |
   | retrieval request    |                      |                      |
   | from QUERY-RETRIEVE  |                      |                      |
   | AE.                  |                      |                      |
   +----------------------+----------------------+----------------------+
   | Permanent archival   | Yes                  | TRUE                 |
   | of SOP Instances     |                      |                      |
   | sent unsolicited by  |                      | (Such received SOP   |
   | a peer AE to the     |                      | Instances are        |
   | STORAGE-SCP AE. I.e. |                      | archived.)           |
   | Not in response to a |                      |                      |
   | retrieval request    |                      |                      |
   | from QUERY-RETRIEVE  |                      |                      |
   | AE.                  |                      |                      |
   +----------------------+----------------------+----------------------+
   | Always open a new    | Yes                  | FALSE                |
   | Association to send  |                      |                      |
   | a Storage Commitment |                      | (Default is to try   |
   | Push Model           |                      | and send             |
   | Notification request |                      | Notifications over   |
   | (N-EVENT-REPORT-RQ). |                      | original Association |
   |                      |                      | opened by peer AE).  |
   +----------------------+----------------------+----------------------+
   | Maximum number of    | Yes                  | 5                    |
   | times to attempt     |                      |                      |
   | sending a Storage    |                      |                      |
   | Commitment Push      |                      |                      |
   | Model N-EVENT-REPORT |                      |                      |
   | Request when an      |                      |                      |
   | error status is      |                      |                      |
   | returned or          |                      |                      |
   | communication        |                      |                      |
   | failure occurs.      |                      |                      |
   +----------------------+----------------------+----------------------+
   | Time to wait between | Yes                  | 5 minutes            |
   | attempts to send a   |                      |                      |
   | Storage Commitment   |                      |                      |
   | Push Model           |                      |                      |
   | N-EVENT-REPORT       |                      |                      |
   | Request when an      |                      |                      |
   | error status is      |                      |                      |
   | returned or          |                      |                      |
   | communication        |                      |                      |
   | failure occurs.      |                      |                      |
   +----------------------+----------------------+----------------------+
   | **QUERY-RETRIEVE-SCP |                      |                      |
   | AE Parameters**      |                      |                      |
   +----------------------+----------------------+----------------------+
   | Maximum PDU Size     | Yes                  | 16384                |
   +----------------------+----------------------+----------------------+
   | Maximum number of    | Yes                  | 10                   |
   | simultaneous         |                      |                      |
   | Associations         |                      |                      |
   |                      |                      |                      |
   | (Can be configured   |                      |                      |
   | to be a maximum      |                      |                      |
   | total number or a    |                      |                      |
   | maximum per external |                      |                      |
   | SCU AE)              |                      |                      |
   +----------------------+----------------------+----------------------+
   | QUERY-RETRIEVE-SCP   | Yes                  | 3 minutes            |
   | AE time-out waiting  |                      |                      |
   | on an open           |                      |                      |
   | Association for the  |                      |                      |
   | next message         |                      |                      |
   | (C-FIND-RQ,          |                      |                      |
   | C-MOVE-RQ,           |                      |                      |
   | Association Close    |                      |                      |
   | Request. etc.)       |                      |                      |
   | (DIMSE timeout)      |                      |                      |
   +----------------------+----------------------+----------------------+
   | QUERY-RETRIEVE-SCP   | Yes                  | 10                   |
   | AE maximum number of |                      |                      |
   | simultaneous         | .. note::            |                      |
   | Associations         |                      |                      |
   |                      |    Can be configured |                      |
   |                      |    with a maximum    |                      |
   |                      |    per external AE   |                      |
   +----------------------+----------------------+----------------------+

.. _sect_F.5:

Media Interchange
-----------------

EXAMPLE-QUERY-RETRIEVE-SERVER does not support Media Storage.

.. _sect_F.6:

Support of Extended Character Sets
----------------------------------

All EXAMPLE-QUERY-RETRIEVE-SERVER DICOM applications support the
following:

ISO_IR 100 (ISO 8859-1:1987 Latin Alphabet No. 1 supplementary set)

As well as supporting this Extended Character Set for DICOM messaging,
the Query-Server system database and user interface can support the
expected display of this character set.

.. _sect_F.7:

Security
--------

.. _sect_F.7.1:

Security Profiles
~~~~~~~~~~~~~~~~~

The EXAMPLE-QUERY-RETRIEVE-SERVER conforms to the bit preserving Digital
Signatures Security Profile, if the STORAGE SCP AE receives a SOP
Instance in an Explicit Transfer Syntax and the STORAGE SCU AE can
export such SOP Instances using an Explicit Transfer Syntax.

.. _sect_F.7.2:

Association Level Security
~~~~~~~~~~~~~~~~~~~~~~~~~~

The QUERY-RETRIEVE-SCP AE and the STORAGE-SCP AE can both be configured
to check the following DICOM values when determining whether to accept
Association Open Requests:

Calling AE Title

Called AE Title

Application Context

Each SCP AE can be configured to accept Association Requests from only a
limited list of Calling AE Titles. They SCP AEs can have different
lists. Each SCP AE can be configured to check that the Association
requestor specifies the correct Called AE Title for the SCP.

In addition the IP address of the requestor can be checked. The SCP AEs
can be constrained to only accept Association Requests from a configured
list of IP addresses. The SCP AEs can have different lists.

.. _sect_F.8:

Annexes
-------

.. _sect_F.8.1:

IOD Contents
~~~~~~~~~~~~

.. _sect_F.8.1.1:

STORAGE-SCP AE Element Use
^^^^^^^^^^^^^^^^^^^^^^^^^^

The following Elements of Composite SOP Instances received by the
STORAGE-SCP AE are either stored to the permanent
EXAMPLE-QUERY-RETRIEVE-SERVER database or of particular importance in
the received images.

SOP Instances conforming to the following Composite Image SOP Classes
are fully supported for display on the system workstations.

.. table:: Supported Composite Image SOP Classes for Display

   +------------------------------------+
   | US Image Storage (Retired)         |
   +------------------------------------+
   | US Image Storage                   |
   +------------------------------------+
   | US Multi-frame Storage (Retired)   |
   +------------------------------------+
   | US Multi-frame Storage             |
   +------------------------------------+
   | Computed Radiography Image Storage |
   +------------------------------------+
   | CT Image Storage                   |
   +------------------------------------+
   | MR Image Storage                   |
   +------------------------------------+
   | Secondary Capture Image Storage    |
   +------------------------------------+

.. table:: Significant Elements in Received Composite SOP Instances

   +-------------+-------------+-------------+-------------+-------------+
   | Module      | Attribute   | Tag ID      | Type        | S           |
   |             | Name        |             |             | ignificance |
   +=============+=============+=============+=============+=============+
   | Patient     | Patient     | (0010,0010) | Opt         | STORAGE-SCP |
   |             | Name        |             |             | AE can be   |
   |             |             |             |             | configured  |
   |             |             |             |             | to apply a  |
   |             |             |             |             | default     |
   |             |             |             |             | value if    |
   |             |             |             |             | there is no |
   |             |             |             |             | value       |
   |             |             |             |             | specified.  |
   |             |             |             |             |             |
   |             |             |             |             | Value is    |
   |             |             |             |             | saved to    |
   |             |             |             |             | database as |
   |             |             |             |             | separate    |
   |             |             |             |             | first and   |
   |             |             |             |             | last names. |
   |             |             |             |             | Only first  |
   |             |             |             |             | and last    |
   |             |             |             |             | names are   |
   |             |             |             |             | entered in  |
   |             |             |             |             | the         |
   |             |             |             |             | EXAMPLE     |
   |             |             |             |             | -QUERY-RETR |
   |             |             |             |             | IEVE-SERVER |
   |             |             |             |             | database.   |
   |             |             |             |             | Both first  |
   |             |             |             |             | and last    |
   |             |             |             |             | names can   |
   |             |             |             |             | be a        |
   |             |             |             |             | maximum of  |
   |             |             |             |             | 64          |
   |             |             |             |             | characters  |
   |             |             |             |             | each.       |
   |             |             |             |             |             |
   |             |             |             |             | Names will  |
   |             |             |             |             | be parsed   |
   |             |             |             |             | correctly   |
   |             |             |             |             | if they are |
   |             |             |             |             | in the      |
   |             |             |             |             | format of   |
   |             |             |             |             | 'l          |
   |             |             |             |             | name^fname' |
   |             |             |             |             | or 'lname,  |
   |             |             |             |             | fname'. If  |
   |             |             |             |             | space       |
   |             |             |             |             | separation  |
   |             |             |             |             | is used     |
   |             |             |             |             | (i.e.,      |
   |             |             |             |             | 'lname      |
   |             |             |             |             | fname')     |
   |             |             |             |             | then the    |
   |             |             |             |             | entire name |
   |             |             |             |             | will be     |
   |             |             |             |             | treated as  |
   |             |             |             |             | the last    |
   |             |             |             |             | name.       |
   +-------------+-------------+-------------+-------------+-------------+
   | Patient ID  | (0010,0020) | Opt         | STORAGE-SCP |             |
   |             |             |             | AE can be   |             |
   |             |             |             | configured  |             |
   |             |             |             | to apply a  |             |
   |             |             |             | default     |             |
   |             |             |             | value if    |             |
   |             |             |             | there is no |             |
   |             |             |             | value       |             |
   |             |             |             | specified.  |             |
   |             |             |             |             |             |
   |             |             |             | V           |             |
   |             |             |             | erification |             |
   |             |             |             | on incoming |             |
   |             |             |             | Patient IDs |             |
   |             |             |             | is          |             |
   |             |             |             | performed.  |             |
   |             |             |             | If an ID    |             |
   |             |             |             | already     |             |
   |             |             |             | exists but  |             |
   |             |             |             | the         |             |
   |             |             |             | existing    |             |
   |             |             |             | name does   |             |
   |             |             |             | not match,  |             |
   |             |             |             | then the ID |             |
   |             |             |             | is coerced  |             |
   |             |             |             | because     |             |
   |             |             |             | different   |             |
   |             |             |             | Patient     |             |
   |             |             |             | records in  |             |
   |             |             |             | the         |             |
   |             |             |             | EXAMPLE     |             |
   |             |             |             | -QUERY-RETR |             |
   |             |             |             | IEVE-SERVER |             |
   |             |             |             | database    |             |
   |             |             |             | cannot have |             |
   |             |             |             | identical   |             |
   |             |             |             | Patient     |             |
   |             |             |             | IDs.        |             |
   |             |             |             |             |             |
   |             |             |             | Value is    |             |
   |             |             |             | saved to    |             |
   |             |             |             | database.   |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Patient's   | (0010,0030) | Opt         | STORAGE-SCP |             |
   | Birth Date  |             |             | AE can be   |             |
   |             |             |             | configured  |             |
   |             |             |             | to apply a  |             |
   |             |             |             | default     |             |
   |             |             |             | value if    |             |
   |             |             |             | there is no |             |
   |             |             |             | value       |             |
   |             |             |             | specified.  |             |
   |             |             |             |             |             |
   |             |             |             | Value is    |             |
   |             |             |             | saved to    |             |
   |             |             |             | database.   |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Patient's   | (0010,0040) | Opt         | First       |             |
   | Sex         |             |             | character   |             |
   |             |             |             | must be     |             |
   |             |             |             | 'M', 'm',   |             |
   |             |             |             | 'F', 'f',   |             |
   |             |             |             | 'O', or     |             |
   |             |             |             | 'o'. If a   |             |
   |             |             |             | different   |             |
   |             |             |             | value, or   |             |
   |             |             |             | not         |             |
   |             |             |             | specified,  |             |
   |             |             |             | then will   |             |
   |             |             |             | be entered  |             |
   |             |             |             | in the      |             |
   |             |             |             | database as |             |
   |             |             |             | 'U',        |             |
   |             |             |             | unknown.    |             |
   |             |             |             | Value is    |             |
   |             |             |             | saved to    |             |
   |             |             |             | database.   |             |
   |             |             |             | 'U' is      |             |
   |             |             |             | never       |             |
   |             |             |             | exported in |             |
   |             |             |             | DICOM       |             |
   |             |             |             | images;     |             |
   |             |             |             | instead,    |             |
   |             |             |             | the Element |             |
   |             |             |             | value will  |             |
   |             |             |             | be left     |             |
   |             |             |             | empty for   |             |
   |             |             |             | export.     |             |
   +-------------+-------------+-------------+-------------+-------------+
   | General     | Study       | (0020,000D) | Mand        | Must be     |
   | Study       | Instance    |             |             | provided.   |
   |             | UID         |             |             |             |
   |             |             |             |             | Value is    |
   |             |             |             |             | saved to    |
   |             |             |             |             | database.   |
   +-------------+-------------+-------------+-------------+-------------+
   | Study Date  | (0008,0020) | Opt         | STORAGE-SCP |             |
   |             |             |             | AE can be   |             |
   |             |             |             | configured  |             |
   |             |             |             | to apply a  |             |
   |             |             |             | default     |             |
   |             |             |             | value if    |             |
   |             |             |             | there is no |             |
   |             |             |             | value       |             |
   |             |             |             | specified.  |             |
   |             |             |             |             |             |
   |             |             |             | Value is    |             |
   |             |             |             | saved to    |             |
   |             |             |             | database.   |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Referring   | (0008,0090) | Opt         | Value is    |             |
   | Physician's |             |             | saved to    |             |
   | Name        |             |             | database.   |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Accession   | (0008,0050) | Opt         | STORAGE-SCP |             |
   | Number      |             |             | AE can be   |             |
   |             |             |             | configured  |             |
   |             |             |             | to apply a  |             |
   |             |             |             | default     |             |
   |             |             |             | value if    |             |
   |             |             |             | there is no |             |
   |             |             |             | value       |             |
   |             |             |             | specified.  |             |
   |             |             |             | Matching    |             |
   |             |             |             | used to     |             |
   |             |             |             | determine   |             |
   |             |             |             | which       |             |
   |             |             |             | Accession   |             |
   |             |             |             | number to   |             |
   |             |             |             | apply is    |             |
   |             |             |             | c           |             |
   |             |             |             | onfigurable |             |
   |             |             |             | (i.e.,      |             |
   |             |             |             | HIS/RIS     |             |
   |             |             |             | provided    |             |
   |             |             |             | Accession   |             |
   |             |             |             | Number may  |             |
   |             |             |             | be used if  |             |
   |             |             |             | the Patient |             |
   |             |             |             | ID, Patient |             |
   |             |             |             | Name, Study |             |
   |             |             |             | Date, and   |             |
   |             |             |             | Modality    |             |
   |             |             |             | provided in |             |
   |             |             |             | the HIS/RIS |             |
   |             |             |             | and SOP     |             |
   |             |             |             | Instance    |             |
   |             |             |             | match).     |             |
   |             |             |             |             |             |
   |             |             |             | Value is    |             |
   |             |             |             | saved to    |             |
   |             |             |             | database.   |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Study       | (0008,1030) | Opt         | If matched  |             |
   | Description |             |             | value(s) in |             |
   |             |             |             | the         |             |
   |             |             |             | EXAMPLE     |             |
   |             |             |             | -QUERY-RETR |             |
   |             |             |             | IEVE-SERVER |             |
   |             |             |             | exam type   |             |
   |             |             |             | database,   |             |
   |             |             |             | then it     |             |
   |             |             |             | will be     |             |
   |             |             |             | saved to    |             |
   |             |             |             | the         |             |
   |             |             |             | database as |             |
   |             |             |             | an exam     |             |
   |             |             |             | type.       |             |
   +-------------+-------------+-------------+-------------+-------------+
   | General     | Modality    | (0008,0060) | Opt         | STORAGE-SCP |
   | Series      |             |             |             | AE can be   |
   |             |             |             |             | configured  |
   |             |             |             |             | to apply a  |
   |             |             |             |             | default     |
   |             |             |             |             | value if    |
   |             |             |             |             | there is no |
   |             |             |             |             | value       |
   |             |             |             |             | specified.  |
   |             |             |             |             |             |
   |             |             |             |             | Value is    |
   |             |             |             |             | saved to    |
   |             |             |             |             | database    |
   |             |             |             |             | but must be |
   |             |             |             |             | two         |
   |             |             |             |             | characters  |
   |             |             |             |             | in length.  |
   +-------------+-------------+-------------+-------------+-------------+
   | Series      | (0008,103E) | Opt         | If matched  |             |
   | Description |             |             | value(s) in |             |
   |             |             |             | the         |             |
   |             |             |             | EXAMPLE     |             |
   |             |             |             | -QUERY-RETR |             |
   |             |             |             | IEVE-SERVER |             |
   |             |             |             | exam type   |             |
   |             |             |             | database    |             |
   |             |             |             | then it     |             |
   |             |             |             | will be     |             |
   |             |             |             | saved to    |             |
   |             |             |             | the         |             |
   |             |             |             | database as |             |
   |             |             |             | an exam     |             |
   |             |             |             | type.       |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Operator's  | (0008,1070) | Opt         | Value is    |             |
   | Name        |             |             | saved to    |             |
   |             |             |             | database.   |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Body Part   | (0018,0015) | Opt         | If matched  |             |
   | Examined    |             |             | value(s) in |             |
   |             |             |             | the         |             |
   |             |             |             | EXAMPLE     |             |
   |             |             |             | -QUERY-RETR |             |
   |             |             |             | IEVE-SERVER |             |
   |             |             |             | exam type   |             |
   |             |             |             | database    |             |
   |             |             |             | then it     |             |
   |             |             |             | will be     |             |
   |             |             |             | saved to    |             |
   |             |             |             | the         |             |
   |             |             |             | database as |             |
   |             |             |             | an exam     |             |
   |             |             |             | type.       |             |
   +-------------+-------------+-------------+-------------+-------------+
   | General     | Image Type  | (0008,0008) | Opt         | If the      |
   | Image       |             |             |             | third       |
   |             |             |             |             | value, the  |
   |             |             |             |             | modality    |
   |             |             |             |             | specific    |
   |             |             |             |             | value,      |
   |             |             |             |             | matches     |
   |             |             |             |             | value(s) in |
   |             |             |             |             | the         |
   |             |             |             |             | EXAMPLE     |
   |             |             |             |             | -QUERY-RETR |
   |             |             |             |             | IEVE-SERVER |
   |             |             |             |             | exam type   |
   |             |             |             |             | database    |
   |             |             |             |             | then it     |
   |             |             |             |             | will be     |
   |             |             |             |             | saved to    |
   |             |             |             |             | the         |
   |             |             |             |             | database as |
   |             |             |             |             | an exam     |
   |             |             |             |             | type.       |
   +-------------+-------------+-------------+-------------+-------------+
   | Image Plane | Pixel       | (0028,0030) | Opt         | Used for    |
   |             | Spacing     |             |             | automatic   |
   |             |             |             |             | scaling of  |
   |             |             |             |             | measurement |
   |             |             |             |             | tool if     |
   |             |             |             |             | specified   |
   |             |             |             |             | in an image |
   |             |             |             |             | SOP         |
   |             |             |             |             | Instance.   |
   +-------------+-------------+-------------+-------------+-------------+
   | US Region   | Sequence of | (0018,6011) | Opt         | Used for    |
   | Calibration | Ultrasound  |             |             | automatic   |
   |             | Regions     |             |             | scaling of  |
   |             |             |             |             | measurement |
   |             |             |             |             | tool if     |
   |             |             |             |             | specified   |
   |             |             |             |             | in an       |
   |             |             |             |             | Ultrasound  |
   |             |             |             |             | or          |
   |             |             |             |             | Ultrasound  |
   |             |             |             |             | Multi-frame |
   |             |             |             |             | Image SOP   |
   |             |             |             |             | Instance.   |
   +-------------+-------------+-------------+-------------+-------------+
   | Image Pixel | Photometric | (0028,0004) | Cond        | The         |
   |             | Int         |             |             | following   |
   |             | erpretation |             |             | photometric |
   |             |             |             |             | inte        |
   |             |             |             |             | rpretations |
   |             |             |             |             | are         |
   |             |             |             |             | supported   |
   |             |             |             |             | for image   |
   |             |             |             |             | display     |
   |             |             |             |             | purposes:   |
   |             |             |             |             |             |
   |             |             |             |             | M           |
   |             |             |             |             | ONOCHROME1, |
   |             |             |             |             | M           |
   |             |             |             |             | ONOCHROME2, |
   |             |             |             |             | RGB,        |
   |             |             |             |             |             |
   |             |             |             |             | PALETTE     |
   |             |             |             |             | COLOR, YBR  |
   |             |             |             |             | FULL 422,   |
   |             |             |             |             | and YBR     |
   |             |             |             |             | FULL.       |
   |             |             |             |             |             |
   |             |             |             |             | Required if |
   |             |             |             |             | SOP         |
   |             |             |             |             | Instance is |
   |             |             |             |             | an Image.   |
   +-------------+-------------+-------------+-------------+-------------+
   | Bits        | (0028,0100) | Cond        | Must be 8   |             |
   | Allocated   |             |             | or 16 bits  |             |
   |             |             |             | for image   |             |
   |             |             |             | display     |             |
   |             |             |             | purposes.   |             |
   |             |             |             |             |             |
   |             |             |             | Required if |             |
   |             |             |             | SOP         |             |
   |             |             |             | Instance is |             |
   |             |             |             | an Image.   |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Bits Stored | (0028,0101) | Cond        | All values  |             |
   |             |             |             | of 16 or    |             |
   |             |             |             | fewer are   |             |
   |             |             |             | supported   |             |
   |             |             |             | for image   |             |
   |             |             |             | display     |             |
   |             |             |             | purposes.   |             |
   |             |             |             |             |             |
   |             |             |             | Required if |             |
   |             |             |             | SOP         |             |
   |             |             |             | Instance is |             |
   |             |             |             | an Image.   |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Overlay     | Overlay     | (6000,0010) | Cond        | Number of   |
   | Plane       | Rows        |             |             | Rows in     |
   | Module      |             |             |             | Overlay.    |
   |             |             |             |             |             |
   | (See Note)  |             |             |             | Required in |
   |             |             |             |             | order to    |
   |             |             |             |             | display an  |
   |             |             |             |             | Overlay.    |
   +-------------+-------------+-------------+-------------+-------------+
   | Overlay     | (6000,0011) | Cond        | Number of   |             |
   | Columns     |             |             | Columns in  |             |
   |             |             |             | Overlay.    |             |
   |             |             |             |             |             |
   |             |             |             | Required in |             |
   |             |             |             | order to    |             |
   |             |             |             | display an  |             |
   |             |             |             | Overlay.    |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Overlay     | (6000,0040) | Cond        | Overlay     |             |
   | Type        |             |             | data is     |             |
   |             |             |             | used only   |             |
   |             |             |             | if the      |             |
   |             |             |             | value is    |             |
   |             |             |             | "G",        |             |
   |             |             |             | Graphics.   |             |
   |             |             |             | Graphic     |             |
   |             |             |             | overlay     |             |
   |             |             |             | data can be |             |
   |             |             |             | au          |             |
   |             |             |             | tomatically |             |
   |             |             |             | displayed   |             |
   |             |             |             | if the      |             |
   |             |             |             | system is   |             |
   |             |             |             | configured  |             |
   |             |             |             | to do so.   |             |
   |             |             |             | "ROI",      |             |
   |             |             |             | Region Of   |             |
   |             |             |             | Interest,   |             |
   |             |             |             | overlay     |             |
   |             |             |             | data is not |             |
   |             |             |             | displayed   |             |
   |             |             |             | to the user |             |
   |             |             |             | of the      |             |
   |             |             |             | system.     |             |
   |             |             |             |             |             |
   |             |             |             | Required in |             |
   |             |             |             | order to    |             |
   |             |             |             | display an  |             |
   |             |             |             | Overlay.    |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Overlay     | (6000,0050) | Cond        | Value must  |             |
   | Origin      |             |             | be 1\1 or   |             |
   |             |             |             | greater. If |             |
   |             |             |             | either      |             |
   |             |             |             | Overlay     |             |
   |             |             |             | Origin      |             |
   |             |             |             | coordinate  |             |
   |             |             |             | is less     |             |
   |             |             |             | than 1 then |             |
   |             |             |             | the overlay |             |
   |             |             |             | is not      |             |
   |             |             |             | displayed.  |             |
   |             |             |             |             |             |
   |             |             |             | Required in |             |
   |             |             |             | order to    |             |
   |             |             |             | display an  |             |
   |             |             |             | Overlay.    |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Overlay     | (6000,0100) | Cond        | Must be 8   |             |
   | Bits        |             |             | or 16 if    |             |
   | Allocated   |             |             | the overlay |             |
   |             |             |             | data are    |             |
   |             |             |             | embedded.   |             |
   |             |             |             |             |             |
   |             |             |             | Required in |             |
   |             |             |             | order to    |             |
   |             |             |             | display an  |             |
   |             |             |             | Overlay.    |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Overlay Bit | (6000,0102) | Cond        | Used if the |             |
   | Position    |             |             | overlay     |             |
   |             |             |             | data is     |             |
   |             |             |             | embedded.   |             |
   |             |             |             | If the data |             |
   |             |             |             | is embedded |             |
   |             |             |             | then this   |             |
   |             |             |             | position    |             |
   |             |             |             | must        |             |
   |             |             |             | indicate a  |             |
   |             |             |             | bit not     |             |
   |             |             |             | used by     |             |
   |             |             |             | each image  |             |
   |             |             |             | pixel       |             |
   |             |             |             | sample.     |             |
   |             |             |             |             |             |
   |             |             |             | Required in |             |
   |             |             |             | order to    |             |
   |             |             |             | display an  |             |
   |             |             |             | Overlay.    |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Overlay     | (6000,3000) | Cond        | Overlay     |             |
   | Data        |             |             | data        |             |
   |             |             |             | present in  |             |
   |             |             |             | this        |             |
   |             |             |             | Element or  |             |
   |             |             |             | embedded in |             |
   |             |             |             | the pixel   |             |
   |             |             |             | data is     |             |
   |             |             |             | supported   |             |
   |             |             |             | for         |             |
   |             |             |             | display.    |             |
   |             |             |             |             |             |
   |             |             |             | Required in |             |
   |             |             |             | order to    |             |
   |             |             |             | display a   |             |
   |             |             |             | n           |             |
   |             |             |             | on-embedded |             |
   |             |             |             | Overlay.    |             |
   +-------------+-------------+-------------+-------------+-------------+
   | VOI LUT     | Window      | (0028,1050) | Opt         | It is       |
   |             | Center      |             |             | recommended |
   |             |             |             |             | that this   |
   |             |             |             |             | value be    |
   |             |             |             |             | defined for |
   |             |             |             |             | images that |
   |             |             |             |             | have        |
   |             |             |             |             | greater     |
   |             |             |             |             | than 8 bits |
   |             |             |             |             | stored per  |
   |             |             |             |             | pixel       |
   |             |             |             |             | sample for  |
   |             |             |             |             | image       |
   |             |             |             |             | display     |
   +-------------+-------------+-------------+-------------+-------------+
   | Window      | (0028,1051) | Opt         | It is       |             |
   | Width       |             |             | recommended |             |
   |             |             |             | that this   |             |
   |             |             |             | value be    |             |
   |             |             |             | defined for |             |
   |             |             |             | images that |             |
   |             |             |             | have        |             |
   |             |             |             | greater     |             |
   |             |             |             | than 8 bits |             |
   |             |             |             | stored per  |             |
   |             |             |             | pixel       |             |
   |             |             |             | sample for  |             |
   |             |             |             | image       |             |
   |             |             |             | display     |             |
   +-------------+-------------+-------------+-------------+-------------+
   | SOP Common  | SOP         | (0008,0018) | Mand        | Must be     |
   |             | Instance    |             |             | provided.   |
   |             | UID         |             |             | If a        |
   |             |             |             |             | duplicate   |
   |             |             |             |             | SOP         |
   |             |             |             |             | Instance    |
   |             |             |             |             | UID is      |
   |             |             |             |             | received,   |
   |             |             |             |             | the system  |
   |             |             |             |             | can be      |
   |             |             |             |             | configured  |
   |             |             |             |             | to either   |
   |             |             |             |             | coerce the  |
   |             |             |             |             | duplicate   |
   |             |             |             |             | value with  |
   |             |             |             |             | a new UID   |
   |             |             |             |             | or replace  |
   |             |             |             |             | the         |
   |             |             |             |             | original    |
   |             |             |             |             | UID with    |
   |             |             |             |             | the newly   |
   |             |             |             |             | received    |
   |             |             |             |             | one. The    |
   |             |             |             |             | system can  |
   |             |             |             |             | also be     |
   |             |             |             |             | configured  |
   |             |             |             |             | to either   |
   |             |             |             |             | preserve    |
   |             |             |             |             | the         |
   |             |             |             |             | original    |
   |             |             |             |             | UID or      |
   |             |             |             |             | assign a    |
   |             |             |             |             | new UID if  |
   |             |             |             |             | the         |
   |             |             |             |             | received    |
   |             |             |             |             | image data  |
   |             |             |             |             | is lossy    |
   |             |             |             |             | compressed  |
   |             |             |             |             | by the      |
   |             |             |             |             | QUERY-RETR  |
   |             |             |             |             | IEVE-SERVER |
   |             |             |             |             | prior to    |
   |             |             |             |             | archival.   |
   +-------------+-------------+-------------+-------------+-------------+

.. note::

   Note that only overlay information contained in the 6000 Group will
   be used for display. Overlay information contained in the other
   possible Groups (6002, 6004, etc.) will be ignored for display
   purposes. Such information will still be archived however.

.. _sect_F.8.1.2:

STORAGE-SCU AE Element Modification
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The following table contains a list of all Elements that can have a
value modified by the STORAGE-SCU at the time of export using the
Storage Service depending on the capabilities of the receiver:

.. table:: Significant Elements in Exported Composite SOP Instances

   +--------------+----------------+----------------+----------------+
   | Module       | Attribute Name | Tag ID         | Value          |
   +==============+================+================+================+
   | Image Pixel  | Photometric    | (0028,0004)    | STORAGE-SCU AE |
   |              | Interpretation |                | can convert    |
   |              |                |                | all images to  |
   |              |                |                | MONOCHROME2 or |
   |              |                |                | RGB based on   |
   |              |                |                | the            |
   |              |                |                | configuration  |
   |              |                |                | for the        |
   |              |                |                | destination    |
   |              |                |                | AE.            |
   |              |                |                |                |
   |              |                |                | If the         |
   |              |                |                | photometric    |
   |              |                |                | interpretation |
   |              |                |                | of the image   |
   |              |                |                | data is        |
   |              |                |                | altered in a   |
   |              |                |                | lossy manner,  |
   |              |                |                | which could    |
   |              |                |                | occur when     |
   |              |                |                | converting     |
   |              |                |                | from color to  |
   |              |                |                | grayscale,     |
   |              |                |                | then the SOP   |
   |              |                |                | Instance UID   |
   |              |                |                | is altered.    |
   +--------------+----------------+----------------+----------------+
   | VOI LUT      | Window Center  | (0028,1050)    | Default Window |
   |              |                |                | Center value   |
   |              |                |                | can be         |
   |              |                |                | configured for |
   |              |                |                | a specific     |
   |              |                |                | destination    |
   |              |                |                | AE.            |
   +--------------+----------------+----------------+----------------+
   | Window Width | (0028,1051)    | Default Window |                |
   |              |                | Width value    |                |
   |              |                | can be         |                |
   |              |                | configured for |                |
   |              |                | a specific     |                |
   |              |                | external       |                |
   |              |                | destination    |                |
   |              |                | AE.            |                |
   +--------------+----------------+----------------+----------------+
   | SOP Common   | SOP Instance   | (0008,0018)    | System assigns |
   |              | UID            |                | a new UID if   |
   |              |                |                | the image data |
   |              |                |                | is lossy       |
   |              |                |                | compressed by  |
   |              |                |                | the            |
   |              |                |                | STORAGE-SCU AE |
   |              |                |                | at the time of |
   |              |                |                | export. Unless |
   |              |                |                | the pixel data |
   |              |                |                | is lossy       |
   |              |                |                | compressed or  |
   |              |                |                | there is a     |
   |              |                |                | conflict       |
   |              |                |                | between        |
   |              |                |                | duplicate SOP  |
   |              |                |                | Instance UIDs  |
   |              |                |                | the original   |
   |              |                |                | value received |
   |              |                |                | is not         |
   |              |                |                | altered.       |
   +--------------+----------------+----------------+----------------+

