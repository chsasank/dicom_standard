.. _chapter_D:

Conformance Statement Sample DICOM Image Viewer (Informative)
=============================================================

Disclaimer:

This document is an example DICOM Conformance Statement for a fictional
image display device for DICOM images and spectroscopy objects obtained
over the network, from interchange media, or from files loaded from the
local file system.

As stated in the annex title, this document is truly informative, and
not normative. A conformance statement of an actual product might
implement additional services and options as appropriate for its
specific purpose. In addition, an actual product might implement the
services described in a different manner and, for example, with
different characteristics and/or sequencing of activities. In other
words, this conformance statement example does not intend to standardize
a particular manner that a product might implement DICOM functionality.

.. _sect_D.0:

Cover Page
----------

Company Name: EXAMPLE-Viewing ­PRODUCTS.

Product Name: SAMPLE DICOM Image Viewer

Version: 1.0-rev. A.1

Internal document number: 4226-xxx-yyy-zzz rev 1

Date: YYYYMMDD

.. _sect_D.1:

Conformance Statement Overview
------------------------------

The application supports querying a remote system for a list of DICOM
objects that may then be retrieved to the local system. It also supports
sending locally loaded images across the network to another system.

All storage SOP Classes defined as of DICOM 2002 can be received, stored
and transmitted by the application, but only images and spectroscopy
objects may be loaded and viewed. All single and multi-frame with
grayscale and RGB color (but not palette color, except for Enhanced MR
images) images may be displayed.

Only hierarchical query and retrieval is supported.

.. table:: Network Services

   +----------------------+----------------------+----------------------+
   | SOP Classes          | User of Service(SCU) | Provider of          |
   |                      |                      | Service(SCP)         |
   +======================+======================+======================+
   | Transfer             |                      |                      |
   +----------------------+----------------------+----------------------+
   | Stored Print Storage | Stored only          | Yes                  |
   | SOP Class            |                      |                      |
   +----------------------+----------------------+----------------------+
   | Hardcopy Grayscale   | Stored and Viewed    | Yes                  |
   | Image Storage SOP    |                      |                      |
   | Class                |                      |                      |
   +----------------------+----------------------+----------------------+
   | Hardcopy Color Image | Stored and Viewed    | Yes                  |
   | Storage SOP Class    |                      |                      |
   +----------------------+----------------------+----------------------+
   | Computed Radiography | Stored and Viewed    | Yes                  |
   | Image Storage        |                      |                      |
   +----------------------+----------------------+----------------------+
   | Digital X-Ray Image  | Stored and Viewed    | Yes                  |
   | Storage - For        |                      |                      |
   | Presentation         |                      |                      |
   +----------------------+----------------------+----------------------+
   | Digital X-Ray Image  | Stored only          | Yes                  |
   | Storage - For        |                      |                      |
   | Processing           |                      |                      |
   +----------------------+----------------------+----------------------+
   | Digital Mammography  | Stored and Viewed    | Yes                  |
   | X-Ray Image Storage  |                      |                      |
   | - For Presentation   |                      |                      |
   +----------------------+----------------------+----------------------+
   | Digital Mammography  | Stored only          | Yes                  |
   | X-Ray Image Storage  |                      |                      |
   | - For Processing     |                      |                      |
   +----------------------+----------------------+----------------------+
   | Digital Intra-oral   | Stored and Viewed    | Yes                  |
   | X-Ray Image Storage  |                      |                      |
   | - For Presentation   |                      |                      |
   +----------------------+----------------------+----------------------+
   | Digital Intra-oral   | Stored only          | Yes                  |
   | X-Ray Image Storage  |                      |                      |
   | - For Processing     |                      |                      |
   +----------------------+----------------------+----------------------+
   | CT Image Storage     | Stored and Viewed    | Yes                  |
   +----------------------+----------------------+----------------------+
   | Ultrasound           | Stored and Viewed    | Yes                  |
   | Multi-frame Image    |                      |                      |
   | Storage (Retired)    |                      |                      |
   +----------------------+----------------------+----------------------+
   | Ultrasound           | Stored and Viewed    | Yes                  |
   | Multi-frame Image    |                      |                      |
   | Storage              |                      |                      |
   +----------------------+----------------------+----------------------+
   | MR Image Storage     | Stored and Viewed    | Yes                  |
   +----------------------+----------------------+----------------------+
   | Enhanced MR Image    | Stored and Viewed    | Yes                  |
   | Storage              |                      |                      |
   +----------------------+----------------------+----------------------+
   | MR Spectroscopy      | Stored and Viewed    | Yes                  |
   | Storage              |                      |                      |
   +----------------------+----------------------+----------------------+
   | Nuclear Medicine     | Stored and Viewed    | Yes                  |
   | Image Storage        |                      |                      |
   | (Retired)            |                      |                      |
   +----------------------+----------------------+----------------------+
   | Ultrasound Image     | Stored and Viewed    | Yes                  |
   | Storage (Retired)    |                      |                      |
   +----------------------+----------------------+----------------------+
   | Ultrasound Image     | Stored and Viewed    | Yes                  |
   | Storage              |                      |                      |
   +----------------------+----------------------+----------------------+
   | Secondary Capture    | Stored and Viewed    | Yes                  |
   | Image Storage        |                      |                      |
   +----------------------+----------------------+----------------------+
   | Multi-frame Single   | Stored and Viewed    | Yes                  |
   | Bit Secondary        |                      |                      |
   | Capture Image        |                      |                      |
   | Storage              |                      |                      |
   +----------------------+----------------------+----------------------+
   | Multi-frame          | Stored and Viewed    | Yes                  |
   | Grayscale Byte       |                      |                      |
   | Secondary Capture    |                      |                      |
   | Image Storage        |                      |                      |
   +----------------------+----------------------+----------------------+
   | Multi-frame          | Stored and Viewed    | Yes                  |
   | Grayscale Word       |                      |                      |
   | Secondary Capture    |                      |                      |
   | Image Storage        |                      |                      |
   +----------------------+----------------------+----------------------+
   | Multi-frame True     | Stored and Viewed    | Yes                  |
   | Color Secondary      |                      |                      |
   | Capture Image        |                      |                      |
   | Storage              |                      |                      |
   +----------------------+----------------------+----------------------+
   | Standalone Overlay   | Stored only          | Yes                  |
   | Storage              |                      |                      |
   +----------------------+----------------------+----------------------+
   | Standalone Curve     | Stored only          | Yes                  |
   | Storage              |                      |                      |
   +----------------------+----------------------+----------------------+
   | 12-lead ECG Waveform | Stored only          | Yes                  |
   | Storage              |                      |                      |
   +----------------------+----------------------+----------------------+
   | General ECG Waveform | Stored only          | Yes                  |
   | Storage              |                      |                      |
   +----------------------+----------------------+----------------------+
   | Ambulatory ECG       | Stored only          | Yes                  |
   | Waveform Storage     |                      |                      |
   +----------------------+----------------------+----------------------+
   | Hemodynamic Waveform | Stored only          | Yes                  |
   | Storage              |                      |                      |
   +----------------------+----------------------+----------------------+
   | Cardiac              | Stored only          | Yes                  |
   | Electrophysiology    |                      |                      |
   | Waveform Storage     |                      |                      |
   +----------------------+----------------------+----------------------+
   | Basic Voice Audio    | Stored only          | Yes                  |
   | Waveform Storage     |                      |                      |
   +----------------------+----------------------+----------------------+
   | Standalone Modality  | Stored only          | Yes                  |
   | LUT Storage          |                      |                      |
   +----------------------+----------------------+----------------------+
   | Standalone VOI LUT   | Stored only          | Yes                  |
   | Storage              |                      |                      |
   +----------------------+----------------------+----------------------+
   | Grayscale Softcopy   | Stored and Viewed    | Yes                  |
   | Presentation State   |                      |                      |
   | Storage SOP Class    |                      |                      |
   +----------------------+----------------------+----------------------+
   | X-Ray Angiographic   | Stored and Viewed    | Yes                  |
   | Image Storage        |                      |                      |
   +----------------------+----------------------+----------------------+
   | X-Ray                | Stored and Viewed    | Yes                  |
   | Radiofluoroscopic    |                      |                      |
   | Image Storage        |                      |                      |
   +----------------------+----------------------+----------------------+
   | X-Ray Angiographic   | Stored only          | Yes                  |
   | Bi-Plane Image       |                      |                      |
   | Storage (Retired)    |                      |                      |
   +----------------------+----------------------+----------------------+
   | Nuclear Medicine     | Stored and Viewed    | Yes                  |
   | Image Storage        |                      |                      |
   +----------------------+----------------------+----------------------+
   | Raw Data Storage     | Stored only          | Yes                  |
   +----------------------+----------------------+----------------------+
   | VL Image Storage     | Stored and Viewed    | Yes                  |
   | (Retired)            |                      |                      |
   +----------------------+----------------------+----------------------+
   | VL Multi-frame Image | Stored and Viewed    | Yes                  |
   | Storage (Retired)    |                      |                      |
   +----------------------+----------------------+----------------------+
   | VL Endoscopic Image  | Stored and Viewed    | Yes                  |
   | Storage              |                      |                      |
   +----------------------+----------------------+----------------------+
   | VL Microscopic Image | Stored and Viewed    | Yes                  |
   | Storage              |                      |                      |
   +----------------------+----------------------+----------------------+
   | VL Slide-Coordinates | Stored and Viewed    | Yes                  |
   | Microscopic Image    |                      |                      |
   | Storage              |                      |                      |
   +----------------------+----------------------+----------------------+
   | VL Photographic      | Stored and Viewed    | Yes                  |
   | Image Storage        |                      |                      |
   +----------------------+----------------------+----------------------+
   | Basic Text SR        | Stored only          | Yes                  |
   +----------------------+----------------------+----------------------+
   | Enhanced SR          | Stored only          | Yes                  |
   +----------------------+----------------------+----------------------+
   | Comprehensive SR     | Stored only          | Yes                  |
   +----------------------+----------------------+----------------------+
   | Mammography CAD SR   | Stored only          | Yes                  |
   +----------------------+----------------------+----------------------+
   | Key Object Selection | Stored only          | Yes                  |
   | Document             |                      |                      |
   +----------------------+----------------------+----------------------+
   | Positron Emission    | Stored and Viewed    | Yes                  |
   | Tomography Image     |                      |                      |
   | Storage              |                      |                      |
   +----------------------+----------------------+----------------------+
   | Standalone PET Curve | Stored only          | Yes                  |
   | Storage              |                      |                      |
   +----------------------+----------------------+----------------------+
   | RT Image Storage     | Stored and Viewed    | Yes                  |
   +----------------------+----------------------+----------------------+
   | RT Dose Storage      | Stored only          | Yes                  |
   +----------------------+----------------------+----------------------+
   | RT Structure Set     | Stored only          | Yes                  |
   | Storage              |                      |                      |
   +----------------------+----------------------+----------------------+
   | RT Beams Treatment   | Stored only          | Yes                  |
   | Record Storage       |                      |                      |
   +----------------------+----------------------+----------------------+
   | RT Plan Storage      | Stored only          | Yes                  |
   +----------------------+----------------------+----------------------+
   | RT Brachy Treatment  | Stored only          | Yes                  |
   | Record Storage       |                      |                      |
   +----------------------+----------------------+----------------------+
   | RT Treatment Summary | Stored only          | Yes                  |
   | Record Storage       |                      |                      |
   +----------------------+----------------------+----------------------+
   | Query/Retrieve       |                      |                      |
   +----------------------+----------------------+----------------------+
   | Study Root           | Yes - Hierarchical   | No                   |
   | Information Model    | only                 |                      |
   | FIND                 |                      |                      |
   +----------------------+----------------------+----------------------+
   | Study Root           | Yes - Hierarchical   | No                   |
   | Information Model    | only                 |                      |
   | MOVE                 |                      |                      |
   +----------------------+----------------------+----------------------+

.. table:: Media Services

   +-----------------------------------+-------------------------+-----------------+
   | Media Storage Application Profile | Write Files(FSC or FSU) | Read Files(FSR) |
   +===================================+=========================+=================+
   | Compact Disk - Recordable         |                         |                 |
   +-----------------------------------+-------------------------+-----------------+
   | General Purpose CD-R              | No                      | Yes             |
   +-----------------------------------+-------------------------+-----------------+
   | DVD                               |                         |                 |
   +-----------------------------------+-------------------------+-----------------+
   | General Purpose DVD-RAM           | No                      | Yes             |
   +-----------------------------------+-------------------------+-----------------+

.. _sect_D.2:

Table of Contents
-----------------

A table of contents shall be provided to assist readers in easily
finding the needed information.

.. _sect_D.3:

Introduction
------------

.. _sect_D.3.1:

Revision History
~~~~~~~~~~~~~~~~

.. table:: Revision History

   ================ ================ ====== ======================
   Document Version Date of Issue    Author Description
   ================ ================ ====== ======================
   1.1              October 30, 2003 WG 6   Version for Final Text
   1.2              August 30, 2007  WG 6   Revised Introduction
   ================ ================ ====== ======================

.. _sect_D.3.2:

Audience, Remarks, Terms and Definitions, Basics of DICOM Communication, Abbreviations, References
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

*See example text in*\ `Introduction <#sect_A.3>`__\ *.*

.. _sect_D.3.3:

Additional Remarks for This Example
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This document is a sample DICOM Conformance Statement created for DICOM
. It is to be used solely as an example to illustrate how to create a
DICOM Conformance Statement for a workstation supporting a variety of
types of DICOM images. The subject of the document, SAMPLE DICOM IMAGE
VIEWER, is a fictional product.

.. _sect_D.4:

Networking
----------

.. _sect_D.4.1:

Implementation Model
~~~~~~~~~~~~~~~~~~~~

.. _sect_D.4.1.1:

Application Data Flow
^^^^^^^^^^^^^^^^^^^^^

The application is a single pure Java application that provides both a
user interface, internal database and network listener that spawns
additional threads as necessary to handle incoming connections, as well
as media support.

Conceptually the network services may be modeled as the following
separate AEs, though in fact all the AEs share a single (configurable)
AE Title:

-  ECHO-SCP, which responds to verification requests

-  STORAGE-SCP, which receives incoming images and other composite
   instances

-  STORAGE-SCU, which sends outbound images and other composite
   instances

-  FIND-SCU, which queries remote AEs for lists of studies, series and
   instances

-  MOVE-SCU, which retrieves selected studies, series or instances

.. _sect_D.4.1.2:

Functional Definitions of AEs
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. _sect_D.4.1.2.1:

ECHO-SCP
''''''''

ECHO-SCP waits in the background for connections, will accept
associations with Presentation Contexts for SOP Class of the
Verification Service Class, and will respond successfully to echo
requests.

.. _sect_D.4.1.2.2:

STORAGE-SCP
'''''''''''

STORAGE-SCP waits in the background for connections, will accept
associations with Presentation Contexts for SOP Classes of the Storage
Service Class, and will store the received instances to the local
database where they may subsequently be listed and viewed through the
user interface.

.. _sect_D.4.1.2.3:

STORAGE-SCU
'''''''''''

STORAGE-SCU is activated through the user interface when a user selects
instances from the local database or a DICOMDIR, or the currently
displayed instance, and requests that they be sent to a remote AE
(selected from a pre-configured list).

.. _sect_D.4.1.2.4:

FIND-SCU
''''''''

FIND-SCU is activated through the user interface when a user selects a
remote AE to query (from a pre-configured list), then initiates a query.
Queries are performed recursively from the study through the series and
instance levels until all matching instances have been listed.

.. _sect_D.4.1.2.5:

MOVE-SCU
''''''''

MOVE-SCU is activated through the user interface when a user selects a
study, series or instance for retrieval. A connection to the remote AE
is established to initiate and monitor the retrieval and the STORAGE-SCP
AE receives the retrieved instances.

.. _sect_D.4.1.3:

Sequencing of Real-World Activities
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

All SCP activities are performed asynchronously in the background and
not dependent on any sequencing.

All SCU activities are sequentially initiated in the user interface, and
another activity may not be initiated until the prior activity has
completed.

.. _sect_D.4.2:

AE Specifications
~~~~~~~~~~~~~~~~~

.. _sect_D.4.2.1:

ECHO-SCP
^^^^^^^^

.. _sect_D.4.2.1.1:

SOP Classes
'''''''''''

ECHO-SCP provide Standard Conformance to the following SOP Class(es) :

.. table:: SOP Classes Supported By ECHO-SCP

   ====================== ================= === ===
   SOP Class Name         SOP Class UID     SCU SCP
   ====================== ================= === ===
   Verification SOP Class 1.2.840.10008.1.1 No  Yes
   ====================== ================= === ===

.. _sect_D.4.2.1.2:

Association Policies
''''''''''''''''''''

.. _sect_D.4.2.1.2.1:

General
       

ECHO-SCP accepts but never initiates associations.

.. table:: Maximum PDU Size Received as a SCP for ECHO-SCP

   ========================= =========
   Maximum PDU size received Unlimited
   ========================= =========

.. _sect_D.4.2.1.2.2:

Number of Associations
                      

.. table:: Number of Associations as a SCP for ECHO-SCP

   =========================================== =========
   Maximum number of simultaneous associations Unlimited
   =========================================== =========

.. _sect_D.4.2.1.2.3:

Asynchronous Nature
                   

ECHO-SCP will only allow a single outstanding operation on an
Association. Therefore, ECHO-SCP will not perform asynchronous
operations window negotiation.

.. _sect_D.4.2.1.2.4:

Implementation Identifying Information
                                      

.. table:: DICOM Implementation Class and Version for ECHO-SCP

   =========================== =============================
   Implementation Class UID    xxxxxxxxxxx.yy.etc.ad.inf.usw
   Implementation Version Name Viewer1.0
   =========================== =============================

.. _sect_D.4.2.1.3:

Association Initiation Policy
'''''''''''''''''''''''''''''

ECHO-SCP does not initiate associations.

.. _sect_D.4.2.1.4:

Association Acceptance Policy
'''''''''''''''''''''''''''''

When ECHO-SCP accepts an association, it will respond to echo requests.
If the Called AE Title does not match the pre-configured AE Title shared
by all the SCPs of the application, the association will be rejected.

.. _sect_D.4.2.1.4.1:

Activity- Receive Echo Request
                              

.. _sect_D.4.2.1.4.1.1:

Description and Sequencing of Activities
                                        

.. _sect_D.4.2.1.4.1.2:

Accepted Presentation Contexts
                              

.. table:: Acceptable Presentation Contexts for ECHO-SCP and Receive
Echo Request

   +------------+------------+------------+------------+-----+------+
   | Pr         |            |            |            |     |      |
   | esentation |            |            |            |     |      |
   | Context    |            |            |            |     |      |
   | Table      |            |            |            |     |      |
   +============+============+============+============+=====+======+
   | Ve         | 1.2.840    | Implicit   | 1.2.840    | SCP | None |
   | rification | .10008.1.1 | VR Little  | .10008.1.2 |     |      |
   |            |            | Endian     |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | Explicit   | 1.2.840.1  |            |            |     |      |
   | VR Little  | 0008.1.2.1 |            |            |     |      |
   | Endian     |            |            |            |     |      |
   +------------+------------+------------+------------+-----+------+

.. _sect_D.4.2.1.4.1.2.1:

Extended Negotiation
                    

No extended negotiation is performed.

.. _sect_D.4.2.1.4.1.3:

SOP Specific Conformance
                        

.. _sect_D.4.2.1.4.1.3.1:

SOP Specific Conformance to Verification SOP Class
                                                  

ECHO-SCP provides standard conformance to the Verification Service
Class.

.. _sect_D.4.2.1.4.1.3.2:

Presentation Context Acceptance Criterion
                                         

ECHO-SCP will always accept any Presentation Context for the supported
SOP Classes with the supported Transfer Syntaxes. More than one proposed
Presentation Context will be accepted for the same Abstract Syntax if
the Transfer Syntax is supported, whether or not it is the same as
another Presentation Context.

.. _sect_D.4.2.1.4.1.3.3:

Transfer Syntax Selection Policies
                                  

ECHO-SCP prefers explicit Transfer Syntaxes. If offered a choice of
Transfer Syntaxes in a Presentation Context, it will apply the following
priority to the choice of Transfer Syntax:

a. first encountered explicit Transfer Syntax,

b. default Transfer Syntax.

ECHO-SCP will accept duplicate Presentation Contexts, that is, if it is
offered multiple Presentation Contexts, each of which offers acceptable
Transfer Syntaxes, it will accept all Presentation Contexts, applying
the same priority for selecting a Transfer Syntax for each.

.. _sect_D.4.2.2:

STORAGE-SCP
^^^^^^^^^^^

.. _sect_D.4.2.2.1:

SOP Classes
'''''''''''

STORAGE-SCP provide Standard Conformance to the following SOP Class(es)
:

.. table:: SOP Classes Supported By STORAGE-SCP

   +---------------------------+---------------------------+-----+-----+
   | SOP Class Name            | SOP Class UID             | SCU | SCP |
   +===========================+===========================+=====+=====+
   | Stored Print Storage      | 1.2.840.10008.5.1.1.27    | No  | Yes |
   +---------------------------+---------------------------+-----+-----+
   | Hardcopy Grayscale Image  | 1.2.840.10008.5.1.1.29    | No  | Yes |
   | Storage                   |                           |     |     |
   +---------------------------+---------------------------+-----+-----+
   | Hardcopy Color Image      | 1.2.840.10008.5.1.1.30    | No  | Yes |
   | Storage                   |                           |     |     |
   +---------------------------+---------------------------+-----+-----+
   | Computed Radiography      | 1.2.840.10008.5.1.4.1.1.1 | No  | Yes |
   | Image Storage             |                           |     |     |
   +---------------------------+---------------------------+-----+-----+
   | Digital X-Ray Image       | 1.                        | No  | Yes |
   | Storage - For             | 2.840.10008.5.1.4.1.1.1.1 |     |     |
   | Presentation              |                           |     |     |
   +---------------------------+---------------------------+-----+-----+
   | Digital X-Ray Image       | 1.2.                      | No  | Yes |
   | Storage - For Processing  | 840.10008.5.1.4.1.1.1.1.1 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | Digital Mammography X-Ray | 1.                        | No  | Yes |
   | Image Storage - For       | 2.840.10008.5.1.4.1.1.1.2 |     |     |
   | Presentation              |                           |     |     |
   +---------------------------+---------------------------+-----+-----+
   | Digital Mammography X-Ray | 1.2.                      | No  | Yes |
   | Image Storage - For       | 840.10008.5.1.4.1.1.1.2.1 |     |     |
   | Processing                |                           |     |     |
   +---------------------------+---------------------------+-----+-----+
   | Digital Intra-oral X-Ray  | 1.                        | No  | Yes |
   | Image Storage - For       | 2.840.10008.5.1.4.1.1.1.3 |     |     |
   | Presentation              |                           |     |     |
   +---------------------------+---------------------------+-----+-----+
   | Digital Intra-oral X-Ray  | 1.2.                      | No  | Yes |
   | Image Storage - For       | 840.10008.5.1.4.1.1.1.3.1 |     |     |
   | Processing                |                           |     |     |
   +---------------------------+---------------------------+-----+-----+
   | CT Image Storage          | 1.2.840.10008.5.1.4.1.1.2 | No  | Yes |
   +---------------------------+---------------------------+-----+-----+
   | Ultrasound Multi-frame    | 1.2.840.10008.5.1.4.1.1.3 | No  | Yes |
   | Image Storage (Retired)   |                           |     |     |
   +---------------------------+---------------------------+-----+-----+
   | Ultrasound Multi-frame    | 1.                        | No  | Yes |
   | Image Storage             | 2.840.10008.5.1.4.1.1.3.1 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | MR Image Storage          | 1.2.840.10008.5.1.4.1.1.4 | No  | Yes |
   +---------------------------+---------------------------+-----+-----+
   | Enhanced MR Image Storage | 1.                        | No  | Yes |
   |                           | 2.840.10008.5.1.4.1.1.4.1 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | MR Spectroscopy Storage   | 1.                        | No  | Yes |
   |                           | 2.840.10008.5.1.4.1.1.4.2 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | Standalone Modality LUT   | 1                         | No  | Yes |
   | Storage                   | .2.840.10008.5.1.4.1.1.10 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | Standalone VOI LUT        | 1                         | No  | Yes |
   | Storage                   | .2.840.10008.5.1.4.1.1.11 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | Grayscale Softcopy        | 1.2                       | No  | Yes |
   | Presentation State        | .840.10008.5.1.4.1.1.11.1 |     |     |
   | Storage                   |                           |     |     |
   +---------------------------+---------------------------+-----+-----+
   | X-Ray Angiographic Image  | 1.2                       | No  | Yes |
   | Storage                   | .840.10008.5.1.4.1.1.12.1 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | X-Ray Radiofluoroscopic   | 1.2                       | No  | Yes |
   | Image Storage             | .840.10008.5.1.4.1.1.12.2 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | X-Ray Angiographic        | 1.2                       | No  | Yes |
   | Bi-Plane Image Storage    | .840.10008.5.1.4.1.1.12.3 |     |     |
   | (Retired)                 |                           |     |     |
   +---------------------------+---------------------------+-----+-----+
   | Nuclear Medicine Image    | 1                         | No  | Yes |
   | Storage                   | .2.840.10008.5.1.4.1.1.20 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | Raw Data Storage          | 1                         | No  | Yes |
   |                           | .2.840.10008.5.1.4.1.1.66 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | VL Image Storage          | 1.2                       | No  | Yes |
   | (Retired)                 | .840.10008.5.1.4.1.1.77.1 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | VL Multi-frame Image      | 1.2                       | No  | Yes |
   | Storage (Retired)         | .840.10008.5.1.4.1.1.77.2 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | VL Endoscopic Image       | 1.2.8                     | No  | Yes |
   | Storage                   | 40.10008.5.1.4.1.1.77.1.1 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | VL Microscopic Image      | 1.2.8                     | No  | Yes |
   | Storage                   | 40.10008.5.1.4.1.1.77.1.2 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | VL Slide-Coordinates      | 1.2.8                     | No  | Yes |
   | Microscopic Image Storage | 40.10008.5.1.4.1.1.77.1.3 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | VL Photographic Image     | 1.2.8                     | No  | Yes |
   | Storage                   | 40.10008.5.1.4.1.1.77.1.4 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | Basic Text SR             | 1.2.                      | No  | Yes |
   |                           | 840.10008.5.1.4.1.1.88.11 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | Enhanced SR               | 1.2.                      | No  | Yes |
   |                           | 840.10008.5.1.4.1.1.88.22 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | Comprehensive SR          | 1.2.                      | No  | Yes |
   |                           | 840.10008.5.1.4.1.1.88.33 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | Mammography CAD SR        | 1.2.                      | No  | Yes |
   |                           | 840.10008.5.1.4.1.1.88.50 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | Key Object Selection      | 1.2.                      | No  | Yes |
   | Document                  | 840.10008.5.1.4.1.1.88.59 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | Positron Emission         | 1.                        | No  | Yes |
   | Tomography Image Storage  | 2.840.10008.5.1.4.1.1.128 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | Standalone PET Curve      | 1.                        | No  | Yes |
   | Storage                   | 2.840.10008.5.1.4.1.1.129 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | RT Image Storage          | 1.2.                      | No  | Yes |
   |                           | 840.10008.5.1.4.1.1.481.1 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | RT Dose Storage           | 1.2.                      | No  | Yes |
   |                           | 840.10008.5.1.4.1.1.481.2 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | RT Structure Set Storage  | 1.2.                      | No  | Yes |
   |                           | 840.10008.5.1.4.1.1.481.3 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | RT Beams Treatment Record | 1.2.                      | No  | Yes |
   | Storage                   | 840.10008.5.1.4.1.1.481.4 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | RT Plan Storage           | 1.2.                      | No  | Yes |
   |                           | 840.10008.5.1.4.1.1.481.5 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | RT Brachy Treatment       | 1.2.                      | No  | Yes |
   | Record Storage            | 840.10008.5.1.4.1.1.481.6 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | RT Treatment Summary      | 1.2.                      | No  | Yes |
   | Record Storage            | 840.10008.5.1.4.1.1.481.7 |     |     |
   +---------------------------+---------------------------+-----+-----+

.. _sect_D.4.2.2.2:

Association Policies
''''''''''''''''''''

.. _sect_D.4.2.2.2.1:

General
       

STORAGE-SCP accepts but never initiates associations.

.. table:: Maximum PDU Size Received as a SCP for STORAGE-SCP

   ========================= =========
   Maximum PDU size received Unlimited
   ========================= =========

.. _sect_D.4.2.2.2.2:

Number of Associations
                      

.. table:: Number of Associations as a SCP for STORAGE-SCP

   =========================================== =========
   Maximum number of simultaneous associations Unlimited
   =========================================== =========

.. _sect_D.4.2.2.2.3:

Asynchronous Nature
                   

STORAGE-SCP will only allow a single outstanding operation on an
Association. Therefore, STORAGE-SCP will not perform asynchronous
operations window negotiation.

.. _sect_D.4.2.2.2.4:

Implementation Identifying Information
                                      

.. table:: DICOM Implementation Class and Version for STORAGE-SCP

   =========================== =============================
   Implementation Class UID    xxxxxxxxxxx.yy.etc.ad.inf.usw
   Implementation Version Name Viewer1.0
   =========================== =============================

.. _sect_D.4.2.2.3:

Association Initiation Policy
'''''''''''''''''''''''''''''

STORAGE-SCP does not initiate associations.

.. _sect_D.4.2.2.4:

Association Acceptance Policy
'''''''''''''''''''''''''''''

When STORAGE-SCP accepts an association, it will respond to storage
requests. If the Called AE Title does not match the pre-configured AE
Title shared by all the SCPs of the application, the association will be
rejected.

.. _sect_D.4.2.2.4.1:

Activity - Receive Storage Request
                                  

.. _sect_D.4.2.2.4.1.1:

Description and Sequencing of Activities
                                        

As instances are received they are copied to the local file system and a
record inserted into the local database. If the received instance is a
duplicate of a previously received instance, the old file and database
record will be overwritten with the new one.

.. _sect_D.4.2.2.4.1.2:

Accepted Presentation Contexts
                              

.. table:: Acceptable Presentation Contexts for STORAGE-SCP and Receive
Storage Request

   +------------+------------+------------+------------+-----+------+
   | Pr         |            |            |            |     |      |
   | esentation |            |            |            |     |      |
   | Context    |            |            |            |     |      |
   | Table      |            |            |            |     |      |
   +============+============+============+============+=====+======+
   | See        | See        | Implicit   | 1.2.840    | SCP | None |
   | `t         | `t         | VR Little  | .10008.1.2 |     |      |
   | able_title | able_title | Endian     |            |     |      |
   |  <#table_D |  <#table_D |            |            |     |      |
   | .4.2-6>`__ | .4.2-6>`__ |            |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | Explicit   | 1.2.840.1  |            |            |     |      |
   | VR Little  | 0008.1.2.1 |            |            |     |      |
   | Endian     |            |            |            |     |      |
   +------------+------------+------------+------------+-----+------+

.. _sect_D.4.2.2.4.1.2.1:

Extended Negotiation
                    

No extended negotiation is performed, though STORAGE-SCP:

-  is a Level 2 Storage SCP (Full - does not discard any data elements)

-  does not support digital signatures

-  does not coerce any received data elements

.. _sect_D.4.2.2.4.1.3:

SOP Specific Conformance
                        

.. _sect_D.4.2.2.4.1.3.1:

SOP Specific Conformance to Storage SOP Classes
                                               

STORAGE-SCP provides standard conformance to the Storage Service Class.

When displaying an image in the viewing application, the newest
Grayscale Softcopy Presentation State containing references to the image
will be automatically applied and the GSPS Presentation Label and
Presentation description will be displayed. The user has the option to
select any other Presentation States that also references the image. If
no Presentation State references the image then no Presentation State
will be applied by default.

The Mask Subtraction transformation is not supported by this
implementation. It is not possible display Presentation States
containing the Mask Subtraction Sequence (0028,6100).

All of the Image Storage SOP Classes listed in
`table_title <#table_D.4.2-6>`__ are supported as references from
instances of the Grayscale Softcopy Presentation State Storage SOP
Class.

.. _sect_D.4.2.2.4.1.3.2:

Presentation Context Acceptance Criterion
                                         

STORAGE-SCP will always accept any Presentation Context for the
supported SOP Classes with the supported Transfer Syntaxes. More than
one proposed Presentation Context will be accepted for the same Abstract
Syntax if the Transfer Syntax is supported, whether or not it is the
same as another Presentation Context.

.. _sect_D.4.2.2.4.1.3.3:

Transfer Syntax Selection Policies
                                  

STORAGE-SCP prefers explicit Transfer Syntaxes. If offered a choice of
Transfer Syntaxes in a Presentation Context, it will apply the following
priority to the choice of Transfer Syntax:

a. first encountered explicit Transfer Syntax,

b. default Transfer Syntax.

STORAGE-SCP will accept duplicate Presentation Contexts, that is, if it
is offered multiple Presentation Contexts, each of which offers
acceptable Transfer Syntaxes, it will accept all Presentation Contexts,
applying the same priority for selecting a Transfer Syntax for each.

.. _sect_D.4.2.2.4.1.3.4:

Response Status
               

STORAGE-SCP will behave as described in the Table below when generating
the C-STORE response command message.

.. table:: Response Status for STORAGE-SCP and Receive Storage Request

   +----------------+----------------+--------------+----------------+
   | Service Status | Further        | Status Codes | Reason         |
   |                | Meaning        |              |                |
   +================+================+==============+================+
   | Refused        | Out of         | A7xx         | Never sent     |
   |                | Resources      |              |                |
   +----------------+----------------+--------------+----------------+
   | Error          | Data Set does  | A9xx         | Never sent -   |
   |                | not match SOP  |              | Data Set is    |
   |                | Class          |              | not checked    |
   |                |                |              | prior to       |
   |                |                |              | storage        |
   +----------------+----------------+--------------+----------------+
   |                | Cannot         | Cxxx         | Never sent     |
   |                | understand     |              |                |
   +----------------+----------------+--------------+----------------+
   | Warning        | Coercion of    | B000         | Never sent -   |
   |                | Data Elements  |              | no coercion is |
   |                |                |              | ever performed |
   +----------------+----------------+--------------+----------------+
   |                | Data Set does  | B007         | Never sent -   |
   |                | not match SOP  |              | Data Set is    |
   |                | Class          |              | not checked    |
   |                |                |              | prior to       |
   |                |                |              | storage        |
   +----------------+----------------+--------------+----------------+
   |                | Elements       | B006         | Never sent -   |
   |                | Discarded      |              | all elements   |
   |                |                |              | are always     |
   |                |                |              | stored         |
   +----------------+----------------+--------------+----------------+
   | Success        |                | 0000         |                |
   +----------------+----------------+--------------+----------------+

.. _sect_D.4.2.3:

STORAGE-SCU
^^^^^^^^^^^

.. _sect_D.4.2.3.1:

SOP Classes
'''''''''''

STORAGE-SCU provide Standard Conformance to the following SOP Class(es)
:

.. table:: SOP Classes Supported By STORAGE-SCU

   +---------------------------+---------------------------+-----+-----+
   | SOP Class Name            | SOP Class UID             | SCU | SCP |
   +===========================+===========================+=====+=====+
   | Stored Print Storage      | 1.2.840.10008.5.1.1.27    | Yes | No  |
   +---------------------------+---------------------------+-----+-----+
   | Hardcopy Grayscale Image  | 1.2.840.10008.5.1.1.29    | Yes | No  |
   | Storage                   |                           |     |     |
   +---------------------------+---------------------------+-----+-----+
   | Hardcopy Color Image      | 1.2.840.10008.5.1.1.30    | Yes | No  |
   | Storage                   |                           |     |     |
   +---------------------------+---------------------------+-----+-----+
   | Computed Radiography      | 1.2.840.10008.5.1.4.1.1.1 | Yes | No  |
   | Image Storage             |                           |     |     |
   +---------------------------+---------------------------+-----+-----+
   | Digital X-Ray Image       | 1.                        | Yes | No  |
   | Storage - For             | 2.840.10008.5.1.4.1.1.1.1 |     |     |
   | Presentation              |                           |     |     |
   +---------------------------+---------------------------+-----+-----+
   | Digital X-Ray Image       | 1.2.                      | Yes | No  |
   | Storage - For Processing  | 840.10008.5.1.4.1.1.1.1.1 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | Digital Mammography X-Ray | 1.                        | Yes | No  |
   | Image Storage - For       | 2.840.10008.5.1.4.1.1.1.2 |     |     |
   | Presentation              |                           |     |     |
   +---------------------------+---------------------------+-----+-----+
   | Digital Mammography X-Ray | 1.2.                      | Yes | No  |
   | Image Storage - For       | 840.10008.5.1.4.1.1.1.2.1 |     |     |
   | Processing                |                           |     |     |
   +---------------------------+---------------------------+-----+-----+
   | Digital Intra-oral X-Ray  | 1.                        | Yes | No  |
   | Image Storage - For       | 2.840.10008.5.1.4.1.1.1.3 |     |     |
   | Presentation              |                           |     |     |
   +---------------------------+---------------------------+-----+-----+
   | Digital Intra-oral X-Ray  | 1.2.                      | Yes | No  |
   | Image Storage - For       | 840.10008.5.1.4.1.1.1.3.1 |     |     |
   | Processing                |                           |     |     |
   +---------------------------+---------------------------+-----+-----+
   | CT Image Storage          | 1.2.840.10008.5.1.4.1.1.2 | Yes | No  |
   +---------------------------+---------------------------+-----+-----+
   | Ultrasound Multi-frame    | 1.2.840.10008.5.1.4.1.1.3 | Yes | No  |
   | Image Storage (Retired)   |                           |     |     |
   +---------------------------+---------------------------+-----+-----+
   | Ultrasound Multi-frame    | 1.                        | Yes | No  |
   | Image Storage             | 2.840.10008.5.1.4.1.1.3.1 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | MR Image Storage          | 1.2.840.10008.5.1.4.1.1.4 | Yes | No  |
   +---------------------------+---------------------------+-----+-----+
   | Enhanced MR Image Storage | 1.                        | Yes | No  |
   |                           | 2.840.10008.5.1.4.1.1.4.1 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | MR Spectroscopy Storage   | 1.                        | Yes | No  |
   |                           | 2.840.10008.5.1.4.1.1.4.2 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | Standalone Modality LUT   | 1                         | Yes | No  |
   | Storage                   | .2.840.10008.5.1.4.1.1.10 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | Standalone VOI LUT        | 1                         | Yes | No  |
   | Storage                   | .2.840.10008.5.1.4.1.1.11 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | Grayscale Softcopy        | 1.2                       | Yes | No  |
   | Presentation State        | .840.10008.5.1.4.1.1.11.1 |     |     |
   | Storage                   |                           |     |     |
   +---------------------------+---------------------------+-----+-----+
   | X-Ray Angiographic Image  | 1.2                       | Yes | No  |
   | Storage                   | .840.10008.5.1.4.1.1.12.1 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | X-Ray Radiofluoroscopic   | 1.2                       | Yes | No  |
   | Image Storage             | .840.10008.5.1.4.1.1.12.2 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | X-Ray Angiographic        | 1.2                       | Yes | No  |
   | Bi-Plane Image Storage    | .840.10008.5.1.4.1.1.12.3 |     |     |
   | (Retired)                 |                           |     |     |
   +---------------------------+---------------------------+-----+-----+
   | Nuclear Medicine Image    | 1                         | Yes | No  |
   | Storage                   | .2.840.10008.5.1.4.1.1.20 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | Raw Data Storage          | 1                         | Yes | No  |
   |                           | .2.840.10008.5.1.4.1.1.66 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | VL Image Storage          | 1.2                       | Yes | No  |
   | (Retired)                 | .840.10008.5.1.4.1.1.77.1 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | VL Multi-frame Image      | 1.2                       | Yes | No  |
   | Storage (Retired)         | .840.10008.5.1.4.1.1.77.2 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | VL Endoscopic Image       | 1.2.8                     | Yes | No  |
   | Storage                   | 40.10008.5.1.4.1.1.77.1.1 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | VL Microscopic Image      | 1.2.8                     | Yes | No  |
   | Storage                   | 40.10008.5.1.4.1.1.77.1.2 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | VL Slide-Coordinates      | 1.2.8                     | Yes | No  |
   | Microscopic Image Storage | 40.10008.5.1.4.1.1.77.1.3 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | VL Photographic Image     | 1.2.8                     | Yes | No  |
   | Storage                   | 40.10008.5.1.4.1.1.77.1.4 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | Basic Text SR             | 1.2.                      | Yes | No  |
   |                           | 840.10008.5.1.4.1.1.88.11 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | Enhanced SR               | 1.2.                      | Yes | No  |
   |                           | 840.10008.5.1.4.1.1.88.22 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | Comprehensive SR          | 1.2.                      | Yes | No  |
   |                           | 840.10008.5.1.4.1.1.88.33 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | Mammography CAD SR        | 1.2.                      | Yes | No  |
   |                           | 840.10008.5.1.4.1.1.88.50 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | Key Object Selection      | 1.2.                      | Yes | No  |
   | Document                  | 840.10008.5.1.4.1.1.88.59 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | Positron Emission         | 1.                        | Yes | No  |
   | Tomography Image Storage  | 2.840.10008.5.1.4.1.1.128 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | Standalone PET Curve      | 1.                        | Yes | No  |
   | Storage                   | 2.840.10008.5.1.4.1.1.129 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | RT Image Storage          | 1.2.                      | Yes | No  |
   |                           | 840.10008.5.1.4.1.1.481.1 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | RT Dose Storage           | 1.2.                      | Yes | No  |
   |                           | 840.10008.5.1.4.1.1.481.2 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | RT Structure Set Storage  | 1.2.                      | Yes | No  |
   |                           | 840.10008.5.1.4.1.1.481.3 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | RT Beams Treatment Record | 1.2.                      | Yes | No  |
   | Storage                   | 840.10008.5.1.4.1.1.481.4 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | RT Plan Storage           | 1.2.                      | Yes | No  |
   |                           | 840.10008.5.1.4.1.1.481.5 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | RT Brachy Treatment       | 1.2.                      | Yes | No  |
   | Record Storage            | 840.10008.5.1.4.1.1.481.6 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | RT Treatment Summary      | 1.2.                      | Yes | No  |
   | Record Storage            | 840.10008.5.1.4.1.1.481.7 |     |     |
   +---------------------------+---------------------------+-----+-----+

.. _sect_D.4.2.3.2:

Association Policies
''''''''''''''''''''

.. _sect_D.4.2.3.2.1:

General
       

STORAGE-SCU initiates but never accepts associations.

.. table:: Maximum PDU Size Received as a SCP for STORAGE-SCU

   ========================= =========
   Maximum PDU size received Unlimited
   ========================= =========

.. _sect_D.4.2.3.2.2:

Number of Associations
                      

.. table:: Number of Associations as a SCP for STORAGE-SCU

   =========================================== =
   Maximum number of simultaneous associations 1
   =========================================== =

.. _sect_D.4.2.3.2.3:

Asynchronous Nature
                   

STORAGE-SCU will only allow a single outstanding operation on an
Association. Therefore, STORAGE-SCU will not perform asynchronous
operations window negotiation.

.. _sect_D.4.2.3.2.4:

Implementation Identifying Information
                                      

.. table:: DICOM Implementation Class and Version for STORAGE-SCU

   =========================== =============================
   Implementation Class UID    xxxxxxxxxxx.yy.etc.ad.inf.usw
   Implementation Version Name Viewer1.0
   =========================== =============================

.. _sect_D.4.2.3.3:

Association Initiation Policy
'''''''''''''''''''''''''''''

STORAGE-SCU attempts to initiate a new association for each instance it
attempts to transfer.

.. _sect_D.4.2.3.3.1:

Activity - Send Storage Request
                               

.. _sect_D.4.2.3.3.1.1:

Description and Sequencing of Activities
                                        

For each instance selected from the user interface to be transferred, a
single attempt will be made to transmit it to the selected remote AE. If
the send fails, for whatever reason, no retry will be performed, and an
attempt will be made to send the next instance.

.. _sect_D.4.2.3.3.1.2:

Proposed Presentation Contexts
                              

.. table:: Proposed Presentation Contexts for STORAGE-SCU and Receive
Storage Request

   +------------+------------+------------+------------+-----+------+
   | Pr         |            |            |            |     |      |
   | esentation |            |            |            |     |      |
   | Context    |            |            |            |     |      |
   | Table      |            |            |            |     |      |
   +============+============+============+============+=====+======+
   | See        | See        | Implicit   | 1.2.840    | SCU | None |
   | `ta        | `ta        | VR Little  | .10008.1.2 |     |      |
   | ble_title  | ble_title  | Endian     |            |     |      |
   | <#table_D. | <#table_D. |            |            |     |      |
   | 4.2-12>`__ | 4.2-12>`__ |            |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | Explicit   | 1.2.840.1  |            |            |     |      |
   | VR Little  | 0008.1.2.1 |            |            |     |      |
   | Endian     |            |            |            |     |      |
   +------------+------------+------------+------------+-----+------+

STORAGE-SCU will propose Presentation Contexts only for the SOP Class of
the instance that is to be transferred.

For that SOP Class, STORAGE-SCU will propose multiple Presentation
Contexts, one for each of the supported Transfer Syntaxes, and an
additional Presentation Context with all of the supported Transfer
Syntaxes, in order to determine which Transfer Syntaxes the remote SCP
supports, and which it prefers.

.. _sect_D.4.2.3.3.1.2.1:

Extended Negotiation
                    

No extended negotiation is performed.

.. _sect_D.4.2.3.3.1.3:

SOP Specific Conformance
                        

.. _sect_D.4.2.3.3.1.3.1:

SOP Specific Conformance to Storage SOP Classes
                                               

STORAGE-SCU provides standard conformance to the Storage Service Class.

.. _sect_D.4.2.3.3.1.3.2:

Presentation Context Acceptance Criterion
                                         

STORAGE-SCU does not accept associations.

.. _sect_D.4.2.3.3.1.3.3:

Transfer Syntax Selection Policies
                                  

STORAGE-SCU prefers explicit Transfer Syntaxes. If offered a choice of
Transfer Syntaxes in the accepted Presentation Contexts, it will apply
the following priority to the choice of Presentation Context to use for
the C-STORE operation:

a. first encountered explicit Transfer Syntax,

b. default Transfer Syntax.

.. _sect_D.4.2.3.3.1.3.4:

Response Status
               

STORAGE-SCU will behave as described in the Table below in response to
the status returned in the C-STORE response command message.

.. table:: Response Status for STORAGE-SCU and Receive Storage Request

   ============== ================================= ============ ========
   Service Status Further Meaning                   Status Codes Behavior
   ============== ================================= ============ ========
   Refused        Out of Resources                  A7xx         Ignored
   Error          Data Set does not match SOP Class A9xx         Ignored
   \              Cannot understand                 Cxxx         Ignored
   Warning        Coercion of Data Elements         B000         Ignored
   \              Data Set does not match SOP Class B007         Ignored
   \              Elements Discarded                B006         Ignored
   Success                                          0000         Ignored
   ============== ================================= ============ ========

.. _sect_D.4.2.3.4:

Association Acceptance Policy
'''''''''''''''''''''''''''''

STORAGE-SCU does not accept associations.

.. _sect_D.4.2.4:

FIND-SCU
^^^^^^^^

.. _sect_D.4.2.4.1:

SOP Classes
'''''''''''

FIND-SCU provide Standard Conformance to the following SOP Class(es) :

.. table:: SOP Classes Supported By FIND-SCU

   +---------------------------+---------------------------+-----+-----+
   | SOP Class Name            | SOP Class UID             | SCU | SCP |
   +===========================+===========================+=====+=====+
   | Study Root Query/Retrieve | 1.                        | Yes | No  |
   | Information Model - FIND  | 2.840.10008.5.1.4.1.2.2.1 |     |     |
   +---------------------------+---------------------------+-----+-----+

.. _sect_D.4.2.4.2:

Association Policies
''''''''''''''''''''

.. _sect_D.4.2.4.2.1:

General
       

FIND-SCU initiates but never accepts associations.

.. table:: Maximum PDU Size Received as a SCP for FIND-SCU

   ========================= =========
   Maximum PDU size received Unlimited
   ========================= =========

.. _sect_D.4.2.4.2.2:

Number of Associations
                      

.. table:: Number of Associations as a SCP for FIND-SCU

   =========================================== =
   Maximum number of simultaneous associations 1
   =========================================== =

.. _sect_D.4.2.4.2.3:

Asynchronous Nature
                   

FIND-SCU will only allow a single outstanding operation on an
Association. Therefore, FIND-SCU will not perform asynchronous
operations window negotiation.

.. _sect_D.4.2.4.2.4:

Implementation Identifying Information
                                      

.. table:: DICOM Implementation Class and Version for FIND-SCU

   =========================== =============================
   Implementation Class UID    xxxxxxxxxxx.yy.etc.ad.inf.usw
   Implementation Version Name Viewer1.0
   =========================== =============================

.. _sect_D.4.2.4.3:

Association Initiation Policy
'''''''''''''''''''''''''''''

FIND-SCU attempts to initiate a new association when the user performs
the query action from the user interface. If this involves recursive
queries for lower query levels in the hierarchy, these will be performed
on the same association.

.. _sect_D.4.2.4.3.1:

Activity - Query Remote AE
                          

.. _sect_D.4.2.4.3.1.1:

Description and Sequencing of Activities
                                        

A single attempt will be made to query the remote AE. If the query
fails, for whatever reason, no retry will be performed.

.. _sect_D.4.2.4.3.1.2:

Proposed Presentation Contexts
                              

.. table:: Proposed Presentation Contexts for FIND-SCU and Query Remote
AE

   +------------+------------+------------+------------+-----+------+
   | Pr         |            |            |            |     |      |
   | esentation |            |            |            |     |      |
   | Context    |            |            |            |     |      |
   | Table      |            |            |            |     |      |
   +============+============+============+============+=====+======+
   | See        | See        | Implicit   | 1.2.840    | SCU | None |
   | `ta        | `ta        | VR Little  | .10008.1.2 |     |      |
   | ble_title  | ble_title  | Endian     |            |     |      |
   | <#table_D. | <#table_D. |            |            |     |      |
   | 4.2-18>`__ | 4.2-18>`__ |            |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | Explicit   | 1.2.840.1  |            |            |     |      |
   | VR Little  | 0008.1.2.1 |            |            |     |      |
   | Endian     |            |            |            |     |      |
   +------------+------------+------------+------------+-----+------+

FIND-SCU will propose multiple Presentation Contexts, one for each of
the supported Transfer Syntaxes, and an additional Presentation Context
with all of the supported Transfer Syntaxes, in order to determine which
Transfer Syntaxes the remote SCP supports, and which it prefers.

.. _sect_D.4.2.4.3.1.2.1:

Extended Negotiation
                    

No extended negotiation is performed.

In particular, relational queries are not supported.

.. _sect_D.4.2.4.3.1.3:

SOP Specific Conformance
                        

.. _sect_D.4.2.4.3.1.3.1:

SOP Specific Conformance to C-FIND SOP Classes
                                              

FIND-SCU provides standard conformance to the supported C-FIND SOP
Classes.

Only a single information model, Study Root, is supported.

All queries are initiated at the highest level of the information model
(the STUDY level), and then for each response received, recursively
repeated at the next lower levels (the SERIES and then IMAGE levels), in
order to completely elucidate the "tree" of instances available on the
remote AE (from which the user may subsequently request a retrieval at
any level).

No CANCEL requests are ever issued.

Unexpected attributes returned in a C-FIND response (those not
requested) are listed in the browser at the appropriate level if present
in the dictionary. Requested return attributes not returned by the SCP
are ignored. Non-matching responses returned by the SCP due to
unsupported (hopefully optional) matching keys are not filtered locally
by the FIND-SCU and thus will still be presented in the browser. No
attempt is made to filter out duplicate responses.

Specific Character Set will always be included at every query level. If
present in the response, Specific Character Set will be used to identify
character sets other than the default character set for display of
strings in the browser.

.. table:: Study Root Request Identifier for FIND-SCU

   ================================== =========== =================
   Name                               Tag         Types of Matching
   ================================== =========== =================
   STUDY Level                                    
   Patient's ID                       (0010,0020) S,*,U
   Patient's Name                     (0010,0010) S,*,U
   Patient's Birth Date               (0010,0030) S,*,U,R
   Patient's Sex                      (0010,0040) S,*,U
   Patient's Birth Time               (0010,0032) S,*,U,R
   Other Patient's ID's               (0010,1000) S,*,U
   Other Patient's Names              (0010,1001) S,*,U
   Ethnic Group                       (0010,2160) S,*,U
   Patient Comments                   (0010,4000) S,*,U
   Study ID                           (0020,0010) S,*,U
   Study Description                  (0008,1030) S,*,U
   Modalities In Study                (0008,0061) S,*,U
   Study Date                         (0008,0020) S,*,U,R
   Study Time                         (0008,0030) S,*,U,R
   Referring Physician's Name         (0008,0090) S,*,U
   Accession Number                   (0008,0050) S,*,U
   Physician of Record                (0008,1048) S,*,U
   Name of Physician(s) Reading Study (0008,1060) S,*,U
   Admitting Diagnoses Description    (0008,1080) S,*,U
   Patient's Age                      (0010,1010) S,*,U
   Patient's Size                     (0010,1020) S,*,U
   Patient's Weight                   (0010,1030) S,*,U
   Occupation                         (0010,2180) S,*,U
   Additional Patient History         (0010,21B0) S,*,U
   Study Instance UID                 (0020,000D) UNIQUE
   SERIES Level                                   
   Series Number                      (0020,0011) S,*,U
   Series Description                 (0008,103E) S,*,U
   Modality                           (0008,0060) S,*,U
   Series Date                        (0008,0021) S,*,U
   Series Time                        (0008,0031) S,*,U
   Performing Physician's Name        (0008,1050) S,*,U
   Protocol Name                      (0018,1030) S,*,U
   Operator's Name                    (0008,1070) S,*,U
   Laterality                         (0020,0060) S,*,U
   Body Part Examined                 (0018,0015) S,*,U
   Manufacturer                       (0008,0070) S,*,U
   Manufacturer's Model Name          (0008,1090) S,*,U
   Station Name                       (0008,1010) S,*,U
   Institution Name                   (0008,0080) S,*,U
   Institutional Department Name      (0008,1040) S,*,U
   Series Instance UID                (0020,000E) UNIQUE
   IMAGE Level                                    
   Instance Number                    (0020,0013) S,*,U
   Image Comments                     (0020,4000) S,*,U
   Content Date                       (0008,0023) S,*,U,R
   Content Time                       (0008,0033) S,*,U,R
   Image Type                         (0008,0008) S,*,U
   Acquisition Number                 (0020,0012) S,*,U
   Acquisition Date                   (0008,0022) S,*,U,R
   Acquisition Time                   (0008,0032) S,*,U,R
   Acquisition Date Time              (0008,002A) S,*,U,R
   Derivation Description             (0008,2111) S,*,U
   Contrast/Bolus Agent               (0018,0010) S,*,U
   Quality Control Image              (0028,0300) S,*,U
   Burned In Annotation               (0028,0301) S,*,U
   Lossy Image Compression            (0028,2110) S,*,U
   Lossy Image Compression Ratio      (0028,2112) S,*,U
   Number of Frames                   (0028,0008) S,*,U
   SOP Instance UID                   (0008,0018) UNIQUE
   SOP Class UID                      (0008,0016) NONE
   Common to all query levels                     
   Specific Character Set             (0008,0005) S,*,U
   ================================== =========== =================

Types of Matching:

The types of Matching supported by the C-FIND SCU. An "S" indicates the
identifier attribute uses Single Value Matching, an "R" indicates Range
Matching, a n"*"indicates wild card matching, a 'U' indicates Universal
Matching, and an 'L' indicates that UID lists are sent. "NONE" indicates
that no matching is supported, but that values for this Element are
requested to be returned (i.e., universal matching), and "UNIQUE"
indicates that this is the Unique Key for that query level, in which
case Universal Matching or Single Value Matching is used depending on
the query level.

.. _sect_D.4.2.4.3.1.3.2:

Presentation Context Acceptance Criterion
                                         

FIND-SCU does not accept associations.

.. _sect_D.4.2.4.3.1.3.3:

Transfer Syntax Selection Policies
                                  

FIND-SCU prefers explicit Transfer Syntaxes. If offered a choice of
Transfer Syntaxes in the accepted Presentation Contexts, it will apply
the following priority to the choice of Presentation Context to use for
the C-STORE operation:

a. first encountered explicit Transfer Syntax,

b. default Transfer Syntax.

.. _sect_D.4.2.4.3.1.3.4:

Response Status
               

FIND-SCU will behave as described in `table_title <#table_D.4.2-24>`__
in response to the status returned in the C-FIND response command
message(s).

.. table:: Response Status for FIND-SCU and Query Remote AE Request

   +----------------+----------------+--------------+----------------+
   | Service Status | Further        | Status Codes | Behavior       |
   |                | Meaning        |              |                |
   +================+================+==============+================+
   | Refused        | Out of         | A700         | Current query  |
   |                | Resources      |              | is terminated; |
   |                |                |              | remaining      |
   |                |                |              | queries        |
   |                |                |              | continue       |
   +----------------+----------------+--------------+----------------+
   | Error          | Identifier     | A900         | Current query  |
   |                | does not match |              | is terminated; |
   |                | SOP Class      |              | remaining      |
   |                |                |              | queries        |
   |                |                |              | continue       |
   +----------------+----------------+--------------+----------------+
   |                | Unable to      | Cxxx         | Current query  |
   |                | process        |              | is terminated; |
   |                |                |              | remaining      |
   |                |                |              | queries        |
   |                |                |              | continue       |
   +----------------+----------------+--------------+----------------+
   | Cancel         | Matching       | FE00         | Ignored        |
   |                | terminated due |              | (should never  |
   |                | to Cancel      |              | occur, since   |
   |                | request        |              | cancels never  |
   |                |                |              | issued)        |
   +----------------+----------------+--------------+----------------+
   | Success        | Matching is    | 0000         | Current query  |
   |                | complete - No  |              | is terminated; |
   |                | final          |              | remaining      |
   |                | Identifier is  |              | queries        |
   |                | supplied       |              | continue       |
   +----------------+----------------+--------------+----------------+
   | Pending        | Matches are    | FF00         | Identifier     |
   |                | continuing -   |              | used to        |
   |                | Current Match  |              | populate       |
   |                | is supplied    |              | browser and    |
   |                | and any        |              | trigger        |
   |                | Optional Keys  |              | recursive      |
   |                | were supported |              | lower level    |
   |                | in the same    |              | queries        |
   |                | manner as      |              |                |
   |                | Required Keys  |              |                |
   +----------------+----------------+--------------+----------------+
   |                | Matches are    | FF01         | Identifier     |
   |                | continuing -   |              | used to        |
   |                | Warning that   |              | populate       |
   |                | one or more    |              | browser and    |
   |                | Optional Keys  |              | trigger        |
   |                | were not       |              | recursive      |
   |                | supported for  |              | lower level    |
   |                | existence      |              | queries        |
   |                | and/or         |              |                |
   |                | matching for   |              |                |
   |                | this           |              |                |
   |                | Identifier     |              |                |
   +----------------+----------------+--------------+----------------+

.. _sect_D.4.2.4.4:

Association Acceptance Policy
'''''''''''''''''''''''''''''

FIND-SCU does not accept associations.

.. _sect_D.4.2.5:

MOVE-SCU
^^^^^^^^

.. _sect_D.4.2.5.1:

SOP Classes
'''''''''''

MOVE-SCU provide Standard Conformance to the following SOP Class(es) :

.. table:: SOP Classes Supported By MOVE-SCU

   +---------------------------+---------------------------+-----+-----+
   | SOP Class Name            | SOP Class UID             | SCU | SCP |
   +===========================+===========================+=====+=====+
   | Study Root Query/Retrieve | 1.                        | Yes | No  |
   | Information Model - MOVE  | 2.840.10008.5.1.4.1.2.2.2 |     |     |
   +---------------------------+---------------------------+-----+-----+

.. _sect_D.4.2.5.2:

Association Policies
''''''''''''''''''''

.. _sect_D.4.2.5.2.1:

General
       

MOVE-SCU initiates but never accepts associations.

.. table:: Maximum PDU Size Received as a SCP for MOVE-SCU

   ========================= =========
   Maximum PDU size received Unlimited
   ========================= =========

.. _sect_D.4.2.5.2.2:

Number of Associations
                      

.. table:: Number of Associations as a SCP for MOVE-SCU

   =========================================== =
   Maximum number of simultaneous associations 1
   =========================================== =

.. _sect_D.4.2.5.2.3:

Asynchronous Nature
                   

MOVE-SCU will only allow a single outstanding operation on an
Association. Therefore, MOVE-SCU will not perform asynchronous
operations window negotiation.

.. _sect_D.4.2.5.2.4:

Implementation Identifying Information
                                      

.. table:: DICOM Implementation Class and Version for MOVE-SCU

   =========================== =============================
   Implementation Class UID    xxxxxxxxxxx.yy.etc.ad.inf.usw
   Implementation Version Name Viewer1.0
   =========================== =============================

.. _sect_D.4.2.5.3:

Association Initiation Policy
'''''''''''''''''''''''''''''

MOVE-SCU attempts to initiate a new association when the user performs
the retrieve action from the user interface.

.. _sect_D.4.2.5.3.1:

Activity - Retrieve From Remote AE
                                  

.. _sect_D.4.2.5.3.1.1:

Description and Sequencing of Activities
                                        

For the entity (study, series or instance) selected from the user
interface to be retrieved, a single attempt will be made to retrieve it
from the selected remote AE. If the retrieve fails, for whatever reason,
no retry will be performed.

.. _sect_D.4.2.5.3.1.2:

Proposed Presentation Contexts
                              

.. table:: Proposed Presentation Contexts for MOVE-SCU and Retrieve From
Remote AE

   +------------+------------+------------+------------+-----+------+
   | Pr         |            |            |            |     |      |
   | esentation |            |            |            |     |      |
   | Context    |            |            |            |     |      |
   | Table      |            |            |            |     |      |
   +============+============+============+============+=====+======+
   | See        | See        | Implicit   | 1.2.840    | SCP | None |
   | `ta        | `ta        | VR Little  | .10008.1.2 |     |      |
   | ble_title  | ble_title  | Endian     |            |     |      |
   | <#table_D. | <#table_D. |            |            |     |      |
   | 4.2-25>`__ | 4.2-25>`__ |            |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | Explicit   | 1.2.840.1  |            |            |     |      |
   | VR Little  | 0008.1.2.1 |            |            |     |      |
   | Endian     |            |            |            |     |      |
   +------------+------------+------------+------------+-----+------+

MOVE-SCU will propose multiple Presentation Contexts, one for each of
the supported Transfer Syntaxes, and an additional Presentation Context
with all of the supported Transfer Syntaxes, in order to determine which
Transfer Syntaxes the remote SCP supports, and which it prefers.

.. _sect_D.4.2.5.3.1.2.1:

Extended Negotiation
                    

No extended negotiation is performed.

In particular, relational retrievals are not supported.

.. _sect_D.4.2.5.3.1.3:

SOP Specific Conformance
                        

.. _sect_D.4.2.5.3.1.3.1:

SOP Specific Conformance to C-FIND SOP Classes
                                              

MOVE-SCU provides standard conformance to the supported C-MOVE SOP
Classes.

Only a single information model, Study Root, is supported.

A retrieval will be performed at the STUDY, SERIES or IMAGE level
depending on what level of entity has been selected by the user in the
browser.

No CANCEL requests are ever issued.

The retrieval is performed from the AE that was specified in the
Retrieve AE attribute returned from the query performed by FIND-SCU. The
instances are retrieved to the current application's local database by
specifying the destination as the AE Title of the STORE-SCP AE of the
local application. This implies that the remote C-MOVE SCP must be
preconfigured to determine the presentation address corresponding to the
STORE-SCP AE. The STORE-SCP AE will accept storage requests addressed to
it from anywhere, so no pre-configuration of the local application to
accept from the remote AE is necessary (except in so far as it was
necessary to configure FIND-SCU).

.. table:: Study Root Request Identifier for MOVE-SCU

   =================== =========== ==============================
   Name                Tag         Unique, Matching or Return Key
   =================== =========== ==============================
   STUDY level                     
   Study Instance UID  (0020,000D) U
   SERIES level                    
   Series Instance UID (0020,000E) U
   IMAGE level                     
   SOP Instance UID    (0008,0018) U
   =================== =========== ==============================

.. _sect_D.4.2.5.3.1.3.2:

Presentation Context Acceptance Criterion
                                         

MOVE-SCU does not accept associations.

.. _sect_D.4.2.5.3.1.3.3:

Transfer Syntax Selection Policies
                                  

MOVE-SCU prefers explicit Transfer Syntaxes. If offered a choice of
Transfer Syntaxes in the accepted Presentation Contexts, it will apply
the following priority to the choice of Presentation Context to use for
the C-STORE operation:

a. first encountered explicit Transfer Syntax,

.. _sect_D.4.2.5.3.1.3.4:

Response Status
               

MOVE-SCU will behave as described in the Table below in response to the
status returned in the C-MOVE response command message(s).

.. table:: Response Status for MOVE-SCU and Retrieve From Remote AE
Request

   +-------------+-------------+-------------+-------------+-------------+
   | Service     | Further     | Status      | Related     | Behavior    |
   | Status      | Meaning     | Codes       | Fields      |             |
   +=============+=============+=============+=============+=============+
   | Refused     | Out of      | A701        | (0000,0902) | Retrieval   |
   |             | Resources - |             |             | is          |
   |             | Unable to   |             |             | terminated  |
   |             | calculate   |             |             |             |
   |             | number of   |             |             |             |
   |             | matches     |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   |             | Out of      | A702        | (0000,1020) | Retrieval   |
   |             | Resources - |             |             | is          |
   |             | Unable to   |             | (0000,1021) | terminated  |
   |             | perform     |             |             |             |
   |             | sub         |             | (0000,1022) |             |
   |             | -operations |             |             |             |
   |             |             |             | (0000,1023) |             |
   +-------------+-------------+-------------+-------------+-------------+
   |             | Move        | A801        | (0000,0902) | Retrieval   |
   |             | Destination |             |             | is          |
   |             | unknown     |             |             | terminated  |
   +-------------+-------------+-------------+-------------+-------------+
   | Failed      | Identifier  | A900        | (0000,0901) | Retrieval   |
   |             | does not    |             |             | is          |
   |             | match SOP   |             | (0000,0902) | terminated  |
   |             | Class       |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   |             | Unable to   | Cxxx        | (0000,0901) | Retrieval   |
   |             | process     |             |             | is          |
   |             |             |             | (0000,0902) | terminated  |
   +-------------+-------------+-------------+-------------+-------------+
   | Cancel      | Sub         | FE00        | (0000,1020) | Retrieval   |
   |             | -operations |             |             | is          |
   |             | terminated  |             | (0000,1021) | terminated  |
   |             | due to      |             |             | (should     |
   |             | Cancel      |             | (0000,1022) | never       |
   |             | Indication  |             |             | occur,      |
   |             |             |             | (0000,1023) | since       |
   |             |             |             |             | cancels     |
   |             |             |             |             | never       |
   |             |             |             |             | issued)     |
   +-------------+-------------+-------------+-------------+-------------+
   | Warning     | Sub         | B000        | (0000,1020) | Retrieval   |
   |             | -operations |             |             | is          |
   |             | Complete -  |             | (0000,1022) | terminated  |
   |             | One or more |             |             |             |
   |             | Failures    |             | (0000,1023) |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Success     | Sub         | 0000        | (0000,1020) | Retrieval   |
   |             | -operations |             |             | is          |
   |             | Complete -  |             | (0000,1021) | terminated  |
   |             | No Failures |             |             |             |
   |             |             |             | (0000,1022) |             |
   |             |             |             |             |             |
   |             |             |             | (0000,1023) |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Pending     | Sub         | FF00        | (0000,1020) | Retrieval   |
   |             | -operations |             |             | continues   |
   |             | are         |             | (0000,1021) |             |
   |             | continuing  |             |             |             |
   |             |             |             | (0000,1022) |             |
   |             |             |             |             |             |
   |             |             |             | (0000,1023) |             |
   +-------------+-------------+-------------+-------------+-------------+

.. _sect_D.4.2.5.3.1.3.5:

Sub-Operation Dependent Behavior
                                

Since the C-MOVE operation is dependent on completion of C-STORE
sub-operations that are occurring on a separate association, the
question of failure of operations on the other association(s) must be
considered.

MOVE-SCU completely ignores whatever activities are taking place in
relation to the STORAGE-SCP AE that is receiving the retrieved
instances. Once the C-MOVE has been initiated it runs to completion (or
failure) as described in the C-MOVE response command message(s). There
is no attempt by MOVE-SCU to confirm that instances have actually been
successfully received or locally stored.

Whether or not completely or partially successfully retrievals are made
available in the local database to the user is purely dependent on the
success or failure of the C-STORE sub-operations, not on any explicit
action by MOVE-SCU.

Whether or not the remote AE attempts to retry any failed C-STORE
sub-operations is beyond the control of MOVE-SCU.

If the association on which the C-MOVE was issued is aborted for any
reason, whether or not the C-STORE sub-operations continue is dependent
on the remote AE; the local STORAGE-SCP will continue to accept
associations and storage operations regardless.

.. _sect_D.4.2.5.4:

Association Acceptance Policy
'''''''''''''''''''''''''''''

MOVE-SCU does not accept associations.

.. _sect_D.4.3:

Network Interfaces
~~~~~~~~~~~~~~~~~~

.. _sect_D.4.3.1:

Physical Network Interface
^^^^^^^^^^^^^^^^^^^^^^^^^^

The application is indifferent to the physical medium over which TCP/IP
executes, which is dependent on the underlying operating system and
hardware.

.. _sect_D.4.3.2:

Additional Protocols
^^^^^^^^^^^^^^^^^^^^

When host names rather than IP addresses are used in the configuration
properties to specify presentation addresses for remote AEs, the
application is dependent on the name resolution mechanism of the
underlying operating system.

.. _sect_D.4.3.3:

IPv4 and IPv6 Support
^^^^^^^^^^^^^^^^^^^^^

This product supports both IPv4 and IPv6. It does not utilize any of the
optional configuration identification or security features of IPv6.

.. _sect_D.4.4:

Configuration
~~~~~~~~~~~~~

All configuration is performed through the use of Java properties
file(s) stored in pre-defined locations that are specific to the
underlying operating system. Refer to the Release Notes for specific
details.

.. _sect_D.4.4.1:

AE Title/Presentation Address Mapping
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Calling AE Title of the local application is configurable in the
preferences file, and is shared by all of the AEs. The mapping of the
logical name by which remote AEs are described in the user interface to
Called AE Titles as well as presentation address (hostname or IP address
and port number) is configurable in the preferences file.

.. _sect_D.4.4.2:

Parameters
^^^^^^^^^^

.. table:: Configuration Parameters Table

   +--------------------------+--------------+--------------------------+
   | Parameter                | Configurable | Default Value            |
   +==========================+==============+==========================+
   | **General Parameters**   |              |                          |
   +--------------------------+--------------+--------------------------+
   | PDU Size                 | No           | 16kB                     |
   +--------------------------+--------------+--------------------------+
   | Time-out waiting for     | No           | None                     |
   | acceptance or rejection  |              |                          |
   | Response to an           |              |                          |
   | Association Open         |              |                          |
   | Request. (Application    |              |                          |
   | Level timeout)           |              |                          |
   +--------------------------+--------------+--------------------------+
   | General DIMSE level      | No           | None                     |
   | time-out values          |              |                          |
   +--------------------------+--------------+--------------------------+
   | Time-out waiting for     | No           | None                     |
   | response to TCP/IP       |              |                          |
   | connect() request.       |              |                          |
   | (Low-level timeout)      |              |                          |
   +--------------------------+--------------+--------------------------+
   | Time-out waiting for     | No           | None                     |
   | acceptance of a TCP/IP   |              |                          |
   | message over the         |              |                          |
   | network. (Low-level      |              |                          |
   | timeout)                 |              |                          |
   +--------------------------+--------------+--------------------------+
   | Time-out for waiting for | No           | None                     |
   | data between TCP/IP      |              |                          |
   | packets. (Low-level      |              |                          |
   | timeout)                 |              |                          |
   +--------------------------+--------------+--------------------------+
   | Any changes to default   | No           | None                     |
   | TCP/IP settings, such as |              |                          |
   | configurable stack       |              |                          |
   | parameters.              |              |                          |
   +--------------------------+--------------+--------------------------+
   | **AE Specific Parameters |              |                          |
   | (all AEs)**              |              |                          |
   +--------------------------+--------------+--------------------------+
   | Size constraint in       | No           | None                     |
   | maximum object size      |              |                          |
   +--------------------------+--------------+--------------------------+
   | Maximum PDU size the AE  | No           | Unlimited                |
   | can receive (see note 1) |              |                          |
   +--------------------------+--------------+--------------------------+
   | Maximum PDU size the AE  | No           | Unlimited                |
   | can send                 |              |                          |
   +--------------------------+--------------+--------------------------+
   | AE specific DIMSE level  | No           | None                     |
   | time-out values          |              |                          |
   +--------------------------+--------------+--------------------------+
   | Number of simultaneous   | No           | Unlimited                |
   | Associations by Service  |              |                          |
   | and/or SOP Class         |              |                          |
   +--------------------------+--------------+--------------------------+
   | SOP Class support        | No           | All supported SOP        |
   |                          |              | Classes always proposed  |
   |                          |              | and accepted             |
   +--------------------------+--------------+--------------------------+
   | Transfer Syntax support  | No           | All supported Transfer   |
   |                          |              | Syntaxes always proposed |
   |                          |              | and accepted             |
   +--------------------------+--------------+--------------------------+
   | Other parameters that    | No           | None                     |
   | are configurable         |              |                          |
   +--------------------------+--------------+--------------------------+

.. note::

   Though the application can support unlimited PDU sizes, it will never
   offer a Maximum Received PDU Length of zero (unlimited) since this
   triggers a bug in some older systems.

.. _sect_D.5:

Media Interchange
-----------------

.. _sect_D.5.1:

Implementation Model
~~~~~~~~~~~~~~~~~~~~

.. _sect_D.5.1.1:

Application Data Flow
^^^^^^^^^^^^^^^^^^^^^

The application is a single pure Java application that provides a user
interface, network support and media support as a File Set Reader.

Conceptually it may be modeled as the following single AE:

-  MEDIA-FSR, which loads a user-selected compliant file, which may be a
   DICOMDIR or an image or spectroscopy object, either from the local
   file system or from compliant media according to one of the General
   Purpose Media Application Profiles of (CD-R or DVD-RAM)

In effect, the application is media-neutral, since the user is required
to browse and locate the DICOMDIR file. Furthermore, any DICOM image or
spectroscopy object encoded in one of the standard uncompressed Transfer
Syntaxes may be loaded, even in the absence of a compliant
meta-information header, in which case a "best guess" at the Transfer
Syntax will be made.

Compressed Transfer Syntaxes are not supported, which limits the Media
Application Profiles supported.

.. _sect_D.5.1.2:

Functional Definitions of AEs
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. _sect_D.5.1.2.1:

MEDIA-FSR
'''''''''

MEDIA-FSR is activated through the user interface to select directories,
images and spectra for display, import into the local database or
network transmission.

.. _sect_D.5.1.3:

Sequencing of Real-World Activities
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

All FSR activities are sequentially initiated in the user interface, and
another activity may not be initiated until the prior activity has
completed.

.. _sect_D.5.2:

AE Specifications
~~~~~~~~~~~~~~~~~

.. _sect_D.5.2.1:

MEDIA-FSR
^^^^^^^^^

MEDIA-FSR provides standard conformance to the Media Storage Service
Class.

.. table:: Application Profiles, Activities, and Roles for MEDIA-FSR

   ============================== ====================== ====
   Application Profiles Supported Real World Activity    Role
   ============================== ====================== ====
   STD-GEN-CD                     Load directory or file FSR
   STD-GEN-DVD-RAM                Load directory or file FSR
   ============================== ====================== ====

.. note::

   The application is media neutral and dependent on the underlying
   hardware. Any (non-secure) General Purpose Profile can be supported.

.. _sect_D.5.2.1.1:

File Meta Information for the Application Entity
''''''''''''''''''''''''''''''''''''''''''''''''

Not applicable, since MEDIA-FSR is not an FSC or FSU.

.. _sect_D.5.2.1.2:

Real World Activities
'''''''''''''''''''''

.. _sect_D.5.2.1.2.1:

Activity - Load Directory or File
                                 

MEDIA-FSR is activated through the user interface when a user selects
the File load operation.

If the loaded file is a DICOMDIR, a browser will be displayed, from
which instances may be selected and in turn loaded for display, imported
into the local database or sent to a remote AE over the network.

If the file is an image or spectroscopy instance, it will be loaded and
displayed.

.. _sect_D.5.2.1.2.1.1:

Application Profile Specific Conformance
                                        

There are no extensions or specializations.

.. _sect_D.5.3:

Augmented and Private Profiles
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. _sect_D.5.3.1:

Augmented Profiles
^^^^^^^^^^^^^^^^^^

None.

.. _sect_D.5.3.2:

Private Profiles
^^^^^^^^^^^^^^^^

None.

.. _sect_D.5.4:

Media Configuration
~~~~~~~~~~~~~~~~~~~

None.

.. _sect_D.6:

Support of Character Sets
-------------------------

.. _sect_D.6.1:

Overview
~~~~~~~~

The application supports all extended character sets defined in the
DICOM 2002 standard, including single-byte and multi-byte character sets
as well as code extension techniques using ISO 2022 escapes.

Support extends to correctly decoding and displaying the correct symbol
for all names and strings found in the DICOMDIR, in storage instances
from media and received over the network, and in the local database.

No specific support for sorting of strings other than in the default
character set is provided in the browsers.

.. _sect_D.6.2:

Character Sets
~~~~~~~~~~~~~~

In addition to the default character repertoire, the Defined Terms for
Specific Character Set in `table_title <#table_D.6.2-1>`__ are
supported:

.. table:: Supported Specific Character Set Defined Terms

   ========================= ===============
   Character Set Description Defined Term
   ========================= ===============
   Latin alphabet No. 1      ISO_IR 100
   Latin alphabet No. 2      ISO_IR 101
   Latin alphabet No. 3      ISO_IR 109
   Latin alphabet No. 4      ISO_IR 110
   Cyrillic                  ISO_IR 144
   Arabic                    ISO_IR 127
   Greek                     ISO_IR 126
   Hebrew                    ISO_IR 138
   Latin alphabet No. 5      ISO_IR 148
   Japanese                  ISO_IR 13
   Thai                      ISO_IR 166
   Default repertoire        ISO 2022 IR 6
   Latin alphabet No. 1      ISO 2022 IR 100
   Latin alphabet No. 2      ISO 2022 IR 101
   Latin alphabet No. 3      ISO 2022 IR 109
   Latin alphabet No. 4      ISO 2022 IR 110
   Cyrillic                  ISO 2022 IR 144
   Arabic                    ISO 2022 IR 127
   Greek                     ISO 2022 IR 126
   Hebrew                    ISO 2022 IR 138
   Latin alphabet No. 5      ISO 2022 IR 148
   Japanese                  ISO 2022 IR 13
   Thai                      ISO 2022 IR 166
   Japanese                  ISO 2022 IR 87
   Japanese                  ISO 2022 IR 159
   Korean                    ISO 2022 IR 149
   ========================= ===============

.. _sect_D.6.3:

Character Set Configuration
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Whether or not characters are displayed correctly depends on the
presence of font support in the underlying operating system. Typically,
as described in the Release Notes, it may be necessary for the user to
add one of the "all Unicode" fonts to their system configuration in
order to correctly display characters that would not typically be used
in the default locale.

.. _sect_D.7:

Security
--------

.. _sect_D.7.1:

Security Profiles
~~~~~~~~~~~~~~~~~

None supported.

.. _sect_D.7.2:

Association Level Security
~~~~~~~~~~~~~~~~~~~~~~~~~~

None supported.

Any Calling AE Titles and/or IP addresses may open an Association.

.. _sect_D.7.3:

Application Level Security
~~~~~~~~~~~~~~~~~~~~~~~~~~

None supported.

.. _sect_D.8:

Annexes
-------

.. _sect_D.8.1:

IOD Contents
~~~~~~~~~~~~

.. _sect_D.8.1.1:

Created SOP Instances
^^^^^^^^^^^^^^^^^^^^^

None.

.. _sect_D.8.1.2:

Usage of Attributes From Received IODs
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

No SOP Class specific fields are required.

The local database, remote query and directory browsers make use of the
conventional identification attributes to distinguish patients, studies,
series and instances. In particular, if two patients have the same value
for Patient ID, they will be treated as the same in the browser and the
local database.

.. _sect_D.8.1.3:

Attribute Mapping
^^^^^^^^^^^^^^^^^

Not applicable.

.. _sect_D.8.1.4:

Coerced/Modified Fields
^^^^^^^^^^^^^^^^^^^^^^^

No coercion is performed.

.. _sect_D.8.2:

Data Dictionary of Private Attributes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

No private attributes are defined.

.. _sect_D.8.3:

Coded Terminology and Templates
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The value for Code Meaning will be displayed for all code sequences. No
local lexicon is provided to look up alternative code meanings.

.. _sect_D.8.4:

Grayscale Image Consistency
~~~~~~~~~~~~~~~~~~~~~~~~~~~

The high resolution display monitor attached to the product can be
calibrated according to the Grayscale Standard Display Function (GSDF).
The Service/Installation Tool is used together with a luminance meter to
measure the Characteristic Curve of the display system and the current
ambient light. See the product Service Manual for details on the
calibration procedure and supported calibration hardware. The result of
the calibration procedure is a Monitor Correction LUT that will be
active within the display subsystem after a system reboot.

.. _sect_D.8.5:

Standard Extended/Specialized/Private SOP Classes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

None

.. _sect_D.8.6:

Private Transfer Syntaxes
~~~~~~~~~~~~~~~~~~~~~~~~~

None.

