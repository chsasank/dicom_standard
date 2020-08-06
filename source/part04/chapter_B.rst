.. _chapter_B:

Storage Service Class (Normative)
=================================

.. _sect_B.1:

Overview
--------

.. _sect_B.1.1:

Scope
~~~~~

The Storage Service Class defines an application-level class-of-service
that facilitates the simple transfer of information Instances
(objects).. It allows one DICOM AE to send images, waveforms, reports,
etc., to another.

Information Object Definitions for Instances that are transferred under
the Storage Service Class shall adhere to the Composite Instance IOD
Information Model specified in , and include at least the Patient,
Study, and Series Information Entities.

.. _sect_B.1.2:

Service Definition
~~~~~~~~~~~~~~~~~~

Two peer DICOM AEs implement a SOP Class of the Storage Service Class
with one serving in the SCU role and one serving in the SCP role. SOP
Classes of the Storage Service Class are implemented using the C-STORE
DIMSE-C service. C-STORE is described in . A successful completion of
the C-STORE has the following semantics:

-  Both the SCU and the SCP support the type of information to be
   stored.

-  The information is stored in some medium.

-  For some time frame, the information may be accessed.

.. note::

   1. Support for Storage SOP Classes does not necessarily involve
      support for SOP Classes of the Query/Retrieve Service Class. How
      the information may be accessed is implementation dependent. It is
      required that some access method exists. This method may require
      an implementation dependent operation at the SCP of the Storage
      Service Class. The duration of the storage is also implementation
      dependent, but is described in the Conformance Statement of the
      SCP. Storage SOP Classes are intended to be used in a variety of
      environments: e.g., for modalities to transfer images to
      workstations or archives, for archives to transfer images to
      workstations or back to modalities, for workstations to transfer
      processed images to archives, etc.

   2. For the JPIP Referenced Pixel Data transfer syntaxes, transfers
      may result in storage of incomplete information in that the pixel
      data may be partially or completely transferred by some other
      mechanism at the discretion of the SCP.

.. _sect_B.2:

Behavior
--------

This Section discusses the SCU and SCP behavior for SOP Classes of the
Storage Service Class. The C-STORE DIMSE-C Service shall be the
mechanism used to transfer SOP Instances between peer DICOM AEs as
described in .

.. _sect_B.2.1:

Behavior of an SCU
~~~~~~~~~~~~~~~~~~

The SCU invokes a C-STORE DIMSE Service with a SOP Instance that meets
the requirements of the corresponding IOD. The SCU shall recognize the
status of the C-STORE service and take appropriate action upon the
success or failure of the service.

.. note::

   The appropriate action is implementation dependent. It is required
   that the SCU distinguish between successful and failed C-STORE
   responses. Appropriate action may differ according to application,
   but are described in the Conformance Statement of the SCU.

.. _sect_B.2.2:

Behavior of an SCP
~~~~~~~~~~~~~~~~~~

An SCP of a Storage SOP Class acts as a performing DIMSE-service-user
for the C-STORE Service. By performing this service successfully, the
SCP indicates that the SOP Instance has been successfully stored.

.. _sect_B.2.3:

Statuses
~~~~~~~~

`table_title <#table_B.2-1>`__ defines the specific status code values
that might be returned in a C-STORE response. General status code values
and fields related to status code values are defined for C-STORE DIMSE
Service in .

.. table:: C-STORE Status

   +----------------+----------------+--------------+----------------+
   | Service Status | Further        | Status Codes | Related Fields |
   |                | Meaning        |              |                |
   +================+================+==============+================+
   | Failure        | Refused: Out   | A7xx         | (0000,0902)    |
   |                | of resources   |              |                |
   +----------------+----------------+--------------+----------------+
   | Error: Data    | A9xx           | (0000,0901)  |                |
   | Set does not   |                |              |                |
   | match SOP      |                | (0000,0902)  |                |
   | Class          |                |              |                |
   +----------------+----------------+--------------+----------------+
   | Error: Cannot  | Cxxx           | (0000,0901)  |                |
   | understand     |                |              |                |
   |                |                | (0000,0902)  |                |
   +----------------+----------------+--------------+----------------+
   | Warning        | Coercion of    | B000         | (0000,0901)    |
   |                | Data Elements  |              |                |
   |                |                |              | (0000,0902)    |
   +----------------+----------------+--------------+----------------+
   | Data Set does  | B007           | (0000,0901)  |                |
   | not match SOP  |                |              |                |
   | Class          |                | (0000,0902)  |                |
   +----------------+----------------+--------------+----------------+
   | Elements       | B006           | (0000,0901)  |                |
   | Discarded      |                |              |                |
   |                |                | (0000,0902)  |                |
   +----------------+----------------+--------------+----------------+
   | Success        | Success        | 0000         | None           |
   +----------------+----------------+--------------+----------------+

Some Failure Status Codes are implementation specific.

An SCP implementation shall assign specific failure status codes by
replacing each 'x' symbol with a hexadecimal digit in the range from 0
to F. An SCP implementation wishing to differentiate between causes
within the same Failure Meaning shall assign those causes specific
Status Code Values within valid range specified in
`table_title <#table_B.2-1>`__.

An SCU implementation shall recognize any Failure Status Code within the
value range specified in `table_title <#table_B.2-1>`__ as an indicator
of the Failure Meaning stated in the table. There is no requirement for
an SCU implementation to differentiate between specific Status Codes
within the valid range.

.. _sect_B.3:

Association Negotiation
-----------------------

SCUs and SCPs of Storage SOP Classes operate on SOP Instances specific
to the SOP Class. They may use the SOP Class Extended Negotiation
Sub-Item defined in . This Sub-Item allows DICOM AEs to exchange
application information specific to SOP Class specifications. This is
achieved by defining the Service-class-application-information field.

SCUs may use the SOP Class Common Extended Negotiation Sub-Item defined
in . This Sub-Item allows DICOM AEs to exchange information about the
nature of the SOP Classes.

The SOP Class Extended Negotiation Sub-Item and SOP Class Common
Extended Negotiation Sub-Item negotiation is optional for storage based
SOP Classes.

The following negotiation rules apply to all DICOM SOP Classes and
Specialized SOP Classes of the Storage Service Class.

The Association-requester (Storage SCU role) in the A-ASSOCIATE request
shall convey:

-  one Abstract Syntax, in a Presentation Context, for each supported
   SOP Class of the Storage Service Class

-  optionally, one SOP Class Extended Negotiation Sub-Item, for each
   supported SOP Class of the Storage Service Class

-  optionally, one SOP Class Common Extended Negotiation Sub-Item, for
   each supported SOP Class of the Storage Service Class

The Association-acceptor (Storage SCP role) in the A-ASSOCIATE request
shall accept:

-  one Abstract Syntax, in a Presentation Context, for each supported
   SOP Class of the Storage Service Class

-  optionally, one SOP Class Extended Negotiation Sub-Item, for each
   supported SOP Class of the Storage Service Class

.. _sect_B.3.1:

Extended Negotiation
~~~~~~~~~~~~~~~~~~~~

At the time of Association establishment implementations may exchange
information about their respective capabilities, as described in and .
SCUs and SCPs may use the SOP Class Extended Negotiation Sub-Item
Structure as described in to exchange information about the level of
conformance and options supported. SCUs may use the SOP Class Common
Extended Negotiation Sub-Item defined in to exchange information about
the nature of the SOP Classes.

Extended negotiation is optional. In the event that either the SCU or
the SCP does not support extended negotiation, the defaults shall apply.

.. _sect_B.3.1.1:

Service-Class-Application-Information (A-ASSOCIATE-RQ)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The SOP Class Extended Negotiation Sub-Item is made of a sequence of
mandatory fields as defined by . `table_title <#table_B.3-1>`__ shows
the format of the Service-class-application-information field of the SOP
Class Extended Negotiation Sub-Item for SOP Classes of the Storage
Service Class in the A-ASSOCIATE-RQ.

.. table:: Service-Class-Application-Information (A-ASSOCIATE-RQ)

   +------------+---------------------------+---------------------------+
   | Item Bytes | Field Name                | Description of Field      |
   +============+===========================+===========================+
   | 1          | Level of support          | This byte field defines   |
   |            |                           | the supported storage     |
   |            |                           | level of the              |
   |            |                           | Association-requester. It |
   |            |                           | shall be encoded as an    |
   |            |                           | unsigned binary integer   |
   |            |                           | and shall use one of the  |
   |            |                           | following values:         |
   |            |                           |                           |
   |            |                           | 0 - level 0 SCP           |
   |            |                           |                           |
   |            |                           | 1 - level 1 SCP           |
   |            |                           |                           |
   |            |                           | 2 - level 2 SCP           |
   |            |                           |                           |
   |            |                           | 3 - N/A                   |
   |            |                           | Association-requester is  |
   |            |                           | SCU only                  |
   |            |                           |                           |
   |            |                           | If extended negotiation   |
   |            |                           | is not supported, the     |
   |            |                           | default shall have a      |
   |            |                           | value of 3.               |
   +------------+---------------------------+---------------------------+
   | 2          | Reserved                  | This reserved field shall |
   |            |                           | be sent with a value 00H  |
   |            |                           | but not tested to this    |
   |            |                           | value when received.      |
   +------------+---------------------------+---------------------------+
   | 3          | Level of Digital          | A Level 2 SCP may further |
   |            | Signature support         | define its behavior in    |
   |            |                           | this byte field.          |
   |            |                           |                           |
   |            |                           | 0 - The signature level   |
   |            |                           | is unspecified, the AE is |
   |            |                           | an SCU only, or the AE is |
   |            |                           | not a level 2 SCP         |
   |            |                           |                           |
   |            |                           | 1 - signature level 1     |
   |            |                           |                           |
   |            |                           | 2 - signature level 2     |
   |            |                           |                           |
   |            |                           | 3 - signature level 3     |
   |            |                           |                           |
   |            |                           | If extended negotiation   |
   |            |                           | is not supported, the     |
   |            |                           | default shall have a      |
   |            |                           | value of 0.               |
   +------------+---------------------------+---------------------------+
   | 4          | Reserved                  | This reserved field shall |
   |            |                           | be sent with a value 00H  |
   |            |                           | but not tested to this    |
   |            |                           | value when received.      |
   +------------+---------------------------+---------------------------+
   | 5          | Element Coercion          | This byte field defines   |
   |            |                           | whether the               |
   |            |                           | Association-requester may |
   |            |                           | coerce Data Elements. It  |
   |            |                           | shall be encoded as an    |
   |            |                           | unsigned binary integer   |
   |            |                           | and shall use one of the  |
   |            |                           | following values:         |
   |            |                           |                           |
   |            |                           | 0 - does not coerce any   |
   |            |                           | Data Element              |
   |            |                           |                           |
   |            |                           | 1 - may coerce Data       |
   |            |                           | Elements                  |
   |            |                           |                           |
   |            |                           | 2 - N/A -                 |
   |            |                           | Association-requester is  |
   |            |                           | SCU only                  |
   |            |                           |                           |
   |            |                           | If extended negotiation   |
   |            |                           | is not supported, the     |
   |            |                           | default shall have a      |
   |            |                           | value of 2.               |
   +------------+---------------------------+---------------------------+
   | 6          | Reserved                  | This reserved field shall |
   |            |                           | be sent with a value 00H  |
   |            |                           | but not tested to this    |
   |            |                           | value when received.      |
   +------------+---------------------------+---------------------------+

.. _sect_B.3.1.2:

Service-Class-Application-Information (A-ASSOCIATE-AC)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The SOP Class Extended Negotiation Sub-Item is made of a sequence of
mandatory fields as defined by . `table_title <#table_B.3-2>`__ shows
the format of the Service-class-application-information field of the SOP
Class Extended Negotiation Sub-Item for SOP Classes of the Storage
Service Class in the A-ASSOCIATE-AC.

.. table:: Service-Class-Application-Information (A-ASSOCIATE-AC)

   +------------+---------------------------+---------------------------+
   | Item Bytes | Field Name                | Description of Field      |
   +============+===========================+===========================+
   | 1          | Level of support          | This byte field defines   |
   |            |                           | the supported storage     |
   |            |                           | level of the              |
   |            |                           | Association-acceptor. It  |
   |            |                           | shall be encoded as an    |
   |            |                           | unsigned binary integer   |
   |            |                           | and shall use one of the  |
   |            |                           | following values:         |
   |            |                           |                           |
   |            |                           | 0 - level 0 SCP           |
   |            |                           |                           |
   |            |                           | 1 - level 1 SCP           |
   |            |                           |                           |
   |            |                           | 2 - level 2 SCP           |
   |            |                           |                           |
   |            |                           | 3 - N/A -                 |
   |            |                           | Association-acceptor is   |
   |            |                           | SCU only                  |
   |            |                           |                           |
   |            |                           | If extended negotiation   |
   |            |                           | is not supported, no      |
   |            |                           | assumptions shall be made |
   |            |                           | by the                    |
   |            |                           | Association-requester     |
   |            |                           | about the capabilities of |
   |            |                           | the Association-acceptor  |
   |            |                           | based upon this extended  |
   |            |                           | negotiation.              |
   +------------+---------------------------+---------------------------+
   | 2          | Reserved                  | This reserved field shall |
   |            |                           | be sent with a value 00H  |
   |            |                           | but not tested to this    |
   |            |                           | value when received.      |
   +------------+---------------------------+---------------------------+
   | 3          | Level of Digital          | A Level 2 SCP may further |
   |            | Signature support         | define its behavior in    |
   |            |                           | this byte field.          |
   |            |                           |                           |
   |            |                           | 0 - The signature level   |
   |            |                           | is unspecified, the AE is |
   |            |                           | an SCU only, or the AE is |
   |            |                           | not a level 2 SCP         |
   |            |                           |                           |
   |            |                           | 1 - signature level 1     |
   |            |                           |                           |
   |            |                           | 2 - signature level 2     |
   |            |                           |                           |
   |            |                           | 3 - signature level 3     |
   |            |                           |                           |
   |            |                           | If extended negotiation   |
   |            |                           | is not supported, no      |
   |            |                           | assumptions shall be made |
   |            |                           | by the                    |
   |            |                           | Association-requester     |
   |            |                           | about the capabilities of |
   |            |                           | the Association-acceptor  |
   |            |                           | based upon this extended  |
   |            |                           | negotiation.              |
   +------------+---------------------------+---------------------------+
   | 4          | Reserved                  | This reserved field shall |
   |            |                           | be sent with a value 00H  |
   |            |                           | but not tested to this    |
   |            |                           | value when received.      |
   +------------+---------------------------+---------------------------+
   | 5          | Element Coercion          | This byte field defines   |
   |            |                           | whether the               |
   |            |                           | Association-acceptor may  |
   |            |                           | coerce Data Elements. It  |
   |            |                           | shall be encoded as an    |
   |            |                           | unsigned binary integer   |
   |            |                           | and shall use one of the  |
   |            |                           | following values:         |
   |            |                           |                           |
   |            |                           | 0 - does not coerce any   |
   |            |                           | Data Element              |
   |            |                           |                           |
   |            |                           | 1 - may coerce Data       |
   |            |                           | Elements                  |
   |            |                           |                           |
   |            |                           | 2 - N/A -                 |
   |            |                           | Association-acceptor is   |
   |            |                           | SCU only                  |
   |            |                           |                           |
   |            |                           | If extended negotiation   |
   |            |                           | is not supported, no      |
   |            |                           | assumptions shall be made |
   |            |                           | by the                    |
   |            |                           | Association-requester     |
   |            |                           | about the capabilities of |
   |            |                           | the Association-acceptor  |
   |            |                           | based upon this extended  |
   |            |                           | negotiation.              |
   +------------+---------------------------+---------------------------+
   | 6          | Reserved                  | This reserved field shall |
   |            |                           | be sent with a value 00H  |
   |            |                           | but not tested to this    |
   |            |                           | value when received.      |
   +------------+---------------------------+---------------------------+

.. _sect_B.3.1.3:

Service Class UID (A-ASSOCIATE-RQ)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

SOP Class Common Extended Negotiation Sub-Item allows the SCU to convey
the Service Class UID of each proposed SOP Class.

The Storage Service Class UID shall be "1.2.840.10008.4.2".

.. _sect_B.3.1.4:

Related General SOP Classes (A-ASSOCIATE-RQ)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

A limited set of Standard SOP Classes in the Storage Service Class are
defined to have one or more Related General SOP Classes. The Related
General SOP Classes may be conveyed using the SOP Class Relationship
Extended Negotiation during association establishment as defined in .
`table_title <#table_B.3-3>`__ identifies which Standard SOP Classes
participate in this mechanism. If a Standard SOP Class is not listed in
this table, Related General SOP Classes shall not be included in a
Related Storage SOP Class Extended Negotiation Sub-Item.

.. note::

   Implementation-defined Specialized SOP Classes (see ) of the Storage
   Service Class may convey a Related General SOP Class.

.. table:: Standard and Related General SOP Classes

   +----------------------------------+----------------------------------+
   | SOP Class Name                   | Related General SOP Class Name   |
   +==================================+==================================+
   | 12-lead ECG Waveform Storage     | General ECG Waveform Storage     |
   +----------------------------------+----------------------------------+
   | Digital Mammography X-Ray Image  | Digital X-Ray Image Storage -    |
   | Storage - For Presentation       | For Presentation                 |
   +----------------------------------+----------------------------------+
   | Digital Mammography X-Ray Image  | Digital X-Ray Image Storage -    |
   | Storage - For Processing         | For Processing                   |
   +----------------------------------+----------------------------------+
   | Digital Intra-Oral X-Ray Image   | Digital X-Ray Image Storage -    |
   | Storage - For Presentation       | For Presentation                 |
   +----------------------------------+----------------------------------+
   | Digital Intra-Oral X-Ray Image   | Digital X-Ray Image Storage -    |
   | Storage - For Processing         | For Processing                   |
   +----------------------------------+----------------------------------+
   | Basic Text SR                    | Enhanced SR                      |
   +----------------------------------+----------------------------------+
   | Comprehensive SR                 |                                  |
   +----------------------------------+----------------------------------+
   | Comprehensive 3D SR              |                                  |
   +----------------------------------+----------------------------------+
   | Extensible SR                    |                                  |
   +----------------------------------+----------------------------------+
   | Enhanced SR                      | Comprehensive SR                 |
   +----------------------------------+----------------------------------+
   | Comprehensive 3D SR              |                                  |
   +----------------------------------+----------------------------------+
   | Extensible SR                    |                                  |
   +----------------------------------+----------------------------------+
   | Comprehensive SR                 | Comprehensive 3D SR              |
   +----------------------------------+----------------------------------+
   | Extensible SR                    |                                  |
   +----------------------------------+----------------------------------+
   | Comprehensive 3D SR              | Extensible SR                    |
   +----------------------------------+----------------------------------+
   | Procedure Log                    | Enhanced SR                      |
   +----------------------------------+----------------------------------+
   | Comprehensive SR                 |                                  |
   +----------------------------------+----------------------------------+
   | Comprehensive 3D SR              |                                  |
   +----------------------------------+----------------------------------+
   | Extensible SR                    |                                  |
   +----------------------------------+----------------------------------+
   | Simplified Adult Echo SR         | Enhanced SR                      |
   +----------------------------------+----------------------------------+
   | Comprehensive SR                 |                                  |
   +----------------------------------+----------------------------------+
   | Comprehensive 3D SR              |                                  |
   +----------------------------------+----------------------------------+
   | Extensible SR                    |                                  |
   +----------------------------------+----------------------------------+
   | X-Ray Radiation Dose SR          | Enhanced SR                      |
   +----------------------------------+----------------------------------+
   | Comprehensive SR                 |                                  |
   +----------------------------------+----------------------------------+
   | Comprehensive 3D SR              |                                  |
   +----------------------------------+----------------------------------+
   | Extensible SR                    |                                  |
   +----------------------------------+----------------------------------+
   | Radiopharmaceutical Radiation    | Enhanced SR                      |
   | Dose SR                          |                                  |
   +----------------------------------+----------------------------------+
   | Comprehensive SR                 |                                  |
   +----------------------------------+----------------------------------+
   | Comprehensive 3D SR              |                                  |
   +----------------------------------+----------------------------------+
   | Extensible SR                    |                                  |
   +----------------------------------+----------------------------------+
   | Patient Radiation Dose SR        | Enhanced SR                      |
   +----------------------------------+----------------------------------+
   | Comprehensive SR                 |                                  |
   +----------------------------------+----------------------------------+
   | Comprehensive 3D SR              |                                  |
   +----------------------------------+----------------------------------+
   | Extensible SR                    |                                  |
   +----------------------------------+----------------------------------+
   | Acquisition Context SR           | Enhanced SR (see note)           |
   +----------------------------------+----------------------------------+
   | Comprehensive SR (see note)      |                                  |
   +----------------------------------+----------------------------------+
   | Comprehensive 3D SR              |                                  |
   +----------------------------------+----------------------------------+
   | Extensible SR                    |                                  |
   +----------------------------------+----------------------------------+
   | Spectacle Prescription Report    | Enhanced SR                      |
   +----------------------------------+----------------------------------+
   | Macular Grid Thickness and       | Enhanced SR                      |
   | Volume Report                    |                                  |
   +----------------------------------+----------------------------------+
   | Enhanced CT Image Storage        | Legacy Converted Enhanced CT     |
   |                                  | Image Storage                    |
   +----------------------------------+----------------------------------+
   | Enhanced MR Image Storage        | Legacy Converted Enhanced MR     |
   |                                  | Image Storage                    |
   +----------------------------------+----------------------------------+
   | Enhanced PET Image Storage       | Legacy Converted Enhanced PET    |
   |                                  | Image Storage                    |
   +----------------------------------+----------------------------------+

.. note::

   The Acquisition Context SR may be encoded as Enhanced or
   Comprehensive only if it does not contain stereotactic coordinates
   (SCOORD3D).

.. _sect_B.4:

Conformance
-----------

An implementation that conforms to Storage SOP Classes shall meet the:

-  C-STORE Service requirements as defined in `Behavior <#sect_B.2>`__

-  Association requirements as defined in `Association
   Negotiation <#sect_B.3>`__

.. note::

   No SCU or SCP behavior requirements other than those in this section
   are specified. In particular, an SCP of the Storage SOP Classes may
   not attach any significance to the particular association or
   associations over which C-STORE operations are requested, nor the
   order in which C-STORE operations occur within an association. No
   constraints are placed on the operations an SCU may perform during
   any particular association, other than those defined during
   association negotiation. An SCP may not expect an SCU to perform
   C-STORE operations in a particular order.

Similarly, no semantics are attached to the closing of an Association,
such as the end of a Study or Performed Procedure Step.

.. _sect_B.4.1:

Conformance as an SCP
~~~~~~~~~~~~~~~~~~~~~

.. _sect_B.4.1.1:

Levels of Conformance
^^^^^^^^^^^^^^^^^^^^^

Three levels of conformance to the Storage SOP Classes as an SCP may be
provided:

-  Level 0 (Local). Level 0 conformance indicates that a user-defined
   subset of the Attributes of the image will be stored, and all others
   will be discarded. This subset of the Attributes shall be defined in
   the Conformance Statement of the implementer.

-  Level 1 (Base). Level 1 conformance indicates that all Type 1 and 2
   Attributes defined in the IOD associated with the SOP Class will be
   stored, and may be accessed. All other elements may be discarded. The
   SCP may, but is not required to validate that the Attributes of the
   SOP Instance meets the requirements of the IOD.

-  Level 2 (Full). Level 2 conformance indicates that all Type 1, Type
   2, and Type 3 Attributes defined in the Information Object Definition
   associated with the SOP Class, as well as any Standard Extended
   Attributes (including Private Attributes) included in the SOP
   Instance, will be stored and may be accessed. The SCP may, but is not
   required to validate that the Attributes of the SOP Instance meet the
   requirements of the IOD.

.. note::

   A Level 2 SCP may discard (not store) Type 3 Attributes that are
   empty (zero length and no Value), since the meaning of an empty Type
   3 Attribute is the same as absence of the Attribute. See definition
   of "Type 3 Optional Data Elements".

.. _sect_B.4.1.2:

Support of Additional SOP Classes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

An SCP that claims conformance to Level 2 (Full) support of the Storage
Service Class may accept any Presentation Context negotiation of a SOP
Class that specifies the Storage Service Class during the SOP Class
Common Extended Negotiation (see `Service Class UID
(A-ASSOCIATE-RQ) <#sect_B.3.1.3>`__), without asserting conformance to
that SOP Class in its Conformance Statement.

.. note::

   1. The SCP may support storage of all SOP Classes of the Storage
      Service Class, preserving all Attributes as a Level 2 SCP.

   2. This Extended Negotiation allows an SCP to determine that a
      Private SOP Class in a proposed Presentation Context follows the
      semantics of the Storage Service Class, and may be handled
      accordingly.

An SCP that claims conformance to Level 2 (Full) support of a Related
General SOP Class may accept any Presentation Context negotiation of a
SOP Class that specifies that Related General SOP Class during the SOP
Class Common Extended Negotiation, without asserting conformance to that
specialized SOP Class in its Conformance Statement.

.. note::

   1. The term "specialized" in this section is used generically,
      including both Implementation-defined Specialized SOP Classes and
      Standard SOP Classes specified in `table_title <#table_B.3-3>`__.

   2. The SCP may handle instances of such specialized SOP Classes using
      the semantics of the Related General SOP Class, but preserving all
      additional (potentially Type 1 or 2) Attributes as a Level 2 SCP.

   3. An SCP that has access to the current content of
      `table_title <#table_B.5-1>`__ might use that to determine
      acceptance of proposed Presentation Context SOP Classes. This
      allows an SCP, even without Extended Negotiation, to be able to
      identify all Standard SOP Classes of the Storage Service Class.
      Access to `table_title <#table_B.5-1>`__ may be through private
      means, or to the publication of PS3 on the web site of the DICOM
      Standards Committee. This provides an automated alternative to
      manually editing a table of supported Storage SOP Classes.

.. _sect_B.4.1.3:

Coercion of Attributes
^^^^^^^^^^^^^^^^^^^^^^

At any level of conformance, the SCP of the Storage Service Class may
modify the values of certain Attributes in order to coerce the SOP
Instance into the Query Model of the SCP. The Attributes that may be
modified are shown in `table_title <#table_B.4-1>`__.

.. table:: Attributes Subject to Coercion

   ========================== ===========
   Attribute Name             Tag
   ========================== ===========
   Patient ID                 (0010,0020)
   Issuer of Patient ID       (0010,0021)
   Other Patient IDs Sequence (0010,1002)
   Study Instance UID         (0020,000D)
   Series Instance UID        (0020,000E)
   ========================== ===========

The SCP of the Storage Service Class may modify the values of Code
Sequence Attributes to convert from one coding scheme into another. This
includes changing from deprecated values of Coding Scheme Designator
(0008,0102) or Code Value (0008,0100) to currently valid values.

If an SCP performs such a modification, it shall return a C-STORE
response with a status of Warning.

.. note::

   1. Modification of these Attributes may be necessary if the SCP is
      also an SCP of a Query/Retrieve SOP Classes. These SOP Classes are
      described in this Standard. For example, an MR scanner may be
      implemented to generate Study Instance UIDs for images generated
      on the MR. When these images are sent to an archive that is
      HIS/RIS aware, it may choose to change the UID of the study
      assigned to the study by the PACS. The mechanism by which it
      performs this coercion is implementation dependent.

   2. An SCP may, for instance, convert retired Code Values with a
      Coding Scheme Designator value of "99SDM", "SNM3" or "SRT" to the
      corresponding SCT Code Values and use the "SCT" Coding Scheme
      Designator, in accordance with the DICOM conventions for SNOMED
      (see ).

   3. Modification of Attributes that may be used to reference a SOP
      Instance by another SOP Instance (such as Study Instance UID and
      Series Instance UID Attributes) will make that reference invalid.
      Modification of these Attributes is strongly discouraged.

   4. Other Attributes may be modified/corrected by an SCP of a Storage
      SOP Class.

   5. Modification of Attributes may affect digital signatures
      referencing the content of the SOP Instance.

.. _sect_B.4.1.4:

Levels of Digital Signature
^^^^^^^^^^^^^^^^^^^^^^^^^^^

Three levels of Digital Signature support are defined for an SCP that
claims conformance to Level 2 (Full) storage support:

-  Signature Level 1. SCP may not preserve Digital Signatures and does
   not replace them.

-  Signature Level 2. SCP does not preserve the integrity of incoming
   Digital Signatures, but does validate the signatures of SOP Instances
   being stored, takes implementation-specific measures for insuring the
   integrity of data stored, and will add replacement Digital Signatures
   before sending SOP Instances elsewhere.

-  Signature Level 3. SCP does preserve the integrity of incoming
   Digital Signatures (i.e., is bit-preserving and stores and retrieves
   all Attributes regardless of whether they are defined in the IOD).

.. _sect_B.4.2:

Conformance as an SCU
~~~~~~~~~~~~~~~~~~~~~

The SCU shall generate only C-STORE requests with SOP Instances that
meet the requirements of the IOD associated with the SOP Class.

.. _sect_B.4.2.1:

SCU Fall-Back Behavior
^^^^^^^^^^^^^^^^^^^^^^

During Association Negotiation, an application may propose a specialized
SOP Class and its related general SOP Class in separate Presentation
Contexts as a Storage SCU. If the Association Acceptor rejects the
specialized SOP Class Presentation Context, but accepts the related
general SOP Class Presentation Context, the application may send
instances of the specialized SOP Class as instances of the related
general SOP Class. In this fall-back behavior, the SOP Class UID of the
instance shall be the UID of the related general SOP Class, and any
special semantics associated with the specialized SOP Class may be lost;
the SOP Instance UID shall remain the same.

.. note::

   The SCU may include the SOP Class UID of the original intended
   specialized SOP Class in the Attribute Original Specialized SOP Class
   UID (0008,001B) of the instance sent under the related general SOP
   Class. In some cases, e.g., when all intermediate storage
   applications are Level 2 SCPs, this may allow an ultimate receiver of
   the instance to recast it as an instance of the specialized SOP Class
   IOD. However, this transformation is not guaranteed.

.. _sect_B.4.3:

Conformance Statement Requirements
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

An implementation may conform to a SOP Class of the Storage Service
Class as an SCU, SCP or both. The Conformance Statement shall be in the
format defined in .

.. _sect_B.4.3.1:

Conformance Statement for an SCU
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The following issues shall be documented in the Conformance Statement of
any implementation claiming conformance to the Storage SOP Class as an
SCU:

-  The behavior of the SCU in the case of a successful C-STORE response
   status shall be described.

-  The behavior of the SCU in each case of an unsuccessful C-STORE
   response status shall be described.

-  The behavior of the SCU in the case of a Warning status received in
   response to a C-STORE operation.

-  Whether extended negotiation is supported.

-  The optional elements that may be included in Storage SOP Instances
   for each IOD supported shall be listed.

-  The standard and privately defined Functional Groups that may be
   included in Storage SOP Instances for each Multi-frame IOD that
   support Functional Groups.

-  The behavior of the SCU in the case of a C-STORE operation using a
   referenced pixel data transfer syntax such as JPIP Referenced Pixel
   Data Transfer Syntax shall be described. This includes the duration
   of validity of the reference

.. _sect_B.4.3.2:

Conformance Statement for an SCP
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The following issues shall be documented in the Conformance Statement of
any implementation claiming conformance to the Storage Service Class as
an SCP:

-  The level of conformance, as defined by `Conformance as an
   SCP <#sect_B.4.1>`__, shall be stated.

-  The level of Digital Signature support, as defined by `Conformance as
   an SCP <#sect_B.4.1>`__, shall be stated.

-  The optional elements that will be discarded (if any) shall be listed
   for each IOD supported.

-  The mechanisms by which additional SOP Classes are dynamically
   supported, as defined by `Support of Additional SOP
   Classes <#sect_B.4.1.2>`__, shall be stated.

-  The Conformance Statement shall document the policies concerning the
   Attribute Lossy Image Compression (0028,2110).

-  The behavior of the SCP in the case of a successful C-STORE operation
   shall be described. This includes the following:

   -  the access method for a stored SOP Instance

   -  the duration of the storage

-  The meaning of each case of an unsuccessful C-STORE response status
   shall be described, as well as appropriate recovery action.

-  The meaning of each case of a warning C-STORE response status shall
   be described, as well as appropriate action.

-  If the SCP performs coercion on any Attributes, this shall be stated,
   and the conditions under which it may occur shall be described.

.. _sect_B.4.4:

Specialized Conformance
~~~~~~~~~~~~~~~~~~~~~~~

Implementations may provide Specialized SOP Class conformance by
providing a proper superset of the SOP Instances to be stored.
Implementations providing Specialized SOP Class Conformance to one of
the SOP Classes defined in this Annex shall be conformant as described
in the following sections and shall include within their Conformance
Statement information as described in the following sections.

An implementation shall be permitted to conform as a Specialization of
the Standard SOP Class as an SCU, SCP or both. The Conformance Statement
shall be in the format defined in .

.. _sect_B.4.4.1:

Specialized SOP Class Identification
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Any implementation that specializes the Standard SOP Class shall define
its specialization as an Allomorphic subclass of the Standard SOP Class.
As such, the specialization shall have its own unique SOP Class
identification.

The Conformance Statement shall include a SOP Class Identification
Statement as defined in , declaring a SOP Name and SOP Class UID that
identify the Specialized SOP Class. The SOP Name is not guaranteed to be
unique (unless the implementer chooses to copyright it) but is provided
for informal identification of the SOP Class. The SOP Class UID shall
uniquely identify the Specialized SOP Class and conform to the DICOM UID
requirements as specified in .

.. _sect_B.4.4.2:

Specialized Information Object Definition
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Standard SOP Class may be specialized by supporting additional
private Attributes. The SCU Operations Statement shall describe these
specializations and be formatted as defined in . Following this
statement shall be the list of Attributes that may be sent or stored
with SOP Instances.

.. _sect_B.5:

Standard SOP Classes
--------------------

The SOP Classes in the Storage Service Class identify the Composite IODs
to be stored. `table_title <#table_B.5-1>`__ identifies Standard SOP
Classes.

.. table:: Standard SOP Classes

   +----------------+----------------+----------------+----------------+
   | SOP Class Name | SOP Class UID  | **IOD          | Specialization |
   |                |                | Specification  |                |
   |                |                | (defined in    |                |
   |                |                | )**            |                |
   +================+================+================+================+
   | Computed       | 1.2.840.100    |                |                |
   | Radiography    | 08.5.1.4.1.1.1 |                |                |
   | Image Storage  |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Digital X-Ray  | 1.2.840.10008  |                | `Digital X-Ray |
   | Image Storage  | .5.1.4.1.1.1.1 |                | Image Storage  |
   | - For          |                |                | SOP            |
   | Presentation   |                |                | Classes <#se   |
   |                |                |                | ct_B.5.1.1>`__ |
   +----------------+----------------+----------------+----------------+
   | Digital X-Ray  | 1              |                | `Digital X-Ray |
   | Image Storage  | .2.840.10008.5 |                | Image Storage  |
   | - For          | .1.4.1.1.1.1.1 |                | SOP            |
   | Processing     |                |                | Classes <#se   |
   |                |                |                | ct_B.5.1.1>`__ |
   +----------------+----------------+----------------+----------------+
   | Digital        | 1.2.840.10008  |                | `Digital       |
   | Mammography    | .5.1.4.1.1.1.2 |                | Mammography    |
   | X-Ray Image    |                |                | X-Ray Image    |
   | Storage - For  |                |                | Storage SOP    |
   | Presentation   |                |                | Classes <#se   |
   |                |                |                | ct_B.5.1.2>`__ |
   +----------------+----------------+----------------+----------------+
   | Digital        | 1              |                | `Digital       |
   | Mammography    | .2.840.10008.5 |                | Mammography    |
   | X-Ray Image    | .1.4.1.1.1.2.1 |                | X-Ray Image    |
   | Storage - For  |                |                | Storage SOP    |
   | Processing     |                |                | Classes <#se   |
   |                |                |                | ct_B.5.1.2>`__ |
   +----------------+----------------+----------------+----------------+
   | Digital        | 1.2.840.10008  |                | `Digital       |
   | Intra-Oral     | .5.1.4.1.1.1.3 |                | Intra-Oral     |
   | X-Ray Image    |                |                | X-Ray Image    |
   | Storage - For  |                |                | Storage SOP    |
   | Presentation   |                |                | Classes <#se   |
   |                |                |                | ct_B.5.1.3>`__ |
   +----------------+----------------+----------------+----------------+
   | Digital        | 1              |                | `Digital       |
   | Intra-Oral     | .2.840.10008.5 |                | Intra-Oral     |
   | X-Ray Image    | .1.4.1.1.1.3.1 |                | X-Ray Image    |
   | Storage - For  |                |                | Storage SOP    |
   | Processing     |                |                | Classes <#se   |
   |                |                |                | ct_B.5.1.3>`__ |
   +----------------+----------------+----------------+----------------+
   | CT Image       | 1.2.840.100    |                |                |
   | Storage        | 08.5.1.4.1.1.2 |                |                |
   +----------------+----------------+----------------+----------------+
   | Enhanced CT    | 1.2.840.10008  |                | `Enhanced CT   |
   | Image Storage  | .5.1.4.1.1.2.1 |                | Image Storage  |
   |                |                |                | and Legacy     |
   |                |                |                | Converted      |
   |                |                |                | Enhanced CT    |
   |                |                |                | Image Storage  |
   |                |                |                | SOP            |
   |                |                |                | Class <#se     |
   |                |                |                | ct_B.5.1.7>`__ |
   |                |                |                |                |
   |                |                |                | `Enhanced      |
   |                |                |                | Multi-Frame    |
   |                |                |                | Image SOP      |
   |                |                |                | Classes <#sec  |
   |                |                |                | t_B.5.1.23>`__ |
   +----------------+----------------+----------------+----------------+
   | Legacy         | 1.2.840.10008  |                | `Enhanced CT   |
   | Converted      | .5.1.4.1.1.2.2 |                | Image Storage  |
   | Enhanced CT    |                |                | and Legacy     |
   | Image Storage  |                |                | Converted      |
   |                |                |                | Enhanced CT    |
   |                |                |                | Image Storage  |
   |                |                |                | SOP            |
   |                |                |                | Class <#se     |
   |                |                |                | ct_B.5.1.7>`__ |
   |                |                |                |                |
   |                |                |                | `Enhanced      |
   |                |                |                | Multi-Frame    |
   |                |                |                | Image SOP      |
   |                |                |                | Classes <#sec  |
   |                |                |                | t_B.5.1.23>`__ |
   +----------------+----------------+----------------+----------------+
   | Ultrasound     | 1.2.840.10008  |                |                |
   | Multi-frame    | .5.1.4.1.1.3.1 |                |                |
   | Image Storage  |                |                |                |
   +----------------+----------------+----------------+----------------+
   | MR Image       | 1.2.840.100    |                |                |
   | Storage        | 08.5.1.4.1.1.4 |                |                |
   +----------------+----------------+----------------+----------------+
   | Enhanced MR    | 1.2.840.10008  |                | `Enhanced MR   |
   | Image Storage  | .5.1.4.1.1.4.1 |                | Image Storage  |
   |                |                |                | and Legacy     |
   |                |                |                | Converted      |
   |                |                |                | Enhanced MR    |
   |                |                |                | Image Storage  |
   |                |                |                | SOP            |
   |                |                |                | Class <#se     |
   |                |                |                | ct_B.5.1.6>`__ |
   |                |                |                |                |
   |                |                |                | `Enhanced      |
   |                |                |                | Multi-Frame    |
   |                |                |                | Image SOP      |
   |                |                |                | Classes <#sec  |
   |                |                |                | t_B.5.1.23>`__ |
   +----------------+----------------+----------------+----------------+
   | MR             | 1.2.840.10008  |                |                |
   | Spectroscopy   | .5.1.4.1.1.4.2 |                |                |
   | Storage        |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Enhanced MR    | 1.2.840.10008  |                | `Enhanced MR   |
   | Color Image    | .5.1.4.1.1.4.3 |                | Color Image    |
   | Storage        |                |                | Storage SOP    |
   |                |                |                | Class <#se     |
   |                |                |                | ct_B.5.1.8>`__ |
   |                |                |                |                |
   |                |                |                | `Enhanced      |
   |                |                |                | Multi-Frame    |
   |                |                |                | Image SOP      |
   |                |                |                | Classes <#sec  |
   |                |                |                | t_B.5.1.23>`__ |
   +----------------+----------------+----------------+----------------+
   | Legacy         | 1.2.840.10008  |                | `Enhanced MR   |
   | Converted      | .5.1.4.1.1.4.4 |                | Image Storage  |
   | Enhanced MR    |                |                | and Legacy     |
   | Image Storage  |                |                | Converted      |
   |                |                |                | Enhanced MR    |
   |                |                |                | Image Storage  |
   |                |                |                | SOP            |
   |                |                |                | Class <#se     |
   |                |                |                | ct_B.5.1.6>`__ |
   |                |                |                |                |
   |                |                |                | `Enhanced      |
   |                |                |                | Multi-Frame    |
   |                |                |                | Image SOP      |
   |                |                |                | Classes <#sec  |
   |                |                |                | t_B.5.1.23>`__ |
   +----------------+----------------+----------------+----------------+
   | Ultrasound     | 1.2.840.10008  |                |                |
   | Image Storage  | .5.1.4.1.1.6.1 |                |                |
   +----------------+----------------+----------------+----------------+
   | Enhanced US    | 1.2.840.10008  |                |                |
   | Volume Storage | .5.1.4.1.1.6.2 |                |                |
   +----------------+----------------+----------------+----------------+
   | Secondary      | 1.2.840.100    |                |                |
   | Capture Image  | 08.5.1.4.1.1.7 |                |                |
   | Storage        |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Multi-frame    | 1.2.840.10008  |                |                |
   | Single Bit     | .5.1.4.1.1.7.1 |                |                |
   | Secondary      |                |                |                |
   | Capture Image  |                |                |                |
   | Storage        |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Multi-frame    | 1.2.840.10008  |                |                |
   | Grayscale Byte | .5.1.4.1.1.7.2 |                |                |
   | Secondary      |                |                |                |
   | Capture Image  |                |                |                |
   | Storage        |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Multi-frame    | 1.2.840.10008  |                |                |
   | Grayscale Word | .5.1.4.1.1.7.3 |                |                |
   | Secondary      |                |                |                |
   | Capture Image  |                |                |                |
   | Storage        |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Multi-frame    | 1.2.840.10008  |                |                |
   | True Color     | .5.1.4.1.1.7.4 |                |                |
   | Secondary      |                |                |                |
   | Capture Image  |                |                |                |
   | Storage        |                |                |                |
   +----------------+----------------+----------------+----------------+
   | 12-lead ECG    | 1              |                |                |
   | Waveform       | .2.840.10008.5 |                |                |
   | Storage        | .1.4.1.1.9.1.1 |                |                |
   +----------------+----------------+----------------+----------------+
   | General ECG    | 1              |                |                |
   | Waveform       | .2.840.10008.5 |                |                |
   | Storage        | .1.4.1.1.9.1.2 |                |                |
   +----------------+----------------+----------------+----------------+
   | Ambulatory ECG | 1              |                |                |
   | Waveform       | .2.840.10008.5 |                |                |
   | Storage        | .1.4.1.1.9.1.3 |                |                |
   +----------------+----------------+----------------+----------------+
   | Hemodynamic    | 1              |                |                |
   | Waveform       | .2.840.10008.5 |                |                |
   | Storage        | .1.4.1.1.9.2.1 |                |                |
   +----------------+----------------+----------------+----------------+
   | Cardiac        | 1              |                |                |
   | Ele            | .2.840.10008.5 |                |                |
   | ctrophysiology | .1.4.1.1.9.3.1 |                |                |
   | Waveform       |                |                |                |
   | Storage        |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Basic Voice    | 1              |                |                |
   | Audio Waveform | .2.840.10008.5 |                |                |
   | Storage        | .1.4.1.1.9.4.1 |                |                |
   +----------------+----------------+----------------+----------------+
   | General Audio  | 1              |                |                |
   | Waveform       | .2.840.10008.5 |                |                |
   | Storage        | .1.4.1.1.9.4.2 |                |                |
   +----------------+----------------+----------------+----------------+
   | Arterial Pulse | 1              |                |                |
   | Waveform       | .2.840.10008.5 |                |                |
   | Storage        | .1.4.1.1.9.5.1 |                |                |
   +----------------+----------------+----------------+----------------+
   | Respiratory    | 1              |                |                |
   | Waveform       | .2.840.10008.5 |                |                |
   | Storage        | .1.4.1.1.9.6.1 |                |                |
   +----------------+----------------+----------------+----------------+
   | Multi-channel  | 1              |                |                |
   | Respiratory    | .2.840.10008.5 |                |                |
   | Waveform       | .1.4.1.1.9.6.2 |                |                |
   | Storage        |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Routine Scalp  | 1              |                |                |
   | Electr         | .2.840.10008.5 |                |                |
   | oencephalogram | .1.4.1.1.9.7.1 |                |                |
   | Waveform       |                |                |                |
   | Storage        |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Electromyogram | 1              |                |                |
   | Waveform       | .2.840.10008.5 |                |                |
   | Storage        | .1.4.1.1.9.7.2 |                |                |
   +----------------+----------------+----------------+----------------+
   | El             | 1              |                |                |
   | ectrooculogram | .2.840.10008.5 |                |                |
   | Waveform       | .1.4.1.1.9.7.3 |                |                |
   | Storage        |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Sleep          | 1              |                |                |
   | Electr         | .2.840.10008.5 |                |                |
   | oencephalogram | .1.4.1.1.9.7.4 |                |                |
   | Waveform       |                |                |                |
   | Storage        |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Body Position  | 1              |                |                |
   | Waveform       | .2.840.10008.5 |                |                |
   | Storage        | .1.4.1.1.9.8.1 |                |                |
   +----------------+----------------+----------------+----------------+
   | Grayscale      | 1.2.840.10008. |                |                |
   | Softcopy       | 5.1.4.1.1.11.1 |                |                |
   | Presentation   |                |                |                |
   | State Storage  |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Color Softcopy | 1.2.840.10008. |                |                |
   | Presentation   | 5.1.4.1.1.11.2 |                |                |
   | State Storage  |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Pseudo-Color   | 1.2.840.10008. |                |                |
   | Softcopy       | 5.1.4.1.1.11.3 |                |                |
   | Presentation   |                |                |                |
   | State Storage  |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Blending       | 1.2.840.10008. |                |                |
   | Softcopy       | 5.1.4.1.1.11.4 |                |                |
   | Presentation   |                |                |                |
   | State Storage  |                |                |                |
   +----------------+----------------+----------------+----------------+
   | XA/XRF         | 1.2.840.10008. |                |                |
   | Grayscale      | 5.1.4.1.1.11.5 |                |                |
   | Softcopy       |                |                |                |
   | Presentation   |                |                |                |
   | State Storage  |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Grayscale      | 1.2.840        |                | `Planar MPR    |
   | Planar MPR     | .10008.​5.​1.​ |                | Volumetric     |
   | Volumetric     | 4.​1.​1.​11.​6 |                | Presentation   |
   | Presentation   |                |                | State Storage  |
   | State Storage  |                |                | SOP            |
   |                |                |                | Classes <#sec  |
   |                |                |                | t_B.5.1.19>`__ |
   +----------------+----------------+----------------+----------------+
   | Compositing    | 1.2.840        |                | `Planar MPR    |
   | Planar MPR     | .10008.​5.​1.​ |                | Volumetric     |
   | Volumetric     | 4.​1.​1.​11.​7 |                | Presentation   |
   | Presentation   |                |                | State Storage  |
   | State Storage  |                |                | SOP            |
   |                |                |                | Classes <#sec  |
   |                |                |                | t_B.5.1.19>`__ |
   +----------------+----------------+----------------+----------------+
   | Advanced       | 1.2.840.10008. |                |                |
   | Blending       | 5.1.4.1.1.11.8 |                |                |
   | Presentation   |                |                |                |
   | State Storage  |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Volume         | 1.2.840.10008. |                | `Volume        |
   | Rendering      | 5.1.4.1.1.11.9 |                | Rendering      |
   | Volumetric     |                |                | Volumetric     |
   | Presentation   |                |                | Presentation   |
   | State Storage  |                |                | State Storage  |
   |                |                |                | SOP            |
   |                |                |                | Classes <#sec  |
   |                |                |                | t_B.5.1.24>`__ |
   +----------------+----------------+----------------+----------------+
   | Segmented      | 1              |                | `Volume        |
   | Volume         | .2.840.10008.5 |                | Rendering      |
   | Rendering      | .1.4.1.1.11.10 |                | Volumetric     |
   | Volumetric     |                |                | Presentation   |
   | Presentation   |                |                | State Storage  |
   | State Storage  |                |                | SOP            |
   |                |                |                | Classes <#sec  |
   |                |                |                | t_B.5.1.24>`__ |
   +----------------+----------------+----------------+----------------+
   | Multiple       | 1              |                | `Volume        |
   | Volume         | .2.840.10008.5 |                | Rendering      |
   | Rendering      | .1.4.1.1.11.11 |                | Volumetric     |
   | Volumetric     |                |                | Presentation   |
   | Presentation   |                |                | State Storage  |
   | State Storage  |                |                | SOP            |
   |                |                |                | Classes <#sec  |
   |                |                |                | t_B.5.1.24>`__ |
   +----------------+----------------+----------------+----------------+
   | X-Ray          | 1.2.840.10008. |                |                |
   | Angiographic   | 5.1.4.1.1.12.1 |                |                |
   | Image Storage  |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Enhanced XA    | 1.             |                |                |
   | Image Storage  | 2.840.10008.5. |                |                |
   |                | 1.4.1.1.12.1.1 |                |                |
   +----------------+----------------+----------------+----------------+
   | X-Ray          | 1.2.840.10008. |                |                |
   | Rad            | 5.1.4.1.1.12.2 |                |                |
   | iofluoroscopic |                |                |                |
   | Image Storage  |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Enhanced XRF   | 1.             |                |                |
   | Image Storage  | 2.840.10008.5. |                |                |
   |                | 1.4.1.1.12.2.1 |                |                |
   +----------------+----------------+----------------+----------------+
   | X-Ray 3D       | 1.             |                |                |
   | Angiographic   | 2.840.10008.5. |                |                |
   | Image Storage  | 1.4.1.1.13.1.1 |                |                |
   +----------------+----------------+----------------+----------------+
   | X-Ray 3D       | 1.             |                |                |
   | Craniofacial   | 2.840.10008.5. |                |                |
   | Image Storage  | 1.4.1.1.13.1.2 |                |                |
   +----------------+----------------+----------------+----------------+
   | Breast         | 1.             |                |                |
   | Tomosynthesis  | 2.840.10008.5. |                |                |
   | Image Storage  | 1.4.1.1.13.1.3 |                |                |
   +----------------+----------------+----------------+----------------+
   | Breast         | 1.             |                | `Breast        |
   | Projection     | 2.840.10008.5. |                | Projection     |
   | X-Ray Image    | 1.4.1.1.13.1.4 |                | X-Ray Image    |
   | Storage - For  |                |                | Storage SOP    |
   | Presentation   |                |                | Classes <#sec  |
   |                |                |                | t_B.5.1.18>`__ |
   +----------------+----------------+----------------+----------------+
   | Breast         | 1.             |                | `Breast        |
   | Projection     | 2.840.10008.5. |                | Projection     |
   | X-Ray Image    | 1.4.1.1.13.1.5 |                | X-Ray Image    |
   | Storage - For  |                |                | Storage SOP    |
   | Processing     |                |                | Classes <#sec  |
   |                |                |                | t_B.5.1.18>`__ |
   +----------------+----------------+----------------+----------------+
   | Intravascular  | 1.2.840.10008. |                | `Intravascular |
   | Optical        | 5.1.4.1.1.14.1 |                | OCT Image      |
   | Coherence      |                |                | Storage SOP    |
   | Tomography     |                |                | Classes <#sec  |
   | Image Storage  |                |                | t_B.5.1.13>`__ |
   | - For          |                |                |                |
   | Presentation   |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Intravascular  | 1.2.840.10008. |                | `Intravascular |
   | Optical        | 5.1.4.1.1.14.2 |                | OCT Image      |
   | Coherence      |                |                | Storage SOP    |
   | Tomography     |                |                | Classes <#sec  |
   | Image Storage  |                |                | t_B.5.1.13>`__ |
   | - For          |                |                |                |
   | Processing     |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Nuclear        | 1.2.840.1000   |                |                |
   | Medicine Image | 8.5.1.4.1.1.20 |                |                |
   | Storage        |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Parametric Map | 1.2.840.1000   |                |                |
   | Storage        | 8.5.1.4.1.1.30 |                |                |
   +----------------+----------------+----------------+----------------+
   | Raw Data       | 1.2.840.1000   |                | `Raw Data      |
   | Storage        | 8.5.1.4.1.1.66 |                | Storage SOP    |
   |                |                |                | Class <#sec    |
   |                |                |                | t_B.5.1.22>`__ |
   +----------------+----------------+----------------+----------------+
   | Spatial        | 1.2.840.10008. |                |                |
   | Registration   | 5.1.4.1.1.66.1 |                |                |
   | Storage        |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Spatial        | 1.2.840.10008. |                |                |
   | Fiducials      | 5.1.4.1.1.66.2 |                |                |
   | Storage        |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Deformable     | 1.2.840.10008. |                |                |
   | Spatial        | 5.1.4.1.1.66.3 |                |                |
   | Registration   |                |                |                |
   | Storage        |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Segmentation   | 1.2.840.10008. |                |                |
   | Storage        | 5.1.4.1.1.66.4 |                |                |
   +----------------+----------------+----------------+----------------+
   | Surface        | 1.2.840.10008. |                |                |
   | Segmentation   | 5.1.4.1.1.66.5 |                |                |
   | Storage        |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Tractography   | 1.2.840.10008. |                |                |
   | Results        | 5.1.4.1.1.66.6 |                |                |
   | Storage        |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Real World     | 1.2.840.1000   |                |                |
   | Value Mapping  | 8.5.1.4.1.1.67 |                |                |
   | Storage        |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Surface Scan   | 1.2.840.10008. |                |                |
   | Mesh Storage   | 5.1.4.1.1.68.1 |                |                |
   +----------------+----------------+----------------+----------------+
   | Surface Scan   | 1.2.840.10008. |                |                |
   | Point Cloud    | 5.1.4.1.1.68.2 |                |                |
   | Storage        |                |                |                |
   +----------------+----------------+----------------+----------------+
   | VL Endoscopic  | 1.             |                |                |
   | Image Storage  | 2.840.10008.5. |                |                |
   |                | 1.4.1.1.77.1.1 |                |                |
   +----------------+----------------+----------------+----------------+
   | Video          | 1.2.           |                |                |
   | Endoscopic     | 840.10008.5.1. |                |                |
   | Image Storage  | 4.1.1.77.1.1.1 |                |                |
   +----------------+----------------+----------------+----------------+
   | VL Microscopic | 1.             |                |                |
   | Image Storage  | 2.840.10008.5. |                |                |
   |                | 1.4.1.1.77.1.2 |                |                |
   +----------------+----------------+----------------+----------------+
   | Video          | 1.2.           |                |                |
   | Microscopic    | 840.10008.5.1. |                |                |
   | Image Storage  | 4.1.1.77.1.2.1 |                |                |
   +----------------+----------------+----------------+----------------+
   | VL             | 1.             |                |                |
   | Sli            | 2.840.10008.5. |                |                |
   | de-Coordinates | 1.4.1.1.77.1.3 |                |                |
   | Microscopic    |                |                |                |
   | Image Storage  |                |                |                |
   +----------------+----------------+----------------+----------------+
   | VL             | 1.             |                |                |
   | Photographic   | 2.840.10008.5. |                |                |
   | Image Storage  | 1.4.1.1.77.1.4 |                |                |
   +----------------+----------------+----------------+----------------+
   | Video          | 1.2.           |                |                |
   | Photographic   | 840.10008.5.1. |                |                |
   | Image Storage  | 4.1.1.77.1.4.1 |                |                |
   +----------------+----------------+----------------+----------------+
   | Ophthalmic     | 1.2.           |                |                |
   | Photography 8  | 840.10008.5.1. |                |                |
   | Bit Image      | 4.1.1.77.1.5.1 |                |                |
   | Storage        |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Ophthalmic     | 1.2.           |                |                |
   | Photography 16 | 840.10008.5.1. |                |                |
   | Bit Image      | 4.1.1.77.1.5.2 |                |                |
   | Storage        |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Stereometric   | 1.2.           |                |                |
   | Relationship   | 840.10008.5.1. |                |                |
   | Storage        | 4.1.1.77.1.5.3 |                |                |
   +----------------+----------------+----------------+----------------+
   | Ophthalmic     | 1.2.           |                |                |
   | Tomography     | 840.10008.5.1. |                |                |
   | Image Storage  | 4.1.1.77.1.5.4 |                |                |
   +----------------+----------------+----------------+----------------+
   | Wide Field     | 1.2.           |                |                |
   | Ophthalmic     | 840.10008.5.1. |                |                |
   | Photography    | 4.1.1.77.1.5.5 |                |                |
   | Stereographic  |                |                |                |
   | Projection     |                |                |                |
   | Image Storage  |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Wide Field     | 1.2.           |                |                |
   | Ophthalmic     | 840.10008.5.1. |                |                |
   | Photography 3D | 4.1.1.77.1.5.6 |                |                |
   | Coordinates    |                |                |                |
   | Image Storage  |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Ophthalmic     | 1.2.           |                |                |
   | Optical        | 840.10008.5.1. |                |                |
   | Coherence      | 4.1.1.77.1.5.7 |                |                |
   | Tomography En  |                |                |                |
   | Face Image     |                |                |                |
   | Storage        |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Ophthalmic     | 1.2.           |                |                |
   | Optical        | 840.10008.5.1. |                |                |
   | Coherence      | 4.1.1.77.1.5.8 |                |                |
   | Tomography     |                |                |                |
   | B-scan Volume  |                |                |                |
   | Analysis       |                |                |                |
   | Storage        |                |                |                |
   +----------------+----------------+----------------+----------------+
   | VL Whole Slide | 1.             |                |                |
   | Microscopy     | 2.840.10008.5. |                |                |
   | Image Storage  | 1.4.1.1.77.1.6 |                |                |
   +----------------+----------------+----------------+----------------+
   | Lensometry     | 1.2.840.10008. |                |                |
   | Measurements   | 5.1.4.1.1.78.1 |                |                |
   | Storage        |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Autorefraction | 1.2.840.10008. |                |                |
   | Measurements   | 5.1.4.1.1.78.2 |                |                |
   | Storage        |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Keratometry    | 1.2.840.10008. |                |                |
   | Measurements   | 5.1.4.1.1.78.3 |                |                |
   | Storage        |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Subjective     | 1.2.840.10008. |                |                |
   | Refraction     | 5.1.4.1.1.78.4 |                |                |
   | Measurements   |                |                |                |
   | Storage        |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Visual Acuity  | 1.2.840.10008. |                |                |
   | Measurements   | 5.1.4.1.1.78.5 |                |                |
   | Storage        |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Spectacle      | 1.2.840.10008. |                |                |
   | Prescription   | 5.1.4.1.1.78.6 |                |                |
   | Report Storage |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Ophthalmic     | 1.2.840.10008. |                |                |
   | Axial          | 5.1.4.1.1.78.7 |                |                |
   | Measurements   |                |                |                |
   | Storage        |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Intraocular    | 1.2.840.10008. |                |                |
   | Lens           | 5.1.4.1.1.78.8 |                |                |
   | Calculations   |                |                |                |
   | Storage        |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Macular Grid   | 1.2.840.10008. |                |                |
   | Thickness and  | 5.1.4.1.1.79.1 |                |                |
   | Volume Report  |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Ophthalmic     | 1.2.840.10008. |                |                |
   | Visual Field   | 5.1.4.1.1.80.1 |                |                |
   | Static         |                |                |                |
   | Perimetry      |                |                |                |
   | Measurements   |                |                |                |
   | Storage        |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Ophthalmic     | 1.2.840.10008. |                |                |
   | Thickness Map  | 5.1.4.1.1.81.1 |                |                |
   | Storage        |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Corneal        | 1.2.840.10008. |                | `Corneal       |
   | Topography Map | 5.1.4.1.1.82.1 |                | Topography Map |
   | Storage        |                |                | Storage SOP    |
   |                |                |                | Class <#sec    |
   |                |                |                | t_B.5.1.17>`__ |
   +----------------+----------------+----------------+----------------+
   | Basic Text SR  | 1              |                |                |
   | Storage        | .2.840.10008.5 |                |                |
   |                | .1.4.1.1.88.11 |                |                |
   +----------------+----------------+----------------+----------------+
   | Enhanced SR    | 1              |                |                |
   | Storage        | .2.840.10008.5 |                |                |
   |                | .1.4.1.1.88.22 |                |                |
   +----------------+----------------+----------------+----------------+
   | Comprehensive  | 1              |                |                |
   | SR Storage     | .2.840.10008.5 |                |                |
   |                | .1.4.1.1.88.33 |                |                |
   +----------------+----------------+----------------+----------------+
   | Comprehensive  | 1              |                |                |
   | 3D SR Storage  | .2.840.10008.5 |                |                |
   |                | .1.4.1.1.88.34 |                |                |
   +----------------+----------------+----------------+----------------+
   | Extensible SR  | 1              |                |                |
   | Storage        | .2.840.10008.5 |                |                |
   |                | .1.4.1.1.88.35 |                |                |
   +----------------+----------------+----------------+----------------+
   | Procedure Log  | 1              |                |                |
   | Storage        | .2.840.10008.5 |                |                |
   |                | .1.4.1.1.88.40 |                |                |
   +----------------+----------------+----------------+----------------+
   | Mammography    | 1              |                |                |
   | CAD SR Storage | .2.840.10008.5 |                |                |
   |                | .1.4.1.1.88.50 |                |                |
   +----------------+----------------+----------------+----------------+
   | Key Object     | 1              |                |                |
   | Selection      | .2.840.10008.5 |                |                |
   | Document       | .1.4.1.1.88.59 |                |                |
   | Storage        |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Chest CAD SR   | 1              |                |                |
   | Storage        | .2.840.10008.5 |                |                |
   |                | .1.4.1.1.88.65 |                |                |
   +----------------+----------------+----------------+----------------+
   | X-Ray          | 1              |                |                |
   | Radiation Dose | .2.840.10008.5 |                |                |
   | SR Storage     | .1.4.1.1.88.67 |                |                |
   +----------------+----------------+----------------+----------------+
   | Radio          | 1              |                |                |
   | pharmaceutical | .2.840.10008.5 |                |                |
   | Radiation Dose | .1.4.1.1.88.68 |                |                |
   | SR Storage     |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Colon CAD SR   | 1              |                |                |
   | Storage        | .2.840.10008.5 |                |                |
   |                | .1.4.1.1.88.69 |                |                |
   +----------------+----------------+----------------+----------------+
   | Implantation   | 1              |                |                |
   | Plan SR        | .2.840.10008.5 |                |                |
   | Document       | .1.4.1.1.88.70 |                |                |
   | Storage        |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Acquisition    | 1.2.840        |                |                |
   | Context SR     | .10008.5.​1.​4 |                |                |
   | Storage        | .​1.​1.​88.​71 |                |                |
   +----------------+----------------+----------------+----------------+
   | Simplified     | 1.2.840        |                |                |
   | Adult Echo SR  | .10008.5.​1.​4 |                |                |
   | Storage        | .​1.​1.​88.​72 |                |                |
   +----------------+----------------+----------------+----------------+
   | Patient        | 1.2.840        |                |                |
   | Radiation Dose | .10008.5.​1.​4 |                |                |
   | SR Storage     | .​1.​1.​88.​73 |                |                |
   +----------------+----------------+----------------+----------------+
   | Planned        | 1.2.840        |                |                |
   | Imaging Agent  | .10008.5.​1.​4 |                |                |
   | Administration | .​1.​1.​88.​74 |                |                |
   | SR Storage     |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Performed      | 1.2.840        |                |                |
   | Imaging Agent  | .10008.5.​1.​4 |                |                |
   | Administration | .​1.​1.​88.​75 |                |                |
   | SR Storage     |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Content        | 1.2.840.10008. |                | `Content       |
   | Assessment     | 5.1.4.1.1.90.1 |                | Assessment     |
   | Results        |                |                | Results        |
   | Storage        |                |                | Storage SOP    |
   |                |                |                | Classes <#sec  |
   |                |                |                | t_B.5.1.20>`__ |
   +----------------+----------------+----------------+----------------+
   | Encapsulated   | 1              |                |                |
   | PDF Storage    | .2.840.10008.5 |                |                |
   |                | .1.4.1.1.104.1 |                |                |
   +----------------+----------------+----------------+----------------+
   | Encapsulated   | 1              |                |                |
   | CDA Storage    | .2.840.10008.5 |                |                |
   |                | .1.4.1.1.104.2 |                |                |
   +----------------+----------------+----------------+----------------+
   | Encapsulated   | 1              |                |                |
   | STL Storage    | .2.840.10008.5 |                |                |
   |                | .1.4.1.1.104.3 |                |                |
   +----------------+----------------+----------------+----------------+
   | Encapsulated   | 1              |                |                |
   | OBJ Storage    | .2.840.10008.5 |                |                |
   |                | .1.4.1.1.104.4 |                |                |
   +----------------+----------------+----------------+----------------+
   | Encapsulated   | 1              |                |                |
   | MTL Storage    | .2.840.10008.5 |                |                |
   |                | .1.4.1.1.104.5 |                |                |
   +----------------+----------------+----------------+----------------+
   | Positron       | 1.2.840.10008  |                |                |
   | Emission       | .5.1.4.1.1.128 |                |                |
   | Tomography     |                |                |                |
   | Image Storage  |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Enhanced PET   | 1.2.840.10008  |                | `Enhanced PET  |
   | Image Storage  | .5.1.4.1.1.130 |                | Image Storage  |
   |                |                |                | SOP            |
   |                |                |                | Classes <#sec  |
   |                |                |                | t_B.5.1.16>`__ |
   |                |                |                |                |
   |                |                |                | `Enhanced      |
   |                |                |                | Multi-Frame    |
   |                |                |                | Image SOP      |
   |                |                |                | Classes <#sec  |
   |                |                |                | t_B.5.1.23>`__ |
   +----------------+----------------+----------------+----------------+
   | Legacy         | 1              | `Enhanced      |                |
   | Converted      | .2.840.10008.5 | Multi-Frame    |                |
   | Enhanced PET   | .1.4.1.1.128.1 | Image SOP      |                |
   | Image Storage  |                | Classes <#sec  |                |
   |                |                | t_B.5.1.23>`__ |                |
   +----------------+----------------+----------------+----------------+
   | Basic          | 1.2.840.10008  |                | `Basic         |
   | Structured     | .5.1.4.1.1.131 |                | Structured     |
   | Display        |                |                | Display <#se   |
   | Storage        |                |                | ct_B.5.1.9>`__ |
   +----------------+----------------+----------------+----------------+
   | CT Performed   | 1              |                | `CT Performed  |
   | Procedure      | .2.840.10008.5 |                | Procedure      |
   | Protocol       | .1.4.1.1.200.2 |                | Protocol       |
   | Storage        |                |                | Storage SOP    |
   |                |                |                | Class <#sec    |
   |                |                |                | t_B.5.1.21>`__ |
   +----------------+----------------+----------------+----------------+
   | RT Image       | 1              |                |                |
   | Storage        | .2.840.10008.5 |                |                |
   |                | .1.4.1.1.481.1 |                |                |
   +----------------+----------------+----------------+----------------+
   | RT Dose        | 1              |                |                |
   | Storage        | .2.840.10008.5 |                |                |
   |                | .1.4.1.1.481.2 |                |                |
   +----------------+----------------+----------------+----------------+
   | RT Structure   | 1              |                |                |
   | Set Storage    | .2.840.10008.5 |                |                |
   |                | .1.4.1.1.481.3 |                |                |
   +----------------+----------------+----------------+----------------+
   | RT Beams       | 1              |                |                |
   | Treatment      | .2.840.10008.5 |                |                |
   | Record Storage | .1.4.1.1.481.4 |                |                |
   +----------------+----------------+----------------+----------------+
   | RT Plan        | 1              |                |                |
   | Storage        | .2.840.10008.5 |                |                |
   |                | .1.4.1.1.481.5 |                |                |
   +----------------+----------------+----------------+----------------+
   | RT Brachy      | 1              |                |                |
   | Treatment      | .2.840.10008.5 |                |                |
   | Record Storage | .1.4.1.1.481.6 |                |                |
   +----------------+----------------+----------------+----------------+
   | RT Treatment   | 1              |                |                |
   | Summary Record | .2.840.10008.5 |                |                |
   | Storage        | .1.4.1.1.481.7 |                |                |
   +----------------+----------------+----------------+----------------+
   | RT Ion Plan    | 1              |                |                |
   | Storage        | .2.840.10008.5 |                |                |
   |                | .1.4.1.1.481.8 |                |                |
   +----------------+----------------+----------------+----------------+
   | RT Ion Beams   | 1              |                |                |
   | Treatment      | .2.840.10008.5 |                |                |
   | Record Storage | .1.4.1.1.481.9 |                |                |
   +----------------+----------------+----------------+----------------+
   | RT Physician   | 1.             |                |                |
   | Intent Storage | 2.840.10008.5. |                |                |
   |                | 1.4.1.1.481.10 |                |                |
   +----------------+----------------+----------------+----------------+
   | RT Segment     | 1.             |                |                |
   | Annotation     | 2.840.10008.5. |                |                |
   | Storage        | 1.4.1.1.481.11 |                |                |
   +----------------+----------------+----------------+----------------+
   | RT Radiation   | 1.             |                |                |
   | Set Storage    | 2.840.10008.5. |                |                |
   |                | 1.4.1.1.481.12 |                |                |
   +----------------+----------------+----------------+----------------+
   | C-Arm          | 1.             |                |                |
   | P              | 2.840.10008.5. |                |                |
   | hoton-Electron | 1.4.1.1.481.13 |                |                |
   | Radiation      |                |                |                |
   | Storage        |                |                |                |
   +----------------+----------------+----------------+----------------+
   | T              | 1.             |                |                |
   | omotherapeutic | 2.840.10008.5. |                |                |
   | Radiation      | 1.4.1.1.481.14 |                |                |
   | Storage        |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Robotic-Arm    | 1.             |                |                |
   | Radiation      | 2.840.10008.5. |                |                |
   | Storage        | 1.4.1.1.481.15 |                |                |
   +----------------+----------------+----------------+----------------+
   | RT Radiation   | 1.             |                |                |
   | Record Set     | 2.840.10008.5. |                |                |
   | Storage        | 1.4.1.1.481.16 |                |                |
   +----------------+----------------+----------------+----------------+
   | RT Radiation   | 1.             |                |                |
   | Salvage Record | 2.840.10008.5. |                |                |
   | Storage        | 1.4.1.1.481.17 |                |                |
   +----------------+----------------+----------------+----------------+
   | T              | 1.             |                |                |
   | omotherapeutic | 2.840.10008.5. |                |                |
   | Radiation      | 1.4.1.1.481.18 |                |                |
   | Record Storage |                |                |                |
   +----------------+----------------+----------------+----------------+
   | C-Arm          | 1.             |                |                |
   | P              | 2.840.10008.5. |                |                |
   | hoton-Electron | 1.4.1.1.481.19 |                |                |
   | Radiation      |                |                |                |
   | Record Storage |                |                |                |
   +----------------+----------------+----------------+----------------+
   | Robotic        | 1.             |                |                |
   | Radiation      | 2.840.10008.5. |                |                |
   | Record Storage | 1.4.1.1.481.20 |                |                |
   +----------------+----------------+----------------+----------------+
   | RT Beams       | 1.2.840.10     |                |                |
   | Delivery       | 008.5.1.4.34.7 |                |                |
   | Instruction    |                |                |                |
   | Storage        |                |                |                |
   +----------------+----------------+----------------+----------------+
   | RT Brachy      | 1.2.840.100    |                |                |
   | Application    | 08.5.1.4.34.10 |                |                |
   | Setup Delivery |                |                |                |
   | Instruction    |                |                |                |
   | Storage        |                |                |                |
   +----------------+----------------+----------------+----------------+

.. note::

   The Generic Implant Template Storage, Implant Assembly Template
   Storage, and Implant Template Group Storage SOP Classes were formerly
   specified in this table, incorrectly since they do not use the
   Patient / Study / Series / Instance information model. Those have
   been consolidated into the Non-Patient Object Storage Service Class
   (see `Non-Patient Object Storage Service Class <#chapter_GG>`__).

.. _sect_B.5.1:

Specialization for Standard SOP Classes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. _sect_B.5.1.1:

Digital X-Ray Image Storage SOP Classes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Digital X-Ray Image Storage - For Presentation SOP Class shall use
the DX IOD with an Enumerated Value of FOR PRESENTATION for Presentation
Intent Type (0008,0068).

The Digital X-Ray Image Storage - For Processing SOP Class shall use the
DX IOD with an Enumerated Value of FOR PROCESSING for Presentation
Intent Type (0008,0068).

An SCU or SCP of the Digital X-Ray Image Storage - For Processing SOP
Class shall also support the Digital X-Ray Image Storage - For
Presentation SOP Class.

.. note::

   1. The intent of this requirement is to ensure a useful level of
      interoperability by avoiding the situation where an SCU might
      support only the Digital X-Ray Image Storage - For Processing SOP
      Class and an SCP only the Digital X-Ray Image Storage - For
      Presentation SOP Class, or vice versa. The burden is therefore to
      support the Digital X-Ray Image Storage - For Presentation SOP
      Class as a "baseline".

   2. The term "support" is used in this section in the sense that an
      SCU or SCP must be capable of sending or receiving the For
      Presentation SOP Class. There is no intent to imply that an SCU
      must always send an instance of the For Presentation SOP Class
      when an instance of the For Processing SOP Class is sent.

      Nor is there any intent to imply that during Association
      establishment, that a Presentation Context for the For
      Presentation SOP Class has to be proposed by the initiator.
      However, an association acceptor may reject a For Presentation SOP
      Class Presentation Context if it accepts a For Processing SOP
      Class Presentation Context, and prefers that SOP Class, in which
      case it may no longer be able to "pass on" the object later as an
      SCU unless it is able to generate a For Presentation object.

      It is not possible for an SCP to determine from proposed
      Presentation Contexts whether or not an SCU "supports" (is capable
      of sending) both For Processing and For Presentation SOP Class
      Instances. Such a determination requires a priori knowledge of the
      information contained in the Conformance Statement for the SCU, as
      well as how the SCU is configured and operated. An SCU that
      supports both SOP Classes may well choose to only propose one or
      the other during Association establishment, depending on which
      Instances it actually intends to send over that particular
      association (although the SCU must be capable of sending instances
      of the For Presentation SOP Class if the SCP does not accept the
      For Processing).

      The intent of the requirement is that if an SCU is only capable of
      sending the For Presentation SOP Class, any SCP will be guaranteed
      to be able to receive it. Conversely, if an SCP is only capable of
      receiving the For Presentation SOP Class, any SCU will be
      guaranteed to be able to send it.

.. _sect_B.5.1.2:

Digital Mammography X-Ray Image Storage SOP Classes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Digital Mammography X-Ray Image Storage - For Presentation SOP Class
shall use the Digital Mammography IOD with an Enumerated Value of FOR
PRESENTATION for Presentation Intent Type (0008,0068).

The Digital Mammography X-Ray Image Storage - For Processing SOP Class
shall use the Digital Mammography IOD with an Enumerated Value of FOR
PROCESSING for Presentation Intent Type (0008,0068).

An SCU or SCP of the Digital Mammography X-Ray Image Storage - For
Processing SOP Class shall also support the Digital Mammography X-Ray
Image Storage - For Presentation SOP Class.

.. _sect_B.5.1.3:

Digital Intra-Oral X-Ray Image Storage SOP Classes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Digital Intra-Oral X-Ray Image Storage - For Presentation SOP Class
shall use the Digital Intra-Oral X-Ray IOD with an Enumerated Value of
FOR PRESENTATION for Presentation Intent Type (0008,0068).

The Digital Intra-Oral X-Ray Image Storage - For Processing SOP Class
shall use the Digital Intra-Oral X-Ray IOD with an Enumerated Value of
FOR PROCESSING for Presentation Intent Type (0008,0068).

An SCU or SCP of the Digital Intra-Oral X-Ray Image Storage - For
Processing SOP Class shall also support the Digital Intra-Oral X-Ray
Image Storage - For Presentation SOP Class.

.. _sect_B.5.1.4:

Softcopy Presentation State Storage SOP Classes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

See `Softcopy Presentation State Storage SOP Classes
(Normative) <#chapter_N>`__.

.. _sect_B.5.1.5:

Structured Reporting Storage SOP Classes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The requirements of `Structured Reporting Storage SOP Classes
(Normative) <#chapter_O>`__ apply to the following SOP Classes:

-  Basic Text SR

-  Extensible SR, Enhanced SR, and SOP Classes for which it is the
   Related General SOP Class

-  Comprehensive 3D SR, Comprehensive SR, and SOP Classes for which they
   are the Related General SOP Classes

-  Mammography CAD SR

-  Chest CAD SR

-  Procedure Log

-  X-Ray Radiation Dose SR

-  Radiopharmaceutical Radiation Dose SR

-  Patient Radiation Dose SR

-  Spectacle Prescription Report

-  Colon CAD SR

-  Macular Grid Thickness and Volume Report

-  Implantation Plan SR Document

-  Acquisition Context SR

-  Simplified Adult Echo SR

`Structured Reporting Storage SOP Classes (Normative) <#chapter_O>`__
requirements do not apply to the Key Object Selection Document SOP
Class.

.. _sect_B.5.1.6:

Enhanced MR Image Storage and Legacy Converted Enhanced MR Image Storage SOP Class
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

An SCP of the Enhanced MR Image Storage or Legacy Converted Enhanced MR
Image Storage SOP Class shall also support the Grayscale Softcopy
Presentation State Storage SOP Class.

.. note::

   This requirement is present in order to allow the exchange of
   graphical annotations created by an acquisition or conversion device.

.. _sect_B.5.1.7:

Enhanced CT Image Storage and Legacy Converted Enhanced CT Image Storage SOP Class
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

An SCP of the Enhanced CT Image Storage or Legacy Converted Enhanced CT
Image Storage SOP Class shall also support the Grayscale Softcopy
Presentation State Storage SOP Class.

.. note::

   This requirement is present in order to allow the exchange of
   graphical annotations created by an acquisition or conversion device.

.. _sect_B.5.1.8:

Enhanced MR Color Image Storage SOP Class
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

An SCP of the Enhanced MR Color Image Storage SOP Class shall also
support the Color Softcopy Presentation State Storage SOP Class.

.. note::

   This requirement is present in order to allow the exchange of
   graphical annotations created by an acquisition device.

.. _sect_B.5.1.9:

Basic Structured Display
^^^^^^^^^^^^^^^^^^^^^^^^

An SCU of the Basic Structured Display Storage SOP Class that creates
SOP Instances of the Class shall identify in its Conformance Statement
the Composite Storage SOP Classes and Softcopy Presentation State
Storage SOP Classes that are also supported by the SCU, and may be
referenced by Basic Structured Display SOP Instances it creates. It
shall identify in its Conformance Statement the values it may use in the
Attributes Image Box Layout Type (0072,0304) and Type of Synchronization
(0072,0434).

An SCP of the Basic Structured Display Storage SOP Class, when rendering
SOP Instances of the Class, shall preserve the aspect ratio specified by
the Nominal Screen Definition Sequence (0072,0102) Attributes Number of
Vertical Pixels (0072,0104) and Number of Horizontal Pixels (0072,0106)
without clipping.

.. note::

   1. The SCP is not required to display using the exact number of
      vertical and horizontal pixels. The SCP may use as much of its
      display screen as it desires, while maintaining the Structured
      Display aspect ratio.

   2. If the display screen has a different aspect ratio, the
      positioning of the display on the screen is unspecified (centered,
      left or right justified, top or bottom justified).

An SCP of the Basic Structured Display Storage SOP Class that is capable
of rendering SOP Instances of the Class shall identify in its
Conformance Statement the Composite Storage SOP Classes and Softcopy
Presentation State Storage SOP Classes that are also supported by the
SCP, and will be rendered when referenced by Basic Structured Display
SOP Instances for display. It shall specify in its Conformance Statement
the user display controls and interactions for the values of Image Box
Layout Type (0072,0304) and Type of Synchronization (0072,0434) that it
supports. It shall identify in its Conformance Statement its behavior
when encountering a referenced Presentation State or other Composite
Storage SOP Instance whose display it does not support, or an
unsupported value of Image Box Layout Type or Type of Synchronization;
such behavior shall include at a minimum a display to the user of the
nature of the incompatibility.

.. _sect_B.5.1.10:

Implant Template Storage SOP Classes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

See `Non-Patient Object Storage Service Class <#chapter_GG>`__.

.. note::

   The requirements of this section have been consolidated into the
   Non-Patient Object Storage Service Class (see `Template Storage SOP
   Classes <#sect_GG.6.3>`__).

.. _sect_B.5.1.11:

Ophthalmic Axial Measurements Storage SOP Class
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Ophthalmic axial measurements devices are used in the preoperative
assessment of every cataract surgery patient. Ophthalmic axial
measurements SOP Classes support ophthalmic axial measurements devices.

For a device that is both a SCU and a SCP of the Ophthalmic Axial
Measurements Storage SOP Class, in addition to the behavior for the
Storage Service Class specified in `Behavior of an SCP <#sect_B.2.2>`__,
the following additional requirements are specified for Ophthalmic Axial
Measurements Storage SOP Classes:

-  A SCP of this SOP Class shall support Level 2 Conformance as defined
   in `Conformance as an SCP <#sect_B.4.1>`__.

.. note::

   This requirement means that all Type 1, Type 2, and Type 3 Attributes
   defined in the Information Object Definition and Private Attributes
   associated with the SOP Class will be stored and may be accessed.

.. _sect_B.5.1.12:

IOL Calculation Storage SOP Class
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

IOL (intraocular lens) calculation is used in the preoperative
assessment of every cataract surgery patient. IOL Calculation SOP
Classes support IOL calculation software, which may be located either on
ophthalmic axial measurement devices or on a separate computer.

For a device that is both a SCU and a SCP of the IOL Calculation Storage
SOP Class, in addition to the behavior for the Storage Service Class
specified in `Behavior of an SCP <#sect_B.2.2>`__, the following
additional requirements are specified for IOL Calculation Storage SOP
Classes:

-  A SCP of this SOP Class shall support Level 2 Conformance as defined
   in `Conformance as an SCP <#sect_B.4.1>`__.

.. note::

   This requirement means that all Type 1, Type 2, and Type 3 Attributes
   defined in the Information Object Definition and Private Attributes
   associated with the SOP Class will be stored and may be accessed.

.. _sect_B.5.1.13:

Intravascular OCT Image Storage SOP Classes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Intravascular OCT Image Storage - For Presentation SOP Class shall
use the IVOCT IOD with an Enumerated Value of FOR PRESENTATION for
Presentation Intent Type (0008,0068).

The Intravascular OCT Image Storage - For Processing SOP Class shall use
the IVOCT IOD with an Enumerated Value of FOR PROCESSING for
Presentation Intent Type (0008,0068).

An SCU or SCP of the Intravascular OCT Image Storage - For Processing
SOP Class shall also support the Intravascular OCT Image Storage - For
Presentation SOP Class.

.. note::

   1. The intent of this requirement is to ensure a useful level of
      interoperability by avoiding the situation where an SCU might
      support only the Intravascular OCT Image Storage - For Processing
      SOP Class and an SCP only the Intravascular OCT Image Storage -
      For Presentation SOP Class, or vice versa. The burden is therefore
      to support the Intravascular OCT Image Storage - For Presentation
      SOP Class as a "baseline".

   2. The term "support" is used in this section in the sense that an
      SCU or SCP must be capable of sending or receiving the For
      Presentation SOP Class. There is no intent to imply that an SCU
      must always send an instance of the For Presentation SOP Class
      when an instance of the For Processing SOP Class is sent.

      Nor is there any intent to imply that during Association
      establishment, that a Presentation Context for the For
      Presentation SOP Class has to be proposed by the initiator.
      However, an association acceptor may reject a For Presentation SOP
      Class Presentation Context if it accepts a For Processing SOP
      Class Presentation Context, and prefers that SOP Class, in which
      case it may no longer be able to "pass on" the object later as an
      SCU unless it is able to generate a For Presentation object.

      It is not possible for an SCP to determine from proposed
      Presentation Contexts whether or not an SCU "supports" (is capable
      of sending) both For Processing and For Presentation SOP Class
      Instances. Such a determination requires a priori knowledge of the
      information contained in the Conformance Statement for the SCU, as
      well as how the SCU is configured and operated. An SCU that
      supports both SOP Classes may well choose to only propose one or
      the other during Association establishment, depending on which
      Instances it actually intends to send over that particular
      association (although the SCU must be capable of sending instances
      of the For Presentation SOP Class if the SCP does not accept the
      For Processing).

      The intent of the requirement is that if an SCU is only capable of
      sending the For Presentation SOP Class, any SCP will be guaranteed
      to be able to receive it. Conversely, if an SCP is only capable of
      receiving the For Presentation SOP Class, any SCU will be
      guaranteed to be able to send it.

.. _sect_B.5.1.14:

Ophthalmic Thickness Map Storage SOP Class
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Ophthalmic Thickness Map SOP Class encodes a topographic
representation of the thickness/height measurements of the posterior
eye.

For a device that is both a SCU and a SCP of the Ophthalmic Thickness
Map Storage SOP Class, in addition to the behavior for the Storage
Service Class specified in `Behavior of an SCP <#sect_B.2.2>`__, the
following additional requirements are specified for Ophthalmic Thickness
Map Storage SOP Classes:

-  A SCP of this SOP Class shall support Level 2 Conformance as defined
   in `Conformance as an SCP <#sect_B.4.1>`__.

.. note::

   This requirement means that all Type 1, Type 2, and Type 3 Attributes
   defined in the Information Object Definition and Private Attributes
   associated with the SOP Class will be stored and may be accessed.

.. _sect_B.5.1.15:

Enhanced PET Image Storage and Legacy Converted Enhanced PET Image Storage SOP Class
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

An SCP of the Enhanced PET Image Storage or Legacy Converted Enhanced
PET Image Storage SOP Class shall also support the Grayscale Softcopy
Presentation State Storage SOP Class.

.. note::

   This requirement is present in order to allow the exchange of
   graphical annotations created by an acquisition or conversion device.

.. _sect_B.5.1.16:

Enhanced PET Image Storage SOP Classes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

An SCP of the Enhanced PET Image Storage SOP Class shall also support
the Grayscale Softcopy Presentation State Storage SOP Class.

.. note::

   This requirement is present in order to allow the exchange of
   graphical annotations created by an acquisition device.

.. _sect_B.5.1.17:

Corneal Topography Map Storage SOP Class
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Corneal Topography Map SOP Class encodes a topographic
representation of the curvature and/or elevation measurements of corneal
anterior and posterior surfaces (e.g., maps that display corneal
curvatures, corneal elevations, and corneal power, etc.).

For a device that is both a SCU and a SCP of the Corneal Topography Map
Storage SOP Class, in addition to the behavior for the Storage Service
Class specified in `Behavior of an SCP <#sect_B.2.2>`__, the following
additional requirements are specified for Corneal Topography Map Storage
SOP Classes:

-  A SCP of this SOP Class shall support Level 2 Conformance as defined
   in `Conformance as an SCP <#sect_B.4.1>`__.

.. note::

   This requirement means that all Type 1, Type 2, and Type 3 Attributes
   defined in the Information Object Definition and Private Attributes
   associated with the SOP Class will be stored and may be accessed.

.. _sect_B.5.1.18:

Breast Projection X-Ray Image Storage SOP Classes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Breast Projection X-Ray Image Storage - For Presentation SOP Class
shall use the Breast Projection X-Ray Image IOD with an Enumerated Value
of FOR PRESENTATION for Presentation Intent Type (0008,0068).

The Breast Projection X-Ray Image Storage - For Processing SOP Class
shall use the Breast Projection X-Ray Image IOD with an Enumerated Value
of FOR PROCESSING for Presentation Intent Type (0008,0068).

An SCU or SCP of the Breast Projection X-Ray Image Storage - For
Processing SOP Class shall also support the Breast Projection X-Ray
Image Storage - For Presentation SOP Class.

.. _sect_B.5.1.19:

Planar MPR Volumetric Presentation State Storage SOP Classes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The requirements of `Planar MPR Volumetric
Transformations <#sect_FF.2.1.1>`__ apply to the following SOP Classes:

-  Grayscale Planar MPR Volumetric Presentation State Storage

-  Compositing Planar MPR Volumetric Presentation State Storage

The Grayscale Planar MPR Volumetric Presentation State Storage SOP Class
shall use the with an Enumerated Value of MONOCHROME for Pixel
Presentation (0008,9205) and shall have only a single item in the
Volumetric Presentation State Input Sequence (0070,1201).

The Compositing Planar MPR Volumetric Presentation State Storage SOP
Class shall use the with an Enumerated Value of TRUE COLOR for Pixel
Presentation (0008,9205).

.. _sect_B.5.1.20:

Content Assessment Results Storage SOP Classes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

An SCU of the Content Assessment Results Storage SOP Class that creates
SOP Instances of the Class shall identify in its Conformance Statement
the criteria for setting the Observation Significance (0082,0008).

.. _sect_B.5.1.21:

CT Performed Procedure Protocol Storage SOP Class
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The CT Performed Procedure Protocol Storage SOP Class encodes the
acquisition and reconstruction protocol parameter values used during a
specific performed CT procedure and related details.

For a device that is both a SCU and a SCP of the CT Performed Procedure
Protocol Storage SOP Class, in addition to the behavior for the Storage
Service Class specified in `Behavior of an SCP <#sect_B.2.2>`__, the
following additional requirements are specified for CT Performed
Procedure Protocol Storage SOP Classes:

-  A SCP of this SOP Class shall support Level 2 Conformance as defined
   in `Conformance as an SCP <#sect_B.4.1>`__.

.. note::

   This requirement means that all Type 1, Type 2, and Type 3 Attributes
   defined in the Information Object Definition and Private Attributes
   associated with the SOP Class will be stored and may be accessed.

.. _sect_B.5.1.22:

Raw Data Storage SOP Class
^^^^^^^^^^^^^^^^^^^^^^^^^^

For a device that is both a SCU and a SCP of the Raw Data Storage SOP
Class, in addition to the behavior for the Storage Service Class
specified in `Behavior of an SCP <#sect_B.2.2>`__, the following
additional requirements are specified for the Raw Data Storage SOP
Class:

-  An SCP of this SOP Class shall support Level 2 Conformance as defined
   in `Conformance as an SCP <#sect_B.4.1>`__.

.. note::

   This requirement means that all Type 1, Type 2, and Type 3 Attributes
   defined in the Information Object Definition and Private Attributes
   associated with the SOP Class will be stored and may be accessed.

.. _sect_B.5.1.23:

Enhanced Multi-Frame Image SOP Classes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

An SCP of any of the Enhanced Multi-Frame Image SOP Classes that makes
SOP Instances available through the Enhanced Multi-Frame Image
Conversion Extended Negotiation of the Query/Retrieve Service Class (see
`New Instance Creation for Enhanced Multi-Frame Image
Conversion <#sect_C.3.5>`__) shall provide Level 2 (Full) Storage SCP
Conformance.

.. note::

   Effective use of the Image Conversion option requires the storage of
   Type 3 Attributes.

.. _sect_B.5.1.24:

Volume Rendering Volumetric Presentation State Storage SOP Classes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The requirements of `Volume Rendering Volumetric
Transformations <#sect_FF.2.1.2>`__ apply to the following SOP Classes:

-  Volume Rendering Volumetric Presentation State SOP Class

-  Segmented Volume Rendering Volumetric Presentation State SOP Class

-  Multiple Volume Rendering Volumetric Presentation State SOP Class

The Volume Rendering Volumetric Presentation State Storage SOP Class
shall use the and include a single item in Volumetric Presentation State
Input Sequence (0070,1201) and a single item in Volume Stream Sequence
(0070,1A08). Also, the value of Crop (0070,1204) shall be NO.

The Segmented Volume Rendering Volumetric Presentation State Storage SOP
Class shall use the and include a single item in Volume Stream Sequence
(0070,1A08).

The Multiple Volume Rendering Volumetric Presentation State Storage SOP
Class shall use the and include two or more items in Volume Stream
Sequence (0070,1A08).

.. _sect_B.6:

Retired Standard SOP Classes
----------------------------

The SOP Classes in `table_title <#table_B.6-1>`__ were defined in
previous versions of the DICOM Standard. They are now retired and have
been replaced by new Standard SOP Classes shown in
`table_title <#table_B.5-1>`__.

.. note::

   Usage of the retired SOP Classes is permitted by DICOM. However, new
   implementations are strongly encouraged to implement the newer SOP
   Classes.

.. table:: Retired Standard SOP Classes

   ========================================= ============================
   SOP Class Name                            SOP Class UID
   ========================================= ============================
   Nuclear Medicine Image Storage            1.2.840.10008.5.1.4.1.1.5
   Ultrasound Image Storage                  1.2.840.10008.5.1.4.1.1.6
   Ultrasound Multi-frame Image Storage      1.2.840.10008.5.1.4.1.1.3
   X-Ray Angiographic Bi-plane Image Storage 1.2.840.10008.5.1.4.1.1.12.3
   ========================================= ============================

