.. _chapter_P:

Application Event Logging Service Class (Normative)
===================================================

.. _sect_P.1:

Overview
--------

.. _sect_P.1.1:

Scope
~~~~~

The Application Event Logging Service Class defines an application-level
class-of-service that facilitates the network transfer of Event Log
Records to be logged or recorded in a central location.

The Application Event Logging Service Class addresses the class of
application specific logs (e.g., procedural event logs) that are managed
by a medical application. The Application Event Logging Service Class
does not specify the means of accessing the central logs.

.. note::

   This Service Class does not address system security or audit logs
   that are managed by general system logging applications and may use
   non-DICOM protocols (e.g., SYSLOG).

.. _sect_P.1.2:

Service Definition
~~~~~~~~~~~~~~~~~~

Two peer DICOM AEs implement a SOP Class of the Application Event
Logging Service Class with one serving in the SCU role and one serving
in the SCP role. SOP Classes of the Application Event Logging Service
Class are implemented using the DIMSE-N N-ACTION service as defined in .

The N-ACTION service conveys the following semantics:

-  The SCU notifies the SCP that an event has occurred that the SCP
   should record in a log. The Action Information of the N-ACTION-RQ
   contains the information about the event.

-  The SCP responds with a confirmation of the status of the recording
   action.

The association negotiation procedure is used to negotiate the supported
SOP Classes. specifies the association procedure. The Application Event
Logging Service Class does not support extended negotiation.

The release of an association shall not have any effect on the contents
of the log managed by the SCP.

.. _sect_P.2:

Procedural Event Logging SOP Class Definition
---------------------------------------------

The Procedural Event Logging SOP Class allows SCUs to report to an SCP
the events that are to be recorded in a Procedure Log SOP Instance, as
described in . This allows multiple devices participating in a Study to
cooperatively construct a log of events that occur during that Study.

The multiple procedural events reported through this SOP Class are
related by Patient ID, Study Instance UID, Study ID, and/or Performed
Location. The mechanism by which multiple devices obtain these shared
identifiers is not defined by this SOP Class.

.. note::

   The Modality Worklist or UPS SOP Classes may be used for this
   purpose. For simple devices that cannot support worklist SOP Classes,
   the SCP may be able to use Performed Location, or the SCU AE Title,
   to relate the use of the device to a particular procedure.

The SCP may also provide for recording events for which the SCU does not
provide identifiers for matching. The mechanism by which the SCP
determines the association of such an unidentified event with the log
for a specific procedure is not defined by this SOP Class.

.. note::

   The network address and/or AE Title of the SCU may be used to
   identify the device as a participant in a particular procedure.

.. _sect_P.2.1:

DIMSE Service Group
~~~~~~~~~~~~~~~~~~~

The DIMSE-N Services applicable to the Procedural Event Logging SOP
Class are shown in `table_title <#table_P.2-1>`__.

.. table:: DIMSE Service Group Applicable to Procedural Event Logging

   ============================= =============
   DICOM Message Service Element Usage SCU/SCP
   ============================= =============
   N-ACTION                      M/M
   ============================= =============

The DIMSE-N Services and Protocol are specified in .

.. _sect_P.2.2:

Operation
~~~~~~~~~

The DICOM AEs that claim conformance to this SOP Class as an SCU shall
invoke the N-ACTION request. The DICOM AEs that claim conformance to
this SOP Class as an SCP shall support the N-ACTION request.

.. _sect_P.2.2.1:

Action Information
^^^^^^^^^^^^^^^^^^

The DICOM AEs that claim conformance to this SOP Class as an SCU and/or
an SCP shall support the Action Type and Action Information in the
N-ACTION-RQ as specified in `table_title <#table_P.2-2>`__.

.. table:: Procedural Event Logging Action Information

   +-------------+-------------+-------------+-------------+-------------+
   | Action Type | Action Type | Attribute   | Tag         | Requirement |
   | Name        | ID          | Name        |             | Type        |
   |             |             |             |             | SCU/SCP     |
   +=============+=============+=============+=============+=============+
   | Record      | 1           | Specific    | (0008,0005) | 1C/1C       |
   | Procedural  |             | Character   |             |             |
   | Event       |             | Set         |             | (Required   |
   |             |             |             |             | if an       |
   |             |             |             |             | extended or |
   |             |             |             |             | replacement |
   |             |             |             |             | character   |
   |             |             |             |             | set is      |
   |             |             |             |             | used)       |
   +-------------+-------------+-------------+-------------+-------------+
   |             |             | Patient ID  | (0010,0020) | 2/2         |
   +-------------+-------------+-------------+-------------+-------------+
   |             |             | Study       | (0020,000D) | 2/2         |
   |             |             | Instance    |             |             |
   |             |             | UID         |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   |             |             | Study ID    | (0020,0010) | 2/2         |
   +-------------+-------------+-------------+-------------+-------------+
   |             |             | Sync        | (0020,0200) | 2/2         |
   |             |             | hronization |             |             |
   |             |             | Frame of    |             |             |
   |             |             | Reference   |             |             |
   |             |             | UID         |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   |             |             | Performed   | (0040,0243) | 2/2         |
   |             |             | Location    |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   |             |             | *All other  |             | See         |
   |             |             | Attributes  |             | `           |
   |             |             | of the      |             | Constraints |
   |             |             | using*      |             | on          |
   |             |             |             |             | Attributes  |
   |             |             |             |             | of the SR   |
   |             |             |             |             | Document    |
   |             |             |             |             | Content     |
   |             |             |             |             | Modul       |
   |             |             |             |             | e <#sect_P. |
   |             |             |             |             | 2.2.1.3>`__ |
   +-------------+-------------+-------------+-------------+-------------+

.. _sect_P.2.2.1.1:

Study Matching Attributes
'''''''''''''''''''''''''

The SCU may provide Patient ID (0010,0020), Study Instance UID
(0020,000D), Study ID (0020,0010), and/or Performed Location (0040,0243)
Attributes to allow the SCP to match the N-ACTION with a Study for which
a procedure log is being created.

.. _sect_P.2.2.1.2:

Synchronization Frame of Reference UID
''''''''''''''''''''''''''''''''''''''

The Synchronization Frame of Reference UID (0020,0200) Attribute
identifies the temporal frame of reference for the Observation DateTime
(0040,A032) Attributes in the Procedural Event record. If the
Observation DateTime Attribute Values are not synchronized in an
identifiable Frame of Reference, the Attribute shall be zero length.

.. _sect_P.2.2.1.3:

Constraints on Attributes of the SR Document Content Module
'''''''''''''''''''''''''''''''''''''''''''''''''''''''''''

The Procedural Event record shall be conveyed in a (top level) Content
Item, and subsidiary Content Items, as specified by the SR Document
Content Module definition in .

The top level and subsidiary Content Items shall be constructed in
accordance with the Procedure Log IOD Content Constraints of .

.. note::

   1. These constraints specify use of BTID 3001 Procedure Log defined
      in , and specific particular use of the Observation DateTime
      (0040,A032) Attributes.

   2. TID 3001 requires the explicit identification of the Observer
      Context of the top level CONTAINER through TID 1002.

   3. There may be multiple events (subsidiary Content Items) included
      in a single N-ACTION-RQ message.

.. _sect_P.2.2.2:

Service Class User Behavior
^^^^^^^^^^^^^^^^^^^^^^^^^^^

The SCU shall request logging of events that occur during a Study, using
the N-ACTION request primitive.

The SCU shall receive N-ACTION responses. The actions taken upon a
response status of Failure, or upon non-response of the SCP, are
implementation dependent.

.. _sect_P.2.2.3:

Service Class Provider Behavior
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The SCP shall manage the creation of SOP Instances of the Procedure Log
Storage Service. It shall receive, via the N-ACTION request primitive,
requests for logging of events that occur during a Study. The SCP shall
(consonant with application dependent constraints) incorporate those
event records into a Procedure Log SOP Instance for the specified Study.

The SCP shall return, via the N-ACTION response primitive, the N-ACTION
Response Status Code applicable to the associated action request.

.. _sect_P.2.2.4:

Status Codes
^^^^^^^^^^^^

`table_title <#table_P.2-3>`__ defines the specific status code values
that might be returned in a N-ACTION response. See for additional
general response status codes.

.. table:: Response Status

   +------------------------+------------------------+-----------------+
   | Service Status         | Further Meaning        | **Status Code** |
   +========================+========================+=================+
   | Success                |                        | 0000            |
   +------------------------+------------------------+-----------------+
   | Warning                | Specified              | B101            |
   |                        | Synchronization Frame  |                 |
   |                        | of Reference UID does  |                 |
   |                        | not match SCP          |                 |
   |                        | Synchronization Frame  |                 |
   |                        | of Reference           |                 |
   +------------------------+------------------------+-----------------+
   | Study Instance UID     | B102                   |                 |
   | coercion; Event logged |                        |                 |
   | under a different      |                        |                 |
   | Study Instance UID     |                        |                 |
   +------------------------+------------------------+-----------------+
   | IDs inconsistent in    | B104                   |                 |
   | matching a current     |                        |                 |
   | study; Event logged    |                        |                 |
   +------------------------+------------------------+-----------------+
   | Failure                | Failed: Procedural     | C101            |
   |                        | Logging not available  |                 |
   |                        | for specified Study    |                 |
   |                        | Instance UID           |                 |
   +------------------------+------------------------+-----------------+
   | Failed: Event          | C102                   |                 |
   | Information does not   |                        |                 |
   | match Template         |                        |                 |
   +------------------------+------------------------+-----------------+
   | Failed: Cannot match   | C103                   |                 |
   | event to a current     |                        |                 |
   | study                  |                        |                 |
   +------------------------+------------------------+-----------------+
   | Failed: IDs            | C104                   |                 |
   | inconsistent in        |                        |                 |
   | matching a current     |                        |                 |
   | study; Event not       |                        |                 |
   | logged                 |                        |                 |
   +------------------------+------------------------+-----------------+

.. _sect_P.2.2.5:

Action Reply
^^^^^^^^^^^^

With any response status indicating Success or Warning, the identifiers
of the study into which the event has been logged shall be returned in
the N-ACTION-RSP Action Reply as specified in
`table_title <#table_P.2-4>`__.

.. table:: Procedural Event Logging Action Reply

   +-------------+-------------+-------------+-------------+-------------+
   | Action Type | Action Type | Attribute   | Tag         | Requirement |
   | Name        | ID          | Name        |             | Type        |
   |             |             |             |             | SCU/SCP     |
   +=============+=============+=============+=============+=============+
   | Record      | 1           | Study       | (0020,000D) | 3/1         |
   | Procedural  |             | Instance    |             |             |
   | Event       |             | UID         |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Patient ID  | (0010,0020) | 3/1         |             |             |
   +-------------+-------------+-------------+-------------+-------------+

.. _sect_P.2.3:

Procedural Event Logging SOP Class UID
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Procedural Event Logging SOP Class shall be uniquely identified by
the Procedural Event Logging SOP Class UID, which shall have the value
"1.2.840.10008.1.40".

.. _sect_P.2.4:

Procedural Event Logging Instance Identification
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The well-known UID of the Procedural Event Logging SOP Instance shall
have the value "1.2.840.10008.1.40.1".

.. _sect_P.2.5:

Conformance Requirements
~~~~~~~~~~~~~~~~~~~~~~~~

The DICOM AE's Conformance Statement shall be formatted as defined in .

.. _sect_P.2.5.1:

SCU Conformance
^^^^^^^^^^^^^^^

The SCU shall document in its Conformance Statement the behavior and
actions that cause the SCU to generate an N-ACTION primitive (Procedural
Event Notification). It shall specify the Template used for constructing
the Event Information, and the Coding Schemes used for coded entries in
the Event Information.

The SCU shall document the identifiers it sends for matching purposes,
and how it obtains those Attributes (e.g., through a Modality Worklist
query, manual entry, etc.).

The SCU shall document the behavior and actions performed when a
success, warning, or failure status is received.

The SCU shall document the mechanisms used for establishing time
synchronization and specifying the Synchronization Frame of Reference
UID.

.. _sect_P.2.5.2:

SCP Conformance
^^^^^^^^^^^^^^^

The SCP shall document in its Conformance Statement how it uses the
identifiers it receives for matching the N-ACTION (Procedural Event
Notification) to a specific procedure.

The SCP shall document the behavior and actions that cause the SCP to
generate a success, warning, or failure status for a received N-ACTION.

The SCP shall document the behavior and actions that cause the SCP to
generate a Procedure Log SOP Instance including the received Event
Information.

The SCP shall document how it assigns the value of the Observation
Datetime (0040,A032) Attribute when the SCU-provided Synchronization
Frame of Reference UID is absent, or differs from that of the SCP.

.. _sect_P.3:

Substance Administration Logging SOP Class Definition
-----------------------------------------------------

The Substance Administration Logging SOP Class allows an SCU to report
to an SCP the events that are to be recorded in a patient's Medication
Administration Record (MAR) or similar log, whose definition is outside
the scope of the Standard. This allows devices with DICOM protocol
interfaces to report administration of diagnostic agents (including
contrast) and therapeutic drugs, and implantation of devices.

The Substance Administration reported through this SOP Class is related
to the MAR by Patient ID or Admission ID. The mechanism by which the SCU
obtains this identifier is not defined by this SOP Class.

The log entry to the MAR is authorized by at least one of the Operators
identified in the Operator Identification Sequence. The mechanism by
which the SCU obtains these identifiers is not defined by this SOP
Class. The SCP may refuse the log entry if none of the identified
Operators is authorized to add entries to the MAR. The mechanism by
which the SCP validates such authorization is not defined by this SOP
Class.

.. note::

   1. The SCP of this Service Class is not necessarily the Medication
      Administration Record system, but may be a gateway system between
      this DICOM Service and an HL7 or proprietary interface of a MAR
      system. Such implementation design is beyond the scope of the
      DICOM Standard.

   2. This SOP Class is not limited to only specifying medications,
      although the conventional name of the destination log is the
      Medication Administration Record. The SOP Class may also be used
      to record the implantation of therapeutic devices, including both
      drug-eluting and bare stents, prosthetic and cardiovascular
      devices, implantable infusion pumps, etc.

   3. The application level authorization of Operators for the purpose
      of logging a MAR entry is distinct from any access control
      mechanism at the transport layer (see User Identity Association
      profiles in ).

.. _sect_P.3.1:

DIMSE Service Group
~~~~~~~~~~~~~~~~~~~

The DIMSE-N Services applicable to the Substance Administration Logging
SOP Class are shown in `table_title <#table_P.3-1>`__.

.. table:: DIMSE Service Group Applicable to Substance Administration
Logging

   ============================= =============
   DICOM Message Service Element Usage SCU/SCP
   ============================= =============
   N-ACTION                      M/M
   ============================= =============

The DIMSE-N Services and Protocol are specified in .

.. _sect_P.3.2:

Operation
~~~~~~~~~

The DICOM AEs that claim conformance to this SOP Class as an SCU shall
invoke the N-ACTION request. The DICOM AEs that claim conformance to
this SOP Class as an SCP shall support the N-ACTION request.

.. _sect_P.3.2.1:

Substance Administration Log Action Information
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This operation allows an SCU to submit a Medication Administration
Record log item or entry, providing information about a specific
real-world act of Substance Administration that is the purview of the
SCU. This operation shall be invoked through the DIMSE N-ACTION Service.

The Action Information Attributes are defined by the Substance
Administration Log Module specified in . The DICOM AEs that claim
conformance to this SOP Class as an SCU and/or an SCP shall support the
Action Type and Action Information Attributes in the N-ACTION-RQ as
specified in `table_title <#table_P.3-2>`__.

.. table:: Substance Administration Logging N-ACTION Information

   +-------------+-------------+-------------+-------------+-------------+
   | Action Type | Action Type | Attribute   | Tag         | Requirement |
   | Name        | ID          | Name        |             | Type        |
   |             |             |             |             | SCU/SCP     |
   +=============+=============+=============+=============+=============+
   | Record      | 1           | Specific    | (0008,0005) | 1C/1C       |
   | Substance   |             | Character   |             |             |
   | Adm         |             | Set         |             | (Required   |
   | inistration |             |             |             | if an       |
   | Event       |             |             |             | extended or |
   |             |             |             |             | replacement |
   |             |             |             |             | character   |
   |             |             |             |             | set is      |
   |             |             |             |             | used)       |
   +-------------+-------------+-------------+-------------+-------------+
   | Patient ID  | (0010,0020) | 1C/1C       |             |             |
   |             |             |             |             |             |
   |             |             | Either or   |             |             |
   |             |             | both        |             |             |
   |             |             | Patient ID  |             |             |
   |             |             | and         |             |             |
   |             |             | Admission   |             |             |
   |             |             | ID shall be |             |             |
   |             |             | supplied by |             |             |
   |             |             | the SCU;    |             |             |
   |             |             | the SCP     |             |             |
   |             |             | shall       |             |             |
   |             |             | support the |             |             |
   |             |             | Attribute   |             |             |
   |             |             | if supplied |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Issuer of   | (0010,0021) | 3/2         |             |             |
   | Patient ID  |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Patient's   | (0010,0010) | 2/2         |             |             |
   | Name        |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Admission   | (0038,0010) | 1C/1C       |             |             |
   | ID          |             |             |             |             |
   |             |             | Either or   |             |             |
   |             |             | both        |             |             |
   |             |             | Patient ID  |             |             |
   |             |             | and         |             |             |
   |             |             | Admission   |             |             |
   |             |             | ID shall be |             |             |
   |             |             | supplied by |             |             |
   |             |             | the SCU;    |             |             |
   |             |             | the SCP     |             |             |
   |             |             | shall       |             |             |
   |             |             | support the |             |             |
   |             |             | Attribute   |             |             |
   |             |             | if supplied |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Issuer of   | (0038,0011) | 3/2         |             |             |
   | Admission   |             |             |             |             |
   | ID          |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Product     | (0044,0001) | 1C/1C       |             |             |
   | Package     |             |             |             |             |
   | Identifier  |             | Either or   |             |             |
   |             |             | both        |             |             |
   |             |             | Product     |             |             |
   |             |             | Package     |             |             |
   |             |             | Identifier  |             |             |
   |             |             | and Product |             |             |
   |             |             | Name shall  |             |             |
   |             |             | be supplied |             |             |
   |             |             | by the SCU; |             |             |
   |             |             | the SCP     |             |             |
   |             |             | shall       |             |             |
   |             |             | support the |             |             |
   |             |             | Attribute   |             |             |
   |             |             | if supplied |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Product     | (0044,0008) | 1C/1C       |             |             |
   | Name        |             |             |             |             |
   |             |             | Either or   |             |             |
   |             |             | both        |             |             |
   |             |             | Product     |             |             |
   |             |             | Package     |             |             |
   |             |             | Identifier  |             |             |
   |             |             | and Product |             |             |
   |             |             | Name shall  |             |             |
   |             |             | be supplied |             |             |
   |             |             | by the SCU; |             |             |
   |             |             | the SCP     |             |             |
   |             |             | shall       |             |             |
   |             |             | support the |             |             |
   |             |             | Attribute   |             |             |
   |             |             | if supplied |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Product     | (0044,0009) | 3/3         |             |             |
   | Description |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Substance   | (0044,0010) | 1/1         |             |             |
   | Adm         |             |             |             |             |
   | inistration |             |             |             |             |
   | DateTime    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Substance   | (0044,0011) | 3/2         |             |             |
   | Adm         |             |             |             |             |
   | inistration |             |             |             |             |
   | Notes       |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Substance   | (0044,0012) | 3/3         |             |             |
   | Adm         |             |             |             |             |
   | inistration |             |             |             |             |
   | Device ID   |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Adm         | (0054,0302) | 2/2         |             |             |
   | inistration |             |             |             |             |
   | Route Code  |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | *>Includ    |             |             |             |             |
   | e*\ `table_ |             |             |             |             |
   | title <#tab |             |             |             |             |
   | le_8-1a>`__ |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Substance   | (0044,0019) | 3/3         |             |             |
   | Adm         |             |             |             |             |
   | inistration |             |             |             |             |
   | Parameter   |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >\ *All     |             | 3/3         |             |             |
   | Attributes  |             |             |             |             |
   | of the      |             |             |             |             |
   | Substance   |             |             |             |             |
   | Adm         |             |             |             |             |
   | inistration |             |             |             |             |
   | Parameter   |             |             |             |             |
   | Sequence*   |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Operator    | (0008,1072) | 1/1         |             |             |
   | Ide         |             |             |             |             |
   | ntification |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Person     | (0040,1101) | 1/1         |             |             |
   | Ide         |             |             |             |             |
   | ntification |             |             |             |             |
   | Code        |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | *>>Includ   |             |             |             |             |
   | e*\ `table_ |             |             |             |             |
   | title <#tab |             |             |             |             |
   | le_8-1a>`__ |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+

.. _sect_P.3.2.2:

Service Class User Behavior
^^^^^^^^^^^^^^^^^^^^^^^^^^^

The SCU shall request logging of substance administration events for a
specified Patient using the N-ACTION request primitive.

The SCU shall receive N-ACTION responses. The actions taken upon a
response status of Failure, or upon non-response of the SCP, are
implementation dependent.

.. _sect_P.3.2.3:

Service Class Provider Behavior
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The SCP shall receive, via the N-ACTION request primitive, requests for
logging of substance administration events. The SCP shall incorporate
those event records into a Medication Administration Record or similar
log for the specified Patient.

.. note::

   The patient's identify may be conveyed explicitly by Patient ID
   (0010,0020), or implicitly by Admission (i.e., Visit) ID (0038,0010).
   An institution may typically chose one or the other to use as the
   primary patient identifier at the point of care, e.g., printed on a
   bar coded wristband, the use of which may facilitate data entry for
   the log entry. However, in the "Model of the Real World for the
   Purpose of Modality-IS Interface" (see ), the Visit is subsidiary to
   the Patient; hence the Admission ID (0038,0010) may only be unique
   within the context of the patient, not within the context of the
   institution. The use of the Admission ID (0038,0010) Attribute to
   identify the Patient is only effective if the Admission ID
   (0038,0010) is unique within the context of the institution.

The SCP shall support inclusion into the Medication Administration
Record or similar log of values of all Type 1 and Type 2 Attributes for
which the SCU has provided values. The SCP may convert these Attributes
into a form appropriate for the destination log.

.. note::

   The SCP may convert coded data to free text in the log, with loss of
   the specific code values, if the log does not support such coded
   data.

The SCP shall return, via the N-ACTION response primitive, the N-ACTION
Response Status Code applicable to the associated action request.

.. _sect_P.3.2.4:

Status Codes
^^^^^^^^^^^^

`table_title <#table_P.3-3>`__ defines the specific status code values
that might be returned in a N-ACTION response. See for additional
general response status codes.

.. table:: Response Status

   +------------------------+------------------------+-----------------+
   | Service Status         | Further Meaning        | **Status Code** |
   +========================+========================+=================+
   | Success                |                        | 0000            |
   +------------------------+------------------------+-----------------+
   | Failure                | Failed: Operator       | C10E            |
   |                        | Refused: Not           |                 |
   |                        | authorized to add      |                 |
   |                        | entry to Medication    |                 |
   |                        | Administration Record  |                 |
   +------------------------+------------------------+-----------------+
   | Failed: Patient cannot | C110                   |                 |
   | be identified from     |                        |                 |
   | Patient ID (0010,0020) |                        |                 |
   | or Admission ID        |                        |                 |
   | (0038,0010)            |                        |                 |
   +------------------------+------------------------+-----------------+
   | Failed: Update of      | C111                   |                 |
   | Medication             |                        |                 |
   | Administration Record  |                        |                 |
   | failed                 |                        |                 |
   +------------------------+------------------------+-----------------+

.. _sect_P.3.3:

Substance Administration Logging SOP Class UID
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Substance Administration Logging SOP Class shall be uniquely
identified by the Substance Administration Logging SOP Class UID, which
shall have the value "1.2.840.10008.1.42".

.. _sect_P.3.4:

Substance Administration Logging Instance UID
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The well-known UID of the Substance Administration Logging SOP Instance
shall have the value "1.2.840.10008.1.42.1".

.. _sect_P.3.5:

Conformance Requirements
~~~~~~~~~~~~~~~~~~~~~~~~

The DICOM AE's Conformance Statement shall be formatted as defined in .

.. _sect_P.3.5.1:

SCU Conformance
^^^^^^^^^^^^^^^

The SCU shall document in its Conformance Statement the behavior and
actions that cause the SCU to generate an N-ACTION-RQ primitive.

The SCU shall document how it obtains the Patient ID (0010,0020) or
Admission ID (0038,0010) Attribute (e.g., through a Modality Worklist
query, bar-code scan, manual entry, etc.).

The SCU shall document the behavior and actions performed when a success
or failure status is received.

.. _sect_P.3.5.2:

SCP Conformance
^^^^^^^^^^^^^^^

The SCP shall document in its Conformance Statement how it uses the
information it receives for adding data to a Medication Administration
Record.

The SCP shall document the behavior and actions that cause the SCP to
generate a success or failure status for a received N-ACTION-RQ.

