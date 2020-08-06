.. _chapter_C:

Conformance Statement Sample DICOMRis Interface (Informative)
=============================================================

Disclaimer:

This document is an example DICOM Conformance Statement for a product
that supports DICOM SOP Classes frequently associated with a Radiology
Information System or RIS. The product whose conformance is being
documented, DICOMRis, and the manufacturer, Hospital Systems, are
fictional.

As stated in the annex title, this document is truly informative, and
not normative. A conformance statement of an actual product might
implement additional services and options as appropriate for its
specific purpose. In addition, an actual product might implement the
services described in a different manner and, for example, with
different characteristics and/or sequencing of activities. In other
words, this conformance statement example does not intend to standardize
a particular manner that a product might implement DICOM functionality.

.. _sect_C.0:

Cover Page
----------

Company Name: EXAMPLE RIS Products.

Product Name: SAMPLE DICOMRis Interface

Version: 1.0-rev. A.1

Internal document number: 4226-xxx-yyy-zzz rev 1

Date: YYYYMMDD

.. _sect_C.1:

Conformance Statement Overview
------------------------------

Hospital Systems' DICOMRis is a suite of applications that implement a
full-featured Radiology Information System (RIS). DICOMRis includes
features typically associated with a RIS, including interfaces to
various Hospital Information Systems, Patient Tracking, Results
Reporting, Film Tracking, Management Reporting, PACS Integration, etc.
The DICOMRis GUI-based client application, RisView, runs on a Windows
95/98/NT platform; the server platform is Digital Unix.

As part of PACS Integration DICOMRis supports several DICOM Service
Classes, using DICOMTool's DICOM Toolkit, to provide the following
capabilities:

Allowing Modalities to query for worklists of procedures to be performed
and for patient and procedure demographics. DICOMRis processes these
queries by directly accessing the DICOMRis database, which is
automatically updated with appropriate data through the normal
operations of the RIS.

Updating the DICOMRis database in response to Procedure Step
transactions initiated by Modalities as they perform examinations.
Relevant data contained in these transactions may be viewed using
RisView.

.. table:: Network Services

   +----------------------+----------------------+----------------------+
   | SOP Classes          | User of Service      | Provider of Service  |
   |                      | (SCU)                | (SCP)                |
   +======================+======================+======================+
   | Workflow Management  |                      |                      |
   +----------------------+----------------------+----------------------+
   | Modality Worklist    | No                   | Yes                  |
   +----------------------+----------------------+----------------------+
   | Modality Performed   | No                   | Yes                  |
   | Procedure Step       |                      |                      |
   +----------------------+----------------------+----------------------+

.. _sect_C.2:

Table of Contents
-----------------

A table of contents shall be provided to assist readers in easily
finding the needed information.

.. _sect_C.3:

Introduction
------------

.. _sect_C.3.1:

Revision History
~~~~~~~~~~~~~~~~

.. table:: Revision History

   ================ ================ =============== ======================
   Document Version Revision Date    Revision Author Revision Description
   ================ ================ =============== ======================
   1.1              October 30, 2003 WG 6            Version for Final Text
   1.2              August 30, 2007  WG 6            Revised Introduction
   ================ ================ =============== ======================

.. _sect_C.3.2:

Audience, Remarks, Terms and Definitions, Basics of DICOM Communication, Abbreviations, References
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

*See example text in*\ `Introduction <#sect_A.3>`__\ *.*

.. _sect_C.3.3:

Additional References for This Example
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

IHE Radiology Technical Framework, Revision 7.0, ACC/HIMSS/RSNA, 2006.

Logical Observation Identifier Names and Codes (LOINC). Regenstrief
Institute. Indianapolis. 2018.\ http://loinc.org/

.. _sect_C.3.4:

Additional Remarks and Definitions for This Example
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This document is a sample DICOM Conformance Statement created for DICOM
. It is to be used solely as an example to illustrate how to create a
DICOM Conformance Statement for a departmental information system
supporting DICOM Modality Worklist and Modality Performed Procedure Step
Services. The subject of the document, DICOMRis, is a fictional product.

DICOMRis Database The database that indexes procedures, orders and
patients

DICOMSRV DICOM MWL and MPPS application

RisView DICOMRis' GUI-based application providing views into the
DICOMRis' Database, reporting function, etc.

.. _sect_C.4:

Networking
----------

.. _sect_C.4.1:

Implementation Model
~~~~~~~~~~~~~~~~~~~~

.. _sect_C.4.1.1:

Application Data Flow
^^^^^^^^^^^^^^^^^^^^^

The DICOMRis DICOMSRV application provides access to Scheduled Procedure
information, supports updating of the RIS database as procedures are
performed. The various flows in the diagram above are described as
follows

DICOMSRV accepts associations for Verification from Verification SCUs
and responds automatically with Success status

DICOMSRV accepts Association Requests for Modality Worklist from MWL
SCUs and responds to queries from these SCUs. When a query is received
DICOMSRV engages in local real-world activity Scheduled Procedure
Queries. This results in a set of matching responses that DICOMSRV
returns to the MWL SCU.

DICOMSRV accepts Association Requests for Modality Performed Procedure
Step from MPPS SCUs and responds to N-CREATE and N-SET Requests from
these SCUs. When an N-CREATE or N-SET is received DICOMSRV engages in
local real-world activity Update Procedure. This results in updates to
the DICOMRis Database per the contents of the received message. DICOMSRV
then returns N-SET or N-CREATE status to the MPPS SCU.

.. _sect_C.4.1.2:

Functional Definition of AEs
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. _sect_C.4.1.2.1:

Functional Definition of DICOMSRV Application Entity
''''''''''''''''''''''''''''''''''''''''''''''''''''

DICOMSRV is a background process running on a Unix server. A single
instance of DICOMSRV is started at System boot but multiple instances
may be running at any one time as a result of forking of additional
processes. The application may be started/restarted interactively via a
utility. In addition, there is a monitoring process that may be
configured to restart the application automatically should it crash.
Events are logged to application-specific log files with a time stamp.
Multiple logging levels are supported. At the lowest logging level the
following are logged:

-  The AE Title of the remote AE when the Association is created

-  The status of each DICOM Service Request

-  Any updates to the DICOMRis Database

Higher levels of logging can be configured to cause dumping of the
contents of DICOM Service and Association messages..

DICOMSRV will listen for connection requests at the Presentation Address
configured for its AE Title. This application is an implementation of a
concurrent server; it forks a new process for each connection request it
receives. Each forked process exists for the life of a single
association and then exits. DICOMSRV will accept Presentation Contexts
for the Modality Worklist, Modality Performed Procedure Step and
Verification SOP Classes. Validation of DICOM Service Request messages
is configurable using command-line parameters and may return Failure
status in the event of an invalid Service Request according to the
specifications in the standard. Upon receipt of a Verification Request
DICOMSRV will respond with a successful Verification response. When a
MWL query is received DICOMSRV will query the DICOMRis database for a
list of Scheduled Procedure Steps matching the query and will return a
pending C-Find response for each match. Before DICOMRis can include
patient and order information in response to a Modality Worklist query,
patients must be registered and there must be orders for those patients
in the DICOMRis database.. Registration and order information is
typically interfaced to DICOMRis from a HIS but can also be entered
directly into DICOMRis using DICOMRis's registration and order entry
applications. Reception of an MPPS N-Create or N-Set Request may result
in updates to various tables in the DICOMRis database and may result in
changes to the procedure state of the Requested Procedure(s) referenced
within the message. If an MPPS message containing non-matching
demographic data is received, this will be logged, an exception document
generated and an entry added to an exception table in the database.

.. _sect_C.4.1.3:

Sequencing of Real World Activities
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Under normal circumstances the sequencing depicted above applies:

1. The Modality queries for a worklist of Scheduled Procedure Steps

2. DICOMSRV searches its database and returns matches to the query

3. The Modality begins performance of a Procedure Step and sends the
   MPPS N-CREATE

4. The Modality completes or discontinues the procedure and sends the
   MPPS N-SET with status of COMPLETE or DISCONTINUED

The workflow above is not the only one possible. For example, in a
Trauma or unscheduled flow there may be no worklist query prior to the
performance of the procedure and the sending of MPPS messages. The flow
would also be altered if the Modality did not support both Modality
Worklist and MPPS. The Description and Sequencing of Activities and the
SOP Specific Conformance sections below for the respective Real World
Activities provide additional detail

.. _sect_C.4.2:

AE Specifications
~~~~~~~~~~~~~~~~~

.. _sect_C.4.2.1:

DICOMSRV AE Specification
^^^^^^^^^^^^^^^^^^^^^^^^^

This application provides Standard Conformance to the following DICOM
SOP Classes:

.. _sect_C.4.2.1.1:

SOP Classes
'''''''''''

.. table:: SOP Classes for AE DICOMSRV

   ================================= ======================= === ===
   SOP Class Name                    SOP Class UID           SCU SCP
   ================================= ======================= === ===
   Verification                      1.2.840.10008.1.1       No  Yes
   Modality Worklist                 1.2.840.10008.5.1.4.31  No  Yes
   Modality Performed Procedure Step 1.2.840.10008.3.1.2.3.3 No  Yes
   ================================= ======================= === ===

.. _sect_C.4.2.1.2:

Association Policies
''''''''''''''''''''

.. _sect_C.4.2.1.2.1:

General
       

The Application Context Name for DICOM is the only Application Context
proposed.

.. table:: DICOM Application Context

   ======================== =====================
   Application Context Name 1.2.840.10008.3.1.1.1
   ======================== =====================

.. _sect_C.4.2.1.2.2:

Number of Associations
                      

DICOMSRV will support as many simultaneous associations as SCP as are
requested by Workflow SCUs up to a configurable maximum. DICOMSRV limits
the number of concurrent associations to a given Workflow SCU as
described below.

.. table:: Number of Associations as an SCP for AE DICOMSRV

   +----------------------------------+----------------------------------+
   | Maximum number of simultaneous   | Configurable value. Maximum of 3 |
   | associations                     | simultaneous associations to a   |
   |                                  | given SCU                        |
   +----------------------------------+----------------------------------+

.. _sect_C.4.2.1.2.3:

Asynchronous Nature
                   

Asynchronous communication (multiple outstanding transactions over a
single association) is not supported.

.. _sect_C.4.2.1.2.4:

Implementation Identifying Information
                                      

.. table:: DICOM Implementation Class and Version for DICOMSRV

   =========================== ==========================
   Implementation Class UID    xxxxxxx.yyy.etc.ad.inf.usw
   Implementation Version Name DICOMRis_260
   =========================== ==========================

.. _sect_C.4.2.1.3:

Association Initiation Policy
'''''''''''''''''''''''''''''

DICOMSRV does not initiate Associations.

.. _sect_C.4.2.1.4:

Association Acceptance Policy
'''''''''''''''''''''''''''''

DICOMSRV will accept associations for the MWL, MPPS and Verification SOP
Classes as an SCP. The job runs in the background and forks a new
process for each connection request from a Remote AE

.. _sect_C.4.2.1.4.1:

Activity - Configured AE Requests MWL Query
                                           

.. _sect_C.4.2.1.4.1.1:

Description and Sequencing of Activities
                                        

When Modality Worklist SCUs query DICOMSRV the queries run against the
Scheduled Procedure Step Worklist (referred to hereafter as the 'SPS
Worklist' or 'Worklist') in the DICOMRis database. There is a
configurable mapping between the Universal Service ID contained in the
HL7 Order messages (see `table_title <#table_C.8.1-4>`__) and one or
more Requested Procedures within the DICOMRis database. A Requested
Procedure may, in turn, map to 1 or more Scheduled Procedure Steps
though the relation is usually 1-to-1. This mapping is also
site-configurable. The relation between Accession Number (0008,0050) and
Requested Procedure ID (0040,1001) is 1-to-1 within DICOMRis and these
attributes have the same value in all MWL responses. Scheduled Procedure
Step entries are added and removed from the Worklist as follows:

-  Add Scheduled Procedure Step Entries Normal Pathway - As orders are
   received from the HIS via HL7 or entered using DICOMRis' Ordering and
   Scheduling application, additions are made to the SPS Worklist in the
   DICOMRis database per the mapping specified above.

-  Add Scheduled Procedure Step Entries Exception Pathway - Users can
   interactively create additional Scheduled Procedure Step entries for
   a given Requested Procedure using the Procedure Update application.
   It may be necessary to create additional entries under certain
   conditions such as when it is discovered that a procedure must be
   redone after having previously been marked as completed. This does
   not apply to canceled procedures

-  Remove Scheduled Procedure Step Entries Normal Pathway - An SPS entry
   is removed from the SPS Worklist under the following circumstances:

-  As mentioned previously, DICOMRis supports common RIS function to set
   the state of the procedure as it progresses from being ordered to
   being resulted and signed. Setting the procedure state may be
   initiated interactively via the Procedure Update application or as a
   result of various events. An entry in the SPS Worklist is removed
   when the Requested Procedure that is the parent of the SPS is set to
   a configured status. This configuration is system-wide applying
   equally to all procedures.

-  If configured to change the state of a Requested Procedure on receipt
   of an MPPS N-CREATE or N-SET referencing the procedure then the
   change in state may result in removal of SPS entries related to the
   procedure as described above

-  Remove Entries Exception Pathway - When a procedure is canceled all
   SPS entries related to that procedure are removed from the Worklist.

Remove Entries Maintenance Pathway - SPS entries that are still in the
Worklist a configurable time after their scheduled start date/time will
be removed by a day-end maintenance job.

In the table below the following applies:

-  To cause a given action to occur, MPPS messages must reference the
   parent Requested Procedure related to the SPS entry and applicable
   configuration must be in place.

.. table:: Scheduled Procedure Step Entry Actions Table

   +----------------------------------+----------------------------------+
   | Events                           | Scheduled Procedure Step Entry   |
   |                                  | Actions                          |
   +==================================+==================================+
   | Order received from HIS or       | Add one or more Entries to       |
   | entered using DICOMRis           | Worklist                         |
   | application                      |                                  |
   +----------------------------------+----------------------------------+
   | User adds SPS entry              | Add Entry to Worklist            |
   | interactively                    |                                  |
   +----------------------------------+----------------------------------+
   | MPPS message received that       | Remove Entry from Worklist       |
   | changes procedure state of       |                                  |
   | parent procedure to status       |                                  |
   | configured for removal of child  |                                  |
   | SPS entry from Worklist          |                                  |
   +----------------------------------+----------------------------------+
   | Current time exceeds SPS         | Remove Entry from Worklist       |
   | scheduled time by a Worklist     |                                  |
   | configured time interval         |                                  |
   +----------------------------------+----------------------------------+
   | Parent procedure canceled        | Remove one or more Entries from  |
   |                                  | Worklist                         |
   +----------------------------------+----------------------------------+
   | Parent procedure set to a state  | Remove one or more Entries from  |
   | that causes removal of child SPS | Worklist                         |
   | entries from Worklist            |                                  |
   +----------------------------------+----------------------------------+

The figure above is a possible sequence of messages between a Modality
Worklist SCU and DICOMSRV.

1. The Modality opens an Association with DICOMSRV for the purpose of
   querying for a Modality Worklist

2. The Modality sends an MWL C-FIND query to DICOMSRV

3. DICOMSRV queries its database using the attributes from the C-FIND
   Request and returns 0 to N C-FIND responses depending on matches
   returned from the database. DICOMSRV checks for a C-FIND Cancel
   Request after a configured number of responses are sent. If a Cancel
   is received then no further Pending responses are sent.

4. DICOMSRV sends the final C-FIND response

5. The Modality closes the Association

.. _sect_C.4.2.1.4.1.2:

Accepted Presentation Contexts
                              

.. table:: Acceptable Presentation Contexts for AE DICOMSRV and
Real-World Activity 'Configured AE Requests MWL Query'

   +------------+------------+------------+------------+-----+------+
   | Pr         |            |            |            |     |      |
   | esentation |            |            |            |     |      |
   | Context    |            |            |            |     |      |
   | Table      |            |            |            |     |      |
   +============+============+============+============+=====+======+
   | Modality   | 1.         | Implicit   | 1.2.840    | SCP | None |
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

.. _sect_C.4.2.1.4.1.2.1:

Presentation Context Acceptance Criterion
                                         

Depending on configuration, DICOMSRV may or may not accept multiple
Presentation Contexts containing the same Abstract Syntax.

.. _sect_C.4.2.1.4.1.2.2:

Transfer Syntax Selection Policy
                                

Transfer Syntaxes in addition to the default Implicit VR Little Endian
may be configured for a given Abstract Syntax. DICOMSRV's preferred
Transfer Syntax is Explicit VR Little Endian and this will be selected
if offered.

.. _sect_C.4.2.1.4.1.3:

SOP Specific Conformance for Modality Worklist SOP Class
                                                        

DICOMSRV does not support matching on any optional matching key
attributes.

DICOMSRV supports case-insensitive matching on the following Person Name
Value Representation elements:

Patient Name (0010,0010)

DICOMSRV supports optional return key attributes as described in the
table below.

.. table:: Modality Worklist Optional Return Keys Supported

   +--------------------------+-------------+--------------------------+
   | Description/Module       | Tag         | Remark                   |
   +==========================+=============+==========================+
   | Scheduled Procedure Step |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Scheduled Protocol Code | (0040,0008) |                          |
   | Sequence                 |             |                          |
   +--------------------------+-------------+--------------------------+
   | >>Code Meaning           | (0008,0104) |                          |
   +--------------------------+-------------+--------------------------+
   | >Comments on the         | (0040,0400) | This attribute, if       |
   | Scheduled Procedure Step |             | valued, will contain     |
   |                          |             | details of the protocol  |
   |                          |             | to be used in carrying   |
   |                          |             | out this step. The       |
   |                          |             | attribute could contain  |
   |                          |             | a full description of    |
   |                          |             | the protocol or simply   |
   |                          |             | indicate modifications   |
   |                          |             | to the protocol          |
   |                          |             | designated by the        |
   |                          |             | Scheduled Protocol Code  |
   |                          |             | Sequence                 |
   +--------------------------+-------------+--------------------------+
   | >Requested Contrast      | (0032,1070) |                          |
   | Agent                    |             |                          |
   +--------------------------+-------------+--------------------------+
   | Requested Procedure      |             |                          |
   +--------------------------+-------------+--------------------------+
   | Reason for the Requested | (0040,1002) |                          |
   | Procedure                |             |                          |
   +--------------------------+-------------+--------------------------+
   | Requested Procedure      | (0040,1400) |                          |
   | Comments                 |             |                          |
   +--------------------------+-------------+--------------------------+
   | Imaging Service Request  |             |                          |
   +--------------------------+-------------+--------------------------+
   | Reason for the Imaging   | (0040,2001) |                          |
   | Service Request          |             |                          |
   +--------------------------+-------------+--------------------------+
   | Imaging Service Request  | (0040,2400) |                          |
   | Comments                 |             |                          |
   +--------------------------+-------------+--------------------------+
   | Requesting Service       | (0032,1033) |                          |
   +--------------------------+-------------+--------------------------+
   | Issuing Date of Imaging  | (0040,2004) |                          |
   | Service Request          |             |                          |
   +--------------------------+-------------+--------------------------+
   | Issuing Time of Imaging  | (0040,2005) |                          |
   | Service Request          |             |                          |
   +--------------------------+-------------+--------------------------+
   | Placer Order Number /    | (0040,2016) |                          |
   | Imaging Service Request  |             |                          |
   +--------------------------+-------------+--------------------------+
   | Filler Order Number /    | (0040,2017) |                          |
   | Imaging Service Request  |             |                          |
   +--------------------------+-------------+--------------------------+
   | Order entered by         | (0040,2008) |                          |
   +--------------------------+-------------+--------------------------+
   | Order Enterer's Location | (0040,2009) |                          |
   +--------------------------+-------------+--------------------------+
   | Visit Status             |             |                          |
   +--------------------------+-------------+--------------------------+
   | Patient's Institution    | (0038,0400) |                          |
   | Residence                |             |                          |
   +--------------------------+-------------+--------------------------+
   | Visit Admission          |             |                          |
   +--------------------------+-------------+--------------------------+
   | Referring Physician's    | (0008,0090) |                          |
   +--------------------------+-------------+--------------------------+
   | Referring Physician's    | (0008,0092) |                          |
   | Address                  |             |                          |
   +--------------------------+-------------+--------------------------+
   | Referring Physician's    | (0008,0094) |                          |
   | Phone Numbers            |             |                          |
   +--------------------------+-------------+--------------------------+
   | Admitting Diagnosis      | (0008,1080) |                          |
   | Description              |             |                          |
   +--------------------------+-------------+--------------------------+
   | Admitting Date           | (0038,0020) |                          |
   +--------------------------+-------------+--------------------------+
   | Admitting Time           | (0038,0021) |                          |
   +--------------------------+-------------+--------------------------+
   | Patient Identification   |             |                          |
   +--------------------------+-------------+--------------------------+
   | Issuer of Patient ID     | (0010,0021) |                          |
   +--------------------------+-------------+--------------------------+
   | Patient Demographic      |             |                          |
   +--------------------------+-------------+--------------------------+
   | Occupation               | (0010,2180) |                          |
   +--------------------------+-------------+--------------------------+
   | Patient's Address        | (0010,1040) |                          |
   +--------------------------+-------------+--------------------------+
   | Country of Residence     | (0010,2150) |                          |
   +--------------------------+-------------+--------------------------+
   | Patient's Telephone      | (0010,2154) |                          |
   | Numbers                  |             |                          |
   +--------------------------+-------------+--------------------------+
   | Ethnic Group             | (0010,2160) |                          |
   +--------------------------+-------------+--------------------------+
   | Patient's Religious      | (0010,21F0) |                          |
   | Preference               |             |                          |
   +--------------------------+-------------+--------------------------+
   | Patient Comments         | (0010,4000) |                          |
   +--------------------------+-------------+--------------------------+
   | Patient Medical          |             |                          |
   +--------------------------+-------------+--------------------------+
   | Smoking Status           | (0010,21A0) |                          |
   +--------------------------+-------------+--------------------------+
   | Last Menstrual Date      | (0010,21D0) |                          |
   +--------------------------+-------------+--------------------------+

DICOMSRV returns C-FIND response statuses as specified below.

.. table:: MWL C-FIND Response Status Reasons

   +----------------+----------------+----------------+----------------+
   | Service Status | Further        | Error Code     | Reasons        |
   |                | Meaning        |                |                |
   +================+================+================+================+
   | Success        | Matching is    | 0000           | The response   |
   |                | complete       |                | status code    |
   |                |                |                | and meaning    |
   |                |                |                | are logged in  |
   |                |                |                | the job log    |
   |                |                |                | file.          |
   +----------------+----------------+----------------+----------------+
   | Failure        | Out of         | A700           | If the number  |
   |                | resources      |                | of matches     |
   |                |                |                | exceeds a      |
   |                |                |                | configurable   |
   |                |                |                | maximum this   |
   |                |                |                | error code is  |
   |                |                |                | returned. An   |
   |                |                |                | error comment  |
   |                |                |                | describing the |
   |                |                |                | error is also  |
   |                |                |                | returned. The  |
   |                |                |                | response       |
   |                |                |                | status code    |
   |                |                |                | and meaning    |
   |                |                |                | are logged in  |
   |                |                |                | the job log    |
   |                |                |                | file.          |
   +----------------+----------------+----------------+----------------+
   | Identifier     | A900           | This status is |                |
   | does not match |                | returned if    |                |
   | SOP class      |                | the C-FIND     |                |
   |                |                | request        |                |
   |                |                | specifies      |                |
   |                |                | query or       |                |
   |                |                | Return keys    |                |
   |                |                | that are not   |                |
   |                |                | specified as   |                |
   |                |                | part of the    |                |
   |                |                | Modality       |                |
   |                |                | Worklist       |                |
   |                |                | Information    |                |
   |                |                | Model - FIND   |                |
   |                |                | SOP Class. The |                |
   |                |                | response       |                |
   |                |                | status code    |                |
   |                |                | and meaning    |                |
   |                |                | are logged in  |                |
   |                |                | the job log    |                |
   |                |                | file.          |                |
   +----------------+----------------+----------------+----------------+
   | Unable to      | C001           | This status is |                |
   | process        |                | returned due   |                |
   |                |                | to internal    |                |
   |                |                | errors within  |                |
   |                |                | DICOMSRV such  |                |
   |                |                | as a           |                |
   |                |                | processing     |                |
   |                |                | failure        |                |
   |                |                | response on a  |                |
   |                |                | query of the   |                |
   |                |                | DICOMRis       |                |
   |                |                | database. The  |                |
   |                |                | response       |                |
   |                |                | status code    |                |
   |                |                | and meaning    |                |
   |                |                | are logged in  |                |
   |                |                | the job log    |                |
   |                |                | file.          |                |
   +----------------+----------------+----------------+----------------+
   | Canceled       | Matching       | FE00           | This status is |
   |                | terminated due |                | returned if a  |
   |                | to cancel      |                | Cancel Request |
   |                | request        |                | is received    |
   |                |                |                | from the SCU   |
   |                |                |                | during the     |
   |                |                |                | processing of  |
   |                |                |                | a Modality     |
   |                |                |                | Worklist       |
   |                |                |                | request. The   |
   |                |                |                | response       |
   |                |                |                | status code    |
   |                |                |                | and meaning    |
   |                |                |                | are logged in  |
   |                |                |                | the job log    |
   |                |                |                | file.          |
   +----------------+----------------+----------------+----------------+
   | Pending        | Matching is    | FF00           | The status is  |
   |                | continuing     |                | returned with  |
   |                |                |                | each matching  |
   |                |                |                | response. A    |
   |                |                |                | message is     |
   |                |                |                | logged for     |
   |                |                |                | each pending   |
   |                |                |                | response.      |
   +----------------+----------------+----------------+----------------+
   | Matching is    | FF01           | The status is  |                |
   | continuing -   |                | returned with  |                |
   | Current match  |                | each matching  |                |
   | is supplied    |                | response if    |                |
   | and any        |                | one or more    |                |
   | optional keys  |                | optional       |                |
   | were supported |                | matching or    |                |
   | in the same    |                | return keys    |                |
   | matter as      |                | are not        |                |
   | required keys  |                | supported for  |                |
   |                |                | existence. A   |                |
   |                |                | message is     |                |
   |                |                | logged for     |                |
   |                |                | each pending   |                |
   |                |                | response.      |                |
   +----------------+----------------+----------------+----------------+

.. _sect_C.4.2.1.4.2:

Activity - Configured AE Makes Procedure Step Request
                                                     

When a configured remote AE sends a conformant association request
including one of the Modality Performed Procedure Step Presentation
Contexts in the table below then DICOMSRV will accept the Association.

.. _sect_C.4.2.1.4.2.1:

Description and Sequencing of Activities
                                        

As mentioned above, DICOMSRV is started at system boot time and is thus
ready to process MPPS messages at any time thereafter. The sequencing
diagram below specifies a common flow of messages related to this
activity. Prior to this sequence of messages it is necessary that orders
have been received from the HIS interface or created via DICOMRis
Ordering and Scheduling application. Attributes from the orders and
created procedures, usually queried using MWL, will be included in the
MPPS messages the Modality sends to DICOMSRV. Key attributes in the MPPS
N-CREATE and N-SET, specified below, are extracted and matched against
values in the DICOMRis database. A match allows full update of all
applicable DICOMRis database tables.

The figure above is a possible sequence of messages and events for the
Configured AE Makes Procedure Step Request activity.

1. The Modality opens an Association to update DICOMSRV using MPPS

2. The Modality sends an N-CREATE Request to indicate that it is
   performing one or more Requested Procedures

3. The Modality performs all or part of the procedure(s)

4. DICOMSRV stores the MPPS and executes the matching algorithm
   described in the conformance section below. If a successful match is
   found, then updates to various tables per the N-CREATE are performed.
   See `table_title <#table_C.4.2-10>`__ for additional detail. In the
   matching case, the procedure state of the procedure(s) referenced in
   the MPPS is updated if so configured

5. The Modality sends an N-SET setting the status of the MPPS to
   COMPLETED

6. DICOMSRV stores the MPPS. If the N-CREATE for this step matched then
   updates are performed as specified in step 4

7. The Modality closes the Association

DICOMSRV also supports the 5 IHE Unidentified Patient Use Cases. Cases
1, 2 and 4 are transparent to the MPPS SCU and follow the normal flow.
In case 3, the patient upon whom a given procedure must be immediately
performed has been registered on the HIS and has a valid Patient ID but
has no order specifying the applicable procedure. DICOMSRV recognizes
this case when an MPPS N-CREATE is received with a matching Patient ID,
zero-length Accession Number (0008,0050) and Requested Procedure ID
(0040,1001). If the MPPS SCU is configured for support of IHE Trauma
cases, DICOMSRV will order a procedure corresponding to the code
contained in the Procedure Code Sequence (0008,1032), if this code is
recognized, or will order a default procedure based on configuration. If
the default procedure is ordered then a user may modify the procedure
using DICOMRis Ordering and Scheduling application.

In case 5, there is no existing registration or order for a patient on
whom a procedure must be immediately performed. Values are entered on
the Modality identifying the patient and procedure. DICOMSRV recognizes
this case when an MPPS N-CREATE is received containing a Patient ID
within a configured range. This range will never contain Patient IDs
created in the normal flow. If the MPPS SCU is configured for support of
IHE Trauma cases, DICOMSRV will register the patient with the Patient ID
provided and will order a procedure as described above.

.. _sect_C.4.2.1.4.2.2:

Accepted Presentation Contexts
                              

.. table:: Acceptable Presentation Contexts for AE DICOMSRV and
Real-World Activity "Configured AE Makes Procedure Step Request"

   +------------+------------+------------+------------+-----+------+
   | Pr         |            |            |            |     |      |
   | esentation |            |            |            |     |      |
   | Context    |            |            |            |     |      |
   | Table      |            |            |            |     |      |
   +============+============+============+============+=====+======+
   | Modality   | 1.2        | Implicit   | 1.2.840.1  | SCP | None |
   | Performed  | .840.10008 | VR Little  | 0008.1.2.1 |     |      |
   | Procedure  | .3.1.2.3.3 | Endian     |            |     |      |
   | Step SOP   |            |            |            |     |      |
   | Class      |            |            |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | Explicit   | 1.2.840.1  |            |            |     |      |
   | VR Little  | 0008.1.2.1 |            |            |     |      |
   | Endian     |            |            |            |     |      |
   +------------+------------+------------+------------+-----+------+

DICOMSRV's preferred Transfer Syntax is Explicit VR Little Endian and
this will be selected if offered.

.. _sect_C.4.2.1.4.2.3:

SOP Specific Conformance for MPPS SOP Class
                                           

The table below lists all Modality Performed Procedure Step attributes,
whether they may be created by N-CREATE and updated by N-SET and what
parts of the DICOMRis database they are used to update. All MPPS
messages and thus their attributes are stored for the configurable Purge
Period described below. The 'Database Updates' column considers updates
separate from the storage of MPPS messages. If no value is present this
indicates that there are is no update to the database associated with
the given element.

.. table:: Supported N-SET/N-CREATE Attributes for MPPS

   +----------------+-------------+----------+-------+----------------+
   | Attribute Name | Tag         | N-Create | N-Set | Database       |
   |                |             |          |       | Updates        |
   +================+=============+==========+=======+================+
   | SOP Common     |             |          |       |                |
   | Module         |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+
   | Specific       | (0008,0005) | Y        | N     |                |
   | Character Set  |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+
   | Performed      |             |          |       |                |
   | Procedure Step |             |          |       |                |
   | Relationship   |             |          |       |                |
   | Module         |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+
   | Scheduled Step | (0040,0270) | Y        | N     | Y              |
   | Attribute      |             |          |       |                |
   | Sequence       |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+
   | >Study         | (0020,000D) | Y        | N     | Overwrite      |
   | Instance UID   |             |          |       | existing value |
   |                |             |          |       | if different   |
   |                |             |          |       | from received  |
   |                |             |          |       | value          |
   +----------------+-------------+----------+-------+----------------+
   | >Referenced    | (0008,1110) | Y        | N     |                |
   | Study Sequence |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+
   | >>Referenced   | (0008,1150) | Y        | N     |                |
   | SOP Class UID  |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+
   | >>Referenced   | (0008,1155) | Y        | N     |                |
   | SOP Instance   |             |          |       |                |
   | UID            |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+
   | >Accession     | (0008,0050) | Y        | N     |                |
   | Number         |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+
   | >Placer Order  | (0040,2006) | Y        | N     |                |
   | Number/Imaging |             |          |       |                |
   | Service        |             |          |       |                |
   | Request        |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+
   | >Filler Order  | (0040,2007) | Y        | N     |                |
   | Number/Imaging |             |          |       |                |
   | Service        |             |          |       |                |
   | Request        |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+
   | >Requested     | (0040,1001) | Y        | N     |                |
   | Procedure ID   |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+
   | >Requested     | (0032,1060) | Y        | N     |                |
   | Procedure      |             |          |       |                |
   | Description    |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+
   | >Scheduled     | (0040,0009) | Y        | N     |                |
   | Procedure Step |             |          |       |                |
   | ID             |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+
   | >Scheduled     | (0040,0007) | Y        | N     |                |
   | Procedure Step |             |          |       |                |
   | Description    |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+
   | >Scheduled     | (0040,0008) | Y        | N     |                |
   | Protocol Code  |             |          |       |                |
   | Sequence       |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+
   | >>Code Value   | (0008,0100) | Y        | N     |                |
   +----------------+-------------+----------+-------+----------------+
   | >>Coding       | (0008,0102) | Y        | N     |                |
   | Scheme         |             |          |       |                |
   | designator     |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+
   | >>Code Meaning | (0008,0104) | Y        | N     |                |
   +----------------+-------------+----------+-------+----------------+
   | Patient Name   | (0010,0010) | Y        | N     |                |
   +----------------+-------------+----------+-------+----------------+
   | Patient ID     | (0010,0020) | Y        | N     |                |
   +----------------+-------------+----------+-------+----------------+
   | Patient's      | (0010,0030) | Y        | N     |                |
   | Birth Date     |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+
   | Patient's Sex  | (0010,0040) | Y        | N     |                |
   +----------------+-------------+----------+-------+----------------+
   | Referenced     | (0008,1120) | Y        | N     |                |
   | Patient        |             |          |       |                |
   | Sequence       |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+
   | >Referenced    | (0008,1150) | Y        | N     |                |
   | SOP Class UID  |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+
   | >Referenced    | (0008,1155) | Y        | N     |                |
   | SOP Instance   |             |          |       |                |
   | UID            |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+
   | Performed      |             |          |       |                |
   | Procedure Step |             |          |       |                |
   | Information    |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+
   | Performed      | (0040,0253) | Y        | N     |                |
   | Procedure Step |             |          |       |                |
   | ID             |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+
   | Performed      | (0040,0241) | Y        | N     |                |
   | Station AE     |             |          |       |                |
   | Title          |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+
   | Performed      | (0040,0242) | Y        | N     |                |
   | Station Name   |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+
   | Performed      | (0040,0243) | Y        | N     |                |
   | Location       |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+
   | Performed      | (0040,0244) | Y        | N     |                |
   | Procedure Step |             |          |       |                |
   | Start Date     |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+
   | Performed      | (0040,0245) | Y        | N     |                |
   | Procedure Step |             |          |       |                |
   | Start Time     |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+
   | Performed      | (0040,0252) | Y        | Y     |                |
   | Procedure Step |             |          |       |                |
   | Status         |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+
   | Performed      | (0040,0254) | Y        | Y     |                |
   | Procedure Step |             |          |       |                |
   | Description    |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+
   | Performed      | (0040,0255) | Y        | Y     |                |
   | Procedure Type |             |          |       |                |
   | Description    |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+
   | Procedure Code | (0008,1032) | Y        | Y     |                |
   | Sequence       |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+
   | >Code Value    | (0008,0100) | Y        | Y     |                |
   +----------------+-------------+----------+-------+----------------+
   | >Coding Scheme | (0008,0102) | Y        | Y     |                |
   | Designator     |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+
   | >Code Meaning  | (0008,0104) | Y        | Y     |                |
   +----------------+-------------+----------+-------+----------------+
   | Performed      | (0040,0250) | Y        | Y     |                |
   | Procedure Step |             |          |       |                |
   | End Date       |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+
   | Performed      | (0040,0251) | Y        | Y     |                |
   | Procedure Step |             |          |       |                |
   | End Time       |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+
   | Comments on    | (0040,0280) | Y        | Y     |                |
   | the Performed  |             |          |       |                |
   | Procedure Step |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+
   | Image          |             |          |       |                |
   | Acquisition    |             |          |       |                |
   | Results        |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+
   | Modality       | (0008,0060) | Y        | N     |                |
   +----------------+-------------+----------+-------+----------------+
   | Study ID       | (0020,0010) | Y        | N     |                |
   +----------------+-------------+----------+-------+----------------+
   | Performed      | (0040,0260) | Y        | Y     | If valued,     |
   | Protocol Code  |             |          |       | stored with    |
   | Sequence       |             |          |       | current and    |
   |                |             |          |       | historical     |
   |                |             |          |       | procedure      |
   |                |             |          |       | records        |
   +----------------+-------------+----------+-------+----------------+
   | >Code Value    | (0008,0100) | Y        | Y     |                |
   +----------------+-------------+----------+-------+----------------+
   | >Coding Scheme | (0008,0102) | Y        | Y     |                |
   | Designator     |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+
   | >Code Meaning  | (0008,0104) | Y        | Y     |                |
   +----------------+-------------+----------+-------+----------------+
   | Performed      | (0040,0340) | Y        | Y     | Y              |
   | Series         |             |          |       |                |
   | Sequence       |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+
   | >Performing    | (0008,1050) | Y        | Y     | Y              |
   | Physician's    |             |          |       |                |
   | Name           |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+
   | >Protocol Name | (0018,1030) | Y        | Y     | Stored with    |
   |                |             |          |       | current and    |
   |                |             |          |       | historical     |
   |                |             |          |       | tables         |
   +----------------+-------------+----------+-------+----------------+
   | >Operator's    | (0008,1070) | Y        | Y     | If automatic   |
   | Name           |             |          |       | setting of     |
   |                |             |          |       | procedure      |
   |                |             |          |       | states is      |
   |                |             |          |       | enabled,       |
   |                |             |          |       | stored in      |
   |                |             |          |       | current and    |
   |                |             |          |       | historical     |
   |                |             |          |       | procedure      |
   |                |             |          |       | tables to      |
   |                |             |          |       | indicate who   |
   |                |             |          |       | modified the   |
   |                |             |          |       | state of the   |
   |                |             |          |       | procedure      |
   +----------------+-------------+----------+-------+----------------+
   | >Series        | (0020,000E) | Y        | Y     |                |
   | Instance UID   |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+
   | >Series        | (0008,103E) | Y        | Y     |                |
   | Description    |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+
   | >Retrieve AE   | (0008,0054) | Y        | Y     |                |
   | Title          |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+
   | Referenced     | (0008,1140) | Y        | Y     |                |
   | Image Sequence |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+
   | >>Referenced   | (0008,1150) | Y        | Y     |                |
   | SOP Class UID  |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+
   | >>Referenced   | (0008,1155) | Y        | Y     |                |
   | SOP Instance   |             |          |       |                |
   | UID            |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+
   | >Referenced    | (0040,0220) | Y        | Y     |                |
   | Standalone SOP |             |          |       |                |
   | Instance       |             |          |       |                |
   | Sequence       |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+
   | >>Referenced   | (0008,1150) | Y        | Y     |                |
   | SOP Class UID  |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+
   | >>Referenced   | (0008,1155) | Y        | Y     |                |
   | SOP Instance   |             |          |       |                |
   | UID            |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+
   | Billing and    |             |          |       |                |
   | Material       |             |          |       |                |
   | Management     |             |          |       |                |
   | Code           |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+
   | Billing        |             |          |       |                |
   | Procedure Step |             |          |       |                |
   | Sequence       |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+
   | >Code Value    | (0008,0100) | Y        | Y     |                |
   +----------------+-------------+----------+-------+----------------+
   | >Coding Scheme | (0008,0102) | Y        | Y     |                |
   | Designator     |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+
   | >Code Meaning  | (0008,0104) | Y        | Y     |                |
   +----------------+-------------+----------+-------+----------------+
   | Film           | (0040,0321) | Y        | Y     |                |
   | Consumption    |             |          |       |                |
   | Sequence       |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+
   | > Number of    | (2100,0170) | Y        | Y     | Updates Supply |
   | Films          |             |          |       | and            |
   |                |             |          |       | Film-Procedure |
   |                |             |          |       | Tables         |
   +----------------+-------------+----------+-------+----------------+
   | > Medium Type  | (2000,0030) | Y        | Y     |                |
   +----------------+-------------+----------+-------+----------------+
   | > Film Size ID | (2010,0050) | Y        | Y     |                |
   +----------------+-------------+----------+-------+----------------+
   | Billing        | (0040,0384) | Y        | Y     |                |
   | Supplies and   |             |          |       |                |
   | Devices        |             |          |       |                |
   | Sequence       |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+
   | >Billing Item  | (0040,0296) | Y        | Y     |                |
   | Sequence       |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+
   | >>Code Value   | (0008,0100) | Y        | Y     | Updates Supply |
   |                |             |          |       | table if       |
   |                |             |          |       | Coding Scheme  |
   |                |             |          |       | Designator for |
   |                |             |          |       | Billing Item   |
   |                |             |          |       | Sequence is    |
   |                |             |          |       | D              |
   |                |             |          |       | ICOMRIS_SUPPLY |
   |                |             |          |       | and the Code   |
   |                |             |          |       | Value is a     |
   |                |             |          |       | value from     |
   |                |             |          |       | this Code Set  |
   +----------------+-------------+----------+-------+----------------+
   | >>Coding       | (0008,0102) | Y        | Y     |                |
   | Scheme         |             |          |       |                |
   | Designator     |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+
   | >>Code Meaning | (0008,0104) | Y        | Y     |                |
   +----------------+-------------+----------+-------+----------------+
   | >Quantity      | (0040,0293) | Y        | Y     |                |
   | Sequence       |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+
   | >>Quantity     | (0040,0294) | Y        | Y     |                |
   +----------------+-------------+----------+-------+----------------+
   | >>Measuring    | (0040,0295) | Y        | Y     |                |
   | Units Sequence |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+
   | >>>Code Value  | (0008,0100) | Y        | Y     |                |
   +----------------+-------------+----------+-------+----------------+
   | >>>Coding      | (0008,0102) | Y        | Y     |                |
   | Scheme         |             |          |       |                |
   | Designator     |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+
   | >>>Code        | (0008,0104) | Y        | Y     |                |
   | Meaning        |             |          |       |                |
   +----------------+-------------+----------+-------+----------------+

The list below details the behavior of DICOMSRV on occurrence of certain
MPPS events and with respect to the coercion of attributes and duration
of storage of MPPS messages:

-  Reception of a New MPPS Instance - The MPPS message is stored in the
   database. DICOMSRV will then extract the Patient ID (0020,0010) and
   as many Accession Numbers (0008,0050) as there are items in the
   Scheduled Step Attribute Sequence (0040,0270) from the N-CREATE and
   try to match these values against the Patient Medical Record Number
   and one or more Accession Numbers in the DICOMRis database. If a
   non-matching N-CREATE is received, it and any following N-SETs will
   be marked as exceptions. These exceptions can be reconciled using the
   RisView application. Otherwise, DICOMSRV will:

-  Update its database with values contained in the N-CREATE per table
   above.

-  Update the state of each referenced procedure if so configured.

-  Update of MPPS to 'DISCONTINUED' or 'COMPLETED' - The N-SET is stored
   in the database. If the preceding N-CREATE matched then the following
   is done:

-  The attribute values in the N-SET will be used to update the DICOMRis
   database per table above.

-  Update the state of each referenced procedure if so configured.

-  Coercion of Attributes - DICOMSRV will coerce attributes as specified
   in `table_title <#table_C.8.1-3>`__. This coercion may occur when a
   given step is set to the 'IN PROGRESS' or 'COMPLETED' or
   'DISCONTINUED'

-  Storage Duration for MPPS Messages - MPPS messages are purged from
   the DICOMRis database after a configurable period of time has elapsed
   since the step has been set to a final state or was last updated.

.. table:: MPPS N-CREATE/N-SET Response Status Reasons

   +----------------+----------------+----------------+----------------+
   | Service Status | Further        | Error Code     | Reasons        |
   |                | Meaning        |                |                |
   +================+================+================+================+
   | Success        | Successful     | 0000           | The response   |
   |                | completion of  |                | status code    |
   |                | the N-SET or   |                | and meaning    |
   |                | N-CREATE       |                | are logged in  |
   |                | Request        |                | the job log    |
   |                |                |                | file.          |
   +----------------+----------------+----------------+----------------+
   | Failure        | Processing     | 0110           | Internal error |
   |                | Failure        |                | within         |
   |                |                |                | DICOMSRV. The  |
   |                |                |                | response       |
   |                |                |                | status code    |
   |                |                |                | and meaning    |
   |                |                |                | are logged in  |
   |                |                |                | the job log    |
   |                |                |                | file.          |
   +----------------+----------------+----------------+----------------+
   | Duplicate SOP  | 0111           | This status is |                |
   | Instance       |                | returned when  |                |
   |                |                | the SCU has    |                |
   |                |                | attempted to   |                |
   |                |                | N-CREATE a SOP |                |
   |                |                | Instance that  |                |
   |                |                | has already    |                |
   |                |                | been created.  |                |
   |                |                | The response   |                |
   |                |                | status code    |                |
   |                |                | and meaning    |                |
   |                |                | are logged in  |                |
   |                |                | the job log    |                |
   |                |                | file           |                |
   +----------------+----------------+----------------+----------------+
   | No such SOP    | 0112           | Status         |                |
   | Instance       |                | returned when  |                |
   |                |                | the SCU is     |                |
   |                |                | trying to SET  |                |
   |                |                | a SOP instance |                |
   |                |                | that has not   |                |
   |                |                | been created.  |                |
   |                |                | The response   |                |
   |                |                | status code    |                |
   |                |                | and meaning    |                |
   |                |                | are logged in  |                |
   |                |                | the job log    |                |
   |                |                | file           |                |
   +----------------+----------------+----------------+----------------+
   | Missing        | 0120           | This status is |                |
   | Attribute      |                | returned if an |                |
   |                |                | attribute      |                |
   |                |                | required to be |                |
   |                |                | sent in the    |                |
   |                |                | N-CREATE or    |                |
   |                |                | required to be |                |
   |                |                | sent before    |                |
   |                |                | completion of  |                |
   |                |                | the Procedure  |                |
   |                |                | Step has not   |                |
   |                |                | been sent. The |                |
   |                |                | response       |                |
   |                |                | status code    |                |
   |                |                | and meaning    |                |
   |                |                | are logged in  |                |
   |                |                | the job log    |                |
   |                |                | file.          |                |
   +----------------+----------------+----------------+----------------+

.. _sect_C.4.2.1.4.3:

Activity - Configured AE Requests Verification
                                              

.. _sect_C.4.2.1.4.3.1:

Description and Sequencing of Activities
                                        

A remote AE sends an Echo Request to verify that DICOMSRV is awake and
listening. DICOMSRV responds with success status as long as the request
can be parsed.

.. _sect_C.4.2.1.4.3.2:

Accepted Presentation Contexts
                              

.. table:: Acceptable Presentation Contexts for AE DICOMSRV and
Real-World Activity Configured AE Requests Verification

   +------------+------------+------------+------------+-----+------+
   | Pr         |            |            |            |     |      |
   | esentation |            |            |            |     |      |
   | Context    |            |            |            |     |      |
   | Table      |            |            |            |     |      |
   +============+============+============+============+=====+======+
   | Ve         | 1.2.840    | Implicit   | 1.2.840    | SCP | None |
   | rification | .10008.1.1 | VR Little  | .10008.1.2 |     |      |
   | SOP Class  |            | Endian     |            |     |      |
   +------------+------------+------------+------------+-----+------+
   | Explicit   | 1.2.840.1  |            |            |     |      |
   | VR Little  | 0008.1.2.1 |            |            |     |      |
   | Endian     |            |            |            |     |      |
   +------------+------------+------------+------------+-----+------+

.. _sect_C.4.2.1.4.3.3:

SOP Specific Conformance
                        

DICOMSRV provides Standard conformance to the DICOM Verification service
class.

.. _sect_C.4.2.1.4.3.4:

Presentation Context Acceptance Criterion
                                         

Depending on configuration, DICOMSRV may or may not accept multiple
presentation contexts containing the same abstract syntax.

.. _sect_C.4.2.1.4.3.5:

Transfer Syntax Selection Policy
                                

Transfer Syntaxes in addition to the default Implicit VR Little Endian
may be configured for a given Abstract Syntax using DICOM Tool's
configuration files. When this is done, the first Transfer Syntax
encountered in the configuration file, which matches a Transfer Syntax
offered for a given Presentation Context, will be selected as the
accepted Transfer Syntax for that Presentation Context.

.. _sect_C.4.3:

Network Interfaces
~~~~~~~~~~~~~~~~~~

.. _sect_C.4.3.1:

Physical Network Interface
^^^^^^^^^^^^^^^^^^^^^^^^^^

The DICOMRis DICOM applications are indifferent to the physical medium
over which TCP/IP executes.

.. _sect_C.4.3.2:

Additional Protocols
^^^^^^^^^^^^^^^^^^^^

DHCP support can be configured using the Configuration application. If
DHCP is not configured a static IP address is assigned.

If DNS support exists on the local network, then DNS is used for address
resolution. The address of the DNS server is retrieved using DHCP if the
DHCP option is enabled. If DNS is not supported then the hostnames and
addresses are configured in the local hosts file.

.. _sect_C.4.3.3:

IPv4 and IPv6 Support
^^^^^^^^^^^^^^^^^^^^^

This product supports both IPv4 and IPv6. It does not utilize any of the
optional configuration identification or security features of IPv6.

.. _sect_C.4.4:

Configuration
~~~~~~~~~~~~~

.. _sect_C.4.4.1:

AE Title/Presentation Address Mapping
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The AE Title and port of DICOMSRV is configurable by the user from a
GUI-based configuration application. The IP Address is picked by the
site and may be changed by a Field Engineer.

.. _sect_C.4.4.1.1:

Local AE Titles
'''''''''''''''

.. table:: AE Title Configuration Table

   ================== ================== ===================
   Application Entity Default AE Title   Default TCP/IP Port
   ================== ================== ===================
   DICOMSRV           Must be configured 104
   ================== ================== ===================

.. _sect_C.4.4.1.2:

Remote AE Title/Presentation Address Mapping
''''''''''''''''''''''''''''''''''''''''''''

The AE Titles, host names, port numbers and supported Presentation
Contexts of remote applications are configured in file DICOMSRV.cfg.
This file is referenced by DICOMTool's software when API calls are made
to create Associations to remote AEs

.. _sect_C.4.4.2:

Parameters
^^^^^^^^^^

DICOMSRV configuration parameters related to DICOM communications are
below. A blank cell under the 'Default Value' heading indicates that
there is no default value for the specific configuration attribute.

.. table:: Configuration Parameters Table

   +--------------------------+--------------+--------------------------+
   | Parameter                | Configurable | Default Value            |
   +==========================+==============+==========================+
   | **General Parameters**   |              |                          |
   +--------------------------+--------------+--------------------------+
   | Time-out waiting for     | Yes          | 30 Seconds               |
   | acceptance or rejection  |              |                          |
   | Response to an           |              |                          |
   | Association Open Request |              |                          |
   +--------------------------+--------------+--------------------------+
   | Time-out waiting for     | Yes          | 15 Seconds               |
   | response to TCP/IP       |              |                          |
   | connect() request.       |              |                          |
   +--------------------------+--------------+--------------------------+
   | Time-out for waiting for | Yes          | 15 Seconds               |
   | data between TCP/IP      |              |                          |
   | packets. (Low-level      |              |                          |
   | timeout)                 |              |                          |
   +--------------------------+--------------+--------------------------+
   | Time-out waiting for a   | Yes          | 30 Seconds               |
   | response to a DIMSE      |              |                          |
   | Request                  |              |                          |
   +--------------------------+--------------+--------------------------+
   | Time-out waiting for the | Yes          | 60 Seconds               |
   | next DIMSE Request       |              |                          |
   +--------------------------+--------------+--------------------------+
   | **Debugging              |              |                          |
   | Capabilities**           |              |                          |
   +--------------------------+--------------+--------------------------+
   | Hex Dump DIMSE Messages  | Yes          | Off                      |
   +--------------------------+--------------+--------------------------+
   | Hex Dump Association     | Yes          | Off                      |
   | Messages                 |              |                          |
   +--------------------------+--------------+--------------------------+
   | **TCP/IP Settings**      |              |                          |
   +--------------------------+--------------+--------------------------+
   | TCP/IP Send Buffer       | Yes          | 65535 Bytes              |
   +--------------------------+--------------+--------------------------+
   | TCP//IP Receive Buffer   | Yes          | 65535 Bytes              |
   +--------------------------+--------------+--------------------------+
   | PacketFilter             | Yes          | On. This option enables  |
   |                          |              | running of tcpdump       |
   |                          |              | utility from the command |
   |                          |              | line to capture TCP      |
   |                          |              | packet headers/contents  |
   +--------------------------+--------------+--------------------------+
   | **DICOMSRV Parameters**  |              |                          |
   +--------------------------+--------------+--------------------------+
   | Maximum Number of        | Yes          | 20                       |
   | Simultaneous             |              |                          |
   | Associations             |              |                          |
   +--------------------------+--------------+--------------------------+
   | Maximum Number of        | Yes          | 3                        |
   | Associations to a given  |              |                          |
   | device                   |              |                          |
   +--------------------------+--------------+--------------------------+
   | Maximum PDU size the AE  | Yes          | 65536 Bytes              |
   | can receive              |              |                          |
   +--------------------------+--------------+--------------------------+
   | Maximum PDU size the AE  | No           | The lower of the value   |
   | can send                 |              | above and the max PDU    |
   |                          |              | size specified by the    |
   |                          |              | Remote AE in the         |
   |                          |              | Association Request      |
   +--------------------------+--------------+--------------------------+
   | Validation of DICOM      | Yes          | Validate messages and    |
   | Service Messages         |              | log validation errors.   |
   |                          |              | Do not automatically     |
   |                          |              | return error for all     |
   |                          |              | validation errors        |
   +--------------------------+--------------+--------------------------+
   | **Modality Worklist      |              |                          |
   | Parameters**             |              |                          |
   +--------------------------+--------------+--------------------------+
   | Maximum Number of        | Yes          | 100                      |
   | Matches for an MWL       |              |                          |
   | Request                  |              |                          |
   +--------------------------+--------------+--------------------------+
   | Time period after        | Yes          | 2880 min                 |
   | Scheduled Date/Time to   |              |                          |
   | leave SPS entries in the |              |                          |
   | SPS Worklist             |              |                          |
   +--------------------------+--------------+--------------------------+
   | State of Parent          | Yes          | PROCEDURE STARTED        |
   | Procedure that causes    |              |                          |
   | deletion of child SPS    |              |                          |
   | Entries                  |              |                          |
   +--------------------------+--------------+--------------------------+
   | Supported Transfer       | Yes          | Explicit VR Little       |
   | Syntaxes                 |              | Endian                   |
   |                          |              |                          |
   |                          |              | Implicit VR Little       |
   |                          |              | Endian                   |
   +--------------------------+--------------+--------------------------+
   | **Modality Performed     |              |                          |
   | Procedure Step           |              |                          |
   | Parameters**             |              |                          |
   +--------------------------+--------------+--------------------------+
   | Generate charges based   | Yes          | Off                      |
   | on supplies specified in |              |                          |
   | MPPS transactions        |              |                          |
   +--------------------------+--------------+--------------------------+
   | Purge Period for MPPS    | Yes          | 30 days                  |
   | transactions in final    |              |                          |
   | state                    |              |                          |
   +--------------------------+--------------+--------------------------+
   | State to automatically   | Yes          |                          |
   | set procedures to for a  |              |                          |
   | given AE on receipt of   |              |                          |
   | matching N-CREATE        |              |                          |
   +--------------------------+--------------+--------------------------+
   | State to automatically   | Yes          |                          |
   | set procedures to for a  |              |                          |
   | given AE on receipt of   |              |                          |
   | matching N-SET COMPLETED |              |                          |
   +--------------------------+--------------+--------------------------+
   | State to automatically   | Yes          |                          |
   | set procedures to for a  |              |                          |
   | given AE on receipt of   |              |                          |
   | matching N-SET           |              |                          |
   | DISCONTINUED             |              |                          |
   +--------------------------+--------------+--------------------------+
   | Flag specifying support  | Yes          | false                    |
   | for IHE Trauma cases for |              |                          |
   | a given AE               |              |                          |
   +--------------------------+--------------+--------------------------+
   | Patient ID Range to be   | Yes          |                          |
   | used for Patient         |              |                          |
   | Registration for IHE     |              |                          |
   | Trauma case              |              |                          |
   +--------------------------+--------------+--------------------------+
   | Default Procedure Code   | Yes          |                          |
   | to be used for orders    |              |                          |
   | for IHE Trauma cases     |              |                          |
   +--------------------------+--------------+--------------------------+
   | Supported Transfer       | Yes          | Explicit VR Little       |
   | Syntaxes                 |              | Endian                   |
   |                          |              |                          |
   |                          |              | Implicit VR Little       |
   |                          |              | Endian                   |
   +--------------------------+--------------+--------------------------+

.. _sect_C.5:

Media Interchange
-----------------

DICOMSRV does not support Media Storage

.. _sect_C.6:

Support of Character Sets
-------------------------

DICOMSRV support the following character sets in addition to the
default:

-  ISO_IR 100

.. _sect_C.7:

Security
--------

DICOMSRV does not support any specific security measures

.. _sect_C.8:

Annexes
-------

.. _sect_C.8.1:

IOD Contents
~~~~~~~~~~~~

.. _sect_C.8.1.1:

Created SOP Instances
^^^^^^^^^^^^^^^^^^^^^

DICOMRis does not create SOP instances

.. _sect_C.8.1.2:

Usage of Attributes From Received IODs
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Fields from MPPS such as technique and supplies and how they are used.

.. table:: Attributes in MPPS IOD Used By DICOMRis Applications

   +--------------------------+-------------+--------------------------+
   | Attribute Name           | Tag         | Database Updates         |
   +==========================+=============+==========================+
   | SOP Common Module        |             |                          |
   +--------------------------+-------------+--------------------------+
   | Performed Procedure Step |             |                          |
   | Relationship Module      |             |                          |
   +--------------------------+-------------+--------------------------+
   | Scheduled Step Attribute | (0040,0270) |                          |
   | Sequence                 |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Accession Number        | (0008,0050) | These attributes need to |
   |                          |             | match values in the      |
   |                          |             | DICOMRis database so     |
   |                          |             | other data contained in  |
   |                          |             | MPPS messages e.g., Dose |
   |                          |             | and Materials data, can  |
   |                          |             | update the database and  |
   |                          |             | be displayed by the      |
   |                          |             | RisView application as   |
   |                          |             | described below          |
   +--------------------------+-------------+--------------------------+
   | Patient ID               | (0010,0020) |                          |
   +--------------------------+-------------+--------------------------+
   | Performed Procedure Step |             |                          |
   | Information              |             |                          |
   +--------------------------+-------------+--------------------------+
   | Performed Station AE     | (0040,0241) | This attribute is used   |
   | Title                    |             | by the MppsSrv           |
   |                          |             | application as a key     |
   |                          |             | into the DICOM           |
   |                          |             | Configuration database   |
   |                          |             | to determine if the      |
   |                          |             | procedure referenced by  |
   |                          |             | the MPPS message should  |
   |                          |             | automatically have its   |
   |                          |             | state changed            |
   +--------------------------+-------------+--------------------------+
   | Performed Procedure Step | (0040,0254) | Values for these         |
   | Description              |             | attributes are           |
   |                          |             | accessible using the     |
   |                          |             | RisView application if   |
   |                          |             | they have been stored    |
   +--------------------------+-------------+--------------------------+
   | Procedure Code Sequence  | (0008,1032) |                          |
   +--------------------------+-------------+--------------------------+
   | >Code Value              | (0008,0100) |                          |
   +--------------------------+-------------+--------------------------+
   | >Coding Scheme           | (0008,0102) |                          |
   | Designator               |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Code Meaning            | (0008,0104) |                          |
   +--------------------------+-------------+--------------------------+
   | Image Acquisition        |             |                          |
   | Results                  |             |                          |
   +--------------------------+-------------+--------------------------+
   | Performed Protocol Code  | (0040,0260) | Values for these         |
   | Sequence                 |             | attributes are required  |
   |                          |             | if the RisView           |
   |                          |             | application is to        |
   |                          |             | display the protocol     |
   |                          |             | used to perform the      |
   |                          |             | procedure                |
   +--------------------------+-------------+--------------------------+
   | >Code Value              | (0008,0100) |                          |
   +--------------------------+-------------+--------------------------+
   | >Coding Scheme           | (0008,0102) |                          |
   | Designator               |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Code Meaning            | (0008,0104) |                          |
   +--------------------------+-------------+--------------------------+
   | Performed Series         | (0040,0340) |                          |
   | Sequence                 |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Protocol Name           | (0018,1030) |                          |
   +--------------------------+-------------+--------------------------+
   | >Operator's Name         | (0008,1070) | Can be displayed by      |
   |                          |             | RisView application      |
   +--------------------------+-------------+--------------------------+
   | >Retrieve AE Title       | (0008,0054) |                          |
   +--------------------------+-------------+--------------------------+
   | Billing and Material     |             |                          |
   | Management Code          |             |                          |
   +--------------------------+-------------+--------------------------+
   | Billing Procedure Step   |             | Values are needed for    |
   | Sequence                 |             | these attributes so that |
   |                          |             | the RisView application  |
   |                          |             | can display actual       |
   |                          |             | supplies and film used   |
   |                          |             | to perform a given       |
   |                          |             | procedure rather than    |
   |                          |             | default values           |
   |                          |             | associated with the      |
   |                          |             | given procedure in the   |
   |                          |             | DICOMRis database        |
   |                          |             |                          |
   |                          |             | The values of these      |
   |                          |             | attributes may also be   |
   |                          |             | used to generate charges |
   |                          |             | if the site is           |
   |                          |             | configured for charging  |
   |                          |             | based on MPPS            |
   +--------------------------+-------------+--------------------------+
   | >Code Value              | (0008,0100) |                          |
   +--------------------------+-------------+--------------------------+
   | >Coding Scheme           | (0008,0102) |                          |
   | Designator               |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Code Meaning            | (0008,0104) |                          |
   +--------------------------+-------------+--------------------------+
   | Film Consumption         | (0040,0321) |                          |
   | Sequence                 |             |                          |
   +--------------------------+-------------+--------------------------+
   | > Number of Films        | (2100,0170) |                          |
   +--------------------------+-------------+--------------------------+
   | > Medium Type            | (2000,0030) |                          |
   +--------------------------+-------------+--------------------------+
   | > Film Size ID           | (2010,0050) |                          |
   +--------------------------+-------------+--------------------------+
   | Billing Supplies and     | (0040,0384) |                          |
   | Devices Sequence         |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Billing Item Sequence   | (0040,0296) |                          |
   +--------------------------+-------------+--------------------------+
   | >>Code Value             | (0008,0100) |                          |
   +--------------------------+-------------+--------------------------+
   | >>Coding Scheme          | (0008,0102) |                          |
   | Designator               |             |                          |
   +--------------------------+-------------+--------------------------+
   | >>Code Meaning           | (0008,0104) |                          |
   +--------------------------+-------------+--------------------------+
   | >Quantity Sequence       | (0040,0293) |                          |
   +--------------------------+-------------+--------------------------+
   | >>Quantity               | (0040,0294) |                          |
   +--------------------------+-------------+--------------------------+
   | >>Measuring Units        | (0040,0295) |                          |
   | Sequence                 |             |                          |
   +--------------------------+-------------+--------------------------+
   | >>>Code Value            | (0008,0100) |                          |
   +--------------------------+-------------+--------------------------+
   | >>>Coding Scheme         | (0008,0102) |                          |
   | Designator               |             |                          |
   +--------------------------+-------------+--------------------------+
   | >>>Code Meaning          | (0008,0104) |                          |
   +--------------------------+-------------+--------------------------+

.. _sect_C.8.1.3:

Attribute Mapping
^^^^^^^^^^^^^^^^^

The mapping between attributes received via HL7 from the HIS and those
supplied in Modality Worklist is configurable. The default mapping is
contained in the table below. Empty cells indicate that there is no
mapping for the specific attribute

.. table:: HL7/Modality Worklist Attribute Mapping

   +-------------+-------------+-------------+-------------+-------------+
   | DICOM       | DICOM Tag   | HL7         | HL7 Segment | Notes       |
   | Attribute   |             | Attribute   |             |             |
   |             |             | Name        |             |             |
   +=============+=============+=============+=============+=============+
   | Scheduled   |             |             |             |             |
   | Procedure   |             |             |             |             |
   | Step        |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Scheduled   | (0040,0100) |             |             |             |
   | Procedure   |             |             |             |             |
   | Step        |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Scheduled  | (0040,0001) |             |             | DICOMRis    |
   | Station AE  |             |             |             | generated   |
   | Title       |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Scheduled  | (0040,0002) | Quan        | ORM OBR:27  | DICOMRis    |
   | Procedure   |             | tity/Timing |             | generated   |
   | Step Start  |             |             |             |             |
   | Date        |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Scheduled  | (0040,0003) | Quan        | ORM OBR:27  | DICOMRis    |
   | Procedure   |             | tity/Timing |             | generated   |
   | Step Start  |             |             |             |             |
   | Time        |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Modality   | (0008,0060) |             |             | DICOMRis    |
   |             |             |             |             | generated   |
   +-------------+-------------+-------------+-------------+-------------+
   | >Scheduled  | (0040,0006) | Technician  | ORM OBR:34  |             |
   | Performing  |             |             |             |             |
   | Physician's |             |             |             |             |
   | Name        |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Scheduled  | (0040,0007) |             |             | DICOMRis    |
   | Procedure   |             |             |             | generated   |
   | Step        |             |             |             |             |
   | Description |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Scheduled  | (0040,0010) |             |             | DICOMRis    |
   | Station     |             |             |             | generated   |
   | Name        |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Scheduled  | (0040,0011) |             |             | DICOMRis    |
   | Procedure   |             |             |             | generated   |
   | Step        |             |             |             |             |
   | Location    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Scheduled  | (0040,0008) |             |             |             |
   | Protocol    |             |             |             |             |
   | Code        |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Code      | (0008,0100) |             |             | DICOMRis    |
   | Value       |             |             |             | generated   |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Coding    | (0008,0102) |             |             | DICOMRis    |
   | Scheme      |             |             |             | generated   |
   | Designator  |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Code      | (0008,0104) |             |             | DICOMRis    |
   | Meaning     |             |             |             | generated   |
   +-------------+-------------+-------------+-------------+-------------+
   | >Pre        | (0040,0012) |             |             | DICOMRis    |
   | -Medication |             |             |             | generated   |
   +-------------+-------------+-------------+-------------+-------------+
   | >Scheduled  | (0040,0009) |             |             | DICOMRis    |
   | Procedure   |             |             |             | generated   |
   | Step ID     |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Requested  | (0032,1070) |             |             | DICOMRis    |
   | Contrast    |             |             |             | generated   |
   | Agent       |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Scheduled  | (0040,0020) |             |             | DICOMRis    |
   | Procedure   |             |             |             | generated   |
   | Step Status |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Comments   | (0040,0400) |             |             | DICOMRis    |
   | on the      |             |             |             | generated   |
   | Scheduled   |             |             |             |             |
   | Procedure   |             |             |             |             |
   | Step        |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Requested   |             |             |             |             |
   | Procedure   |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Requested   | (0040,1001) |             |             | DICOMRis    |
   | Procedure   |             |             |             | generated   |
   | ID          |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Requested   | (0032,1060) |             |             | DICOMRis    |
   | Procedure   |             |             |             | generated   |
   | Description |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Requested   | (0032,1064) |             |             |             |
   | Procedure   |             |             |             |             |
   | Code        |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Code Value | (0008,0100) | Universal   | ORM OBR:44  | The value   |
   |             |             | Service Id  |             | in the HL7  |
   |             |             |             |             | attribute   |
   |             |             |             |             | is mapped   |
   |             |             |             |             | to one or   |
   |             |             |             |             | more        |
   |             |             |             |             | procedure   |
   |             |             |             |             | codes in    |
   |             |             |             |             | the         |
   |             |             |             |             | DICOMRis    |
   |             |             |             |             | database.   |
   |             |             |             |             | The mapping |
   |             |             |             |             | is          |
   |             |             |             |             | c           |
   |             |             |             |             | onfigurable |
   +-------------+-------------+-------------+-------------+-------------+
   | >Coding     | (0008,0102) | Universal   | ORM OBR:44  | Maps to a   |
   | Scheme      |             | Service Id  |             | s           |
   | Designator  |             |             |             | ite-defined |
   |             |             |             |             | Coding      |
   |             |             |             |             | Scheme, the |
   |             |             |             |             | LOINC       |
   |             |             |             |             | Coding      |
   |             |             |             |             | Scheme or   |
   |             |             |             |             | the         |
   |             |             |             |             | DICOMRis    |
   |             |             |             |             | internal    |
   |             |             |             |             | Coding      |
   |             |             |             |             | Scheme      |
   +-------------+-------------+-------------+-------------+-------------+
   | >Code       | (0008,0008) |             |             | DICOMRis    |
   | Meaning     |             |             |             | generated   |
   +-------------+-------------+-------------+-------------+-------------+
   | Study       | (0020,000D) |             |             | DICOMRis    |
   | Instance    |             |             |             | generated   |
   | UID         |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Referenced  | (0008,1110) |             |             |             |
   | Study       |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Referenced | (0008,1150) |             |             | DICOMRis    |
   | SOP Class   |             |             |             | generated   |
   | UID         |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Referenced | (0008,1155) |             |             | DICOMRis    |
   | SOP         |             |             |             | generated   |
   | Instance    |             |             |             |             |
   | UID         |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Requested   | (0040,1003) |             | ORM OBR:27  |             |
   | Procedure   |             |             |             |             |
   | Priority    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Patient     | (0040,1004) |             | ORM OBR:30  |             |
   | Transport   |             |             |             |             |
   | A           |             |             |             |             |
   | rrangements |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Reason for  | (0040,0040) |             |             | DICOMRis    |
   | the         |             |             |             | generated   |
   | Requested   |             |             |             |             |
   | Procedure   |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Imaging     |             |             |             |             |
   | Service     |             |             |             |             |
   | Request     |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Accession   | (0008,0050) |             |             | DICOMRis    |
   | Number      |             |             |             | generated   |
   +-------------+-------------+-------------+-------------+-------------+
   | Requesting  | (0032,1032) |             | ORM OBR:16  |             |
   | Physician   |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Referring   | (0008,0090) |             | ORM PV1:8   |             |
   | Physician's |             |             |             |             |
   | Name        |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Reason for  | (0040,2001) | Reason for  | ORM OBR:31  |             |
   | the Imaging |             | Study       |             |             |
   | Service     |             |             |             |             |
   |             |             |             |             |             |
   | Request     |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Order       | (0040,2008) | Entered By  | ORM ORC:10  |             |
   | Entered By  |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Order       | (0040,2009) | Entering    | ORM ORC:17  |             |
   | Enterer's   |             | O           |             |             |
   | Location    |             | rganization |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Visit       |             |             |             |             |
   | Ide         |             |             |             |             |
   | ntification |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Admission   | (0038,0010) |             | ADT PID:3   |             |
   | ID          |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Admitting   | (0008,1080) |             | ADT DG1:4   |             |
   | Diagnosis   |             |             |             |             |
   | Description |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Admitting   | (0008,1084) |             |             |             |
   | Diagnoses   |             |             |             |             |
   | Code        |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Code Value | (0008,0008) |             | ADT DG1:3   |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Coding     | (0008,0008) |             | ADT DG1:2   |             |
   | Scheme      |             |             |             |             |
   | Designator  |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Code       | (0008,0008) |             |             |             |
   | Meaning     |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Patient     |             |             |             |             |
   | Ide         |             |             |             |             |
   | ntification |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Patient's   | (0010,0010) |             | ADT PID:5   |             |
   | Name        |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Patient ID  | (0010,0020) |             | ADT PID:3   |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Patient     |             |             |             |             |
   | D           |             |             |             |             |
   | emographics |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Patients    | (0010,0030) |             | ADT PID:7   |             |
   | Birth Date  |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Patient's   | (0010,0040) |             | ADT PID:8   |             |
   | Sex         |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Patient's   | (0010,1030) |             | ADT OBX:5   |             |
   | Weight      |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Ethnic      | (0010,2160) |             | ADT PID:10  |             |
   | Group       |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Patient     | (0010,4000) |             | ORM NTE:3   |             |
   | Comment     |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Patient     |             |             |             |             |
   | Medical     |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Patient     | (0038,0500) | Danger Code | ORM OBR:12  |             |
   | State       |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Pregnancy   | (0010,21C0) | Filler      | ORM OBR:20  |             |
   | Status      |             | Field 1     |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Medical     | (0010,2000) | Relevant    | ORM OBR:13  |             |
   | Alerts      |             | Clinical    |             |             |
   |             |             | Information |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Allergies   | (0010,2110) |             | ADT AL1:3   |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Last        | (0010,21D0) | Filler      | ORM OBR:20  |             |
   | Menstrual   |             | Field 1     |             |             |
   | Date        |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+

.. _sect_C.8.1.4:

Coerced/Modified Fields
^^^^^^^^^^^^^^^^^^^^^^^

.. table:: Coerced Fields for Modality Performed Procedure Step

   +--------------------------+-------------+--------------------------+
   | Attribute Name           | Tag         | Coercion Conditions      |
   +==========================+=============+==========================+
   | Performed Procedure Step |             |                          |
   | Relationship Module      |             |                          |
   +--------------------------+-------------+--------------------------+
   | Scheduled Step Attribute | (0040,0270) |                          |
   | Sequence                 |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Accession Number        | (0008,0050) | Procedure Step has been  |
   |                          |             | placed in the Exception  |
   |                          |             | queue due to failure to  |
   |                          |             | match DICOMRis database. |
   |                          |             | User enters a corrected  |
   |                          |             | value for Accession      |
   |                          |             | number through the       |
   |                          |             | RisView application      |
   +--------------------------+-------------+--------------------------+
   | >Placer Order            | (0040,2006) | Value for this attribute |
   | Number/Imaging Service   |             | is coerced when the      |
   | Request                  |             | value does not match the |
   |                          |             | corresponding value in   |
   |                          |             | the DICOMRis database.   |
   |                          |             | This may occur when the  |
   |                          |             | step is initially        |
   |                          |             | processed or during      |
   |                          |             | exception resolution     |
   +--------------------------+-------------+--------------------------+
   | >Filler Order            | (0040,2007) | As for attribute Placer  |
   | Number/Imaging Service   |             | Order Number/Imaging     |
   | Request                  |             | Service Request          |
   +--------------------------+-------------+--------------------------+
   | >Requested Procedure ID  | (0040,1001) | As for attribute Placer  |
   |                          |             | Order Number/Imaging     |
   |                          |             | Service Request          |
   +--------------------------+-------------+--------------------------+
   | >Requested Procedure     | (0032,1060) | As for attribute Placer  |
   | Description              |             | Order Number/Imaging     |
   |                          |             | Service Request          |
   +--------------------------+-------------+--------------------------+
   | >Scheduled Procedure     | (0040,0009) | As for attribute Placer  |
   | Step ID                  |             | Order Number/Imaging     |
   |                          |             | Service Request          |
   +--------------------------+-------------+--------------------------+
   | >Scheduled Procedure     | (0040,0007) | As for attribute Placer  |
   | Step Description         |             | Order Number/Imaging     |
   |                          |             | Service Request          |
   +--------------------------+-------------+--------------------------+
   | >Scheduled Protocol Code | (0040,0008) | As for attribute Placer  |
   | Sequence                 |             | Order Number/Imaging     |
   |                          |             | Service Request          |
   +--------------------------+-------------+--------------------------+
   | >>Code Value             | (0008,0100) | As for attribute Placer  |
   |                          |             | Order Number/Imaging     |
   |                          |             | Service Request          |
   +--------------------------+-------------+--------------------------+
   | >>Coding Scheme          | (0008,0102) | As for attribute Placer  |
   | designator               |             | Order Number/Imaging     |
   |                          |             | Service Request          |
   +--------------------------+-------------+--------------------------+
   | >>Code Meaning           | (0008,0104) | As for attribute Placer  |
   |                          |             | Order Number/Imaging     |
   |                          |             | Service Request          |
   +--------------------------+-------------+--------------------------+
   | Patient Name             | (0010,0010) | As for attribute Placer  |
   |                          |             | Order Number/Imaging     |
   |                          |             | Service Request          |
   +--------------------------+-------------+--------------------------+
   | Patient ID               | (0010,0020) | Procedure Step has been  |
   |                          |             | placed in the Exception  |
   |                          |             | queue due to failure to  |
   |                          |             | match DICOMRis database. |
   |                          |             | User enters a corrected  |
   |                          |             | value for Patient ID     |
   |                          |             | through the RisView      |
   |                          |             | application              |
   +--------------------------+-------------+--------------------------+
   | Patient's Birth Date     | (0010,0030) | As for attribute Placer  |
   |                          |             | Order Number/Imaging     |
   |                          |             | Service Request          |
   +--------------------------+-------------+--------------------------+
   | Patient's Sex            | (0010,0040) | As for attribute Placer  |
   |                          |             | Order Number/Imaging     |
   |                          |             | Service Request          |
   +--------------------------+-------------+--------------------------+

.. _sect_C.8.2:

Data Dictionary of Private Attributes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

DICOMSRV does not use any private attributes.

.. _sect_C.8.3:

Coded Terminology and Templates
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

DICOMRis's usage of Coding Schemes is specified in the table below. This
table lists the Coding Schemes used by DICOMRis for attributes it
originates. Usage of Controlled Terminology by Applications sending IODs
to DICOMRis is discussed in the relevant SOP Specific Conformance
sections above. The Procedure and Protocol Codes in the DICOMRis
database can be exported to files and transferred across the network
using the Configuration Utility. This allows Modalities to access and
incorporate these codes if so desired.

.. table:: DICOMRis Controlled Terminology Usage

   +----------+----------+----------+----------+----------+----------+
   | SOP      | A        | Tag      | Baseline | Coding   | Remarks  |
   | Class    | ttribute |          | Context  | Scheme   |          |
   | /Service | Name     |          | ID       |          |          |
   +==========+==========+==========+==========+==========+==========+
   | S        |          |          |          |          |          |
   | cheduled |          |          |          |          |          |
   | P        |          |          |          |          |          |
   | rocedure |          |          |          |          |          |
   | Step     |          |          |          |          |          |
   | Module   |          |          |          |          |          |
   +----------+----------+----------+----------+----------+----------+
   | MWL/     | >S       | (00      | None     | LOINC,   | At the   |
   | C-FIND   | cheduled | 40,0008) |          | DICOMRis | option   |
   |          | Protocol |          |          | Pr       | of the   |
   |          | Code     |          |          | ocedure, | site,    |
   |          | Sequence |          |          | site-    | DICOMRis |
   |          |          |          |          | supplied | may be   |
   |          |          |          |          | p        | co       |
   |          |          |          |          | rocedure | nfigured |
   |          |          |          |          | codes or | to       |
   |          |          |          |          | site-    | a        |
   |          |          |          |          | supplied | ssociate |
   |          |          |          |          | protocol | LOINC,   |
   |          |          |          |          | codes    | DICOMRis |
   |          |          |          |          |          | Internal |
   |          |          |          |          |          | codes or |
   |          |          |          |          |          | site-    |
   |          |          |          |          |          | supplied |
   |          |          |          |          |          | p        |
   |          |          |          |          |          | rocedure |
   |          |          |          |          |          | codes    |
   |          |          |          |          |          | with the |
   |          |          |          |          |          | various  |
   |          |          |          |          |          | pr       |
   |          |          |          |          |          | ocedures |
   |          |          |          |          |          | rep      |
   |          |          |          |          |          | resented |
   |          |          |          |          |          | in their |
   |          |          |          |          |          | Item     |
   |          |          |          |          |          | master   |
   |          |          |          |          |          | file.    |
   |          |          |          |          |          | The      |
   |          |          |          |          |          | co       |
   |          |          |          |          |          | nfigured |
   |          |          |          |          |          | p        |
   |          |          |          |          |          | rocedure |
   |          |          |          |          |          | code     |
   |          |          |          |          |          | will be  |
   |          |          |          |          |          | passed   |
   |          |          |          |          |          | in this  |
   |          |          |          |          |          | a        |
   |          |          |          |          |          | ttribute |
   |          |          |          |          |          | unless   |
   |          |          |          |          |          | the site |
   |          |          |          |          |          | has      |
   |          |          |          |          |          | supplied |
   |          |          |          |          |          | and      |
   |          |          |          |          |          | co       |
   |          |          |          |          |          | nfigured |
   |          |          |          |          |          | protocol |
   |          |          |          |          |          | codes to |
   |          |          |          |          |          | be       |
   |          |          |          |          |          | as       |
   |          |          |          |          |          | sociated |
   |          |          |          |          |          | with the |
   |          |          |          |          |          | re       |
   |          |          |          |          |          | spective |
   |          |          |          |          |          | pr       |
   |          |          |          |          |          | ocedures |
   |          |          |          |          |          | in       |
   |          |          |          |          |          | addition |
   |          |          |          |          |          | to       |
   |          |          |          |          |          | p        |
   |          |          |          |          |          | rocedure |
   |          |          |          |          |          | codes.   |
   |          |          |          |          |          | In this  |
   |          |          |          |          |          | case the |
   |          |          |          |          |          | co       |
   |          |          |          |          |          | nfigured |
   |          |          |          |          |          | protocol |
   |          |          |          |          |          | code     |
   |          |          |          |          |          | will be  |
   |          |          |          |          |          | passed   |
   +----------+----------+----------+----------+----------+----------+
   | R        |          |          |          |          |          |
   | equested |          |          |          |          |          |
   | P        |          |          |          |          |          |
   | rocedure |          |          |          |          |          |
   | Module   |          |          |          |          |          |
   +----------+----------+----------+----------+----------+----------+
   |          | R        | (00      | None     | LOINC,   | See      |
   |          | equested | 32,1064) |          | DICOMRis | remarks  |
   |          | P        |          |          | Pr       | for      |
   |          | rocedure |          |          | ocedure, | S        |
   |          | Code     |          |          | site-    | cheduled |
   |          | Sequence |          |          | supplied | Protocol |
   |          |          |          |          | p        | Code     |
   |          |          |          |          | rocedure | Sequence |
   |          |          |          |          | codes    | (004     |
   |          |          |          |          |          | 0,0040). |
   |          |          |          |          |          | The      |
   |          |          |          |          |          | di       |
   |          |          |          |          |          | fference |
   |          |          |          |          |          | is that  |
   |          |          |          |          |          | a        |
   |          |          |          |          |          | p        |
   |          |          |          |          |          | rocedure |
   |          |          |          |          |          | code is  |
   |          |          |          |          |          | always   |
   |          |          |          |          |          | passed   |
   |          |          |          |          |          | in this  |
   |          |          |          |          |          | a        |
   |          |          |          |          |          | ttribute |
   |          |          |          |          |          | rather   |
   |          |          |          |          |          | than a   |
   |          |          |          |          |          | protocol |
   |          |          |          |          |          | code     |
   +----------+----------+----------+----------+----------+----------+

.. _sect_C.8.4:

Grayscale Image Consistency
~~~~~~~~~~~~~~~~~~~~~~~~~~~

DICOMSRV does not support the Grayscale Standard Display Function

.. _sect_C.8.5:

Standard Extended/Specialized/Private SOP Classes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

DICOMSRV does not claim conformance to any Extended, Specialized or
Private SOP Classes.

.. _sect_C.8.6:

Private Transfer Syntaxes
~~~~~~~~~~~~~~~~~~~~~~~~~

DICOMSRV does not employ any Private Transfer Syntaxes.

