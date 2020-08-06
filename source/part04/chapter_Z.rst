.. _chapter_Z:

Composite Instance Retrieve Without Bulk Data Service Class (Normative)
=======================================================================

.. _sect_Z.1:

Overview
--------

.. _sect_Z.1.1:

Scope
~~~~~

Composite Instance Retrieve Without Bulk Data Service is a service
within the DICOM Query/Retrieve Service class defined in `Query/Retrieve
Service Class (Normative) <#chapter_C>`__.The retrieve capability of
this service allows a DICOM AE to retrieve Composite Instances without
retrieving their pixel data or other potentially large Attributes as
defined in `Attributes Not Included <#sect_Z.1.3>`__.

The Enhanced Multi-Frame Image Conversion Extended Negotiation Option of
the DICOM Query/Retrieve Service class defined in `Query/Retrieve
Service Class (Normative) <#chapter_C>`__ is also supported for the
Composite Instance Retrieve Without Bulk Data Service.

.. _sect_Z.1.2:

Composite Instance Retrieve Without Bulk Data Information Model
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Retrievals are implemented against the Composite Instance Retrieve
Without Bulk Data Information Model, as defined in this Annex of the
DICOM Standard. A specific SOP Class of the Query/Retrieve Service Class
consists of an Information Model Definition and a DIMSE-C Service Group.

.. _sect_Z.1.3:

Attributes Not Included
~~~~~~~~~~~~~~~~~~~~~~~

The Attributes that shall not be included in the top level of the Data
set sent by an SCP of this Service are as defined in
`table_title <#table_Z.1-1>`__

.. table:: Attributes Not to Be Included in Instances Sent

   ======================= ===========
   Attribute Name          Tag
   ======================= ===========
   Pixel Data              (7FE0,0010)
   Float Pixel Data        (7FE0,0008)
   Double Float Pixel Data (7FE0,0009)
   Pixel Data Provider URL (0028,7FE0)
   Spectroscopy Data       (5600,0020)
   Overlay Data            (60xx,3000)
   Curve Data              (50xx,3000)
   Audio Sample Data       (50xx,200C)
   Encapsulated Document   (0042,0011)
   ======================= ===========

.. note::

   This implies that the pixel data within Icon Image Sequence
   (0088,0200) Items will be preserved.

The Waveform Data (5400,1010) Attribute shall not be included within the
Waveform Sequence (5400,0100).

Private Attributes may be preserved or discarded by a Storage SCP, as
defined in `Conformance as an SCP <#sect_B.4.1>`__. A Storage SCP that
claims conformance to Level 2 (Full) support of the Storage Service
Class may choose to return Private Attributes in the2 Retrieve Without
Bulk Data Service or not. Whether or not particular Private Attributes
are returned shall be documented in the Conformance Statement.

.. note::

   The decision as to whether or not to return a particular Private
   Attribute may be dependent on its size.

.. _sect_Z.1.4:

Service Definition
~~~~~~~~~~~~~~~~~~

Two peer DICOM AEs implement a SOP Class of the Composite Instance
Retrieve Without Bulk Data Service with one serving in the SCU role and
one serving in the SCP role. SOP Classes of the Composite Instance
Retrieve Without Bulk Data Service are implemented using the DIMSE-C
C-GET service as defined in .

The following descriptions of the DIMSE-C C-GET service provide a brief
overview of the SCU/SCP semantics:

a. A C-GET service conveys the following semantics:

   -  The SCP shall identify a set of Entities at the level of the
      retrieval based upon the values in the Unique Keys in the
      Identifier of the C-GET request. The SCP shall then generate
      C-STORE sub-operations for the corresponding storage SOP
      Instances, but shall not include Attributes as described in
      `Attributes Not Included <#sect_Z.1.3>`__ in the data sent during
      those sub-operations. These C-STORE sub-operations occur on the
      same Association as the C-GET service and the SCU/SCP roles are
      reversed for the C-STORE.

      .. note::

         If the source instance does not contain any of the Attributes
         described in `Attributes Not Included <#sect_Z.1.3>`__ then,
         the version sent via the C-STORE sub-operation would be
         identical to the original data. This is not an error.

   -  The SCP may optionally generate responses to the C-GET with status
      equal to Pending during the processing of the C-STORE
      sub-operations. These C-GET responses indicate the number of
      remaining C-STORE sub-operations and the number of C-STORE
      sub-operations returning the status of Success, Warning, and
      Failed.

   -  When the number of Remaining C-STORE sub-operations reaches zero,
      the SCP generates a final response with a status equal to Success,
      Warning, Failed, or Refused. This response shall indicate the
      number of C-STORE sub-operations returning the status of Success,
      Warning, and Failed. If the status of any C-STORE sub-operation
      was Failed a UID List shall be returned.

   -  The SCU may cancel the C-GET service by issuing a C-GET-CANCEL
      request at any time during the processing of the C-GET. The SCP
      terminates all incomplete C-STORE sub-operations and returns a
      status of Canceled.

.. _sect_Z.2:

Composite Instance Retrieve Without Bulk Data Information Model Definition
--------------------------------------------------------------------------

The Composite Instance Retrieve Without Bulk Data Information Model is
identified by the SOP Class negotiated at Association establishment
time. The SOP Class is composed of both an Information Model and a
DIMSE-C Service Group.

.. note::

   This SOP Class identifies the class of the Composite Instance
   Retrieve Without Bulk Data Information Model (i.e., not the SOP Class
   of the stored SOP Instances for which the SCP has information).

Information Model Definitions for Standard SOP Classes of the Composite
Instance Retrieve Without Bulk Data Service are defined in this Annex. A
Composite Instance Retrieve Without Bulk Data Information Model
Definition contains:

-  Entity-Relationship Model Definition

-  Key Attributes Definition

.. _sect_Z.2.1:

Entity-Relationship Model Definition
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

For any Composite Instance Retrieve Without Bulk Data Information Model,
an Entity-Relationship Model defines a hierarchy of entities, with
Attributes defined for each level in the hierarchy (e.g., Composite
Instance, Frame)..

.. _sect_Z.2.2:

Attributes Definition
~~~~~~~~~~~~~~~~~~~~~

Attributes and matching shall be as defined in section `Attributes
Definition <#sect_C.2.2>`__

.. _sect_Z.3:

Standard Composite Instance Retrieve Without Bulk Data Information Model
------------------------------------------------------------------------

One standard Composite Instance Retrieve Without Bulk Data Information
Model is defined in this Annex. The Composite Instance Retrieve Without
Bulk Data Information Model is associated with a single SOP Class. The
following Composite Instance Retrieve Without Bulk Data Information
Model is defined:

-  Retrieve Without Bulk Data

.. _sect_Z.3.1:

Composite Instance Retrieve Without Bulk Data Information Model
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Composite Instance Retrieve Without Bulk Data Information Model is
based upon a one level hierarchy:

-  Composite Instance

The Retrieve Without Bulk Data Information Model may be represented by
the entity relationship diagram shown in
`figure_title <#figure_Z.3.1-1>`__.

The Composite Instance level is the only level and contains only the SOP
Instance UID.

.. _sect_Z.4:

DIMSE-C Service Groups
----------------------

A single DIMSE-C Service is used in the construction of SOP Classes of
the Composite Instance Retrieve Without Bulk Data Service. The following
DIMSE-C operation is used:

-  C-GET

.. _sect_Z.4.1:

C-GET Operation
~~~~~~~~~~~~~~~

SCUs of the Composite Instance Retrieve Without Bulk Data Service shall
generate retrievals using the C-GET operation as described in . The
C-GET operation allows an application entity to instruct another
application entity to transfer SOP Instances without the Attributes as
described in `Attributes Not Included <#sect_Z.1.3>`__ to the initiating
application entity using the C-STORE operation. Support for the C-GET
service shall be agreed upon at Association establishment time by both
the SCU and SCP of the C-GET in order for a C-GET operation to occur
over the Association. The C-STORE Sub-operations shall be accomplished
on the same Association as the C-GET operation. Hence, the SCP of the
Query/Retrieve Service Class serves as the SCU of the Storage Service
Class.

.. note::

   The Application Entity that receives the stored SOP Instances is
   always the originator of the C-GET operation.

.. _sect_Z.4.2.1:

C-GET Service Parameters
^^^^^^^^^^^^^^^^^^^^^^^^

.. _sect_Z.4.2.1.1:

SOP Class UID
'''''''''''''

The SOP Class UID identifies the Query/Retrieve Information Model
against which the C-GET is to be performed. Support for the SOP Class
UID is implied by the Abstract Syntax UID of the Presentation Context
used by this C-GET operation.

.. _sect_Z.4.2.1.2:

Priority
''''''''

The Priority Attribute defines the requested priority of the C-GET
operation and corresponding C-STORE sub-operations with respect to other
DIMSE operations being performed by the same SCP.

Processing of priority requests is not required of SCPs. Whether or not
an SCP supports priority processing, and the meaning of the different
priority levels shall be stated in the Conformance Statement of the SCP.
The same priority shall be used for all C-STORE sub-operations.

.. _sect_Z.4.2.1.3:

Identifier
''''''''''

The C-GET request shall contain an Identifier. The C-GET response shall
conditionally contain an Identifier as required in `Response Identifier
Structure <#sect_C.4.3.1.3.2>`__.

.. note::

   The Identifier is specified as U in the definition of the C-GET
   primitive in but is specialized for use with this service.

.. _sect_Z.4.2.1.3.1:

Request Identifier Structure
                            

An Identifier in a C-GET request shall contain:

-  the Query/Retrieve Level (0008,0052) that defines the level of the
   retrieval

-  SOP Instance UID(s) (0008,0018)

-  Conditionally, the Attribute Query/Retrieve View (0008,0053). This
   Attribute may be included if Enhanced Multi-Frame Image Conversion
   has accepted during Association Extended Negotiation. It shall not be
   included otherwise.

Query/Retrieve Level (0008,0052) shall be IMAGE.

Specific Character Set (0008,0005) shall not be present.

The Keys at each level of the hierarchy and the values allowable for the
level of the retrieval are defined in the SOP Class definition for the
Query/Retrieve Information Model.

.. _sect_Z.4.2.1.4:

Status
''''''

`table_title <#table_Z.4-1>`__ defines the status code values that might
be returned in a C-GET response. General status code values and fields
related to status code values are defined for C-GET DIMSE Service in .

.. table:: C-GET Response Status Values for Composite Instance Retrieve
Without Bulk Data

   +----------------+----------------+--------------+----------------+
   | Service Status | Further        | Status Codes | Related Fields |
   |                | Meaning        |              |                |
   +================+================+==============+================+
   | Failure        | Refused: Out   | A701         | (0000,0902)    |
   |                | of resources - |              |                |
   |                | Unable to      |              |                |
   |                | calculate      |              |                |
   |                | number of      |              |                |
   |                | matches        |              |                |
   +----------------+----------------+--------------+----------------+
   | Refused: Out   | A702           | (0000,1020)  |                |
   | of resources - |                |              |                |
   | Unable to      |                | (0000,1021)  |                |
   | perform        |                |              |                |
   | sub-operations |                | (0000,1022)  |                |
   |                |                |              |                |
   |                |                | (0000,1023)  |                |
   +----------------+----------------+--------------+----------------+
   | Error: Data    | A900           | (0000,0901)  |                |
   | Set does not   |                |              |                |
   | match SOP      |                | (0000,0902)  |                |
   | Class          |                |              |                |
   +----------------+----------------+--------------+----------------+
   | Failed: Unable | Cxxx           | (0000,0901)  |                |
   | to process     |                |              |                |
   |                |                | (0000,0902)  |                |
   +----------------+----------------+--------------+----------------+
   | Cancel         | Sub-operations | FE00         | (0000,1020)    |
   |                | terminated due |              |                |
   |                | to Cancel      |              | (0000,1021)    |
   |                | Indication     |              |                |
   |                |                |              | (0000,1022)    |
   |                |                |              |                |
   |                |                |              | (0000,1023)    |
   +----------------+----------------+--------------+----------------+
   | Warning        | Sub-operations | B000         | (0000,1020)    |
   |                | Complete - One |              |                |
   |                | or more        |              | (0000,1021)    |
   |                | Failures or    |              |                |
   |                | Warnings       |              | (0000,1022)    |
   |                |                |              |                |
   |                |                |              | (0000,1023)    |
   +----------------+----------------+--------------+----------------+
   | Success        | Sub-operations | 0000         | (0000,1020)    |
   |                | Complete - No  |              |                |
   |                | Failures or    |              | (0000,1021)    |
   |                | Warnings       |              |                |
   |                |                |              | (0000,1022)    |
   |                |                |              |                |
   |                |                |              | (0000,1023)    |
   +----------------+----------------+--------------+----------------+
   | Pending        | Sub-operations | FF00         | (0000,1020)    |
   |                | are continuing |              |                |
   |                |                |              | (0000,1021)    |
   |                |                |              |                |
   |                |                |              | (0000,1022)    |
   |                |                |              |                |
   |                |                |              | (0000,1023)    |
   +----------------+----------------+--------------+----------------+

Some Failure Status Codes are implementation specific.

An SCP implementation shall assign specific failure status codes by
replacing each 'x' symbol with a hexadecimal digit in the range from 0
to F. An SCP implementation wishing to differentiate between causes of
"Failed: Unable to process" Failure Meaning shall assign those causes
specific Status Code Values within valid range specified in
`table_title <#table_Y.4-2>`__.

An SCU implementation shall recognize any Failure Status Code within the
value range specified in `table_title <#table_Y.4-2>`__ as an indicator
of the Failure Meaning stated in the table. There is no requirement for
an SCU implementation to differentiate between specific Status Codes
within the valid range.

.. _sect_Z.4.2.1.5:

Number of Remaining Sub-Operations
''''''''''''''''''''''''''''''''''

Inclusion of the Number of Remaining Sub-operations shall be as
specified in `Number of Remaining Sub-Operations <#sect_C.4.3.1.5>`__

.. _sect_Z.4.2.1.6:

Number of Completed Sub-Operations
''''''''''''''''''''''''''''''''''

Inclusion of the Number of Completed Sub-operations shall be as
specified in `Number of Completed Sub-Operations <#sect_C.4.3.1.6>`__

.. _sect_Z.4.2.1.7:

Number of Failed Sub-Operations
'''''''''''''''''''''''''''''''

Inclusion of the Number of Failed Sub-operations shall be as specified
in `Number of Failed Sub-Operations <#sect_C.4.3.1.7>`__

.. _sect_Z.4.2.1.8:

Number of Warning Sub-Operations
''''''''''''''''''''''''''''''''

Inclusion of the Number of Warning Sub-operations shall be as specified
in `Number of Warning Sub-Operations <#sect_C.4.3.1.8>`__.

.. _sect_Z.4.2.2:

C-GET SCU and C-STORE SCP Behavior
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. _sect_Z.4.2.2.1:

Baseline Behavior of SCU
''''''''''''''''''''''''

An SCU conveys the following semantics with a C-GET request:

-  The SCU shall specify one Instance UID or a list of Instance UIDs.

-  The SCU shall have proposed sufficient presentation contexts at
   Association establishment time to accommodate expected C-STORE
   sub-operations that will occur over the same Association. The SCU of
   the Query/Retrieve Service Class shall serve as the SCP of the
   Storage Service Class.

-  The SCP of the Storage Service Class shall not store the incomplete
   SOP Instance; rather the behavior is implementation defined.

-  The SCU shall accept C-GET responses with status equal to Pending
   during the processing of the C-STORE sub-operations. These responses
   indicate the number of Remaining, Completed, Failed and Warning
   C-STORE sub-operations.

-  The SCU shall interpret a C-GET response with a status equal to
   Success, Warning, Failure, or Refused as a final response. The final
   response indicates the number of Completed sub-operations and the
   number of Failed C-STORE sub-operations resulting from the C-GET
   operation. The SCU shall interpret a status of:

   -  Success to indicate that all sub-operations were successfully
      completed

   -  Failure or Refused to indicate all sub-operations were
      unsuccessful

   -  Warning in all other cases. The Number of Completed Sub-Operations
      (0000,1021), Number of Warning Sub-Operations (0000,1023), Number
      of Failed Sub-Operations (0000,1022) can be used to obtain more
      detailed information.

-  The SCU may cancel the C-GET operation by issuing a C-GET-CANCEL
   request at any time during the processing of the C-GET request. A
   C-GET response with a status of Canceled shall indicate to the SCU
   that the retrieve was canceled. Optionally, the C-GET response with a
   status of Canceled shall indicate the number of Completed, Failed,
   and Warning C-STORE sub-operations. If present, the Remaining
   sub-operations count shall contain the number of C-STORE
   sub-operations that were not initiated due to the C-GET-CANCEL
   request.

-  The SCP of the Storage Service Class shall not return a status of
   "Error: Data Set does not match SOP Class" (A9xx) or "Warning: Data
   Set does not match SOP Class" (B007) due to the absence of the
   Attributes described in `Attributes Not Included <#sect_Z.1.3>`__.

.. _sect_Z.4.2.2.2:

Extended Behavior of SCU
''''''''''''''''''''''''

The extended behavior of the SCU shall be as specified in `Extended
Behavior of SCU <#sect_C.4.3.2.2>`__, except that Relational-retrieve
shall not be supported.

.. _sect_Z.4.2.3:

C-GET SCP and C-STORE SCU Behavior
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. _sect_Z.4.2.3.1:

Baseline Behavior of SCP
''''''''''''''''''''''''

An SCP conveys the following semantics with a C-GET response:

-  The SCP shall identify a set of Entities at the level of the transfer
   based upon the values in the Unique Keys in the Identifier of the
   C-GET request.

-  The SCP shall initiate C-STORE sub-operations for the identified SOP
   Instances, but shall not include in this C-STORE sub-operation the
   Attributes described in section `Attributes Not
   Included <#sect_Z.1.3>`__. The SCP of the Query/Retrieve Service
   Class shall serve as an SCU of the Storage Service Class.

-  Apart from the Attributes listed in section `Attributes Not
   Included <#sect_Z.1.3>`__, the SOP Instance sent via the C-STORE
   sub-operation shall be unchanged, and no corresponding changes to
   other Attributes shall be made.

.. note::

   In particular, the Study, Series and SOP Instance UIDs and SOP Class
   UID will not be altered.

-  The SCP shall initiate C-STORE sub-operations over the same
   Association for all SOP Instances specified in the C-GET request.

-  A sub-operation is considered a Failure if the SCP is unable to
   initiate a C-STORE sub-operation because the Query/Retrieve SCU did
   not offer an appropriate presentation context for a given stored SOP
   Instance.

-  Optionally, the SCP may generate responses to the C-GET with status
   equal to Pending during the processing of the C-STORE sub-operations.
   These responses shall indicate the number of Remaining, Completed,
   Failure, and Warning C-STORE sub-operations.

-  When the number of Remaining sub-operations reaches zero, the SCP
   shall generate a final response with a status equal to Success,
   Warning or Failed. The status contained in the C-GET response shall
   contain:

   -  Success if all sub-operations were successfully completed

   -  Failure if all sub-operations were unsuccessful

   -  Warning in all other cases.

-  The SCP may receive a C-GET-CANCEL request at any time during the
   processing of the C-GET request. The SCP shall interrupt all C-STORE
   sub-operation processing and return a status of Canceled in the C-GET
   response. The C-GET response with a status of Canceled shall contain
   the number of Completed, Failed, and Warning C-STORE sub-operations.
   If present, the Remaining sub-operations count shall contain the
   number of C-STORE sub-operations that were not initiated due to the
   C-GET-CANCEL request.

-  If the SCP manages images in multiple alternate encodings (see
   `Alternate Representation Sequence <#sect_C.6.1.1.5.1>`__), only one
   of the alternate encodings of an image shall be used as the existing
   SOP Instance from which frames are to be extracted.

.. _sect_Z.4.2.3.2:

Extended Behavior of SCP
''''''''''''''''''''''''

The extended behavior of the SCP shall be as specified in `Extended
Behavior of SCP <#sect_C.4.3.3.2>`__, except that Relational-retrieve
shall not be supported.

.. _sect_Z.5:

Association Negotiation
-----------------------

Association establishment is the first phase of any instance of
communication between peer DICOM AEs. AEs supporting DICOM
Query/Retrieve SOP Classes utilize Association establishment negotiation
by defining the use of Application Association Information. See for an
overview of Association negotiation.

SOP Classes of the Composite Instance Retrieve Without Bulk Data
Service, which include retrieval services based on the C-GET operation,
use the SCP/SCU Role Selection Sub-Item to identify the SOP Classes that
may be used for retrieval.

.. _sect_Z.5.1:

Association Negotiation for C-GET SOP Classes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Rules are as specified in `Association Negotiation for C-GET SOP
Classes <#sect_C.5.3>`__, except that the extended negotiation sub-item,
if used, shall be used as defined in `SOP Class Extended
Negotiation <#sect_Y.5.1.1>`__.

.. note::

   1. Though converted images may be specified by their SOP Instance UID
      in the Request Identifier, which is always at the instance level,
      there remains a need for extended negotiation and specification of
      the Query/Retrieve View in order to assure that referential
      integrity is maintained within the returned SOP Instances (e.g.,
      that a reference to a SOP Instance UID is to a converted image or
      not, as appropriate).

   2. Relational-retrieval is not applicable to this SOP Class, hence
      the Extended Negotiation Sub-Item does not include the use of that
      byte.

.. _sect_Z.6:

SOP Class Definitions
---------------------

.. _sect_Z.6.1:

Composite Instance Retrieve Without Bulk Data SOP Class Group
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In the Composite Instance Retrieve Without Bulk Data Only Information
Model, only a single Retrieve Level is used.

.. table:: Retrieve Level Value for Composite Instance Retrieve Without
Bulk Data

   ================== ====================
   Retrieve Level     Value in (0008,0052)
   ================== ====================
   Composite Instance IMAGE
   ================== ====================

.. note::

   The use of the word "IMAGE" rather than "Composite Instance" is
   historical to allow backward compatibility with previous editions of
   the Standard. It should not be taken to mean that Composite Instances
   of other than image type are not included at the level indicated by
   the value IMAGE.

.. _sect_Z.6.1.1:

Composite Instance Retrieve Without Bulk Data Information Model
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. _sect_Z.6.1.1.1:

E/R Model
'''''''''

The Composite Instance Retrieve Without Bulk Data Only Information Model
has only a single level: IMAGE.

.. _sect_Z.6.1.1.2:

Composite Instance Level
''''''''''''''''''''''''

`table_title <#table_Z.6-1>`__ defines the keys at the Composite
Instance level of the Composite Instance Retrieve Without Bulk Data
Query/Retrieve Information model.

.. table:: Composite Instance Level Keys for the Composite Instance
Retrieve Without Bulk Data Information Model

   ================ =========== =================
   Attribute Name   Tag         Matching Key Type
   ================ =========== =================
   SOP Instance UID (0008,0018) U
   ================ =========== =================

.. _sect_Z.6.1.1.3:

Scope of the C-GET Commands and Sub-Operations
''''''''''''''''''''''''''''''''''''''''''''''

A C-GET request may only be performed at the IMAGE level of the
Query/Retrieve Model. A C-GET indicates that selected individual
Composite Instances, without bulk data Attributes shall be transferred.

.. _sect_Z.6.1.2:

Conformance Requirements
^^^^^^^^^^^^^^^^^^^^^^^^

An implementation may conform to one of the SOP Classes of the Composite
Instance Retrieve Without Bulk Data SOP Class Group as an SCU, SCP or
both. The Conformance Statement shall be in the format defined in .

.. _sect_Z.6.1.2.1:

SCU Conformance
'''''''''''''''

An implementation that conforms to one of the SOP Classes of the
Composite Instance Retrieve Without Bulk Data SOP Class Group as an SCU
shall support retrievals against the Query/Retrieve Information Model
described in `Composite Instance Retrieve Without Bulk Data Information
Model <#sect_Z.6.1.1>`__ using the C-GET SCU Behavior described in
`C-GET SCU and C-STORE SCP Behavior <#sect_Z.4.2.2>`__. An
implementation that conforms to one of the SOP Classes of the Composite
Instance Retrieve Without Bulk Data SOP Class Group as an SCU, and that
generates retrievals using the C-GET operation, shall state in its
Conformance Statement the Storage Service Class SOP Classes under which
it shall support the C-STORE sub-operations generated by the C-GET.

.. _sect_Z.6.1.2.2:

SCP Conformance
'''''''''''''''

An implementation that conforms to one of the SOP Classes of the
Composite Instance Retrieve Without Bulk Data SOP Class Group as an SCP
shall support retrievals against both levels of the Retrieve Information
Model described in `Composite Instance Retrieve Without Bulk Data
Information Model <#sect_Z.6.1.1>`__ using the C-GET SCP Behavior
described in `C-GET SCP and C-STORE SCU Behavior <#sect_Z.4.2.3>`__. An
implementation that conforms to one of the SOP Classes of the Composite
Instance Retrieve Without Bulk Data SOP Class Group as an SCP, and that
satisfies retrievals using the C-GET operation, shall state in its
Conformance Statement the Storage Service Class SOP Classes under which
it shall support the C-STORE sub-operations generated by the C-GET.

.. _sect_Z.6.1.3:

SOP Classes
^^^^^^^^^^^

The SOP Classes in the Composite Instance Retrieve Without Bulk Data SOP
Class Group of the Query/Retrieve Service Class identify the Composite
Instance Retrieve Without Bulk Data Only Information Model, and the
DIMSE-C operations supported. The Standard SOP Classes are listed in
`table_title <#table_Z.6.1.3-1>`__.

.. table:: SOP Classes for Composite Instance Retrieve Without Bulk Data

   +---------------------------------------+-----------------------------+
   | SOP Class Name                        | SOP Class UID               |
   +=======================================+=============================+
   | Composite Instance Retrieve Without   | 1.2.840.10008.5.1.4.1.2.5.3 |
   | Bulk Data - GET                       |                             |
   +---------------------------------------+-----------------------------+

