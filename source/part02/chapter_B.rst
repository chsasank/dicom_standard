.. _chapter_B:

Conformance Statement Sample Integrated Modality (Informative)
==============================================================

Disclaimer:

This document is an example DICOM Conformance Statement for a fictional
image acquisition modality called EXAMPLE-INTEGRATED-MODALITY produced
by a fictional vendor called EXAMPLE-IMAGING-PRODUCTS.

As stated in the annex title, this document is truly informative, and
not normative. A conformance statement of an actual product might
implement additional services and options as appropriate for its
specific purpose. In addition, an actual product might implement the
services described in a different manner and, for example, with
different characteristics and/or sequencing of activities. In other
words, this conformance statement example does not intend to standardize
a particular manner that a product might implement DICOM functionality.

.. _sect_B.0:

Cover Page
----------

Company Name: EXAMPLE-IMAGING-PRODUCTS.

Product Name: SAMPLE INTEGRATED MODALITY

Version: 1.0-rev. A.1

Internal document number: 4226-xxx-yyy-zzz rev 1

Date: YYYYMMDD

.. _sect_B.1:

Conformance Statement Overview
------------------------------

This fictional product EXAMPLE-INTEGRATED-MODALITY implements the
necessary DICOM services to download work lists from an information
system, save acquired RF images and associated Presentation States to a
network storage device or CD-R, print to a networked hardcopy device and
inform the information system about the work actually done.

`table_title <#table_B.1-1>`__ provides an overview of the network
services supported by EXAMPLE-INTEGRATED-MODALITY.

.. table:: Network Services

   +----------------------+----------------------+----------------------+
   | SOP Classes          | User of Service      | Provider of Service  |
   |                      | (SCU)                | (SCP)                |
   +======================+======================+======================+
   | Transfer             |                      |                      |
   +----------------------+----------------------+----------------------+
   | X-Ray                | Yes                  | No                   |
   | Radiofluoroscopic    |                      |                      |
   | Image Storage        |                      |                      |
   +----------------------+----------------------+----------------------+
   | Grayscale Softcopy   | Yes                  | No                   |
   | Presentation State   |                      |                      |
   +----------------------+----------------------+----------------------+
   | Workflow Management  |                      |                      |
   +----------------------+----------------------+----------------------+
   | Modality Worklist    | Yes                  | No                   |
   +----------------------+----------------------+----------------------+
   | Storage Commitment   | Yes                  | No                   |
   | Push Model           |                      |                      |
   +----------------------+----------------------+----------------------+
   | Modality Performed   | Yes                  | No                   |
   | Procedure Step       |                      |                      |
   +----------------------+----------------------+----------------------+
   | Print Management     |                      |                      |
   +----------------------+----------------------+----------------------+
   | Basic Grayscale      | Option (see Note 1)  | No                   |
   | Print Management     |                      |                      |
   +----------------------+----------------------+----------------------+
   | Presentation LUT     | Option (see Note 1)  | No                   |
   +----------------------+----------------------+----------------------+

.. note::

   1. Support for the Print Services is a separately licensable option.
      Details about licensable options can be found
      under:http://www.example-imaging-products.nocom/example­integrated-modality/licence-options

`table_title <#table_B.1-2>`__ provides an overview of the Media Storage
Application Profiles supported by Example-Integrated-Modality.

.. table:: Media Services

   +------------------------+------------------------+------------------+
   | Media Storage          | Write Files (FSC or    | Read Files (FSR) |
   | Application Profile    | FSU)                   |                  |
   +========================+========================+==================+
   | Compact Disk -         |                        |                  |
   | Recordable             |                        |                  |
   +------------------------+------------------------+------------------+
   | General Purpose CD-R   | Yes                    | No               |
   +------------------------+------------------------+------------------+

.. _sect_B.2:

Table of Contents
-----------------

A table of contents shall be provided to assist readers in easily
finding the needed information.

.. _sect_B.3:

Introduction
------------

.. _sect_B.3.1:

Revision History
~~~~~~~~~~~~~~~~

.. table:: Revision History

   ================ ================ ====== ======================
   Document Version Date of Issue    Author Description
   ================ ================ ====== ======================
   1.1              October 30, 2003 WG 6   Version for Final Text
   1.2              August 30, 2007  WG 6   Revised Introduction
   ================ ================ ====== ======================

.. _sect_B.3.2:

Audience, Remarks, Terms and Definitions, Basics of DICOM Communication, Abbreviations, References
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

*See example text in*\ `Introduction <#sect_A.3>`__\ *.*

.. _sect_B.3.3:

Additional Remarks for This Example
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This document is a sample DICOM Conformance Statement created for DICOM
. It is to be used solely as an example to illustrate how to create a
DICOM Conformance Statement for an acquisition modality. The subject of
the document, EXAMPLE-INTEGRATED-MODALITY, is a fictional product.

.. _sect_B.4:

Networking
----------

.. _sect_B.4.1:

Implementation Model
~~~~~~~~~~~~~~~~~~~~

.. _sect_B.4.1.1:

Application Data Flow
^^^^^^^^^^^^^^^^^^^^^

-  The Storage Application Entity sends images and Presentation States
   to a remote AE. It is associated with the local real-world activity
   "Send Images & GSPS". "Send Images & GSPS" is performed upon user
   request for each study completed or for specific images selected.
   When activated by user's settings (auto-send), each marked set of
   images and associated Presentation States can be immediately stored
   to a preferred destination whenever a Patient/Study is closed by the
   user. If the remote AE is configured as an archive device the Storage
   AE will request Storage Commitment and if a commitment is
   successfully obtained will record this information in the local
   database.

-  The Workflow Application Entity receives Worklist information from
   and sends MPPS information to a remote AE. It is associated with the
   local real-world activities "Update Worklist" and "Acquire Images".
   When the "Update Worklist" local real-world activity is performed the
   Workflow Application Entity queries a remote AE for worklist items
   and provides the set of worklist items matching the query request.
   "Update Worklist" is performed as a result of an operator request or
   can be performed automatically at specific time intervals. When the
   "Acquire Images" local real-world activity is performed the Workflow
   Application Entity creates and updates Modality Performed Procedure
   Step instances managed by a remote AE. Acquisition of images will
   result in automated creation of an MPPS Instance. Completion of the
   MPPS is performed as the result of an operator action.

-  The Hardcopy Application Entity prints images on a remote AE
   (Printer). It is associated with the local real-world activity "Film
   Images". "Film Images" creates a print-job within the print queue
   containing one or more virtual film sheets composed from images
   selected by the user.

.. _sect_B.4.1.2:

Functional Definition of AEs
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. _sect_B.4.1.2.1:

Functional Definition of Storage Application Entity
'''''''''''''''''''''''''''''''''''''''''''''''''''

The existence of a send-job queue entry with associated network
destination will activate the Storage AE. An association request is sent
to the destination AE and upon successful negotiation of a Presentation
Context the image transfer is started. If the association cannot be
opened, the related send-job is set to an error state and can be
restarted by the user via job control interface. By default, the Storage
AE will not try to initiate another association for this send-job
automatically. However, an automatic retry (retry-timer, retry­count)
can be configured by a CSE.

.. _sect_B.4.1.2.2:

Functional Definition of Workflow Application Entity
''''''''''''''''''''''''''''''''''''''''''''''''''''

Worklist Update attempts to download a Worklist from a remote node. If
the Workflow AE establishes an Association to a remote AE, it will
transfer all worklist items via the open Association. During receiving
the worklist response items are counted and the query processing is
canceled if the configurable limit of items is reached. The results will
be displayed in a separate list, which will be cleared with the next
Worklist Update.

The Workflow AE performs the creation of a MPPS Instance automatically
whenever images are acquired. Further updates on the MPPS data can be
performed interactively from the related MPPS user interface. The MPPS
"Complete" or "Discontinued" states can only be set from the user
interface.

.. _sect_B.4.1.2.3:

Functional Definition of Hardcopy Application Entity
''''''''''''''''''''''''''''''''''''''''''''''''''''

The existence of a print-job in the print queue will activate the
Hardcopy AE. An association is established with the printer and the
printer's status determined. If the printer is operating normally, the
film sheets described within the print-job will be printed. Changes in
printer status will be detected (e.g., out of film) and reported to the
user. If the printer is not operating normally, the print-job will set
to an error state and can be restarted by the user via the job control
interface.

.. _sect_B.4.1.3:

Sequencing of Real-World Activities
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Under normal scheduled workflow conditions the sequencing constraints
illustrated in `figure_title <#figure_B.4.1-2>`__ apply:

1. Query Worklist

2. Receive Worklist of Modality Scheduled Procedure Steps (MSPS)

3. Select Workitem (MSPS) from Worklist

4. Start acquisition and create MPPS

5. Acquire Images

6. Complete acquisition and finalize MPPS

7. Print acquired images (optional step)

8. Store acquired images and any associated Grayscale Softcopy
   Presentation State (GSPS) instances.

9. If the Image Manager is configured as an archive device the Storage
   AE will request Storage Commitment for the images and associated GSPS
   instances.

Other workflow situations (e.g., unscheduled procedure steps) will have
other sequencing constraints. Printing could equally take place after
the acquired images have been stored. Printing could be omitted
completely if no printer is connected or hard copies are not required.

.. _sect_B.4.2:

AE Specifications
~~~~~~~~~~~~~~~~~

.. _sect_B.4.2.1:

Storage Application Entity Specification
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. _sect_B.4.2.1.1:

SOP Classes
'''''''''''

EXAMPLE-INTEGRATED-MODALITY provides Standard Conformance to the
following SOP Classes:

.. table:: SOP Classes for AE Storage

   +---------------------------+---------------------------+-----+-----+
   | SOP Class Name            | SOP Class UID             | SCU | SCP |
   +===========================+===========================+=====+=====+
   | X-Ray Radiofluoroscopic   | 1.2                       | Yes | No  |
   | Image Storage             | .840.10008.5.1.4.1.1.12.2 |     |     |
   +---------------------------+---------------------------+-----+-----+
   | Grayscale Softcopy        | 1.2                       | Yes | No  |
   | Presentation State        | .840.10008.5.1.4.1.1.11.1 |     |     |
   | Storage                   |                           |     |     |
   +---------------------------+---------------------------+-----+-----+
   | Storage Commitment Push   | 1.2.840.10008.1.20.1      | Yes | No  |
   | Model                     |                           |     |     |
   +---------------------------+---------------------------+-----+-----+
   | Verification              | 1.2.840.10008.1.1         | No  | Yes |
   +---------------------------+---------------------------+-----+-----+

.. _sect_B.4.2.1.2:

Association Policies
''''''''''''''''''''

.. _sect_B.4.2.1.2.1:

General
       

The DICOM standard application context name for DICOM is always
proposed:

.. table:: DICOM Application Context for AE Storage

   ======================== =====================
   Application Context Name 1.2.840.10008.3.1.1.1
   ======================== =====================

.. _sect_B.4.2.1.2.2:

Number of Associations
                      

EXAMPLE-INTEGRATED-MODALITY initiates one Association at a time for each
destination to which a transfer request is being processed in the active
job queue list. Only one job will be active at a time, the other remains
pending until the active job is completed or failed.

.. table:: Number of Associations Initiated for AE Storage

   =========================================== ================
   Maximum number of simultaneous Associations 1 (configurable)
   =========================================== ================

EXAMPLE-INTEGRATED-MODALITY accepts Associations to receive
N-EVENT-REPORT notifications for the Storage Commitment Push Model SOP
Class.

.. table:: Number of Associations Accepted for AE Storage

   =========================================== ================
   Maximum number of simultaneous Associations 5 (configurable)
   =========================================== ================

.. _sect_B.4.2.1.2.3:

Asynchronous Nature
                   

EXAMPLE-INTEGRATED-MODALITY does not support asynchronous communication
(multiple outstanding transactions over a single Association).

.. table:: Asynchronous Nature as a SCU for AE Storage

   ======================================================= =
   Maximum number of outstanding asynchronous transactions 1
   ======================================================= =

.. _sect_B.4.2.1.2.4:

Implementation Identifying Information
                                      

The implementation information for this Application Entity is:

.. table:: DICOM Implementation Class and Version for AE Storage

   =========================== ============================
   Implementation Class UID    1.xxxxxxx.yyy.etc.ad.inf.usw
   Implementation Version Name EXINTMOD_01
   =========================== ============================

.. _sect_B.4.2.1.3:

Association Initiation Policy
'''''''''''''''''''''''''''''

.. _sect_B.4.2.1.3.1:

Activity - Send Images
                      

.. _sect_B.4.2.1.3.1.1:

Description and Sequencing of Activities
                                        

A user can select images and presentation states and request them to be
sent to multiple destinations (up to 3). Each request is forwarded to
the job queue and processed individually. When the "Auto-send" option is
active, each marked instance or marked set of instances stored in
database will be forwarded to the network job queue for a pre-configured
auto-send target destination. Which instances will be automatically
marked and the destination where the instances are automatically sent to
can be configured. The "Auto-send" is triggered by the Close Patient
user application.

The Storage AE is invoked by the job control interface that is
responsible for processing network archival tasks. The job consists of
data describing the instances marked for storage and the destination. An
internal daemon process triggered by a job for a specific network
destination initiates a C-STORE request to store images. If the process
successfully establishes an Association to a remote Application Entity,
it will transfer each marked instance one after another via the open
Association. Status of the transfer is reported through the job control
interface. Only one job will be active at a time. If the C-STORE
Response from the remote Application contains a status other than
Success or Warning, the Association is aborted and the related Job is
switched to a failed state. It can be restarted any time by user
interaction or, if configured, by automated retry.

The Storage AE attempts to initiate a new Association in order to issue
a C-STORE request. If the job contains multiple images then multiple
C-STORE requests will be issued over the same Association.

If the Remote AE is configured as an archive device the Storage AE will,
after all images and presentation states have been sent, transmit a
single Storage Commitment request (N-ACTION) over the same Association.
Upon receiving the N-ACTION response the Storage AE will delay releasing
the Association for a configurable amount of time. If no N-EVENT-REPORT
is received within this time period the Association will be immediately
released (i.e., notification of Storage Commitment success or failure
will be received over a separate association). However, the Storage AE
is capable of receiving an N-EVENT-REPORT request at any time during an
association provided a Presentation Context for the Storage Commitment
Push Model has been successfully negotiated (i.e., the N-ACTION is sent
at the end of one association and the N-EVENT-REPORT is received during
an association initiated for a subsequent send job or during an
association initiated by the Remote AE for the specific purpose of
sending the N-EVENT-REPORT).

A possible sequence of interactions between the Storage AE and an Image
Manager (e.g., a storage or archive device supporting the Storage and
Storage Commitment SOP Classes as an SCP) is illustrated in
`figure_title <#figure_B.4.2-1>`__:

1. The Storage AE opens an association with the Image Manager

2. An acquired RF image is transmitted to the Image Manager using a
   C-STORE request and the Image Manager replies with a C-STORE response
   (status success).

3. A GSPS instance is transmitted to the Image Manager using a C-STORE
   request and the Image Manager replies with a C-STORE response (status
   success).

4. Another acquired RF image is transmitted to the Image Manager using a
   C-STORE request and the Image Manager replies with a C-STORE response
   (status success).

5. Another GSPS instance is transmitted to the Image Manager using a
   C-STORE request and the Image Manager replies with a C-STORE response
   (status success).

6. An N-ACTION request is transmitted to the Image Manager to obtain
   storage commitment of previously transmitted RF images and GSPS
   instances. The Image Manager replies with a N-ACTION response
   indicating the request has been received and is being processed.

7. The Image Manager immediately transmits an N-EVENT-REPORT request
   notifying the Storage AE of the status of the Storage Commitment
   Request (sent in step 6 using the N-ACTION message). The Storage AE
   replies with a N-EVENT-REPORT response confirming receipt. The Image
   Manager could send this message at any time or omit it entirely in
   favor of transmitting the N-EVENT-REPORT over a separate dedicated
   association (see note).

8. The Storage AE closes the association with the Image Manager.

.. note::

   Many other message sequences are possible depending on the number of
   images and GSPS instances to be stored, support for Storage
   Commitment and when the SCP sends the N-EVENT-REPORT. The
   N-EVENT-REPORT can also be sent over a separate association initiated
   by the Image Manager (see `Activity - Receive Storage Commitment
   Response <#sect_B.4.2.1.4.1>`__ on Activity - Receive Storage
   Commitment Response).

.. _sect_B.4.2.1.3.1.2:

Proposed Presentation Contexts
                              

EXAMPLE-INTEGRATED-MODALITY is capable of proposing the Presentation
Contexts shown in the following table:

.. table:: Proposed Presentation Contexts for Activity Send Images

   +------------+------------+------------+------------+-----+------+
   | Pr         |            |            |            |     |      |
   | esentation |            |            |            |     |      |
   | Context    |            |            |            |     |      |
   | Table      |            |            |            |     |      |
   +============+============+============+============+=====+======+
   | X-Ray      | 1.2.840.   | Implicit   | 1.2.840    | SCU | None |
   | Radio      | 10008.5.1. | VR Little  | .10008.1.2 |     |      |
   | Fl         | 4.1.1.12.2 | Endian     |            |     |      |
   | uoroscopic |            |            | 1.2.840.1  |     |      |
   | Image      |            | Explicit   | 0008.1.2.1 |     |      |
   | Storage    |            | VR Little  |            |     |      |
   |            |            | Endian     |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | Grayscale  | 1.2.840.   | Implicit   | 1.2.840    | SCU | None |
   | Softcopy   | 10008.5.1. | VR Little  | .10008.1.2 |     |      |
   | Pr         | 4.1.1.11.1 | Endian     |            |     |      |
   | esentation |            |            | 1.2.840.1  |     |      |
   | State      |            | Explicit   | 0008.1.2.1 |     |      |
   | Storage    |            | VR Little  |            |     |      |
   |            |            | Endian     |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | Storage    | 1.2.840.10 | Implicit   | 1.2.840    | SCU | None |
   | Commitment | 008.1.20.1 | VR Little  | .10008.1.2 |     |      |
   | Push Model |            | Endian     |            |     |      |
   |            |            |            | 1.2.840.1  |     |      |
   |            |            | Explicit   | 0008.1.2.1 |     |      |
   |            |            | VR Little  |            |     |      |
   |            |            | Endian     |            |     |      |
   +------------+------------+------------+------------+-----+------+

Presentation Contexts for X-Ray Radio Fluoroscopic Image Storage or
Grayscale Softcopy Presentation State Storage will only be proposed if
the Send Job contains instances for these SOP Classes.

A Presentation Context for the Storage Commitment Push Model will only
be proposed if the Remote AE is configured as an archive device.

.. _sect_B.4.2.1.3.1.3:

SOP Specific Conformance Image & Pres State Storage SOP Classes
                                                               

All Image & Presentation State Storage SOP Classes supported by the
Storage AE exhibit the same behavior, except where stated, and are
described together in this section.

If X-Ray Radio Fluoroscopic Image Storage SOP Instances are included in
the Send Job and a corresponding Presentation Context is not accepted
then the Association is aborted using AP-ABORT and the send job is
marked as failed. The job failure is logged and reported to the user via
the job control application.

If Grayscale Softcopy Presentation State Storage SOP Instances are
included in the Send Job and a corresponding Presentation Context cannot
be negotiated then Grayscale Softcopy Presentation State Storage SOP
Instances will not be sent and a warning is logged. Any remaining Image
Storage SOP Instances included in the Send Job will be transmitted.
Failure to negotiate a Presentation Context for Grayscale Softcopy
Presentation State Storage does not in itself cause the Send Job to be
marked as failed. The behavior of Storage AE when encountering status
codes in a C-STORE response is summarized in the Table below:

.. table:: Storage C-STORE Response Status Handling Behavior

   +----------------+----------------+----------------+----------------+
   | Service Status | Further        | Error Code     | Behavior       |
   |                | Meaning        |                |                |
   +================+================+================+================+
   | Success        | Success        | 0000           | The SCP has    |
   |                |                |                | successfully   |
   |                |                |                | stored the SOP |
   |                |                |                | Instance. If   |
   |                |                |                | all SOP        |
   |                |                |                | Instances in a |
   |                |                |                | send job have  |
   |                |                |                | status success |
   |                |                |                | then the job   |
   |                |                |                | is marked as   |
   |                |                |                | complete.      |
   +----------------+----------------+----------------+----------------+
   | Refused        | Out of         | A700-A7FF      | The            |
   |                | Resources      |                | Association is |
   |                |                |                | aborted using  |
   |                |                |                | A-ABORT and    |
   |                |                |                | the send job   |
   |                |                |                | is marked as   |
   |                |                |                | failed. The    |
   |                |                |                | status meaning |
   |                |                |                | is logged and  |
   |                |                |                | the job        |
   |                |                |                | failure is     |
   |                |                |                | reported to    |
   |                |                |                | the user via   |
   |                |                |                | the job        |
   |                |                |                | control        |
   |                |                |                | application.   |
   |                |                |                | This is a      |
   |                |                |                | transient      |
   |                |                |                | failure.       |
   +----------------+----------------+----------------+----------------+
   | Error          | Data Set does  | A900-A9FF      | The            |
   |                | not match SOP  |                | Association is |
   |                | Class          |                | aborted using  |
   |                |                |                | A-ABORT and    |
   |                |                |                | the send job   |
   |                |                |                | is marked as   |
   |                |                |                | failed. The    |
   |                |                |                | status meaning |
   |                |                |                | is logged and  |
   |                |                |                | the job        |
   |                |                |                | failure is     |
   |                |                |                | reported to    |
   |                |                |                | the user via   |
   |                |                |                | the job        |
   |                |                |                | control        |
   |                |                |                | application.   |
   +----------------+----------------+----------------+----------------+
   | Error          | Cannot         | C000-CFFF      | The            |
   |                | Understand     |                | Association is |
   |                |                |                | aborted using  |
   |                |                |                | A-ABORT and    |
   |                |                |                | the send job   |
   |                |                |                | is marked as   |
   |                |                |                | failed. The    |
   |                |                |                | status meaning |
   |                |                |                | is logged and  |
   |                |                |                | the job        |
   |                |                |                | failure is     |
   |                |                |                | reported to    |
   |                |                |                | the user via   |
   |                |                |                | the job        |
   |                |                |                | control        |
   |                |                |                | application.   |
   +----------------+----------------+----------------+----------------+
   | Warning        | Coercion of    | B000           | Image          |
   |                | Data Elements  |                | transmission   |
   |                |                |                | is considered  |
   |                |                |                | successful but |
   |                |                |                | the status     |
   |                |                |                | meaning is     |
   |                |                |                | logged.        |
   +----------------+----------------+----------------+----------------+
   | Warning        | Data Set does  | B007           | Image          |
   |                | not match SOP  |                | transmission   |
   |                | Class          |                | is considered  |
   |                |                |                | successful but |
   |                |                |                | the status     |
   |                |                |                | meaning is     |
   |                |                |                | logged.        |
   +----------------+----------------+----------------+----------------+
   | Warning        | Elements       | B006           | Image          |
   |                | Discarded      |                | transmission   |
   |                |                |                | is considered  |
   |                |                |                | successful but |
   |                |                |                | the status     |
   |                |                |                | meaning is     |
   |                |                |                | logged.        |
   +----------------+----------------+----------------+----------------+
   | \*             | \*             | Any other      | The            |
   |                |                | status code.   | Association is |
   |                |                |                | aborted using  |
   |                |                |                | A-ABORT and    |
   |                |                |                | the send job   |
   |                |                |                | is marked as   |
   |                |                |                | failed. The    |
   |                |                |                | status code is |
   |                |                |                | logged and the |
   |                |                |                | job failure is |
   |                |                |                | reported to    |
   |                |                |                | the user via   |
   |                |                |                | the job        |
   |                |                |                | control        |
   |                |                |                | application.   |
   +----------------+----------------+----------------+----------------+

The behavior of Storage AE during communication failure is summarized in
the Table below:

.. table:: Storage Communication Failure Behavior

   +----------------------------------+----------------------------------+
   | Exception                        | Behavior                         |
   +==================================+==================================+
   | Timeout                          | The Association is aborted using |
   |                                  | A-ABORT and the send job is      |
   |                                  | marked as failed. The reason is  |
   |                                  | logged and the job failure is    |
   |                                  | reported to the user via the job |
   |                                  | control application.             |
   +----------------------------------+----------------------------------+
   | Association aborted by the SCP   | The send job is marked as        |
   | or network layers                | failed. The reason is logged and |
   |                                  | the job failure is reported to   |
   |                                  | the user via the job control     |
   |                                  | application.                     |
   +----------------------------------+----------------------------------+

A failed send job can be restarted by user interaction. The system can
be configured to automatically resend failed jobs if a transient status
code is received. The delay between resending failed jobs and the number
of retries is also configurable.

The contents of X-Ray Radio Fluoroscopic Image Storage SOP Instances
created by EXAMPLE-INTEGRATED-MODALITY conform to the DICOM X-Ray Radio
Fluoroscopic Image IOD definition and are described in `IOD
Contents <#sect_B.8.1>`__.

The contents of Grayscale Softcopy Presentation State Storage SOP
Instances created by EXAMPLE-INTEGRATED-MODALITY conform to the DICOM
Grayscale Softcopy Presentation State IOD and are described in `IOD
Contents <#sect_B.8.1>`__.

Grayscale Softcopy Presentation State Storage SOP Instances are created
upon user request (e.g., explicitly via "Save" or implicitly via "Close
Patient") in order to save the most recent visual appearance of an image
(e.g., window center/width, shutters, graphic annotations). When saving
the visual appearance, a default Presentation Label will be supplied,
which the user can change. The user also has the possibility to enter a
detailed Presentation Description. If multiple images from the same
study are being displayed the request to save the visual appearance will
create one or more Presentation States referencing all displayed images.
If images from multiple studies are being displayed at least a separate
Presentation State will be created for each study.

When displaying an existing image the most recently saved Grayscale
Softcopy Presentation State containing references to the image will be
automatically applied. The user has the option to select other
Presentation States that also reference the image.

Grayscale Softcopy Presentation State Storage SOP Instances created by
EXAMPLE-INTEGRATED-MODALITY will only reference instances of X-Ray Radio
Fluoroscopic Image Storage SOP Instances.

Graphical annotations and shutters are only stored in Grayscale Softcopy
Presentation State objects. Remote AEs that do not support the Grayscale
Softcopy Presentation State Storage SOP Class will not have access to
graphical annotations or shutters created by
EXAMPLE-INTEGRATED-MODALITY.

.. _sect_B.4.2.1.3.1.4:

SOP Specific Conformance for Storage Commitment SOP Class
                                                         

.. _sect_B.4.2.1.3.1.4.1:

Storage Commitment Operations (N-ACTION)
                                        

The Storage AE will request storage commitment for instances of the
X-Ray Radio Fluoroscopic Image Storage SOP Class and Grayscale Softcopy
Presentation State Storage SOP Class if the Remote AE is configured as
an archive device and a presentation context for the Storage Commitment
Push Model has been accepted.

The Storage AE will consider Storage Commitment failed if no
N-EVENT-REPORT is received for a Transaction UID within a configurable
time period after receiving a successful N-ACTION response (duration of
applicability for a Transaction UID).

The Storage AE does not send the optional Storage Media File­Set ID &
UID Attributes or the Referenced Study Component Sequence Attribute in
the N-ACTION

The behavior of Storage AE when encountering status codes in a N-ACTION
response is summarized in the Table below:

.. table:: Storage Commitment N-ACTION Response Status Handling Behavior

   +----------------+----------------+----------------+----------------+
   | Service Status | Further        | Error Code     | Behavior       |
   |                | Meaning        |                |                |
   +================+================+================+================+
   | Success        | Success        | 0000           | The request    |
   |                |                |                | for storage    |
   |                |                |                | comment is     |
   |                |                |                | considered     |
   |                |                |                | successfully   |
   |                |                |                | sent. A timer  |
   |                |                |                | is started     |
   |                |                |                | that will      |
   |                |                |                | expire if no   |
   |                |                |                | N-EVENT-REPORT |
   |                |                |                | for the        |
   |                |                |                | Transaction    |
   |                |                |                | UID is         |
   |                |                |                | received       |
   |                |                |                | within a       |
   |                |                |                | configurable   |
   |                |                |                | timeout        |
   |                |                |                | period.        |
   +----------------+----------------+----------------+----------------+
   | \*             | \*             | Any other      | The            |
   |                |                | status code.   | Association is |
   |                |                |                | aborted using  |
   |                |                |                | A-ABORT and    |
   |                |                |                | the request    |
   |                |                |                | for storage    |
   |                |                |                | comment is     |
   |                |                |                | marked as      |
   |                |                |                | failed. The    |
   |                |                |                | status meaning |
   |                |                |                | is logged and  |
   |                |                |                | reported to    |
   |                |                |                | the user.      |
   +----------------+----------------+----------------+----------------+

The behavior of Storage AE during communication failure is summarized in
the Table below:

.. table:: Storage Commitment Communication Failure Behavior

   +----------------------------------+----------------------------------+
   | Exception                        | Behavior                         |
   +==================================+==================================+
   | Timeout                          | The Association is aborted using |
   |                                  | A-ABORT and the send job is      |
   |                                  | marked as failed. The reason is  |
   |                                  | logged and the job failure is    |
   |                                  | reported to the user via the job |
   |                                  | control application.             |
   +----------------------------------+----------------------------------+
   | Association aborted by the SCP   | The send job is marked as        |
   | or network layers                | failed. The reason is logged and |
   |                                  | the job failure is reported to   |
   |                                  | the user via the job control     |
   |                                  | application.                     |
   +----------------------------------+----------------------------------+

.. _sect_B.4.2.1.3.1.4.2:

Storage Commitment Notifications (N-EVENT-REPORT)
                                                 

The Storage AE is capable of receiving an N-EVENT-REPORT notification if
it has successfully negotiated a Presentation Context for the Storage
Commitment Push Model (i.e., only associations established with archive
devices).

Upon receipt of a N-EVENT-REPORT the timer associated with the
Transaction UID will be canceled.

The behavior of Storage AE when receiving Event Types within the
N-EVENT-REPORT is summarized in the Table below.

.. table:: Storage Commitment N-EVENT-REPORT Behavior

   +-------------------------+---------------+-------------------------+
   | Event Type Name         | Event Type ID | Behavior                |
   +=========================+===============+=========================+
   | Storage Commitment      | 1             | The Referenced SOP      |
   | Request Successful      |               | Instances under         |
   |                         |               | Referenced SOP Sequence |
   |                         |               | (0008,1199) are marked  |
   |                         |               | within the database as  |
   |                         |               | "Stored & Committed     |
   |                         |               | (SC) " to the value of  |
   |                         |               | Retrieve AE Title       |
   |                         |               | (0008,0054).            |
   |                         |               | Successfully committed  |
   |                         |               | SOP Instances are       |
   |                         |               | candidates for          |
   |                         |               | automatic deletion from |
   |                         |               | the local database if   |
   |                         |               | local resources become  |
   |                         |               | scarce. The conditions  |
   |                         |               | under which automatic   |
   |                         |               | deletion is initiated   |
   |                         |               | and the amount of space |
   |                         |               | freed are site          |
   |                         |               | configurable. SOP       |
   |                         |               | Instances will not be   |
   |                         |               | deleted if they are     |
   |                         |               | marked with a lock      |
   |                         |               | flag. The least         |
   |                         |               | recently accessed SOP   |
   |                         |               | Instances are deleted   |
   |                         |               | first.                  |
   +-------------------------+---------------+-------------------------+
   | Storage Commitment      | 2             | The Referenced SOP      |
   | Request Complete -      |               | Instances under         |
   | Failures Exist          |               | Referenced SOP Sequence |
   |                         |               | (0008,1199) are treated |
   |                         |               | in the same way as in   |
   |                         |               | the success case (Event |
   |                         |               | Type 1). The Referenced |
   |                         |               | SOP Instances under     |
   |                         |               | Failed SOP Sequence     |
   |                         |               | (0008,1198) are marked  |
   |                         |               | within the database as  |
   |                         |               | "Store & Commit Failed  |
   |                         |               | (Sf) ". The Failure     |
   |                         |               | Reasons are logged and  |
   |                         |               | the job failure is      |
   |                         |               | reported to the user    |
   |                         |               | via the job control     |
   |                         |               | application. A send job |
   |                         |               | that failed storage     |
   |                         |               | commitment will not be  |
   |                         |               | automatically restarted |
   |                         |               | but can be restarted by |
   |                         |               | user interaction.       |
   +-------------------------+---------------+-------------------------+

The reasons for returning specific status codes in a N-EVENT-REPORT
response are summarized in the Table below.

.. table:: Storage Commitment N-EVENT-REPORT Response Status Reasons

   +----------------+-----------------+------------+-----------------+
   | Service Status | Further Meaning | Error Code | Reasons         |
   +================+=================+============+=================+
   | Success        | Success         | 0000       | The storage     |
   |                |                 |            | commitment      |
   |                |                 |            | result has been |
   |                |                 |            | successfully    |
   |                |                 |            | received.       |
   +----------------+-----------------+------------+-----------------+
   | Failure        | Unrecognized    | 0211H      | The Transaction |
   |                | Operation       |            | UID in the      |
   |                |                 |            | N-EVENT-REPORT  |
   |                |                 |            | request is not  |
   |                |                 |            | recognized (was |
   |                |                 |            | never issued    |
   |                |                 |            | within an       |
   |                |                 |            | N-ACTION        |
   |                |                 |            | request).       |
   +----------------+-----------------+------------+-----------------+
   | Failure        | Resource        | 0213H      | The Transaction |
   |                | Limitation      |            | UID in the      |
   |                |                 |            | N-EVENT-REPORT  |
   |                |                 |            | request has     |
   |                |                 |            | expired (no     |
   |                |                 |            | N-EVENT-REPORT  |
   |                |                 |            | was received    |
   |                |                 |            | within a        |
   |                |                 |            | configurable    |
   |                |                 |            | time limit).    |
   +----------------+-----------------+------------+-----------------+
   | Failure        | No Such Event   | 0113H      | An invalid      |
   |                | Type            |            | Event Type ID   |
   |                |                 |            | was supplied in |
   |                |                 |            | the             |
   |                |                 |            | N-EVENT-REPORT  |
   |                |                 |            | request.        |
   +----------------+-----------------+------------+-----------------+
   | Failure        | Processing      | 0110H      | An internal     |
   |                | Failure         |            | error occurred  |
   |                |                 |            | during          |
   |                |                 |            | processing of   |
   |                |                 |            | the             |
   |                |                 |            | N-EVENT-REPORT. |
   |                |                 |            | A short         |
   |                |                 |            | description of  |
   |                |                 |            | the error will  |
   |                |                 |            | be returned in  |
   |                |                 |            | Error Comment   |
   |                |                 |            | (0000,0902).    |
   +----------------+-----------------+------------+-----------------+
   | Failure        | Invalid         | 0115H      | One or more SOP |
   |                | Argument Value  |            | Instance UIDs   |
   |                |                 |            | with the        |
   |                |                 |            | Referenced SOP  |
   |                |                 |            | Sequence        |
   |                |                 |            | (0008,1199) or  |
   |                |                 |            | Failed SOP      |
   |                |                 |            | Sequence        |
   |                |                 |            | (0008,1198) was |
   |                |                 |            | not included in |
   |                |                 |            | the Storage     |
   |                |                 |            | Commitment      |
   |                |                 |            | Request         |
   |                |                 |            | associated with |
   |                |                 |            | this            |
   |                |                 |            | Transaction     |
   |                |                 |            | UID. The        |
   |                |                 |            | unrecognized    |
   |                |                 |            | SOP Instance    |
   |                |                 |            | UIDs will be    |
   |                |                 |            | returned within |
   |                |                 |            | the Event       |
   |                |                 |            | Information of  |
   |                |                 |            | the             |
   |                |                 |            | N-EVENT-REPORT  |
   |                |                 |            | response.       |
   +----------------+-----------------+------------+-----------------+

.. _sect_B.4.2.1.4:

Association Acceptance Policy
'''''''''''''''''''''''''''''

.. _sect_B.4.2.1.4.1:

Activity - Receive Storage Commitment Response
                                              

.. _sect_B.4.2.1.4.1.1:

Description and Sequencing of Activities
                                        

The Storage AE will accept associations in order to receive responses to
a Storage Commitment Request.

A possible sequence of interactions between the Storage AE and an Image
Manager (e.g., a storage or archive device supporting Storage Commitment
SOP Classes as an SCP) is illustrated in the Figure above:

1. The Image Manager opens a new association with the Storage AE.

2. The Image Manager sends an N-EVENT-REPORT request notifying the
   Storage AE of the status of a previous Storage Commitment Request.
   The Storage AE replies with a N-EVENT-REPORT response confirming
   receipt.

3. The Image Manager closes the association with the Storage AE.

The Storage AE may reject association attempts as shown in the Table
below. The Result, Source and Reason/Diag columns represent the values
returned in the appropriate fields of an ASSOCIATE-RJ PDU (see ). The
contents of the Source column is abbreviated to save space and the
meaning of the abbreviations are:

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
   |                  |        |                  | associations has |
   |                  |        |                  | been reached. An |
   |                  |        |                  | association      |
   |                  |        |                  | request with the |
   |                  |        |                  | same parameters  |
   |                  |        |                  | may succeed at a |
   |                  |        |                  | later time.      |
   +------------------+--------+------------------+------------------+
   | 2 -              | c      | 1 -              | No associations  |
   | re               |        | temp             | can be accepted  |
   | jected-transient |        | orary-congestion | at this time due |
   |                  |        |                  | to the real-time |
   |                  |        |                  | requirements of  |
   |                  |        |                  | higher priority  |
   |                  |        |                  | activities       |
   |                  |        |                  | (e.g., during    |
   |                  |        |                  | image            |
   |                  |        |                  | acquisition no   |
   |                  |        |                  | associations     |
   |                  |        |                  | will be          |
   |                  |        |                  | accepted) or     |
   |                  |        |                  | because          |
   |                  |        |                  | insufficient     |
   |                  |        |                  | resources are    |
   |                  |        |                  | available (e.g., |
   |                  |        |                  | memory,          |
   |                  |        |                  | processes,       |
   |                  |        |                  | threads). An     |
   |                  |        |                  | association      |
   |                  |        |                  | request with the |
   |                  |        |                  | same parameters  |
   |                  |        |                  | may succeed at a |
   |                  |        |                  | later time.      |
   +------------------+--------+------------------+------------------+
   | 1 -              | a      | 2 -              | The association  |
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
   | 1 -              | a      | 7 -              | The association  |
   | re               |        | called-AE-titl   | request          |
   | jected-permanent |        | e-not-recognized | contained an     |
   |                  |        |                  | unrecognized     |
   |                  |        |                  | Called AE Title. |
   |                  |        |                  | An association   |
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
   |                  |        |                  | association      |
   |                  |        |                  | initiator is     |
   |                  |        |                  | incorrectly      |
   |                  |        |                  | configured and   |
   |                  |        |                  | attempts to      |
   |                  |        |                  | address the      |
   |                  |        |                  | association      |
   |                  |        |                  | acceptor using   |
   |                  |        |                  | the wrong AE     |
   |                  |        |                  | Title.           |
   +------------------+--------+------------------+------------------+
   | 1 -              | a      | 3 -              | The association  |
   | re               |        | calling-AE-titl  | request          |
   | jected-permanent |        | e-not-recognized | contained an     |
   |                  |        |                  | unrecognized     |
   |                  |        |                  | Calling AE       |
   |                  |        |                  | Title. An        |
   |                  |        |                  | association      |
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
   |                  |        |                  | association      |
   |                  |        |                  | acceptor has not |
   |                  |        |                  | been configured  |
   |                  |        |                  | to recognize the |
   |                  |        |                  | AE Title of the  |
   |                  |        |                  | association      |
   |                  |        |                  | initiator.       |
   +------------------+--------+------------------+------------------+
   | 1 -              | b      | 1 -              | The association  |
   | re               |        | no-reason-given  | request could    |
   | jected-permanent |        |                  | not be parsed.   |
   |                  |        |                  | An association   |
   |                  |        |                  | request with the |
   |                  |        |                  | same format will |
   |                  |        |                  | not succeed at a |
   |                  |        |                  | later time.      |
   +------------------+--------+------------------+------------------+

.. _sect_B.4.2.1.4.1.2:

Accepted Presentation Contexts
                              

The Storage AE will accept Presentation Contexts as shown in the Table
below.

.. table:: Acceptable Presentation Contexts for Activity Receive Storage
Commitment Response

   +------------+------------+------------+------------+-----+------+
   | Pr         |            |            |            |     |      |
   | esentation |            |            |            |     |      |
   | Context    |            |            |            |     |      |
   | Table      |            |            |            |     |      |
   +============+============+============+============+=====+======+
   | Storage    | 1.2.840.10 | Implicit   | 1.2.840    | SCU | None |
   | Commitment | 008.1.20.1 | VR Little  | .10008.1.2 |     |      |
   | Push Model |            | Endian     |            |     |      |
   |            |            |            | 1.2.840.1  |     |      |
   |            |            | Explicit   | 0008.1.2.1 |     |      |
   |            |            | VR Little  |            |     |      |
   |            |            | Endian     |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | Ve         | 1.2.840    | Implicit   | 1.2.840    | SCP | None |
   | rification | .10008.1.1 | VR Little  | .10008.1.2 |     |      |
   |            |            | Endian     |            |     |      |
   |            |            |            | 1.2.840.1  |     |      |
   |            |            | Explicit   | 0008.1.2.1 |     |      |
   |            |            | VR Little  |            |     |      |
   |            |            | Endian     |            |     |      |
   +------------+------------+------------+------------+-----+------+

The Storage AE will prefer to select the Explicit VR Little Endian
Transfer Syntax if multiple transfer syntaxes are offered. The Storage
AE will only accept the SCU role (which must be proposed via SCP/SCU
Role Selection Negotiation) within a Presentation Context for the
Storage Commitment Push Model SOP Class.

.. _sect_B.4.2.1.4.1.3:

SOP Specific Conformance for Storage Commitment SOP Class
                                                         

.. _sect_B.4.2.1.4.1.3.1:

Storage Commitment Notifications (N-EVENT-REPORT)
                                                 

Upon receipt of a N-EVENT-REPORT the timer associated with the
Transaction UID will be canceled.

The behavior of Storage AE when receiving Event Types within the
N-EVENT-REPORT is summarized in `table_title <#table_B.4.2-12>`__.

The reasons for returning specific status codes in a N-EVENT-REPORT
response are summarized in `table_title <#table_B.4.2-13>`__.

.. _sect_B.4.2.1.4.1.4:

SOP Specific Conformance for Verification SOP Class
                                                   

The Storage AE provides standard conformance to the Verification SOP
Class as an SCP. If the C-ECHO request was successfully received, a 0000
(Success) status code will be returned in the C-ECHO response.
Otherwise, a C000 (Error - Cannot Understand) status code will be
returned in the C-ECHO response.

.. _sect_B.4.2.2:

Workflow Application Entity Specification
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. _sect_B.4.2.2.1:

SOP Classes
'''''''''''

EXAMPLE-INTEGRATED-MODALITY provides Standard Conformance to the
following SOP Classes:

.. table:: SOP Classes for AE Workflow

   +--------------------------------------------+-------------------------+-----+-----+
   | SOP Class Name                             | SOP Class UID           | SCU | SCP |
   +============================================+=========================+=====+=====+
   | Modality Worklist Information Model - FIND | 1.2.840.10008.5.1.4.31  | Yes | No  |
   +--------------------------------------------+-------------------------+-----+-----+
   | Modality Performed Procedure Step          | 1.2.840.10008.3.1.2.3.3 | Yes | No  |
   +--------------------------------------------+-------------------------+-----+-----+

.. _sect_B.4.2.2.2:

Association Policies
''''''''''''''''''''

.. _sect_B.4.2.2.2.1:

General
       

The DICOM standard application context name for DICOM is always
proposed:

.. table:: DICOM Application Context for AE Workflow

   ======================== =====================
   Application Context Name 1.2.840.10008.3.1.1.1
   ======================== =====================

.. _sect_B.4.2.2.2.2:

Number of Associations
                      

EXAMPLE-INTEGRATED-MODALITY initiates one Association at a time for a
Worklist request.

.. table:: Number of Associations Initiated for AE Workflow

   =========================================== =
   Maximum number of simultaneous Associations 1
   =========================================== =

.. _sect_B.4.2.2.2.3:

Asynchronous Nature
                   

EXAMPLE-INTEGRATED-MODALITY does not support asynchronous communication
(multiple outstanding transactions over a single Association).

.. table:: Asynchronous Nature as a SCU for AE Workflow

   ======================================================= =
   Maximum number of outstanding asynchronous transactions 1
   ======================================================= =

.. _sect_B.4.2.2.2.4:

Implementation Identifying Information
                                      

The implementation information for this Application Entity is:

.. table:: DICOM Implementation Class and Version for AE Workflow

   =========================== ============================
   Implementation Class UID    1.xxxxxxx.yyy.etc.ad.inf.usw
   Implementation Version Name EXINTMOD_01
   =========================== ============================

.. _sect_B.4.2.2.3:

Association Initiation Policy
'''''''''''''''''''''''''''''

.. _sect_B.4.2.2.3.1:

Activity - Worklist Update
                          

.. _sect_B.4.2.2.3.1.1:

Description and Sequencing of Activities
                                        

The request for a Worklist Update is initiated by user interaction,
i.e., pressing the buttons "Worklist Update"/"Patient Worklist Query" or
automatically at specific time intervals, configurable by the user. With
"Worklist Update" the automated query mechanism is performed immediately
on request, while with "Patient Worklist Query" a dialog to enter search
criteria is opened and an interactive query can be performed.

The interactive Patient Worklist Query will display a dialog for
entering data as search criteria. When the Query is started on user
request, only the data from the dialog will be inserted as matching keys
into the query.

With automated worklist queries (including "Worklist Update") the
EXAMPLE-INTEGRATED-MODALITY always requests all items for a Scheduled
Procedure Step Start Date (actual date), Modality (RF) and Scheduled
Station AE Title. Query for the Scheduled Station AE Title is
configurable by a Service Engineer.

Upon initiation of the request, the EXAMPLE-INTEGRATED-MODALITY will
build an Identifier for the C-FIND request, will initiate an Association
to send the request and will wait for Worklist responses. After
retrieval of all responses, EXAMPLE-INTEGRATED-MODALITY will access the
local database to add or update patient demographic data. To protect the
system from overflow, the EXAMPLE-INTEGRATED-MODALITY will limit the
number of processed worklist responses to a configurable maximum. During
receiving the worklist response items are counted and the query
processing is canceled by issuing a C-FIND-CANCEL if the configurable
limit of items is reached. The results will be displayed in a separate
list, which will be cleared with the next worklist update.

EXAMPLE-INTEGRATED-MODALITY will initiate an Association in order to
issue a C-FIND request according to the Modality Worklist Information
Model.

A possible sequence of interactions between the Workflow AE and a
Departmental Scheduler (e.g., a device such as a RIS or HIS that
supports the Modality Worklist SOP Class as an SCP) is illustrated in
the Figure above:

1. The Worklist AE opens an association with the Departmental Scheduler

2. The Worklist AE sends a C-FIND request to the Departmental Scheduler
   containing the Worklist Query attributes.

3. The Departmental Scheduler returns a C-FIND response containing the
   requested attributes of the first matching Worklist Item.

4. The Departmental Scheduler returns another C-FIND response containing
   the requested attributes of the second matching Worklist Item.

5. The Departmental Scheduler returns another C-FIND response with
   status Success indicating that no further matching Worklist Items
   exist. This example assumes that only 2 Worklist items match the
   Worklist Query.

6. The Worklist AE closes the association with the Departmental
   Scheduler.

7. The user selects a Worklist Item from the Worklist and prepares to
   acquire new images.

.. _sect_B.4.2.2.3.1.2:

Proposed Presentation Contexts
                              

EXAMPLE-INTEGRATED-MODALITY will propose Presentation Contexts as shown
in the following table:

.. table:: Proposed Presentation Contexts for Activity Worklist Update

   +------------+------------+------------+------------+-----+------+
   | Pr         |            |            |            |     |      |
   | esentation |            |            |            |     |      |
   | Context    |            |            |            |     |      |
   | Table      |            |            |            |     |      |
   +============+============+============+============+=====+======+
   | Modality   | 1.         | Implicit   | 1.2.840    | SCU | None |
   | Worklist   | 2.840.1000 | VR Little  | .10008.1.2 |     |      |
   | I          | 8.5.1.4.31 | Endian     |            |     |      |
   | nformation |            |            |            |     |      |
   | Model -    |            |            |            |     |      |
   | FIND       |            |            |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | Explicit   | 1.2.840.1  |            |            |     |      |
   | VR Little  | 0008.1.2.1 |            |            |     |      |
   | Endian     |            |            |            |     |      |
   +------------+------------+------------+------------+-----+------+

.. _sect_B.4.2.2.3.1.3:

SOP Specific Conformance for Modality Worklist
                                              

The behavior of EXAMPLE-INTEGRATED-MODALITY when encountering status
codes in a Modality Worklist C-FIND response is summarized in the Table
below. If any other SCP response status than "Success" or "Pending" is
received by EXAMPLE­INTEGRATED-MODALITY, a message "query failed" will
appear on the user interface.

.. table:: Modality Worklist C-FIND Response Status Handling Behavior

   +----------------+----------------+----------------+----------------+
   | Service Status | Further        | Error Code     | Behavior       |
   |                | Meaning        |                |                |
   +================+================+================+================+
   | Success        | Matching is    | 0000           | The SCP has    |
   |                | complete       |                | completed the  |
   |                |                |                | matches.       |
   |                |                |                | Worklist items |
   |                |                |                | are available  |
   |                |                |                | for display or |
   |                |                |                | further        |
   |                |                |                | processing.    |
   +----------------+----------------+----------------+----------------+
   | Refused        | Out of         | A700           | The            |
   |                | Resources      |                | Association is |
   |                |                |                | aborted using  |
   |                |                |                | A-ABORT and    |
   |                |                |                | the worklist   |
   |                |                |                | query is       |
   |                |                |                | marked as      |
   |                |                |                | failed. The    |
   |                |                |                | status meaning |
   |                |                |                | is logged and  |
   |                |                |                | reported to    |
   |                |                |                | the user if an |
   |                |                |                | interactive    |
   |                |                |                | query. Any     |
   |                |                |                | additional     |
   |                |                |                | error          |
   |                |                |                | information in |
   |                |                |                | the Response   |
   |                |                |                | will be        |
   |                |                |                | logged.        |
   +----------------+----------------+----------------+----------------+
   | Failed         | Identifier     | A900           | The            |
   |                | does not match |                | Association is |
   |                | SOP Class      |                | aborted using  |
   |                |                |                | A-ABORT and    |
   |                |                |                | the worklist   |
   |                |                |                | query is       |
   |                |                |                | marked as      |
   |                |                |                | failed. The    |
   |                |                |                | status meaning |
   |                |                |                | is logged and  |
   |                |                |                | reported to    |
   |                |                |                | the user if an |
   |                |                |                | interactive    |
   |                |                |                | query. Any     |
   |                |                |                | additional     |
   |                |                |                | error          |
   |                |                |                | information in |
   |                |                |                | the Response   |
   |                |                |                | will be        |
   |                |                |                | logged.        |
   +----------------+----------------+----------------+----------------+
   | Failed         | Unable to      | C000 - CFFF    | The            |
   |                | Process        |                | Association is |
   |                |                |                | aborted using  |
   |                |                |                | A-ABORT and    |
   |                |                |                | the worklist   |
   |                |                |                | query is       |
   |                |                |                | marked as      |
   |                |                |                | failed. The    |
   |                |                |                | status meaning |
   |                |                |                | is logged and  |
   |                |                |                | reported to    |
   |                |                |                | the user if an |
   |                |                |                | interactive    |
   |                |                |                | query. Any     |
   |                |                |                | additional     |
   |                |                |                | error          |
   |                |                |                | information in |
   |                |                |                | the Response   |
   |                |                |                | will be        |
   |                |                |                | logged.        |
   +----------------+----------------+----------------+----------------+
   | Cancel         | Matching       | FE00           | If the query   |
   |                | terminated due |                | was canceled   |
   |                | to Cancel      |                | due to too may |
   |                | request        |                | worklist items |
   |                |                |                | then the SCP   |
   |                |                |                | has completed  |
   |                |                |                | the matches.   |
   |                |                |                | Worklist items |
   |                |                |                | are available  |
   |                |                |                | for display or |
   |                |                |                | further        |
   |                |                |                | processing.    |
   |                |                |                | Otherwise, the |
   |                |                |                | Association is |
   |                |                |                | aborted using  |
   |                |                |                | A-ABORT and    |
   |                |                |                | the worklist   |
   |                |                |                | query is       |
   |                |                |                | marked as      |
   |                |                |                | failed. The    |
   |                |                |                | status meaning |
   |                |                |                | is logged and  |
   |                |                |                | reported to    |
   |                |                |                | the user if an |
   |                |                |                | interactive    |
   |                |                |                | query.         |
   +----------------+----------------+----------------+----------------+
   | Pending        | Matches are    | FF00           | The worklist   |
   |                | continuing     |                | item contained |
   |                |                |                | in the         |
   |                |                |                | Identifier is  |
   |                |                |                | collected for  |
   |                |                |                | later display  |
   |                |                |                | or further     |
   |                |                |                | processing.    |
   +----------------+----------------+----------------+----------------+
   | Pending        | Matches are    | FF01           | The worklist   |
   |                | continuing -   |                | item contained |
   |                | Warning that   |                | in the         |
   |                | one or more    |                | Identifier is  |
   |                | Optional Keys  |                | collected for  |
   |                | were not       |                | later display  |
   |                | supported      |                | or further     |
   |                |                |                | processing.    |
   |                |                |                | The status     |
   |                |                |                | meaning is     |
   |                |                |                | logged only    |
   |                |                |                | once for each  |
   |                |                |                | C-FIND         |
   |                |                |                | operation.     |
   +----------------+----------------+----------------+----------------+
   | \*             | \*             | Any other      | The            |
   |                |                | status code.   | Association is |
   |                |                |                | aborted using  |
   |                |                |                | A-ABORT and    |
   |                |                |                | the worklist   |
   |                |                |                | is marked as   |
   |                |                |                | failed. The    |
   |                |                |                | status meaning |
   |                |                |                | is logged and  |
   |                |                |                | reported to    |
   |                |                |                | the user if an |
   |                |                |                | interactive    |
   |                |                |                | query. Any     |
   |                |                |                | additional     |
   |                |                |                | error          |
   |                |                |                | information in |
   |                |                |                | the Response   |
   |                |                |                | will be        |
   |                |                |                | logged.        |
   +----------------+----------------+----------------+----------------+

The behavior of EXAMPLE-INTEGRATED-MODALITY during communication failure
is summarized in the Table below.

.. table:: Modality Worklist Communication Failure Behavior

   +----------------------------------+----------------------------------+
   | Exception                        | Behavior                         |
   +==================================+==================================+
   | Timeout                          | The Association is aborted using |
   |                                  | A-ABORT and the worklist query   |
   |                                  | marked as failed. The reason is  |
   |                                  | logged and reported to the user  |
   |                                  | if an interactive query.         |
   +----------------------------------+----------------------------------+
   | Association aborted by the SCP   | The worklist query is marked as  |
   | or network layers                | failed. The reason is logged and |
   |                                  | reported to the user if an       |
   |                                  | interactive query.               |
   +----------------------------------+----------------------------------+

Acquired images will always use the Study Instance UID specified for the
Scheduled Procedure Step (if available). If an acquisition is
unscheduled, a Study Instance UID will be generated locally.

The Table below provides a description of the
EXAMPLE­INTEGRATED-MODALITY Worklist Request Identifier and specifies
the attributes that are copied into the images. Unexpected attributes
returned in a C-FIND response are ignored.

Requested return attributes not supported by the SCP are set to have no
value. Non-matching responses returned by the SCP due to unsupported
optional matching keys are ignored. No attempt is made it filter out
possible duplicate entries.

.. table:: Worklist Request Identifier

   +-----------------+-------------+----+-----+---+---+---+---+
   | Module Name     |             |    |     |   |   |   |   |
   +=================+=============+====+=====+===+===+===+===+
   | **Scheduled     |             |    |     |   |   |   |   |
   | Procedure       |             |    |     |   |   |   |   |
   | Step**          |             |    |     |   |   |   |   |
   +-----------------+-------------+----+-----+---+---+---+---+
   | Scheduled       | (0040,0100) | SQ |     |   |   |   |   |
   | Procedure Step  |             |    |     |   |   |   |   |
   | Sequence        |             |    |     |   |   |   |   |
   +-----------------+-------------+----+-----+---+---+---+---+
   | >Scheduled      | (0040,0001) | AE | (S) |   |   | x |   |
   | Station AE      |             |    |     |   |   |   |   |
   | Title           |             |    |     |   |   |   |   |
   +-----------------+-------------+----+-----+---+---+---+---+
   | >Scheduled      | (0040,0002) | DA | S   |   |   | x |   |
   | Procedure Step  |             |    |     |   |   |   |   |
   | Start Date      |             |    |     |   |   |   |   |
   +-----------------+-------------+----+-----+---+---+---+---+
   | >Scheduled      | (0040,0003) | TM |     | x |   | x |   |
   | Procedure Step  |             |    |     |   |   |   |   |
   | Start Time      |             |    |     |   |   |   |   |
   +-----------------+-------------+----+-----+---+---+---+---+
   | >Modality       | (0008,0060) | CS | S   | x |   |   |   |
   +-----------------+-------------+----+-----+---+---+---+---+
   | >Scheduled      | (0040,0006) | PN |     | x | x | x | x |
   | Performing      |             |    |     |   |   |   |   |
   | Physician's     |             |    |     |   |   |   |   |
   | Name            |             |    |     |   |   |   |   |
   +-----------------+-------------+----+-----+---+---+---+---+
   | >Scheduled      | (0040,0007) | LO |     | x |   | x | x |
   | Procedure Step  |             |    |     |   |   |   |   |
   | Description     |             |    |     |   |   |   |   |
   +-----------------+-------------+----+-----+---+---+---+---+
   | >Scheduled      | (0040,0010) | SH |     | x |   |   |   |
   | Station Name    |             |    |     |   |   |   |   |
   +-----------------+-------------+----+-----+---+---+---+---+
   | >Scheduled      | (0040,0011) | SH |     | x |   |   |   |
   | Procedure Step  |             |    |     |   |   |   |   |
   | Location        |             |    |     |   |   |   |   |
   +-----------------+-------------+----+-----+---+---+---+---+
   | >Scheduled      | (0040,0008) | SQ |     | x |   |   | x |
   | Protocol Code   |             |    |     |   |   |   |   |
   | Sequence        |             |    |     |   |   |   |   |
   +-----------------+-------------+----+-----+---+---+---+---+
   | >Pre-Medication | (0040,0012) | LO |     | x |   | x |   |
   +-----------------+-------------+----+-----+---+---+---+---+
   | >Scheduled      | (0040,0009) | SH |     | x |   | x | x |
   | Procedure Step  |             |    |     |   |   |   |   |
   | ID              |             |    |     |   |   |   |   |
   +-----------------+-------------+----+-----+---+---+---+---+
   | >Requested      | (0032,1070) | LO |     | x |   | x |   |
   | Contrast Agent  |             |    |     |   |   |   |   |
   +-----------------+-------------+----+-----+---+---+---+---+
   | **Requested     |             |    |     |   |   |   |   |
   | Procedure**     |             |    |     |   |   |   |   |
   +-----------------+-------------+----+-----+---+---+---+---+
   | Requested       | (0040,1001) | SH |     | x | x | x | x |
   | Procedure ID    |             |    |     |   |   |   |   |
   +-----------------+-------------+----+-----+---+---+---+---+
   | Requested       | (0032,1060) | LO |     | x |   | x | x |
   | Procedure       |             |    |     |   |   |   |   |
   | Description     |             |    |     |   |   |   |   |
   +-----------------+-------------+----+-----+---+---+---+---+
   | Study Instance  | (0020,000D) | UI |     | x |   |   | x |
   | UID             |             |    |     |   |   |   |   |
   +-----------------+-------------+----+-----+---+---+---+---+
   | Requested       | (0040,1003) | SH |     | x |   |   |   |
   | Procedure       |             |    |     |   |   |   |   |
   | Priority        |             |    |     |   |   |   |   |
   +-----------------+-------------+----+-----+---+---+---+---+
   | Patient         | (0040,1004) | LO |     | x |   |   |   |
   | Transport       |             |    |     |   |   |   |   |
   | Arrangements    |             |    |     |   |   |   |   |
   +-----------------+-------------+----+-----+---+---+---+---+
   | Referenced      | (0008,1110) | SQ |     | x |   |   | x |
   | Study Sequence  |             |    |     |   |   |   |   |
   +-----------------+-------------+----+-----+---+---+---+---+
   | Requested       | (0032,1064) | SQ |     | x |   |   | x |
   | Procedure Code  |             |    |     |   |   |   |   |
   | Sequence        |             |    |     |   |   |   |   |
   +-----------------+-------------+----+-----+---+---+---+---+
   | **Imaging       |             |    |     |   |   |   |   |
   | Service         |             |    |     |   |   |   |   |
   | Request**       |             |    |     |   |   |   |   |
   +-----------------+-------------+----+-----+---+---+---+---+
   | Accession       | (0008,0050) | SH |     | x | x | x | x |
   | Number          |             |    |     |   |   |   |   |
   +-----------------+-------------+----+-----+---+---+---+---+
   | Requesting      | (0032,1032) | PN |     | x |   | x | x |
   | Physician       |             |    |     |   |   |   |   |
   +-----------------+-------------+----+-----+---+---+---+---+
   | Referring       | (0008,0090) | PN |     | x | x | x | x |
   | Physician's     |             |    |     |   |   |   |   |
   | Name            |             |    |     |   |   |   |   |
   +-----------------+-------------+----+-----+---+---+---+---+
   | **Visit         |             |    |     |   |   |   |   |
   | I               |             |    |     |   |   |   |   |
   | dentification** |             |    |     |   |   |   |   |
   +-----------------+-------------+----+-----+---+---+---+---+
   | Admission ID    | (0038,0010) | LO |     | x |   |   |   |
   +-----------------+-------------+----+-----+---+---+---+---+
   | **Visit         |             |    |     |   |   |   |   |
   | Status**        |             |    |     |   |   |   |   |
   +-----------------+-------------+----+-----+---+---+---+---+
   | Current Patient | (0038,0300) | LO |     | x | x |   |   |
   | Location        |             |    |     |   |   |   |   |
   +-----------------+-------------+----+-----+---+---+---+---+
   | **Visit         |             |    |     |   |   |   |   |
   | Admission**     |             |    |     |   |   |   |   |
   +-----------------+-------------+----+-----+---+---+---+---+
   | Admitting       | (0008,1080) | LO |     | x |   | x |   |
   | Diagnosis       |             |    |     |   |   |   |   |
   | Description     |             |    |     |   |   |   |   |
   +-----------------+-------------+----+-----+---+---+---+---+
   | **Patient       |             |    |     |   |   |   |   |
   | I               |             |    |     |   |   |   |   |
   | dentification** |             |    |     |   |   |   |   |
   +-----------------+-------------+----+-----+---+---+---+---+
   | Patient's Name  | (0010,0010) | PN |     | x | x | x | x |
   +-----------------+-------------+----+-----+---+---+---+---+
   | Patient ID      | (0010,0020) | LO |     | x | x | x | x |
   +-----------------+-------------+----+-----+---+---+---+---+
   | **Patient       |             |    |     |   |   |   |   |
   | Demographic**   |             |    |     |   |   |   |   |
   +-----------------+-------------+----+-----+---+---+---+---+
   | Patient's Birth | (0010,0030) | DA |     | x | x | x | x |
   | Date            |             |    |     |   |   |   |   |
   +-----------------+-------------+----+-----+---+---+---+---+
   | Patient's Sex   | (0010,0040) | CS |     | x | x | x | x |
   +-----------------+-------------+----+-----+---+---+---+---+
   | Patient's       | (0010,1030) | DS |     | x |   | x | x |
   | Weight          |             |    |     |   |   |   |   |
   +-----------------+-------------+----+-----+---+---+---+---+
   | Confidentiality | (0040,3001) | LO |     | x |   | x |   |
   | Constraint on   |             |    |     |   |   |   |   |
   | Patient Data    |             |    |     |   |   |   |   |
   | Description     |             |    |     |   |   |   |   |
   +-----------------+-------------+----+-----+---+---+---+---+
   | **Patient       |             |    |     |   |   |   |   |
   | Medical**       |             |    |     |   |   |   |   |
   +-----------------+-------------+----+-----+---+---+---+---+
   | Patient State   | (0038,0500) | LO |     | x |   | x |   |
   +-----------------+-------------+----+-----+---+---+---+---+
   | Pregnancy       | (0010,21C0) | US |     | x |   | x |   |
   | Status          |             |    |     |   |   |   |   |
   +-----------------+-------------+----+-----+---+---+---+---+
   | Medical Alerts  | (0010,2000) | LO |     | x |   | x |   |
   +-----------------+-------------+----+-----+---+---+---+---+
   | Allergies       | (0010,2110) | LO |     | x |   | x |   |
   +-----------------+-------------+----+-----+---+---+---+---+
   | Special Needs   | (0038,0050) | LO |     | x |   | x |   |
   +-----------------+-------------+----+-----+---+---+---+---+

.. note::

   If an extended character set is used in the Request Identifier,
   Specific Character Set (0008,0005) will be included in the Identifier
   with the value "ISO_IR 100" or "ISO_IR 144" (see `Support of
   Character Sets <#sect_B.6>`__). Otherwise, Specific Character Set
   (0008,0005) will not be sent

The above tables should be read as follows:

Module Name
   The name of the associated module for supported worklist attributes.

Attribute Name
   Attributes supported to build an EXAMPLE­INTEGRATED-MODALITY Worklist
   Request Identifier.

Tag
   DICOM tag for this attribute.

VR
   DICOM VR for this attribute.

M
   Matching keys for (automatic) Worklist Update. A "S" will indicate
   that EXAMPLE-INTEGRATED-MODALITY will supply an attribute value for
   Single Value Matching, a "R" will indicate Range Matching and a "*"
   will denote wild card matching. It can be configured if "Scheduled
   Station AE Title" is additionally supplied "(S) " and if Modality is
   set to RF or SC.

R
   Return keys. An "x" will indicate that EXAMPLE-INTEGRATED-MODALITY
   will supply this attribute as Return Key with zero length for
   Universal Matching. The EXAMPLE-INTEGRATED-MODALITY will support
   retired date format (yyyy.mm.dd) for "Patient's Birth Date" and
   "Scheduled Procedure Step Start Date" in the response identifiers.
   For "Scheduled Procedure Step Start Time" also retired time format as
   well as unspecified time components are supported.

Q
   Interactive Query Key. An "x" " will indicate that
   EXAMPLE-INTEGRATED-MODALITY will supply this attribute as matching
   key, if entered in the Query Patient Worklist dialog. For example,
   the Patient Name can be entered thereby restricting Worklist
   responses to Procedure Steps scheduled for the patient.

D
   Displayed keys. An "x" indicates that this worklist attribute is
   displayed to the user during a patient registration dialog. For
   example, Patient Name will be displayed when registering the patient
   prior to an examination.

IOD
   An "x" indicates that this Worklist attribute is included into all
   Object Instances created during performance of the related Procedure
   Step.

The default Query Configuration is set to "Modality" (RF) and "Date"
(date of today). Optionally, additional matching for the own AET is
configurable.

.. _sect_B.4.2.2.3.2:

Activity - Acquire Images
                         

.. _sect_B.4.2.2.3.2.1:

Description and Sequencing of Activities
                                        

After Patient registration, the EXAMPLE-INTEGRATED-MODALITY is awaiting
the 1st application of X-Ray Dose to the patient. The trigger to create
a MPPS SOP Instance is derived from this event. An Association to the
configured MPPS SCP system is established immediately and the related
MPPS SOP Instance will be created.

A manual update can be performed with the MPPS user interface where is
it possible to set the final state of the MPPS to "COMPLETED" or
"DISCONTINUED". In the "Discontinued" case the user can also select the
discontinuation reason from a list corresponding to . A MPPS Instance
that has been sent with a state of "COMPLETED" or "DISCONTINUED" can no
longer be updated.

The EXAMPLE-INTEGRATED-MODALITY will support creation of "unscheduled
cases" by allowing MPPS Instances to be communicated for locally
registered Patients.

The EXAMPLE-INTEGRATED-MODALITY only supports a 0-to-1 relationship
between Scheduled and Performed Procedure Steps.

EXAMPLE-INTEGRATED-MODALITY will initiate an Association to issue an:

-  N-CREATE request according to the CREATE Modality Performed Procedure
   Step SOP Instance operation or a

-  N-SET request to update the contents and state of the MPPS according
   to the SET Modality Performed Procedure Step Information operation.

A possible sequence of interactions between the Workflow AE and a
Departmental Scheduler (e.g., a device such as a RIS or HIS that
supports the MPPS SOP Class as an SCP) is illustrated in
`figure_title <#figure_B.4.2-4>`__:

1. The Worklist AE opens an association with the Departmental Scheduler

2. The Worklist AE sends an N-CREATE request to the Departmental
   Scheduler to create an MPPS instance with status of "IN PROGRESS" and
   create all necessary attributes. The Departmental Scheduler
   acknowledges the MPPS creation with an N-CREATE response (status
   success).

3. The Worklist AE closes the association with the Departmental
   Scheduler.

4. All images are acquired and stored in the local database.

5. The Worklist AE opens an association with the Departmental Scheduler.

6. The Worklist AE sends an N-SET request to the Departmental Scheduler
   to update the MPPS instance with status of "COMPLETED" and set all
   necessary attributes. The Departmental Scheduler acknowledges the
   MPPS update with an N-SET response (status success).

7. The Worklist AE closes the association with the Departmental
   Scheduler.

.. _sect_B.4.2.2.3.2.2:

Proposed Presentation Contexts
                              

EXAMPLE-INTEGRATED-MODALITY will propose Presentation Contexts as shown
in the following table:

.. table:: Proposed Presentation Contexts for Real-World Activity
Acquire Images

   +------------+------------+------------+------------+-----+------+
   | Pr         |            |            |            |     |      |
   | esentation |            |            |            |     |      |
   | Context    |            |            |            |     |      |
   | Table      |            |            |            |     |      |
   +============+============+============+============+=====+======+
   | Modality   | 1.2        | Implicit   | 1.2.840    | SCU | None |
   | Performed  | .840.10008 | VR Little  | .10008.1.2 |     |      |
   | Procedure  | .3.1.2.3.3 | Endian     |            |     |      |
   | Step       |            |            |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | Explicit   | 1.2.840.1  |            |            |     |      |
   | VR Little  | 0008.1.2.1 |            |            |     |      |
   | Endian     |            |            |            |     |      |
   +------------+------------+------------+------------+-----+------+

.. _sect_B.4.2.2.3.2.3:

SOP Specific Conformance for MPPS
                                 

The behavior of EXAMPLE-INTEGRATED-MODALITY when encountering status
codes in an MPPS N-CREATE or N-SET response is summarized in
`table_title <#table_B.4.2-26>`__. If any other SCP response status than
"Success" or "Warning" is received by EXAMPLE­INTEGRATED-MODALITY, a
message "MPPS update failed" will appear on the user interface.

.. table:: MPPS N-CREATE / N-SET Response Status Handling Behavior

   +----------------+----------------+----------------+----------------+
   | Service Status | Further        | Error Code     | Behavior       |
   |                | Meaning        |                |                |
   +================+================+================+================+
   | Success        | Success        | 0000           | The SCP has    |
   |                |                |                | completed the  |
   |                |                |                | operation      |
   |                |                |                | successfully.  |
   +----------------+----------------+----------------+----------------+
   | Failure        | Processing     | 0110           | The            |
   |                | Failure -      |                | Association is |
   |                | Performed      |                | aborted using  |
   |                | Procedure Step |                | A-ABORT and    |
   |                | Object may no  |                | the MPPS is    |
   |                | longer be      |                | marked as      |
   |                | updated        |                | failed. The    |
   |                |                |                | status meaning |
   |                |                |                | is logged and  |
   |                |                |                | reported to    |
   |                |                |                | the user.      |
   |                |                |                | Additional     |
   |                |                |                | information in |
   |                |                |                | the Response   |
   |                |                |                | will be logged |
   |                |                |                | (i.e., Error   |
   |                |                |                | Comment and    |
   |                |                |                | Error ID).     |
   +----------------+----------------+----------------+----------------+
   | Warning        | Attribute      | 0116H          | The MPPS       |
   |                | Value Out of   |                | operation is   |
   |                | Range          |                | considered     |
   |                |                |                | successful but |
   |                |                |                | the status     |
   |                |                |                | meaning is     |
   |                |                |                | logged.        |
   |                |                |                | Additional     |
   |                |                |                | information in |
   |                |                |                | the Response   |
   |                |                |                | identifying    |
   |                |                |                | the attributes |
   |                |                |                | out of range   |
   |                |                |                | will be logged |
   |                |                |                | (i.e.,         |
   |                |                |                | Elements in    |
   |                |                |                | the            |
   |                |                |                | Modification   |
   |                |                |                | List/Attribute |
   |                |                |                | List)          |
   +----------------+----------------+----------------+----------------+
   | \*             | \*             | Any other      | The            |
   |                |                | status code.   | Association is |
   |                |                |                | aborted using  |
   |                |                |                | A-ABORT and    |
   |                |                |                | the MPPS is    |
   |                |                |                | marked as      |
   |                |                |                | failed. The    |
   |                |                |                | status meaning |
   |                |                |                | is logged and  |
   |                |                |                | reported to    |
   |                |                |                | the user.      |
   +----------------+----------------+----------------+----------------+

The behavior of EXAMPLE-INTEGRATED-MODALITY during communication failure
is summarized in the Table below:

.. table:: MPPS Communication Failure Behavior

   +----------------------------------+----------------------------------+
   | Exception                        | Behavior                         |
   +==================================+==================================+
   | Timeout                          | The Association is aborted using |
   |                                  | A-ABORT and MPPS marked as       |
   |                                  | failed. The reason is logged and |
   |                                  | reported to the user.            |
   +----------------------------------+----------------------------------+
   | Association aborted by the SCP   | The MPPS is marked as failed.    |
   | or network layers                | The reason is logged and         |
   |                                  | reported to the user.            |
   +----------------------------------+----------------------------------+

`table_title <#table_B.4.2-28>`__ provides a description of the MPPS
N-CREATE and N-SET request identifiers sent by
EXAMPLE-INTEGRATED-MODALITY. Empty cells in the N-CREATE and N-SET
columns indicate that the attribute is not sent. An "x" indicates that
an appropriate value will be sent. A "Zero length" attribute will be
sent with zero length.

.. table:: MPPS N-CREATE / N-SET Request Identifier

   +---------------+-------------+----+---------------+---------------+
   | Attribute     | Tag         | VR | N-CREATE      | N-SET         |
   | Name          |             |    |               |               |
   +===============+=============+====+===============+===============+
   | Specific      | (0008,0005) | CS | "ISO_IR 100"  |               |
   | Character Set |             |    | or "ISO_IR    |               |
   |               |             |    | 144"          |               |
   +---------------+-------------+----+---------------+---------------+
   | Modality      | (0008,0060) | CS | RF            |               |
   +---------------+-------------+----+---------------+---------------+
   | Referenced    | (0008,1120) | SQ | Zero length   |               |
   | Patient       |             |    |               |               |
   | Sequence      |             |    |               |               |
   +---------------+-------------+----+---------------+---------------+
   | Patient's     | (0010,0010) | PN | From Modality |               |
   | Name          |             |    | Worklist or   |               |
   |               |             |    | user input    |               |
   |               |             |    | (all 5        |               |
   |               |             |    | components).  |               |
   |               |             |    | The user can  |               |
   |               |             |    | modify values |               |
   |               |             |    | provided via  |               |
   |               |             |    | Modality      |               |
   |               |             |    | Worklist.     |               |
   +---------------+-------------+----+---------------+---------------+
   | Patient ID    | (0010,0020) | LO | From Modality |               |
   |               |             |    | Worklist or   |               |
   |               |             |    | user input.   |               |
   |               |             |    | The user can  |               |
   |               |             |    | modify values |               |
   |               |             |    | provided via  |               |
   |               |             |    | Modality      |               |
   |               |             |    | Worklist.     |               |
   +---------------+-------------+----+---------------+---------------+
   | Patient's     | (0010,0030) | DA | From Modality |               |
   | Birth Date    |             |    | Worklist or   |               |
   |               |             |    | user input.   |               |
   |               |             |    | The user can  |               |
   |               |             |    | modify values |               |
   |               |             |    | provided via  |               |
   |               |             |    | Modality      |               |
   |               |             |    | Worklist.     |               |
   +---------------+-------------+----+---------------+---------------+
   | Patient's Sex | (0010,0040) | CS | From Modality |               |
   |               |             |    | Worklist or   |               |
   |               |             |    | user input.   |               |
   |               |             |    | The user can  |               |
   |               |             |    | modify values |               |
   |               |             |    | provided via  |               |
   |               |             |    | Modality      |               |
   |               |             |    | Worklist.     |               |
   +---------------+-------------+----+---------------+---------------+
   | Distance      | (0018,1110) | DS | Zero length   | x             |
   | Source to     |             |    |               |               |
   | Detector      |             |    |               |               |
   | (SID)         |             |    |               |               |
   +---------------+-------------+----+---------------+---------------+
   | Image Area    | (0018,115E) | DS | Zero length   | x             |
   | Dose Product  |             |    |               |               |
   +---------------+-------------+----+---------------+---------------+
   | Study ID      | (0020,0010) | SH | From Modality |               |
   |               |             |    | Worklist or   |               |
   |               |             |    | user input.   |               |
   |               |             |    | The user can  |               |
   |               |             |    | modify values |               |
   |               |             |    | provided via  |               |
   |               |             |    | Modality      |               |
   |               |             |    | Worklist.     |               |
   +---------------+-------------+----+---------------+---------------+
   | Performed     | (0040,0241) | AE | MPPS AE Title |               |
   | Station AE    |             |    |               |               |
   | Title         |             |    |               |               |
   +---------------+-------------+----+---------------+---------------+
   | Performed     | (0040,0242) | SH | From          |               |
   | Station Name  |             |    | configuration |               |
   +---------------+-------------+----+---------------+---------------+
   | Performed     | (0040,0243) | SH | From          |               |
   | Location      |             |    | configuration |               |
   +---------------+-------------+----+---------------+---------------+
   | Performed     | (0040,0244) | DA | Actual start  |               |
   | Procedure     |             |    | date          |               |
   | Step Start    |             |    |               |               |
   | Date          |             |    |               |               |
   +---------------+-------------+----+---------------+---------------+
   | Performed     | (0040,0245) | TM | Actual start  |               |
   | Procedure     |             |    | time          |               |
   | Step Start    |             |    |               |               |
   | Time          |             |    |               |               |
   +---------------+-------------+----+---------------+---------------+
   | Performed     | (0040,0250) | DA | Zero length   | Actual end    |
   | Procedure     |             |    |               | date          |
   | Step End Date |             |    |               |               |
   +---------------+-------------+----+---------------+---------------+
   | Performed     | (0040,0251) | TM | Zero length   | Actual end    |
   | Procedure     |             |    |               | time          |
   | Step End Time |             |    |               |               |
   +---------------+-------------+----+---------------+---------------+
   | Performed     | (0040,0252) | CS | IN PROGRESS   | DISCONTINUED  |
   | Procedure     |             |    |               | or COMPLETED  |
   | Step Status   |             |    |               |               |
   +---------------+-------------+----+---------------+---------------+
   | Performed     | (0040,0281) | SQ | Zero length   | If Performed  |
   | Procedure     |             |    |               | Procedure     |
   | Step          |             |    |               | Step Status   |
   | Di            |             |    |               | (0040,0252)   |
   | scontinuation |             |    |               | is            |
   | Reason Code   |             |    |               | "             |
   | Sequence      |             |    |               | DISCONTINUED" |
   |               |             |    |               | then a single |
   |               |             |    |               | item will be  |
   |               |             |    |               | present       |
   |               |             |    |               | containing a  |
   |               |             |    |               | user-selected |
   |               |             |    |               | entry drawn   |
   |               |             |    |               | from .        |
   +---------------+-------------+----+---------------+---------------+
   | Performed     | (0040,0253) | SH | Automatically |               |
   | Procedure     |             |    | created but   |               |
   | Step ID       |             |    | can be        |               |
   |               |             |    | modified by   |               |
   |               |             |    | the user.     |               |
   +---------------+-------------+----+---------------+---------------+
   | Performed     | (0040,0254) | LO | From Modality |               |
   | Procedure     |             |    | Worklist or   |               |
   | Step          |             |    | user input.   |               |
   | Description   |             |    | The user can  |               |
   |               |             |    | modify the    |               |
   |               |             |    | description   |               |
   |               |             |    | provided via  |               |
   |               |             |    | Modality      |               |
   |               |             |    | Worklist.     |               |
   +---------------+-------------+----+---------------+---------------+
   | Performed     | (0040,0255) | LO | Zero length   |               |
   | Procedure     |             |    |               |               |
   | Type          |             |    |               |               |
   | Description   |             |    |               |               |
   +---------------+-------------+----+---------------+---------------+
   | Performed     | (0040,0260) | SQ | Zero length   | Zero or more  |
   | Protocol Code |             |    |               | items         |
   | Sequence      |             |    |               |               |
   +---------------+-------------+----+---------------+---------------+
   | Scheduled     | (0040,0270) | SQ | If 1st dose   |               |
   | Step          |             |    | applied       |               |
   | Attributes    |             |    | results in an |               |
   | Sequence      |             |    | Instance      |               |
   +---------------+-------------+----+---------------+---------------+
   | > Accession   | (0008,0050) | SH | From Modality |               |
   | Number        |             |    | Worklist or   |               |
   |               |             |    | user input.   |               |
   |               |             |    | The user can  |               |
   |               |             |    | modify values |               |
   |               |             |    | provided via  |               |
   |               |             |    | Modality      |               |
   |               |             |    | Worklist.     |               |
   +---------------+-------------+----+---------------+---------------+
   | > Referenced  | (0008,1110) | SQ | From Modality |               |
   | Study         |             |    | Worklist      |               |
   | Sequence      |             |    |               |               |
   +---------------+-------------+----+---------------+---------------+
   | >> Referenced | (0008,1150) | UI | From Modality |               |
   | SOP Class UID |             |    | Worklist      |               |
   +---------------+-------------+----+---------------+---------------+
   | >> Referenced | (0008,1155) | UI | From Modality |               |
   | SOP Instance  |             |    | Worklist      |               |
   | UID           |             |    |               |               |
   +---------------+-------------+----+---------------+---------------+
   | > Study       | (0020,000D) | UI | From Modality |               |
   | Instance UID  |             |    | Worklist      |               |
   +---------------+-------------+----+---------------+---------------+
   | > Requested   | (0032,1060) | LO | From Modality |               |
   | Procedure     |             |    | Worklist      |               |
   | Description   |             |    |               |               |
   +---------------+-------------+----+---------------+---------------+
   | > Scheduled   | (0040,0007) | LO | From Modality |               |
   | Procedure     |             |    | Worklist      |               |
   | Step          |             |    |               |               |
   | Description   |             |    |               |               |
   +---------------+-------------+----+---------------+---------------+
   | > Scheduled   | (0040,0008) | SQ | From Modality |               |
   | Protocol Code |             |    | Worklist      |               |
   | Sequence      |             |    |               |               |
   +---------------+-------------+----+---------------+---------------+
   | > Scheduled   | (0040,0009) | SH | From Modality |               |
   | Procedure     |             |    | Worklist      |               |
   | Step ID       |             |    |               |               |
   +---------------+-------------+----+---------------+---------------+
   | > Requested   | (0040,1001) | SH | From Modality |               |
   | Procedure ID  |             |    | Worklist      |               |
   +---------------+-------------+----+---------------+---------------+
   | Performed     | (0040,0340) | SQ | if 1st dose   | One or more   |
   | Series        |             |    | applied       | items         |
   | Sequence      |             |    | results in an |               |
   |               |             |    | instance      |               |
   +---------------+-------------+----+---------------+---------------+
   | > Retrieve AE | (0008,0054) | AE | x             | x             |
   | Title         |             |    |               |               |
   +---------------+-------------+----+---------------+---------------+
   | > Series      | (0008,103E) | LO | x             | x             |
   | Description   |             |    |               |               |
   +---------------+-------------+----+---------------+---------------+
   | > Performing  | (0008,1050) | PN | x             | x             |
   | Physician's   |             |    |               |               |
   | Name          |             |    |               |               |
   +---------------+-------------+----+---------------+---------------+
   | > Operator's  | (0008,1070) | PN | x             | x             |
   | Name          |             |    |               |               |
   +---------------+-------------+----+---------------+---------------+
   | > Referenced  | (0008,1140) | SQ | One or more   | One or more   |
   | Image         |             |    | items         | items         |
   | Sequence      |             |    |               |               |
   +---------------+-------------+----+---------------+---------------+
   | >> Referenced | (0008,1150) | UI | x             | x             |
   | SOP Class UID |             |    |               |               |
   +---------------+-------------+----+---------------+---------------+
   | >> Referenced | (0008,1155) | UI | x             | x             |
   | SOP Instance  |             |    |               |               |
   | UID           |             |    |               |               |
   +---------------+-------------+----+---------------+---------------+
   | > Protocol    | (0018,1030) | LO | x             | x             |
   | Name          |             |    |               |               |
   +---------------+-------------+----+---------------+---------------+
   | > Series      | (0020,000E) | UI | x             | x             |
   | Instance UID  |             |    |               |               |
   +---------------+-------------+----+---------------+---------------+
   | > Referenced  | (0040,0220) | SQ | Zero length   | Zero length   |
   | Standalone    |             |    | (SOP classes  | (SOP classes  |
   | SOP Instance  |             |    | not           | not           |
   | Seq.          |             |    | supported)    | supported)    |
   +---------------+-------------+----+---------------+---------------+
   | Total Time of | (0040,0300) | US | Zero length   | Total time    |
   | Fluoroscopy   |             |    |               |               |
   +---------------+-------------+----+---------------+---------------+
   | Total Number  | (0040,0301) | US | Zero length   | Number of     |
   | of Exposures  |             |    |               | exposures     |
   +---------------+-------------+----+---------------+---------------+
   | Entrance Dose | (0040,0302) | US | Zero length   | Entrance dose |
   +---------------+-------------+----+---------------+---------------+
   | Exposed Area  | (0040,0303) | US | Zero length   | Exposed area  |
   +---------------+-------------+----+---------------+---------------+
   | Film          | (0040,0321) | SQ | Zero length   | Zero or more  |
   | Consumption   |             |    |               | items         |
   | Sequence      |             |    |               |               |
   +---------------+-------------+----+---------------+---------------+
   | > Medium Type | (2000,0030) | CS |               | x             |
   +---------------+-------------+----+---------------+---------------+
   | > Film Size   | (2010,0050) | CS |               | x             |
   | ID            |             |    |               |               |
   +---------------+-------------+----+---------------+---------------+
   | > Number of   | (2100,0170) | IS |               | x             |
   | Films         |             |    |               |               |
   +---------------+-------------+----+---------------+---------------+

.. _sect_B.4.2.2.4:

Association Acceptance Policy
'''''''''''''''''''''''''''''

The Workflow Application Entity does not accept Associations.

.. _sect_B.4.2.3:

Hardcopy Application Entity Specification
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. _sect_B.4.2.3.1:

SOP Classes
'''''''''''

EXAMPLE-INTEGRATED-MODALITY provides Standard Conformance to the
following SOP Classes:

.. table:: SOP Classes for AE Hardcopy

   ===================================== ====================== === ===
   SOP Class Name                        SOP Class UID          SCU SCP
   ===================================== ====================== === ===
   Basic Grayscale Print Management Meta 1.2.840.10008.5.1.1.9  Yes No
   Presentation LUT                      1.2.840.10008.5.1.1.23 Yes No
   ===================================== ====================== === ===

.. _sect_B.4.2.3.2:

Association Policies
''''''''''''''''''''

.. _sect_B.4.2.3.2.1:

General
       

The DICOM standard application context name for DICOM is always
proposed:

.. table:: DICOM Application Context for AE Hardcopy

   ======================== =====================
   Application Context Name 1.2.840.10008.3.1.1.1
   ======================== =====================

.. _sect_B.4.2.3.2.2:

Number of Associations
                      

EXAMPLE-INTEGRATED-MODALITY initiates one Association at a time for each
configured hardcopy device. Multiple hardcopy devices can be configured.

.. table:: Number of Associations Initiated for AE Hardcopy

   +----------------------------------+----------------------------------+
   | Maximum number of simultaneous   | (number of configured hardcopy   |
   | Associations                     | devices)                         |
   +----------------------------------+----------------------------------+

.. _sect_B.4.2.3.2.3:

Asynchronous Nature
                   

EXAMPLE-INTEGRATED-MODALITY does not support asynchronous communication
(multiple outstanding transactions over a single Association).

.. table:: Asynchronous Nature as a SCU for AE Hardcopy

   ======================================================= =
   Maximum number of outstanding asynchronous transactions 1
   ======================================================= =

.. _sect_B.4.2.3.2.4:

Implementation Identifying Information
                                      

The implementation information for this Application Entity is:

.. table:: DICOM Implementation Class and Version for AE Hardcopy

   =========================== ============================
   Implementation Class UID    1.xxxxxxx.yyy.etc.ad.inf.usw
   Implementation Version Name EXINTMOD_01
   =========================== ============================

.. _sect_B.4.2.3.3:

Association Initiation Policy
'''''''''''''''''''''''''''''

.. _sect_B.4.2.3.3.1:

Activity - Film Images
                      

.. _sect_B.4.2.3.3.1.1:

Description and Sequencing of Activities
                                        

A user composes images onto film sheets and requests them to be sent to
a specific hardcopy device. The user can select the desired film format
and number of copies. Each print-job is forwarded to the job queue and
processed individually.

The Hardcopy AE is invoked by the job control interface that is
responsible for processing network tasks. The job consists of data
describing the images and graphics to be printed as well as the
requested layout and other parameters. The film sheet is internally
processed, converted to a STANDARD/1,1 page and then the page image is
sent. If no association to the printer can be established, the print-job
is switched to a failed state and the user informed.

A typical sequence of DIMSE messages sent over an association between
Hardcopy AE and a Printer is illustrated in
`figure_title <#figure_B.4.2-5>`__:

1.  Hardcopy AE opens an association with the Printer

2.  N-GET on the Printer SOP Class is used to obtain current printer
    status information. If the Printer reports a status of FAILURE, the
    print-job is switched to a failed state and the user informed.

3.  N-CREATE on the Film Session SOP Class creates a Film Session.

4.  N-CREATE on the Presentation LUT SOP Class creates a Presentation
    LUT (if supported by the printer).

5.  N-CREATE on the Film Box SOP Class creates a Film Box linked to the
    Film Session. A single Image Box will be created as the result of
    this operation (Hardcopy AE only uses the format STANDARD\1,1)

6.  N-SET on the Image Box SOP Class transfers the contents of the film
    sheet to the printer. If the printer does not support the
    Presentation LUT SOP Class, the image data will be passed through a
    printer-specific correction LUT before being sent.

7.  N-ACTION on the Film Box SOP Class instructs the printer to print
    the Film Box

8.  The printer prints the requested number of film sheets

9.  The Printer asynchronously reports its status via N-EVENT-REPORT
    notification (Printer SOP Class). The printer can send this message
    at any time. Hardcopy AE does not require the N-EVENT-REPORT to be
    sent. Hardcopy AE is capable of receiving an N-EVENT-REPORT
    notification at any time during an association. If the Printer
    reports a status of FAILURE, the print-job is switched to a failed
    state and the user informed.

10. N-DELETE on the Film Session SOP Class deletes the complete Film
    Session SOP Instance hierarchy.

11. Hardcopy AE closes the association with the Printer

Status of the print-job is reported through the job control interface.
Only one job will be active at a time for each separate hardcopy device.
If any Response from the remote Application contains a status other than
Success or Warning, the Association is aborted and the related Job is
switched to a failed state. It can be restarted any time by user
interaction or, if configured, by automated retry.

.. _sect_B.4.2.3.3.1.2:

Proposed Presentation Contexts
                              

EXAMPLE-INTEGRATED-MODALITY is capable of proposing the Presentation
Contexts shown in the Table below:

.. table:: Proposed Presentation Contexts for Activity Film Images

   +------------+------------+------------+------------+-----+------+
   | Pr         |            |            |            |     |      |
   | esentation |            |            |            |     |      |
   | Context    |            |            |            |     |      |
   | Table      |            |            |            |     |      |
   +============+============+============+============+=====+======+
   | Basic      | 1          | Implicit   | 1.2.840    | SCU | None |
   | Grayscale  | .2.840.100 | VR Little  | .10008.1.2 |     |      |
   | Print      | 08.5.1.1.9 | Endian     |            |     |      |
   | Management |            |            | 1.2.840.1  |     |      |
   | Meta       |            | Explicit   | 0008.1.2.1 |     |      |
   |            |            | VR Little  |            |     |      |
   |            |            | Endian     |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | Pr         | 1.         | Implicit   | 1.2.840    | SCU | None |
   | esentation | 2.840.1000 | VR Little  | .10008.1.2 |     |      |
   | LUT        | 8.5.1.1.23 | Endian     |            |     |      |
   |            |            |            | 1.2.840.1  |     |      |
   |            |            | Explicit   | 0008.1.2.1 |     |      |
   |            |            | VR Little  |            |     |      |
   |            |            | Endian     |            |     |      |
   +------------+------------+------------+------------+-----+------+

.. _sect_B.4.2.3.3.1.3:

Common SOP Specific Conformance for All Print SOP Classes
                                                         

The general behavior of Hardcopy AE during communication failure is
summarized in the Table below. This behavior is common for all SOP
Classes supported by Hardcopy AE.

.. table:: Hardcopy Communication Failure Behavior

   +----------------------------------+----------------------------------+
   | Exception                        | Behavior                         |
   +==================================+==================================+
   | Timeout                          | The Association is aborted using |
   |                                  | A-ABORT and the print-job is     |
   |                                  | marked as failed. The reason is  |
   |                                  | logged and the job failure is    |
   |                                  | reported to the user via the job |
   |                                  | control application.             |
   +----------------------------------+----------------------------------+
   | Association aborted by the SCP   | The print-job is marked as       |
   | or network layers                | failed. The reason is logged and |
   |                                  | the job failure is reported to   |
   |                                  | the user via the job control     |
   |                                  | application.                     |
   +----------------------------------+----------------------------------+

.. _sect_B.4.2.3.3.1.4:

SOP Specific Conformance for the Printer SOP Class
                                                  

Hardcopy AE supports the following DIMSE operations and notifications
for the Printer SOP Class:

-  N-GET

-  N-EVENT-REPORT

Details of the supported attributes and status handling behavior are
described in the following subsections.

.. _sect_B.4.2.3.3.1.4.1:

Printer SOP Class Operations (N-GET)
                                    

Hardcopy AE uses the Printer SOP Class N-GET operation to obtain
information about the current printer status. The attributes obtained
via N-GET are listed in the Table below:

.. table:: Printer SOP Class N-GET Request Attributes

   +-----------+-----------+----+-----------+-----------+---------+
   | Attribute | Tag       | VR | Value     | Presence  | Source  |
   | Name      |           |    |           | of Value  |         |
   +===========+===========+====+===========+===========+=========+
   | Printer   | (2        | CS | Provided  | ALWAYS    | Printer |
   | Status    | 110,0010) |    | by        |           |         |
   |           |           |    | Printer   |           |         |
   +-----------+-----------+----+-----------+-----------+---------+
   | Printer   | (2        | CS | Provided  | ALWAYS    | Printer |
   | Status    | 110,0020) |    | by        |           |         |
   | Info      |           |    | Printer   |           |         |
   +-----------+-----------+----+-----------+-----------+---------+

The Printer Status information is evaluated as follows:

1. If Printer status (2110,0010) is NORMAL, the print-job continues to
   be printed.

2. If Printer status (2110,0010) is FAILURE, the print-job is marked as
   failed. The contents of Printer Status Info (2110,0020) is logged and
   reported to the user via the job ­control application.

3. If Printer status (2110,0010) is WARNING, the print-job continues to
   be printed. The contents of Printer Status Info (2110,0020) is logged
   and reported to the user via the job­ control application.

The behavior of Hardcopy AE when encountering status codes in a N-GET
response is summarized in the Table below:

.. table:: Printer SOP Class N-GET Response Status Handling Behavior

   +----------------+----------------+----------------+----------------+
   | Service Status | Further        | Error Code     | Behavior       |
   |                | Meaning        |                |                |
   +================+================+================+================+
   | Success        | Success        | 0000           | The request to |
   |                |                |                | get printer    |
   |                |                |                | status         |
   |                |                |                | information    |
   |                |                |                | was success.   |
   +----------------+----------------+----------------+----------------+
   | \*             | \*             | Any other      | The            |
   |                |                | status code.   | Association is |
   |                |                |                | aborted using  |
   |                |                |                | A-ABORT and    |
   |                |                |                | the print-job  |
   |                |                |                | is marked as   |
   |                |                |                | failed. The    |
   |                |                |                | status meaning |
   |                |                |                | is logged and  |
   |                |                |                | reported to    |
   |                |                |                | the user.      |
   +----------------+----------------+----------------+----------------+

.. _sect_B.4.2.3.3.1.4.2:

Printer SOP Class Notifications (N-EVENT-REPORT)
                                                

Hardcopy AE is capable of receiving an N-EVENT-REPORT request at any
time during an association.

The behavior of Hardcopy AE when receiving Event Types within the
N-EVENT-REPORT is summarized in the Table below:

.. table:: Printer SOP Class N-EVENT-REPORT Behavior

   +-----------------+---------------+----------------------------------+
   | Event Type Name | Event Type ID | Behavior                         |
   +=================+===============+==================================+
   | Normal          | 1             | The print-job continues to be    |
   |                 |               | printed.                         |
   +-----------------+---------------+----------------------------------+
   | Warning         | 2             | The print-job continues to be    |
   |                 |               | printed. The contents of Printer |
   |                 |               | Status Info (2110,0020) is       |
   |                 |               | logged and reported to the user  |
   |                 |               | via the job-control application. |
   +-----------------+---------------+----------------------------------+
   | Failure         | 3             | The print-job is marked as       |
   |                 |               | failed. The contents of Printer  |
   |                 |               | Status Info (2110,0020) is       |
   |                 |               | logged and reported to the user  |
   |                 |               | via the job-control application. |
   +-----------------+---------------+----------------------------------+
   | \*              | \*            | An invalid Event Type ID will    |
   |                 |               | cause a status code of 0113H to  |
   |                 |               | be returned in a N-EVENT-REPORT  |
   |                 |               | response.                        |
   +-----------------+---------------+----------------------------------+

The reasons for returning specific status codes in a N-EVENT-REPORT
response are summarized in the Table below:

.. table:: Printer SOP Class N-EVENT-REPORT Response Status Reasons

   +----------------+-----------------+------------+-----------------+
   | Service Status | Further Meaning | Error Code | Reasons         |
   +================+=================+============+=================+
   | Success        | Success         | 0000       | The             |
   |                |                 |            | notification    |
   |                |                 |            | event has been  |
   |                |                 |            | successfully    |
   |                |                 |            | received.       |
   +----------------+-----------------+------------+-----------------+
   | Failure        | No Such Event   | 0113H      | An invalid      |
   |                | Type            |            | Event Type ID   |
   |                |                 |            | was supplied in |
   |                |                 |            | the             |
   |                |                 |            | N-EVENT-REPORT  |
   |                |                 |            | request.        |
   +----------------+-----------------+------------+-----------------+
   | Failure        | Processing      | 0110H      | An internal     |
   |                | Failure         |            | error occurred  |
   |                |                 |            | during          |
   |                |                 |            | processing of   |
   |                |                 |            | the             |
   |                |                 |            | N-EVENT-REPORT. |
   |                |                 |            | A short         |
   |                |                 |            | description of  |
   |                |                 |            | the error will  |
   |                |                 |            | be returned in  |
   |                |                 |            | Error Comment   |
   |                |                 |            | (0000,0902).    |
   +----------------+-----------------+------------+-----------------+

.. _sect_B.4.2.3.3.1.5:

SOP Specific Conformance for the Film Session SOP Class
                                                       

Hardcopy AE supports the following DIMSE operations for the Film Session
SOP Class:

-  N-CREATE

-  N-DELETE

Details of the supported attributes and status handling behavior are
described in the following subsections.

.. _sect_B.4.2.3.3.1.5.1:

Film Session SOP Class Operations (N-CREATE)
                                            

The attributes supplied in an N-CREATE Request are listed in the Table
below:

.. table:: Film Session SOP Class N-CREATE Request Attributes

   +------------+------------+----+------------+------------+--------+
   | Attribute  | Tag        | VR | Value      | Presence   | Source |
   | Name       |            |    |            | of Value   |        |
   +============+============+====+============+============+========+
   | Number of  | (          | IS | 1 .. 10    | ALWAYS     | User   |
   | Copies     | 2000,0010) |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | Medium     | (          | CS | BLUE FILM, | ALWAYS     | User   |
   | Type       | 2000,0030) |    | CLEAR FILM |            |        |
   |            |            |    | or PAPER   |            |        |
   +------------+------------+----+------------+------------+--------+
   | Film       | (          | CS | MAGAZINE   | ALWAYS     | User   |
   | D          | 2000,0040) |    | or         |            |        |
   | estination |            |    | PROCESSOR  |            |        |
   +------------+------------+----+------------+------------+--------+

The behavior of Hardcopy AE when encountering status codes in a N-CREATE
response is summarized in the Table below:

.. table:: Film Session SOP Class N-CREATE Response Status Handling
Behavior

   +----------------+----------------+----------------+----------------+
   | Service Status | Further        | Error Code     | Behavior       |
   |                | Meaning        |                |                |
   +================+================+================+================+
   | Success        | Success        | 0000           | The SCP has    |
   |                |                |                | completed the  |
   |                |                |                | operation      |
   |                |                |                | successfully.  |
   +----------------+----------------+----------------+----------------+
   | Warning        | Attribute      | 0116H          | The N-CREATE   |
   |                | Value Out of   |                | operation is   |
   |                | Range          |                | considered     |
   |                |                |                | successful but |
   |                |                |                | the status     |
   |                |                |                | meaning is     |
   |                |                |                | logged.        |
   |                |                |                | Additional     |
   |                |                |                | information in |
   |                |                |                | the Response   |
   |                |                |                | identifying    |
   |                |                |                | the attributes |
   |                |                |                | out of range   |
   |                |                |                | will be logged |
   |                |                |                | (i.e.,         |
   |                |                |                | Elements in    |
   |                |                |                | the            |
   |                |                |                | Modification   |
   |                |                |                | List/Attribute |
   |                |                |                | List)          |
   +----------------+----------------+----------------+----------------+
   | Warning        | Attribute List | 0107H          | The N-CREATE   |
   |                | Error          |                | operation is   |
   |                |                |                | considered     |
   |                |                |                | successful but |
   |                |                |                | the status     |
   |                |                |                | meaning is     |
   |                |                |                | logged.        |
   |                |                |                | Additional     |
   |                |                |                | information in |
   |                |                |                | the Response   |
   |                |                |                | identifying    |
   |                |                |                | the attributes |
   |                |                |                | will be logged |
   |                |                |                | (i.e.,         |
   |                |                |                | Elements in    |
   |                |                |                | the Attribute  |
   |                |                |                | Identifier     |
   |                |                |                | List)          |
   +----------------+----------------+----------------+----------------+
   | \*             | \*             | Any other      | The            |
   |                |                | status code.   | Association is |
   |                |                |                | aborted using  |
   |                |                |                | A-ABORT and    |
   |                |                |                | the print-job  |
   |                |                |                | is marked as   |
   |                |                |                | failed. The    |
   |                |                |                | status meaning |
   |                |                |                | is logged and  |
   |                |                |                | reported to    |
   |                |                |                | the user.      |
   +----------------+----------------+----------------+----------------+

.. _sect_B.4.2.3.3.1.5.2:

Film Session SOP Class Operations (N-DELETE)
                                            

The behavior of Hardcopy AE when encountering status codes in a N-DELETE
response is summarized in the Table below:

.. table:: Printer SOP Class N-DELETE Response Status Handling Behavior

   +----------------+----------------+----------------+----------------+
   | Service Status | Further        | Error Code     | Behavior       |
   |                | Meaning        |                |                |
   +================+================+================+================+
   | Success        | Success        | 0000           | The SCP has    |
   |                |                |                | completed the  |
   |                |                |                | operation      |
   |                |                |                | successfully.  |
   +----------------+----------------+----------------+----------------+
   | \*             | \*             | Any other      | The            |
   |                |                | status code.   | Association is |
   |                |                |                | aborted using  |
   |                |                |                | A-ABORT and    |
   |                |                |                | the print-job  |
   |                |                |                | is marked as   |
   |                |                |                | failed. The    |
   |                |                |                | status meaning |
   |                |                |                | is logged and  |
   |                |                |                | reported to    |
   |                |                |                | the user.      |
   +----------------+----------------+----------------+----------------+

.. _sect_B.4.2.3.3.1.6:

SOP Specific Conformance for the Presentation LUT SOP Class
                                                           

Hardcopy AE supports the following DIMSE operations for the Presentation
LUT SOP Class:

-  N-CREATE

Details of the supported attributes and status handling behavior are
described in the following subsections.

.. _sect_B.4.2.3.3.1.6.1:

Presentation LUT SOP Class Operations (N-CREATE)
                                                

The attributes supplied in an N-CREATE Request are listed in the Table
below:

.. table:: Presentation LUT SOP Class N-CREATE Request Attributes

   ====================== =========== == ======== ================= ======
   Attribute Name         Tag         VR Value    Presence of Value Source
   ====================== =========== == ======== ================= ======
   Presentation LUT Shape (2050,0020) CS IDENTITY ALWAYS            Auto
   ====================== =========== == ======== ================= ======

The behavior of Hardcopy AE when encountering status codes in a N-CREATE
response is summarized in the Table below:

.. table:: Presentation LUT SOP Class N-CREATE Response Status Handling
Behavior

   +----------------+----------------+----------------+----------------+
   | Service Status | Further        | Error Code     | Behavior       |
   |                | Meaning        |                |                |
   +================+================+================+================+
   | Success        | Success        | 0000           | The SCP has    |
   |                |                |                | completed the  |
   |                |                |                | operation      |
   |                |                |                | successfully.  |
   +----------------+----------------+----------------+----------------+
   | Warning        | Requested Min  | B605H          | The N-CREATE   |
   |                | Density or Max |                | operation is   |
   |                | Density        |                | considered     |
   |                | outside of     |                | successful but |
   |                | printer's      |                | the status     |
   |                | operating      |                | meaning is     |
   |                | range          |                | logged.        |
   +----------------+----------------+----------------+----------------+
   | \*             | \*             | Any other      | The            |
   |                |                | status code.   | Association is |
   |                |                |                | aborted using  |
   |                |                |                | A-ABORT and    |
   |                |                |                | the print-job  |
   |                |                |                | is marked as   |
   |                |                |                | failed. The    |
   |                |                |                | status meaning |
   |                |                |                | is logged and  |
   |                |                |                | reported to    |
   |                |                |                | the user.      |
   +----------------+----------------+----------------+----------------+
   | Service Status | Further        | Error Code     | Behavior       |
   |                | Meaning        |                |                |
   +----------------+----------------+----------------+----------------+
   | Success        | Success        | 0000           | The SCP has    |
   |                |                |                | completed the  |
   |                |                |                | operation      |
   |                |                |                | successfully.  |
   +----------------+----------------+----------------+----------------+

.. _sect_B.4.2.3.3.1.7:

SOP Specific Conformance for the Film Box SOP Class
                                                   

Hardcopy AE supports the following DIMSE operations for the Presentation
LUT SOP Class:

-  N-CREATE

-  N-ACTION

Details of the supported attributes and status handling behavior are
described in the following subsections.

.. _sect_B.4.2.3.3.1.7.1:

Film Box SOP Class Operations (N-CREATE)
                                        

The attributes supplied in an N-CREATE Request are listed in the Table
below:

.. table:: Film Box SOP Class N-CREATE Request Attributes

   +------------+------------+----+------------+------------+--------+
   | Attribute  | Tag        | VR | Value      | Presence   | Source |
   | Name       |            |    |            | of Value   |        |
   +============+============+====+============+============+========+
   | Image      | (          | CS | ST         | ALWAYS     | Auto   |
   | Display    | 2010,0010) |    | ANDARD\1,1 |            |        |
   | Format     |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | Referenced | (          | SQ |            | ALWAYS     | Auto   |
   | Film       | 2010,0500) |    |            |            |        |
   | Session    |            |    |            |            |        |
   | Sequence   |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | >          | (          | UI | 1          | ALWAYS     | Auto   |
   | Referenced | 0008,1150) |    | .2.840.100 |            |        |
   | SOP Class  |            |    | 08.5.1.1.1 |            |        |
   | UID        |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | >          | (          | UI | From       | ALWAYS     | Auto   |
   | Referenced | 0008,1155) |    | created    |            |        |
   | SOP        |            |    | Film       |            |        |
   | Instance   |            |    | Session    |            |        |
   | UID        |            |    | SOP        |            |        |
   |            |            |    | Instance   |            |        |
   +------------+------------+----+------------+------------+--------+
   | Film       | (          | CS | PORTRAIT   | ALWAYS     | User   |
   | O          | 2010,0040) |    | or         |            |        |
   | rientation |            |    | LANDSCAPE  |            |        |
   +------------+------------+----+------------+------------+--------+
   | Film Size  | (          | CS | 14INX17IN, | ALWAYS     | User   |
   | ID         | 2010,0050) |    | 14INX14IN, |            |        |
   |            |            |    | 11INX14IN, |            |        |
   |            |            |    | 11INX11IN, |            |        |
   |            |            |    | 85INX11IN, |            |        |
   |            |            |    | 8INX10IN   |            |        |
   +------------+------------+----+------------+------------+--------+
   | Mag        | (          | CS | REPLICATE, | ALWAYS     | User   |
   | nification | 2010,0060) |    | BILINEAR,  |            |        |
   | Type       |            |    | CUBIC or   |            |        |
   |            |            |    | NONE       |            |        |
   +------------+------------+----+------------+------------+--------+
   | Border     | (          | CS | BLACK or   | ALWAYS     | User   |
   | Density    | 2010,0100) |    | WHITE      |            |        |
   +------------+------------+----+------------+------------+--------+
   | Max        | (          | US | 0 .. 310   | ALWAYS     | Auto   |
   | Density    | 2010,0130) |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | Min        | (          | US | 0 .. 50    | ALWAYS     | Auto   |
   | Density    | 2010,0120) |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | Il         | (          | US | 0 .. 5000  | ALWAYS     | User   |
   | lumination | 2010,015E) |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | Reflective | (          | US | 0 .. 100   | ALWAYS     | User   |
   | Ambient    | 2010,0160) |    |            |            |        |
   | Light      |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | Referenced | (          | SQ | Only sent  | ANAP       | Auto   |
   | Pr         | 2050,0500) |    | if         |            |        |
   | esentation |            |    | Pr         |            |        |
   | LUT        |            |    | esentation |            |        |
   | Sequence   |            |    | LUT SOP    |            |        |
   |            |            |    | Class has  |            |        |
   |            |            |    | been       |            |        |
   |            |            |    | n          |            |        |
   |            |            |    | egotiated. |            |        |
   +------------+------------+----+------------+------------+--------+
   | >          | (          | UI | 1.         | ALWAYS     | Auto   |
   | Referenced | 0008,1150) |    | 2.840.1000 |            |        |
   | SOP Class  |            |    | 8.5.1.1.23 |            |        |
   | UID        |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | >          | (          | UI | From       | ALWAYS     | Auto   |
   | Referenced | 0008,1155) |    | created    |            |        |
   | SOP        |            |    | Pr         |            |        |
   | Instance   |            |    | esentation |            |        |
   | UID        |            |    | LUT SOP    |            |        |
   |            |            |    | Instance   |            |        |
   +------------+------------+----+------------+------------+--------+

The behavior of Hardcopy AE when encountering status codes in a N-CREATE
response is summarized in the Table below:

.. table:: Film Box SOP Class N-CREATE Response Status Handling Behavior

   +----------------+----------------+----------------+----------------+
   | Service Status | Further        | Error Code     | Behavior       |
   |                | Meaning        |                |                |
   +================+================+================+================+
   | Success        | Success        | 0000           | The SCP has    |
   |                |                |                | completed the  |
   |                |                |                | operation      |
   |                |                |                | successfully.  |
   +----------------+----------------+----------------+----------------+
   | Warning        | Requested Min  | B605H          | The N-CREATE   |
   |                | Density or Max |                | operation is   |
   |                | Density        |                | considered     |
   |                | outside of     |                | successful but |
   |                | printer's      |                | the status     |
   |                | operating      |                | meaning is     |
   |                | range          |                | logged.        |
   +----------------+----------------+----------------+----------------+
   | \*             | \*             | Any other      | The            |
   |                |                | status code.   | Association is |
   |                |                |                | aborted using  |
   |                |                |                | A-ABORT and    |
   |                |                |                | the print-job  |
   |                |                |                | is marked as   |
   |                |                |                | failed. The    |
   |                |                |                | status meaning |
   |                |                |                | is logged and  |
   |                |                |                | reported to    |
   |                |                |                | the user.      |
   +----------------+----------------+----------------+----------------+

.. _sect_B.4.2.3.3.1.7.2:

Film Box SOP Class Operations (N-ACTION)
                                        

An N-ACTION Request is issued to instruct the Print SCP to print the
contents of the Film Box. The Action Reply argument in an N-ACTION
response is not evaluated.

The behavior of Hardcopy AE when encountering status codes in a N-ACTION
response is summarized in the Table below:

.. table:: Film Box SOP Class N-ACTION Response Status Handling Behavior

   +----------------+----------------+----------------+----------------+
   | Service Status | Further        | Error Code     | Behavior       |
   |                | Meaning        |                |                |
   +================+================+================+================+
   | Success        | Success        | 0000           | The SCP has    |
   |                |                |                | completed the  |
   |                |                |                | operation      |
   |                |                |                | successfully.  |
   |                |                |                | The film has   |
   |                |                |                | been accepted  |
   |                |                |                | for printing.  |
   +----------------+----------------+----------------+----------------+
   | Warning        | Film Box SOP   | B603H          | The            |
   |                | Instance       |                | Association is |
   |                | hierarchy does |                | aborted using  |
   |                | not contain    |                | A-ABORT and    |
   |                | Image Box SOP  |                | the print-job  |
   |                | Instances      |                | is marked as   |
   |                | (empty page)   |                | failed. The    |
   |                |                |                | status meaning |
   |                |                |                | is logged and  |
   |                |                |                | reported to    |
   |                |                |                | the user.      |
   +----------------+----------------+----------------+----------------+
   | Warning        | Image size is  | B604H          | The N-ACTION   |
   |                | larger than    |                | operation is   |
   |                | Image Box      |                | considered     |
   |                | size. The      |                | successful but |
   |                | image has been |                | the status     |
   |                | demagnified.   |                | meaning is     |
   |                |                |                | logged.        |
   +----------------+----------------+----------------+----------------+
   | Warning        | Image size is  | B609H          | The N-ACTION   |
   |                | larger than    |                | operation is   |
   |                | Image Box      |                | considered     |
   |                | size. The      |                | successful but |
   |                | image has been |                | the status     |
   |                | cropped to     |                | meaning is     |
   |                | fit.           |                | logged.        |
   +----------------+----------------+----------------+----------------+
   | Warning        | Image size or  | B60AH          | The N-ACTION   |
   |                | Combined Print |                | operation is   |
   |                | Image Size is  |                | considered     |
   |                | larger than    |                | successful but |
   |                | Image Box      |                | the status     |
   |                | size. The      |                | meaning is     |
   |                | image or       |                | logged.        |
   |                | combined Print |                |                |
   |                | Image has been |                |                |
   |                | decimated to   |                |                |
   |                | fit.           |                |                |
   +----------------+----------------+----------------+----------------+
   | Failure        | Unable to      | C602           | The            |
   |                | create Print   |                | Association is |
   |                | Job SOP        |                | aborted using  |
   |                | Instance;      |                | A-ABORT and    |
   |                | print queue is |                | the print-job  |
   |                | full.          |                | is marked as   |
   |                |                |                | failed. The    |
   |                |                |                | status meaning |
   |                |                |                | is logged and  |
   |                |                |                | reported to    |
   |                |                |                | the user.      |
   +----------------+----------------+----------------+----------------+
   | Failure        | Image size is  | C603           | The            |
   |                | larger than    |                | Association is |
   |                | Image Box      |                | aborted using  |
   |                | size.          |                | A-ABORT and    |
   |                |                |                | the print-job  |
   |                |                |                | is marked as   |
   |                |                |                | failed. The    |
   |                |                |                | status meaning |
   |                |                |                | is logged and  |
   |                |                |                | reported to    |
   |                |                |                | the user.      |
   +----------------+----------------+----------------+----------------+
   | Failure        | Combined Print | C613           | The            |
   |                | Image Size is  |                | Association is |
   |                | larger than    |                | aborted using  |
   |                | Image Box      |                | A-ABORT and    |
   |                | size.          |                | the print-job  |
   |                |                |                | is marked as   |
   |                |                |                | failed. The    |
   |                |                |                | status meaning |
   |                |                |                | is logged and  |
   |                |                |                | reported to    |
   |                |                |                | the user.      |
   +----------------+----------------+----------------+----------------+
   | \*             | \*             | Any other      | The            |
   |                |                | status code.   | Association is |
   |                |                |                | aborted using  |
   |                |                |                | A-ABORT and    |
   |                |                |                | the print-job  |
   |                |                |                | is marked as   |
   |                |                |                | failed. The    |
   |                |                |                | status meaning |
   |                |                |                | is logged and  |
   |                |                |                | reported to    |
   |                |                |                | the user.      |
   +----------------+----------------+----------------+----------------+

.. _sect_B.4.2.3.3.1.8:

SOP Specific Conformance for the Image Box SOP Class
                                                    

Hardcopy AE supports the following DIMSE operations for the Image Box
SOP Class:

-  N-SET

Details of the supported attributes and status handling behavior are
described in the following subsections.

.. _sect_B.4.2.3.3.1.8.1:

Image Box SOP Class Operations (N-SET)
                                      

The attributes supplied in an N-SET Request are listed in the Table
below:

.. table:: Image Box SOP Class N-SET Request Attributes

   +------------+------------+----+------------+------------+--------+
   | Attribute  | Tag        | VR | Value      | Presence   | Source |
   | Name       |            |    |            | of Value   |        |
   +============+============+====+============+============+========+
   | Image      | (          | US | 1          | ALWAYS     | Auto   |
   | Position   | 2020,0010) |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | Basic      | (          | SQ |            | ALWAYS     | Auto   |
   | Grayscale  | 2020,0110) |    |            |            |        |
   | Image      |            |    |            |            |        |
   | Sequence   |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | >Samples   | (          | US | 1          | ALWAYS     | Auto   |
   | Per Pixel  | 0028,0002) |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | >P         | (          | CS | M          | ALWAYS     | Auto   |
   | hotometric | 0028,0004) |    | ONOCHROME2 |            |        |
   | Inte       |            |    |            |            |        |
   | rpretation |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | >Rows      | (          | US | Depends on | ALWAYS     | Auto   |
   |            | 0028,0010) |    | film size  |            |        |
   +------------+------------+----+------------+------------+--------+
   | >Columns   | (          | US | Depends on | ALWAYS     | Auto   |
   |            | 0028,0011) |    | film size  |            |        |
   +------------+------------+----+------------+------------+--------+
   | >Pixel     | (          | IS | 1\1        | ALWAYS     | Auto   |
   | Aspect     | 0028,0034) |    |            |            |        |
   | Ratio      |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | >Bits      | (          | US | 8          | ALWAYS     | Auto   |
   | Allocated  | 0028,0100) |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | >Bits      | (          | US | 8          | ALWAYS     | Auto   |
   | Stored     | 0028,0101) |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | >High Bit  | (          | US | 7          | ALWAYS     | Auto   |
   |            | 0028,0102) |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | >Pixel     | (          | US | 0          | ALWAYS     | Auto   |
   | Repr       | 0028,0103) |    |            |            |        |
   | esentation |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | >Pixel     | (          | OB | Pixels of  | ALWAYS     | Auto   |
   | Data       | 7FE0,0010) |    | rendered   |            |        |
   |            |            |    | film sheet |            |        |
   +------------+------------+----+------------+------------+--------+

The behavior of Hardcopy AE when encountering status codes in a N-SET
response is summarized in the Table below:

.. table:: Image Box SOP Class N-SET Response Status Handling Behavior

   +----------------+----------------+----------------+----------------+
   | Service Status | Further        | Error Code     | Behavior       |
   |                | Meaning        |                |                |
   +================+================+================+================+
   | Success        | Success        | 0000           | The SCP has    |
   |                |                |                | completed the  |
   |                |                |                | operation      |
   |                |                |                | successfully.  |
   |                |                |                | Image          |
   |                |                |                | successfully   |
   |                |                |                | stored in      |
   |                |                |                | Image Box.     |
   +----------------+----------------+----------------+----------------+
   | Warning        | Image size is  | B604H          | The N-SET      |
   |                | larger than    |                | operation is   |
   |                | Image Box      |                | considered     |
   |                | size. The      |                | successful but |
   |                | image has been |                | the status     |
   |                | demagnified.   |                | meaning is     |
   |                |                |                | logged.        |
   +----------------+----------------+----------------+----------------+
   | Warning        | Requested Min  | B605H          | The N-SET      |
   |                | Density or Max |                | operation is   |
   |                | Density        |                | considered     |
   |                | outside of     |                | successful but |
   |                | printer's      |                | the status     |
   |                | operating      |                | meaning is     |
   |                | range.         |                | logged.        |
   +----------------+----------------+----------------+----------------+
   | Warning        | Image size is  | B609H          | The N-SET      |
   |                | larger than    |                | operation is   |
   |                | Image Box      |                | considered     |
   |                | size. The      |                | successful but |
   |                | image has been |                | the status     |
   |                | cropped to     |                | meaning is     |
   |                | fit.           |                | logged.        |
   +----------------+----------------+----------------+----------------+
   | Warning        | Image size or  | B60AH          | The N-SET      |
   |                | Combined Print |                | operation is   |
   |                | Image Size is  |                | considered     |
   |                | larger than    |                | successful but |
   |                | Image Box      |                | the status     |
   |                | size. The      |                | meaning is     |
   |                | image or       |                | logged.        |
   |                | combined Print |                |                |
   |                | Image has been |                |                |
   |                | decimated to   |                |                |
   |                | fit.           |                |                |
   +----------------+----------------+----------------+----------------+
   | Failure        | Image size is  | C603           | The            |
   |                | larger than    |                | Association is |
   |                | Image Box      |                | aborted using  |
   |                | size.          |                | A-ABORT and    |
   |                |                |                | the print-job  |
   |                |                |                | is marked as   |
   |                |                |                | failed. The    |
   |                |                |                | status meaning |
   |                |                |                | is logged and  |
   |                |                |                | reported to    |
   |                |                |                | the user.      |
   +----------------+----------------+----------------+----------------+
   | Failure        | Insufficient   | C605           | The            |
   |                | memory in      |                | Association is |
   |                | printer to     |                | aborted using  |
   |                | store the      |                | A-ABORT and    |
   |                | image.         |                | the print-job  |
   |                |                |                | is marked as   |
   |                |                |                | failed. The    |
   |                |                |                | status meaning |
   |                |                |                | is logged and  |
   |                |                |                | reported to    |
   |                |                |                | the user.      |
   +----------------+----------------+----------------+----------------+
   | Failure        | Combined Print | C613           | The            |
   |                | Image Size is  |                | Association is |
   |                | larger than    |                | aborted using  |
   |                | Image Box      |                | A-ABORT and    |
   |                | size.          |                | the print-job  |
   |                |                |                | is marked as   |
   |                |                |                | failed. The    |
   |                |                |                | status meaning |
   |                |                |                | is logged and  |
   |                |                |                | reported to    |
   |                |                |                | the user.      |
   +----------------+----------------+----------------+----------------+
   | \*             | \*             | Any other      | The            |
   |                |                | status code.   | Association is |
   |                |                |                | aborted using  |
   |                |                |                | A-ABORT and    |
   |                |                |                | the print-job  |
   |                |                |                | is marked as   |
   |                |                |                | failed. The    |
   |                |                |                | status meaning |
   |                |                |                | is logged and  |
   |                |                |                | reported to    |
   |                |                |                | the user.      |
   +----------------+----------------+----------------+----------------+

.. _sect_B.4.2.3.4:

Association Acceptance Policy
'''''''''''''''''''''''''''''

The Hardcopy Application Entity does not accept Associations.

.. _sect_B.4.3:

Network Interfaces
~~~~~~~~~~~~~~~~~~

.. _sect_B.4.3.1:

Physical Network Interface
^^^^^^^^^^^^^^^^^^^^^^^^^^

EXAMPLE-INTEGRATED-MODALITY supports a single network interface. One of
the following physical network interfaces will be available depending on
installed hardware options:

.. table:: Supported Physical Network Interfaces

   +-------------------+
   | Ethernet 100baseT |
   +-------------------+
   | Ethernet 10baseT  |
   +-------------------+

.. _sect_B.4.3.2:

Additional Protocols
^^^^^^^^^^^^^^^^^^^^

EXAMPLE-INTEGRATED-MODLALITY conforms to the System Management Profiles
listed in the Table below. All requested transactions for the listed
profiles and actors are supported. Support for optional transactions are
listed in the Table below:

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
   | Time        | NTP Client  | NTP         | Find NTP    |             |
   | Sync        |             |             | Server      |             |
   | hronization |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | DHCP Client | DHCP        | N/A         |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | DICOM       | LDAP Client | LDAP        | Client      | See         |
   | Application |             |             | Update LDAP | `S          |
   | Co          |             |             | Server      | ecurity <#s |
   | nfiguration |             |             |             | ect_B.7>`__ |
   | Management  |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+

.. _sect_B.4.3.2.1:

DHCP
''''

DHCP can be used to obtain TCP/IP network configuration information. The
network parameters obtainable via DHCP are shown in the Table below. The
Default Value column of the table shows the default used if the DHCP
server does not provide a value. Values for network parameters set in
the Service/Installation tool take precedence over values obtained from
the DHCP server. Support for DHCP can be configured via the
Service/Installation Tool. The Service/Installation tool can be used to
configure the machine name. If DHCP is not in use, TCP/IP network
configuration information can be manually configured via the
Service/Installation Tool.

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
   Time offset         Site configurable (from Timezone)
   MTU                 Network Hardware Dependent
   Auto-IP permission  No permission
   =================== ============================================

If the DHCP server refuses to renew a lease on the assigned IP address
all active DICOM Associations will be aborted.

.. _sect_B.4.3.2.2:

DNS
'''

DNS can be used for address resolution. If DHCP is not in use or the
DHCP server does not return any DNS server addresses, the identity of a
DNS server can be configured via the Service/Installation Tool. If a DNS
server is not in use, local mapping between hostname and IP address can
be manually configured via the Service/Installation Tool.

.. _sect_B.4.3.2.3:

NTP
'''

The NTP client implements the optional Find NTP Server Transaction. The
NTP client will issue an NTP broadcast to identify any local NTP
servers. If no local servers can found via NTP broadcast, the NTP
Servers identified by DHCP will be used as time references.
Additionally, one or more NTP Servers can be configured via the
Service/Installation Tool. If no NTP Servers are identified then the
local clock will be used as a time reference and a warning written to
the system log files.

.. _sect_B.4.3.2.4:

LDAP
''''

LDAP can be used to obtain information about network Application
Entities. The identity of an LDAP server can be obtained using the Find
LDAP Server Transaction of the DICOM Application Configuration
Management Profile (i.e., a DNS SRV RR query for the LDAP service) and
the first LDAP server returned will be used. The Service/Installation
Tool can also be used to manually configure the identity of an LDAP
server (a manually entered value takes precedence).

LDAP Basic Authentication can be configured via the Service/Installation
Tool by specifying a bind DN and password. If LDAP Basic Authentication
is not configured the LDAP client will bind anonymously.

The supported LDAP Security Profiles are:

-  Basic

-  Basic-Manual

-  Anonymous

-  Anonymous-Manual

The use of LDAP to publish and obtain device configuration information
is described in `Configuration <#sect_B.4.4>`__.

.. _sect_B.4.3.3:

IPv4 and IPv6 Support
^^^^^^^^^^^^^^^^^^^^^

This product only supports IPv4 connections.

.. _sect_B.4.4:

Configuration
~~~~~~~~~~~~~

.. _sect_B.4.4.1:

AE Title/Presentation Address Mapping
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. _sect_B.4.4.1.1:

Local AE Titles
'''''''''''''''

All local applications use the AE Titles and TCP/IP Ports configured via
the Service/Installation Tool. The Field Service Engineer can configure
the TCP Port via the Service/Installation Tool. No Default AE Titles are
provided. The AE Titles must be configured during installation. The
local AE Title used by each individual application can be configured
independently of the AE Title used by other local applications. If so
configured, all local AEs are capable of using the same AE Title.

.. table:: AE Title Configuration Table

   ================== ================ ===================
   Application Entity Default AE Title Default TCP/IP Port
   ================== ================ ===================
   Storage            No Default       104
   Workflow           No Default       Not Applicable
   Hardcopy           No Default       Not Applicable
   ================== ================ ===================

.. _sect_B.4.4.1.1.1:

Obtaining Local Configuration From LDAP Server
                                              

The Service/Installation Tool can be used to specify that an LDAP Server
be the master of local configuration information. The Query LDAP Server
transaction of the Network Configuration Profile is used to obtain
configuration information. The LDAP

Server will be queried for updated information at boot time but the
query can also be manually invoked from the Service/Installation Tool. A
search is performed for an LDAP entity within the DICOM configuration
sub-tree having an identical device name (as entered in the
Service/Installation Tool). The local configuration will be updated to
match the central configuration (i.e., AE Titles, TCP Port Numbers, Peer
AEs, Private Data, etc). The central configuration information will be
checked for consistency before the local configuration is updated.

The configuration parameters that can be updated by the central LDAP
server and can affect the local configuration for the device are listed
in the Table below:

.. table:: Device Configuration Parameters Obtained From LDAP Server

   +-------------------+------------------+-----------------------------+
   | LDAP object class | LDAP attribute   | Local Meaning               |
   +===================+==================+=============================+
   | dicomDevice       | dicomDescription | Displayed in the            |
   |                   |                  | Service/Installation Tool   |
   +-------------------+------------------+-----------------------------+
   | dicomDevice       | dicomVendorData  | Private device              |
   |                   |                  | configuration parameters    |
   |                   |                  | (e.g., examination protocol |
   |                   |                  | codes and parameters)       |
   +-------------------+------------------+-----------------------------+
   | dicomDevice       | dicomDeviceType  | Displayed in the            |
   |                   |                  | Service/Installation Tool   |
   +-------------------+------------------+-----------------------------+

The Application Entities described by the LDAP server are matched to the
supported local application entities (Storage, Workflow or Hardcopy) by
inspecting the private information within the dicomVendorData attribute
for each dicomNetworkAE.

The configuration parameters that can be updated by the central LDAP
server and affect the local configuration for each supported local AE
are listed in the Table below:

.. table:: AE Configuration Parameters Obtained From LDAP Server

   +-------------------+-----------------------+-----------------------+
   | LDAP object class | LDAP attribute        | Local Meaning         |
   +===================+=======================+=======================+
   | dicomNetworkAE    | dicomAETitle          | Local AE Title(s)     |
   +-------------------+-----------------------+-----------------------+
   | dicomNetworkAE    | dicomDescription      | Displayed in the      |
   |                   |                       | Service/Installation  |
   |                   |                       | Tool                  |
   +-------------------+-----------------------+-----------------------+
   | dicomNetworkAE    | dicomNetwo            | Associated network    |
   |                   | rkConnectionReference | connection parameters |
   +-------------------+-----------------------+-----------------------+
   | dicomNetworkAE    | dicomPeerAETitle      | Default collection of |
   |                   |                       | Peer AE               |
   +-------------------+-----------------------+-----------------------+
   | dicomNetworkAE    | dicomVendorData       | Private AE            |
   |                   |                       | configuration         |
   |                   |                       | parameters (e.g.,     |
   |                   |                       | timeouts, max PDU     |
   |                   |                       | lengths, maximum      |
   |                   |                       | number of             |
   |                   |                       | simultaneous          |
   |                   |                       | associations).        |
   +-------------------+-----------------------+-----------------------+
   | dicomNetworkAE    | di                    | Displayed in the      |
   |                   | comApplicationCluster | Service/Installation  |
   |                   |                       | Tool                  |
   +-------------------+-----------------------+-----------------------+

The configuration parameters that can be updated by the central LDAP
server and affect the local configuration for the network connection are
listed in the Table below:

.. table:: Network Connection Configuration Parameters Obtained From
LDAP Server

   ====================== ============== =============
   LDAP object class      LDAP attribute Local Meaning
   ====================== ============== =============
   dicomNetworkConnection dicomHostname  Hostname
   dicomNetworkConnection dicomPort      TCP Port
   ====================== ============== =============

.. _sect_B.4.4.1.1.2:

Publishing Local Configuration to LDAP Server
                                             

The Service/Installation Tool can be used to publish local configuration
information to the LDAP Server.

The LDAP client will bind to the server using LDAP Basic Authentication
(or anonymously if LDAP Basic Authentication is not configured). The
LDAP Client expects that the necessary DICOM Root objects exist in the
LDAP DIT and performed searches to identify the following information:

a. The DN of the dicomConfigurationRoot identifying the root if all
   DICOM Configuration information.

b. The DN of the dicomDevicesRoot under which new devices can be
   inserted

c. The DN of the dicomUniqueAETitlesRegistryRoot under which unique AE
   Titles can be registered

d. The DN of any existing dicomDevice object that represents the device
   hosting the LDAP client (dicomDeviceName identical to locally
   configured device name).

Modifications can be made to existing LDAP entries for the device or new
entries will be created if necessary. It is possible to manually assign
AE Titles for each local Application Entity or to automatically generate
random AE Titles. In both cases, the LDAP server is queried to determine
that the AE Titles are currently unused.

Two different methods (Manual and Automatic) are supported to update the
LDAP server and an appropriate method must be selected depending on the
security policies enforced by the LDAP server.

Manual Update

-  An LDIF file (RFC 2489) will be created containing all new or updated
   LDAP objects and attributes. The objects will be appropriately
   located in the server's LDAP tree. The LDIF file will be written to
   the local file system or to exchangeable media (e.g., floppy). The
   file can be transferred to the LDAP server and imported using server
   specific tools.

Automatic Update

-  The LDAP client will attempt to register unique AE Titles. If the
   manually chosen AE Titles are manually already in use the update will
   be aborted and new AE Titles must be chosen. If AE Titles were
   randomly selected the LDAP client will use the random AE Title
   allocation technique described by the "Update LDAP Server"
   transaction of the DICOM Application Configuration Management
   Profile.

-  The LDAP client will create new LDAP objects or update existing
   objects as necessary at appropriate locations in the server's LDAP
   tree.

-  If the server refuses any object creation or update operation the
   Automatic Update will be aborted. In case of failure, the LDAP server
   may contain partial configuration information that must be corrected
   by the LDAP server administrator.

The same set of LDAP objects and attributes will be entered into the
LDAP DIT for both the Manual and Automatic Update methods. Values for
all configurable attributes can be entered using Service/Installation
Tool. `table_title <#table_B.4.4-5>`__ lists the attributes and default
values created for the installed device.

.. table:: Device Configuration Parameters Updated On LDAP Server

   +----------------+----------------+----------------+---------------+
   | LDAP object    | LDAP attribute | Configurable   | Default Value |
   | class          |                | (Yes/No)       |               |
   +================+================+================+===============+
   | dicomDevice    | d              | Yes            |               |
   |                | icomDeviceName |                |               |
   +----------------+----------------+----------------+---------------+
   | di             | Yes            | Radi           |               |
   | comDescription |                | o-Fluoroscopic |               |
   |                |                | Image          |               |
   |                |                | Acquisition    |               |
   |                |                | Modality       |               |
   +----------------+----------------+----------------+---------------+
   | dic            | No             | EXAMPLE-IM     |               |
   | omManufacturer |                | AGING-PRODUCTS |               |
   +----------------+----------------+----------------+---------------+
   | dicomManufac   | No             | Example-Integ  |               |
   | turerModelName |                | rated-Modality |               |
   +----------------+----------------+----------------+---------------+
   | dicomVersion   | No             | 1              |               |
   +----------------+----------------+----------------+---------------+
   | dicomPri       | No             | RF             |               |
   | maryDeviceType |                |                |               |
   +----------------+----------------+----------------+---------------+
   | d              | Yes            |                |               |
   | icomVendorData |                |                |               |
   +----------------+----------------+----------------+---------------+

`table_title <#table_B.4.4-6>`__ lists the attributes and default values
used to describe the network configuration:

.. table:: Network Connection Configuration Parameters Updated On LDAP
Server

   +------------------------+----------------+-----------------------+---------------+
   | LDAP object class      | LDAP attribute | Configurable (Yes/No) | Default Value |
   +========================+================+=======================+===============+
   | dicomNetworkConnection | dicomHostname  | Yes                   |               |
   +------------------------+----------------+-----------------------+---------------+
   | dicomPort              | Yes            | 104                   |               |
   +------------------------+----------------+-----------------------+---------------+

The Table below lists the attributes and default values used to describe
the Storage AE:

.. table:: Storage AE Configuration Parameters Updated On LDAP Server

   +----------------+----------------+----------------+----------------+
   | LDAP object    | LDAP attribute | Configurable   | Default Value  |
   | class          |                | (Yes/No)       |                |
   +================+================+================+================+
   | dicomNetworkAE | dicomAETitle   | Yes            |                |
   +----------------+----------------+----------------+----------------+
   | di             | Yes            | Storage        |                |
   | comDescription |                | Application    |                |
   +----------------+----------------+----------------+----------------+
   | di             | Yes            |                |                |
   | comPeerAETitle |                |                |                |
   +----------------+----------------+----------------+----------------+
   | d              | Yes            |                |                |
   | icomVendorData |                |                |                |
   +----------------+----------------+----------------+----------------+
   | dicomAppl      | Yes            |                |                |
   | icationCluster |                |                |                |
   +----------------+----------------+----------------+----------------+
   | dicomAssoci    | No             | TRUE           |                |
   | ationInitiator |                |                |                |
   +----------------+----------------+----------------+----------------+
   | dicomAssoc     | No             | TRUE           |                |
   | iationAcceptor |                |                |                |
   +----------------+----------------+----------------+----------------+
   | dicomTran      | dicomSOPClass  | No             | X-Ray          |
   | sferCapability |                |                | Rad            |
   |                |                |                | iofluoroscopic |
   |                |                |                | Image Storage  |
   |                |                |                |                |
   |                |                |                | Grayscale      |
   |                |                |                | Softcopy       |
   |                |                |                | Presentation   |
   |                |                |                | State Storage  |
   |                |                |                |                |
   |                |                |                | Storage        |
   |                |                |                | Commitment     |
   |                |                |                | Push Model     |
   +----------------+----------------+----------------+----------------+
   | dic            | No             | SCU            |                |
   | omTransferRole |                |                |                |
   +----------------+----------------+----------------+----------------+
   | dicom          | Yes            | Explicit VR    |                |
   | TransferSyntax |                | Little Endian  |                |
   |                |                |                |                |
   |                |                | Implicit VR    |                |
   |                |                | Little Endian  |                |
   +----------------+----------------+----------------+----------------+

The Table below lists the attributes and default values used to describe
the Workflow AE:

.. table:: Workflow AE Configuration Parameters Updated On LDAP Server

   +----------------+----------------+----------------+----------------+
   | LDAP object    | LDAP attribute | Configurable   | Default Value  |
   | class          |                | (Yes/No)       |                |
   +================+================+================+================+
   | dicomNetworkAE | dicomAETitle   | Yes            |                |
   +----------------+----------------+----------------+----------------+
   | di             | Yes            | Workflow       |                |
   | comDescription |                | Application    |                |
   +----------------+----------------+----------------+----------------+
   | di             | Yes            |                |                |
   | comPeerAETitle |                |                |                |
   +----------------+----------------+----------------+----------------+
   | d              | Yes            |                |                |
   | icomVendorData |                |                |                |
   +----------------+----------------+----------------+----------------+
   | dicomAppl      | Yes            |                |                |
   | icationCluster |                |                |                |
   +----------------+----------------+----------------+----------------+
   | dicomAssoci    | No             | TRUE           |                |
   | ationInitiator |                |                |                |
   +----------------+----------------+----------------+----------------+
   | dicomAssoc     | No             | FALSE          |                |
   | iationAcceptor |                |                |                |
   +----------------+----------------+----------------+----------------+
   | dicomTran      | dicomSOPClass  | No             | Modality       |
   | sferCapability |                |                | Worklist       |
   |                |                |                | Information    |
   |                |                |                | Model - FIND   |
   |                |                |                |                |
   |                |                |                | Modality       |
   |                |                |                | Performed      |
   |                |                |                | Procedure Step |
   +----------------+----------------+----------------+----------------+
   | dic            | No             | SCU            |                |
   | omTransferRole |                |                |                |
   +----------------+----------------+----------------+----------------+
   | dicom          | Yes            | Explicit VR    |                |
   | TransferSyntax |                | Little Endian  |                |
   |                |                |                |                |
   |                |                | Implicit VR    |                |
   |                |                | Little Endian  |                |
   +----------------+----------------+----------------+----------------+

The Table below lists the attributes and default values used to describe
the Hardcopy AE:

.. table:: Hardcopy AE Configuration Parameters Updated On LDAP Server

   +----------------+----------------+----------------+----------------+
   | LDAP object    | LDAP attribute | Configurable   | Default Value  |
   | class          |                | (Yes/No)       |                |
   +================+================+================+================+
   | dicomNetworkAE | dicomAETitle   | Yes            |                |
   +----------------+----------------+----------------+----------------+
   | di             | Yes            | Hardcopy       |                |
   | comDescription |                | Application    |                |
   +----------------+----------------+----------------+----------------+
   | dic            | n/a            |                |                |
   | omNetworkConne |                |                |                |
   | ctionReference |                |                |                |
   +----------------+----------------+----------------+----------------+
   | di             | Yes            |                |                |
   | comPeerAETitle |                |                |                |
   +----------------+----------------+----------------+----------------+
   | d              | Yes            |                |                |
   | icomVendorData |                |                |                |
   +----------------+----------------+----------------+----------------+
   | dicomAppl      | Yes            |                |                |
   | icationCluster |                |                |                |
   +----------------+----------------+----------------+----------------+
   | dicomAssoci    | No             | TRUE           |                |
   | ationInitiator |                |                |                |
   +----------------+----------------+----------------+----------------+
   | dicomAssoc     | No             | FALSE          |                |
   | iationAcceptor |                |                |                |
   +----------------+----------------+----------------+----------------+
   | dicomTran      | dicomSOPClass  | No             | Basic          |
   | sferCapability |                |                | Grayscale      |
   |                |                |                | Print          |
   |                |                |                | Management     |
   |                |                |                | Meta           |
   |                |                |                |                |
   |                |                |                | Presentation   |
   |                |                |                | LUT            |
   +----------------+----------------+----------------+----------------+
   | dic            | No             | SCU            |                |
   | omTransferRole |                |                |                |
   +----------------+----------------+----------------+----------------+
   | dicom          | Yes            | Explicit VR    |                |
   | TransferSyntax |                | Little Endian  |                |
   |                |                |                |                |
   |                |                | Implicit VR    |                |
   |                |                | Little Endian  |                |
   +----------------+----------------+----------------+----------------+

.. _sect_B.4.4.1.2:

Remote AE Title/Presentation Address Mapping
''''''''''''''''''''''''''''''''''''''''''''

The AE Title, host names and port numbers of remote applications are
configured using the EXAMPLE-INTEGRATED-MODALITY Service/Installation
Tool.

.. _sect_B.4.4.1.2.1:

Storage
       

The EXAMPLE-INTEGRATED-MODALITY Service/Installation Tool must be used
to set the AE Titles, port-numbers, host-names and capabilities for the
remote Storage SCPs. Associations will only be accepted from known AE
Titles and associations from unknown AE Titles will be rejected (an AE
Title is known if it can be selected within the Service/Installation
Tool). Multiple remote Storage SCPs can be defined. Any Storage SCP can
be configured to be an "Archive" device causing storage commitment to be
requested for images or presentation states transmitted to the device.

If an LDAP server is available, the Service/Installation Tool will
search for suitable remote Storage SCPs and present these for selection.
If the LDAP object for the Storage AE contains one or more
dicomPeerAETitle attributes then only these Peer AEs will be available
for selection. Otherwise, remote AEs will only be available for
selection if they support compatible SOP Classes as an SCP. If a remote
AE is attached to a device containing a dicomDeviceType attribute with
value "ARCHIVE" it will be automatically configured as an "Archive"
device provided the AE also supports Storage Commitment as an SCP.

These LDAP-assisted selection policies can be overridden and a search
performed for a specific device or AE Title.

.. _sect_B.4.4.1.2.2:

Workflow
        

The EXAMPLE-INTEGRATED-MODALITY Service/Installation Tool must be used
to set the AE Title, port-number, host-name and capabilities of the
remote Modality Worklist SCP. Only a single remote Modality Worklist SCP
can be defined.

If an LDAP server is available, the Service/Installation Tool will
search for suitable remote Modality Worklist SCPs and present these for
selection. Remote AEs will only be available for selection if they
support the Modality Worklist SOP Class as an SCP. If a remote AE is
attached to a device containing a dicomDeviceType attribute with value
"DSS" (Department System Scheduler) it will be presented as the
preferred selection.

The EXAMPLE-INTEGRATED-MODALITY Service/Installation Tool must be used
to set the AE Title, port-number, host-name and capabilities of the
remote MPPS SCP. Only a single remote MPPS SCP can be defined.

If an LDAP server is available, the Service/Installation Tool will
search for suitable remote MPPS SCPs and present these for selection.
Remote AEs will only be available for selection if they support the MPPS
SOP Class as an SCP. If a remote AE is attached to a device containing a
dicomDeviceType attribute with value "DSS" (Department System Scheduler)
it will be presented as the preferred selection.

.. _sect_B.4.4.1.2.3:

Hardcopy
        

The EXAMPLE-INTEGRATED-MODALITY Service/Installation Tool must be used
to set the AEs' AE Titles, port-numbers, host-names, IP­addresses and
capabilities for the remote Print SCPs.

Multiple remote Print SCPs can be defined.

If an LDAP server is available, the Service/Installation Tool will
search for suitable remote Print SCPs and present these for selection.
Remote AEs will only be available for selection if they support the
Basic Grayscale Print Management Meta SOP Class as an SCP. If a remote
AE is attached to a device containing a dicomDeviceType attribute with
value "PRINT" (Hard Copy Print Server) it will be presented as the
preferred selection.

.. _sect_B.4.4.2:

Parameters
^^^^^^^^^^

A large number of parameters related to acquisition and general
operation can be configured using the Service/Installation Tool. The
Table below only shows those configuration parameters relevant to DICOM
communication. See the EXAMPLE­INTEGRATED-MODALITY Service Manual for
details on general configuration capabilities.

.. table:: Configuration Parameters Table

   +----------------------+----------------------+----------------------+
   | Parameter            | Configurable         | Default Value        |
   |                      | (Yes/No)             |                      |
   +======================+======================+======================+
   | **General            |                      |                      |
   | Parameters**         |                      |                      |
   +----------------------+----------------------+----------------------+
   | Max PDU Receive Size | Yes                  | 65536 Bytes(64 kB)   |
   +----------------------+----------------------+----------------------+
   | Max PDU Send         | No                   | 65536 Bytes(64 kB)   |
   | Size(larger PDUs     |                      |                      |
   | will never be sent,  |                      |                      |
   | even if the receiver |                      |                      |
   | supports a larger    |                      |                      |
   | Max PDU Receive      |                      |                      |
   | Size. If the         |                      |                      |
   | receiver supports a  |                      |                      |
   | smaller Max PDU      |                      |                      |
   | Receive Size then    |                      |                      |
   | the Max PDU Send     |                      |                      |
   | Size will be reduced |                      |                      |
   | accordingly for the  |                      |                      |
   | duration of the      |                      |                      |
   | Association. Max PDU |                      |                      |
   | Receive Size         |                      |                      |
   | information is       |                      |                      |
   | exchanged during     |                      |                      |
   | DICOM Association    |                      |                      |
   | Negotiation in the   |                      |                      |
   | Maximum Length       |                      |                      |
   | Sub-Item of the      |                      |                      |
   | A-ASSOCIATION-RQ and |                      |                      |
   | A-ASSOCIATE-AC)      |                      |                      |
   +----------------------+----------------------+----------------------+
   | Time-out waiting for | Yes                  | 15 s                 |
   | a acceptance or      |                      |                      |
   | rejection response   |                      |                      |
   | to an Association    |                      |                      |
   | Request (Application |                      |                      |
   | Level Timeout)       |                      |                      |
   +----------------------+----------------------+----------------------+
   | Time-out waiting for | Yes                  | 30 s                 |
   | a response to an     |                      |                      |
   | Association release  |                      |                      |
   | request (Application |                      |                      |
   | Level Timeout)       |                      |                      |
   +----------------------+----------------------+----------------------+
   | Time-out waiting for | Yes                  | 15 s                 |
   | completion of a      |                      |                      |
   | TCP/IP connect       |                      |                      |
   | request (Low-level   |                      |                      |
   | timeout)             |                      |                      |
   +----------------------+----------------------+----------------------+
   | Time-out awaiting a  | Yes                  | 360 s                |
   | Response to a DIMSE  |                      |                      |
   | Request (Low-Level   |                      |                      |
   | Timeout)             |                      |                      |
   +----------------------+----------------------+----------------------+
   | Time-out for waiting | Yes                  | 30 s                 |
   | for data between     |                      |                      |
   | TCP/IP-packets (Low  |                      |                      |
   | Level Timeout)       |                      |                      |
   +----------------------+----------------------+----------------------+
   | **Storage            |                      |                      |
   | Parameters**         |                      |                      |
   +----------------------+----------------------+----------------------+
   | Storage SCU time-out | Yes                  | 120 s                |
   | waiting for a        |                      |                      |
   | response to a        |                      |                      |
   | C-STORE-RQ           |                      |                      |
   +----------------------+----------------------+----------------------+
   | Number of times a    | Yes                  | 0 (Failed send jobs  |
   | failed send job may  |                      | are not retried)     |
   | be retried           |                      |                      |
   +----------------------+----------------------+----------------------+
   | Delay between        | Yes                  | 60 s                 |
   | retrying failed send |                      |                      |
   | jobs                 |                      |                      |
   +----------------------+----------------------+----------------------+
   | Maximum number of    | Yes                  | 1                    |
   | simultaneously       |                      |                      |
   | initiated            |                      |                      |
   | Associations by the  |                      |                      |
   | Storage AE           |                      |                      |
   +----------------------+----------------------+----------------------+
   | Supported Transfer   | Yes                  | Implicit VR Little   |
   | Syntaxes (separately |                      | Endian               |
   | configurable for     |                      |                      |
   | each remote AE)      |                      | Explicit VR Little   |
   |                      |                      | Endian               |
   +----------------------+----------------------+----------------------+
   | **Storage Commitment |                      |                      |
   | Parameters**         |                      |                      |
   +----------------------+----------------------+----------------------+
   | Timeout waiting for  | Yes                  | 24 hours             |
   | a Storage Commitment |                      |                      |
   | Notification         |                      |                      |
   | (maximum duration of |                      |                      |
   | applicability for a  |                      |                      |
   | Storage Commitment   |                      |                      |
   | Transaction UID).    |                      |                      |
   +----------------------+----------------------+----------------------+
   | Maximum number of    | Yes                  | 5                    |
   | simultaneously       |                      |                      |
   | accepted             |                      |                      |
   | Associations by the  |                      |                      |
   | Storage AE           |                      |                      |
   +----------------------+----------------------+----------------------+
   | Delay association    | Yes                  | 120 s                |
   | release after        |                      |                      |
   | sending a Storage    |                      |                      |
   | Commitment Request   |                      |                      |
   | (wait for a Storage  |                      |                      |
   | Commitment           |                      |                      |
   | Notification over    |                      |                      |
   | the same             |                      |                      |
   | association).        |                      |                      |
   +----------------------+----------------------+----------------------+
   | **Modality Worklist  |                      |                      |
   | Parameters**         |                      |                      |
   +----------------------+----------------------+----------------------+
   | Modality Worklist    | Yes                  | 600 s                |
   | SCU time-out waiting |                      |                      |
   | for the final        |                      |                      |
   | response to a        |                      |                      |
   | C-FIND-RQ            |                      |                      |
   +----------------------+----------------------+----------------------+
   | Maximum number of    | Yes                  | 100                  |
   | Worklist Items       |                      |                      |
   +----------------------+----------------------+----------------------+
   | Supported Transfer   | Yes                  | Implicit VR Little   |
   | Syntaxes for         |                      | Endian               |
   | Modality Worklist    |                      |                      |
   |                      |                      | Explicit VR Little   |
   |                      |                      | Endian               |
   +----------------------+----------------------+----------------------+
   | Delay between        | Yes                  | 10 mins              |
   | automatic Worklist   |                      |                      |
   | Updates              |                      |                      |
   +----------------------+----------------------+----------------------+
   | Query Worklist for   | Yes                  | EXINTMOD_WFL         |
   | specific Scheduled   |                      |                      |
   | Station AE Title     |                      |                      |
   +----------------------+----------------------+----------------------+
   | Query Worklist for   | Yes                  | RF                   |
   | specific Modality    |                      |                      |
   | Value                |                      |                      |
   +----------------------+----------------------+----------------------+
   | **MPPS Parameters**  |                      |                      |
   +----------------------+----------------------+----------------------+
   | MPPS SCU time-out    | Yes                  | 60 s                 |
   | waiting for a        |                      |                      |
   | response to a        |                      |                      |
   | N-CREATE-RQ          |                      |                      |
   +----------------------+----------------------+----------------------+
   | MPPS SCU time-out    | Yes                  | 30 s                 |
   | waiting for a        |                      |                      |
   | response to a        |                      |                      |
   | N-SET-RQ             |                      |                      |
   +----------------------+----------------------+----------------------+
   | Supported Transfer   | Yes                  | Implicit VR Little   |
   | Syntaxes for MPPS    |                      | Endian               |
   |                      |                      |                      |
   |                      |                      | Explicit VR Little   |
   |                      |                      | Endian               |
   +----------------------+----------------------+----------------------+
   | **Print Parameters** |                      |                      |
   +----------------------+----------------------+----------------------+
   | Print SCU time-out   | Yes                  | 60 s                 |
   | waiting for a        |                      |                      |
   | response to a        |                      |                      |
   | N-CREATE-RQ          |                      |                      |
   +----------------------+----------------------+----------------------+
   | Print SCU time-out   | Yes                  | 30 s                 |
   | waiting for a        |                      |                      |
   | response to a        |                      |                      |
   | N-SET-RQ             |                      |                      |
   +----------------------+----------------------+----------------------+
   | Print SCU time-out   | Yes                  | 360s                 |
   | waiting for a        |                      |                      |
   | response to a        |                      |                      |
   | N-ACTION-RQ          |                      |                      |
   +----------------------+----------------------+----------------------+
   | Supported Transfer   | Yes                  | Implicit VR Little   |
   | Syntaxes (separately |                      | Endian               |
   | configurable for     |                      |                      |
   | each remote printer) |                      | Explicit VR Little   |
   |                      |                      | Endian               |
   +----------------------+----------------------+----------------------+
   | Number of times a    | Yes                  | 0 (Failed send jobs  |
   | failed print-job may |                      | are not retried)     |
   | be retried           |                      |                      |
   +----------------------+----------------------+----------------------+
   | Delay between        | Yes                  | 60 s                 |
   | retrying failed      |                      |                      |
   | print-jobs           |                      |                      |
   +----------------------+----------------------+----------------------+
   | Printer correction   | Yes                  | Identity LUT         |
   | LUT (separately      |                      |                      |
   | configurable for     |                      |                      |
   | each remote printer) |                      |                      |
   +----------------------+----------------------+----------------------+

.. _sect_B.5:

Media Interchange
-----------------

.. _sect_B.5.1:

Implementation Model
~~~~~~~~~~~~~~~~~~~~

.. _sect_B.5.1.1:

Application Data Flow
^^^^^^^^^^^^^^^^^^^^^

The Offline-Media Application Entity exports images and Presentation
States to a CD-R Storage medium. It is associated with the local
real-world activity "Export to CD-R". "Export to CD-R" is performed upon
user request for selected patients, studies, series or instances (images
or presentation states).

.. _sect_B.5.1.2:

Functional Definition of AEs
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. _sect_B.5.1.2.1:

Functional Definition of Offline-Media Application Entity
'''''''''''''''''''''''''''''''''''''''''''''''''''''''''

Activation of the "Export to CD-R" icon or menu entry will pass the
currently selected patients, studies, series or instances (images or
presentation states) to the Offline-Media Application Entity. The SOP
Instances associated with the selection will be collected into one or
more export jobs. The contents of each export job will be written to a
single CD-R media.

.. _sect_B.5.1.3:

Sequencing of Real-World Activities
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

At least one image or presentation state must exist and be selected
before the Offline-Media Application Entity can be invoked. The operator
can insert a new CD-R media at any time before or after invocation of
the Offline-Media Application Entity. The Offline-Media Application
Entity will wait indefinitely for a media to be inserted before starting
to write to the CD-R device. If no CD-R media is available the export
job can be canceled from the job queue.

.. _sect_B.5.1.4:

File Meta Information Options
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The implementation information written to the File Meta Header in each
file is:

.. table:: DICOM Implementation Class and Version for Media Storage

   =========================== ============================
   Implementation Class UID    1.xxxxxxx.yyy.etc.ad.inf.usw
   Implementation Version Name EXINTMOD_01
   =========================== ============================

.. _sect_B.5.2:

AE Specifications
~~~~~~~~~~~~~~~~~

.. _sect_B.5.2.1:

Offline-Media Application Entity Specification
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Offline-Media Application Entity provides standard conformance to
the Media Storage Service Class. The Application Profiles and roles are
listed below:

.. table:: Application Profiles, Activities and Roles for Offline-Media

   ============================== =================== ====
   Application Profiles Supported Real World Activity Role
   ============================== =================== ====
   STD-GEN-CD                     Export to CD-R      FSC
   ============================== =================== ====

.. _sect_B.5.2.1.1:

File Meta Information for the Application Entity
''''''''''''''''''''''''''''''''''''''''''''''''

The Source Application Entity Title included in the File Meta Header is
configurable (see `Media Configuration <#sect_B.5.4>`__).

.. _sect_B.5.2.1.2:

Real-World Activities
'''''''''''''''''''''

.. _sect_B.5.2.1.2.1:

Activity - Export to CD-R
                         

The Offline-Media Application Entity acts as an FSC when requested to
export SOP Instances from the local database to a CD-R medium.

A dialogue will be presented allowing the user to modify the suggested
media label and provides control over the available media capacity. If
the contents of the current selection do not fit on a single media an
automatic separation into multiple export jobs will be suggested that
can be adapted by the user.

The user will be prompted to insert an empty CD-R for each export job.
The contents of the export job will be written together with a
corresponding DICOMDIR to a single-session CD­R. Writing in
multi-session mode is not supported. The user can cancel an export job
in the job queue.

.. _sect_B.5.2.1.2.1.1:

Media Storage Application Profiles
                                  

The Offline-Media Application Entity support the STD-GEN-CD Application
Profile.

.. _sect_B.5.2.1.2.1.1.1:

Options
       

The Offline-Media Application Entity supports the SOP Classes and
Transfer Syntaxes listed in the Table below:

.. table:: IODs, SOP Classes and Transfer Syntaxes for Offline­Media

   +----------------+----------------+----------------+----------------+
   | Information    | SOP Class UID  | Transfer       | Transfer       |
   | Object         |                | Syntax         | Syntax UID     |
   | Definition     |                |                |                |
   +================+================+================+================+
   | Media Storage  | 1.2.84         | Explicit VR    | 1.2.8          |
   | Directory      | 0.10008.1.3.10 | Little Endian  | 40.10008.1.2.1 |
   | Storage        |                |                |                |
   +----------------+----------------+----------------+----------------+
   | X-Ray Radio    | 1.2.840.10008. | Explicit VR    | 1.2.8          |
   | Fluoroscopic   | 5.1.4.1.1.12.2 | Little Endian  | 40.10008.1.2.1 |
   | Image Storage  |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Grayscale      | 1.2.840.10008. | Explicit VR    | 1.2.8          |
   | Softcopy       | 5.1.4.1.1.11.1 | Little Endian  | 40.10008.1.2.1 |
   | Presentation   |                |                |                |
   | State Storage  |                |                |                |
   +----------------+----------------+----------------+----------------+

.. _sect_B.5.3:

Augmented and Private Application Profiles
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

EXAMPLE-INTEGRATED-MODALITY does not support any augmented for private
application profiles.

.. _sect_B.5.4:

Media Configuration
~~~~~~~~~~~~~~~~~~~

All local applications use the AE Titles configured via the
Service/Installation Tool. The Application Entity Titles configurable
for Media Services are listed in the Table below:

.. table:: AE Title Configuration Table

   ================== ================
   Application Entity Default AE Title
   ================== ================
   Offline-Media      EXINTMOD_MEDIA
   ================== ================

.. _sect_B.6:

Support of Character Sets
-------------------------

All EXAMPLE-INTEGRATED-MODALITY DICOM applications support the

ISO_IR 100 (ISO 8859-1:1987 Latin Alphabet No. 1 supplementary set)

ISO_IR 144 (ISO 8859-5:1988 Latin/Cyrillic Alphabet supplementary set)

If the EXAMPLE-INTEGRATED-MODALITY is configured for Cyrillic character
set support, ISO_IR 144 will be used automatically.

.. _sect_B.7:

Security
--------

EXAMPLE-INTEGRATED-MODALITY does not support any specific security
measures.

It is assumed that EXAMPLE-INTEGRATED-MODALITY is used within a secured
environment. It is assumed that a secured environment includes at a
minimum:

a. Firewall or router protections to ensure that only approved external
   hosts have network access to EXAMPLE­INTEGRATED-MODALITY.

b. Firewall or router protections to ensure that
   EXAMPLE­INTEGRATED-MODALITY only has network access to approved
   external hosts and services.

c. Any communication with external hosts and services outside the
   locally secured environment use appropriate secure network channels
   (e.g., such as a Virtual Private Network (VPN) )

Other network security procedures such as automated intrusion detection
may be appropriate in some environments. Additional security features
may be established by the local security policy and are beyond the scope
of this conformance statement.

.. _sect_B.8:

Annexes
-------

.. _sect_B.8.1:

IOD Contents
~~~~~~~~~~~~

.. _sect_B.8.1.1:

Created SOP Instances
^^^^^^^^^^^^^^^^^^^^^

Examples of X-Ray Radiofluoroscopic images and Grayscale Softcopy
Presentation States created by EXAMPLE-INTEGRATED-MODALITY can be
downloaded from:

http://www.example-imaging-products.nocom/example-integrated-modality/example-images

`table_title <#table_B.8.1-1>`__ specifies the attributes of an X-Ray
Radiofluoroscopic Image transmitted by the EXAMPLE-INTEGRATED-MODALITY
storage application.

`table_title <#table_B.8.1-2>`__ specifies the attributes of a Grayscale
Softcopy Presentation State transmitted by the
EXAMPLE­INTEGRATED-MODALITY storage application.

The following tables use a number of abbreviations. The abbreviations
used in the "Presence of …" column are:

VNAP
   Value Not Always Present (attribute sent zero length if no value is
   present)

ANAP
   Attribute Not Always Present

ALWAYS
   Always Present

EMPTY
   Attribute is sent without a value

The abbreviations used in the "Source" column:

MWL
   the attribute value source Modality Worklist

USER
   the attribute value source is from User input

AUTO
   the attribute value is generated automatically

MPPS
   the attribute value is the same as that use for Modality Performed
   Procedure Step

CONFIG
   the attribute value source is a configurable parameter

.. note::

   All dates and times are encoded in the local configured calendar and
   time. Date, Time and Time zone are configured using the
   Service/Installation Tool.

.. _sect_B.8.1.1.1:

X-Ray Radiofluoroscopic Image IOD
'''''''''''''''''''''''''''''''''

.. table:: IOD of Created Rf SOP Instances

   +----------------+----------------+----------------+----------------+
   | IE             | Module         | Reference      | Presence of    |
   |                |                |                | Module         |
   +================+================+================+================+
   | Patient        | Patient        | `tab           | ALWAYS         |
   |                |                | le_title <#tab |                |
   |                |                | le_B.8.1-3>`__ |                |
   +----------------+----------------+----------------+----------------+
   | Study          | General Study  | `tab           | ALWAYS         |
   |                |                | le_title <#tab |                |
   |                |                | le_B.8.1-4>`__ |                |
   +----------------+----------------+----------------+----------------+
   | Patient Study  | `tab           | ALWAYS         |                |
   |                | le_title <#tab |                |                |
   |                | le_B.8.1-5>`__ |                |                |
   +----------------+----------------+----------------+----------------+
   | Series         | General Series | `tab           | ALWAYS         |
   |                |                | le_title <#tab |                |
   |                |                | le_B.8.1-6>`__ |                |
   +----------------+----------------+----------------+----------------+
   | Equipment      | General        | `tab           | ALWAYS         |
   |                | Equipment      | le_title <#tab |                |
   |                |                | le_B.8.1-7>`__ |                |
   +----------------+----------------+----------------+----------------+
   | Image          | General Image  | `tab           | ALWAYS         |
   |                |                | le_title <#tab |                |
   |                |                | le_B.8.1-8>`__ |                |
   +----------------+----------------+----------------+----------------+
   | Image Pixel    | `tabl          | ALWAYS         |                |
   |                | e_title <#tabl |                |                |
   |                | e_B.8.1-10>`__ |                |                |
   +----------------+----------------+----------------+----------------+
   | Cine           | `tabl          | Only if        |                |
   |                | e_title <#tabl | Multi-frame    |                |
   |                | e_B.8.1-11>`__ |                |                |
   +----------------+----------------+----------------+----------------+
   | Multi-Frame    | `tabl          | Only if        |                |
   |                | e_title <#tabl | Multi-frame    |                |
   |                | e_B.8.1-12>`__ |                |                |
   +----------------+----------------+----------------+----------------+
   | Frame Pointers | `tabl          | Only if        |                |
   |                | e_title <#tabl | Multi-frame    |                |
   |                | e_B.8.1-13>`__ |                |                |
   +----------------+----------------+----------------+----------------+
   | Mask           | `tabl          | ALWAYS         |                |
   |                | e_title <#tabl |                |                |
   |                | e_B.8.1-14>`__ |                |                |
   +----------------+----------------+----------------+----------------+
   | X-Ray Image    | `tabl          | ALWAYS         |                |
   |                | e_title <#tabl |                |                |
   |                | e_B.8.1-15>`__ |                |                |
   +----------------+----------------+----------------+----------------+
   | X-Ray          | `tabl          | ALWAYS         |                |
   | Acquisition    | e_title <#tabl |                |                |
   |                | e_B.8.1-16>`__ |                |                |
   +----------------+----------------+----------------+----------------+
   | Modality LUT   | `tabl          | Only if Pixel  |                |
   |                | e_title <#tabl | Intensity      |                |
   |                | e_B.8.1-17>`__ | Relationship   |                |
   |                |                | (0028,1040) is |                |
   |                |                | LOG            |                |
   +----------------+----------------+----------------+----------------+
   | VOI LUT        | `tabl          | ALWAYS         |                |
   |                | e_title <#tabl |                |                |
   |                | e_B.8.1-18>`__ |                |                |
   +----------------+----------------+----------------+----------------+
   | SOP Common     | `tabl          | ALWAYS         |                |
   |                | e_title <#tabl |                |                |
   |                | e_B.8.1-19>`__ |                |                |
   +----------------+----------------+----------------+----------------+
   | Private        | `tab           | ALWAYS         |                |
   | Application    | le_title <#tab |                |                |
   |                | le_B.8.1-8>`__ |                |                |
   +----------------+----------------+----------------+----------------+

.. _sect_B.8.1.1.2:

Grayscale Softcopy Presentation State IOD
'''''''''''''''''''''''''''''''''''''''''

.. table:: IOD of Created Grayscale Softcopy Presentation State SOP
Instances

   +----------------+----------------+----------------+----------------+
   | IE             | Module         | Reference      | Presence of    |
   |                |                |                | Module         |
   +================+================+================+================+
   | Patient        | Patient        | `tab           | ALWAYS         |
   |                |                | le_title <#tab |                |
   |                |                | le_B.8.1-3>`__ |                |
   +----------------+----------------+----------------+----------------+
   | Study          | General Study  | `tab           | ALWAYS         |
   |                |                | le_title <#tab |                |
   |                |                | le_B.8.1-4>`__ |                |
   +----------------+----------------+----------------+----------------+
   | Patient Study  | `tab           | ALWAYS         |                |
   |                | le_title <#tab |                |                |
   |                | le_B.8.1-5>`__ |                |                |
   +----------------+----------------+----------------+----------------+
   | Series         | General Series | `tab           | ALWAYS         |
   |                |                | le_title <#tab |                |
   |                |                | le_B.8.1-6>`__ |                |
   +----------------+----------------+----------------+----------------+
   |                | Presentation   | `tabl          | ALWAYS         |
   |                | Series         | e_title <#tabl |                |
   |                |                | e_B.8.1-20>`__ |                |
   +----------------+----------------+----------------+----------------+
   | Equipment      | General        | `tab           | ALWAYS         |
   |                | Equipment      | le_title <#tab |                |
   |                |                | le_B.8.1-7>`__ |                |
   +----------------+----------------+----------------+----------------+
   | Presentation   | Presentation   | `tabl          | ALWAYS         |
   | State          | State          | e_title <#tabl |                |
   |                |                | e_B.8.1-21>`__ |                |
   +----------------+----------------+----------------+----------------+
   | Display        | `tabl          | Only if        |                |
   | Shutter        | e_title <#tabl | Shutter        |                |
   |                | e_B.8.1-22>`__ | applied        |                |
   +----------------+----------------+----------------+----------------+
   | Displayed Area | `tabl          | ALWAYS         |                |
   |                | e_title <#tabl |                |                |
   |                | e_B.8.1-23>`__ |                |                |
   +----------------+----------------+----------------+----------------+
   | Graphic        | `tabl          | Only if        |                |
   | Annotation     | e_title <#tabl | Graphic        |                |
   |                | e_B.8.1-24>`__ | Annotations    |                |
   |                |                | are present    |                |
   +----------------+----------------+----------------+----------------+
   | Spatial        | `tabl          | Only if        |                |
   | Transformation | e_title <#tabl | Spacial        |                |
   |                | e_B.8.1-25>`__ | Transformation |                |
   |                |                | applied        |                |
   +----------------+----------------+----------------+----------------+
   | Graphic Layer  | `tabl          | Only if        |                |
   |                | e_title <#tabl | Graphic        |                |
   |                | e_B.8.1-26>`__ | Annotations    |                |
   |                |                | are present    |                |
   +----------------+----------------+----------------+----------------+
   | Modality LUT   | `tabl          | ALWAYS         |                |
   |                | e_title <#tabl |                |                |
   |                | e_B.8.1-27>`__ |                |                |
   +----------------+----------------+----------------+----------------+
   | Softcopy VOI   | `tabl          | ALWAYS         |                |
   | LUT            | e_title <#tabl |                |                |
   |                | e_B.8.1-28>`__ |                |                |
   +----------------+----------------+----------------+----------------+
   | Softcopy       | `tabl          | ALWAYS         |                |
   | Presentation   | e_title <#tabl |                |                |
   | LUT            | e_B.8.1-29>`__ |                |                |
   +----------------+----------------+----------------+----------------+
   | SOP Common     | `tabl          | ALWAYS         |                |
   |                | e_title <#tabl |                |                |
   |                | e_B.8.1-19>`__ |                |                |
   +----------------+----------------+----------------+----------------+
   | Private        | `tab           | ALWAYS         |                |
   | Application    | le_title <#tab |                |                |
   |                | le_B.8.1-8>`__ |                |                |
   +----------------+----------------+----------------+----------------+

.. _sect_B.8.1.1.3:

Common Modules
''''''''''''''

.. table:: Patient Module of Created SOP Instances

   +-----------+-----------+----+-----------+-----------+----------+
   | Attribute | Tag       | VR | Value     | Presence  | Source   |
   | Name      |           |    |           | of Value  |          |
   +===========+===========+====+===========+===========+==========+
   | Patient's | (0        | PN | From      | VNAP      | MWL/USER |
   | Name      | 010,0010) |    | Modality  |           |          |
   |           |           |    | Worklist  |           |          |
   |           |           |    | or user   |           |          |
   |           |           |    | input.    |           |          |
   |           |           |    | Values    |           |          |
   |           |           |    | supplied  |           |          |
   |           |           |    | via       |           |          |
   |           |           |    | Modality  |           |          |
   |           |           |    | Worklist  |           |          |
   |           |           |    | will be   |           |          |
   |           |           |    | entered   |           |          |
   |           |           |    | as        |           |          |
   |           |           |    | received. |           |          |
   |           |           |    | Values    |           |          |
   |           |           |    | supplied  |           |          |
   |           |           |    | via user  |           |          |
   |           |           |    | input     |           |          |
   |           |           |    | will      |           |          |
   |           |           |    | contain   |           |          |
   |           |           |    | all 5     |           |          |
   |           |           |    | c         |           |          |
   |           |           |    | omponents |           |          |
   |           |           |    | (some     |           |          |
   |           |           |    | possibly  |           |          |
   |           |           |    | empty). . |           |          |
   |           |           |    | Maximum   |           |          |
   |           |           |    | 64        |           |          |
   |           |           |    | ch        |           |          |
   |           |           |    | aracters. |           |          |
   +-----------+-----------+----+-----------+-----------+----------+
   | Patient   | (0        | LO | From      | VNAP      | MWL/USER |
   | ID        | 010,0020) |    | Modality  |           |          |
   |           |           |    | Worklist  |           |          |
   |           |           |    | or user   |           |          |
   |           |           |    | input.    |           |          |
   |           |           |    | Maximum   |           |          |
   |           |           |    | 64        |           |          |
   |           |           |    | ch        |           |          |
   |           |           |    | aracters. |           |          |
   +-----------+-----------+----+-----------+-----------+----------+
   | Patient's | (0        | DA | From      | VNAP      | MWL/USER |
   | Birth     | 010,0030) |    | Modality  |           |          |
   | Date      |           |    | Worklist  |           |          |
   |           |           |    | or user   |           |          |
   |           |           |    | input     |           |          |
   +-----------+-----------+----+-----------+-----------+----------+
   | Patient's | (0        | CS | From      | VNAP      | MWL/USER |
   | Sex       | 010,0040) |    | Modality  |           |          |
   |           |           |    | Worklist  |           |          |
   |           |           |    | or user   |           |          |
   |           |           |    | input     |           |          |
   +-----------+-----------+----+-----------+-----------+----------+
   | Patient   | (0        | LT | From User | VNAP      | USER     |
   | Comments  | 010,4000) |    | Input.    |           |          |
   |           |           |    | Maximum   |           |          |
   |           |           |    | 1024      |           |          |
   |           |           |    | ch        |           |          |
   |           |           |    | aracters. |           |          |
   +-----------+-----------+----+-----------+-----------+----------+

.. table:: General Study Module of Created SOP Instances

   +-----------+-----------+----+-----------+-----------+----------+
   | Attribute | Tag       | VR | Value     | Presence  | Source   |
   | Name      |           |    |           | of Value  |          |
   +===========+===========+====+===========+===========+==========+
   | Study     | (0        | UI | From      | ALWAYS    | MWL/AUTO |
   | Instance  | 020,000D) |    | Modality  |           |          |
   | UID       |           |    | Worklist  |           |          |
   |           |           |    | or        |           |          |
   |           |           |    | generated |           |          |
   |           |           |    | by device |           |          |
   +-----------+-----------+----+-----------+-----------+----------+
   | Study     | (0        | DA | <         | ALWAYS    | AUTO     |
   | Date      | 008,0020) |    | yyyymmdd> |           |          |
   +-----------+-----------+----+-----------+-----------+----------+
   | Study     | (0        | TM | <hhmmss>  | ALWAYS    | AUTO     |
   | Time      | 008,0030) |    |           |           |          |
   +-----------+-----------+----+-----------+-----------+----------+
   | Referring | (0        | PN | From      | VNAP      | MWL      |
   | Ph        | 008,0090) |    | Modality  |           |          |
   | ysician's |           |    | Worklist  |           |          |
   | Name      |           |    |           |           |          |
   +-----------+-----------+----+-----------+-----------+----------+
   | Study ID  | (0        | SH | Requested | VNAP      | MWL/USER |
   |           | 020,0010) |    | Procedure |           |          |
   |           |           |    | ID from   |           |          |
   |           |           |    | Worklist  |           |          |
   |           |           |    | or User   |           |          |
   |           |           |    | Input     |           |          |
   +-----------+-----------+----+-----------+-----------+----------+
   | Accession | (0        | SH | From      | VNAP      | MWL/USER |
   | Number    | 008,0050) |    | Modality  |           |          |
   |           |           |    | Worklist  |           |          |
   |           |           |    | or user   |           |          |
   |           |           |    | input     |           |          |
   +-----------+-----------+----+-----------+-----------+----------+
   | Study     | (0        | LO | Comment   | VNAP      | USER     |
   | De        | 008,1030) |    | text box  |           |          |
   | scription |           |    | in study  |           |          |
   |           |           |    | list.     |           |          |
   |           |           |    | Maximum   |           |          |
   |           |           |    | 1024      |           |          |
   |           |           |    | ch        |           |          |
   |           |           |    | aracters. |           |          |
   +-----------+-----------+----+-----------+-----------+----------+
   | R         | (0        | SQ | From      | VNAP      | MWL      |
   | eferenced | 008,1110) |    | Modality  |           |          |
   | Study     |           |    | Worklist  |           |          |
   | Sequence  |           |    |           |           |          |
   +-----------+-----------+----+-----------+-----------+----------+
   | >R        | (0        | UI | From      | VNAP      | MWL      |
   | eferenced | 008,1150) |    | Modality  |           |          |
   | SOP Class |           |    | Worklist  |           |          |
   | UID       |           |    |           |           |          |
   +-----------+-----------+----+-----------+-----------+----------+
   | >R        | (0        | UI | From      | VNAP      | MWL      |
   | eferenced | 008,1155) |    | Modality  |           |          |
   | SOP       |           |    | Worklist  |           |          |
   | Instance  |           |    |           |           |          |
   | UID       |           |    |           |           |          |
   +-----------+-----------+----+-----------+-----------+----------+

.. table:: Patient Study Module of Created SOP Instances

   +-----------+-----------+----+-----------+-----------+----------+
   | Attribute | Tag       | VR | Value     | Presence  | Source   |
   | Name      |           |    |           | of Value  |          |
   +===========+===========+====+===========+===========+==========+
   | Admitting | (0        | LO | From      | VNAP      | MWL      |
   | Diagnosis | 008,1080) |    | Modality  |           |          |
   | De        |           |    | Worklist  |           |          |
   | scription |           |    |           |           |          |
   +-----------+-----------+----+-----------+-----------+----------+
   | Patient's | (0        | AS | C         | ALWAYS    | AUTO     |
   | Age       | 010,1010) |    | alculated |           |          |
   |           |           |    | from DoB  |           |          |
   |           |           |    | input on  |           |          |
   |           |           |    | base of   |           |          |
   |           |           |    | actual    |           |          |
   |           |           |    | Date      |           |          |
   +-----------+-----------+----+-----------+-----------+----------+
   | Patient's | (0        | DS | From      | VNAP      | MWL/USER |
   | Weight    | 010,1030) |    | Modality  |           |          |
   |           |           |    | Worklist  |           |          |
   |           |           |    | or user   |           |          |
   |           |           |    | input     |           |          |
   +-----------+-----------+----+-----------+-----------+----------+

.. table:: General Series Module of Created SOP Instances

   +------------+------------+----+------------+------------+--------+
   | Attribute  | Tag        | VR | Value      | Presence   | Source |
   | Name       |            |    |            | of Value   |        |
   +============+============+====+============+============+========+
   | Modality   | (          | CS | RF         | ALWAYS     | AUTO   |
   |            | 0008,0060) |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | Series     | (          | UI | Generated  | ALWAYS     | AUTO   |
   | Instance   | 0020,000E) |    | by device  |            |        |
   | UID        |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | Series     | (          | IS | Generated  | ALWAYS     | AUTO   |
   | Number     | 0020,0011) |    | by device  |            |        |
   +------------+------------+----+------------+------------+--------+
   | Series     | (          | DA | <yyyymmdd> | ALWAYS     | AUTO   |
   | Date       | 0008,0021) |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | Series     | (          | TM | <hhmmss>   | ALWAYS     | AUTO   |
   | Time       | 0008,0031) |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | Performing | (          | PN | Physician  | VNAP       | USER   |
   | P          | 0008,1050) |    | field in   |            |        |
   | hysician's |            |    | Study      |            |        |
   | Name       |            |    | list.      |            |        |
   |            |            |    | Maximum 64 |            |        |
   |            |            |    | c          |            |        |
   |            |            |    | haracters. |            |        |
   +------------+------------+----+------------+------------+--------+
   | Protocol   | (          | LO | Organ      | ALWAYS     | AUTO   |
   | Name       | 0018,1030) |    | program    |            |        |
   +------------+------------+----+------------+------------+--------+
   | Series     | (          | LO | Organ from | VNAP       | USER   |
   | D          | 0008,103E) |    | Study      |            |        |
   | escription |            |    | list.      |            |        |
   |            |            |    | Maximum    |            |        |
   |            |            |    | 512        |            |        |
   |            |            |    | c          |            |        |
   |            |            |    | haracters. |            |        |
   +------------+------------+----+------------+------------+--------+
   | Operator's | (          | PN | Operator   | VNAP       | USER   |
   | Name       | 0008,1070) |    | field in   |            |        |
   |            |            |    | Study      |            |        |
   |            |            |    | list.      |            |        |
   |            |            |    | Maximum 64 |            |        |
   |            |            |    | c          |            |        |
   |            |            |    | haracters. |            |        |
   +------------+------------+----+------------+------------+--------+
   | Referenced | (          | SQ | Identifies | ALWAYS     | MPPS   |
   | Performed  | 0008,1111) |    | the MPPS   |            |        |
   | Procedure  |            |    | SOP        |            |        |
   | Step       |            |    | Instance   |            |        |
   | Sequence   |            |    | to which   |            |        |
   |            |            |    | this image |            |        |
   |            |            |    | is related |            |        |
   +------------+------------+----+------------+------------+--------+
   | >          | (          | UI | MPPS SOP   | ALWAYS     | MPPS   |
   | Referenced | 0008,1150) |    | Class UID  |            |        |
   | SOP Class  |            |    |            |            |        |
   | UID        |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | >          | (          | UI | MPPS SOP   | ALWAYS     | MPPS   |
   | Referenced | 0008,1155) |    | Instance   |            |        |
   | SOP        |            |    | UID        |            |        |
   | Instance   |            |    |            |            |        |
   | UID        |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | Request    | (          | SQ | Zero or 1  | ALWAYS     | AUTO   |
   | Attributes | 0040,0275) |    | item will  |            |        |
   | Sequence   |            |    | be present |            |        |
   +------------+------------+----+------------+------------+--------+
   | >Requested | (          | SH | From       | VNAP       | MWL    |
   | Procedure  | 0040,1001) |    | Modality   |            |        |
   | ID         |            |    | Worklist   |            |        |
   +------------+------------+----+------------+------------+--------+
   | >Scheduled | (          | SH | From       | VNAP       | MWL    |
   | Procedure  | 0040,0009) |    | Modality   |            |        |
   | Step ID    |            |    | Worklist   |            |        |
   +------------+------------+----+------------+------------+--------+
   | >Scheduled | (          | LO | From       | VNAP       | MWL    |
   | Procedure  | 0040,0007) |    | Modality   |            |        |
   | Step       |            |    | Worklist   |            |        |
   | D          |            |    |            |            |        |
   | escription |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | >Scheduled | (          | SQ | From       | VNAP       | MWL    |
   | Protocol   | 0040,0008) |    | Modality   |            |        |
   | Code       |            |    | Worklist   |            |        |
   | Sequence   |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | Performed  | (          | SH | Same as    | ALWAYS     | MPPS   |
   | Procedure  | 0040,0253) |    | MPPS.      |            |        |
   | Step ID    |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | Performed  | (          | DA | Same as    | ALWAYS     | MPPS   |
   | Procedure  | 0040,0244) |    | MPPS       |            |        |
   | Step Start |            |    |            |            |        |
   | Date       |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | Performed  | (          | TM | Same as    | ALWAYS     | MPPS   |
   | Procedure  | 0040,0245) |    | MPPS       |            |        |
   | Step Start |            |    |            |            |        |
   | Time       |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | Performed  | (          | LO | Same as    | VNAP       | MPPS   |
   | Procedure  | 0040,0254) |    | MPPS. From |            |        |
   | Step       |            |    | user       |            |        |
   | D          |            |    | input.     |            |        |
   | escription |            |    | Maximum 64 |            |        |
   |            |            |    | c          |            |        |
   |            |            |    | haracters. |            |        |
   +------------+------------+----+------------+------------+--------+
   | Performed  | (          | SQ | Same as    | ALWAYS     | MPPS   |
   | Protocol   | 0040,0260) |    | MPPS       |            |        |
   | Code       |            |    |            |            |        |
   | Sequence   |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | Comments   | (          | LO | Same as    | VNAP       | MPPS   |
   | on the     | 0040,0280) |    | MPPS. From |            |        |
   | Performed  |            |    | user       |            |        |
   | Procedure  |            |    | input.     |            |        |
   | Step       |            |    | Maximum 64 |            |        |
   |            |            |    | c          |            |        |
   |            |            |    | haracters. |            |        |
   +------------+------------+----+------------+------------+--------+

.. table:: General Equipment Module of Created SOP Instances

   +------------+------------+----+------------+------------+--------+
   | Attribute  | Tag        | VR | Value      | Presence   | Source |
   | Name       |            |    |            | of Value   |        |
   +============+============+====+============+============+========+
   | Ma         | (          | LO | EXAM       | ALWAYS     | AUTO   |
   | nufacturer | 0008,0070) |    | PLE-IMAGIN |            |        |
   |            |            |    | G-PRODUCTS |            |        |
   +------------+------------+----+------------+------------+--------+
   | I          | (          | LO | From       | VNAP       | CONFIG |
   | nstitution | 0008,0080) |    | Con        |            |        |
   | Name       |            |    | figuration |            |        |
   +------------+------------+----+------------+------------+--------+
   | Station    | (          | SH | From       | ALWAYS     | CONFIG |
   | Name       | 0008,1010) |    | Con        |            |        |
   |            |            |    | figuration |            |        |
   +------------+------------+----+------------+------------+--------+
   | Manu       | (          | LO | EXAMPLE    | ALWAYS     | AUTO   |
   | facturer's | 0008,1090) |    | -INTEGRATE |            |        |
   | Model Name |            |    | D-MODALITY |            |        |
   +------------+------------+----+------------+------------+--------+
   | Device     | (          | LO | From       | ALWAYS     | CONFIG |
   | Serial     | 0018,1000) |    | Con        |            |        |
   | Number     |            |    | figuration |            |        |
   +------------+------------+----+------------+------------+--------+
   | Software   | (          | LO | From       | ALWAYS     | CONFIG |
   | Version    | 0018,1020) |    | Con        |            |        |
   |            |            |    | figuration |            |        |
   +------------+------------+----+------------+------------+--------+
   | Private    | (          | LO | EXIN       | ALWAYS     | AUTO   |
   | Creator    | 0009,00xx) |    | TMOD_EQ_01 |            |        |
   +------------+------------+----+------------+------------+--------+
   | Equipment  | (          | UI | From       | ALWAYS     | CONFIG |
   | UID        | 0009,xx01) |    | Con        |            |        |
   |            |            |    | figuration |            |        |
   +------------+------------+----+------------+------------+--------+
   | Service    | (          | UI | From       | ALWAYS     | CONFIG |
   | UID        | 0009,xx02) |    | Con        |            |        |
   |            |            |    | figuration |            |        |
   +------------+------------+----+------------+------------+--------+

.. table:: Private Application Module of Created SOP Instances

   +------------+------------+----+------------+------------+--------+
   | Attribute  | Tag        | VR | Value      | Presence   | Source |
   | Name       |            |    |            | of Value   |        |
   +============+============+====+============+============+========+
   | Private    | (          | LO | EXIN       | ALWAYS     | AUTO   |
   | Creator    | 0029,00xx) |    | TMOD_IM_01 |            |        |
   +------------+------------+----+------------+------------+--------+
   | A          | (          | SQ | Zero or    | VNAP       | AUTO   |
   | pplication | 0029,xx40) |    | more       |            |        |
   | Header     |            |    | items.     |            |        |
   | Sequence   |            |    | Each item  |            |        |
   |            |            |    | contains   |            |        |
   |            |            |    | private    |            |        |
   |            |            |    | a          |            |        |
   |            |            |    | pplication |            |        |
   |            |            |    | data from  |            |        |
   |            |            |    | a          |            |        |
   |            |            |    | different  |            |        |
   |            |            |    | ap         |            |        |
   |            |            |    | plication. |            |        |
   +------------+------------+----+------------+------------+--------+
   | >Private   | (          | LO | EXIN       | ALWAYS     | AUTO   |
   | Creator    | 0029,00xx) |    | TMOD_IM_01 |            |        |
   +------------+------------+----+------------+------------+--------+
   | >          | (          | CS | One of     | ALWAYS     | AUTO   |
   | A          | 0029,xx41) |    | PLATFORM   |            |        |
   | pplication |            |    | or PLUGIN  |            |        |
   | Header     |            |    |            |            |        |
   | Type       |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | >          | (          | LO | One of     | ALWAYS     | AUTO   |
   | A          | 0029,xx42) |    | AC         |            |        |
   | pplication |            |    | QUISITION, |            |        |
   | Header ID  |            |    | IMAGE      |            |        |
   |            |            |    | P          |            |        |
   |            |            |    | ROCESSING, |            |        |
   |            |            |    | VIEWER,    |            |        |
   |            |            |    | AUDIT,     |            |        |
   |            |            |    | ACCESS,    |            |        |
   |            |            |    | ROUTING or |            |        |
   |            |            |    | STATUS     |            |        |
   +------------+------------+----+------------+------------+--------+
   | >          | (          | LO | From       | ALWAYS     | AUTO   |
   | A          | 0029,xx43) |    | A          |            |        |
   | pplication |            |    | pplication |            |        |
   | Header     |            |    |            |            |        |
   | Version    |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | >          | (          | OB | From       | ALWAYS     | AUTO   |
   | A          | 0029,xx44) |    | A          |            |        |
   | pplication |            |    | pplication |            |        |
   | Header     |            |    |            |            |        |
   | Data       |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | Workflow   | (          | LO | One or     | VNAP       | AUTO   |
   | Control    | 0029,xx50) |    | more of:P: |            |        |
   | Flags      |            |    | p          |            |        |
   |            |            |    | rintedcom: |            |        |
   |            |            |    | com        |            |        |
   |            |            |    | pletedrea: |            |        |
   |            |            |    | readver:   |            |        |
   |            |            |    | v          |            |        |
   |            |            |    | erifiedRI: |            |        |
   |            |            |    | r          |            |        |
   |            |            |    | eceivedAC: |            |        |
   |            |            |    | archived   |            |        |
   |            |            |    | and        |            |        |
   |            |            |    | c          |            |        |
   |            |            |    | ommittedE: |            |        |
   |            |            |    | exportedm: |            |        |
   |            |            |    | marked     |            |        |
   +------------+------------+----+------------+------------+--------+
   | Archive    | (          | CS | 00 =       | ALWAYS     | AUTO   |
   | Management | 0029,xx51) |    | remote     |            |        |
   | Flag -     |            |    | control    |            |        |
   | Keep       |            |    | not        |            |        |
   | Online     |            |    | required   |            |        |
   |            |            |    | (          |            |        |
   |            |            |    | default)01 |            |        |
   |            |            |    | = keep     |            |        |
   |            |            |    | instance   |            |        |
   |            |            |    | online.    |            |        |
   +------------+------------+----+------------+------------+--------+
   | Archive    | (          | CS | 00 =       | ALWAYS     | AUTO   |
   | Management | 0029,xx52) |    | remote     |            |        |
   | Flag - Do  |            |    | control    |            |        |
   | Not        |            |    | not        |            |        |
   | Archive    |            |    | required   |            |        |
   |            |            |    | (          |            |        |
   |            |            |    | default)01 |            |        |
   |            |            |    | = do not   |            |        |
   |            |            |    | archive    |            |        |
   |            |            |    | instance.  |            |        |
   +------------+------------+----+------------+------------+--------+

.. _sect_B.8.1.1.4:

X-Ray Radiofluoroscopic Image Modules
'''''''''''''''''''''''''''''''''''''

.. table:: General Image Module of Created Rf SOP Instances

   +------------+------------+----+------------+------------+--------+
   | Attribute  | Tag        | VR | Value      | Presence   | Source |
   | Name       |            |    |            | of Value   |        |
   +============+============+====+============+============+========+
   | Instance   | (          | IS | Generated  | ALWAYS     | AUTO   |
   | Number     | 0020,0013) |    | by device  |            |        |
   +------------+------------+----+------------+------------+--------+
   | Patient    | (          | CS | Zero       | EMPTY      | AUTO   |
   | O          | 0020,0020) |    | length     |            |        |
   | rientation |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | Content    | (          | DA | <yyyymmdd> | ALWAYS     | AUTO   |
   | Date       | 0008,0023) |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | Content    | (          | TM | <hhmmss>   | ALWAYS     | AUTO   |
   | Time       | 0008,0033) |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | A          | (          | IS | Generated  | ALWAYS     | AUTO   |
   | cquisition | 0020,0012) |    | by device  |            |        |
   | Number     |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | Image      | (          | LT | From user  | VNAP       | USER   |
   | Comments   | 0020,4000) |    | input.     |            |        |
   |            |            |    | Maximum    |            |        |
   |            |            |    | 1024       |            |        |
   |            |            |    | c          |            |        |
   |            |            |    | haracters. |            |        |
   +------------+------------+----+------------+------------+--------+
   | Anatomic   | (          | SQ | From user  | ALWAYS     | USER   |
   | Region     | 0008,2218) |    | input.     |            |        |
   | Sequence   |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | > Include  | Baseline   |    |            |            |        |
   | 'Code      | Context ID |    |            |            |        |
   | Sequence   | is 4009    |    |            |            |        |
   | Macro'     | (see also  |    |            |            |        |
   |            | `Private   |    |            |            |        |
   |            | Transfer   |    |            |            |        |
   |            | Syntax     |    |            |            |        |
   |            | es <#sect_ |    |            |            |        |
   |            | B.8.6>`__) |    |            |            |        |
   +------------+------------+----+------------+------------+--------+

.. table:: Image Pixel Module of Created Rf SOP Instances

   +------------+------------+----+------------+------------+--------+
   | Attribute  | Tag        | VR | Value      | Presence   | Source |
   | Name       |            |    |            | of Value   |        |
   +============+============+====+============+============+========+
   | Pixel Data | (          | OW | The Pixel  | ALWAYS     | AUTO   |
   |            | 7FE0,0010) |    | Data       |            |        |
   |            |            |    | itself     |            |        |
   |            |            |    | does not   |            |        |
   |            |            |    | contain    |            |        |
   |            |            |    | any        |            |        |
   |            |            |    | burned-in  |            |        |
   |            |            |    | a          |            |        |
   |            |            |    | nnotation. |            |        |
   +------------+------------+----+------------+------------+--------+

.. table:: Cine Module of Created Rf SOP

   +------------+------------+----+------------+------------+--------+
   | Attribute  | Tag        | VR | Value      | Presence   | Source |
   | Name       |            |    |            | of Value   |        |
   +============+============+====+============+============+========+
   | Frame Time | (          | DS | Only if    | ANAP       | AUTO   |
   |            | 0018,1063) |    | mu         |            |        |
   |            |            |    | lti-frame. |            |        |
   +------------+------------+----+------------+------------+--------+
   | R          | (          | IS | Only if    | ANAP       | AUTO   |
   | ecommended | 0008,2144) |    | m          |            |        |
   | Display    |            |    | ulti-frame |            |        |
   | Frame Rate |            |    | Same as    |            |        |
   |            |            |    | Cine Rate  |            |        |
   +------------+------------+----+------------+------------+--------+
   | Cine Rate  | (          | IS | Only if    | ANAP       | AUTO   |
   |            | 0018,0040) |    | m          |            |        |
   |            |            |    | ulti-frame |            |        |
   +------------+------------+----+------------+------------+--------+

.. table:: Multi-Frame Module of Created Rf SOP Instances

   +------------------+-------------+----+---------------------+-------------------+--------+
   | Attribute Name   | Tag         | VR | Value               | Presence of Value | Source |
   +==================+=============+====+=====================+===================+========+
   | Number of Frames | (0028,0008) | IS | Only if multi-frame | ANAP              | AUTO   |
   +------------------+-------------+----+---------------------+-------------------+--------+

.. table:: Frame Pointers Module of Created Rf SOP Instances

   +------------+------------+----+------------+------------+--------+
   | Attribute  | Tag        | VR | Value      | Presence   | Source |
   | Name       |            |    |            | of Value   |        |
   +============+============+====+============+============+========+
   | Repr       | (          | US | Only if    | ANAP       | AUTO   |
   | esentative | 0028,6010) |    | m          |            |        |
   | Frame      |            |    | ulti-frame |            |        |
   | Number     |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+

.. table:: Mask Module of Created Rf SOP Instances

   +------------+------------+----+------------+------------+--------+
   | Attribute  | Tag        | VR | Value      | Presence   | Source |
   | Name       |            |    |            | of Value   |        |
   +============+============+====+============+============+========+
   | Mask       | (          | SQ | Only if    | ANAP       | AUTO   |
   | S          | 0028,6100) |    | m          |            |        |
   | ubtraction |            |    | ulti-frame |            |        |
   | Sequence   |            |    | and        |            |        |
   |            |            |    | (          |            |        |
   |            |            |    | 0028,1040) |            |        |
   |            |            |    | = LOG      |            |        |
   +------------+------------+----+------------+------------+--------+
   | > Mask     | (          | CS | AVG_SUB    | ANAP       | AUTO   |
   | Operation  | 0028,6101) |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | > Mask     | (          | US | Mask Frame | ANAP       | AUTO   |
   | Frame      | 0028,6110) |    | Number     |            |        |
   | Numbers    |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | R          | (          | CS | NAT or SUB | ALWAYS     | AUTO   |
   | ecommended | 0028,1090) |    |            |            |        |
   | Viewing    |            |    |            |            |        |
   | Mode       |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+

.. table:: X-Ray Image Module of Created Rf SOP Instances

   +------------+------------+----+------------+------------+--------+
   | Attribute  | Tag        | VR | Value      | Presence   | Source |
   | Name       |            |    |            | of Value   |        |
   +============+============+====+============+============+========+
   | Frame      | (          | AT | <          | ANAP       | AUTO   |
   | Increment  | 0028,0009) |    | 0018,1063> |            |        |
   | Pointer    |            |    | only if    |            |        |
   |            |            |    | m          |            |        |
   |            |            |    | ulti-frame |            |        |
   +------------+------------+----+------------+------------+--------+
   | Image Type | (          | CS | ORI        | ALWAYS     | AUTO   |
   |            | 0008,0008) |    | GINAL\PRIM |            |        |
   |            |            |    | ARY\SINGLE |            |        |
   |            |            |    | PLANE\DAS  |            |        |
   |            |            |    |            |            |        |
   |            |            |    | (acquired  |            |        |
   |            |            |    | images)    |            |        |
   |            |            |    |            |            |        |
   |            |            |    | ORI        |            |        |
   |            |            |    | GINAL\DERI |            |        |
   |            |            |    | VED\SINGLE |            |        |
   |            |            |    | PLANE      |            |        |
   |            |            |    |            |            |        |
   |            |            |    | (post      |            |        |
   |            |            |    | -processed |            |        |
   |            |            |    | images)    |            |        |
   +------------+------------+----+------------+------------+--------+
   | Pixel      | (          | CS | LIN or LOG | ALWAYS     | AUTO   |
   | Intensity  | 0028,1040) |    |            |            |        |
   | Re         |            |    |            |            |        |
   | lationship |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | Samples    | (          | US | 1          | ALWAYS     | AUTO   |
   | per Pixel  | 0028,0002) |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | P          | (          | CS | M          | ALWAYS     | AUTO   |
   | hotometric | 0028,0004) |    | ONOCHROME2 |            |        |
   | Inte       |            |    |            |            |        |
   | rpretation |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | Rows       | (          | US | 1024       | ALWAYS     | AUTO   |
   |            | 0028,0010) |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | Columns    | (          | US | 1024       | ALWAYS     | AUTO   |
   |            | 0028,0011) |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | Bits       | (          | US | 16         | ALWAYS     | AUTO   |
   | Allocated  | 0028,0100) |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | Bits       | (          | US | 10         | ALWAYS     | AUTO   |
   | Stored     | 0028,0101) |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | High Bit   | (          | US | 9          | ALWAYS     | AUTO   |
   |            | 0028,0102) |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | Pixel      | (          | US | 0000H      | ALWAYS     | AUTO   |
   | Repr       | 0028,0103) |    |            |            |        |
   | esentation |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+

.. table:: X-Ray Acquisition Module of Created Rf SOP Instances

   +------------+------------+----+------------+------------+--------+
   | Attribute  | Tag        | VR | Value      | Presence   | Source |
   | Name       |            |    |            | of Value   |        |
   +============+============+====+============+============+========+
   | KVP        | (          | DS | From       | ALWAYS     | AUTO   |
   |            | 0018,0060) |    | A          |            |        |
   |            |            |    | cquisition |            |        |
   |            |            |    | parameters |            |        |
   +------------+------------+----+------------+------------+--------+
   | Radiation  | (          | CS | GR         | ALWAYS     | AUTO   |
   | Setting    | 0018,1155) |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | X-Ray Tube | (          | IS | From       | ALWAYS     | AUTO   |
   | Current    | 0018,1151) |    | A          |            |        |
   |            |            |    | cquisition |            |        |
   |            |            |    | parameters |            |        |
   +------------+------------+----+------------+------------+--------+
   | Exposure   | (          | IS | From       | ALWAYS     | AUTO   |
   | Time       | 0018,1150) |    | A          |            |        |
   |            |            |    | cquisition |            |        |
   |            |            |    | parameters |            |        |
   +------------+------------+----+------------+------------+--------+
   | Radiation  | (          | CS | CONTINUOUS | ALWAYS     | AUTO   |
   | Mode       | 0018,115A) |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | I          | (          | DS | From       | ALWAYS     | AUTO   |
   | ntensifier | 0018,1162) |    | A          |            |        |
   | Size       |            |    | cquisition |            |        |
   |            |            |    | parameters |            |        |
   +------------+------------+----+------------+------------+--------+
   | Private    | (          | LO | EXIN       | ALWAYS     | AUTO   |
   | Creator    | 0019,00xx) |    | TMOD_AQ_01 |            |        |
   +------------+------------+----+------------+------------+--------+
   | Edge       | (          | IS | 0 .. 100   | VNAP       | AUTO   |
   | E          | 0019,xx10) |    |            |            |        |
   | nhancement |            |    |            |            |        |
   | Percent    |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | Landmark   | (          | IS | 0 .. 100   | VNAP       | AUTO   |
   |            | 0019,xx20) |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | Pixel      | (          | DS | -20 .. +20 | VNAP       | AUTO   |
   | Shift      | 0019,xx30) |    |            |            |        |
   | Horizontal |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | Pixel      | (          | DS | -20 .. +20 | VNAP       | AUTO   |
   | Shift      | 0019,xx40) |    |            |            |        |
   | Vertical   |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+

.. table:: Modality LUT Module of Created Rf SOP Instances

   +------------+------------+----+------------+------------+--------+
   | Attribute  | Tag        | VR | Value      | Presence   | Source |
   | Name       |            |    |            | of Value   |        |
   +============+============+====+============+============+========+
   | Modality   | (          | SQ | present if | ANAP       | AUTO   |
   | LUT        | 0028,3000) |    | (          |            |        |
   | Sequence   |            |    | 0028,1040) |            |        |
   |            |            |    | = LOG      |            |        |
   +------------+------------+----+------------+------------+--------+
   | > LUT      | (          | US | <          | ANAP       | AUTO   |
   | Descriptor | 0028,3002) |    | 1024,0,16> |            |        |
   +------------+------------+----+------------+------------+--------+
   | > Modality | (          | LO | US         | ANAP       | AUTO   |
   | LUT Type   | 0028,3004) |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | > LUT Data | (          | US | LUT        | ANAP       | AUTO   |
   |            | 0028,3006) |    |            |            |        |
   +------------+------------+----+------------+------------+--------+

.. table:: VOI LUT Module of Created RF SOP Instances

   ============== =========== == ====== ================= ======
   Attribute Name Tag         VR Value  Presence of Value Source
   ============== =========== == ====== ================= ======
   Window Center  (0028,1050) DS 0…1023 ALWAYS            AUTO
   Window Width   (0028,1051) DS 1…1024 ALWAYS            AUTO
   ============== =========== == ====== ================= ======

.. table:: SOP Common Module of Created Rf SOP Instances

   +------------+------------+----+------------+------------+--------+
   | Attribute  | Tag        | VR | Value      | Presence   | Source |
   | Name       |            |    |            | of Value   |        |
   +============+============+====+============+============+========+
   | Specific   | (          | CS | "ISO_IR    | ALWAYS     | CONFIG |
   | Character  | 0008,0005) |    | 100" or    |            |        |
   | Set        |            |    | "ISO_IR    |            |        |
   |            |            |    | 144"       |            |        |
   +------------+------------+----+------------+------------+--------+
   | SOP Class  | (          | UI | 1.2.840.   | ALWAYS     | AUTO   |
   | UID        | 0008,0016) |    | 10008.5.1. |            |        |
   |            |            |    | 4.1.1.12.2 |            |        |
   +------------+------------+----+------------+------------+--------+
   | SOP        | (          | UI | Generated  | ALWAYS     | AUTO   |
   | Instance   | 0008,0018) |    | by device  |            |        |
   | UID        |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+

.. _sect_B.8.1.1.5:

Grayscale Softcopy Presentation State Modules
'''''''''''''''''''''''''''''''''''''''''''''

.. table:: Presentation Series Module of Created GSPS SOP Instances

   ============== =========== == ===== ================= ======
   Attribute Name Tag         VR Value Presence of Value Source
   ============== =========== == ===== ================= ======
   Modality       (0008,0060) CS PR    ALWAYS            AUTO
   ============== =========== == ===== ================= ======

.. table:: Presentation State Module of Created GSPS SOP Instances

   +------------+------------+----+------------+------------+--------+
   | Attribute  | Tag        | VR | Value      | Presence   | Source |
   | Name       |            |    |            | of Value   |        |
   +============+============+====+============+============+========+
   | Instance   | (          | IS | Generated  | ALWAYS     | AUTO   |
   | Number     | 0020,0013) |    | by device  |            |        |
   +------------+------------+----+------------+------------+--------+
   | Pr         | (          | CS | From user  | ALWAYS     | USER   |
   | esentation | 0070,0080) |    | input.     |            |        |
   | Label      |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | Pr         | (          | LO | From user  | VNAP       | USER   |
   | esentation | 0070,0081) |    | input.     |            |        |
   | D          |            |    |            |            |        |
   | escription |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | Pr         | (          | DA | Generated  | ALWAYS     | AUTO   |
   | esentation | 0070,0082) |    | by device  |            |        |
   | Creation   |            |    |            |            |        |
   | Date       |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | Pr         | (          | TM | Generated  | ALWAYS     | AUTO   |
   | esentation | 0070,0083) |    | by device  |            |        |
   | Creation   |            |    |            |            |        |
   | Time       |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | Pr         | (          | PN | Generated  | ALWAYS     | AUTO   |
   | esentation | 0070,0084) |    | by device  |            |        |
   | Creator's  |            |    | according  |            |        |
   | Name       |            |    | to         |            |        |
   |            |            |    | currently  |            |        |
   |            |            |    | active     |            |        |
   |            |            |    | user.      |            |        |
   +------------+------------+----+------------+------------+--------+
   | Referenced | (          | SQ | One or     | ALWAYS     | AUTO   |
   | Series     | 0008,1115) |    | more       |            |        |
   | Sequence   |            |    | items.     |            |        |
   +------------+------------+----+------------+------------+--------+
   | >Series    | (          | UI | From       | ALWAYS     | AUTO   |
   | Instance   | 0020,000E) |    | referenced |            |        |
   | UID        |            |    | image      |            |        |
   +------------+------------+----+------------+------------+--------+
   | >          | (          | SQ | From       | ALWAYS     | AUTO   |
   | Referenced | 0008,1140) |    | referenced |            |        |
   | Image      |            |    | image      |            |        |
   | Sequence   |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | >>         | (          | UI | From       | ALWAYS     | AUTO   |
   | Referenced | 0008,1150) |    | referenced |            |        |
   | SOP Class  |            |    | image      |            |        |
   | UID        |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | >>         | (          | UI | From       | ALWAYS     | AUTO   |
   | Referenced | 0008,1155) |    | referenced |            |        |
   | SOP        |            |    | image      |            |        |
   | Instance   |            |    |            |            |        |
   | UID        |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | >>         | (          | IS | If         | ANAP       | AUTO   |
   | Referenced | 0008,1160) |    | referenced |            |        |
   | Frame      |            |    | image is a |            |        |
   | Number     |            |    | m          |            |        |
   |            |            |    | ulti-frame |            |        |
   |            |            |    | image      |            |        |
   +------------+------------+----+------------+------------+--------+
   | Shutter    | (          | US | Generated  | ANAP       | AUTO   |
   | Pr         | 0018,1622) |    | by device  |            |        |
   | esentation |            |    | if shutter |            |        |
   | Value      |            |    | present    |            |        |
   +------------+------------+----+------------+------------+--------+

.. table:: Display Shutter Module of Created GSPS SOP Instances

   +------------+------------+----+------------+------------+--------+
   | Attribute  | Tag        | VR | Value      | Presence   | Source |
   | Name       |            |    |            | of Value   |        |
   +============+============+====+============+============+========+
   | Shutter    | (          | CS | If shutter | ANAP       | AUTO   |
   | Shape      | 0018,1600) |    | applied:   |            |        |
   |            |            |    | RECTANGULA |            |        |
   |            |            |    | R\CIRCULAR |            |        |
   +------------+------------+----+------------+------------+--------+
   | Shutter    | (          | IS | If         | ANAP       | AUTO   |
   | Left       | 0018,1602) |    | R          |            |        |
   | Vertical   |            |    | ECTANGULAR |            |        |
   | Edge       |            |    | shutter    |            |        |
   |            |            |    | applied    |            |        |
   +------------+------------+----+------------+------------+--------+
   | Shutter    | (          | IS | If         | ANAP       | AUTO   |
   | Right      | 0018,1604) |    | R          |            |        |
   | Vertical   |            |    | ECTANGULAR |            |        |
   | Edge       |            |    | shutter    |            |        |
   |            |            |    | applied    |            |        |
   +------------+------------+----+------------+------------+--------+
   | Shutter    | (          | IS | If         | ANAP       | AUTO   |
   | Upper      | 0018,1606) |    | R          |            |        |
   | Horizontal |            |    | ECTANGULAR |            |        |
   | Edge       |            |    | shutter    |            |        |
   |            |            |    | applied    |            |        |
   +------------+------------+----+------------+------------+--------+
   | Shutter    | (          | IS | If         | ANAP       | AUTO   |
   | Lower      | 0018,1608) |    | R          |            |        |
   | Horizontal |            |    | ECTANGULAR |            |        |
   | Edge       |            |    | shutter    |            |        |
   |            |            |    | applied    |            |        |
   +------------+------------+----+------------+------------+--------+
   | Center of  | (          | IS | If         | ANAP       | AUTO   |
   | Circular   | 0018,1610) |    | CIRCULAR   |            |        |
   | Shutter    |            |    | shutter    |            |        |
   |            |            |    | applied    |            |        |
   +------------+------------+----+------------+------------+--------+
   | Radius of  | (          | IS | If         | ANAP       | AUTO   |
   | Circular   | 0018,1612) |    | CIRCULAR   |            |        |
   | Shutter    |            |    | shutter    |            |        |
   |            |            |    | applied    |            |        |
   +------------+------------+----+------------+------------+--------+

.. table:: Displayed Area Module of Created GSPS SOP Instances

   +------------+------------+----+------------+------------+--------+
   | Attribute  | Tag        | VR | Value      | Presence   | Source |
   | Name       |            |    |            | of Value   |        |
   +============+============+====+============+============+========+
   | Displayed  | (          | SQ | One or     | ALWAYS     | AUTO   |
   | Area       | 0070,005A) |    | more items |            |        |
   | Selection  |            |    |            |            |        |
   | Sequence   |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | >          | (          | SQ | One or     | ALWAYS     | AUTO   |
   | Referenced | 0008,1140) |    | more items |            |        |
   | Image      |            |    |            |            |        |
   | Sequence   |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | >>         | (          | UI | From       | ALWAYS     | AUTO   |
   | Referenced | 0008,1150) |    | referenced |            |        |
   | SOP Class  |            |    | image      |            |        |
   | UID        |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | >>         | (          | UI | From       | ALWAYS     | AUTO   |
   | Referenced | 0008,1155) |    | referenced |            |        |
   | SOP        |            |    | image      |            |        |
   | Instance   |            |    |            |            |        |
   | UID        |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | >>         | (          | IS | If         | ANAP       | AUTO   |
   | Referenced | 0008,1160) |    | referenced |            |        |
   | Frame      |            |    | image is a |            |        |
   | Number     |            |    | m          |            |        |
   |            |            |    | ulti-frame |            |        |
   |            |            |    | image      |            |        |
   +------------+------------+----+------------+------------+--------+
   | >Displayed | (          | SL | From       | ALWAYS     | AUTO   |
   | Area Top   | 0070,0052) |    | current    |            |        |
   | Left Hand  |            |    | display    |            |        |
   | Corner     |            |    | setting    |            |        |
   +------------+------------+----+------------+------------+--------+
   | >Displayed | (          | SL | From       | ALWAYS     | AUTO   |
   | Area       | 0070,0053) |    | current    |            |        |
   | Bottom     |            |    | display    |            |        |
   | Right Hand |            |    | setting    |            |        |
   | Corner     |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | >Pr        | (          | CS | From       | ALWAYS     | AUTO   |
   | esentation | 0070,0100) |    | current    |            |        |
   | Size Mode  |            |    | display    |            |        |
   |            |            |    | setting    |            |        |
   +------------+------------+----+------------+------------+--------+
   | >Pr        | (          | DS | From       | ANAP       | AUTO   |
   | esentation | 0070,0101) |    | current    |            |        |
   | Pixel      |            |    | display    |            |        |
   | Spacing    |            |    | setting    |            |        |
   +------------+------------+----+------------+------------+--------+
   | >Pr        | (          | IS | From       | ANAP       | AUTO   |
   | esentation | 0070,0102) |    | current    |            |        |
   | Pixel      |            |    | display    |            |        |
   | Aspect     |            |    | setting    |            |        |
   | Ratio      |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | >Pr        | (          | FL | From       | ANAP       | AUTO   |
   | esentation | 0070,0103) |    | current    |            |        |
   | Pixel      |            |    | display    |            |        |
   | Mag        |            |    | setting    |            |        |
   | nification |            |    |            |            |        |
   | Ratio      |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+

.. table:: Graphic Annotation Module of Created GSPS SOP Instances

   +------------+------------+----+------------+------------+--------+
   | Attribute  | Tag        | VR | Value      | Presence   | Source |
   | Name       |            |    |            | of Value   |        |
   +============+============+====+============+============+========+
   | Graphic    | (          | SQ | One or     | ANAP       | AUTO   |
   | Annotation | 0070,0001) |    | more items |            |        |
   | Sequence   |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | >          | (          | SQ | One or     | ALWAYS     | AUTO   |
   | Referenced | 0008,1140) |    | more items |            |        |
   | Image      |            |    |            |            |        |
   | Sequence   |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | >>         | (          | UI | From       | ALWAYS     | AUTO   |
   | Referenced | 0008,1150) |    | referenced |            |        |
   | SOP Class  |            |    | image      |            |        |
   | UID        |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | >>         | (          | UI | From       | ALWAYS     | AUTO   |
   | Referenced | 0008,1155) |    | referenced |            |        |
   | SOP        |            |    | image      |            |        |
   | Instance   |            |    |            |            |        |
   | UID        |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | >>         | (          | IS | If         | ANAP       | AUTO   |
   | Referenced | 0008,1160) |    | referenced |            |        |
   | Frame      |            |    | image is a |            |        |
   | Number     |            |    | m          |            |        |
   |            |            |    | ulti-frame |            |        |
   |            |            |    | image      |            |        |
   +------------+------------+----+------------+------------+--------+
   | >Graphic   | (          | CS | Layer in   | ALWAYS     | AUTO   |
   | Layer      | 0070,0002) |    | Graphic    |            |        |
   |            |            |    | Layer      |            |        |
   |            |            |    | Module     |            |        |
   +------------+------------+----+------------+------------+--------+
   | >Text      | (          | SQ | One or     | ANAP       | AUTO   |
   | Object     | 0070,0008) |    | more items |            |        |
   | Sequence   |            |    | if text    |            |        |
   |            |            |    | annotation |            |        |
   |            |            |    | present    |            |        |
   +------------+------------+----+------------+------------+--------+
   | >>Anchor   | (          | CS | PIXEL      | ALWAYS     | AUTO   |
   | Point      | 0070,0004) |    |            |            |        |
   | Annotation |            |    |            |            |        |
   | Units      |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | >>U        | (          | ST | From user  | ALWAYS     | USER   |
   | nformatted | 0070,0006) |    | input      |            |        |
   | Text Value |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | >>Anchor   | (          | FL | From user  | ALWAYS     | USER   |
   | Point      | 0070,0014) |    | input      |            |        |
   +------------+------------+----+------------+------------+--------+
   | >>Anchor   | (          | CS | From user  | ALWAYS     | USER   |
   | Point      | 0070,0015) |    | input      |            |        |
   | Visibility |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | >Graphic   | (          | SQ | One or     | ANAP       | AUTO   |
   | Object     | 0070,0009) |    | more items |            |        |
   | Sequence   |            |    | if graphic |            |        |
   |            |            |    | annotation |            |        |
   |            |            |    | present    |            |        |
   +------------+------------+----+------------+------------+--------+
   | >>Graphic  | (          | CS | PIXEL      | ALWAYS     | AUTO   |
   | Annotation | 0070,0005) |    |            |            |        |
   | Units      |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | >>Graphic  | (          | US | 2          | ALWAYS     | AUTO   |
   | Dimensions | 0070,0020) |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | >>Number   | (          | US | From user  | ALWAYS     | USER   |
   | of Graphic | 0070,0021) |    | input      |            |        |
   | Points     |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | >>Graphic  | (          | FL | From user  | ALWAYS     | USER   |
   | Data       | 0070,0022) |    | input      |            |        |
   +------------+------------+----+------------+------------+--------+
   | >>Graphic  | (          | CS | One of     | ALWAYS     | USER   |
   | Type       | 0070,0023) |    | POINT,     |            |        |
   |            |            |    | POLYLINE,  |            |        |
   |            |            |    | INT        |            |        |
   |            |            |    | ERPOLATED, |            |        |
   |            |            |    | CIRCLE or  |            |        |
   |            |            |    | ELLIPSE    |            |        |
   +------------+------------+----+------------+------------+--------+
   | >>Graphic  | (          | CS | From user  | ANAP       | USER   |
   | Filled     | 0070,0024) |    | input      |            |        |
   +------------+------------+----+------------+------------+--------+
   | Attribute  | Tag        | VR | Value      | Presence   | Source |
   | Name       |            |    |            | of Value   |        |
   +------------+------------+----+------------+------------+--------+
   | Graphic    | (          | SQ | One or     | ANAP       | AUTO   |
   | Annotation | 0070,0001) |    | more items |            |        |
   | Sequence   |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | >          | (          | SQ | One or     | ALWAYS     | AUTO   |
   | Referenced | 0008,1140) |    | more items |            |        |
   | Image      |            |    |            |            |        |
   | Sequence   |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | >>         | (          | UI | From       | ALWAYS     | AUTO   |
   | Referenced | 0008,1150) |    | referenced |            |        |
   | SOP Class  |            |    | image      |            |        |
   | UID        |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | >>         | (          | UI | From       | ALWAYS     | AUTO   |
   | Referenced | 0008,1155) |    | referenced |            |        |
   | SOP        |            |    | image      |            |        |
   | Instance   |            |    |            |            |        |
   | UID        |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | >>         | (          | IS | If         | ANAP       | AUTO   |
   | Referenced | 0008,1160) |    | referenced |            |        |
   | Frame      |            |    | image is a |            |        |
   | Number     |            |    | m          |            |        |
   |            |            |    | ulti-frame |            |        |
   |            |            |    | image      |            |        |
   +------------+------------+----+------------+------------+--------+
   | >Graphic   | (          | CS | Layer in   | ALWAYS     | AUTO   |
   | Layer      | 0070,0002) |    | Graphic    |            |        |
   |            |            |    | Layer      |            |        |
   |            |            |    | Module     |            |        |
   +------------+------------+----+------------+------------+--------+
   | >Text      | (          | SQ | One or     | ANAP       | AUTO   |
   | Object     | 0070,0008) |    | more items |            |        |
   | Sequence   |            |    | if text    |            |        |
   |            |            |    | annotation |            |        |
   |            |            |    | present    |            |        |
   +------------+------------+----+------------+------------+--------+
   | >>Anchor   | (          | CS | PIXEL      | ALWAYS     | AUTO   |
   | Point      | 0070,0004) |    |            |            |        |
   | Annotation |            |    |            |            |        |
   | Units      |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | >>U        | (          | ST | From user  | ALWAYS     | USER   |
   | nformatted | 0070,0006) |    | input      |            |        |
   | Text Value |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | >>Anchor   | (          | FL | From user  | ALWAYS     | USER   |
   | Point      | 0070,0014) |    | input      |            |        |
   +------------+------------+----+------------+------------+--------+
   | >>Anchor   | (          | CS | From user  | ALWAYS     | USER   |
   | Point      | 0070,0015) |    | input      |            |        |
   | Visibility |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | >Graphic   | (          | SQ | One or     | ANAP       | AUTO   |
   | Object     | 0070,0009) |    | more items |            |        |
   | Sequence   |            |    | if graphic |            |        |
   |            |            |    | annotation |            |        |
   |            |            |    | present    |            |        |
   +------------+------------+----+------------+------------+--------+
   | >>Graphic  | (          | CS | PIXEL      | ALWAYS     | AUTO   |
   | Annotation | 0070,0005) |    |            |            |        |
   | Units      |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | >>Graphic  | (          | US | 2          | ALWAYS     | AUTO   |
   | Dimensions | 0070,0020) |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | >>Number   | (          | US | From user  | ALWAYS     | USER   |
   | of Graphic | 0070,0021) |    | input      |            |        |
   | Points     |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | >>Graphic  | (          | FL | From user  | ALWAYS     | USER   |
   | Data       | 0070,0022) |    | input      |            |        |
   +------------+------------+----+------------+------------+--------+
   | >>Graphic  | (          | CS | One of     | ALWAYS     | USER   |
   | Type       | 0070,0023) |    | POINT,     |            |        |
   |            |            |    | POLYLINE,  |            |        |
   |            |            |    | INT        |            |        |
   |            |            |    | ERPOLATED, |            |        |
   |            |            |    | CIRCLE or  |            |        |
   |            |            |    | ELLIPSE    |            |        |
   +------------+------------+----+------------+------------+--------+
   | >>Graphic  | (          | CS | From user  | ANAP       | USER   |
   | Filled     | 0070,0024) |    | input      |            |        |
   +------------+------------+----+------------+------------+--------+

.. table:: Spatial Transformation Module of Created GSPS SOP Instances

   +------------+------------+----+------------+------------+--------+
   | Attribute  | Tag        | VR | Value      | Presence   | Source |
   | Name       |            |    |            | of Value   |        |
   +============+============+====+============+============+========+
   | Image      | (          | US | From       | ANAP       | AUTO   |
   | Rotation   | 0070,0042) |    | current    |            |        |
   |            |            |    | display    |            |        |
   |            |            |    | setting    |            |        |
   +------------+------------+----+------------+------------+--------+
   | Image      | (          | CS | From       | ANAP       | AUTO   |
   | Horizontal | 0070,0041) |    | current    |            |        |
   | Flip       |            |    | display    |            |        |
   |            |            |    | setting    |            |        |
   +------------+------------+----+------------+------------+--------+

.. table:: Graphic Layer Module of Created GSPS SOP Instances

   +------------+------------+----+------------+------------+--------+
   | Attribute  | Tag        | VR | Value      | Presence   | Source |
   | Name       |            |    |            | of Value   |        |
   +============+============+====+============+============+========+
   | Graphic    | (          | SQ | One or     | ANAP       | AUTO   |
   | Layer      | 0070,0060) |    | more items |            |        |
   | Sequence   |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | >Graphic   | (          | CS | LAYER1.    | ALWAYS     | AUTO   |
   | Layer      | 0070,0002) |    | LAYER2,    |            |        |
   |            |            |    | LAYER3, …  |            |        |
   +------------+------------+----+------------+------------+--------+
   | >Graphic   | (          | IS | From       | ALWAYS     | AUTO   |
   | Layer      | 0070,0062) |    | current    |            |        |
   | Order      |            |    | display    |            |        |
   |            |            |    | setting    |            |        |
   +------------+------------+----+------------+------------+--------+

.. table:: Modality LUT Module of Created GSPS SOP Instances

   +-----------------------+-------------+----+-------------+-------------------+--------+
   | Attribute Name        | Tag         | VR | Value       | Presence of Value | Source |
   +=======================+=============+====+=============+===================+========+
   | Modality LUT Sequence | (0028,3000) | SQ | One item    | ANAP              | AUTO   |
   +-----------------------+-------------+----+-------------+-------------------+--------+
   | >LUT Descriptor       | (0028,3002) | US | <1024,0,16> | ALWAYS            | AUTO   |
   +-----------------------+-------------+----+-------------+-------------------+--------+
   | >Modality LUT Type    | (0028,3004) | LO | US          | ALWAYS            | AUTO   |
   +-----------------------+-------------+----+-------------+-------------------+--------+
   | >LUT Data             | (0028,3006) | US | LUT         | ALWAYS            | AUTO   |
   +-----------------------+-------------+----+-------------+-------------------+--------+
   | Rescale Intercept     | (0028,1052) | DS | 1           | ANAP              | AUTO   |
   +-----------------------+-------------+----+-------------+-------------------+--------+
   | Rescale Slope         | (0028,1053) | DS | 0           | ANAP              | AUTO   |
   +-----------------------+-------------+----+-------------+-------------------+--------+
   | Rescale Type          | (0028,1054) | LO | US          | ANAP              | AUTO   |
   +-----------------------+-------------+----+-------------+-------------------+--------+

.. table:: Softcopy VOI LUT Module of Created GSPS SOP Instances

   +------------+------------+----+------------+------------+--------+
   | Attribute  | Tag        | VR | Value      | Presence   | Source |
   | Name       |            |    |            | of Value   |        |
   +============+============+====+============+============+========+
   | Softcopy   | (          | SQ | One or     | ALWAYS     | AUTO   |
   | VOI LUT    | 0028,3110) |    | more items |            |        |
   | Sequence   |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | >          | (          | SQ | One or     | ALWAYS     | AUTO   |
   | Referenced | 0008,1140) |    | more items |            |        |
   | Image      |            |    |            |            |        |
   | Sequence   |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | >>         | (          | UI | From       | ALWAYS     | AUTO   |
   | Referenced | 0008,1150) |    | referenced |            |        |
   | SOP Class  |            |    | image      |            |        |
   | UID        |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | >>         | (          | UI | From       | ALWAYS     | AUTO   |
   | Referenced | 0008,1155) |    | referenced |            |        |
   | SOP        |            |    | image      |            |        |
   | Instance   |            |    |            |            |        |
   | UID        |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+
   | >>         | (          | IS | If         | ANAP       | AUTO   |
   | Referenced | 0008,1160) |    | referenced |            |        |
   | Frame      |            |    | image is a |            |        |
   | Number     |            |    | m          |            |        |
   |            |            |    | ulti-frame |            |        |
   |            |            |    | image      |            |        |
   +------------+------------+----+------------+------------+--------+
   | >Window    | (          | DS | From       | ALWAYS     | AUTO   |
   | Center     | 0028,1050) |    | current    |            |        |
   |            |            |    | display    |            |        |
   |            |            |    | setting:   |            |        |
   |            |            |    | 0…1023     |            |        |
   +------------+------------+----+------------+------------+--------+
   | >Window    | (          | DS | From       | ALWAYS     | AUTO   |
   | Width      | 0028,1051) |    | current    |            |        |
   |            |            |    | display    |            |        |
   |            |            |    | setting:   |            |        |
   |            |            |    | 1…1024     |            |        |
   +------------+------------+----+------------+------------+--------+
   | >Window    | (          | LO | Name of    | ANAP       | AUTO   |
   | Center &   | 0028,1055) |    | Window     |            |        |
   | Width      |            |    | Preset     |            |        |
   | E          |            |    |            |            |        |
   | xplanation |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+

.. table:: Softcopy Presentation LUT Module of Created GSPS SOP
Instances

   ====================== ========== == ======== ================= ======
   Attribute Name         Tag        VR Value    Presence of Value Source
   ====================== ========== == ======== ================= ======
   Presentation LUT Shape (2050,0020 CS IDENTITY ALWAYS            AUTO
   ====================== ========== == ======== ================= ======

.. table:: SOP Common Module of Created GSPS SOP Instances

   +------------+------------+----+------------+------------+--------+
   | Attribute  | Tag        | VR | Value      | Presence   | Source |
   | Name       |            |    |            | of Value   |        |
   +============+============+====+============+============+========+
   | Specific   | (          | CS | "ISO_IR    | ALWAYS     | CONFIG |
   | Character  | 0008,0005) |    | 100" or    |            |        |
   | Set        |            |    | "ISO_IR    |            |        |
   |            |            |    | 144"       |            |        |
   +------------+------------+----+------------+------------+--------+
   | SOP Class  | (          | UI | 1.2.840.   | ALWAYS     | AUTO   |
   | UID        | 0008,0016) |    | 10008.5.1. |            |        |
   |            |            |    | 4.1.1.11.1 |            |        |
   +------------+------------+----+------------+------------+--------+
   | SOP        | (          | UI | Generated  | ALWAYS     | AUTO   |
   | Instance   | 0008,0018) |    | by device  |            |        |
   | UID        |            |    |            |            |        |
   +------------+------------+----+------------+------------+--------+

.. _sect_B.8.1.2:

Used Fields in Received IOD By Application
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The EXAMPLE-INTEGRATED-MODALITY storage application does not receive SOP
Instances. The usage of attributes received via Modality Worklist is
described in `SOP Specific Conformance for Modality
Worklist <#sect_B.4.2.2.3.1.3>`__.

.. _sect_B.8.1.3:

Attribute Mapping
^^^^^^^^^^^^^^^^^

The relationships between attributes received via Modality Worklist,
stored in acquired images and communicated via MPPS are summarized in
`table_title <#table_B.8.1-31>`__. The format and conventions used in
DICOM `table_title <#table_B.8.1-31>`__ are the same as the
corresponding table in .

.. table:: Attribute Mapping Between Modality Worklist, Image and MPPS

   +----------------------+----------------------+----------------------+
   | Modality Worklist    | Image IOD            | MPPS IOD             |
   +======================+======================+======================+
   | Patient Name         | Patient Name         | Patient Name         |
   +----------------------+----------------------+----------------------+
   | Patient ID           | Patient ID           | Patient ID           |
   +----------------------+----------------------+----------------------+
   | Patient's Birth Date | Patient's Birth Date | Patient's Birth Date |
   +----------------------+----------------------+----------------------+
   | Patient's Sex        | Patient's Sex        | Patient's Sex        |
   +----------------------+----------------------+----------------------+
   | Patient's Weight     | Patient's Weight     |                      |
   +----------------------+----------------------+----------------------+
   | Referring            | Referring            |                      |
   | Physician's Name     | Physician's Name     |                      |
   +----------------------+----------------------+----------------------+
   | ----                 | ----                 | Scheduled Step       |
   |                      |                      | Attributes Sequence  |
   +----------------------+----------------------+----------------------+
   | Study Instance UID   | Study Instance UID   | >Study Instance UID  |
   +----------------------+----------------------+----------------------+
   | Referenced Study     | Referenced Study     | >Referenced Study    |
   | Sequence             | Sequence             | Sequence             |
   +----------------------+----------------------+----------------------+
   | Accession Number     | Accession Number     | >Accession Number    |
   +----------------------+----------------------+----------------------+
   | ----                 | Request Attributes   | ----                 |
   |                      | Sequence             |                      |
   +----------------------+----------------------+----------------------+
   | Requested Procedure  | >Requested Procedure | >Requested Procedure |
   | ID                   | ID                   | ID                   |
   +----------------------+----------------------+----------------------+
   | Requested Procedure  |                      | >Requested Procedure |
   | Description          |                      | Description          |
   +----------------------+----------------------+----------------------+
   | Scheduled Procedure  | >Scheduled Procedure | >Scheduled Procedure |
   | Step ID              | Step ID              | Step ID              |
   +----------------------+----------------------+----------------------+
   | Scheduled Procedure  | >Scheduled Procedure | >Scheduled Procedure |
   | Step Description     | Step Description     | Step Description     |
   +----------------------+----------------------+----------------------+
   | Scheduled Protocol   | >Scheduled Protocol  | ----                 |
   | Code Sequence        | Code Sequence        |                      |
   +----------------------+----------------------+----------------------+
   | ----                 | Performed Protocol   | Performed Protocol   |
   |                      | Code Sequence        | Code Sequence        |
   +----------------------+----------------------+----------------------+
   | ----                 | Study ID             | Study ID             |
   +----------------------+----------------------+----------------------+
   | ----                 | Performed Procedure  | Performed Procedure  |
   |                      | Step ID              | Step ID              |
   +----------------------+----------------------+----------------------+
   | ----                 | Performed Procedure  | Performed Procedure  |
   |                      | Step Start Date      | Step Start Date      |
   +----------------------+----------------------+----------------------+
   | ----                 | Performed Procedure  | Performed Procedure  |
   |                      | Step Start Time      | Step Start Time      |
   +----------------------+----------------------+----------------------+
   | ----                 | Performed Procedure  | Performed Procedure  |
   |                      | Step Description     | Step Description     |
   +----------------------+----------------------+----------------------+
   | ----                 | Comments on the      | Comments on the      |
   |                      | Performed Procedure  | Performed Procedure  |
   |                      | Step                 | Step                 |
   +----------------------+----------------------+----------------------+
   | ----                 | ----                 | Performed Series     |
   |                      |                      | Sequence             |
   +----------------------+----------------------+----------------------+
   | Scheduled Performing | Performing           | >Performing          |
   | Physician's Name     | Physician's Name     | Physician's Name     |
   +----------------------+----------------------+----------------------+
   | Requested Procedure  | ----                 | Procedure Code       |
   | Code Sequence        |                      | Sequence             |
   +----------------------+----------------------+----------------------+
   | ----                 | Referenced Study     | ----                 |
   |                      | Component Sequence   |                      |
   +----------------------+----------------------+----------------------+
   | ----                 | >Referenced SOP      | SOP Class UID        |
   |                      | Class UID            |                      |
   +----------------------+----------------------+----------------------+
   | ----                 | >Referenced SOP      | SOP Instance UID     |
   |                      | Instance UID         |                      |
   +----------------------+----------------------+----------------------+
   | ----                 | Protocol Name        | Protocol Name        |
   +----------------------+----------------------+----------------------+

.. _sect_B.8.1.4:

Coerced/Modified Fields
^^^^^^^^^^^^^^^^^^^^^^^

The Modality Worklist AE will truncate attribute values received in the
response to a Modality Worklist Query if the value length is longer than
the maximum length permitted by the attribute's VR.

.. _sect_B.8.2:

Data Dictionary of Private Attributes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Private Attributes added to created SOP Instances are listed in the
Table below. EXAMPLE-INTEGRATED-MODALITY reserves blocks of private
attributes in groups 0009, 0019 and 0029. Further details on usage of
these private attributes are contained in `IOD
Contents <#sect_B.8.1>`__.

.. table:: Data Dictionary of Private Attributes

   +-------------+-------------------+----+----+-------------------+
   | Tag         | Attribute Name    | VR | VM | Attribute         |
   |             |                   |    |    | Description       |
   +=============+===================+====+====+===================+
   | (0009,00xx) | Private Creator   | LO | 1  | EXINTMODMAKER     |
   +-------------+-------------------+----+----+-------------------+
   | (0009,xx01) | Equipment UID     | UI | 1  |                   |
   +-------------+-------------------+----+----+-------------------+
   | (0009,xx02) | Service UID       | UI | 1  |                   |
   +-------------+-------------------+----+----+-------------------+
   | (0019,00xx) | Private Creator   | LO | 1  | EXINTMODMAKER     |
   +-------------+-------------------+----+----+-------------------+
   | (0019,xx10) | Edge Enhancement  | IS | 1  |                   |
   |             | Percent           |    |    |                   |
   +-------------+-------------------+----+----+-------------------+
   | (0019,xx20) | Landmark          | IS | 1  |                   |
   +-------------+-------------------+----+----+-------------------+
   | (0019,xx30) | Pixel Shift       | DS | 1  |                   |
   |             | Horizontal        |    |    |                   |
   +-------------+-------------------+----+----+-------------------+
   | (0019,xx40) | Pixel Shift       | DS | 1  |                   |
   |             | Vertical          |    |    |                   |
   +-------------+-------------------+----+----+-------------------+
   | (0029,00xx) | Private Creator   | LO | 1  | EXINTMODMAKER     |
   +-------------+-------------------+----+----+-------------------+
   | (0029,xx40) | Application       | SQ | 1  |                   |
   |             | Header Sequence   |    |    |                   |
   +-------------+-------------------+----+----+-------------------+
   | (0029,xx41) | Application       | CS | 1  |                   |
   |             | Header Type       |    |    |                   |
   +-------------+-------------------+----+----+-------------------+
   | (0029,xx42) | Application       | LO | 1  |                   |
   |             | Header ID         |    |    |                   |
   +-------------+-------------------+----+----+-------------------+
   | (0029,xx43) | Application       | LO | 1  |                   |
   |             | Header Version    |    |    |                   |
   +-------------+-------------------+----+----+-------------------+
   | (0029,xx44) | Application       | OB | 1  |                   |
   |             | Header Data       |    |    |                   |
   +-------------+-------------------+----+----+-------------------+
   | (0029,xx50) | Workflow Control  | LO | 8  |                   |
   |             | Flags             |    |    |                   |
   +-------------+-------------------+----+----+-------------------+
   | (0029,xx51) | Archive           | CS | 1  |                   |
   |             | Management Flag - |    |    |                   |
   |             | Keep Online       |    |    |                   |
   +-------------+-------------------+----+----+-------------------+
   | (0029,xx52) | Archive           | CS | 1  |                   |
   |             | Management Flag - |    |    |                   |
   |             | Do Not Archive    |    |    |                   |
   +-------------+-------------------+----+----+-------------------+

.. _sect_B.8.3:

Coded Terminology and Templates
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Workflow AE is capable of supporting arbitrary coding schemes for
Procedure and Protocol Codes. The contents of Requested Procedure Code
Sequence (0032,1064) and Scheduled Protocol Code Sequence (0040,0008)
supplied in Worklist Items will be mapped to Image IOD and MPPS
attributes as described in `table_title <#table_B.8.1-31>`__. During
installation, a service technician will establish a mapping between the
site-specific codes and the Protocol Names used internally to identify
acquisition protocols.

The contents of Anatomic Region Sequence (0008,2218) in generated images
will be filled with an anatomic code selected by the user from a
catalog. The default catalog of anatomic codes corresponds to but can be
extended using the Service/Installation Tool.

The contents of Performed Procedure Step Discontinuation Reason Code
Sequence (0040,0281) for a discontinued MPPS will be filled with a code
selected by the user from a fixed list corresponding to .

.. _sect_B.8.4:

Grayscale Image Consistency
~~~~~~~~~~~~~~~~~~~~~~~~~~~

The high resolution display monitor attached to
EXAMPLE­INTEGRATED-MODALITY can be calibrated according to the Grayscale
Standard Display Function (GSDF). The Service/Installation Tool is used
together with a luminance meter to measure the Characteristic Curve of
the display system and the current ambient light. See the
EXAMPLE-INTEGRATED-MODALITY Service Manual for details on the
calibration procedure and supported calibration hardware. The result of
the calibration procedure is a Monitor Correction LUT that will be
active within the display subsystem after a system reboot.

.. _sect_B.8.5:

Standard Extended / Specialized / Private SOP Classes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

No Specialized or Private SOP Classes are supported.

.. _sect_B.8.5.1:

X-Ray Radiofluoroscopic Image Storage SOP Class
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The X-Ray Radiofluoroscopic Image Storage SOP Class is extended to
create a Standard Extended SOP Class by addition of standard and private
attributes to the created SOP Instances as documented in `IOD
Contents <#sect_B.8.1>`__.

.. _sect_B.8.6:

Private Transfer Syntaxes
~~~~~~~~~~~~~~~~~~~~~~~~~

No Private Transfer Syntaxes are supported.

