.. _chapter_A:

Secure Use Profiles (Normative)
===============================

.. _sect_A.1:

Online Electronic Storage Secure Use Profile
--------------------------------------------

The Online Electronic Storage Secure Use Profile allows Application
Entities to track and verify the status of SOP Instances in those cases
where local security policies require tracking of the original Data Set
and subsequent copies.

The Conformance Statement shall indicate in what manner the system
restricts remote access.

.. _sect_A.1.1:

SOP Instance Status
~~~~~~~~~~~~~~~~~~~

An implementation that conforms to the Online Electronic Storage Secure
Use Profile shall conform to the following rules regarding the use of
the SOP Instance Status (0100,0410) Attribute with SOP Instances that
are transferred using the Storage Service Class:

a. An Application Entity that supports the Online Electronic Storage
   Secure Use Profile and that creates a SOP Instance intended for
   diagnostic use in Online Electronic Storage shall:

   1. Set the SOP Instance Status to Original (OR).

   2. Include the following Attributes:

      i.    the SOP Class UID (0008,0016) and SOP Instance UID
            (0008,0018)

      ii.   the Instance Creation Date (0008,0012) and Instance Creation
            Time (0008,0013), if known

      iii.  the SOP Instance Status

      iv.   the SOP Authorization Date and Time (0100,0420)

      v.    the SOP Authorization Comment, if any (0100,0424)

      vi.   the SOP Equipment Certification Number (0100,0426)

      vii.  the Study Instance UID (0020,000D) and Series Instance UID
            (0020,000E)

      viii. any Attributes of the General Equipment Module that are
            known

      ix.   any overlay data present

      x.    any image data present

b. The Application Entity that holds a SOP Instance where the SOP
   Instance Status is Original (OR) may change the SOP Instance Status
   to Authorized Original(AO) as long as the following rules are
   followed:

   1. The Application Entity shall determine that an authorized entity
      has certified the SOP Instance as useable for diagnostic purposes.

   2. The Application Entity shall change the SOP Instance Status to
      Authorized Original (AO). The SOP Instance UID shall not change.

   3. The Application Entity shall set the SOP Authorization Date and
      Time (0100,0420) and Authorization Equipment Certification Number
      (0100,0426) Attributes to appropriate values. It may also add an
      appropriate SOP Authorization Comment (0100,0424) Attribute.

c. There shall only be one Application Entity that holds a SOP Instance
   where the SOP Instance Status is Original (OR) or Authorized Original
   (AO). The Application Entity that holds such a SOP instance shall not
   delete it.

d. When communicating with an Application Entity that supports Online
   Electronic Storage the Application Entity that holds a SOP Instance
   where the SOP Instance Status is Original(OR) or Authorized
   Original(AO) may transfer that SOP Instance to another Application
   Entity that also conforms to the Online Electronic Storage Secure Use
   Profile as long as the following rules are followed:

   1. The transfer shall occur on a Secure Transport Connection.

   2. The two Application Entities involved in the transfer shall
      authenticate each other and shall confirm via the authentication
      that the other supports the Online Electronic Storage Secure Use
      Profile.

   3. The receiving Application Entity shall reject the storage request
      and discard the received SOP Instance if the data integrity checks
      done after the transfer indicate that the SOP Instance was altered
      during transmission.

   4. The transfer shall be confirmed using the push model of the
      Storage Commitment Service Class. Until it has completed this
      confirmation, the receiving Application Entity shall not forward
      the SOP Instance or Authorized Copies of the SOP instance to any
      other Application Entity.

   5. Once confirmed that the receiving Application Entity has
      successfully committed the SOP Instance to storage, the sending
      Application Entity shall do one of the following to its local copy
      of the SOP Instance:

      i.   delete the SOP Instance,

      ii.  change the SOP Instance Status to Not Specified (NS),

      iii. if the SOP Instance Status was Authorized Original (AO),
           change the SOP Instance Status to Authorized Copy (AC).

e. When communicating with an Application Entity that supports Online
   Electronic Storage an Application Entity that holds a SOP Instance
   whose SOP Instance Status is Authorized Original (AO) or Authorized
   Copy (AC) may send an Authorized Copy of the SOP Instance to another
   Application Entity as long as the following rules are followed:

   1. The transfer shall occur on a Secure Transport Connection.

   2. The two Application Entities involved in the transfer shall
      authenticate each other, and shall confirm via the authentication
      that the other supports the Online Electronic Storage Secure Use
      Profile.

   3. The sending Application Entity shall set the SOP Instance Status
      to either Not Specified (NS) or Authorized Copy (AC) in the copy
      sent. The SOP Instance UID shall not change.

   4. The receiving Application Entity shall reject the storage request
      and discard the copy if data integrity checks done after the
      transfer indicate that the SOP Instance was altered during
      transmission.

f. If communicating with a system that does not support the Online
   Electronic Storage Secure Use Profile, or if communication is not
   done over a Secure Transport Connection, then

   1. A sending Application Entity that conforms to this Security
      Profile shall either set the SOP Instance Status to Not Specified
      (NS), or leave out the SOP Instance Status and associated
      parameters of any SOP Instances that the sending Application
      Entity sends out over the unsecured Transport Connection or to
      systems that do not support the Online Electronic Storage Secure
      Use Profile.

   2. A receiving Application Entity that conforms to this Security
      Profile shall set the SOP Instance Status to Not Specified (NS) of
      any SOP Instance received over the unsecured Transport Connection
      or from systems that do not support the Online Electronic Storage
      Secure Use Profile.

g. The receiving Application Entity shall store SOP Instances in
   accordance with Level 2 as defined in the Storage Service Class
   (i.e., all Attributes, including Private Attributes), as required by
   the Storage Commitment Storage Service Class, and shall not coerce
   any Attribute other than SOP Instance Status, SOP Authorization Date
   and Time, Authorization Equipment Certification Number, and SOP
   Authorization Comment.

h. Other than changes to the SOP Instance Status, SOP Authorization Date
   and Time, Authorization Equipment Certification Number, and SOP
   Authorization Comment Attributes, as outlined above, or changes to
   group length Attributes to accommodate the aforementioned changes,
   the Application Entity shall not change any Attribute values.

.. _sect_A.2:

Basic Digital Signatures Secure Use Profile
-------------------------------------------

An implementation that validates and generates Digital Signatures may
claim conformance to the Basic Digital Signatures Secure Use Profile.
Any implementation that claims conformance to this Security Profile
shall obey the following rules in handling Digital Signatures:

a. The implementation shall store any SOP Instances that it receives in
   such a way that it guards against any unauthorized tampering of the
   SOP Instance.

b. Wherever possible, the implementation shall validate the Digital
   Signatures within any SOP Instance that it receives.

c. If the implementation sends the SOP Instance to another Application
   Entity, it shall do the following:

   1. remove any Digital Signatures that may have become invalid due to
      any allowed variations to the format of Attribute Values (e.g.,
      trimming of padding, alternate representations of numbers),

   2. generate one or more new Digital Signatures covering the Data
      Elements that the implementation was able to verify when the SOP
      Instance was received.

.. _sect_A.3:

Bit-preserving Digital Signatures Secure Use Profile
----------------------------------------------------

An implementation that stores and forwards SOP Instances may claim
conformance to the Bit-Preserving Digital Signatures Secure Use Profile.
Any implementation that claims conformance to this Security Profile
shall obey the following rules in handling Digital Signatures:

a. The implementation shall store any SOP Instances that it receives in
   such a way that when the SOP instance is forwarded to another
   Application Entity, the Value fields of all Attributes are
   bit-for-bit duplicates of the fields originally received.

b. The implementation shall not change the order of Items in a Sequence.

c. The implementation shall not remove or change any Data Element of any
   SOP Instance that it receives when sending that SOP Instance on to
   another Application Entity via DICOM. This includes any Digital
   Signatures received.

   .. note::

      Implementations may add new Data Elements that do not alter any
      existing Digital Signatures.

d. The implementation shall utilize an explicit VR Transfer Syntax.

   .. note::

      Implementations that cannot use an explicit VR Transfer Syntax
      cannot conform to this Secure Use Profile, since it may not be
      able to verify Digital Signatures that are received with an
      implicit VR Transfer Syntax.

e. The implementation shall not change the VR of any Data Element that
   it receives when it transmits that object to another Application
   Entity.

.. _sect_A.4:

Basic SR Digital Signatures Secure Use Profile
----------------------------------------------

Any implementation that claims conformance to this Security Profile
shall obey the following rules when creating a Structured Report or Key
Object Selection Document that includes Digital Signatures:

a. When the implementation signs a Structured Report or Key Object
   Selection Document SOP Instance the Digital Signatures shall be
   created in accordance with the Structured Report RSA Digital
   Signature Profile.

b. In every signed Structured Report or Key Object Selection Document
   SOP Instance created, all referenced SOP Instances listed in the
   Referenced SOP Sequence Items of the Current Requested Procedure
   Evidence Sequence (0040,A375) and Pertinent Other Evidence Sequence
   (0040,A385)shall include either a Referenced Digital Signature
   Sequence or a Referenced SOP Instance MAC Sequence. The references
   may include both.

The implementation claiming conformance shall outline in its conformance
statement the conditions under which it will either sign or not sign a
Structured Report or Key Object Selection Document.

.. _sect_A.5:

Audit Trail Message Format Profile
----------------------------------

To help assure healthcare privacy and security in automated systems,
usage data need to be collected. These data will be reviewed by
administrative staff to verify that healthcare data is being used in
accordance with the healthcare provider's data security requirements and
to establish accountability for data use. This data collection and
review process is called security auditing and the data itself comprises
the audit trail. Audit trails can be used for surveillance purposes to
detect when interesting events might be happening that warrant further
investigation.

This profile defines the format of the data to be collected and the
minimum set of attributes to be captured by healthcare application
systems for subsequent use by a review application. The data includes
records of who accessed healthcare data, when, for what action, from
where, and which patients' records were involved. No behavioral
requirements are specified for when audit messages are generated, or for
what action should be taken on their receipt. These are subject to local
policy decisions and legal requirements.

Any implementation that claims conformance to this Security Profile
shall:

a. format audit trail messages in accordance with the XML schema
   specified in `DICOM Audit Message Schema <#sect_A.5.1>`__ in a
   fashion that allows those messages to be validated against that XML
   schema, following the general conventions specified in `General
   Message Format Conventions <#sect_A.5.2>`__.

b. for the events described in this Profile comply with the restrictions
   specified by this Profile in `DICOM Specific Audit
   Messages <#sect_A.5.3>`__, and describe in its conformance statement
   any extensions.

   .. note::

      An implementation may include implementation-specific extensions
      as long as the above conditions are met.

c. describe in its conformance statement the events that it can detect
   and report,

d. describe in its conformance statement the processing it can perform
   upon receipt of a message

e. describe in its conformance statement how event reporting and
   processing can be configured

.. note::

   Other profiles specify the transmission of audit messages.

.. _sect_A.5.1:

DICOM Audit Message Schema
~~~~~~~~~~~~~~~~~~~~~~~~~~

Implementations claiming conformance to this profile shall use the
following XML schema to format audit trail messages. This schema is
derived from the schema specified in
`biblioentry_title <#biblio_RFC_3881>`__, according to W3C
Recommendation "XML Schema Part 1: Structures," version 1.0, May 2001,
and incorporates the DICOM extensions and restrictions outlined in
`General Message Format Conventions <#sect_A.5.2>`__.

This schema is provided in Relax NG Compact format.

.. note::

   This schema can be converted into an equivalent XML schema or other
   electronic format. It includes some modifications to the
   `biblioentry_title <#biblio_RFC_3881>`__ schema that reflect field
   experience with audit message requirements. It extends the
   `biblioentry_title <#biblio_RFC_3881>`__ schema.

.. _sect_A.5.1.1:

Audit Message Schema
^^^^^^^^^^^^^^^^^^^^

The following is the content of the audit schema:

::

   datatypes xsd = "http://www.w3.org/2001/XMLSchema-datatypes"

   # This defines the coded value type. The comment shows a pattern that can be used to further
   # constrain the token to limit it to the format of an OID. Not all schema software 
   # implementations support the pattern option for tokens.
   other-csd-attributes =
     (attribute codeSystemName { token } |     # OID pattern="[0-2]((\.0)|(\.[1-9][0-9]*))*"
        attribute codeSystemName { token }),   # This makes clear that codeSystemName is
                                               # either an OID or String 
     attribute displayName { token }?,
     attribute originalText { token }          # Note: this also corresponds to DICOM "Code Meaning"
   CodedValueType =
     attribute csd-code { token },
     other-csd-attributes

   # Define the event identification, used later

   EventIdentificationContents =
     element EventID { CodedValueType },
     element EventTypeCode { CodedValueType }*, # Note: DICOM/IHE defines and uses this
                                                # differently than RFC-3881
     attribute EventActionCode {                # Optional action code
       "C" |              ## Create
       "R" |              ## Read
       "U" |              ## Update
       "D" |              ## Delete
       "E"                ## Execute
     }?,
     
     attribute EventDateTime { xsd:dateTime },
     attribute EventOutcomeIndicator {
       "0" |            ## Nominal Success (use if status otherwise unknown or ambiguous)
       "4" |            ## Minor failure (per reporting application definition)
       "8" |            ## Serious failure (per reporting application definition)
       "12"             ## Major failure, (reporting application now unavailable)
     },
     
     element EventOutcomeDescription { text }?
     
   # Define AuditSourceIdentification, used later

   AuditSourceIdentificationContents =
     attribute AuditEnterpriseSiteID { token }?,
     attribute AuditSourceID { token },
     element AuditSourceTypeCode { AuditSourceTypeCodeContent }*

   # Define AuditSourceTypeCodeContent so that an isolated single digit
   # value is acceptable, or a token with other csd attributes so that
   # any controlled terminology can also be used.

   AuditSourceTypeCodeContent = 
     attribute csd-code {
       "1" |                 ## End-user display device, diagnostic device
       "2" |                 ## Data acquisition device or instrument
       "3" |                 ## Web Server process or thread
       "4" |                 ## Application Server process or thread
       "5" |                 ## Database Server process or thread
       "6" |                 ## Security server, e.g., a domain controller
       "7" |                 ## ISO level 1-3 network component
       "8" |                 ## ISO level 4-6 operating software
       "9" |                 ## other
       token },              ## other values are allowed if a codeSystemName is present
     other-csd-attributes?  ## If these are present, they define the meaning of code
     
   # Define ActiveParticipantType, used later

   ActiveParticipantContents =
     element RoleIDCode { CodedValueType }*,
     element MediaIdentifier {
       element MediaType { CodedValueType }
     }?,
     attribute UserID { text },
     attribute AlternativeUserID { text }?,
     attribute UserName { text }?,
     attribute UserIsRequestor { xsd:boolean },
     attribute NetworkAccessPointID { token }?,
     attribute NetworkAccessPointTypeCode {
       "1" |              ## Machine Name, including DNS name
       "2" |              ## IP Address
       "3" |              ## Telephone Number
       "4" |              ## Email address
       "5" }?             ## URI (user directory, HTTP-PUT, ftp, etc.)

   # The BinaryValuePair is used in ParticipantObject descriptions to capture parameters. 
   # All values (even those that are normally plain text) are encoded as xsd:base64Binary.
   # This is to preserve details of encoding (e.g., nulls) and to protect against text
   # contents that contain XML fragments. These are known attack points against applications,
   # so security logs can be expected to need to capture them without modification by the
   # audit encoding process.

   ValuePair =
     # clarify the name
     attribute type { token },
     attribute value { xsd:base64Binary } # used to encode potentially binary, malformed XML text, etc.

   # Define ParticipantObjectIdentification, used later

   # Participant Object Description, used later

   DICOMObjectDescriptionContents =
     element MPPS {
       attribute UID { token }       # OID pattern="[0-2]((\.0)|(\.[1-9][0-9]*))*"
     }*,
     element Accession {
       attribute Number { token }
     }*,
     element SOPClass {              # SOP class for one study
       element Instance {
         attribute UID { token }     # OID pattern="[0-2]((\.0)|(\.[1-9][0-9]*))*"
       }*,
       attribute UID { token }?,     # OID pattern="[0-2]((\.0)|(\.[1-9][0-9]*))*"
       attribute NumberOfInstances { xsd:integer }
     }*,
     element ParticipantObjectContainsStudy {
       element StudyIDs {
         attribute UID { token }
       }*
     }?,
     element Encrypted { xsd:boolean }?,
     element Anonymized { xsd:boolean }?

   ParticipantObjectIdentificationContents =
     element ParticipantObjectIDTypeCode { CodedValueType },
     (element ParticipantObjectName { token } |             # either a name or
     element ParticipantObjectQuery { xsd:base64Binary }),  # a query ID field,
     element ParticipantObjectDetail { ValuePair }*,   # optional details, these can be extensive
                                                       # and large
     element ParticipantObjectDescription { DICOMObjectDescriptionContents }*,
     attribute ParticipantObjectID { token },          # mandatory ID
     attribute ParticipantObjectTypeCode {             # optional type
       "1" | ## Person
       "2" | ## System object
       "3" | ## Organization
       "4"   ## Other
     }?,
     
     attribute ParticipantObjectTypeCodeRole {          ## optional role
       "1" |         ## Patient
       "2" |         ## Location
       "3" |         ## Report
       "4" |         ## Resource
       "5" |         ## Master File
       "6" |         ## User
       "7" |         ## List
       "8" |         ## Doctor
       "9" |         ## Subscriber
       "10" |        ## Guarantor
       "11" |        ## Security User Entity
       "12" |        ## Security User Group
       "13" |        ## Security Resource
       "14" |        ## Security Granularity Definition
       "15" |        ## Provider
       "16" |        ## Data Destination
       "17" |        ## Data Archive
       "18" |        ## Schedule
       "19" |        ## Customer
       "20" |        ## Job
       "21" |        ## Job Stream
       "22" |        ## Table
       "23" |        ## Routing Criteria
       "24" |        ## Query
       "25" |        ## Data Source
       "26"          ## Processing Element
       }?,
     
     attribute ParticipantObjectDataLifeCycle {          # optional life cycle stage
       "1" |         ## Origination, Creation
       "2" |         ## Import/ Copy
       "3" |         ## Amendment
       "4" |         ## Verification
       "5" |         ## Translation
       "6" |         ## Access/Use
       "7" |         ## De-identification
       "8" |         ## Aggregation, summarization, derivation
       "9" |         ## Report
       "10" |        ## Export
       "11" |        ## Disclosure
       "12" |        ## Receipt of Disclosure
       "13" |        ## Archiving
       "14" |        ## Logical deletion
       "15" }?,      ## Permanent erasure, physical destruction
     
     attribute ParticipantObjectSensitivity { token }?
     
   # The basic message
   message =
     element AuditMessage {
       (element EventIdentification { EventIdentificationContents }, # The event must be identified
        element ActiveParticipant { ActiveParticipantContents }+, # It has one or more active
                                                                  # participants
        element AuditSourceIdentification {                       # It is reported by one source
          AuditSourceIdentificationContents
        },
        element ParticipantObjectIdentification {                 # It may have other objects involved
          ParticipantObjectIdentificationContents
        }*)
     }

   # And finally the magic statement that message is the root of everything.
   start = message

       

.. _sect_A.5.1.2:

Codes Used Within The Schema
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The following value sets are defined in the audit schema above. These
are not coded terminology. They are values whose meaning depends upon
their use at the proper location within the message.

.. _sect_A.5.1.2.1:

Audit Source Type Code
''''''''''''''''''''''

The Audit Source Type Code values specify the type of source where an
event originated. Codes from coded terminologies and implementation
defined codes can also be used for the AuditSourceTypeCode.

.. table:: Audit Source Type Code Values

   ===== ======================================================
   Value Meaning
   ===== ======================================================
   1     End-user interface
   2     Data acquisition device or instrument
   3     Web server process tier in a multi-tier system
   4     Application server process tier in a multi-tier system
   5     Application server process tier in a multi-tier system
   6     Security server, e.g., a domain controller
   7     ISO level 1-3 network component
   8     ISO level 4-6 operating software
   9     External source, other or unknown type
   ===== ======================================================

.. _sect_A.5.1.2.2:

Participant Object Type Code Role
'''''''''''''''''''''''''''''''''

The Participant Object Type Code Role is an attribute of the
ParticipantObjectIdentification, and is not extensible. This attribute
may be omitted or one of the following values assigned. Coded
terminologies are not supported.

Table

.. table:: Participant Object Type Code Roles

   +-------+-----------------------------+-----------------------------+
   | Value | Meaning                     | Likely associated           |
   |       |                             | Participant Object Type     |
   |       |                             | Code                        |
   +=======+=============================+=============================+
   | 1     | Patient                     | 1 - Person                  |
   +-------+-----------------------------+-----------------------------+
   | 2     | Location                    | 3 - Organization            |
   +-------+-----------------------------+-----------------------------+
   | 3     | Report                      | 2 - System Object           |
   +-------+-----------------------------+-----------------------------+
   | 4     | Resource                    | 1 - Person, or              |
   |       |                             |                             |
   |       |                             | 3 - Organization            |
   +-------+-----------------------------+-----------------------------+
   | 5     | Master File                 | 2 - System Object           |
   +-------+-----------------------------+-----------------------------+
   | 6     | User                        | 1 - Person, or              |
   |       |                             |                             |
   |       |                             | 2 - System Object           |
   +-------+-----------------------------+-----------------------------+
   | 7     | List                        | 2 - System Object           |
   +-------+-----------------------------+-----------------------------+
   | 8     | Doctor                      | 1 - Person                  |
   +-------+-----------------------------+-----------------------------+
   | 9     | Subscriber                  | 3 - Organization            |
   +-------+-----------------------------+-----------------------------+
   | 10    | Guarantor                   | 1 - Person, or              |
   |       |                             |                             |
   |       |                             | 3 - Organization            |
   +-------+-----------------------------+-----------------------------+
   | 11    | Security User Entity        | 1 - Person, or              |
   |       |                             |                             |
   |       |                             | 2 - System Object           |
   +-------+-----------------------------+-----------------------------+
   | 12    | Security User Group         | 2 - System Object           |
   +-------+-----------------------------+-----------------------------+
   | 13    | Security Resource           | 2 - System Object           |
   +-------+-----------------------------+-----------------------------+
   | 14    | Security Granularity        | 2 - System Object           |
   |       | Definition                  |                             |
   +-------+-----------------------------+-----------------------------+
   | 15    | Provider                    | 1 - Person, or              |
   |       |                             |                             |
   |       |                             | 3 - Organization            |
   +-------+-----------------------------+-----------------------------+
   | 16    | Data Destination            | 2 - System Object           |
   +-------+-----------------------------+-----------------------------+
   | 17    | Data Repository             | 2 - System Object           |
   +-------+-----------------------------+-----------------------------+
   | 18    | Schedule                    | 2 - System Object           |
   +-------+-----------------------------+-----------------------------+
   | 19    | Customer                    | 3 - Organization            |
   +-------+-----------------------------+-----------------------------+
   | 20    | Job                         | 2 - System Object           |
   +-------+-----------------------------+-----------------------------+
   | 21    | Job Stream                  | 2 - System Object           |
   +-------+-----------------------------+-----------------------------+
   | 22    | Table                       | 2 - System Object           |
   +-------+-----------------------------+-----------------------------+
   | 23    | Routing Criteria            | 2 - System Object           |
   +-------+-----------------------------+-----------------------------+
   | 24    | Query                       | 2 - System Object           |
   +-------+-----------------------------+-----------------------------+

.. _sect_A.5.1.2.3:

Participant Object Data Life Cycle
''''''''''''''''''''''''''''''''''

The Participant Object Data Life Cycle is an attribute of the
ParticipantObjectIdentification, and is not extensible. This attribute
may be omitted or one of the following values assigned. Coded
terminologies are not supported.

.. table:: Participant Object Data Life Cycle Values

   ===== =========================================
   Value Meaning
   ===== =========================================
   1     Origination or Creation
   2     Import or Copy from original
   3     Amendment
   4     Verification
   5     Translation
   6     Access or Use
   7     De-identification
   8     Aggregation, summarization, derivation
   9     Report
   10    Export or Copy to target
   11    Disclosure
   12    Receipt of Disclosure
   13    Archiving
   14    Logical Deletion
   15    Permanent erasure or physical destruction
   ===== =========================================

.. _sect_A.5.1.2.4:

Participant Object ID Type Code
'''''''''''''''''''''''''''''''

The Participant Object ID Type Code describes the identifier that is
contained in Participant Object ID. Codes from coded terminologies and
implementation defined codes can also be used for the
ParticipantObjectTypeCodeRole.

.. table:: Participant Object ID Type Code Values

   +-------+------------------------+-----------------------------+
   | Value | Meaning                | Likely associated           |
   |       |                        | Participant Object Type     |
   |       |                        | Code                        |
   +=======+========================+=============================+
   | 1     | Medical Record Number  | 1 - Person                  |
   +-------+------------------------+-----------------------------+
   | 2     | Patient Number         | 1 - Person                  |
   +-------+------------------------+-----------------------------+
   | 3     | Encounter Number       | 1 - Person                  |
   +-------+------------------------+-----------------------------+
   | 4     | Enrollee Number        | 1 - Person                  |
   +-------+------------------------+-----------------------------+
   | 5     | Social Security Number | 1 - Person                  |
   +-------+------------------------+-----------------------------+
   | 6     | Account Number         | 1 - Person, or              |
   |       |                        |                             |
   |       |                        | 3 - Organization            |
   +-------+------------------------+-----------------------------+
   | 7     | Guarantor Number       | 1 - Person, or              |
   |       |                        |                             |
   |       |                        | 3 - Organization            |
   +-------+------------------------+-----------------------------+
   | 8     | Report Name            | 2 - System Object           |
   +-------+------------------------+-----------------------------+
   | 9     | Report Number          | 2 - System Object           |
   +-------+------------------------+-----------------------------+
   | 10    | Search Criteria        | 2 - System Object           |
   +-------+------------------------+-----------------------------+
   | 11    | User Identifier        | 1 - Person, or              |
   |       |                        |                             |
   |       |                        | 2 - System Object           |
   +-------+------------------------+-----------------------------+
   | 12    | URI                    | 2 - System Object           |
   +-------+------------------------+-----------------------------+

.. _sect_A.5.2:

General Message Format Conventions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The following table lists the primary fields from the message schema
specified in A.5.1, with additional instructions, conventions, and
restrictions on how DICOM applications shall fill in the field values.
The field names are leaf elements and attributes that are in the DICOM
Audit Message Schema (see `DICOM Audit Message Schema <#sect_A.5.1>`__).
Note that these fields may be enclosed in other XML elements, as
specified by the schema.

.. note::

   This schema, codes, and content were originally derived from
   `biblioentry_title <#biblio_RFC_3881>`__.
   `biblioentry_title <#biblio_RFC_3881>`__ is not being maintained or
   updated by the IETF, and has gradually diverged from the DICOM schema
   and codes. Other documents exist that refer to
   `biblioentry_title <#biblio_RFC_3881>`__ as the underlying standard.
   `biblioentry_title <#biblio_RFC_3881>`__ does not include corrections
   and additions to the audit schema made in DICOM since 2004.

In subsequent tables the following notation Is used for optionality:

M
   This element or attribute is mandatory

U
   This element or attribute is user optional. The creator may include
   it or omit it.

MC
   This element or attribute is mandatory if a specified condition is
   true.

UC
   This element or attribute may be present only if a specified
   condition is true, if the user chooses to include it.

.. table:: General Message Format

   +-------------+-------------+-------------+-------------+-------------+
   |             | Field Name  | Opt.        | Description | Additional  |
   |             |             |             |             | Conditions  |
   |             |             |             |             | on Field    |
   |             |             |             |             | F           |
   |             |             |             |             | ormat/Value |
   +=============+=============+=============+=============+=============+
   | Event       | EventID     | M           | Identifier  | The         |
   |             |             |             | for a       | identifier  |
   |             |             |             | specific    | for the     |
   |             |             |             | audited     | family of   |
   |             |             |             | event.      | event.      |
   |             |             |             |             | E.g., "User |
   |             |             |             |             | Authe       |
   |             |             |             |             | ntication". |
   |             |             |             |             |             |
   |             |             |             |             | D           |
   +-------------+-------------+-------------+-------------+-------------+
   | Even        | U           | Indicator   | C           |             |
   | tActionCode |             | for type of |    Create a |             |
   |             |             | action      |    new      |             |
   |             |             | performed   |    database |             |
   |             |             | during the  |    object,  |             |
   |             |             | event that  |    such as  |             |
   |             |             | generated   |    Placing  |             |
   |             |             | the audit.  |    an Order |             |
   |             |             |             |             |             |
   |             |             |             | R           |             |
   |             |             |             |             |             |
   |             |             |             |  Read/View/ |             |
   |             |             |             | Print/Query |             |
   |             |             |             |    Display  |             |
   |             |             |             |    or print |             |
   |             |             |             |    data,    |             |
   |             |             |             |    such as  |             |
   |             |             |             |    a Doctor |             |
   |             |             |             |    Census   |             |
   |             |             |             |             |             |
   |             |             |             | U           |             |
   |             |             |             |    Update   |             |
   |             |             |             |    data,    |             |
   |             |             |             |    such as  |             |
   |             |             |             |    Revise   |             |
   |             |             |             |    Patient  |             |
   |             |             |             |             |             |
   |             |             |             | Information |             |
   |             |             |             |             |             |
   |             |             |             | D           |             |
   |             |             |             |    Delete   |             |
   |             |             |             |    items,   |             |
   |             |             |             |    such as  |             |
   |             |             |             |    a master |             |
   |             |             |             |    file     |             |
   |             |             |             |    record   |             |
   |             |             |             |             |             |
   |             |             |             | E           |             |
   |             |             |             |    Perform  |             |
   |             |             |             |    a system |             |
   |             |             |             |    or       |             |
   |             |             |             |             |             |
   |             |             |             | application |             |
   |             |             |             |    function |             |
   |             |             |             |    such as  |             |
   |             |             |             |    log-on,  |             |
   |             |             |             |    program  |             |
   |             |             |             |             |             |
   |             |             |             |  execution, |             |
   |             |             |             |    or use   |             |
   |             |             |             |    of an    |             |
   |             |             |             |    object's |             |
   |             |             |             |    method   |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Ev          | M           | Universal   | The time at |             |
   | entDateTime |             | coordinated | which the   |             |
   |             |             | time (UTC), | audited     |             |
   |             |             | i.e., a     | event       |             |
   |             |             | date/time   | o           |             |
   |             |             | sp          | ccurred.See |             |
   |             |             | ecification | `EventDateT |             |
   |             |             | that is     | ime <#sect_ |             |
   |             |             | unambiguous | A.5.2.5>`__ |             |
   |             |             | as to local |             |             |
   |             |             | time zones. |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | EventOutco  | M           | Indicates   | 0           |             |
   | meIndicator |             | whether the |    Success  |             |
   |             |             | event       |             |             |
   |             |             | succeeded   | 4           |             |
   |             |             | or failed.  |    Minor    |             |
   |             |             |             |    failure; |             |
   |             |             |             |    action   |             |
   |             |             |             |             |             |
   |             |             |             |  restarted, |             |
   |             |             |             |    e.g.,    |             |
   |             |             |             |    invalid  |             |
   |             |             |             |    password |             |
   |             |             |             |    with     |             |
   |             |             |             |    first    |             |
   |             |             |             |    retry    |             |
   |             |             |             |             |             |
   |             |             |             | 8           |             |
   |             |             |             |    Serious  |             |
   |             |             |             |    failure; |             |
   |             |             |             |    action   |             |
   |             |             |             |             |             |
   |             |             |             | terminated, |             |
   |             |             |             |    e.g.,    |             |
   |             |             |             |    invalid  |             |
   |             |             |             |    password |             |
   |             |             |             |    with     |             |
   |             |             |             |    excess   |             |
   |             |             |             |    retries  |             |
   |             |             |             |             |             |
   |             |             |             | 12          |             |
   |             |             |             |    Major    |             |
   |             |             |             |    failure; |             |
   |             |             |             |    action   |             |
   |             |             |             |    made     |             |
   |             |             |             |    u        |             |
   |             |             |             | navailable, |             |
   |             |             |             |    e.g.,    |             |
   |             |             |             |    user     |             |
   |             |             |             |    account  |             |
   |             |             |             |    disabled |             |
   |             |             |             |    due to   |             |
   |             |             |             |             |             |
   |             |             |             |   excessive |             |
   |             |             |             |    invalid  |             |
   |             |             |             |    log-on   |             |
   |             |             |             |    attempts |             |
   |             |             |             |             |             |
   |             |             |             | When a      |             |
   |             |             |             | particular  |             |
   |             |             |             | event has   |             |
   |             |             |             | some        |             |
   |             |             |             | aspects     |             |
   |             |             |             | that        |             |
   |             |             |             | succeeded   |             |
   |             |             |             | and some    |             |
   |             |             |             | that        |             |
   |             |             |             | failed,     |             |
   |             |             |             | then one    |             |
   |             |             |             | message     |             |
   |             |             |             | shall be    |             |
   |             |             |             | generated   |             |
   |             |             |             | for         |             |
   |             |             |             | successful  |             |
   |             |             |             | actions and |             |
   |             |             |             | one message |             |
   |             |             |             | for the     |             |
   |             |             |             | failed      |             |
   |             |             |             | actions     |             |
   |             |             |             | (i.e., not  |             |
   |             |             |             | a single    |             |
   |             |             |             | message     |             |
   |             |             |             | with mixed  |             |
   |             |             |             | results).   |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Ev          | U           | Identifier  | The         |             |
   | entTypeCode |             | for the     | specific    |             |
   |             |             | category of | type(s)     |             |
   |             |             | event.      | within the  |             |
   |             |             |             | family      |             |
   |             |             |             | applicable  |             |
   |             |             |             | to the      |             |
   |             |             |             | event,      |             |
   |             |             |             | e.g., "User |             |
   |             |             |             | Login".     |             |
   |             |             |             |             |             |
   |             |             |             | D           |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Active      | UserID      | M           | Unique      | See         |
   | Participant |             |             | identifier  | `User       |
   | (mu         |             |             | for the     | ID <#sect_A |
   | lti-valued) |             |             | user        | .5.2.1>`__. |
   |             |             |             | actively    |             |
   |             |             |             | pa          |             |
   |             |             |             | rticipating |             |
   |             |             |             | in the      |             |
   |             |             |             | event.      |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Altern      | U           | Alternative | See         |             |
   | ativeUserID |             | unique      | `Alte       |             |
   |             |             | identifier  | rnativeUser |             |
   |             |             | for the     | ID <#sect_A |             |
   |             |             | user.       | .5.2.2>`__. |             |
   +-------------+-------------+-------------+-------------+-------------+
   | UserName    | U           | The         | See         |             |
   |             |             | human       | `Userna     |             |
   |             |             | -meaningful | me <#sect_A |             |
   |             |             | name for    | .5.2.3>`__. |             |
   |             |             | the user.   |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | User        | M           | Indicator   | Used to     |             |
   | IsRequestor |             | that the    | identify    |             |
   |             |             | user is or  | which of    |             |
   |             |             | is not the  | the         |             |
   |             |             | requestor,  | p           |             |
   |             |             | or          | articipants |             |
   |             |             | initiator,  | initiated   |             |
   |             |             | for the     | the         |             |
   |             |             | event being | transaction |             |
   |             |             | audited.    | being       |             |
   |             |             |             | audited. If |             |
   |             |             |             | the audit   |             |
   |             |             |             | source      |             |
   |             |             |             | cannot      |             |
   |             |             |             | determine   |             |
   |             |             |             | which of    |             |
   |             |             |             | the         |             |
   |             |             |             | p           |             |
   |             |             |             | articipants |             |
   |             |             |             | is the      |             |
   |             |             |             | requestor,  |             |
   |             |             |             | then the    |             |
   |             |             |             | field shall |             |
   |             |             |             | be present  |             |
   |             |             |             | with the    |             |
   |             |             |             | value FALSE |             |
   |             |             |             | in all      |             |
   |             |             |             | pa          |             |
   |             |             |             | rticipants. |             |
   |             |             |             |             |             |
   |             |             |             | The system  |             |
   |             |             |             | shall not   |             |
   |             |             |             | identify    |             |
   |             |             |             | multiple    |             |
   |             |             |             | p           |             |
   |             |             |             | articipants |             |
   |             |             |             | as          |             |
   |             |             |             | UserI       |             |
   |             |             |             | sRequestor. |             |
   |             |             |             | If there    |             |
   |             |             |             | are several |             |
   |             |             |             | known       |             |
   |             |             |             | requestors, |             |
   |             |             |             | the         |             |
   |             |             |             | reporting   |             |
   |             |             |             | system      |             |
   |             |             |             | shall pick  |             |
   |             |             |             | only one as |             |
   |             |             |             | UserI       |             |
   |             |             |             | sRequestor. |             |
   +-------------+-------------+-------------+-------------+-------------+
   | RoleIDCode  | U           | Sp          | D           |             |
   |             |             | ecification |             |             |
   |             |             | of the      | .. note::   |             |
   |             |             | role(s) the |             |             |
   |             |             | user plays  |    Usage of |             |
   |             |             | when        |    this     |             |
   |             |             | performing  |    field is |             |
   |             |             | the event,  |    refined  |             |
   |             |             | as assigned |    in the   |             |
   |             |             | in          |             |             |
   |             |             | role-based  |  individual |             |
   |             |             | access      |    message  |             |
   |             |             | control     |    d        |             |
   |             |             | security.   | escriptions |             |
   |             |             |             |    below.   |             |
   |             |             |             |    Other    |             |
   |             |             |             |             |             |
   |             |             |             |  additional |             |
   |             |             |             |    roles    |             |
   |             |             |             |    may also |             |
   |             |             |             |    be       |             |
   |             |             |             |    present, |             |
   |             |             |             |    since    |             |
   |             |             |             |    this is  |             |
   |             |             |             |    a        |             |
   |             |             |             |    m        |             |
   |             |             |             | ulti-valued |             |
   |             |             |             |    field.   |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Netw        | U           | An          | See         |             |
   | orkAccessPo |             | identifier  | `           |             |
   | intTypeCode |             | for the     | Multi-homed |             |
   |             |             | type of     | Nod         |             |
   |             |             | network     | es <#sect_A |             |
   |             |             | access      | .5.2.4>`__. |             |
   |             |             | point.      |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | NetworkAc   | U           | An          |             |             |
   | cessPointID |             | identifier  |             |             |
   |             |             | for the     |             |             |
   |             |             | network     |             |             |
   |             |             | access      |             |             |
   |             |             | point of    |             |             |
   |             |             | the user    |             |             |
   |             |             | device This |             |             |
   |             |             | could be a  |             |             |
   |             |             | device id,  |             |             |
   |             |             | IP address, |             |             |
   |             |             | or some     |             |             |
   |             |             | other       |             |             |
   |             |             | identifier  |             |             |
   |             |             | associated  |             |             |
   |             |             | with a      |             |             |
   |             |             | device.     |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Audit       | AuditEnter  | U           | Logical     | Serves to   |
   | Source      | priseSiteID |             | source      | further     |
   |             |             |             | location    | qualify the |
   |             |             |             | within the  | Audit       |
   |             |             |             | healthcare  | Source ID,  |
   |             |             |             | enterprise  | since Audit |
   |             |             |             | network,    | Source ID   |
   |             |             |             | e.g., a     | is not      |
   |             |             |             | hospital or | required to |
   |             |             |             | other       | be globally |
   |             |             |             | provider    | unique.     |
   |             |             |             | location    |             |
   |             |             |             | within a    |             |
   |             |             |             | m           |             |
   |             |             |             | ulti-entity |             |
   |             |             |             | provider    |             |
   |             |             |             | group.      |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Au          | M           | Identifier  | The         |             |
   | ditSourceID |             | of the      | ide         |             |
   |             |             | source.     | ntification |             |
   |             |             |             | of the      |             |
   |             |             |             | system that |             |
   |             |             |             | detected    |             |
   |             |             |             | the         |             |
   |             |             |             | auditable   |             |
   |             |             |             | event and   |             |
   |             |             |             | created     |             |
   |             |             |             | this audit  |             |
   |             |             |             | message.    |             |
   |             |             |             | Although    |             |
   |             |             |             | often the   |             |
   |             |             |             | audit       |             |
   |             |             |             | source is   |             |
   |             |             |             | one of the  |             |
   |             |             |             | pa          |             |
   |             |             |             | rticipants, |             |
   |             |             |             | it could    |             |
   |             |             |             | also be an  |             |
   |             |             |             | external    |             |
   |             |             |             | system that |             |
   |             |             |             | is          |             |
   |             |             |             | monitoring  |             |
   |             |             |             | the         |             |
   |             |             |             | activities  |             |
   |             |             |             | of the      |             |
   |             |             |             | p           |             |
   |             |             |             | articipants |             |
   |             |             |             | (e.g., an   |             |
   |             |             |             | add-on      |             |
   |             |             |             | audit       |             |
   |             |             |             | -generating |             |
   |             |             |             | device).    |             |
   +-------------+-------------+-------------+-------------+-------------+
   | AuditSou    | U           | Code        | See `Audit  |             |
   | rceTypeCode |             | specifying  | Source Type |             |
   |             |             | the type of | Code        |             |
   |             |             | source.     |  <#sect_A.5 |             |
   |             |             |             | .1.2.1>`__. |             |
   |             |             |             |             |             |
   |             |             |             | E.g., an    |             |
   |             |             |             | acquisition |             |
   |             |             |             | device      |             |
   |             |             |             | might use   |             |
   |             |             |             | "2" (data   |             |
   |             |             |             | acquisition |             |
   |             |             |             | device), a  |             |
   |             |             |             | PACS/RIS    |             |
   |             |             |             | system      |             |
   |             |             |             | might use   |             |
   |             |             |             | "4          |             |
   |             |             |             | "(          |             |
   |             |             |             | application |             |
   |             |             |             | server      |             |
   |             |             |             | process).   |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Participant | Par         | U           | Code for    | 1           |
   | Object      | ticipantObj |             | the         |    Person   |
   | (mu         | ectTypeCode |             | participant |             |
   | lti-valued) |             |             | object type | 2           |
   |             |             |             | being       |    System   |
   |             |             |             | audited.    |    Object   |
   |             |             |             | This value  |             |
   |             |             |             | is distinct | 3           |
   |             |             |             | from the    |    O        |
   |             |             |             | user's role | rganization |
   |             |             |             | or any user |             |
   |             |             |             | r           | 4           |
   |             |             |             | elationship |    Other    |
   |             |             |             | to the      |             |
   |             |             |             | participant |             |
   |             |             |             | object.     |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Partici     | U           | Code        | See         |             |
   | pantObjectT |             | r           | `           |             |
   | ypeCodeRole |             | epresenting | Participant |             |
   |             |             | the         | Object Type |             |
   |             |             | functional  | Code        |             |
   |             |             | application | Role        |             |
   |             |             | role of     |  <#sect_A.5 |             |
   |             |             | Participant | .1.2.2>`__. |             |
   |             |             | Object      |             |             |
   |             |             | being       |             |             |
   |             |             | audited.    |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Particip    | U           | Identifier  | See         |             |
   | antObjectDa |             | for the     | `           |             |
   | taLifeCycle |             | data        | Participant |             |
   |             |             | life-cycle  | Object Data |             |
   |             |             | stage for   | Life        |             |
   |             |             | the         | Cycle       |             |
   |             |             | participant |  <#sect_A.5 |             |
   |             |             | object.     | .1.2.3>`__. |             |
   |             |             | This can be |             |             |
   |             |             | used to     |             |             |
   |             |             | provide an  |             |             |
   |             |             | audit trail |             |             |
   |             |             | for data,   |             |             |
   |             |             | over time,  |             |             |
   |             |             | as it       |             |             |
   |             |             | passes      |             |             |
   |             |             | through the |             |             |
   |             |             | system.     |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Parti       | M           | Describes   | See         |             |
   | cipantObjec |             | the         | `           |             |
   | tIDTypeCode |             | identifier  | Participant |             |
   |             |             | that is     | Object ID   |             |
   |             |             | contained   | Type        |             |
   |             |             | in          | Cod         |             |
   |             |             | Participant | e <#sect_A. |             |
   |             |             | Object ID.  | 5.1.2.4>`__ |             |
   |             |             |             | and         |             |
   |             |             |             |             |             |
   |             |             |             | .. note::   |             |
   |             |             |             |             |             |
   |             |             |             |    Usage of |             |
   |             |             |             |    this     |             |
   |             |             |             |    field is |             |
   |             |             |             |    refined  |             |
   |             |             |             |    in the   |             |
   |             |             |             |             |             |
   |             |             |             |  individual |             |
   |             |             |             |    message  |             |
   |             |             |             |    d        |             |
   |             |             |             | escriptions |             |
   |             |             |             |    below.   |             |
   |             |             |             |    Multiple |             |
   |             |             |             |    roles    |             |
   |             |             |             |    may also |             |
   |             |             |             |    be       |             |
   |             |             |             |    present, |             |
   |             |             |             |    since    |             |
   |             |             |             |    this is  |             |
   |             |             |             |    a        |             |
   |             |             |             |    m        |             |
   |             |             |             | ulti-valued |             |
   |             |             |             |    field.   |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Partic      | U           | Denotes     | Locally     |             |
   | ipantObject |             | pol         | defined     |             |
   | Sensitivity |             | icy-defined | terms.      |             |
   |             |             | sensitivity |             |             |
   |             |             | for the     |             |             |
   |             |             | Participant |             |             |
   |             |             | Object ID   |             |             |
   |             |             | such as     |             |             |
   |             |             | VIP, HIV    |             |             |
   |             |             | status,     |             |             |
   |             |             | mental      |             |             |
   |             |             | health      |             |             |
   |             |             | status, or  |             |             |
   |             |             | similar     |             |             |
   |             |             | topics.     |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Particip    | M           | Identifies  | Usage       |             |
   | antObjectID |             | a specific  | refined by  |             |
   |             |             | instance of | individual  |             |
   |             |             | the         | message     |             |
   |             |             | participant | d           |             |
   |             |             | object.     | escriptions |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Participan  | U           | An          | Usage       |             |
   | tObjectName |             | instan      | refined by  |             |
   |             |             | ce-specific | individual  |             |
   |             |             | descriptor  | message     |             |
   |             |             | of the      | d           |             |
   |             |             | Participant | escriptions |             |
   |             |             | Object ID   |             |             |
   |             |             | audited,    |             |             |
   |             |             | such as a   |             |             |
   |             |             | person's    |             |             |
   |             |             | name.       |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Participant | U           | The actual  | Usage       |             |
   | ObjectQuery |             | query for a | refined by  |             |
   |             |             | query-type  | individual  |             |
   |             |             | participant | message     |             |
   |             |             | object.     | d           |             |
   |             |             |             | escriptions |             |
   +-------------+-------------+-------------+-------------+-------------+
   | P           | U           | Implementat | This        |             |
   | articipantO |             | ion-defined | element is  |             |
   | bjectDetail |             | data about  | a           |             |
   |             |             | specific    | Type-value  |             |
   |             |             | details of  | pair. The   |             |
   |             |             | the object  | "type"      |             |
   |             |             | accessed or | attribute   |             |
   |             |             | used.       | is an       |             |
   |             |             |             | implementat |             |
   |             |             |             | ion-defined |             |
   |             |             |             | text        |             |
   |             |             |             | string. The |             |
   |             |             |             | "value"     |             |
   |             |             |             | attribute   |             |
   |             |             |             | is base 64  |             |
   |             |             |             | encoded     |             |
   |             |             |             | data. The   |             |
   |             |             |             | value is    |             |
   |             |             |             | suitable    |             |
   |             |             |             | for         |             |
   |             |             |             | conveying   |             |
   |             |             |             | binary      |             |
   |             |             |             | data.       |             |
   +-------------+-------------+-------------+-------------+-------------+
   | SOPClass    | MC          |             | The UIDs of |             |
   |             |             |             | SOP classes |             |
   |             |             |             | referred to |             |
   |             |             |             | in this     |             |
   |             |             |             | participant |             |
   |             |             |             | object.     |             |
   |             |             |             |             |             |
   |             |             |             | Required if |             |
   |             |             |             | Parti       |             |
   |             |             |             | cipantObjec |             |
   |             |             |             | tIDTypeCode |             |
   |             |             |             | is (110180, |             |
   |             |             |             | DCM, "Study |             |
   |             |             |             | Instance    |             |
   |             |             |             | UID") and   |             |
   |             |             |             | any of the  |             |
   |             |             |             | optional    |             |
   |             |             |             | fields      |             |
   |             |             |             | (Acces      |             |
   |             |             |             | sionNumber, |             |
   |             |             |             | Co          |             |
   |             |             |             | ntainsMPPS, |             |
   |             |             |             | NumberO     |             |
   |             |             |             | fInstances, |             |
   |             |             |             | ContainsS   |             |
   |             |             |             | OPInstances |             |
   |             |             |             | ,Encrypted, |             |
   |             |             |             | Anonymized) |             |
   |             |             |             | are present |             |
   |             |             |             | in this     |             |
   |             |             |             | Participant |             |
   |             |             |             | Object. May |             |
   |             |             |             | be present  |             |
   |             |             |             | if          |             |
   |             |             |             | Parti       |             |
   |             |             |             | cipantObjec |             |
   |             |             |             | tIDTypeCode |             |
   |             |             |             | is (110180, |             |
   |             |             |             | DCM, "Study |             |
   |             |             |             | Instance    |             |
   |             |             |             | UID") even  |             |
   |             |             |             | though none |             |
   |             |             |             | of the      |             |
   |             |             |             | optional    |             |
   |             |             |             | fields are  |             |
   |             |             |             | present.    |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Accession   | U           |             | An          |             |
   |             |             |             | Accession   |             |
   |             |             |             | Number(s)   |             |
   |             |             |             | associated  |             |
   |             |             |             | with this   |             |
   |             |             |             | participant |             |
   |             |             |             | object.     |             |
   +-------------+-------------+-------------+-------------+-------------+
   | MPPS        | U           |             | An MPPS     |             |
   |             |             |             | Instance    |             |
   |             |             |             | UID(s)      |             |
   |             |             |             | associated  |             |
   |             |             |             | with this   |             |
   |             |             |             | participant |             |
   |             |             |             | object.     |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Number      | U           |             | The number  |             |
   | OfInstances |             |             | of SOP      |             |
   |             |             |             | Instances   |             |
   |             |             |             | referred to |             |
   |             |             |             | by this     |             |
   |             |             |             | participant |             |
   |             |             |             | object.     |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Instance    | U           |             | SOP         |             |
   |             |             |             | Instance    |             |
   |             |             |             | UID         |             |
   |             |             |             | value(s)    |             |
   |             |             |             |             |             |
   |             |             |             | .. note::   |             |
   |             |             |             |             |             |
   |             |             |             |             |             |
   |             |             |             |   Including |             |
   |             |             |             |    the list |             |
   |             |             |             |    of SOP   |             |
   |             |             |             |             |             |
   |             |             |             |   Instances |             |
   |             |             |             |    can      |             |
   |             |             |             |    create a |             |
   |             |             |             |    fairly   |             |
   |             |             |             |    large    |             |
   |             |             |             |    audit    |             |
   |             |             |             |    message. |             |
   |             |             |             |    Under    |             |
   |             |             |             |    most     |             |
   |             |             |             |    cir      |             |
   |             |             |             | cumstances, |             |
   |             |             |             |    the list |             |
   |             |             |             |    of SOP   |             |
   |             |             |             |    Instance |             |
   |             |             |             |    UIDs is  |             |
   |             |             |             |    not      |             |
   |             |             |             |    needed   |             |
   |             |             |             |    for      |             |
   |             |             |             |    audit    |             |
   |             |             |             |             |             |
   |             |             |             |   purposes. |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Encrypted   | U           |             | A single    |             |
   |             |             |             | value of    |             |
   |             |             |             | True or     |             |
   |             |             |             | False       |             |
   |             |             |             | indicating  |             |
   |             |             |             | whether or  |             |
   |             |             |             | not the     |             |
   |             |             |             | data was    |             |
   |             |             |             | encrypted.  |             |
   |             |             |             |             |             |
   |             |             |             | .. note::   |             |
   |             |             |             |             |             |
   |             |             |             |    If there |             |
   |             |             |             |    was a    |             |
   |             |             |             |    mix of   |             |
   |             |             |             |             |             |
   |             |             |             |   encrypted |             |
   |             |             |             |    and      |             |
   |             |             |             |    no       |             |
   |             |             |             | n-encrypted |             |
   |             |             |             |    data,    |             |
   |             |             |             |    then     |             |
   |             |             |             |    create   |             |
   |             |             |             |    two      |             |
   |             |             |             |    event    |             |
   |             |             |             |    reports. |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Anonymized  | U           |             | A single    |             |
   |             |             |             | value of    |             |
   |             |             |             | True or     |             |
   |             |             |             | False       |             |
   |             |             |             | indicating  |             |
   |             |             |             | whether or  |             |
   |             |             |             | not all     |             |
   |             |             |             | patient     |             |
   |             |             |             | identifying |             |
   |             |             |             | information |             |
   |             |             |             | was removed |             |
   |             |             |             | from the    |             |
   |             |             |             | data        |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Particip    | U           |             | A Study     |             |
   | antObjectCo |             |             | Instance    |             |
   | ntainsStudy |             |             | UID, which  |             |
   |             |             |             | may be used |             |
   |             |             |             | when the    |             |
   |             |             |             | Parti       |             |
   |             |             |             | cipantObjec |             |
   |             |             |             | tIDTypeCode |             |
   |             |             |             | is not      |             |
   |             |             |             | (110180,    |             |
   |             |             |             | DCM, "Study |             |
   |             |             |             | Instance    |             |
   |             |             |             | UID").      |             |
   +-------------+-------------+-------------+-------------+-------------+

.. _sect_A.5.2.1:

UserID
^^^^^^

If the participant is a person, then the User ID shall be the identifier
used for that person on this particular system, in the form of
loginName@domain-name.

If the participant is an identifiable process, the UserID selected shall
be one of the identifiers used in the internal system logs. For example,
the User ID may be the process ID as used within the local operating
system in the local system logs. If the participant is a node, then User
ID may be the node name assigned by the system administrator. Other
participants such as threads, relocatable processes, web service
end-points, web server dispatchable threads, etc. will have an
appropriate identifier. The implementation shall document in the
conformance statement the identifiers used, see `Audit Trail Message
Transmission Profile - SYSLOG-TLS <#sect_A.6>`__. The purpose of this
requirement is to allow matching of the audit log identifiers with
internal system logs on the reporting systems. .

When importing or exporting data, e.g., by means of media, the UserID
field is used both to identify people and to identify the media itself.
When the Role ID Code is EV(110154, DCM, "Destination Media") or
EV(110155, DCM, "Source Media"), the UserID may be:

a. a URI (the preferred form) identifying the source or destination,

b. an email address of the form "mailto:user@address"

c. a description of the media type (e.g., DVD) together with a
   description of its identifying label, as a free text field,

d. a description of the media type (e.g., paper, film) together with a
   description of the location of the media creator (i.e., the printer).

The UserID field for Media needs to be highly flexible given the large
variety of media and transports that might be used.

.. _sect_A.5.2.2:

AlternativeUserID
^^^^^^^^^^^^^^^^^

If the participant is a person, then Alternative User ID shall be the
identifier used for that person within an enterprise for authentication
purposes, for example, a Kerberos Username (user@realm). If the
participant is a DICOM application, then Alternative User ID shall be
one or more of the AE Titles that participated in the event. Multiple AE
titles shall be encoded as:

AETITLES= *aetitle1;aetitle2;…*

When importing or exporting data, e.g., by means of media, the
Alternative UserID field is used either to identify people or to
identify the media itself. When the Role ID Code is (110154, DCM,
"Destination Media") or (110155, DCM, "Source Media"), the Alternative
UserID may be any machine readable identifications on the media, such as
media serial number, volume label, or DICOMDIR SOP Instance UID.

.. _sect_A.5.2.3:

Username
^^^^^^^^

A human readable identification of the participant. If the participant
is a person, the person's name shall be used. If the participant is a
process, then the process name shall be used.

.. _sect_A.5.2.4:

Multi-homed Nodes
^^^^^^^^^^^^^^^^^

The NetworkAccessPointTypeCode and NetworkAccessPointID can be ambiguous
for systems that have multiple physical network connections. For these
multi-homed nodes a single DNS name or IP address shall be selected and
used when reporting audit events. DICOM does not require the use of a
specific method for selecting the network connection to be used for
identification, but it must be the same for all of the audit messages
generated for events on that node.

.. _sect_A.5.2.5:

EventDateTime
^^^^^^^^^^^^^

The EventDateTime is the date and time that the event being reported
took place. Some events have a significant duration. In these cases, a
date and time shall be chosen by a method that is consistent and
appropriate for the event being reported.

The EventDateTime shall include the time zone information.

Creators of audit messages may support leap-seconds, but are not
required to. Recipients of audit messages shall be able to process
messages with leap-second information.

.. _sect_A.5.2.6:

ParticipantObjectTypeCodeRole
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The ParticipantObjectTypeCodeRole identifies the role that the object
played in the event that is being reported. Most events involve multiple
participating objects. ParticipantObjectTypeCodeRole identifies which
object took which role in the event. It also covers agents,
multi-purpose entities, and multi-role entities. For the purpose of the
event one primary role is chosen.

.. table:: ParticipantObjectTypeCodeRole

   +------+------------------------------+------------------------------+
   | Code | Short Description            | Description                  |
   +======+==============================+==============================+
   | 1    | Patient                      | This object is the patient   |
   |      |                              | that is the subject of care  |
   |      |                              | related to this event. It is |
   |      |                              | identifiable by patient ID   |
   |      |                              | or equivalent. The patient   |
   |      |                              | may be either human or       |
   |      |                              | animal.                      |
   +------+------------------------------+------------------------------+
   | 2    | Location                     | This is a location           |
   |      |                              | identified as related to the |
   |      |                              | event. This is usually the   |
   |      |                              | location where the event     |
   |      |                              | took place. Note that for    |
   |      |                              | shipping, the usual events   |
   |      |                              | are arrival at a location or |
   |      |                              | departure from a location.   |
   +------+------------------------------+------------------------------+
   | 3    | Report                       | This object is any kind of   |
   |      |                              | persistent document created  |
   |      |                              | as a result of the event.    |
   |      |                              | This could be a paper        |
   |      |                              | report, film, electronic     |
   |      |                              | report, DICOM Study, etc.    |
   |      |                              | Issues related to medical    |
   |      |                              | records life cycle           |
   |      |                              | management are conveyed      |
   |      |                              | elsewhere.                   |
   +------+------------------------------+------------------------------+
   | 4    | Resource                     | (deprecated)                 |
   +------+------------------------------+------------------------------+
   | 5    | Master File                  | This is any configurable     |
   |      |                              | file used to control         |
   |      |                              | creation of documents or     |
   |      |                              | behavior. Examples include   |
   |      |                              | the objects maintained by    |
   |      |                              | the HL7 Master File          |
   |      |                              | transactions, Value Sets,    |
   |      |                              | etc.                         |
   +------+------------------------------+------------------------------+
   | 6    | User                         | A human participant not      |
   |      |                              | otherwise identified by some |
   |      |                              | other category               |
   +------+------------------------------+------------------------------+
   | 7    | List                         | (deprecated)                 |
   +------+------------------------------+------------------------------+
   | 8    | Doctor                       | A person who is providing or |
   |      |                              | performing care related to   |
   |      |                              | the event, generally a       |
   |      |                              | physician. The key           |
   |      |                              | distinction between doctor   |
   |      |                              | and provider is the nature   |
   |      |                              | of their participation. The  |
   |      |                              | doctor is the human who      |
   |      |                              | actually performed the work. |
   |      |                              | The provider is the human or |
   |      |                              | organization that is         |
   |      |                              | responsible for the work.    |
   +------+------------------------------+------------------------------+
   | 9    | Subscriber                   | A person or system that is   |
   |      |                              | being notified as part of    |
   |      |                              | the event. This is relevant  |
   |      |                              | in situations where          |
   |      |                              | automated systems provide    |
   |      |                              | notifications to other       |
   |      |                              | parties when an event took   |
   |      |                              | place.                       |
   +------+------------------------------+------------------------------+
   | 10   | Guarantor                    | Insurance company, or any    |
   |      |                              | other organization who       |
   |      |                              | accepts responsibility for   |
   |      |                              | paying for the healthcare    |
   |      |                              | event.                       |
   +------+------------------------------+------------------------------+
   | 11   | Security User Entity         | A person or active system    |
   |      |                              | object involved in the event |
   |      |                              | with a security role.        |
   +------+------------------------------+------------------------------+
   | 12   | Security User Group          | (deprecated)                 |
   +------+------------------------------+------------------------------+
   | 13   | Security Resource            | A passive object, such as a  |
   |      |                              | role table, that is relevant |
   |      |                              | to the event.                |
   +------+------------------------------+------------------------------+
   | 14   | Security Granularity         | (deprecated) Relevant to     |
   |      | Definition                   | certain RBAC security        |
   |      |                              | methodologies.               |
   +------+------------------------------+------------------------------+
   | 15   | Provider                     | A person or organization     |
   |      |                              | responsible for providing    |
   |      |                              | care. This encompasses all   |
   |      |                              | forms of care, licensed or   |
   |      |                              | otherwise, and all sorts of  |
   |      |                              | teams and care groups. Note, |
   |      |                              | the distinction between      |
   |      |                              | providers and the doctor     |
   |      |                              | that actually provided the   |
   |      |                              | care to the patient.         |
   +------+------------------------------+------------------------------+
   | 16   | Data Destination             | The destination for data     |
   |      |                              | transfer, when some other    |
   |      |                              | role is not appropriate.     |
   +------+------------------------------+------------------------------+
   | 17   | Data Archive                 | A source or destination for  |
   |      |                              | data transfer that acts as   |
   |      |                              | an archive, database, or     |
   |      |                              | similar role.                |
   +------+------------------------------+------------------------------+
   | 18   | Schedule                     | An object that holds         |
   |      |                              | schedule information. This   |
   |      |                              | could be an appointment      |
   |      |                              | book, availability           |
   |      |                              | information, etc.            |
   +------+------------------------------+------------------------------+
   | 19   | Customer                     | An organization or person    |
   |      |                              | that is the recipient of     |
   |      |                              | services. This could be an   |
   |      |                              | organization that is getting |
   |      |                              | services for a patient, or a |
   |      |                              | person that is getting       |
   |      |                              | services for an animal.      |
   +------+------------------------------+------------------------------+
   | 20   | Job                          | An order, task, work item,   |
   |      |                              | procedure step, or other     |
   |      |                              | description of work to be    |
   |      |                              | performed. E.g., a           |
   |      |                              | particular instance of an    |
   |      |                              | MPPS.                        |
   +------+------------------------------+------------------------------+
   | 21   | Job Stream                   | A list of jobs or a system   |
   |      |                              | that provides lists of jobs. |
   |      |                              | E.g., an MWL SCP.            |
   +------+------------------------------+------------------------------+
   | 22   | Table                        | (Deprecated)                 |
   +------+------------------------------+------------------------------+
   | 23   | Routing Criteria             | An object that specifies or  |
   |      |                              | controls the routing or      |
   |      |                              | delivery of items. For       |
   |      |                              | example, a distribution list |
   |      |                              | is the routing criteria for  |
   |      |                              | mail. The items delivered    |
   |      |                              | may be documents, jobs, or   |
   |      |                              | other objects.               |
   +------+------------------------------+------------------------------+
   | 24   | Query                        | The contents of a query.     |
   |      |                              | This is used to capture the  |
   |      |                              | contents of any kind of      |
   |      |                              | query. For security          |
   |      |                              | surveillance purposes        |
   |      |                              | knowing the queries being    |
   |      |                              | made is very important.      |
   +------+------------------------------+------------------------------+
   | 25   | Data Source                  | The source or origin of      |
   |      |                              | data, when there is no other |
   |      |                              | matching role available.     |
   +------+------------------------------+------------------------------+
   | 26   | Processing Element           | A data processing element    |
   |      |                              | that creates, analyzes,      |
   |      |                              | modifies, or manipulates     |
   |      |                              | data as part of this event.  |
   +------+------------------------------+------------------------------+

.. _sect_A.5.3:

DICOM Specific Audit Messages
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The following subsections define message specializations for use by
implementations that claim conformance to the DICOM Audit Trail Profile.
Any field (i.e., XML element and associated attributes) not specifically
mentioned in the following tables shall follow the conventions specified
in `DICOM Audit Message Schema <#sect_A.5.1>`__ and `General Message
Format Conventions <#sect_A.5.2>`__.

An implementation claiming conformance to this Profile that reports an
activity covered by one of the audit messages defined by this Profile
shall use the message format defined in this Profile. However, a system
claiming conformance to this Profile is not required to send a message
each time the activity reported by that audit message occurs. It is
expected that the triggering of audit messages would be configurable on
an individual basis, to be able to balance network load versus the
severity of threats, in accordance with local security policies.

.. note::

   1. It is a system design issue outside the scope of DICOM as to what
      entity actually sends an audit event and when. For example, a
      Query message could be generated by the entity where the query
      originated, by the entity that eventually would respond to the
      query, or by a monitoring entity not directly involved with the
      query, but that generates audit messages based on monitored
      network traffic.

   2. To report events that are similar to the events described here,
      these definitions can be used as the basis for extending the
      schema.

In the subsequent tables, the information entity column indicates the
relationship between real world entities and the information elements
encoded into the message.

.. _sect_A.5.3.1:

Application Activity
^^^^^^^^^^^^^^^^^^^^

This audit message describes the event of an Application Entity starting
or stopping. This is closely related to the more general case of any
kind of application startup or shutdown, and may be suitable for those
purposes also.

.. table:: Application Activity Message

   +-----------------+------------+-----------------+-----------------+
   | Real World      | Field Name | Opt.            | Value           |
   | Entities        |            |                 | Constraints     |
   +=================+============+=================+=================+
   | Event           | EventID    | M               | EV (110100,     |
   |                 |            |                 | DCM,            |
   |                 |            |                 | "Application    |
   |                 |            |                 | Activity")      |
   +-----------------+------------+-----------------+-----------------+
   | EventActionCode | M          | Enumerated      |                 |
   |                 |            | Value           |                 |
   |                 |            |                 |                 |
   |                 |            | E = Execute     |                 |
   +-----------------+------------+-----------------+-----------------+
   | EventDateTime   | M          | not specialized |                 |
   +-----------------+------------+-----------------+-----------------+
   | EventO          | M          | not specialized |                 |
   | utcomeIndicator |            |                 |                 |
   +-----------------+------------+-----------------+-----------------+
   | EventTypeCode   | M          | DT (110120,     |                 |
   |                 |            | DCM,            |                 |
   |                 |            | "Application    |                 |
   |                 |            | Start")         |                 |
   |                 |            |                 |                 |
   |                 |            | DT (110121,     |                 |
   |                 |            | DCM,            |                 |
   |                 |            | "Application    |                 |
   |                 |            | Stop")          |                 |
   +-----------------+------------+-----------------+-----------------+
   | Active          | UserID     | M               | The identity of |
   | Participant:    |            |                 | the process     |
   |                 |            |                 | started or      |
   | Application     |            |                 | stopped         |
   | started (1)     |            |                 | formatted as    |
   |                 |            |                 | specified in    |
   |                 |            |                 | A.5.2.1.        |
   +-----------------+------------+-----------------+-----------------+
   | Al              | MC         | If the process  |                 |
   | ternativeUserID |            | supports DICOM, |                 |
   |                 |            | then the AE     |                 |
   |                 |            | Titles as       |                 |
   |                 |            | specified in    |                 |
   |                 |            | A.5.2.2.        |                 |
   +-----------------+------------+-----------------+-----------------+
   | UserName        | U          | not specialized |                 |
   +-----------------+------------+-----------------+-----------------+
   | UserIsRequestor | M          | not specialized |                 |
   +-----------------+------------+-----------------+-----------------+
   | RoleIDCode      | M          | EV (110150,     |                 |
   |                 |            | DCM,            |                 |
   |                 |            | "Application")  |                 |
   +-----------------+------------+-----------------+-----------------+
   | NetworkAcce     | U          | not specialized |                 |
   | ssPointTypeCode |            |                 |                 |
   +-----------------+------------+-----------------+-----------------+
   | Netwo           | U          | not specialized |                 |
   | rkAccessPointID |            |                 |                 |
   +-----------------+------------+-----------------+-----------------+
   | Active          | UserID     | M               | The person or   |
   | Participant:    |            |                 | process         |
   |                 |            |                 | starting or     |
   | Persons and or  |            |                 | stopping the    |
   | processes that  |            |                 | Application     |
   | started the     |            |                 |                 |
   | Application     |            |                 |                 |
   | (0..N)          |            |                 |                 |
   +-----------------+------------+-----------------+-----------------+
   | Al              | U          | not specialized |                 |
   | ternativeUserID |            |                 |                 |
   +-----------------+------------+-----------------+-----------------+
   | UserName        | U          | not specialized |                 |
   +-----------------+------------+-----------------+-----------------+
   | UserIsRequestor | M          | not specialized |                 |
   +-----------------+------------+-----------------+-----------------+
   | RoleIDCode      | M          | EV (110151,     |                 |
   |                 |            | DCM,            |                 |
   |                 |            | "Application    |                 |
   |                 |            | Launcher")      |                 |
   +-----------------+------------+-----------------+-----------------+
   | NetworkAcce     | U          | not specialized |                 |
   | ssPointTypeCode |            |                 |                 |
   +-----------------+------------+-----------------+-----------------+
   | Netwo           | U          | not specialized |                 |
   | rkAccessPointID |            |                 |                 |
   +-----------------+------------+-----------------+-----------------+

No Participant Objects are needed for this message.

.. _sect_A.5.3.2:

Audit Log Used
^^^^^^^^^^^^^^

This message describes the event of a person or process reading a log of
audit trail information.

.. note::

   For example, an implementation that maintains a local cache of audit
   information that has not been transferred to a central collection
   point might generate this message if its local cache were accessed by
   a user.

.. table:: Audit Log Used Message

   +----------------+----------------+----------------+----------------+
   | Real World     | Field Name     | Opt.           | Value          |
   | Entities       |                |                | Constraints    |
   +================+================+================+================+
   | Event          | EventID        | M              | EV (110101,    |
   |                |                |                | DCM, "Audit    |
   |                |                |                | Log Used")     |
   +----------------+----------------+----------------+----------------+
   | E              | M              | Shall be       |                |
   | ventActionCode |                | enumerated     |                |
   |                |                | value:         |                |
   |                |                |                |                |
   |                |                | R = read       |                |
   +----------------+----------------+----------------+----------------+
   | EventDateTime  | M              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | EventOu        | M              | not            |                |
   | tcomeIndicator |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | EventTypeCode  | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Active         | UserID         | M              | The person or  |
   | Participant:   |                |                | process        |
   |                |                |                | accessing the  |
   | Persons and or |                |                | audit trail.   |
   | processes that |                |                | If both are    |
   | started the    |                |                | known, then    |
   | Application    |                |                | two active     |
   | (1..2)         |                |                | participants   |
   |                |                |                | shall be       |
   |                |                |                | included (both |
   |                |                |                | the person and |
   |                |                |                | the process).  |
   +----------------+----------------+----------------+----------------+
   | Alt            | U              | not            |                |
   | ernativeUserID |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | UserName       | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | U              | M              | not            |                |
   | serIsRequestor |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | RoleIDCode     | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | NetworkAcces   | U              | not            |                |
   | sPointTypeCode |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Networ         | U              | not            |                |
   | kAccessPointID |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Participating  | Participant    | M              | Shall be: 2 =  |
   | Object:        | ObjectTypeCode |                | system         |
   |                |                |                |                |
   | Identity of    |                |                |                |
   | the audit log  |                |                |                |
   | (1)            |                |                |                |
   +----------------+----------------+----------------+----------------+
   | P              | M              | Shall be: 13 = |                |
   | articipantObje |                | security       |                |
   | ctTypeCodeRole |                | resource       |                |
   +----------------+----------------+----------------+----------------+
   | Pa             | U              | not            |                |
   | rticipantObjec |                | specialized    |                |
   | tDataLifeCycle |                |                |                |
   +----------------+----------------+----------------+----------------+
   | ParticipantOb  | M              | Shall be: 12 = |                |
   | jectIDTypeCode |                | EV (12,        |                |
   |                |                | RFC-3881,      |                |
   |                |                | "URI")         |                |
   +----------------+----------------+----------------+----------------+
   | ParticipantObj | U              | not            |                |
   | ectSensitivity |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Parti          | M              | The URI of the |                |
   | cipantObjectID |                | audit log      |                |
   +----------------+----------------+----------------+----------------+
   | Partici        | U              | Shall be:      |                |
   | pantObjectName |                | "Security      |                |
   |                |                | Audit Log"     |                |
   +----------------+----------------+----------------+----------------+
   | Particip       | U              | not            |                |
   | antObjectQuery |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Participa      | U              | not            |                |
   | ntObjectDetail |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | ParticipantObj | U              | not            |                |
   | ectDescription |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | SOPClass       | U              | See `General   |                |
   |                |                | Message Format |                |
   |                |                | Conventions <# |                |
   |                |                | sect_A.5.2>`__ |                |
   +----------------+----------------+----------------+----------------+
   | Accession      | U              | See `General   |                |
   |                |                | Message Format |                |
   |                |                | Conventions <# |                |
   |                |                | sect_A.5.2>`__ |                |
   +----------------+----------------+----------------+----------------+
   | Num            | U              | See `General   |                |
   | berOfInstances |                | Message Format |                |
   |                |                | Conventions <# |                |
   |                |                | sect_A.5.2>`__ |                |
   +----------------+----------------+----------------+----------------+
   | Instances      | U              | See `General   |                |
   |                |                | Message Format |                |
   |                |                | Conventions <# |                |
   |                |                | sect_A.5.2>`__ |                |
   +----------------+----------------+----------------+----------------+
   | Encrypted      | U              | See `General   |                |
   |                |                | Message Format |                |
   |                |                | Conventions <# |                |
   |                |                | sect_A.5.2>`__ |                |
   +----------------+----------------+----------------+----------------+
   | Anonymized     | U              | See `General   |                |
   |                |                | Message Format |                |
   |                |                | Conventions <# |                |
   |                |                | sect_A.5.2>`__ |                |
   +----------------+----------------+----------------+----------------+
   | Pa             | U              | See `General   |                |
   | rticipantObjec |                | Message Format |                |
   | tContainsStudy |                | Conventions <# |                |
   |                |                | sect_A.5.2>`__ |                |
   +----------------+----------------+----------------+----------------+

.. _sect_A.5.3.3:

Begin Transferring DICOM Instances
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This message describes the event of a system beginning to transfer a set
of DICOM instances from one node to another node within control of the
system's security domain. This message may only include information
about a single patient.

.. note::

   A separate Instances Transferred message is defined for transfer
   completion, allowing comparison of what was intended to be sent and
   what was actually sent.

.. table:: Audit Message for Begin Transferring DICOM Instances

   +----------------+----------------+----------------+----------------+
   | Real World     | Field Name     | Opt.           | Value          |
   | Entities       |                |                | Constraints    |
   +================+================+================+================+
   | Event          | EventID        | M              | EV (110102,    |
   |                |                |                | DCM, "Begin    |
   |                |                |                | Transferring   |
   |                |                |                | DICOM          |
   |                |                |                | Instances")    |
   +----------------+----------------+----------------+----------------+
   | E              | M              | Shall be: E =  |                |
   | ventActionCode |                | Execute        |                |
   +----------------+----------------+----------------+----------------+
   | EventDateTime  | M              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | EventOu        | M              | not            |                |
   | tcomeIndicator |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | EventTypeCode  | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Active         | UserID         | M              | The identity   |
   | Participant:   |                |                | of the process |
   |                |                |                | sending the    |
   | Process        |                |                | data.          |
   | Sending the    |                |                |                |
   | Data (1)       |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Alt            | U              | not            |                |
   | ernativeUserID |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | UserName       | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | U              | M              | not            |                |
   | serIsRequestor |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | RoleIDCode     | M              | EV (110153,    |                |
   |                |                | DCM, "Source   |                |
   |                |                | Role ID")      |                |
   +----------------+----------------+----------------+----------------+
   | NetworkAcces   | U              | not            |                |
   | sPointTypeCode |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Networ         | U              | not            |                |
   | kAccessPointID |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Active         | UserID         | M              | The identity   |
   | Participant:   |                |                | of the process |
   |                |                |                | receiving the  |
   | Process        |                |                | data.          |
   | receiving the  |                |                |                |
   | data (1)       |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Alt            | U              | not            |                |
   | ernativeUserID |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | UserName       | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | U              | M              | not            |                |
   | serIsRequestor |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | RoleIDCode     | M              | EV (110152,    |                |
   |                |                | DCM,           |                |
   |                |                | "Destination   |                |
   |                |                | Role ID")      |                |
   +----------------+----------------+----------------+----------------+
   | NetworkAcces   | U              | not            |                |
   | sPointTypeCode |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Networ         | U              | not            |                |
   | kAccessPointID |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Active         | UserID         | M              | The identity   |
   | Participant:   |                |                | of any other   |
   |                |                |                | participants   |
   | Other          |                |                | that might be  |
   | Participants   |                |                | involved and   |
   | (0..N)         |                |                | known,         |
   |                |                |                | especially     |
   |                |                |                | third parties  |
   |                |                |                | that are the   |
   |                |                |                | requestor      |
   +----------------+----------------+----------------+----------------+
   | Alt            | U              | not            |                |
   | ernativeUserID |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | UserName       | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | U              | M              | not            |                |
   | serIsRequestor |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | RoleIDCode     | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | NetworkAcces   | U              | not            |                |
   | sPointTypeCode |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Networ         | U              | not            |                |
   | kAccessPointID |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Participating  | Participant    | M              | Shall be: 2 =  |
   | Object:        | ObjectTypeCode |                | system         |
   |                |                |                |                |
   | Studies being  |                |                |                |
   | transferred    |                |                |                |
   | (1..N)         |                |                |                |
   +----------------+----------------+----------------+----------------+
   | P              | M              | Shall be: 3 =  |                |
   | articipantObje |                | report         |                |
   | ctTypeCodeRole |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Pa             | U              | not            |                |
   | rticipantObjec |                | specialized    |                |
   | tDataLifeCycle |                |                |                |
   +----------------+----------------+----------------+----------------+
   | ParticipantOb  | M              | EV (110180,    |                |
   | jectIDTypeCode |                | DCM, "Study    |                |
   |                |                | Instance UID") |                |
   +----------------+----------------+----------------+----------------+
   | ParticipantObj | U              | not            |                |
   | ectSensitivity |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Parti          | M              | The Study      |                |
   | cipantObjectID |                | Instance UID   |                |
   +----------------+----------------+----------------+----------------+
   | Partici        | U              | not            |                |
   | pantObjectName |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Particip       | U              | not            |                |
   | antObjectQuery |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Participa      | U              | Element        |                |
   | ntObjectDetail |                | "Con           |                |
   |                |                | tainsSOPClass" |                |
   |                |                | with one or    |                |
   |                |                | more SOP Class |                |
   |                |                | UID values     |                |
   +----------------+----------------+----------------+----------------+
   | ParticipantObj | U              | not            |                |
   | ectDescription |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | SOPClass       | MC             | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Accession      | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Num            | U              | not            |                |
   | berOfInstances |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Instances      | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Encrypted      | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Anonymized     | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Participating  | Participant    | M              | Shall be: 1 =  |
   | Object:        | ObjectTypeCode |                | person         |
   |                |                |                |                |
   | Patient (1)    |                |                |                |
   +----------------+----------------+----------------+----------------+
   | P              | M              | Shall be: 1 =  |                |
   | articipantObje |                | patient        |                |
   | ctTypeCodeRole |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Pa             | U              | not            |                |
   | rticipantObjec |                | specialized    |                |
   | tDataLifeCycle |                |                |                |
   +----------------+----------------+----------------+----------------+
   | ParticipantOb  | M              | Shall be: EV   |                |
   | jectIDTypeCode |                | (2, RFC-3881,  |                |
   |                |                | "Patient       |                |
   |                |                | Number")       |                |
   +----------------+----------------+----------------+----------------+
   | ParticipantObj | U              | not            |                |
   | ectSensitivity |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Parti          | M              | The patient ID |                |
   | cipantObjectID |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Partici        | U              | The patient    |                |
   | pantObjectName |                | name           |                |
   +----------------+----------------+----------------+----------------+
   | Particip       | U              | not            |                |
   | antObjectQuery |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Participa      | U              | not            |                |
   | ntObjectDetail |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | ParticipantObj | U              | not            |                |
   | ectDescription |                | specialized    |                |
   +----------------+----------------+----------------+----------------+

.. _sect_A.5.3.4:

Data Export
^^^^^^^^^^^

This message describes the event of exporting data from a system,
meaning that the data is leaving control of the system's security
domain. Examples of exporting include printing to paper, recording on
film, conversion to another format for storage in an EHR, writing to
removable media, or sending via e-mail. Multiple patients may be
described in one event message.

.. table:: Audit Message for Data Export

   +----------------+----------------+----------------+----------------+
   | Real World     | Field Name     | Opt.           | Value          |
   | Entities       |                |                | Constraints    |
   +================+================+================+================+
   | Event          | EventID        | M              | EV (110106,    |
   |                |                |                | DCM, "Export") |
   +----------------+----------------+----------------+----------------+
   | E              | M              | Shall be: R =  |                |
   | ventActionCode |                | Read           |                |
   +----------------+----------------+----------------+----------------+
   | EventDateTime  | M              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | EventOu        | M              | not            |                |
   | tcomeIndicator |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | EventTypeCode  | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Active         | UserID         | M              | The identity   |
   | Participant:   |                |                | of the remote  |
   |                |                |                | user or        |
   | Remote Users   |                |                | process        |
   | and Processes  |                |                | receiving the  |
   | (0..n)         |                |                | data           |
   +----------------+----------------+----------------+----------------+
   | Alt            | U              | not            |                |
   | ernativeUserID |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | UserName       | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | U              | M              | See            |                |
   | serIsRequestor |                | `UserIsRe      |                |
   |                |                | questor <#sect |                |
   |                |                | _A.5.3.4.1>`__ |                |
   +----------------+----------------+----------------+----------------+
   | RoleIDCode     | M              | EV (110152,    |                |
   |                |                | DCM,           |                |
   |                |                | "Destination   |                |
   |                |                | Role ID")      |                |
   +----------------+----------------+----------------+----------------+
   | NetworkAcces   | U              | not            |                |
   | sPointTypeCode |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Networ         | U              | not            |                |
   | kAccessPointID |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Active         | UserID         | M              | The identity   |
   | Participant:   |                |                | of the local   |
   |                |                |                | user or        |
   | User or        |                |                | process        |
   | Process        |                |                | exporting the  |
   | Exporting the  |                |                | data. If both  |
   | data(1..2)     |                |                | are known,     |
   |                |                |                | then two       |
   |                |                |                | active         |
   |                |                |                | participants   |
   |                |                |                | shall be       |
   |                |                |                | included (both |
   |                |                |                | the person and |
   |                |                |                | the process).  |
   +----------------+----------------+----------------+----------------+
   | Alt            | U              | not            |                |
   | ernativeUserID |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | UserName       | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | U              | M              | See            |                |
   | serIsRequestor |                | `UserIsRe      |                |
   |                |                | questor <#sect |                |
   |                |                | _A.5.3.4.1>`__ |                |
   +----------------+----------------+----------------+----------------+
   | RoleIDCode     | M              | EV (110153,    |                |
   |                |                | DCM, "Source   |                |
   |                |                | Role ID")      |                |
   +----------------+----------------+----------------+----------------+
   | NetworkAcces   | U              | not            |                |
   | sPointTypeCode |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Networ         | U              | not            |                |
   | kAccessPointID |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Active         | UserID         | M              | See            |
   | Participant:   |                |                | `Username <#se |
   |                |                |                | ct_A.5.2.3>`__ |
   | Media (1)      |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Alt            | U              | See            |                |
   | ernativeUserID |                | `Multi-homed   |                |
   |                |                | Nodes <#se     |                |
   |                |                | ct_A.5.2.4>`__ |                |
   +----------------+----------------+----------------+----------------+
   | UserName       | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | U              | M              | Shall be FALSE |                |
   | serIsRequestor |                |                |                |
   +----------------+----------------+----------------+----------------+
   | RoleIDCode     | M              | EV (110154,    |                |
   |                |                | DCM,           |                |
   |                |                | "Destination   |                |
   |                |                | Media")        |                |
   +----------------+----------------+----------------+----------------+
   | NetworkAcces   | MC             | Required if    |                |
   | sPointTypeCode |                | being exported |                |
   |                |                | to other than  |                |
   |                |                | physical       |                |
   |                |                | media, e.g.,   |                |
   |                |                | to a network   |                |
   |                |                | destination    |                |
   |                |                | rather than to |                |
   |                |                | film, paper or |                |
   |                |                | CD. May be     |                |
   |                |                | present        |                |
   |                |                | otherwise.     |                |
   +----------------+----------------+----------------+----------------+
   | Networ         | MC             | Required if    |                |
   | kAccessPointID |                | Net Access     |                |
   |                |                | Point Type     |                |
   |                |                | Code is        |                |
   |                |                | present. May   |                |
   |                |                | be present     |                |
   |                |                | otherwise.     |                |
   +----------------+----------------+----------------+----------------+
   | M              | MC             | Volume ID,     |                |
   | ediaIdentifier |                | URI, or other  |                |
   |                |                | identifier for |                |
   |                |                | media.         |                |
   |                |                |                |                |
   |                |                | Required if    |                |
   |                |                | digital media. |                |
   |                |                | May be present |                |
   |                |                | otherwise.     |                |
   +----------------+----------------+----------------+----------------+
   | MediaType      | M              | Values         |                |
   |                |                | selected from  |                |
   |                |                | D              |                |
   +----------------+----------------+----------------+----------------+
   | Participating  | Participant    | M              | Shall be: 2 =  |
   | Object:        | ObjectTypeCode |                | system         |
   |                |                |                |                |
   | Studies (0..N) |                |                |                |
   +----------------+----------------+----------------+----------------+
   | P              | M              | Shall be: 3 =  |                |
   | articipantObje |                | report         |                |
   | ctTypeCodeRole |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Pa             | U              | not            |                |
   | rticipantObjec |                | specialized    |                |
   | tDataLifeCycle |                |                |                |
   +----------------+----------------+----------------+----------------+
   | ParticipantOb  | M              | EV (110180,    |                |
   | jectIDTypeCode |                | DCM, "Study    |                |
   |                |                | Instance UID") |                |
   +----------------+----------------+----------------+----------------+
   | ParticipantObj | U              | not            |                |
   | ectSensitivity |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Parti          | M              | The Study      |                |
   | cipantObjectID |                | Instance UID   |                |
   +----------------+----------------+----------------+----------------+
   | Partici        | U              | not            |                |
   | pantObjectName |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Particip       | U              | not            |                |
   | antObjectQuery |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Participa      | U              | not            |                |
   | ntObjectDetail |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | ParticipantObj | U              | not            |                |
   | ectDescription |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | SOPClass       | MC             | See            |                |
   |                |                | `tab           |                |
   |                |                | le_title <#tab |                |
   |                |                | le_A.5.2-1>`__ |                |
   +----------------+----------------+----------------+----------------+
   | Accession      | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Num            | U              | not            |                |
   | berOfInstances |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Instances      | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Encrypted      | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Anonymized     | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Participating  | Participant    | M              | Shall be: 1 =  |
   | Object:        | ObjectTypeCode |                | person         |
   |                |                |                |                |
   | Patients       |                |                |                |
   | (1..N)         |                |                |                |
   +----------------+----------------+----------------+----------------+
   | P              | M              | Shall be: 1 =  |                |
   | articipantObje |                | patient        |                |
   | ctTypeCodeRole |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Pa             | U              | not            |                |
   | rticipantObjec |                | specialized    |                |
   | tDataLifeCycle |                |                |                |
   +----------------+----------------+----------------+----------------+
   | ParticipantOb  | M              | Shall be: EV   |                |
   | jectIDTypeCode |                | (2, RFC-3881,  |                |
   |                |                | "Patient       |                |
   |                |                | Number")       |                |
   +----------------+----------------+----------------+----------------+
   | ParticipantObj | U              | not            |                |
   | ectSensitivity |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Parti          | M              | The patient ID |                |
   | cipantObjectID |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Partici        | U              | The patient    |                |
   | pantObjectName |                | name           |                |
   +----------------+----------------+----------------+----------------+
   | Particip       | U              | not            |                |
   | antObjectQuery |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Particip       | U              | not            |                |
   | antObjectQuery |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Participa      | U              | not            |                |
   | ntObjectDetail |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | ParticipantObj | U              | not            |                |
   | ectDescription |                | specialized    |                |
   +----------------+----------------+----------------+----------------+

.. _sect_A.5.3.4.1:

UserIsRequestor
'''''''''''''''

A single user (either local or remote) shall be identified as the
requestor, i.e., UserIsRequestor with a value of TRUE. This accommodates
both push and pull transfer models for media.

.. _sect_A.5.3.5:

Data Import
^^^^^^^^^^^

This message describes the event of importing data into an organization,
implying that the data now entering the system was not under the control
of the security domain of this organization. Transfer by media within an
organization is often considered a data transfer rather than a data
import event. An example of importing is creating new local instances
from data on removable media. Multiple patients may be described in one
event message.

A single user (either local or remote) shall be identified as the
requestor, i.e., UserIsRequestor with a value of TRUE. This accommodates
both push and pull transfer models for media.

.. table:: Audit Message for Data Import

   +----------------+----------------+----------------+----------------+
   | Real World     | Field Name     | Opt.           | Value          |
   | Entities       |                |                | Constraints    |
   +================+================+================+================+
   | Event          | EventID        | M              | EV (110107,    |
   |                |                |                | DCM, "Import") |
   +----------------+----------------+----------------+----------------+
   | E              | M              | Shall be: C =  |                |
   | ventActionCode |                | Create         |                |
   +----------------+----------------+----------------+----------------+
   | EventDateTime  | M              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | EventOu        | M              | not            |                |
   | tcomeIndicator |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | EventTypeCode  | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Active         | UserID         | M              | The identity   |
   | Participant:   |                |                | of the local   |
   |                |                |                | user or        |
   | User or        |                |                | process        |
   | Process        |                |                | importing the  |
   | Importing the  |                |                | data.          |
   | data (1..n)    |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Alt            | U              | not            |                |
   | ernativeUserID |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | UserName       | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | U              | M              | See `Data      |                |
   | serIsRequestor |                | Import <#se    |                |
   |                |                | ct_A.5.3.5>`__ |                |
   +----------------+----------------+----------------+----------------+
   | RoleIDCode     | M              | EV (110152,    |                |
   |                |                | DCM,           |                |
   |                |                | "Destination   |                |
   |                |                | Role ID")      |                |
   +----------------+----------------+----------------+----------------+
   | NetworkAcces   | U              | not            |                |
   | sPointTypeCode |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Networ         | U              | not            |                |
   | kAccessPointID |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Active         | UserID         | M              | See            |
   | Participant:   |                |                | `Username <#se |
   |                |                |                | ct_A.5.2.3>`__ |
   | Source Media   |                |                |                |
   | (1)            |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Alt            | U              | See            |                |
   | ernativeUserID |                | `Multi-homed   |                |
   |                |                | Nodes <#se     |                |
   |                |                | ct_A.5.2.4>`__ |                |
   +----------------+----------------+----------------+----------------+
   | UserName       | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | U              | M              | Shall be FALSE |                |
   | serIsRequestor |                |                |                |
   +----------------+----------------+----------------+----------------+
   | RoleIDCode     | M              | EV (110155,    |                |
   |                |                | DCM, "Source   |                |
   |                |                | Media")        |                |
   +----------------+----------------+----------------+----------------+
   | NetworkAcces   | U              | not            |                |
   | sPointTypeCode |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Networ         | MC             | Shall be       |                |
   | kAccessPointID |                | present if Net |                |
   |                |                | Access Point   |                |
   |                |                | Type Code is   |                |
   |                |                | present.       |                |
   +----------------+----------------+----------------+----------------+
   | M              | M              | Volume ID,     |                |
   | ediaIdentifier |                | URI, or other  |                |
   |                |                | identifier for |                |
   |                |                | media          |                |
   +----------------+----------------+----------------+----------------+
   | MediaType      | M              | Values         |                |
   |                |                | selected from  |                |
   |                |                | D              |                |
   +----------------+----------------+----------------+----------------+
   | Active         | UserID         | M              | See            |
   | Participant:   |                |                | `Username <#se |
   |                |                |                | ct_A.5.2.3>`__ |
   | Source (0..n)  |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Alt            | U              | See            |                |
   | ernativeUserID |                | `Multi-homed   |                |
   |                |                | Nodes <#se     |                |
   |                |                | ct_A.5.2.4>`__ |                |
   +----------------+----------------+----------------+----------------+
   | UserName       | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | U              | M              | See `Data      |                |
   | serIsRequestor |                | Import <#se    |                |
   |                |                | ct_A.5.3.5>`__ |                |
   +----------------+----------------+----------------+----------------+
   | RoleIDCode     | M              | EV (110153,    |                |
   |                |                | DCM, "Source   |                |
   |                |                | Role ID")      |                |
   +----------------+----------------+----------------+----------------+
   | NetworkAcces   | U              | not            |                |
   | sPointTypeCode |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Networ         | MC             | Shall be       |                |
   | kAccessPointID |                | present if Net |                |
   |                |                | Access Point   |                |
   |                |                | Type Code is   |                |
   |                |                | present.       |                |
   +----------------+----------------+----------------+----------------+
   | Participating  | Participant    | M              | Shall be: 2 =  |
   | Object:        | ObjectTypeCode |                | system         |
   |                |                |                |                |
   | Studies (0..N) |                |                |                |
   +----------------+----------------+----------------+----------------+
   | P              | M              | Shall be: 3 =  |                |
   | articipantObje |                | report         |                |
   | ctTypeCodeRole |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Pa             | U              | not            |                |
   | rticipantObjec |                | specialized    |                |
   | tDataLifeCycle |                |                |                |
   +----------------+----------------+----------------+----------------+
   | ParticipantOb  | M              | EV (110180,    |                |
   | jectIDTypeCode |                | DCM, "Study    |                |
   |                |                | Instance UID") |                |
   +----------------+----------------+----------------+----------------+
   | ParticipantObj | U              | not            |                |
   | ectSensitivity |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Parti          | M              | The Study      |                |
   | cipantObjectID |                | Instance UID   |                |
   +----------------+----------------+----------------+----------------+
   | Partici        | U              | not            |                |
   | pantObjectName |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Particip       | U              | not            |                |
   | antObjectQuery |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Participa      | U              | Not            |                |
   | ntObjectDetail |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | ParticipantObj | U              | not            |                |
   | ectDescription |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | SOPClass       | MC             | See            |                |
   |                |                | `tab           |                |
   |                |                | le_title <#tab |                |
   |                |                | le_A.5.2-1>`__ |                |
   +----------------+----------------+----------------+----------------+
   | Accession      | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Num            | U              | not            |                |
   | berOfInstances |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Instances      | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Encrypted      | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Anonymized     | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Participating  | Participant    | M              | Shall be: 1 =  |
   | Object:        | ObjectTypeCode |                | person         |
   |                |                |                |                |
   | Patients       |                |                |                |
   | (1..N)         |                |                |                |
   +----------------+----------------+----------------+----------------+
   | P              | M              | Shall be: 1 =  |                |
   | articipantObje |                | patient        |                |
   | ctTypeCodeRole |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Pa             | U              | not            |                |
   | rticipantObjec |                | specialized    |                |
   | tDataLifeCycle |                |                |                |
   +----------------+----------------+----------------+----------------+
   | ParticipantOb  | M              | Shall be: EV   |                |
   | jectIDTypeCode |                | (2, RFC-3881,  |                |
   |                |                | "Patient       |                |
   |                |                | Number")       |                |
   +----------------+----------------+----------------+----------------+
   | ParticipantObj | U              | not            |                |
   | ectSensitivity |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Parti          | M              | The patient ID |                |
   | cipantObjectID |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Partici        | U              | The patient    |                |
   | pantObjectName |                | name           |                |
   +----------------+----------------+----------------+----------------+
   | Particip       | U              | not            |                |
   | antObjectQuery |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Participa      | U              | not            |                |
   | ntObjectDetail |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | ParticipantObj | U              | not            |                |
   | ectDescription |                | specialized    |                |
   +----------------+----------------+----------------+----------------+

.. _sect_A.5.3.6:

DICOM Instances Accessed
^^^^^^^^^^^^^^^^^^^^^^^^

This message describes the event of DICOM SOP Instances being viewed,
utilized, updated, or deleted. This message shall only include
information about a single patient and can be used to summarize all
activity for several studies for that patient. This message records the
studies to which the instances belong, not the individual instances.

If all instances within a study are deleted, then the EV(110105, DCM,
"DICOM Study Deleted") event shall be used, see `DICOM Study
Deleted <#sect_A.5.3.8>`__.

.. table:: Audit Message for DICOM Instances Accessed

   +----------------+----------------+----------------+----------------+
   | Real World     | Field Name     | Opt.           | Value          |
   | Entities       |                |                | Constraints    |
   +================+================+================+================+
   | Event          | EventID        | M              | EV (110103,    |
   |                |                |                | DCM, "DICOM    |
   |                |                |                | Instances      |
   |                |                |                | Accessed")     |
   +----------------+----------------+----------------+----------------+
   | E              | M              | Enumerated     |                |
   | ventActionCode |                | value:         |                |
   |                |                |                |                |
   |                |                | C = create     |                |
   |                |                |                |                |
   |                |                | R = read       |                |
   |                |                |                |                |
   |                |                | U = update     |                |
   |                |                |                |                |
   |                |                | D = delete     |                |
   +----------------+----------------+----------------+----------------+
   | EventDateTime  | M              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | EventOu        | M              | not            |                |
   | tcomeIndicator |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | EventTypeCode  | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Active         | UserID         | M              | not            |
   | Participant:   |                |                | specialized    |
   |                |                |                |                |
   | Person and or  |                |                |                |
   | Process        |                |                |                |
   | manipulating   |                |                |                |
   | the data       |                |                |                |
   |                |                |                |                |
   | (1..2)         |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Alt            | U              | not            |                |
   | ernativeUserID |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | UserName       | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | U              | M              | not            |                |
   | serIsRequestor |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | RoleIDCode     | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | NetworkAcces   | U              | not            |                |
   | sPointTypeCode |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Networ         | U              | not            |                |
   | kAccessPointID |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Participating  | Participant    | M              | Shall be: 2 =  |
   | Object:        | ObjectTypeCode |                | system         |
   |                |                |                |                |
   | Studies (1..N) |                |                |                |
   +----------------+----------------+----------------+----------------+
   | P              | M              | Shall be: 3 =  |                |
   | articipantObje |                | report         |                |
   | ctTypeCodeRole |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Pa             | U              | not            |                |
   | rticipantObjec |                | specialized    |                |
   | tDataLifeCycle |                |                |                |
   +----------------+----------------+----------------+----------------+
   | ParticipantOb  | M              | EV (110180,    |                |
   | jectIDTypeCode |                | DCM, "Study    |                |
   |                |                | Instance UID") |                |
   +----------------+----------------+----------------+----------------+
   | ParticipantObj | U              | not            |                |
   | ectSensitivity |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Parti          | M              | The Study      |                |
   | cipantObjectID |                | Instance UID   |                |
   +----------------+----------------+----------------+----------------+
   | Partici        | U              | not            |                |
   | pantObjectName |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Particip       | U              | not            |                |
   | antObjectQuery |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Participa      | U              | Not            |                |
   | ntObjectDetail |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | ParticipantObj | U              | Not            |                |
   | ectDescription |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | SOPClass       | MC             | See            |                |
   |                |                | `tab           |                |
   |                |                | le_title <#tab |                |
   |                |                | le_A.5.2-1>`__ |                |
   +----------------+----------------+----------------+----------------+
   | Accession      | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Num            | U              | not            |                |
   | berOfInstances |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Instances      | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Encrypted      | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Anonymized     | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Participating  | Participant    | M              | Shall be: 1 =  |
   | Object:        | ObjectTypeCode |                | person         |
   |                |                |                |                |
   | Patient (1)    |                |                |                |
   +----------------+----------------+----------------+----------------+
   | P              | M              | Shall be: 1 =  |                |
   | articipantObje |                | patient        |                |
   | ctTypeCodeRole |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Pa             | U              | not            |                |
   | rticipantObjec |                | specialized    |                |
   | tDataLifeCycle |                |                |                |
   +----------------+----------------+----------------+----------------+
   | ParticipantOb  | M              | Shall be: EV   |                |
   | jectIDTypeCode |                | (2, RFC-3881,  |                |
   |                |                | "Patient       |                |
   |                |                | Number")       |                |
   +----------------+----------------+----------------+----------------+
   | ParticipantObj | U              | not            |                |
   | ectSensitivity |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Parti          | M              | The patient ID |                |
   | cipantObjectID |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Partici        | U              | The patient    |                |
   | pantObjectName |                | name           |                |
   +----------------+----------------+----------------+----------------+
   | Particip       | U              | not            |                |
   | antObjectQuery |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Participa      | U              | not            |                |
   | ntObjectDetail |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | ParticipantObj | U              | not            |                |
   | ectDescription |                | specialized    |                |
   +----------------+----------------+----------------+----------------+

.. _sect_A.5.3.7:

DICOM Instances Transferred
^^^^^^^^^^^^^^^^^^^^^^^^^^^

This message describes the event of the completion of transferring DICOM
SOP Instances between two Application Entities. This message may only
include information about a single patient.

.. note::

   This message may have been preceded by a Begin Transferring Instances
   message. The Begin Transferring Instances message conveys the intent
   to store SOP Instances, while the Instances Transferred message
   records the completion of the transfer. Any disagreement between the
   two messages might indicate a potential security breach.

.. table:: Audit Message for DICOM Instances Transferred

   +----------------+----------------+----------------+----------------+
   | Real World     | Field Name     | Opt.           | Value          |
   | Entities       |                |                | Constraints    |
   +================+================+================+================+
   | Event          | EventID        | M              | EV (110104,    |
   |                |                |                | DCM, "DICOM    |
   |                |                |                | Instances      |
   |                |                |                | Transferred")  |
   +----------------+----------------+----------------+----------------+
   | E              | M              | Enumerated     |                |
   | ventActionCode |                | Value:         |                |
   |                |                |                |                |
   |                |                | C = (create)   |                |
   |                |                | if the         |                |
   |                |                | receiver did   |                |
   |                |                | not hold       |                |
   |                |                | copies of the  |                |
   |                |                | instances      |                |
   |                |                | transferred    |                |
   |                |                |                |                |
   |                |                | R = (read) if  |                |
   |                |                | the receiver   |                |
   |                |                | already holds  |                |
   |                |                | copies of the  |                |
   |                |                | SOP Instances  |                |
   |                |                | transferred,   |                |
   |                |                | and has        |                |
   |                |                | determined     |                |
   |                |                | that no        |                |
   |                |                | changes are    |                |
   |                |                | needed to the  |                |
   |                |                | copies held.   |                |
   |                |                |                |                |
   |                |                | U = (update)   |                |
   |                |                | if the         |                |
   |                |                | receiver is    |                |
   |                |                | altering its   |                |
   |                |                | held copies to |                |
   |                |                | reconcile      |                |
   |                |                | differences    |                |
   |                |                | between the    |                |
   |                |                | held copies    |                |
   |                |                | and the        |                |
   |                |                | received       |                |
   |                |                | copies.        |                |
   |                |                |                |                |
   |                |                | If the Audit   |                |
   |                |                | Source is      |                |
   |                |                | either not the |                |
   |                |                | receiver, or   |                |
   |                |                | otherwise does |                |
   |                |                | not know       |                |
   |                |                | whether or not |                |
   |                |                | the instances  |                |
   |                |                | previously     |                |
   |                |                | were held by   |                |
   |                |                | the receiving  |                |
   |                |                | node, then use |                |
   |                |                | "R" = (Read).  |                |
   +----------------+----------------+----------------+----------------+
   | EventDateTime  | M              | Shall be the   |                |
   |                |                | time when the  |                |
   |                |                | transfer has   |                |
   |                |                | completed      |                |
   +----------------+----------------+----------------+----------------+
   | EventOu        | M              | not            |                |
   | tcomeIndicator |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | EventTypeCode  | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Active         | UserID         | M              | not            |
   | Participant:   |                |                | specialized    |
   |                |                |                |                |
   | Process that   |                |                |                |
   | sent the data  |                |                |                |
   | (1)            |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Alt            | U              | not            |                |
   | ernativeUserID |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | UserName       | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | U              | M              | not            |                |
   | serIsRequestor |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | RoleIDCode     | M              | EV (110153,    |                |
   |                |                | DCM, "Source   |                |
   |                |                | Role ID")      |                |
   +----------------+----------------+----------------+----------------+
   | NetworkAcces   | U              | not            |                |
   | sPointTypeCode |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Networ         | U              | not            |                |
   | kAccessPointID |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Active         | UserID         | M              | not            |
   | Participant:   |                |                | specialized    |
   |                |                |                |                |
   | The process    |                |                |                |
   | that received  |                |                |                |
   | the data. (1)  |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Alt            | U              | not            |                |
   | ernativeUserID |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | UserName       | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | U              | M              | not            |                |
   | serIsRequestor |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | RoleIDCode     | M              | EV (110152,    |                |
   |                |                | DCM,           |                |
   |                |                | "Destination   |                |
   |                |                | Role ID")      |                |
   +----------------+----------------+----------------+----------------+
   | NetworkAcces   | U              | not            |                |
   | sPointTypeCode |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Networ         | U              | not            |                |
   | kAccessPointID |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Active         | UserID         | M              | not            |
   | Participant:   |                |                | specialized    |
   |                |                |                |                |
   | Other          |                |                |                |
   | participants   |                |                |                |
   | that are       |                |                |                |
   | known,         |                |                |                |
   | especially     |                |                |                |
   | third parties  |                |                |                |
   | that are the   |                |                |                |
   | requestor      |                |                |                |
   | (0..N)         |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Alt            | U              | not            |                |
   | ernativeUserID |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | UserName       | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | U              | M              | not            |                |
   | serIsRequestor |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | RoleIDCode     | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | NetworkAcces   | U              | not            |                |
   | sPointTypeCode |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Networ         | U              | not            |                |
   | kAccessPointID |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Participating  | Participant    | M              | Shall be: 2 =  |
   | Object:        | ObjectTypeCode |                | system         |
   |                |                |                |                |
   | Studies being  |                |                |                |
   | transferred    |                |                |                |
   | (1..N)         |                |                |                |
   +----------------+----------------+----------------+----------------+
   | P              | M              | Shall be: 3 =  |                |
   | articipantObje |                | report         |                |
   | ctTypeCodeRole |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Pa             | U              | not            |                |
   | rticipantObjec |                | specialized    |                |
   | tDataLifeCycle |                |                |                |
   +----------------+----------------+----------------+----------------+
   | ParticipantOb  | M              | EV (110180,    |                |
   | jectIDTypeCode |                | DCM, "Study    |                |
   |                |                | Instance UID") |                |
   +----------------+----------------+----------------+----------------+
   | ParticipantObj | U              | not            |                |
   | ectSensitivity |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Parti          | M              | The Study      |                |
   | cipantObjectID |                | Instance UID   |                |
   +----------------+----------------+----------------+----------------+
   | Partici        | U              | not            |                |
   | pantObjectName |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Particip       | U              | not            |                |
   | antObjectQuery |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Participa      | U              | Not            |                |
   | ntObjectDetail |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | ParticipantObj | U              | Not            |                |
   | ectDescription |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | SOPClass       | MC             | See            |                |
   |                |                | `tab           |                |
   |                |                | le_title <#tab |                |
   |                |                | le_A.5.2-1>`__ |                |
   +----------------+----------------+----------------+----------------+
   | Accession      | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Num            | U              | not            |                |
   | berOfInstances |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Instances      | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Encrypted      | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Anonymized     | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Participating  | Participant    | M              | Shall be: 1 =  |
   | Object:        | ObjectTypeCode |                | person         |
   |                |                |                |                |
   | Patient (1)    |                |                |                |
   +----------------+----------------+----------------+----------------+
   | P              | M              | Shall be: 1 =  |                |
   | articipantObje |                | patient        |                |
   | ctTypeCodeRole |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Pa             | U              | not            |                |
   | rticipantObjec |                | specialized    |                |
   | tDataLifeCycle |                |                |                |
   +----------------+----------------+----------------+----------------+
   | ParticipantOb  | M              | Shall be: EV   |                |
   | jectIDTypeCode |                | (2, RFC-3881,  |                |
   |                |                | "Patient       |                |
   |                |                | Number")       |                |
   +----------------+----------------+----------------+----------------+
   | ParticipantObj | U              | not            |                |
   | ectSensitivity |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Parti          | M              | The patient ID |                |
   | cipantObjectID |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Partici        | U              | The patient    |                |
   | pantObjectName |                | name           |                |
   +----------------+----------------+----------------+----------------+
   | Particip       | U              | not            |                |
   | antObjectQuery |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Participa      | U              | not            |                |
   | ntObjectDetail |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | ParticipantObj | U              | not            |                |
   | ectDescription |                | specialized    |                |
   +----------------+----------------+----------------+----------------+

.. _sect_A.5.3.8:

DICOM Study Deleted
^^^^^^^^^^^^^^^^^^^

This message describes the event of deletion of one or more studies and
all associated SOP Instances in a single action. This message shall only
include information about a single patient.

.. table:: Audit Message for DICOM Study Deleted

   +----------------+----------------+----------------+----------------+
   | Real World     | Field Name     | Opt.           | Value          |
   | Entities       |                |                | Constraints    |
   +================+================+================+================+
   | Event          | EventID        | M              | EV (110105,    |
   |                |                |                | DCM, "DICOM    |
   |                |                |                | Study          |
   |                |                |                | Deleted")      |
   +----------------+----------------+----------------+----------------+
   | E              | M              | Shall be: D =  |                |
   | ventActionCode |                | delete         |                |
   +----------------+----------------+----------------+----------------+
   | EventDateTime  | M              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | EventOu        | M              | not            |                |
   | tcomeIndicator |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | EventTypeCode  | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Active         | UserID         | M              | not            |
   | Participant:   |                |                | specialized    |
   |                |                |                |                |
   | the person or  |                |                |                |
   | process        |                |                |                |
   | deleting the   |                |                |                |
   | study (1..2)   |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Alt            | U              | not            |                |
   | ernativeUserID |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | UserName       | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | U              | M              | not            |                |
   | serIsRequestor |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | RoleIDCode     | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | NetworkAcces   | U              | not            |                |
   | sPointTypeCode |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Networ         | U              | not            |                |
   | kAccessPointID |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Participating  | Participant    | M              | Shall be: 2 =  |
   | Object:        | ObjectTypeCode |                | system         |
   |                |                |                |                |
   | Studies being  |                |                |                |
   | transferred    |                |                |                |
   | (1..N)         |                |                |                |
   +----------------+----------------+----------------+----------------+
   | P              | M              | Shall be: 3 =  |                |
   | articipantObje |                | report         |                |
   | ctTypeCodeRole |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Pa             | U              | not            |                |
   | rticipantObjec |                | specialized    |                |
   | tDataLifeCycle |                |                |                |
   +----------------+----------------+----------------+----------------+
   | ParticipantOb  | M              | EV (110180,    |                |
   | jectIDTypeCode |                | DCM, "Study    |                |
   |                |                | Instance UID") |                |
   +----------------+----------------+----------------+----------------+
   | ParticipantObj | U              | not            |                |
   | ectSensitivity |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Parti          | M              | The Study      |                |
   | cipantObjectID |                | Instance UID   |                |
   +----------------+----------------+----------------+----------------+
   | Partici        | U              | not            |                |
   | pantObjectName |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Particip       | U              | not            |                |
   | antObjectQuery |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Participa      | U              | Not            |                |
   | ntObjectDetail |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | ParticipantObj | U              | Not            |                |
   | ectDescription |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | SOPClass       | MC             | See            |                |
   |                |                | `tab           |                |
   |                |                | le_title <#tab |                |
   |                |                | le_A.5.2-1>`__ |                |
   +----------------+----------------+----------------+----------------+
   | Accession      | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Num            | U              | not            |                |
   | berOfInstances |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Instances      | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Encrypted      | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Anonymized     | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Participating  | Participant    | M              | Shall be: 1 =  |
   | Object:        | ObjectTypeCode |                | person         |
   |                |                |                |                |
   | Patient (1)    |                |                |                |
   +----------------+----------------+----------------+----------------+
   | P              | M              | Shall be: 1 =  |                |
   | articipantObje |                | patient        |                |
   | ctTypeCodeRole |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Pa             | U              | not            |                |
   | rticipantObjec |                | specialized    |                |
   | tDataLifeCycle |                |                |                |
   +----------------+----------------+----------------+----------------+
   | ParticipantOb  | M              | Shall be: EV   |                |
   | jectIDTypeCode |                | (2, RFC-3881,  |                |
   |                |                | "Patient       |                |
   |                |                | Number")       |                |
   +----------------+----------------+----------------+----------------+
   | ParticipantObj | U              | not            |                |
   | ectSensitivity |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Parti          | M              | The patient ID |                |
   | cipantObjectID |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Partici        | U              | The patient    |                |
   | pantObjectName |                | name           |                |
   +----------------+----------------+----------------+----------------+
   | Particip       | U              | not            |                |
   | antObjectQuery |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Participa      | U              | not            |                |
   | ntObjectDetail |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | ParticipantObj | U              | not            |                |
   | ectDescription |                | specialized    |                |
   +----------------+----------------+----------------+----------------+

.. _sect_A.5.3.9:

Network Entry
^^^^^^^^^^^^^

This message describes the event of a system, such as a mobile device,
intentionally entering or leaving the network.

.. note::

   The machine should attempt to send this message prior to detaching.
   If this is not possible, it should retain the message in a local
   buffer so that it can be sent later. The mobile machine can then
   capture audit messages in a local buffer while it is outside the
   secure domain. When it is reconnected to the secure domain, it can
   send the detach message (if buffered), followed by the buffered
   messages, followed by a mobile machine message for rejoining the
   secure domain. The timestamps on these messages is the time that the
   event was noticed to have occurred, not the time that the message is
   sent.

.. table:: Audit Message for Network Entry

   +-----------------+------------+-----------------+-----------------+
   | Real World      | Field Name | Opt.            | Value           |
   | Entities        |            |                 |                 |
   +=================+============+=================+=================+
   | Event           | EventID    | M               | EV (110108,     |
   |                 |            |                 | DCM, "Network   |
   |                 |            |                 | Entry")         |
   +-----------------+------------+-----------------+-----------------+
   | EventActionCode | M          | Shall be: E =   |                 |
   |                 |            | Execute         |                 |
   +-----------------+------------+-----------------+-----------------+
   | EventDateTime   | M          | not specialized |                 |
   +-----------------+------------+-----------------+-----------------+
   | EventO          | M          | not specialized |                 |
   | utcomeIndicator |            |                 |                 |
   +-----------------+------------+-----------------+-----------------+
   | EventTypeCode   | M          | EV (110124,     |                 |
   |                 |            | DCM,            |                 |
   |                 |            | "Attach")EV     |                 |
   |                 |            | (110125, DCM,   |                 |
   |                 |            | "Detach")       |                 |
   +-----------------+------------+-----------------+-----------------+
   | Active          | UserID     | M               | not specialized |
   | Participant:    |            |                 |                 |
   |                 |            |                 |                 |
   | Node or System  |            |                 |                 |
   | entering or     |            |                 |                 |
   | leaving the     |            |                 |                 |
   | network (1)     |            |                 |                 |
   +-----------------+------------+-----------------+-----------------+
   | Al              | U          | not specialized |                 |
   | ternativeUserID |            |                 |                 |
   +-----------------+------------+-----------------+-----------------+
   | UserName        | U          | not specialized |                 |
   +-----------------+------------+-----------------+-----------------+
   | UserIsRequestor | M          | Shall be FALSE  |                 |
   +-----------------+------------+-----------------+-----------------+
   | RoleIDCode      | U          | not specialized |                 |
   +-----------------+------------+-----------------+-----------------+
   | NetworkAcce     | U          | not specialized |                 |
   | ssPointTypeCode |            |                 |                 |
   +-----------------+------------+-----------------+-----------------+
   | Netwo           | U          | not specialized |                 |
   | rkAccessPointID |            |                 |                 |
   +-----------------+------------+-----------------+-----------------+

No Participant Objects are needed for this message.

.. _sect_A.5.3.10:

Query
^^^^^

This message describes the event of a Query being issued or received.
The message does not record the response to the query, but merely
records the fact that a query was issued. For example, this would report
queries using the DICOM SOP Classes:

a. Modality Worklist

b. UPS Pull

c. UPS Watch

d. Composite Instance Query

.. note::

   1. The response to a query may result in one or more Instances
      Transferred or Instances Accessed messages, depending on what
      events transpire after the query. If there were security-related
      failures, such as access violations, when processing a query,
      those failures should show up in other audit messages, such as a
      Security Alert message.

   2. Non-DICOM queries may also be captured by this message. The
      Participant Object ID Type Code, the Participant Object ID, and
      the Query fields may have values related to such non-DICOM
      queries.

.. table:: Audit Message for Query

   +----------------+----------------+----------------+----------------+
   | Real World     | Field Name     | Opt.           | Value          |
   | Entities       |                |                | Constraints    |
   +================+================+================+================+
   | Event          | EventID        | M              | EV (110112,    |
   |                |                |                | DCM, "Query")  |
   +----------------+----------------+----------------+----------------+
   | E              | M              | Shall be: E =  |                |
   | ventActionCode |                | Execute        |                |
   +----------------+----------------+----------------+----------------+
   | EventDateTime  | M              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | EventOu        | M              | not            |                |
   | tcomeIndicator |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | EventTypeCode  | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Active         | UserID         | M              | not            |
   | Participant:   |                |                | specialized    |
   |                |                |                |                |
   | Process        |                |                |                |
   | Issuing the    |                |                |                |
   | Query (1)      |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Alt            | U              | not            |                |
   | ernativeUserID |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | UserName       | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | U              | M              | not            |                |
   | serIsRequestor |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | RoleIDCode     | M              | EV (110153,    |                |
   |                |                | DCM, "Source   |                |
   |                |                | Role ID")      |                |
   +----------------+----------------+----------------+----------------+
   | NetworkAcces   | U              | not            |                |
   | sPointTypeCode |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Networ         | U              | not            |                |
   | kAccessPointID |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Active         | UserID         | M              | not            |
   | Participant:   |                |                | specialized    |
   |                |                |                |                |
   | The process    |                |                |                |
   | that will      |                |                |                |
   | respond to the |                |                |                |
   | query (1)      |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Alt            | U              | not            |                |
   | ernativeUserID |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | UserName       | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | U              | M              | not            |                |
   | serIsRequestor |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | RoleIDCode     | M              | EV (110152,    |                |
   |                |                | DCM,           |                |
   |                |                | "Destination   |                |
   |                |                | Role ID")      |                |
   +----------------+----------------+----------------+----------------+
   | NetworkAcces   | U              | not            |                |
   | sPointTypeCode |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Networ         | U              | not            |                |
   | kAccessPointID |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Active         | UserID         | M              | not            |
   | Participant:   |                |                | specialized    |
   |                |                |                |                |
   | Other          |                |                |                |
   | Participants   |                |                |                |
   | that are       |                |                |                |
   | known,         |                |                |                |
   | especially     |                |                |                |
   | third parties  |                |                |                |
   | that requested |                |                |                |
   | the query      |                |                |                |
   | (0..N)         |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Alt            | U              | not            |                |
   | ernativeUserID |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | UserName       | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | U              | M              | not            |                |
   | serIsRequestor |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | RoleIDCode     | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | NetworkAcces   | U              | not            |                |
   | sPointTypeCode |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Networ         | U              | not            |                |
   | kAccessPointID |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Participating  | Participant    | M              | Shall be: 2 =  |
   | Object:        | ObjectTypeCode |                | system         |
   |                |                |                |                |
   | SOP Queried    |                |                |                |
   | and the Query  |                |                |                |
   | (1)            |                |                |                |
   +----------------+----------------+----------------+----------------+
   | P              | M              | Shall be: 3 =  |                |
   | articipantObje |                | report         |                |
   | ctTypeCodeRole |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Pa             | U              | not            |                |
   | rticipantObjec |                | specialized    |                |
   | tDataLifeCycle |                |                |                |
   +----------------+----------------+----------------+----------------+
   | ParticipantOb  | M              | DT (110181,    |                |
   | jectIDTypeCode |                | DCM, "SOP      |                |
   |                |                | Class UID")    |                |
   +----------------+----------------+----------------+----------------+
   | ParticipantObj | U              | not            |                |
   | ectSensitivity |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Parti          | M              | If the         |                |
   | cipantObjectID |                | ParticipantOb  |                |
   |                |                | jectIDTypeCode |                |
   |                |                | is (110181,    |                |
   |                |                | DCM, "SOP      |                |
   |                |                | Class UID"),   |                |
   |                |                | then this      |                |
   |                |                | field shall    |                |
   |                |                | hold the UID   |                |
   |                |                | of the SOP     |                |
   |                |                | Class being    |                |
   |                |                | queried        |                |
   +----------------+----------------+----------------+----------------+
   | Partici        | U              | not            |                |
   | pantObjectName |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Particip       | M              | If the         |                |
   | antObjectQuery |                | ParticipantOb  |                |
   |                |                | jectIDTypeCode |                |
   |                |                | is (110181,    |                |
   |                |                | DCM, "SOP      |                |
   |                |                | Class UID"),   |                |
   |                |                | then this      |                |
   |                |                | field shall    |                |
   |                |                | hold the       |                |
   |                |                | Dataset of the |                |
   |                |                | DICOM query,   |                |
   |                |                | x              |                |
   |                |                | s:base64Binary |                |
   |                |                | encoded.       |                |
   |                |                | Otherwise, it  |                |
   |                |                | shall be the   |                |
   |                |                | query in the   |                |
   |                |                | format of the  |                |
   |                |                | protocol used. |                |
   +----------------+----------------+----------------+----------------+
   | Participa      | MC             | Required if    |                |
   | ntObjectDetail |                | the            |                |
   |                |                | ParticipantOb  |                |
   |                |                | jectIDTypeCode |                |
   |                |                | is (110181,    |                |
   |                |                | DCM, "SOP      |                |
   |                |                | Class UID")    |                |
   |                |                |                |                |
   |                |                | A              |                |
   |                |                | Participa      |                |
   |                |                | ntObjectDetail |                |
   |                |                | element with   |                |
   |                |                | the XML        |                |
   |                |                | attribute      |                |
   |                |                | "T             |                |
   |                |                | ransferSyntax" |                |
   |                |                | shall be       |                |
   |                |                | present. The   |                |
   |                |                | value of the   |                |
   |                |                | Transfer       |                |
   |                |                | Syntax         |                |
   |                |                | attribute      |                |
   |                |                | shall be the   |                |
   |                |                | UID of the     |                |
   |                |                | transfer       |                |
   |                |                | syntax of the  |                |
   |                |                | query. The     |                |
   |                |                | element        |                |
   |                |                | contents shall |                |
   |                |                | be             |                |
   |                |                | x              |                |
   |                |                | s:base64Binary |                |
   |                |                | encoding. The  |                |
   |                |                | Transfer       |                |
   |                |                | Syntax shall   |                |
   |                |                | be a DICOM     |                |
   |                |                | Transfer       |                |
   |                |                | Syntax.        |                |
   +----------------+----------------+----------------+----------------+
   | ParticipantObj | U              | not            |                |
   | ectDescription |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | SOPClass       | U              | See            |                |
   |                |                | `tab           |                |
   |                |                | le_title <#tab |                |
   |                |                | le_A.5.2-1>`__ |                |
   +----------------+----------------+----------------+----------------+
   | Accession      | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Num            | U              | not            |                |
   | berOfInstances |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Instances      | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Encrypted      | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Anonymized     | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+

.. _sect_A.5.3.11:

Security Alert
^^^^^^^^^^^^^^

This message describes any event for which a node needs to report a
security alert, e.g., a node authentication failure when establishing a
secure communications channel.

.. note::

   The Node Authentication event can be used to report both successes
   and failures. If reporting of success is done, this could generate a
   very large number of audit messages, since every authenticated DICOM
   association, HL7 transaction, and HTML connection should result in a
   successful node authentication. It is expected that in most
   situations only the failures will be reported.

.. table:: Audit Message for Security Alert

   +----------------+----------------+----------------+----------------+
   | Real World     | Field Name     | Opt.           | Value          |
   | Entities       |                |                | Constraints    |
   +================+================+================+================+
   | Event          | EventID        | M              | EV (110113,    |
   |                |                |                | DCM, "Security |
   |                |                |                | Alert")        |
   +----------------+----------------+----------------+----------------+
   | E              | M              | Shall be: E =  |                |
   | ventActionCode |                | Execute        |                |
   +----------------+----------------+----------------+----------------+
   | EventDateTime  | M              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | EventOu        | M              | Success        |                |
   | tcomeIndicator |                | implies an     |                |
   |                |                | informative    |                |
   |                |                | alert. The     |                |
   |                |                | other failure  |                |
   |                |                | values imply   |                |
   |                |                | warning codes  |                |
   |                |                | that indicate  |                |
   |                |                | the severity   |                |
   |                |                | of the alert.  |                |
   |                |                | A Minor or     |                |
   |                |                | Serious        |                |
   |                |                | failure        |                |
   |                |                | indicates that |                |
   |                |                | mitigation     |                |
   |                |                | efforts were   |                |
   |                |                | effective in   |                |
   |                |                | maintaining    |                |
   |                |                | system         |                |
   |                |                | security. A    |                |
   |                |                | Major failure  |                |
   |                |                | indicates that |                |
   |                |                | mitigation     |                |
   |                |                | efforts may    |                |
   |                |                | not have been  |                |
   |                |                | effective, and |                |
   |                |                | that the       |                |
   |                |                | security       |                |
   |                |                | system may     |                |
   |                |                | have been      |                |
   |                |                | compromised.   |                |
   +----------------+----------------+----------------+----------------+
   | EventTypeCode  | M              | Values         |                |
   |                |                | selected from  |                |
   |                |                | D.             |                |
   +----------------+----------------+----------------+----------------+
   | Active         | UserID         | M              | not            |
   | Participant:   |                |                | specialized    |
   |                |                |                |                |
   | Reporting      |                |                |                |
   | Person and/or  |                |                |                |
   | Process (1..2) |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Alt            | U              | not            |                |
   | ernativeUserID |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | UserName       | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | U              | M              | not            |                |
   | serIsRequestor |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | RoleIDCode     | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | NetworkAcces   | U              | not            |                |
   | sPointTypeCode |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Networ         | U              | not            |                |
   | kAccessPointID |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Active         | UserID         | M              | not            |
   | Participant:   |                |                | specialized    |
   |                |                |                |                |
   | Performing     |                |                |                |
   | Persons or     |                |                |                |
   | Processes      |                |                |                |
   | (0..N)         |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Alt            | U              | not            |                |
   | ernativeUserID |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | UserName       | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | U              | M              | Shall be FALSE |                |
   | serIsRequestor |                |                |                |
   +----------------+----------------+----------------+----------------+
   | RoleIDCode     | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | NetworkAcces   | U              | not            |                |
   | sPointTypeCode |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Networ         | U              | not            |                |
   | kAccessPointID |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Participating  | Participant    | M              | Shall be: 2 =  |
   | Object:        | ObjectTypeCode |                | system         |
   |                |                |                |                |
   | Alert Subject  |                |                |                |
   | (0..N)         |                |                |                |
   +----------------+----------------+----------------+----------------+
   | P              | U              | Defined Terms: |                |
   | articipantObje |                |                |                |
   | ctTypeCodeRole |                | 5 = master     |                |
   |                |                | file           |                |
   |                |                |                |                |
   |                |                | 13 = security  |                |
   |                |                | resource       |                |
   +----------------+----------------+----------------+----------------+
   | Pa             | U              | not            |                |
   | rticipantObjec |                | specialized    |                |
   | tDataLifeCycle |                |                |                |
   +----------------+----------------+----------------+----------------+
   | ParticipantOb  | M              | Defined Terms: |                |
   | jectIDTypeCode |                |                |                |
   |                |                | DT (12,        |                |
   |                |                | RFC-3881,      |                |
   |                |                | "URI")         |                |
   |                |                |                |                |
   |                |                | DT (110182,    |                |
   |                |                | DCM, "Node     |                |
   |                |                | ID")           |                |
   +----------------+----------------+----------------+----------------+
   | ParticipantObj | U              | not            |                |
   | ectSensitivity |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Parti          | M              | For a          |                |
   | cipantObjectID |                | ParticipantOb  |                |
   |                |                | jectIDTypeCode |                |
   |                |                | of (12,        |                |
   |                |                | RFC-3881,      |                |
   |                |                | "URI"), then   |                |
   |                |                | this value     |                |
   |                |                | shall be the   |                |
   |                |                | URI of the     |                |
   |                |                | file or other  |                |
   |                |                | resource that  |                |
   |                |                | is the subject |                |
   |                |                | of the alert.  |                |
   |                |                |                |                |
   |                |                | For a          |                |
   |                |                | ParticipantOb  |                |
   |                |                | jectIDTypeCode |                |
   |                |                | of (110182,    |                |
   |                |                | DCM, "Node     |                |
   |                |                | ID") then the  |                |
   |                |                | value shall    |                |
   |                |                | include the    |                |
   |                |                | identity of    |                |
   |                |                | the node that  |                |
   |                |                | is the subject |                |
   |                |                | of the alert   |                |
   |                |                | either in the  |                |
   |                |                | form of        |                |
   |                |                | node_na        |                |
   |                |                | me@domain_name |                |
   |                |                | or as an IP    |                |
   |                |                | address.       |                |
   |                |                |                |                |
   |                |                | Otherwise, the |                |
   |                |                | value shall be |                |
   |                |                | an identifier  |                |
   |                |                | of the type    |                |
   |                |                | specified by   |                |
   |                |                | ParticipantOb  |                |
   |                |                | jectIDTypeCode |                |
   |                |                | of the subject |                |
   |                |                | of the alert.  |                |
   +----------------+----------------+----------------+----------------+
   | Partici        | U              | not            |                |
   | pantObjectName |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Particip       | U              | not            |                |
   | antObjectQuery |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Participa      | M              | An element     |                |
   | ntObjectDetail |                | with the       |                |
   |                |                | Attribute      |                |
   |                |                | "type" equal   |                |
   |                |                | to "Alert      |                |
   |                |                | Description"   |                |
   |                |                | shall be       |                |
   |                |                | present with a |                |
   |                |                | free text      |                |
   |                |                | description of |                |
   |                |                | the nature of  |                |
   |                |                | the alert as   |                |
   |                |                | the value      |                |
   +----------------+----------------+----------------+----------------+
   | ParticipantObj | U              | not            |                |
   | ectDescription |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | SOPClass       | U              | See            |                |
   |                |                | `tab           |                |
   |                |                | le_title <#tab |                |
   |                |                | le_A.5.2-1>`__ |                |
   +----------------+----------------+----------------+----------------+
   | Accession      | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Num            | U              | not            |                |
   | berOfInstances |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Instances      | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Encrypted      | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Anonymized     | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+

.. _sect_A.5.3.12:

User Authentication
^^^^^^^^^^^^^^^^^^^

This message describes the event that a user has attempted to log on or
log off. This report can be made regardless of whether the attempt was
successful or not. No Participant Objects are needed for this message.

.. note::

   The user usually has UserIsRequestor TRUE, but in the case of a
   logout timer, the Node might be the UserIsRequestor.

.. table:: Audit Message for User Authentication

   +-----------------+------------+-----------------+-----------------+
   | Real World      | Field Name | Opt.            | Value           |
   | Entities        |            |                 | Constraints     |
   +=================+============+=================+=================+
   | Event           | EventID    | M               | EV (110114,     |
   |                 |            |                 | DCM, "User      |
   |                 |            |                 | A               |
   |                 |            |                 | uthentication") |
   +-----------------+------------+-----------------+-----------------+
   | EventActionCode | M          | Shall be: E =   |                 |
   |                 |            | Execute         |                 |
   +-----------------+------------+-----------------+-----------------+
   | EventDateTime   | M          | not specialized |                 |
   +-----------------+------------+-----------------+-----------------+
   | EventO          | M          | not specialized |                 |
   | utcomeIndicator |            |                 |                 |
   +-----------------+------------+-----------------+-----------------+
   | EventTypeCode   | M          | Defined Terms:  |                 |
   |                 |            |                 |                 |
   |                 |            | EV (110122,     |                 |
   |                 |            | DCM, "Login")   |                 |
   |                 |            |                 |                 |
   |                 |            | EV (110123,     |                 |
   |                 |            | DCM, "Logout")  |                 |
   +-----------------+------------+-----------------+-----------------+
   | Active          | UserID     | M               | not specialized |
   | Participant:    |            |                 |                 |
   |                 |            |                 |                 |
   | Person          |            |                 |                 |
   | Authenticated   |            |                 |                 |
   | or claimed      |            |                 |                 |
   |                 |            |                 |                 |
   | (1)             |            |                 |                 |
   +-----------------+------------+-----------------+-----------------+
   | Al              | U          | not specialized |                 |
   | ternativeUserID |            |                 |                 |
   +-----------------+------------+-----------------+-----------------+
   | UserName        | U          | not specialized |                 |
   +-----------------+------------+-----------------+-----------------+
   | UserIsRequestor | M          | not specialized |                 |
   +-----------------+------------+-----------------+-----------------+
   | RoleIDCode      | U          | not specialized |                 |
   +-----------------+------------+-----------------+-----------------+
   | NetworkAcce     | M          | not specialized |                 |
   | ssPointTypeCode |            |                 |                 |
   +-----------------+------------+-----------------+-----------------+
   | Netwo           | M          | not specialized |                 |
   | rkAccessPointID |            |                 |                 |
   +-----------------+------------+-----------------+-----------------+
   | Active          | UserID     | M               | not specialized |
   | Participant:    |            |                 |                 |
   |                 |            |                 |                 |
   | Node or System  |            |                 |                 |
   | performing      |            |                 |                 |
   | authentication  |            |                 |                 |
   | (0..1)          |            |                 |                 |
   +-----------------+------------+-----------------+-----------------+
   | Al              | U          | not specialized |                 |
   | ternativeUserID |            |                 |                 |
   +-----------------+------------+-----------------+-----------------+
   | UserName        | U          | not specialized |                 |
   +-----------------+------------+-----------------+-----------------+
   | UserIsRequestor | M          | not specialized |                 |
   +-----------------+------------+-----------------+-----------------+
   | RoleIDCode      | U          | not specialized |                 |
   +-----------------+------------+-----------------+-----------------+
   | NetworkAcce     | U          | not specialized |                 |
   | ssPointTypeCode |            |                 |                 |
   +-----------------+------------+-----------------+-----------------+
   | Netwo           | U          | not specialized |                 |
   | rkAccessPointID |            |                 |                 |
   +-----------------+------------+-----------------+-----------------+

.. _sect_A.5.3.13:

Order Record
^^^^^^^^^^^^

This message describes the event of an order being created, modified,
accessed, or deleted. This message may only include information about a
single patient.

.. note::

   An order record typically is managed by a non-DICOM system. However,
   DICOM applications often manipulate order records, and thus may be
   obligated by site security policies to record such events in the
   audit logs.

.. table:: Audit Message for Order Record

   +----------------+----------------+----------------+----------------+
   | Real World     | Field Name     | Opt.           | Value          |
   | Entities       |                |                | Constraints    |
   +================+================+================+================+
   | Event          | EventID        | M              | EV (110109,    |
   |                |                |                | DCM, "Order    |
   |                |                |                | Record")       |
   +----------------+----------------+----------------+----------------+
   | E              | M              | Enumerated     |                |
   | ventActionCode |                | value:         |                |
   |                |                |                |                |
   |                |                | C = create     |                |
   |                |                |                |                |
   |                |                | R = read       |                |
   |                |                |                |                |
   |                |                | U = update     |                |
   |                |                |                |                |
   |                |                | D = delete     |                |
   +----------------+----------------+----------------+----------------+
   | EventDateTime  | M              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | EventOu        | M              | not            |                |
   | tcomeIndicator |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | EventTypeCode  | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | User (1..2)    | UserID         | M              | The identity   |
   |                |                |                | of the person  |
   |                |                |                | or process     |
   |                |                |                | manipulating   |
   |                |                |                | the data. If   |
   |                |                |                | both the       |
   |                |                |                | person and the |
   |                |                |                | process are    |
   |                |                |                | known, both    |
   |                |                |                | shall be       |
   |                |                |                | included.      |
   +----------------+----------------+----------------+----------------+
   | A              | U              | not            |                |
   | lternateUserID |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | UserName       | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | U              | U              | not            |                |
   | serIsRequestor |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | RoleIDCode     | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | NetworkAcces   | U              | not            |                |
   | sPointTypeCode |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Networ         | U              | not            |                |
   | kAccessPointID |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Patient (1)    | Participant    | M              | EV 1 (person)  |
   |                | ObjectTypeCode |                |                |
   +----------------+----------------+----------------+----------------+
   | P              | M              | EV 1 (patient) |                |
   | articipantObje |                |                |                |
   | ctTypeCodeRole |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Pa             | U              | not            |                |
   | rticipantObjec |                | specialized    |                |
   | tDataLifeCycle |                |                |                |
   +----------------+----------------+----------------+----------------+
   | ParticipantOb  | M              | EV 2 (patient  |                |
   | jectIDTypeCode |                | ID)            |                |
   +----------------+----------------+----------------+----------------+
   | ParticipantObj | U              | not            |                |
   | ectSensitivity |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Parti          | M              | The patient ID |                |
   | cipantObjectID |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Partici        | U              | The patient    |                |
   | pantObjectName |                | name           |                |
   +----------------+----------------+----------------+----------------+
   | Particip       | U              | not            |                |
   | antObjectQuery |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Participa      | U              | not            |                |
   | ntObjectDetail |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | ParticipantObj | U              | not further    |                |
   | ectDescription |                | specialized    |                |
   +----------------+----------------+----------------+----------------+

.. _sect_A.5.3.14:

Patient Record
^^^^^^^^^^^^^^

This message describes the event of a patient record being created,
modified, accessed, or deleted.

.. note::

   There are several types of patient records managed by both DICOM and
   non-DICOM system. DICOM applications often manipulate patient records
   managed by a variety of systems, and thus may be obligated by site
   security policies to record such events in the audit logs. This audit
   event can be used to record the access or manipulation of patient
   records where specific DICOM SOP Instances are not involved.

.. table:: Audit Message for Patient Record

   +----------------+----------------+----------------+----------------+
   | Real World     | Field Name     | Opt.           | Value          |
   | Entities       |                |                | Constraints    |
   +================+================+================+================+
   | Event          | EventID        | M              | EV (110110,    |
   |                |                |                | DCM, "Patient  |
   |                |                |                | Record")       |
   +----------------+----------------+----------------+----------------+
   | E              | M              | Enumerated     |                |
   | ventActionCode |                | value:         |                |
   |                |                |                |                |
   |                |                | C = create     |                |
   |                |                |                |                |
   |                |                | R = read       |                |
   |                |                |                |                |
   |                |                | U = update     |                |
   |                |                |                |                |
   |                |                | D = delete     |                |
   +----------------+----------------+----------------+----------------+
   | EventDateTime  | M              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | EventOu        | M              | not            |                |
   | tcomeIndicator |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | EventTypeCode  | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | User (1..2)    | UserID         | M              | The identity   |
   |                |                |                | of the person  |
   |                |                |                | or process     |
   |                |                |                | manipulating   |
   |                |                |                | the data. If   |
   |                |                |                | both are       |
   |                |                |                | known, then    |
   |                |                |                | two active     |
   |                |                |                | participants   |
   |                |                |                | shall be       |
   |                |                |                | included (both |
   |                |                |                | the person and |
   |                |                |                | the process).  |
   +----------------+----------------+----------------+----------------+
   | A              | U              | not            |                |
   | lternateUserID |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | UserName       | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | U              | U              | not            |                |
   | serIsRequestor |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | RoleIDCode     | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | NetworkAcces   | U              | not            |                |
   | sPointTypeCode |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Networ         | U              | not            |                |
   | kAccessPointID |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Patient (1)    | Participant    | M              | EV 1 (person)  |
   |                | ObjectTypeCode |                |                |
   +----------------+----------------+----------------+----------------+
   | P              | M              | EV 1 (patient) |                |
   | articipantObje |                |                |                |
   | ctTypeCodeRole |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Pa             | U              | not            |                |
   | rticipantObjec |                | specialized    |                |
   | tDataLifeCycle |                |                |                |
   +----------------+----------------+----------------+----------------+
   | ParticipantOb  | M              | EV 2 (patient  |                |
   | jectIDTypeCode |                | ID)            |                |
   +----------------+----------------+----------------+----------------+
   | ParticipantObj | U              | not            |                |
   | ectSensitivity |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Parti          | M              | The patient ID |                |
   | cipantObjectID |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Partici        | U              | The patient    |                |
   | pantObjectName |                | name           |                |
   +----------------+----------------+----------------+----------------+
   | Particip       | U              | not            |                |
   | antObjectQuery |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Participa      | U              | not            |                |
   | ntObjectDetail |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | ParticipantObj | U              | not further    |                |
   | ectDescription |                | specialized    |                |
   +----------------+----------------+----------------+----------------+

.. _sect_A.5.3.15:

Procedure Record
^^^^^^^^^^^^^^^^

This message describes the event of a procedure record being created,
accessed, modified, accessed, or deleted. This message may only include
information about a single patient.

.. note::

   1. DICOM applications often manipulate procedure records, e.g. with
      MPPS update. Modality Worklist query events are described by the
      Query event message.

   2. The same accession number may appear with several order numbers.
      The Study participant fields or the entire message may be repeated
      to capture such many to many relationships.

.. table:: Audit Message for Procedure Record

   +----------------+----------------+----------------+----------------+
   | Real World     | Field Name     | Opt.           | Value          |
   | Entities       |                |                | Constraints    |
   +================+================+================+================+
   | Event          | EventID        | M              | EV (110111,    |
   |                |                |                | DCM,           |
   |                |                |                | "Procedure     |
   |                |                |                | Record")       |
   +----------------+----------------+----------------+----------------+
   | E              | C              | Enumerated     |                |
   | ventActionCode |                | value:         |                |
   |                |                |                |                |
   |                |                | C = create     |                |
   |                |                |                |                |
   |                |                | R = read       |                |
   |                |                |                |                |
   |                |                | U = update     |                |
   |                |                |                |                |
   |                |                | D = delete     |                |
   +----------------+----------------+----------------+----------------+
   | EventDateTime  | M              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | EventOu        | M              | not            |                |
   | tcomeIndicator |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | EventTypeCode  | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | User (1..2)    | UserID         | M              | The identity   |
   |                |                |                | of the person  |
   |                |                |                | or process     |
   |                |                |                | manipulating   |
   |                |                |                | the data. If   |
   |                |                |                | both are       |
   |                |                |                | known, then    |
   |                |                |                | two active     |
   |                |                |                | participants   |
   |                |                |                | shall be       |
   |                |                |                | included (both |
   |                |                |                | the person and |
   |                |                |                | the process).  |
   +----------------+----------------+----------------+----------------+
   | A              | U              | not            |                |
   | lternateUserID |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | UserName       | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | U              | U              | not            |                |
   | serIsRequestor |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | RoleIDCode     | U              | not            |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | NetworkAcces   | U              | not            |                |
   | sPointTypeCode |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Networ         | U              | not            |                |
   | kAccessPointID |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Study (0..N)   | Participant    | M              | EV 2 (system)  |
   |                | ObjectTypeCode |                |                |
   +----------------+----------------+----------------+----------------+
   | P              | M              | EV 3 (report)  |                |
   | articipantObje |                |                |                |
   | ctTypeCodeRole |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Pa             | U              | not            |                |
   | rticipantObjec |                | specialized    |                |
   | tDataLifeCycle |                |                |                |
   +----------------+----------------+----------------+----------------+
   | ParticipantOb  | M              | EV (110180,    |                |
   | jectIDTypeCode |                | DCM, "Study    |                |
   |                |                | Instance UID") |                |
   +----------------+----------------+----------------+----------------+
   | ParticipantObj | U              | not            |                |
   | ectSensitivity |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Parti          | M              | The Study      |                |
   | cipantObjectID |                | Instance UID   |                |
   +----------------+----------------+----------------+----------------+
   | Partici        | U              | not            |                |
   | pantObjectName |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Particip       | U              | not            |                |
   | antObjectQuery |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Participa      | U              | Not further    |                |
   | ntObjectDetail |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | ParticipantObj | U              | Not further    |                |
   | ectDescription |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | SOPClass       | MC             | not further    |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Accession      | U              | not further    |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Num            | U              | not further    |                |
   | berOfInstances |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Instances      | U              | not further    |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Encrypted      | U              | not further    |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Anonymized     | U              | not further    |                |
   |                |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Patient (1)    | Participant    | M              | EV 1 (person)  |
   |                | ObjectTypeCode |                |                |
   +----------------+----------------+----------------+----------------+
   | P              | M              | EV 1 (patient) |                |
   | articipantObje |                |                |                |
   | ctTypeCodeRole |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Pa             | U              | not            |                |
   | rticipantObjec |                | specialized    |                |
   | tDataLifeCycle |                |                |                |
   +----------------+----------------+----------------+----------------+
   | ParticipantOb  | M              | EV 2 (patient  |                |
   | jectIDTypeCode |                | ID)            |                |
   +----------------+----------------+----------------+----------------+
   | ParticipantObj | U              | not            |                |
   | ectSensitivity |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Parti          | M              | The patient ID |                |
   | cipantObjectID |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Partici        | U              | The patient    |                |
   | pantObjectName |                | name           |                |
   +----------------+----------------+----------------+----------------+
   | Particip       | U              | not            |                |
   | antObjectQuery |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | Participa      | U              | not            |                |
   | ntObjectDetail |                | specialized    |                |
   +----------------+----------------+----------------+----------------+
   | ParticipantObj | U              | not further    |                |
   | ectDescription |                | specialized    |                |
   +----------------+----------------+----------------+----------------+

.. _sect_A.6:

Audit Trail Message Transmission Profile - SYSLOG-TLS
-----------------------------------------------------

This profile defines the transmission of audit trail messages.
`biblioentry_title <#biblio_RFC_5425>`__ provides the mechanisms for
reliable transport, buffering, acknowledgement, authentication,
identification, and encryption. `biblioentry_title <#biblio_RFC_5424>`__
states that the TLS used MUST be TLS version 1.2. For this DICOM profile
TLS MUST be used, and version 1.2 or later is RECOMMENDED.

.. note::

   The words MUST and RECOMMENDED are used in accordance with the IETF
   specification for normative requirements.

Any implementation that claims conformance to this profile shall also
conform to the Audit Trail Message Format Profile. XML audit trail
messages created using the format defined in Audit Trail Message Format
Profile shall be transmitted to a collection point using the syslog over
TLS mechanism, defined in `biblioentry_title <#biblio_RFC_5425>`__.
Systems that comply with this profile shall support message sizes of at
least 32768 octets.

.. note::

   1. Audit messages for other purposes may also be transferred on the
      same syslog connection. These messages might not conform to the
      Audit Trail Message Format.

   2. `biblioentry_title <#biblio_RFC_5425>`__ specifies mandatory
      support for 2KB messages, strongly recommends support for at least
      8KB, and does not restrict the maximum size.

   3. When a received message is longer than the receiving application
      supports, the message might be discarded or truncated. The sending
      application will not be notified.

The XML audit trail message shall be inserted into the MSG portion of
the SYSLOG-MSG element of the syslog message as defined in
`biblioentry_title <#biblio_RFC_5424>`__. The XML audit message may
contain Unicode characters that are encoded using the UTF-8 encoding
rules.

.. note::

   UTF-8 avoids utilizing the control characters that are reserved by
   the syslog protocol, but a system that is not prepared for UTF-8 may
   not be able to display these messages correctly.

The PRI field shall be set using the facility value of 10
(security/authorization messages). Most messages should have the
severity value of 5 (normal but significant), although applications may
choose other values if that is appropriate to the more detailed
information in the audit message. This means that for most audit
messages the PRI field will contain the value "<85>".

The MSGID field in the HEADER of the SYSLOG-MSG shall be set. The value
"DICOM+RFC3881" may be used for messages that comply with this profile.

The MSG field of the SYSLOG-MSG shall be present and shall be an XML
structure following the DICOM Audit Message Schema (see `DICOM Audit
Message Schema <#sect_A.5.1>`__).

The syslog message shall be created and transmitted as described in
`biblioentry_title <#biblio_RFC_5424>`__.

Any implementation that claims conformance to this Security Profile
shall describe in its conformance statement:

a. any configuration parameters relevant to
   `biblioentry_title <#biblio_RFC_5424>`__ and
   `biblioentry_title <#biblio_RFC_5425>`__.

b. Any STRUCTURED-DATA that is generated or processed.

c. Any implementation schema or message element extensions for the audit
   messages.

d. The maximum size of messages that can be sent or received.

.. _sect_A.7:

Audit Trail Message Transmission Profile - SYSLOG-UDP
-----------------------------------------------------

This profile defines the transmission of audit trail messages.
`biblioentry_title <#biblio_RFC_5426>`__ provides the mechanisms for
rapid transport of audit messages. It is the standardized successor to
the informative standard `biblioentry_title <#biblio_RFC_3164>`__, which
is widely used in a variety of settings.

The syslog port number shall be configurable, with the port number (514)
as the default.

The underlying UDP transport might not accept messages longer than the
MTU size minus the UDP header length. This may result in longer syslog
messages being truncated. When these messages are truncated the
resulting XML may be incorrect. Because of this potential for truncated
messages and other security concerns, the transmission of syslog
messages over TLS may be preferred (see `Audit Trail Message
Transmission Profile - SYSLOG-TLS <#sect_A.6>`__).

The PRI field shall be set using the facility value of 10
(security/authorization messages). Most messages should have the
severity value of 5 (normal but significant), although applications may
choose values of 4 (warning condition) if that is appropriate to the
more detailed information in the audit message. This means that for most
audit messages the PRI field will contain the value "<85>". Audit
repositories shall be prepared to deal appropriately with any incoming
PRI value.

The MSGID field in the HEADER of the SYSLOG-MSG shall be set. The value
"DICOM+RFC3881" may be used for messages that comply with this profile.

The MSG field of the SYSLOG-MSG shall be present and shall be an XML
structure following the DICOM Audit Message Schema (see `DICOM Audit
Message Schema <#sect_A.5.1>`__).

The syslog message shall be created and transmitted as described in
`biblioentry_title <#biblio_RFC_5424>`__.

Any implementation that claims conformance to this Security Profile
shall describe in its conformance statement:

a. any configuration parameters relevant to
   `biblioentry_title <#biblio_RFC_5424>`__ and
   `biblioentry_title <#biblio_RFC_5426>`__.

b. Any STRUCTURED-DATA that is generated or processed.

c. Any implementation schema or message element extensions for the audit
   messages.

d. The maximum size of messages that can be sent or received.

