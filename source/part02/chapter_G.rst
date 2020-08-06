.. _chapter_G:

Conformance Statement Sample ImageViewer with Hanging Protocol Support (Informative)
====================================================================================

Disclaimer:

This document is an example DICOM Conformance Statement for a fictional
image display device for DICOM images and Hanging Protocol objects
obtained over the network.

As stated in the annex title, this document is truly informative, and
not normative. A conformance statement of an actual product might
implement additional services and options as appropriate for its
specific purpose. In addition, an actual product might implement the
services described in a different manner and, for example, with
different characteristics and/or sequencing of activities. In other
words, this conformance statement example does not intend to standardize
a particular manner that a product might implement DICOM functionality.

.. _sect_G.0:

Cover Page
----------

Company Name: EXAMPLE-Viewing­PRODUCTS.

Product Name: SAMPLE ImageViewer with Hanging Protocol Support

Version: 1.0-rev. A.1

Internal document number: 4226-xxx-yyy-zzz rev 1

Date: YYYYMMDD

.. _sect_G.1:

Conformance Statement Overview
------------------------------

The application supports accepting Images and Presentation States from
remote systems, and querying a remote system for Hanging Protocol
Instances that may then be retrieved to the local system. It also
supports sending locally loaded images and created Presentation State
and Hanging Protocol Instances across the network to remote systems.

.. table:: Network Services

   +----------------------+----------------------+----------------------+
   | SOP Classes          | User of Service(SCU) | Provider of          |
   |                      |                      | Service(SCP)         |
   +======================+======================+======================+
   | Transfer             |                      |                      |
   +----------------------+----------------------+----------------------+
   | Ultrasound Image     | Yes                  | Yes                  |
   | Storage              |                      |                      |
   +----------------------+----------------------+----------------------+
   | Ultrasound           | Yes                  | Yes                  |
   | Multi-frame Image    |                      |                      |
   | Storage              |                      |                      |
   +----------------------+----------------------+----------------------+
   | MR Image Storage     | Yes                  | Yes                  |
   +----------------------+----------------------+----------------------+
   | Digital Mammography  | Yes                  | Yes                  |
   | X-Ray Image Storage  |                      |                      |
   | - For Presentation   |                      |                      |
   +----------------------+----------------------+----------------------+
   | Grayscale Softcopy   | Yes                  | Yes                  |
   | Presentation State   |                      |                      |
   | Storage SOP Class    |                      |                      |
   +----------------------+----------------------+----------------------+
   | Hanging Protocol     | Yes                  | Yes                  |
   | Storage              |                      |                      |
   +----------------------+----------------------+----------------------+
   | Query/Retrieve       |                      |                      |
   +----------------------+----------------------+----------------------+
   | Hanging Protocol     | Yes                  | No                   |
   | Information Model -  |                      |                      |
   | FIND                 |                      |                      |
   +----------------------+----------------------+----------------------+
   | Hanging Protocol     | Yes                  | No                   |
   | Information Model -  |                      |                      |
   | MOVE                 |                      |                      |
   +----------------------+----------------------+----------------------+

.. _sect_G.2:

Table of Contents
-----------------

A table of contents shall be provided to assist readers in easily
finding the needed information.

.. _sect_G.3:

Introduction
------------

.. _sect_G.3.1:

Revision History
~~~~~~~~~~~~~~~~

.. table:: Revision History

   ================ =============== ====== ======================
   Document Version Date of Issue   Author Description
   ================ =============== ====== ======================
   1.1              April 30, 2004  WG 11  Version for Final Text
   1.2              August 30, 2007 WG 6   Revised Introduction
   ================ =============== ====== ======================

.. _sect_G.3.2:

Audience, Remarks, Terms and Definitions, Basics of DICOM Communication, Abbreviations, References
--------------------------------------------------------------------------------------------------

*See example text in*\ `Introduction <#sect_A.3>`__\ *.*

.. _sect_G.3.3:

Additional Remarks for This Example
-----------------------------------

This document is a sample DICOM Conformance Statement created for DICOM
. It is to be used solely as an example to illustrate how to create a
DICOM Conformance Statement for a workstation supporting a variety of
types of DICOM images and DICOM Hanging Protocol objects. The subject of
the document, SAMPLE IMAGE VIEWER, is a fictional product.

.. _sect_G.4:

Networking
----------

.. _sect_G.4.1:

Implementation Model
~~~~~~~~~~~~~~~~~~~~

.. _sect_G.4.1.1:

Application Data Flow
^^^^^^^^^^^^^^^^^^^^^

The application provides both a user interface, internal database and
network listener that spawns additional threads as necessary to handle
incoming connections.

Conceptually the network services may be modeled as the following
separate AEs, though in fact all the AEs share a single (configurable)
AE Title:

-  STORAGE-SCP, which receives incoming Image, Presentation State, and
   Hanging Protocol Instances

-  STORAGE-SCU, which sends outbound Image, Presentation State, and
   Hanging Protocol Instances

-  FIND-SCU, which queries remote AEs for Hanging Protocol Instances

-  MOVE-SCU, which retrieves Hanging Protocol Instances

.. _sect_G.4.1.2:

Functional Definitions of AEs
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. _sect_G.4.1.2.1:

STORAGE-SCP
'''''''''''

STORAGE-SCP waits in the background for connections, will accept
associations with Presentation Contexts for SOP Classes of the Storage
Service Class and Hanging Protocol Storage Service Class, and will store
the received instances to the local database where they may subsequently
be listed and viewed through the user interface.

.. _sect_G.4.1.2.2:

STORAGE-SCU
'''''''''''

STORAGE-SCU is activated through the user interface when a user selects
instances from the local database, or the currently displayed instance,
and requests that they be sent to a remote AE (selected from a
pre-configured list).

.. _sect_G.4.1.2.3:

FIND-SCU
''''''''

FIND-SCU is activated in the background when images for a study are
received, to query for matching Hanging Protocols if an appropriate
Hanging Protocol Instance is not available in the local database.

.. _sect_G.4.1.2.4:

MOVE-SCU
''''''''

MOVE-SCU is activated in the background, to retrieve Hanging Protocol
Instances identified in the query results returned to the FIND-SCU. A
connection to the remote AE is established to initiate and monitor the
retrieval, and the STORAGE-SCP AE receives the retrieved instances.

.. _sect_G.4.1.3:

Sequencing of Real-World Activities
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

All SCP activities are performed asynchronously in the background and
not dependent on any sequencing.

Storage SCU activities are sequentially initiated in the user interface,
and another activity may not be initiated until the prior activity has
completed. Find and Move SCU activities are performed asynchronously in
the background, where Move activities are triggered by the results of
Find activities.

.. _sect_G.4.2:

AE Specifications
~~~~~~~~~~~~~~~~~

.. _sect_G.4.2.1:

STORAGE-SCP
^^^^^^^^^^^

.. _sect_G.4.2.1.1:

SOP Classes
'''''''''''

STORAGE-SCP provide Standard Conformance to the following SOP Class(es)
:

.. table:: SOP Classes Supported By STORAGE-SCP

   +---------------------------+---------------------------+-----+-----+
   | SOP Class Name            | SOP Class UID             | SCU | SCP |
   +===========================+===========================+=====+=====+
   | Ultrasound Image Storage  | 1.                        | No  | Yes |
   |                           | 2.840.10008.5.1.4.1.1.6.1 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | Ultrasound Multi-frame    | 1.                        | No  | Yes |
   | Image Storage             | 2.840.10008.5.1.4.1.1.3.1 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | MR Image Storage          | 1.2.840.10008.5.1.4.1.1.4 | No  | Yes |
   +---------------------------+---------------------------+-----+-----+
   | Digital Mammography X-Ray | 1.                        | No  | Yes |
   | Image Storage - For       | 2.840.10008.5.1.4.1.1.1.2 |     |     |
   | Presentation              |                           |     |     |
   +---------------------------+---------------------------+-----+-----+
   | Grayscale Softcopy        | 1.2                       | No  | Yes |
   | Presentation State        | .840.10008.5.1.4.1.1.11.1 |     |     |
   | Storage                   |                           |     |     |
   +---------------------------+---------------------------+-----+-----+
   | Hanging Protocol Storage  | 1.2.840.10008.5.1.4.38.1  | No  | Yes |
   +---------------------------+---------------------------+-----+-----+

.. _sect_G.4.2.1.2:

Association Policies
''''''''''''''''''''

.. _sect_G.4.2.1.2.1:

General
       

STORAGE-SCP accepts but never initiates associations.

.. table:: Maximum PDU Size Received as a SCP for STORAGE-SCP

   ========================= =========
   Maximum PDU size received Unlimited
   ========================= =========

.. _sect_G.4.2.1.2.2:

Number of Associations
                      

.. table:: Number of Associations as a SCP for STORAGE-SCP

   =========================================== =========
   Maximum number of simultaneous associations Unlimited
   =========================================== =========

.. _sect_G.4.2.1.2.3:

Asynchronous Nature
                   

STORAGE-SCP will only allow a single outstanding operation on an
Association. Therefore, STORAGE-SCP will not perform asynchronous
operations window negotiation.

.. _sect_G.4.2.1.2.4:

Implementation Identifying Information
                                      

.. table:: DICOM Implementation Class and Version for STORAGE-SCP

   =========================== ==================
   Implementation Class UID    1.2.840.999999.3.6
   Implementation Version Name Viewer1.0
   =========================== ==================

.. _sect_G.4.2.1.3:

Association Initiation Policy
'''''''''''''''''''''''''''''

STORAGE-SCP does not initiate associations.

.. _sect_G.4.2.1.4:

Association Acceptance Policy
'''''''''''''''''''''''''''''

When STORAGE-SCP accepts an association, it will respond to storage
requests. If the Called AE Title does not match the pre-configured AE
Title shared by all the SCPs of the application, the association will be
rejected.

.. _sect_G.4.2.1.4.1:

Activity - Receive Storage Request
                                  

.. _sect_G.4.2.1.4.1.1:

Description and Sequencing of Activities
                                        

As instances are received they are copied to the local file system and a
record inserted into the local database. If the received instance is a
duplicate of a previously received instance, the old file and database
record will be overwritten with the new one.

.. _sect_G.4.2.1.4.1.2:

Accepted Presentation Contexts
                              

.. table:: Accepted Presentation Contexts for STORAGE-SCP and Receive
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
   |  <#table_G |  <#table_G |            |            |     |      |
   | .4.2-1>`__ | .4.2-1>`__ |            |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | Explicit   | 1.2.840.1  |            |            |     |      |
   | VR Little  | 0008.1.2.1 |            |            |     |      |
   | Endian     |            |            |            |     |      |
   +------------+------------+------------+------------+-----+------+

.. _sect_G.4.2.1.4.1.2.1:

Extended Negotiation
                    

No extended negotiation is performed, though STORAGE-SCP:

-  is a Level 2 Storage SCP (Full - does not discard any data elements)

-  does not support digital signatures

-  does not coerce any received data elements

.. _sect_G.4.2.1.4.1.3:

SOP Specific Conformance
                        

.. _sect_G.4.2.1.4.1.3.1:

SOP Specific Conformance to Storage Service Class
                                                 

STORAGE-SCP provides standard conformance to the Storage Service Class.

When displaying an image in the viewing application, if a Hanging
Protocol Instance is not being applied or the instance being applied
does not contain presentation intent attributes, the newest Grayscale
Softcopy Presentation State containing references to the image will be
automatically applied, and the GSPS Presentation Label and Presentation
Description will be displayed. The user has the option to select any
other Presentation States that also reference the image. If no
Presentation State references the image then no Presentation State will
be applied by default. If a Hanging Protocol Instance is being applied,
the presentation intent attributes, if present, are used to select the
closest matching GSPS instance to apply. If there is no GSPS instance,
then the Hanging Protocol Instance presentation intent attributes are
applied, if present.

All of the Image Storage SOP Classes listed in
`table_title <#table_G.4.2-1>`__ are supported as references from
instances of the Grayscale Softcopy Presentation State Storage SOP
Class.

.. _sect_G.4.2.1.4.1.3.2:

SOP Specific Conformance to Hanging Protocol Storage Service Class
                                                                  

STORAGE-SCP provides standard conformance to the Hanging Protocol
Storage Service Class.

If Partial Data Display Handling (0072,0208) is zero length, then
MAINTAIN_LAYOUT behavior is applied. If the value is ADAPT_LAYOUT, then
Image Boxes are proportionally resized to occupy all available display
space.

If the display environment of a Hanging Protocol Instance differs from
the display environment of the ImageViewer, then the layout is
maintained.

The Hanging Protocol SOP instances are stored to a local database until
explicitly deleted. When a study is selected for display, the
application automatically applies a Hanging Protocol Instance to the
study.

.. _sect_G.4.2.1.4.1.3.3:

Presentation Context Acceptance Criterion
                                         

STORAGE-SCP will always accept any Presentation Context for the
supported SOP Classes with the supported Transfer Syntaxes. More than
one proposed Presentation Context will be accepted for the same Abstract
Syntax if the Transfer Syntax is supported, whether or not it is the
same as another Presentation Context.

.. _sect_G.4.2.1.4.1.3.4:

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

.. _sect_G.4.2.1.4.1.3.5:

Response Status
               

STORAGE-SCP will behave as described in the Table below when generating
the C-STORE response command message.

.. table:: Response Status for STORAGE-SCP and Receive Storage Request

   +----------------+----------------+--------------+----------------+
   | Service Status | Further        | Status Codes | Reason         |
   |                | Meaning        |              |                |
   +================+================+==============+================+
   | Failure        | Refused: Out   | A700         | Never sent     |
   |                | of Resources   |              |                |
   +----------------+----------------+--------------+----------------+
   |                | Error: Data    | A900         | Never sent -   |
   |                | Set does not   |              | Data Set is    |
   |                | match SOP      |              | not checked    |
   |                | Class          |              | prior to       |
   |                |                |              | storage        |
   +----------------+----------------+--------------+----------------+
   |                | Error: Cannot  | C000         | Never sent     |
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

.. _sect_G.4.2.2:

STORAGE-SCU
^^^^^^^^^^^

.. _sect_G.4.2.2.1:

SOP Classes
'''''''''''

STORAGE-SCU provides Standard Conformance to the following SOP Class(es)
:

.. table:: SOP Classes Supported By STORAGE-SCU

   +---------------------------+---------------------------+-----+-----+
   | SOP Class Name            | SOP Class UID             | SCU | SCP |
   +===========================+===========================+=====+=====+
   | Ultrasound Image Storage  | 1.                        | Yes | No  |
   |                           | 2.840.10008.5.1.4.1.1.6.1 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | Ultrasound Multi-frame    | 1.                        | Yes | No  |
   | Image Storage             | 2.840.10008.5.1.4.1.1.3.1 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | MR Image Storage          | 1.2.840.10008.5.1.4.1.1.4 | Yes | No  |
   +---------------------------+---------------------------+-----+-----+
   | Digital Mammography X-Ray | 1.                        | Yes | No  |
   | Image Storage - For       | 2.840.10008.5.1.4.1.1.1.2 |     |     |
   | Presentation              |                           |     |     |
   +---------------------------+---------------------------+-----+-----+
   | Grayscale Softcopy        | 1.2                       | Yes | No  |
   | Presentation State        | .840.10008.5.1.4.1.1.11.1 |     |     |
   | Storage                   |                           |     |     |
   +---------------------------+---------------------------+-----+-----+
   | Hanging Protocol Storage  | 1.2.840.10008.5.1.4.38.1  | Yes | No  |
   +---------------------------+---------------------------+-----+-----+

.. _sect_G.4.2.2.2:

Association Policies
''''''''''''''''''''

.. _sect_G.4.2.2.2.1:

General
       

STORAGE-SCU initiates but never accepts associations.

.. table:: Maximum PDU Size Received as a SCP for STORAGE-SCU

   ========================= =========
   Maximum PDU size received Unlimited
   ========================= =========

.. _sect_G.4.2.2.2.2:

Number of Associations
                      

.. table:: Number of Associations as a SCP for STORAGE-SCU

   =========================================== =
   Maximum number of simultaneous associations 1
   =========================================== =

.. _sect_G.4.2.2.2.3:

Asynchronous Nature
                   

STORAGE-SCU will only allow a single outstanding operation on an
Association. Therefore, STORAGE-SCU will not perform asynchronous
operations window negotiation.

.. _sect_G.4.2.2.2.4:

Implementation Identifying Information
                                      

.. table:: DICOM Implementation Class and Version for STORAGE-SCU

   =========================== ==================
   Implementation Class UID    1.2.840.999999.3.6
   Implementation Version Name Viewer1.0
   =========================== ==================

.. _sect_G.4.2.2.3:

Association Initiation Policy
'''''''''''''''''''''''''''''

STORAGE-SCU attempts to initiate a new association for each instance it
attempts to transfer.

.. _sect_G.4.2.2.3.1:

Activity - Send Storage Request
                               

.. _sect_G.4.2.2.3.1.1:

Description and Sequencing of Activities
                                        

For each Image, Presentation State, or Hanging Protocol Instance
selected from the user interface to be transferred, a single attempt
will be made to transmit it to the selected remote AE. If the send
fails, for whatever reason, no retry will be performed, and an attempt
will be made to send the next instance.

.. _sect_G.4.2.2.3.1.2:

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
   | `t         | `t         | VR Little  | .10008.1.2 |     |      |
   | able_title | able_title | Endian     |            |     |      |
   |  <#table_G |  <#table_G |            |            |     |      |
   | .4.2-7>`__ | .4.2-7>`__ |            |            |     |      |
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

.. _sect_G.4.2.2.3.1.2.1:

Extended Negotiation
                    

No extended negotiation is performed.

.. _sect_G.4.2.2.3.1.3:

SOP Specific Conformance
                        

.. _sect_G.4.2.2.3.1.3.1:

SOP Specific Conformance to Storage Service Class
                                                 

STORAGE-SCU provides standard conformance to the Storage Service Class.

.. _sect_G.4.2.2.3.1.3.2:

SOP Specific Conformance to Hanging Protocol Storage Service Class
                                                                  

STORAGE-SCU provides standard conformance to the Hanging Protocol
Storage Service Class.

In Hanging Protocol Instances created on the Viewer, no Private
Attributes are used as the value of Selector Attribute (0072,0026) in
any of the Sequence Attributes to which it applies.

.. _sect_G.4.2.2.3.1.3.3:

Presentation Context Acceptance Criterion
                                         

STORAGE-SCU does not accept associations.

.. _sect_G.4.2.2.3.1.3.4:

Transfer Syntax Selection Policies
                                  

STORAGE-SCU prefers explicit Transfer Syntaxes. If offered a choice of
Transfer Syntaxes in the accepted Presentation Contexts, it will apply
the following priority to the choice of Presentation Context to use for
the C-STORE operation:

a. first encountered explicit Transfer Syntax,

b. default Transfer Syntax.

.. _sect_G.4.2.2.3.1.3.5:

Response Status
               

STORAGE-SCU will behave as described in the Table below in response to
the status returned in the C-STORE response command message.

.. table:: Response Behavior for STORAGE-SCU and Send Storage Request

   +----------------+----------------+--------------+----------------+
   | Service Status | Further        | Status Codes | Behavior       |
   |                | Meaning        |              |                |
   +================+================+==============+================+
   | Failure        | Refused: Out   | A7xx         | The user is    |
   |                | of Resources   |              | notified and   |
   |                |                |              | the failure is |
   |                |                |              | logged         |
   +----------------+----------------+--------------+----------------+
   |                | Error: Data    | A9xx         | The user is    |
   |                | Set does not   |              | notified and   |
   |                | match SOP      |              | the failure is |
   |                | Class          |              | logged         |
   +----------------+----------------+--------------+----------------+
   |                | Error: Cannot  | Cxxx         | The user is    |
   |                | understand     |              | notified and   |
   |                |                |              | the failure is |
   |                |                |              | logged         |
   +----------------+----------------+--------------+----------------+
   | Warning        | Coercion of    | B000         | Ignored        |
   |                | Data Elements  |              |                |
   +----------------+----------------+--------------+----------------+
   |                | Data Set does  | B007         | Ignored        |
   |                | not match SOP  |              |                |
   |                | Class          |              |                |
   +----------------+----------------+--------------+----------------+
   |                | Elements       | B006         | Ignored        |
   |                | Discarded      |              |                |
   +----------------+----------------+--------------+----------------+
   | Success        |                | 0000         | Ignored        |
   +----------------+----------------+--------------+----------------+

.. _sect_G.4.2.2.4:

Association Acceptance Policy
'''''''''''''''''''''''''''''

STORAGE-SCU does not accept associations.

.. _sect_G.4.2.3:

FIND-SCU
^^^^^^^^

.. _sect_G.4.2.3.1:

SOP Classes
'''''''''''

FIND-SCU provide Standard Conformance to the following SOP Class(es) :

.. table:: SOP Classes Supported By FIND-SCU

   +-------------------------------------------+--------------------------+-----+-----+
   | SOP Class Name                            | SOP Class UID            | SCU | SCP |
   +===========================================+==========================+=====+=====+
   | Hanging Protocol Information Model - FIND | 1.2.840.10008.5.1.4.38.2 | Yes | No  |
   +-------------------------------------------+--------------------------+-----+-----+

.. _sect_G.4.2.3.2:

Association Policies
''''''''''''''''''''

.. _sect_G.4.2.3.2.1:

General
       

FIND-SCU initiates but never accepts associations.

.. table:: Maximum PDU Size Received as a SCP for FIND-SCU

   ========================= =========
   Maximum PDU size received Unlimited
   ========================= =========

.. _sect_G.4.2.3.2.2:

Number of Associations
                      

.. table:: Number of Associations as a SCP for FIND-SCU

   =========================================== =
   Maximum number of simultaneous associations 1
   =========================================== =

.. _sect_G.4.2.3.2.3:

Asynchronous Nature
                   

FIND-SCU will only allow a single outstanding operation on an
Association. Therefore, FIND-SCU will not perform asynchronous
operations window negotiation.

.. _sect_G.4.2.3.2.4:

Implementation Identifying Information
                                      

.. table:: DICOM Implementation Class and Version for FIND-SCU

   =========================== ==================
   Implementation Class UID    1.2.840.999999.3.6
   Implementation Version Name Viewer1.0
   =========================== ==================

.. _sect_G.4.2.3.3:

Association Initiation Policy
'''''''''''''''''''''''''''''

FIND-SCU attempts to initiate a new association when a study is received
for which an appropriate Hanging Protocol Instance is not already stored
in the local database.

.. _sect_G.4.2.3.3.1:

Activity - Query Remote AE
                          

.. _sect_G.4.2.3.3.1.1:

Description and Sequencing of Activities
                                        

A single attempt will be made to query the remote AE. If the query
fails, for whatever reason, no retry will be performed.

.. _sect_G.4.2.3.3.1.2:

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
   | <#table_G. | <#table_G. |            |            |     |      |
   | 4.2-13>`__ | 4.2-13>`__ |            |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | Explicit   | 1.2.840.1  |            |            |     |      |
   | VR Little  | 0008.1.2.1 |            |            |     |      |
   | Endian     |            |            |            |     |      |
   +------------+------------+------------+------------+-----+------+

FIND-SCU will propose multiple Presentation Contexts, one for each of
the supported Transfer Syntaxes, and an additional Presentation Context
with all of the supported Transfer Syntaxes, in order to determine which
Transfer Syntaxes the remote SCP supports, and which it prefers.

.. _sect_G.4.2.3.3.1.2.1:

Extended Negotiation
                    

No extended negotiation is performed.

.. _sect_G.4.2.3.3.1.3:

SOP Specific Conformance
                        

.. _sect_G.4.2.3.3.1.3.1:

SOP Specific Conformance to C-FIND SOP Classes
                                              

FIND-SCU provides standard conformance to the supported C-FIND SOP
Class.

The following applies to Hanging Protocol Information Model C-FIND.

If present in the response, Specific Character Set will be used to
identify character sets other than the default character set for
matching between Hanging Protocol and Image Instances.

.. table:: Hanging Protocol Information Model C-FIND SOP Specific
Conformance

   +--------------------------+-------------+--------------------------+
   | Name                     | Tag         | Types of Matching        |
   +==========================+=============+==========================+
   | SOP Class UID            | (0008,0016) | zero length              |
   +--------------------------+-------------+--------------------------+
   | SOP Instance UID         | (0008,0018) | zero length              |
   +--------------------------+-------------+--------------------------+
   | Hanging Protocol Name    | (0072,0002) | S, \*, U                 |
   +--------------------------+-------------+--------------------------+
   | Hanging Protocol         | (0072,0004) | zero length              |
   | Description              |             |                          |
   +--------------------------+-------------+--------------------------+
   | Hanging Protocol Level   | (0072,0006) | S, U                     |
   +--------------------------+-------------+--------------------------+
   | Hanging Protocol Creator | (0072,0008) | zero length              |
   +--------------------------+-------------+--------------------------+
   | Hanging Protocol         | (0072,000A) | zero length              |
   | Creation Datetime        |             |                          |
   +--------------------------+-------------+--------------------------+
   | Hanging Protocol         | (0072,000C) | SQ, U                    |
   | Definition Sequence      |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Modality                | (0008,0060) | From list (US, MR, MG)   |
   |                          |             | or zero length           |
   +--------------------------+-------------+--------------------------+
   | >Anatomic Region         | (0008,2218) | From or zero length      |
   | Sequence                 |             |                          |
   +--------------------------+-------------+--------------------------+
   | >> Code Value            | (0008,0100) | S, U                     |
   +--------------------------+-------------+--------------------------+
   | >> Coding Scheme         | (0008,0102) | S, U                     |
   | Designator               |             |                          |
   +--------------------------+-------------+--------------------------+
   | >>Coding Scheme Version  | (0008,0103) | zero length              |
   +--------------------------+-------------+--------------------------+
   | >>Code Meaning           | (0008,0104) | zero length              |
   +--------------------------+-------------+--------------------------+
   | >Laterality              | (0020,0060) | From list (R, L, U, B)   |
   |                          |             | or zero length           |
   +--------------------------+-------------+--------------------------+
   | > Procedure Code         | (0008,1032) | zero length              |
   | Sequence                 |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Reason for Requested    | (0040,100A) | zero length              |
   | Procedure Code Sequence  |             |                          |
   +--------------------------+-------------+--------------------------+
   | Number of Priors         | (0072,0014) | zero length              |
   | Referenced               |             |                          |
   +--------------------------+-------------+--------------------------+
   | Hanging Protocol User    | (0072,000E) | From list of local coded |
   | Identification Code      |             | terms or zero length     |
   | Sequence                 |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Code Value              | (0008,0100) | S, U                     |
   +--------------------------+-------------+--------------------------+
   | >Coding Scheme           | (0008,0102) | S, U                     |
   | Designator               |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Coding Scheme Version   | (0008,0103) | zero length              |
   +--------------------------+-------------+--------------------------+
   | >Code Meaning            | (0008,0104) | zero length              |
   +--------------------------+-------------+--------------------------+
   | Hanging Protocol User    | (0072,0010) | zero length              |
   | Group Name               |             |                          |
   +--------------------------+-------------+--------------------------+
   | Number of Screens        | (0072,0100) | zero length              |
   +--------------------------+-------------+--------------------------+
   | Nominal Screen           | (0072,0102) | zero length              |
   | Definition Sequence      |             |                          |
   +--------------------------+-------------+--------------------------+

.. _sect_G.4.2.3.3.1.3.2:

Presentation Context Acceptance Criterion
                                         

FIND-SCU does not accept associations.

.. _sect_G.4.2.3.3.1.3.3:

Transfer Syntax Selection Policies
                                  

FIND-SCU prefers explicit Transfer Syntaxes. If offered a choice of
Transfer Syntaxes in the accepted Presentation Contexts, it will apply
the following priority to the choice of Presentation Context to use for
the C-FIND operation:

a. first encountered explicit Transfer Syntax,

b. default Transfer Syntax.

.. _sect_G.4.2.3.3.1.3.4:

Response Status
               

FIND-SCU will behave as described in `table_title <#table_G.4.2-19>`__
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
   |                | complete - No  |              | is terminated. |
   |                | final          |              | If one or more |
   |                | Identifier is  |              | Pending        |
   |                | supplied       |              | responses were |
   |                |                |              | received,      |
   |                |                |              | logic is       |
   |                |                |              | applied to     |
   |                |                |              | trigger        |
   |                |                |              | Retrieve of    |
   |                |                |              | best suited    |
   |                |                |              | Hanging        |
   |                |                |              | Protocol       |
   |                |                |              | Instances;     |
   |                |                |              | remaining      |
   |                |                |              | queries        |
   |                |                |              | continue       |
   +----------------+----------------+--------------+----------------+
   | Pending        | Matches are    | FF00         | Identifier     |
   |                | continuing -   |              | stored         |
   |                | Current Match  |              | temporarily    |
   |                | is supplied    |              | for use in     |
   |                | and any        |              | setting up     |
   |                | Optional Keys  |              | Retrieve.      |
   |                | were supported |              |                |
   |                | in the same    |              |                |
   |                | manner as      |              |                |
   |                | Required Keys  |              |                |
   +----------------+----------------+--------------+----------------+
   |                | Matches are    | FF01         | Identifier     |
   |                | continuing -   |              | stored         |
   |                | Warning that   |              | temporarily    |
   |                | one or more    |              | for use in     |
   |                | Optional Keys  |              | setting up     |
   |                | were not       |              | Retrieve       |
   |                | supported for  |              |                |
   |                | existence      |              |                |
   |                | and/or         |              |                |
   |                | matching for   |              |                |
   |                | this           |              |                |
   |                | Identifier     |              |                |
   +----------------+----------------+--------------+----------------+

.. _sect_G.4.2.3.4:

Association Acceptance Policy
'''''''''''''''''''''''''''''

FIND-SCU does not accept associations.

.. _sect_G.4.2.4:

MOVE-SCU
^^^^^^^^

.. _sect_G.4.2.4.1:

SOP Classes
'''''''''''

MOVE-SCU provide Standard Conformance to the following SOP Class(es) :

.. table:: SOP Classes Supported By MOVE-SCU

   +-------------------------------------------+--------------------------+-----+-----+
   | SOP Class Name                            | SOP Class UID            | SCU | SCP |
   +===========================================+==========================+=====+=====+
   | Hanging Protocol Information Model - MOVE | 1.2.840.10008.5.1.4.38.3 | Yes | No  |
   +-------------------------------------------+--------------------------+-----+-----+

.. _sect_G.4.2.4.2:

Association Policies
''''''''''''''''''''

.. _sect_G.4.2.4.2.1:

General
       

MOVE-SCU initiates but never accepts associations.

.. table:: Maximum PDU Size Received as a SCP for MOVE-SCU

   ========================= =========
   Maximum PDU size received Unlimited
   ========================= =========

.. _sect_G.4.2.4.2.2:

Number of Associations
                      

.. table:: Number of Associations as a SCP for MOVE-SCU

   =========================================== =
   Maximum number of simultaneous associations 1
   =========================================== =

.. _sect_G.4.2.4.2.3:

Asynchronous Nature
                   

MOVE-SCU will only allow a single outstanding operation on an
Association. Therefore, MOVE-SCU will not perform asynchronous
operations window negotiation.

.. _sect_G.4.2.4.2.4:

Implementation Identifying Information
                                      

.. table:: DICOM Implementation Class and Version for MOVE-SCU

   =========================== ==================
   Implementation Class UID    1.2.840.999999.3.6
   Implementation Version Name Viewer1.0
   =========================== ==================

.. _sect_G.4.2.4.3:

Association Initiation Policy
'''''''''''''''''''''''''''''

MOVE-SCU attempts to initiate a new association when the results of the
FIND-SCU indicate matching Hanging Protocol Instances to retrieve.

.. _sect_G.4.2.4.3.1:

Activity - Retrieve From Remote AE
                                  

.. _sect_G.4.2.4.3.1.1:

Description and Sequencing of Activities
                                        

A single attempt will be made to retrieve Hanging Protocol Instances
from the remote AE. If the retrieve fails, for whatever reason, no retry
will be performed.

.. _sect_G.4.2.4.3.1.2:

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
   | <#table_G. | <#table_G. |            |            |     |      |
   | 4.2-20>`__ | 4.2-20>`__ |            |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | Explicit   | 1.2.840.1  |            |            |     |      |
   | VR Little  | 0008.1.2.1 |            |            |     |      |
   | Endian     |            |            |            |     |      |
   +------------+------------+------------+------------+-----+------+

MOVE-SCU will propose multiple Presentation Contexts, one for each of
the supported Transfer Syntaxes, and an additional Presentation Context
with all of the supported Transfer Syntaxes, in order to determine which
Transfer Syntaxes the remote SCP supports, and which it prefers.

.. _sect_G.4.2.4.3.1.2.1:

Extended Negotiation
                    

No extended negotiation is performed.

.. _sect_G.4.2.4.3.1.3:

SOP Specific Conformance
                        

.. _sect_G.4.2.4.3.1.3.1:

SOP Specific Conformance to C-FIND SOP Classes
                                              

MOVE-SCU provides standard conformance to the supported C-MOVE SOP
Class.

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

.. table:: Request Identifier for MOVE-SCU

   ================ =========== ============
   Name             Tag         Request Key
   ================ =========== ============
   Hanging Protocol             
   SOP Instance UID (0008,0018) List of UIDs
   ================ =========== ============

.. _sect_G.4.2.4.3.1.3.2:

Presentation Context Acceptance Criterion
                                         

MOVE-SCU does not accept associations.

.. _sect_G.4.2.4.3.1.3.3:

Transfer Syntax Selection Policies
                                  

MOVE-SCU prefers explicit Transfer Syntaxes. If offered a choice of
Transfer Syntaxes in the accepted Presentation Contexts, it will apply
the following priority to the choice of Presentation Context to use for
the C-MOVE operation:

a. first encountered explicit Transfer Syntax,

b. default Transfer Syntax.

.. _sect_G.4.2.4.3.1.3.4:

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

.. _sect_G.4.2.4.3.1.3.5:

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

.. _sect_G.4.2.4.4:

Association Acceptance Policy
'''''''''''''''''''''''''''''

MOVE-SCU does not accept associations.

.. _sect_G.4.3:

Network Interfaces
~~~~~~~~~~~~~~~~~~

.. _sect_G.4.3.1:

Physical Network Interface
^^^^^^^^^^^^^^^^^^^^^^^^^^

The application is indifferent to the physical medium over which TCP/IP
executes, which is dependent on the underlying operating system and
hardware.

.. _sect_G.4.3.2:

Additional Protocols
^^^^^^^^^^^^^^^^^^^^

When host names rather than IP addresses are used in the configuration
properties to specify presentation addresses for remote AEs, the
application is dependent on the name resolution mechanism of the
underlying operating system.

.. _sect_G.4.3.3:

IPv4 and IPv6 Support
~~~~~~~~~~~~~~~~~~~~~

This product supports both IPv4 and IPv6. It does not utilize any of the
optional configuration identification or security features of IPv6.

.. _sect_G.4.4:

Configuration
~~~~~~~~~~~~~

All configuration is performed through the use of Java properties
file(s) stored in pre-defined locations that are specific to the
underlying operating system. Refer to the Release Notes for specific
details.

.. _sect_G.4.4.1:

AE Title/Presentation Address Mapping
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Calling AE Titles of the local application are configurable in the
preferences file. The mapping of the logical name by which remote AEs
are described in the user interface to Called AE Titles as well as
presentation address (hostname or IP address and port number) is
configurable in the preferences file.

.. _sect_G.4.4.2:

Parameters
^^^^^^^^^^

.. table:: Configuration Parameters Table

   +--------------------------+--------------+--------------------------+
   | Parameter                | Configurable | Default Value            |
   +==========================+==============+==========================+
   | General Parameters       |              |                          |
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

.. _sect_G.5:

Media Interchange
-----------------

None supported.

.. _sect_G.6:

Support of Character Sets
-------------------------

.. _sect_G.6.1:

Overview
~~~~~~~~

Support extends to correctly decoding and displaying the correct symbol
in the supported character sets for all names and strings received over
the network, and in the local database.

No specific support for sorting of strings other than in the default
character set is provided in the browsers.

.. _sect_G.6.2:

Character Sets
~~~~~~~~~~~~~~

In addition to the default character repertoire, the Defined Terms for
Specific Character Set in `table_title <#table_G.6.2-1>`__ are
supported:

.. table:: Supported Specific Character Set Defined Terms

   ========================= ============
   Character Set Description Defined Term
   ========================= ============
   Latin alphabet No. 1      ISO_IR 100
   ========================= ============

.. _sect_G.6.3:

Character Set Configuration
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Whether or not characters are displayed correctly depends on the
presence of font support in the underlying operating system.

.. _sect_G.7:

Security
--------

.. _sect_G.7.1:

Security Profiles
~~~~~~~~~~~~~~~~~

None supported.

.. _sect_G.7.2:

Association Level Security
~~~~~~~~~~~~~~~~~~~~~~~~~~

None supported.

Any Calling AE Titles and/or IP addresses may open an Association.

.. _sect_G.7.3:

Application Level Security
~~~~~~~~~~~~~~~~~~~~~~~~~~

None supported.

.. _sect_G.8:

Annexes
-------

.. _sect_G.8.1:

IOD Contents
~~~~~~~~~~~~

.. _sect_G.8.1.1:

Created SOP Instances
^^^^^^^^^^^^^^^^^^^^^

`table_title <#table_G.8.1-1>`__ specifies the attributes of a Hanging
Protocol Instance transmitted by the ImageViewer application.

The following tables use a number of abbreviations. The abbreviations
used in the "Presence of …" column are:

VNAP Value Not Always Present (attribute sent zero length if no value is
present)

ANAP Attribute Not Always Present

ALWAYS Always Present

EMPTY Attribute is sent without a value

The abbreviations used in the "Source" column:

USER the attribute value source is from User input

AUTO the attribute value is generated automatically

CONFIG the attribute value source is a configurable parameter

.. note::

   All dates and times are encoded in the local configured calendar and
   time. Date, Time and Time zone are configured using the
   Service/Installation Tool.

.. _sect_G.8.1.1.1:

Hanging Protocol IOD
''''''''''''''''''''

.. table:: IOD of Created Hanging Protocol SOP Instances

   +----------------+----------------+----------------+----------------+
   | IE             | Module         | Reference      | Presence of    |
   |                |                |                | Module         |
   +================+================+================+================+
   | Hanging        | SOP Common     | `tab           | ALWAYS         |
   | Protocol       |                | le_title <#tab |                |
   |                |                | le_G.8.1-2>`__ |                |
   +----------------+----------------+----------------+----------------+
   | Hanging        | `tab           | ALWAYS         |                |
   | Protocol       | le_title <#tab |                |                |
   | Definition     | le_G.8.1-3>`__ |                |                |
   +----------------+----------------+----------------+----------------+
   | Hanging        | `tab           | ALWAYS         |                |
   | Protocol       | le_title <#tab |                |                |
   | Environment    | le_G.8.1-4>`__ |                |                |
   +----------------+----------------+----------------+----------------+
   | Hanging        | `tab           | ALWAYS         |                |
   | Protocol       | le_title <#tab |                |                |
   | Display        | le_G.8.1-5>`__ |                |                |
   +----------------+----------------+----------------+----------------+

.. table:: SOP Common Module of Created SOP Instances

   +------------+------------+----+------------+------------+--------+
   | Attribute  | Tag        | VR | Value      | Presence   | Source |
   | Name       |            |    |            | of Value   |        |
   +============+============+====+============+============+========+
   | Specific   | (          | CS | From       | ALWAYS     | CONFIG |
   | Character  | 0008,0005) |    | `t         |            |        |
   | Set        |            |    | able_title |            |        |
   |            |            |    |  <#table_G |            |        |
   |            |            |    | .6.2-1>`__ |            |        |
   +------------+------------+----+------------+------------+--------+
   | SOP Class  | (          | UI | 1.2.       | ALWAYS     | AUTO   |
   | UID        | 0008,0016) |    | 840.10008. |            |        |
   |            |            |    | 5.1.4.38.1 |            |        |
   +------------+------------+----+------------+------------+--------+
   | SOP        | (          | UI | Generated  | ALWAYS     | AUTO   |
   | Instance   | 0008,0018) |    | by device  |            |        |
   | UID        |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+

.. table:: Hanging Protocol Definition Module of Created SOP Instances

   +----------+----------+------+----------+----------+----------+
   | A        | Tag      | VR   | Value    | Presence | Source   |
   | ttribute |          |      |          | of Value |          |
   | Name     |          |      |          |          |          |
   +==========+==========+======+==========+==========+==========+
   | Hanging  | (00      | SH   | From     | ALWAYS   | USER     |
   | Protocol | 72,0002) |      | user     |          |          |
   | Name     |          |      | input.   |          |          |
   +----------+----------+------+----------+----------+----------+
   | Hanging  | (00      | LO   | From     | ALWAYS   | USER     |
   | Protocol | 72,0004) |      | user     |          |          |
   | Des      |          |      | input.   |          |          |
   | cription |          |      |          |          |          |
   +----------+----------+------+----------+----------+----------+
   | Hanging  | (00      | CS   | From     | ALWAYS   | USER     |
   | Protocol | 72,0006) |      | user     |          |          |
   | Level    |          |      | input.   |          |          |
   +----------+----------+------+----------+----------+----------+
   | Hanging  | (00      | LO   | From     | ALWAYS   | AUTO     |
   | Protocol | 72,0008) |      | user     |          |          |
   | Creator  |          |      | login.   |          |          |
   +----------+----------+------+----------+----------+----------+
   | Hanging  | (00      | DT   | G        | ALWAYS   | AUTO     |
   | Protocol | 72,000A) |      | enerated |          |          |
   | Creation |          |      | by       |          |          |
   | Datetime |          |      | device.  |          |          |
   +----------+----------+------+----------+----------+----------+
   | Hanging  | (00      | SQ   | One or   | ALWAYS   | AUTO     |
   | Protocol | 72,000C) |      | more     |          |          |
   | De       |          |      | sequence |          |          |
   | finition |          |      | items.   |          |          |
   | Sequence |          |      |          |          |          |
   +----------+----------+------+----------+----------+----------+
   | >        | (00      | CS   | From     | ANAP     | U        |
   | Modality | 08,0060) |      | Defined  |          | SER/AUTO |
   |          |          |      | Terms,   |          |          |
   |          |          |      | based on |          |          |
   |          |          |      | user     |          |          |
   |          |          |      | input.   |          |          |
   +----------+----------+------+----------+----------+----------+
   | >        | (00      | SQ   | One or   | ANAP     | U        |
   | Anatomic | 08,2218) |      | more     |          | SER/AUTO |
   | Region   |          |      | sequence |          |          |
   | Sequence |          |      | items,   |          |          |
   |          |          |      | based on |          |          |
   |          |          |      | user     |          |          |
   |          |          |      | input.   |          |          |
   +----------+----------+------+----------+----------+----------+
   | *>       | *        |      |          |          |          |
   | >Include | Defined* |      |          |          |          |
   | 'Code    |          |      |          |          |          |
   | Sequence |          |      |          |          |          |
   | Macro'*  |          |      |          |          |          |
   +----------+----------+------+----------+----------+----------+
   | >La      | (00      | CS   | R, L, B, | ANAP     | U        |
   | terality | 20,0060) |      | U or     |          | SER/AUTO |
   |          |          |      | zero     |          |          |
   |          |          |      | length,  |          |          |
   |          |          |      | based on |          |          |
   |          |          |      | user     |          |          |
   |          |          |      | input.   |          |          |
   +----------+----------+------+----------+----------+----------+
   | >        | (00      | SQ   | Zero     | EMPTY    | AUTO     |
   | P        | 08,1032) |      | length.  |          |          |
   | rocedure |          |      |          |          |          |
   | Code     |          |      |          |          |          |
   | Sequence |          |      |          |          |          |
   +----------+----------+------+----------+----------+----------+
   | >Reason  | (00      | SQ   | Zero     | EMPTY    | AUTO     |
   | for      | 40,100A) |      | length.  |          |          |
   | R        |          |      |          |          |          |
   | equested |          |      |          |          |          |
   | P        |          |      |          |          |          |
   | rocedure |          |      |          |          |          |
   | Code     |          |      |          |          |          |
   | Sequence |          |      |          |          |          |
   +----------+----------+------+----------+----------+----------+
   | Number   | (00      | US   | Numeric  | ALWAYS   | AUTO     |
   | of       | 72,0014) |      | value.   |          |          |
   | Priors   |          |      |          |          |          |
   | Re       |          |      |          |          |          |
   | ferenced |          |      |          |          |          |
   +----------+----------+------+----------+----------+----------+
   | Image    | (00      | SQ   | One or   | ALWAYS   | AUTO     |
   | Sets     | 72,0020) |      | more     |          |          |
   | Sequence |          |      | sequence |          |          |
   |          |          |      | items.   |          |          |
   +----------+----------+------+----------+----------+----------+
   | >Image   | (00      | SQ   | One or   | ALWAYS   | AUTO     |
   | Set      | 72,0022) |      | more     |          |          |
   | Selector |          |      | sequence |          |          |
   | Sequence |          |      | items.   |          |          |
   +----------+----------+------+----------+----------+----------+
   | >>Image  | (00      | CS   | MATCH or | ALWAYS   | AUTO     |
   | Set      | 72,0024) |      | N        |          |          |
   | Selector |          |      | O_MATCH, |          |          |
   | Usage    |          |      | d        |          |          |
   | Flag     |          |      | epending |          |          |
   |          |          |      | on       |          |          |
   |          |          |      | Selector |          |          |
   |          |          |      | At       |          |          |
   |          |          |      | tribute. |          |          |
   +----------+----------+------+----------+----------+----------+
   | >>       | (00      | AT   | Relevant | ALWAYS   | AUTO     |
   | Selector | 72,0026) |      | A        |          |          |
   | A        |          |      | ttribute |          |          |
   | ttribute |          |      | Tags     |          |          |
   |          |          |      | from     |          |          |
   |          |          |      | DICOM    |          |          |
   |          |          |      | Data     |          |          |
   |          |          |      | Dic      |          |          |
   |          |          |      | tionary. |          |          |
   +----------+----------+------+----------+----------+----------+
   | >>       | (00      | AT   | Relevant | ANAP     | AUTO     |
   | Selector | 72,0052) |      | Sequence |          |          |
   | Sequence |          |      | A        |          |          |
   | Pointer  |          |      | ttribute |          |          |
   |          |          |      | Tags     |          |          |
   |          |          |      | from     |          |          |
   |          |          |      | DICOM    |          |          |
   |          |          |      | Data     |          |          |
   |          |          |      | Dic      |          |          |
   |          |          |      | tionary, |          |          |
   |          |          |      | if       |          |          |
   |          |          |      | Selector |          |          |
   |          |          |      | A        |          |          |
   |          |          |      | ttribute |          |          |
   |          |          |      | is       |          |          |
   |          |          |      | nested   |          |          |
   |          |          |      | in a     |          |          |
   |          |          |      | S        |          |          |
   |          |          |      | equence. |          |          |
   +----------+----------+------+----------+----------+----------+
   | >>       | (00      | CS   | VR of    | ALWAYS   | AUTO     |
   | Selector | 72,0050) |      | Selector |          |          |
   | A        |          |      | A        |          |          |
   | ttribute |          |      | ttribute |          |          |
   | VR       |          |      |          |          |          |
   +----------+----------+------+----------+----------+----------+
   | >>The    | ALWAYS   | AUTO |          |          |          |
   | a        |          |      |          |          |          |
   | ttribute |          |      |          |          |          |
   | from the |          |      |          |          |          |
   | Hanging  |          |      |          |          |          |
   | Protocol |          |      |          |          |          |
   | Selector |          |      |          |          |          |
   | A        |          |      |          |          |          |
   | ttribute |          |      |          |          |          |
   | Value    |          |      |          |          |          |
   | Macro    |          |      |          |          |          |
   | that is  |          |      |          |          |          |
   | required |          |      |          |          |          |
   | by the   |          |      |          |          |          |
   | value of |          |      |          |          |          |
   | Selector |          |      |          |          |          |
   | A        |          |      |          |          |          |
   | ttribute |          |      |          |          |          |
   | VR.      |          |      |          |          |          |
   +----------+----------+------+----------+----------+----------+
   | >>       | (00      | US   | 0,1-n    | ALWAYS   | AUTO     |
   | Selector | 72,0028) |      |          |          |          |
   | Value    |          |      |          |          |          |
   | Number   |          |      |          |          |          |
   +----------+----------+------+----------+----------+----------+
   | >Time    | (00      | SQ   | One or   | ALWAYS   | AUTO     |
   | Based    | 72,0030) |      | more     |          |          |
   | Image    |          |      | sequence |          |          |
   | Sets     |          |      | items.   |          |          |
   | Sequence |          |      |          |          |          |
   +----------+----------+------+----------+----------+----------+
   | >>Image  | (00      | US   | G        | ALWAYS   | AUTO     |
   | Set      | 72,0032) |      | enerated |          |          |
   | Number   |          |      | by       |          |          |
   |          |          |      | device.  |          |          |
   +----------+----------+------+----------+----------+----------+
   | >>Image  | (00      | CS   | RELAT    | ALWAYS   | AUTO     |
   | Set      | 72,0034) |      | IVE_TIME |          |          |
   | Selector |          |      | or       |          |          |
   | Category |          |      | ABSTRAC  |          |          |
   |          |          |      | T_PRIOR, |          |          |
   |          |          |      | based on |          |          |
   |          |          |      | user     |          |          |
   |          |          |      | input.   |          |          |
   +----------+----------+------+----------+----------+----------+
   | >>       | (00      | US   | From     | ANAP     | USER     |
   | Relative | 72,0038) |      | user     |          |          |
   | Time     |          |      | input.   |          |          |
   +----------+----------+------+----------+----------+----------+
   | >>       | (00      | CS   | From     | ANAP     | USER     |
   | Relative | 72,003A) |      | user     |          |          |
   | Time     |          |      | input.   |          |          |
   | Units    |          |      |          |          |          |
   +----------+----------+------+----------+----------+----------+
   | >>       | (00      | SS   | From     | ANAP     | USER     |
   | Abstract | 72,003C) |      | user     |          |          |
   | Prior    |          |      | input.   |          |          |
   | Value    |          |      |          |          |          |
   +----------+----------+------+----------+----------+----------+
   | >>Image  | (00      | LO   | From     | ANAP     | USER     |
   | Set      | 72,0040) |      | user     |          |          |
   | Label    |          |      | input.   |          |          |
   +----------+----------+------+----------+----------+----------+
   | Hanging  | (00      | SQ   | One      | ALWAYS   | U        |
   | Protocol | 72,000E) |      | sequence |          | SER/AUTO |
   | User     |          |      | item.    |          |          |
   | Identi   |          |      |          |          |          |
   | fication |          |      |          |          |          |
   | Code     |          |      |          |          |          |
   | Sequence |          |      |          |          |          |
   +----------+----------+------+----------+----------+----------+
   | *>       | *Local   |      |          |          |          |
   | >Include | coded    |      |          |          |          |
   | 'Code    | terms    |      |          |          |          |
   | Sequence | for      |      |          |          |          |
   | Macro'*  | users*   |      |          |          |          |
   +----------+----------+------+----------+----------+----------+
   | Hanging  | (00      | LO   | From     | ANAP     | U        |
   | Protocol | 72,0010) |      | user     |          | SER/AUTO |
   | User     |          |      | input.   |          |          |
   | Group    |          |      |          |          |          |
   | Name     |          |      |          |          |          |
   +----------+----------+------+----------+----------+----------+

.. table:: Hanging Protocol Environment Module of Created SOP Instances

   +------------+------------+----+------------+------------+--------+
   | Attribute  | Tag        | VR | Value      | Presence   | Source |
   | Name       |            |    |            | of Value   |        |
   +============+============+====+============+============+========+
   | Number of  | (          | US | 2          | ALWAYS     | AUTO   |
   | Screens    | 0072,0100) |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | Nominal    | (          | SQ | Two        | ALWAYS     | AUTO   |
   | Screen     | 0072,0102) |    | sequence   |            |        |
   | Definition |            |    | items.     |            |        |
   | Sequence   |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | >Number of | (          | US | 1024       | ALWAYS     | AUTO   |
   | Vertical   | 0072,0104) |    |            |            |        |
   | Pixels     |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | >Number of | (          | US | 1280       | ALWAYS     | AUTO   |
   | Horizontal | 0072,0106) |    |            |            |        |
   | Pixels     |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | >Display   | (          | FD | Sequence   | ALWAYS     | AUTO   |
   | E          | 0072,0108) |    | Item 1:    |            |        |
   | nvironment |            |    | 0.0|1      |            |        |
   | Spatial    |            |    | .0|0.5|0.0 |            |        |
   | Position   |            |    |            |            |        |
   |            |            |    | Sequence   |            |        |
   |            |            |    | Item 2:    |            |        |
   |            |            |    | 0.5|1      |            |        |
   |            |            |    | .0|1.0|0.0 |            |        |
   +------------+------------+----+------------+------------+--------+
   | >Screen    | (          | US | 8          | ALWAYS     | AUTO   |
   | Minimum    | 0072,010C) |    |            |            |        |
   | Color Bit  |            |    |            |            |        |
   | Depth      |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+

.. table:: Hanging Protocol Display Module of Created SOP Instances

   +----------+----------+------+----------+----------+----------+
   | A        | Tag      | VR   | Value    | Presence | Source   |
   | ttribute |          |      |          | of Value |          |
   | Name     |          |      |          |          |          |
   +==========+==========+======+==========+==========+==========+
   | Display  | (00      | SQ   | One or   | ALWAYS   | AUTO     |
   | Sets     | 72,0200) |      | more     |          |          |
   | Sequence |          |      | sequence |          |          |
   |          |          |      | items.   |          |          |
   +----------+----------+------+----------+----------+----------+
   | >Display | (00      | US   | G        | ALWAYS   | AUTO     |
   | Set      | 72,0202) |      | enerated |          |          |
   | Number   |          |      | by       |          |          |
   |          |          |      | device.  |          |          |
   +----------+----------+------+----------+----------+----------+
   | >Display | (00      | LO   | From     | ANAP     | USER     |
   | Set      | 72,0203) |      | user     |          |          |
   | Label    |          |      | input    |          |          |
   +----------+----------+------+----------+----------+----------+
   | >Display | (00      | US   | 1        | ALWAYS   | AUTO     |
   | Set      | 72,0204) |      |          |          |          |
   | Pres     |          |      |          |          |          |
   | entation |          |      |          |          |          |
   | Group    |          |      |          |          |          |
   +----------+----------+------+----------+----------+----------+
   | >Image   | (00      | US   | De       | ALWAYS   | AUTO     |
   | Set      | 72,0032) |      | termined |          |          |
   | Number   |          |      | by       |          |          |
   |          |          |      | appl     |          |          |
   |          |          |      | ication. |          |          |
   +----------+----------+------+----------+----------+----------+
   | >Image   | (00      | SQ   | One      | ALWAYS   | AUTO     |
   | Boxes    | 72,0300) |      | sequence |          |          |
   | Sequence |          |      | item.    |          |          |
   +----------+----------+------+----------+----------+----------+
   | >>Image  | (00      | US   | G        | ALWAYS   | AUTO     |
   | Box      | 72,0302) |      | enerated |          |          |
   | Number   |          |      | by       |          |          |
   |          |          |      | device.  |          |          |
   +----------+----------+------+----------+----------+----------+
   | >        | (00      | FD   | De       | ALWAYS   | AUTO     |
   | >Display | 72,0108) |      | termined |          |          |
   | Env      |          |      | by       |          |          |
   | ironment |          |      | app      |          |          |
   | Spatial  |          |      | lication |          |          |
   | Position |          |      | with     |          |          |
   |          |          |      | user     |          |          |
   |          |          |      | input.   |          |          |
   +----------+----------+------+----------+----------+----------+
   | >>Image  | (00      | CS   | TILED,   | ALWAYS   | AUTO     |
   | Box      | 72,0304) |      | STACK or |          |          |
   | Layout   |          |      | SINGLE,  |          |          |
   | Type     |          |      | de       |          |          |
   |          |          |      | termined |          |          |
   |          |          |      | by       |          |          |
   |          |          |      | app      |          |          |
   |          |          |      | lication |          |          |
   |          |          |      | with     |          |          |
   |          |          |      | user     |          |          |
   |          |          |      | input.   |          |          |
   +----------+----------+------+----------+----------+----------+
   | >>Image  | (00      | US   | For      | ANAP     | AUTO     |
   | Box Tile | 72,0306) |      | TILED,   |          |          |
   | Ho       |          |      | de       |          |          |
   | rizontal |          |      | termined |          |          |
   | D        |          |      | by       |          |          |
   | imension |          |      | app      |          |          |
   |          |          |      | lication |          |          |
   |          |          |      | with     |          |          |
   |          |          |      | user     |          |          |
   |          |          |      | input.   |          |          |
   +----------+----------+------+----------+----------+----------+
   | >>Image  | (00      | US   | For      | ANAP     | AUTO     |
   | Box Tile | 72,0308) |      | TILED,   |          |          |
   | Vertical |          |      | de       |          |          |
   | D        |          |      | termined |          |          |
   | imension |          |      | by       |          |          |
   |          |          |      | app      |          |          |
   |          |          |      | lication |          |          |
   |          |          |      | with     |          |          |
   |          |          |      | user     |          |          |
   |          |          |      | input.   |          |          |
   +----------+----------+------+----------+----------+----------+
   | >>Image  | (00      | CS   | For      | ANAP     | AUTO     |
   | Box      | 72,0310) |      | TILED,   |          |          |
   | Scroll   |          |      | VERTICAL |          |          |
   | D        |          |      | or       |          |          |
   | irection |          |      | HOR      |          |          |
   |          |          |      | IZONTAL, |          |          |
   |          |          |      | de       |          |          |
   |          |          |      | termined |          |          |
   |          |          |      | by       |          |          |
   |          |          |      | app      |          |          |
   |          |          |      | lication |          |          |
   |          |          |      | with     |          |          |
   |          |          |      | user     |          |          |
   |          |          |      | input.   |          |          |
   +----------+----------+------+----------+----------+----------+
   | >>Image  | (00      | CS   | For      | ANAP     | AUTO     |
   | Box      | 72,0312) |      | TILED    |          |          |
   | Small    |          |      | only,    |          |          |
   | Scroll   |          |      | value is |          |          |
   | Type     |          |      | IMAGE.   |          |          |
   +----------+----------+------+----------+----------+----------+
   | >>Image  | (00      | US   | For      | ANAP     | AUTO     |
   | Box      | 72,0314) |      | TILED    |          |          |
   | Small    |          |      | only,    |          |          |
   | Scroll   |          |      | value is |          |          |
   | Amount   |          |      | 1.       |          |          |
   +----------+----------+------+----------+----------+----------+
   | >>Image  | (00      | CS   | For      | ANAP     | AUTO     |
   | Box      | 72,0316) |      | TILED    |          |          |
   | Large    |          |      | only,    |          |          |
   | Scroll   |          |      | value is |          |          |
   | Type     |          |      | ROW      |          |          |
   |          |          |      | _COLUMN. |          |          |
   +----------+----------+------+----------+----------+----------+
   | >>Image  | (00      | US   | For      | ANAP     | AUTO     |
   | Box      | 72,0318) |      | TILED    |          |          |
   | Large    |          |      | only,    |          |          |
   | Scroll   |          |      | value is |          |          |
   | Amount   |          |      | 1.       |          |          |
   +----------+----------+------+----------+----------+----------+
   | >Filter  | (00      | SQ   | Zero or  | VNAP     | AUTO     |
   | Op       | 72,0400) |      | more     |          |          |
   | erations |          |      | sequence |          |          |
   | Sequence |          |      | items.   |          |          |
   +----------+----------+------+----------+----------+----------+
   | >>F      | (00      | CS   | IMA      | ANAP     | U        |
   | ilter-by | 72,0402) |      | GE_PLANE |          | SER/AUTO |
   | Category |          |      | if       |          |          |
   |          |          |      | present. |          |          |
   +----------+----------+------+----------+----------+----------+
   | >>       | (00      | AT   | (00      | ANAP     | U        |
   | Selector | 72,0026) |      | 08,0008) |          | SER/AUTO |
   | A        |          |      | Image    |          |          |
   | ttribute |          |      | Type,    |          |          |
   |          |          |      | (00      |          |          |
   |          |          |      | 18,0010) |          |          |
   |          |          |      | Contra   |          |          |
   |          |          |      | st/Bolus |          |          |
   |          |          |      | Agent,   |          |          |
   |          |          |      | (00      |          |          |
   |          |          |      | 18,0086) |          |          |
   |          |          |      | Echo     |          |          |
   |          |          |      | Number,  |          |          |
   |          |          |      | (00      |          |          |
   |          |          |      | 18,5101) |          |          |
   |          |          |      | View     |          |          |
   |          |          |      | P        |          |          |
   |          |          |      | osition, |          |          |
   |          |          |      | (00      |          |          |
   |          |          |      | 54,0220) |          |          |
   |          |          |      | View     |          |          |
   |          |          |      | Code     |          |          |
   |          |          |      | S        |          |          |
   |          |          |      | equence, |          |          |
   |          |          |      | (00      |          |          |
   |          |          |      | 54,0222) |          |          |
   |          |          |      | View     |          |          |
   |          |          |      | Modifier |          |          |
   |          |          |      | Code     |          |          |
   |          |          |      | S        |          |          |
   |          |          |      | equence. |          |          |
   +----------+----------+------+----------+----------+----------+
   | >>       | (00      | AT   | Relevant | ANAP     | AUTO     |
   | Selector | 72,0052) |      | Sequence |          |          |
   | Sequence |          |      | A        |          |          |
   | Pointer  |          |      | ttribute |          |          |
   |          |          |      | Tags     |          |          |
   |          |          |      | from     |          |          |
   |          |          |      | DICOM    |          |          |
   |          |          |      | Data     |          |          |
   |          |          |      | Dic      |          |          |
   |          |          |      | tionary, |          |          |
   |          |          |      | if       |          |          |
   |          |          |      | Selector |          |          |
   |          |          |      | A        |          |          |
   |          |          |      | ttribute |          |          |
   |          |          |      | is       |          |          |
   |          |          |      | nested   |          |          |
   |          |          |      | in a     |          |          |
   |          |          |      | S        |          |          |
   |          |          |      | equence, |          |          |
   |          |          |      | such as  |          |          |
   |          |          |      | (00      |          |          |
   |          |          |      | 54,0220) |          |          |
   |          |          |      | View     |          |          |
   |          |          |      | Code     |          |          |
   |          |          |      | S        |          |          |
   |          |          |      | equence. |          |          |
   +----------+----------+------+----------+----------+----------+
   | >>       | (00      | CS   | VR of    | ANAP     | AUTO     |
   | Selector | 72,0050) |      | Selector |          |          |
   | A        |          |      | At       |          |          |
   | ttribute |          |      | tribute, |          |          |
   | VR       |          |      | if       |          |          |
   |          |          |      | present  |          |          |
   +----------+----------+------+----------+----------+----------+
   | >>The    | ANAP     | AUTO |          |          |          |
   | a        |          |      |          |          |          |
   | ttribute |          |      |          |          |          |
   | from the |          |      |          |          |          |
   | Hanging  |          |      |          |          |          |
   | Protocol |          |      |          |          |          |
   | Selector |          |      |          |          |          |
   | A        |          |      |          |          |          |
   | ttribute |          |      |          |          |          |
   | Value    |          |      |          |          |          |
   | Macro    |          |      |          |          |          |
   | that is  |          |      |          |          |          |
   | required |          |      |          |          |          |
   | by the   |          |      |          |          |          |
   | value of |          |      |          |          |          |
   | Selector |          |      |          |          |          |
   | A        |          |      |          |          |          |
   | ttribute |          |      |          |          |          |
   | VR, if   |          |      |          |          |          |
   | present. |          |      |          |          |          |
   +----------+----------+------+----------+----------+----------+
   | >>       | (00      | US   | 3 for    | ANAP     | AUTO     |
   | Selector | 72,0028) |      | (00      |          |          |
   | Value    |          |      | 08,0008) |          |          |
   | Number   |          |      | Image    |          |          |
   |          |          |      | Type, 1  |          |          |
   |          |          |      | for      |          |          |
   |          |          |      | other    |          |          |
   |          |          |      | Selector |          |          |
   |          |          |      | Att      |          |          |
   |          |          |      | ributes. |          |          |
   +----------+----------+------+----------+----------+----------+
   | >>F      | (00      | CS   | M        | ALWAYS   | USER     |
   | ilter-by | 72,0406) |      | EMBER_OF |          |          |
   | Operator |          |      | or       |          |          |
   |          |          |      | NOT_ME   |          |          |
   |          |          |      | MBER_OF. |          |          |
   +----------+----------+------+----------+----------+----------+
   | >Sorting | (00      | SQ   | Zero or  | VNAP     | AUTO     |
   | Op       | 72,0600) |      | more     |          |          |
   | erations |          |      | sequence |          |          |
   | Sequence |          |      | items.   |          |          |
   +----------+----------+------+----------+----------+----------+
   | >>       | (00      | AT   | (00      | ANAP     | USER     |
   | Selector | 72,0026) |      | 08,0032) |          |          |
   | A        |          |      | Acq      |          |          |
   | ttribute |          |      | uisition |          |          |
   |          |          |      | Time,    |          |          |
   |          |          |      | (00      |          |          |
   |          |          |      | 18,0086) |          |          |
   |          |          |      | Echo     |          |          |
   |          |          |      | Time,    |          |          |
   |          |          |      | (00      |          |          |
   |          |          |      | 20,0013) |          |          |
   |          |          |      | Instance |          |          |
   |          |          |      | Number.  |          |          |
   +----------+----------+------+----------+----------+----------+
   | >>       | (00      | AT   | Relevant | ANAP     | AUTO     |
   | Selector | 72,0052) |      | Sequence |          |          |
   | Sequence |          |      | A        |          |          |
   | Pointer  |          |      | ttribute |          |          |
   |          |          |      | Tags     |          |          |
   |          |          |      | from     |          |          |
   |          |          |      | DICOM    |          |          |
   |          |          |      | Data     |          |          |
   |          |          |      | Dic      |          |          |
   |          |          |      | tionary, |          |          |
   |          |          |      | if       |          |          |
   |          |          |      | Selector |          |          |
   |          |          |      | A        |          |          |
   |          |          |      | ttribute |          |          |
   |          |          |      | is       |          |          |
   |          |          |      | nested   |          |          |
   |          |          |      | in a     |          |          |
   |          |          |      | S        |          |          |
   |          |          |      | equence. |          |          |
   +----------+----------+------+----------+----------+----------+
   | >>       | (00      | US   | 1 for    | ANAP     | AUTO     |
   | Selector | 72,0028) |      | most     |          |          |
   | Value    |          |      | Selector |          |          |
   | Number   |          |      | Att      |          |          |
   |          |          |      | ributes, |          |          |
   |          |          |      | if       |          |          |
   |          |          |      | present. |          |          |
   +----------+----------+------+----------+----------+----------+
   | >        | (00      | CS   | AL       | ANAP     | USER     |
   | >Sort-by | 72,0602) |      | ONG_AXIS |          |          |
   | Category |          |      |          |          |          |
   +----------+----------+------+----------+----------+----------+
   | >        | (00      | CS   | IN       | ALWAYS   | USER     |
   | >Sorting | 72,0604) |      | CREASING |          |          |
   | D        |          |      | or       |          |          |
   | irection |          |      | DE       |          |          |
   |          |          |      | CREASING |          |          |
   +----------+----------+------+----------+----------+----------+
   | >Display | (00      | CS   | From     | ANAP     | U        |
   | Set      | 72,0700) |      | user     |          | SER/AUTO |
   | Patient  |          |      | input or |          |          |
   | Ori      |          |      | a        |          |          |
   | entation |          |      | utomated |          |          |
   |          |          |      | al       |          |          |
   |          |          |      | gorithm. |          |          |
   +----------+----------+------+----------+----------+----------+
   | >VOI     | (00      | CS   | From     | ANAP     | U        |
   | Type     | 72,0702) |      | user     |          | SER/AUTO |
   |          |          |      | input or |          |          |
   |          |          |      | a        |          |          |
   |          |          |      | utomated |          |          |
   |          |          |      | al       |          |          |
   |          |          |      | gorithm. |          |          |
   +----------+----------+------+----------+----------+----------+
   | >Show    | (00      | CS   | NO       | ALWAYS   | AUTO     |
   | Image    | 72,0710) |      |          |          |          |
   | True     |          |      |          |          |          |
   | Size     |          |      |          |          |          |
   | Flag     |          |      |          |          |          |
   +----------+----------+------+----------+----------+----------+
   | >Show    | (00      | CS   | YES      | ALWAYS   | AUTO     |
   | Graphic  | 72,0712) |      |          |          |          |
   | An       |          |      |          |          |          |
   | notation |          |      |          |          |          |
   | Flag     |          |      |          |          |          |
   +----------+----------+------+----------+----------+----------+
   | >Show    | (00      | CS   | YES      | ALWAYS   | AUTO     |
   | Patient  | 72,0714) |      |          |          |          |
   | Demo     |          |      |          |          |          |
   | graphics |          |      |          |          |          |
   | Flag     |          |      |          |          |          |
   +----------+----------+------+----------+----------+----------+
   | >Show    | (00      | CS   | YES      | ALWAYS   | AUTO     |
   | Acq      | 72,0716) |      |          |          |          |
   | uisition |          |      |          |          |          |
   | Te       |          |      |          |          |          |
   | chniques |          |      |          |          |          |
   | Flag     |          |      |          |          |          |
   +----------+----------+------+----------+----------+----------+
   | Partial  | (00      | CS   | MAINTAI  | ALWAYS   | AUTO     |
   | Data     | 72,0208) |      | N_LAYOUT |          |          |
   | Display  |          |      |          |          |          |
   | Handling |          |      |          |          |          |
   +----------+----------+------+----------+----------+----------+
   | Sync     | (00      | SQ   | Zero or  | ANAP     | U        |
   | hronized | 72,0210) |      | more     |          | SER/AUTO |
   | S        |          |      | sequence |          |          |
   | crolling |          |      | items,   |          |          |
   | Sequence |          |      | based on |          |          |
   |          |          |      | user     |          |          |
   |          |          |      | input or |          |          |
   |          |          |      | a        |          |          |
   |          |          |      | utomated |          |          |
   |          |          |      | al       |          |          |
   |          |          |      | gorithm. |          |          |
   +----------+----------+------+----------+----------+----------+
   | >Display | (00      | US   | Display  | ALWAYS   | AUTO     |
   | Set      | 72,0212) |      | Set      |          |          |
   | S        |          |      | numbers. |          |          |
   | crolling |          |      |          |          |          |
   | Group    |          |      |          |          |          |
   +----------+----------+------+----------+----------+----------+
   | Na       | (00      | SQ   | Zero or  | ANAP     | USER     |
   | vigation | 72,0214) |      | more     |          |          |
   | I        |          |      | sequence |          |          |
   | ndicator |          |      | items,   |          |          |
   | Sequence |          |      | based on |          |          |
   |          |          |      | user     |          |          |
   |          |          |      | input.   |          |          |
   +----------+----------+------+----------+----------+----------+
   | >Na      | (00      | US   | Display  | ANAP     | U        |
   | vigation | 72,0216) |      | Set      |          | SER/AUTO |
   | Display  |          |      | number,  |          |          |
   | Set      |          |      | user or  |          |          |
   |          |          |      | au       |          |          |
   |          |          |      | tomated. |          |          |
   +----------+----------+------+----------+----------+----------+
   | >R       | (00      | US   | Display  | ALWAYS   | U        |
   | eference | 72,0218) |      | Set      |          | SER/AUTO |
   | Display  |          |      | numbers, |          |          |
   | Sets     |          |      | user or  |          |          |
   |          |          |      | au       |          |          |
   |          |          |      | tomated. |          |          |
   +----------+----------+------+----------+----------+----------+

.. _sect_G.8.1.2:

Usage of Attributes From Received IODs
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

No SOP Class specific fields for images are required.

The Reformatting Operation Type (0072,0510) attribute with value MPR or
SLAB is supported for the MR Image Storage SOP Class only.

.. _sect_G.8.1.3:

Attribute Mapping
^^^^^^^^^^^^^^^^^

Not applicable.

.. _sect_G.8.1.4:

Coerced/Modified Fields
^^^^^^^^^^^^^^^^^^^^^^^

No coercion is performed.

.. _sect_G.8.2:

Data Dictionary of Private Attributes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

No private attributes are defined.

.. _sect_G.8.3:

Coded Terminology and Templates
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The value for Code Meaning will be displayed for all code sequences. No
local lexicon is provided to look up alternative code meanings.

.. _sect_G.8.4:

Grayscale Image Consistency
~~~~~~~~~~~~~~~~~~~~~~~~~~~

The high resolution display monitor attached to the product can be
calibrated according to the Grayscale Standard Display Function (GSDF).

.. _sect_G.8.5:

Standard Extended/Specialized/Private SOP Classes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

None

.. _sect_G.8.6:

Private Transfer Syntaxes
~~~~~~~~~~~~~~~~~~~~~~~~~

None.

