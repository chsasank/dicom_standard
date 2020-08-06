.. _chapter_Y:

Composite Instance Root Retrieve Service Class (Normative)
==========================================================

.. _sect_Y.1:

Overview
--------

.. _sect_Y.1.1:

Scope
~~~~~

Composite Instance Root Retrieve Service is a service within the DICOM
Query/Retrieve Service class defined in `Query/Retrieve Service Class
(Normative) <#chapter_C>`__.The retrieve capability of this service
allows a DICOM AE to retrieve Composite Instances or selected frames
from a remote DICOM AE over a single Association or request the remote
DICOM AE to initiate a transfer of Composite Object Instances or
selected frames from image objects to another DICOM AE.

The Enhanced Multi-Frame Image Conversion Extended Negotiation Option of
the DICOM Query/Retrieve Service class defined in `Query/Retrieve
Service Class (Normative) <#chapter_C>`__ is also supported for the
Composite Instance Root Retrieve Service.

.. _sect_Y.1.2:

Composite Instance Root Retrieve Information Model
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Retrievals are implemented against the Composite Instance Root Retrieve
Information Model, as defined in this Annex of the DICOM Standard. A
specific SOP Class of the Query/Retrieve Service Class consists of an
Information Model Definition and a DIMSE-C Service Group.

.. _sect_Y.1.3:

Service Definition
~~~~~~~~~~~~~~~~~~

Two peer DICOM AEs implement a SOP Class of the Composite Instance Root
Retrieve Service with one serving in the SCU role and one serving in the
SCP role. SOP Classes of the Composite Instance Root Retrieve Service
are implemented using the DIMSE-C C-MOVE and C-GET services as defined
in .

The following descriptions of the DIMSE-C C-GET and C-MOVE services
provide a brief overview of the SCU/SCP semantics:

a. A C-MOVE service conveys the following semantics:

   -  The SCU supplies Unique and Frame Range Key values to identify the
      requested SOP Instance(s). The SCP creates new SOP instances if
      necessary and then initiates C-STORE sub-operations for the
      corresponding storage SOP Instances. These C-STORE sub-operations
      occur on a different Association than the C-MOVE service. The SCP
      role of the Retrieve SOP Class and the SCU role of the Storage SOP
      Class may be performed by different applications that may or may
      not reside on the same system. Initiation mechanism of C-STORE
      sub-operations is outside of the scope of DICOM Standard.

   -  The SCP may optionally generate responses to the C-MOVE with
      status equal to Pending during the processing of the C-STORE
      sub-operations. These C-MOVE responses indicate the number of
      Remaining C-STORE sub-operations and the number of C-STORE
      sub-operations returning the status of Success, Warning, and
      Failed.

   -  When the number of Remaining C-STORE sub-operations reaches zero,
      the SCP generates a final response with a status equal to Success,
      Warning, Failed, or Refused. This response shall indicate the
      number of C-STORE sub-operations returning the status of Success,
      Warning, and Failed. If any of the sub-operations was successful
      then a Successful UID list shall be returned. If the status of a
      C-STORE sub-operation was Failed a UID List shall be returned.

   -  The SCU may cancel the C-MOVE service by issuing a C-MOVE-CANCEL
      request at any time during the processing of the C-MOVE. The SCP
      terminates all incomplete C-STORE sub-operations and returns a
      status of Canceled.

b. A C-GET service conveys the following semantics:

   -  The SCU supplies Unique and Frame Range Key values to identify the
      requested SOP Instance(s). The SCP creates new SOP instances if
      necessary and then generates C-STORE sub-operations for the
      corresponding storage SOP Instances. These C-STORE sub-operations
      occur on the same Association as the C-GET service and the SCU/SCP
      roles are reversed for the C-STORE.

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

.. _sect_Y.2:

Composite Instance Root Retrieve Information Model Definition
-------------------------------------------------------------

The Composite Instance Root Retrieve Information Model is identified by
the SOP Class negotiated at Association establishment time. The SOP
Class is composed of both an Information Model and a DIMSE-C Service
Group.

.. note::

   This SOP Class identifies the class of the Composite Instance Root
   Retrieve Information Model (i.e., not the SOP Class of the stored SOP
   Instances for which the SCP has information).

Information Model Definitions for Standard SOP Classes of the Composite
Instance Root Retrieve Service are defined in this Annex. A Composite
Instance Root Retrieve Information Model Definition contains:

-  Entity-Relationship Model Definition

-  Key Attributes Definition

.. _sect_Y.2.1:

Entity-Relationship Model Definition
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

For any Composite Instance Root Retrieve Information Model, an
Entity-Relationship Model defines a hierarchy of entities, with
Attributes defined for each level in the hierarchy (e.g., Composite
Instance, Frame)..

.. _sect_Y.2.2:

Attributes Definition
~~~~~~~~~~~~~~~~~~~~~

Attributes and matching shall be as defined in section `Attributes
Definition <#sect_C.2.2>`__

.. _sect_Y.3:

Standard Composite Instance Root Retrieve Information Model
-----------------------------------------------------------

One standard Composite Instance Root Retrieve Information Model is
defined in this Annex. The Composite Instance Root Retrieve Information
Model is associated with a number of SOP Classes. The following
hierarchical Composite Instance Root Retrieve Information Model is
defined:

-  Composite Instance Root

.. _sect_Y.3.1:

Composite Instance Root Information Model
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Composite Instance Root Information Model is based upon a two level
hierarchy:

-  Composite Instance

-  Frame

The Composite Instance level is the top level and contains only the SOP
Instance UID. The Frame level is below the Composite Instance level and
contains only the Attributes that refer to a selection of the frames
from a single multi-frame image object.

.. _sect_Y.3.2:

Construction and Interpretation of Frame Range Keys
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The following rules for the use of Frame Range Keys apply to both an SCU
creating such keys and to an SCP interpreting them.

.. _sect_Y.3.2.1:

Frame List definitions
^^^^^^^^^^^^^^^^^^^^^^

The selection of frames to be included in a new created SOP Instance
made in response to a FRAME level Composite Instance Root Retrieve
request shall be defined by one of the mechanisms defined in this
section, and the list of frames so specified shall be referred to as the
"Frame List".

.. note::

   1. Re-ordering of frames is not supported, and order of the frames in
      the Frame List will always be the same as in the original SOP
      Instance.

   2. New allowable frame selection mechanisms may be defined in the
      future by the addition of new SOP Classes

.. _sect_Y.3.2.1.1:

Simple Frame List
'''''''''''''''''

Simple Frame List (0008,1161) is a multi-valued Attribute containing a
list of frame numbers, each specifying a frame to be included in the
returned object. The first frame of the source instance shall be denoted
as frame number 1.

The frame numbers in the list shall not contain any duplicates, and
shall increase monotonically.

.. note::

   Due to the use of UL for this element, a maximum of 16383 values may
   be specified, as only a 2 byte length is available when an explicit
   VR Transfer Syntax is used.

.. _sect_Y.3.2.1.2:

Calculated Frame List
'''''''''''''''''''''

Calculated Frame List (0008,1162) is a multi-valued Attribute containing
a list of 3-tuples, each representing a sub-range of frames to be
included in the returned object. The first frame of the source instance
shall be denoted as frame number 1.For each 3-tuple: .

-  The first number shall be the frame number of the first frame of the
   sub-range.

-  The second number shall be the upper limit of the sub-range, and
   shall be greater than or equal to the first number.

-  The third number shall be the increment between requested frames of
   the sub-range. This shall be greater than zero.

The difference between the first and second numbers is not required to
be an exact multiple of the increment.

If the difference between the first and second numbers is an exact
multiple of the increment, then the last frame of the sub-range shall be
the second number.

If the first number is greater than the number of frames in the
referenced SOP Instance then that sub-range shall be ignored.

The sub-ranges shall be non-overlapping such that the sequence of frame
numbers determined by concatenating all the sub-ranges shall not contain
any duplicates, and shall increase monotonically. A value of FFFFFFFFH
or any value greater than the number of frames in the referenced SOP
Instance as the second value shall denote the end of the set of frames
in the referenced SOP Instance, and may only occur in the last 3-tuple.

.. note::

   For example, if the Calculated Frame List contains 6 values, 2, 9, 3,
   12, FFFFFFFFH, 5 and is applied to an Instance containing 25 frames.
   The resulting Frame List will contain the values 2, 5, 8, 12, 17 and
   22.

.. _sect_Y.3.2.1.3:

Time Range
''''''''''

Time Range (0008,1163) contains the start and end times to be included
in the returned object. Times are in seconds, relative to the value of
the Content Time (0008,0033) in the parent object.

The range shall include all frames between the specified times including
any frames at the specified times.

The range may be expanded as a consequence of the format in which the
information is stored. Where such expansion occurs, any embedded audio
data shall be similarly selected. Under all circumstances, the returned
Composite SOP Instance shall retain the relationship between image and
audio data.

.. note::

   For MPEG-2, MPEG-4 AVC/H.264 and HEVC/H.265 this would be to the
   nearest surrounding Key Frames.

For JPEG 2000 Part 2, this would be to nearest surrounding precinct or
tile boundary

Time Range shall only be used to specify extraction from SOP instances
where the times of frames can be ascertained using one or more of the
following Attributes:

-  Frame Time (0018,1063)

-  Frame Time Vector (0018,1065)

-  Frame Reference DateTime (0018,9151) in the Frame Content Sequence
   (0020,9111)

.. _sect_Y.3.3:

New Instance Creation At the Frame Level
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

When a C-MOVE or C-GET operation is performed on a source Composite
Instance at the FRAME level then the SCP shall create a new Composite
Instance according to the following rules:

-  The new Composite Instance shall be extracted from the source
   Composite Instance specified by the SOP Instance UID Unique Key
   present at the Composite Instance Level.

-  The new Composite Instance shall be an instance of the same SOP Class
   as the source Composite Instance.

-  The new Composite Instance shall have a new SOP Instance UID.

-  The new Composite Instance shall be a valid SOP Instance.

.. note::

   The new Composite Instance is required to be internally consistent
   and valid. This may require the SCP to make consistent modification
   of any Attributes that reference frames or the relationship between
   them such as start time, time offsets, and modifying the Per-frame
   Functional Group Sequence (5200,9230).

-  The new Composite Instance shall contain the frames from the source
   Composite Object as requested in the Requested Frame List. The
   Requested Frame List shall be interpreted according to the rules in
   `Construction and Interpretation of Frame Range
   Keys <#sect_Y.3.2>`__. The frames shall be in the same order as in
   the source Composite Instance.

-  The new Composite Instance shall include the Frame Extraction Module,
   which shall contain appropriate Attributes from the identifier of the
   C-GET or C-MOVE request that caused this instance to be created. If
   the Frame Extraction Module already exists in the source Composite
   Instance, then a new item shall be appended as an additional item
   into the Frame Extraction Sequence.

-  The new Composite Instance shall contain the Contributing Equipment
   Sequence (0018,A001). If the source Composite Object contains the
   Contributing Equipment Sequence, then a new Item shall be appended to
   the copy of the sequence in the new Composite Instance, and if the
   source Composite Object does not contain the Contributing Equipment
   Sequence, then it shall be created, containing one new Item. In
   either case, the new Item shall describe the equipment that is
   extracting the frames, and the Purpose of Reference Code Sequence
   (0040,A170) within the Item shall be (109105, DCM, "Frame Extracting
   Equipment").

.. note::

   The existing General Equipment Module cannot be used to hold details
   of the creating equipment, as it is a Series level Module. The new
   Composite Instance is part of the same Series as the source Instance,
   and therefore the Series level information cannot be altered.

-  The new Composite Instance shall have the same Patient, Study and
   Series level information as the source Instance, including Study and
   Series Instance UIDs.

-  The new Composite Instance shall have the same values for the
   Attributes of the Image Pixel Module of the source Composite Instance
   except that the Pixel Data Provider URL (0028,7FE0) Attribute shall
   not be present,Pixel Data (7FE0,0010) shall be replaced by the subset
   of frames, as specified in section `New Instance Creation At the
   Frame Level <#sect_Y.3.3>`__, and Number of Frames (0028,0008) shall
   contain the number of frames in the new Composite Instance.

-  The new Composite Instance shall have the same values for other Type
   1 and Type 2 Image level Attributes that are not otherwise specified.
   Other Attributes may be included in the new Composite Instance if
   consistent with the new Composite Instance.

.. note::

   In most cases private Attributes should not be copied unless their
   full significance is known. See for more guidance.

-  The new Composite Instance shall not be contained in a Concatenation.
   This means that it shall not contain a Concatenation UID (0020,9161)
   Attribute or other Concatenation Attributes. If the existing
   Composite Instance contains such Attributes, they shall not be
   included in the new Composite Instance.

.. _sect_Y.4:

DIMSE-C Service Groups
----------------------

A single DIMSE-C Service is used in the construction of SOP Classes of
the Composite Instance Root Retrieve Service. The following DIMSE-C
operation is used:

-  C-MOVE

-  C-GET

.. _sect_Y.4.1:

C-MOVE Operation
~~~~~~~~~~~~~~~~

SCUs of the Composite Instance Root Retrieve Service shall generate
retrievals using the C-MOVE operation as described in .The C-MOVE
operation allows an application entity to instruct another application
entity to transfer stored SOP Instances or new SOP Instances extracted
from such stored SOP Instances to another application entity using the
C-STORE operation. Support for the C-MOVE service shall be agreed upon
at Association establishment time by both the SCU and SCP of the C-MOVE
in order for a C-MOVE operation to occur over the Association. The
C-STORE sub-operations shall always be accomplished over an Association
different from the Association that accomplishes the CMOVE operation.
Hence, the SCP of the Query/Retrieve Service Class serves as the SCU of
the Storage Service Class.

.. note::

   The application entity that receives the stored SOP Instances may or
   may not be the originator of the C-MOVE operation.

A C-MOVE request may be performed to any level of the Composite Object
Instance Root Retrieve Information Model,and the expected SCP behavior
depends on the level selected.

.. _sect_Y.4.1.1:

C-MOVE Service Parameters
^^^^^^^^^^^^^^^^^^^^^^^^^

.. _sect_Y.4.1.1.1:

SOP Class UID
'''''''''''''

The SOP Class UID identifies the Query/Retrieve Information Model
against which the C-MOVE is to be performed. Support for the SOP Class
UID is implied by the Abstract Syntax UID of the Presentation Context
used by this C-MOVE operation.

.. _sect_Y.4.1.1.2:

Priority
''''''''

The Priority Attribute defines the requested priority of the C-MOVE
operation and corresponding C-STORE sub-operations with respect to other
DIMSE operations being performed by the same SCP.

Processing of priority requests is not required of SCPs. Whether or not
an SCP supports priority processing, and the meaning of the different
priority levels shall be stated in the Conformance Statement of the SCP.
The same priority shall be used for all C-STORE sub-operations.

.. _sect_Y.4.1.1.3:

Identifier
''''''''''

The C-MOVE request shall contain an Identifier. The C-MOVE response
shall conditionally contain an Identifier as required in `Response
Identifier Structure <#sect_C.4.3.1.3.2>`__.

.. note::

   The Identifier is specified as U in the definition of the C-MOVE
   primitive in but is specialized for use with this service.

.. _sect_Y.4.1.1.3.1:

Request Identifier Structure
                            

An Identifier in a C-MOVE request shall contain:

-  the Query/Retrieve Level (0008,0052) that defines the level of the
   retrieval

-  SOP Instance UID(s) (0008,0018)

-  One of the Frame Range Keys if present in the Information Model for
   the level of the Retrieval

-  Conditionally, the Attribute Query/Retrieve View (0008,0053). This
   Attribute may be included if Enhanced Multi-Frame Image Conversion
   has accepted during Association Extended Negotiation. It shall not be
   included otherwise.

Specific Character Set (0008,0005) shall not be present.

The Keys at each level of the hierarchy and the values allowable for the
level of the retrieval shall be defined in the SOP Class definition for
the Query/Retrieve Information Model.

.. _sect_Y.4.1.1.4:

Status
''''''

`table_title <#table_Y.4-1>`__ defines the status code values that might
be returned in a C-MOVE response. General status code values and fields
related to status code values are defined for C-MOVE DIMSE Service in .

.. table:: C-MOVE Response Status Values for Composite Instance Root
Retrieve

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
   | Refused: Move  | A801           | (0000,0902)  |                |
   | Destination    |                |              |                |
   | unknown        |                |              |                |
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
   | Failed: None   | AA00           | (0000,0902)  |                |
   | of the frames  |                |              |                |
   | requested were |                |              |                |
   | found in the   |                |              |                |
   | SOP Instance   |                |              |                |
   +----------------+----------------+--------------+----------------+
   | Failed: Unable | AA01           | (0000,0902)  |                |
   | to create new  |                |              |                |
   | object for     |                |              |                |
   | this SOP Class |                |              |                |
   +----------------+----------------+--------------+----------------+
   | Failed: Unable | AA02           | (0000,0902)  |                |
   | to extract     |                |              |                |
   | frames         |                |              |                |
   +----------------+----------------+--------------+----------------+
   | Failed:        | AA03           | (0000,0902)  |                |
   | Time-based     |                |              |                |
   | request        |                |              |                |
   | received for a |                |              |                |
   | non-time-based |                |              |                |
   | original SOP   |                |              |                |
   | Instance.      |                |              |                |
   +----------------+----------------+--------------+----------------+
   | Failed:        | AA04           | (0000,0901)  |                |
   | Invalid        |                |              |                |
   | Request        |                | (0000,0902)  |                |
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
`table_title <#table_Y.4-1>`__.

An SCU implementation shall recognize any Failure Status Code within the
value range specified in `table_title <#table_Y.4-1>`__ as an indicator
of the Failure Meaning stated in the table. There is no requirement for
an SCU implementation to differentiate between specific Status Codes
within the valid range.

.. _sect_Y.4.1.1.5:

Number of Remaining Sub-Operations
''''''''''''''''''''''''''''''''''

Inclusion of the Number of Remaining Sub-operations shall be as
specified in `Number of Remaining Sub-Operations <#sect_C.4.2.1.6>`__

.. _sect_Y.4.1.1.6:

Number of Completed Sub-Operations
''''''''''''''''''''''''''''''''''

Inclusion of the Number of Completed Sub-operations shall be as
specified in `Number of Completed Sub-Operations <#sect_C.4.2.1.7>`__

.. _sect_Y.4.1.1.7:

Number of Failed Sub-Operations
'''''''''''''''''''''''''''''''

Inclusion of the Number of Failed Sub-operations shall be as specified
in `Number of Failed Sub-Operations <#sect_C.4.2.1.8>`__

.. _sect_Y.4.1.1.8:

Number of Warning Sub-Operations
''''''''''''''''''''''''''''''''

Inclusion of the Number of Warning Sub-operations shall be as specified
in `Number of Warning Sub-Operations <#sect_C.4.2.1.9>`__.

.. _sect_Y.4.1.2:

C-MOVE SCU Behavior
^^^^^^^^^^^^^^^^^^^

.. _sect_Y.4.1.2.1:

Baseline Behavior of SCU
''''''''''''''''''''''''

An SCU conveys the following semantics with a C-MOVE request:

-  If the Retrieve Level (0000,0052) is IMAGE, the SCU shall specify one
   SOP Instance UID or a list of SOP Instance UIDs.

-  If the Retrieve Level (0000,0052) is FRAME, the SCU shall specify the
   single SOP Instance UID of the item from which the new Composite SOP
   Instance should be extracted and the requested Frame List. The
   Requested Frame List shall be constructed as defined in `Construction
   and Interpretation of Frame Range Keys <#sect_Y.3.2>`__.

-  The SCU shall accept C-MOVE responses with status equal to Pending
   during the processing of the C-STORE sub-operations. These responses
   indicate the number of Remaining, Completed, Failed and Warning
   C-STORE sub-operations.

-  The SCU shall interpret a C-MOVE response with a status equal to
   Success, Warning, Failure, or Refused as a final response. The final
   response indicates the number of Completed sub-operations and the
   number of Failed C-STORE sub-operations resulting from the C-MOVE
   operation. The SCU shall interpret a status of:

   -  Success to indicate that all sub-operations were successfully
      completed

   -  Failure or Refused to indicate all sub-operations were
      unsuccessful

   -  Warning in all other cases. The Number of Completed Sub-Operations
      (0000,1021), Number of Warning Sub-Operations (0000,1023), Number
      of Failed Sub-Operations (0000,1022) can be used to obtain more
      detailed information.

-  The SCU may cancel the C-MOVE operation by issuing a C-MOVE-CANCEL
   request at any time during the processing of the C-MOVE request. A
   C-MOVE response with a status of Canceled shall indicate to the SCU
   that the retrieve was canceled. Optionally, the C-MOVE response with
   a status of Canceled shall indicate the number of Completed, Failed,
   and Warning C-STORE sub-operations. If present, the Remaining
   sub-operations count shall contain the number of C-STORE
   sub-operations that were not initiated due to the C-MOVE-CANCEL
   request.

.. note::

   For FRAME level C-MOVE operations, the application receiving the
   C-STORE sub-operations will receive a new SOP Instance with a
   different SOP Instance UID from the one included in the C-MOVE
   request. If it is required to link the received instance to the
   request, then it may be necessary to inspect the Frame Extraction
   Sequence of the instance received, to compare the original Instance
   UID and Requested Frame List to those in the request.

.. _sect_Y.4.1.2.2:

Extended Behavior of SCU
''''''''''''''''''''''''

The extended behavior of the SCU shall be as specified in `Extended
Behavior of SCU <#sect_C.4.2.2.2>`__, except that Relational-retrieve
shall not be supported.

.. _sect_Y.4.1.3:

C-MOVE SCP Behavior
^^^^^^^^^^^^^^^^^^^

.. _sect_Y.4.1.3.1:

Baseline Behavior of SCP
''''''''''''''''''''''''

An SCP conveys the following semantics with a C-MOVE response:

-  If the Retrieve Level (0000,0052) is IMAGE the SCP shall identify a
   set of Entities at the level of the transfer based upon the values in
   the Unique Keys in the Identifier of the C-MOVE request.

-  If the Retrieve Level (0000,0052) is FRAME, the SCP shall create a
   new Composite Instance according to the rules in section
   `Construction and Interpretation of Frame Range
   Keys <#sect_Y.3.2>`__. The newly created SOP Instance shall be
   treated in the same manner as the set of Entities identified above.

-  The SCP shall either re-use an established and compatible Association
   or establish a new Association for the C-STORE sub-operations

-  The SCP shall initiate C-STORE sub-operations over the Association
   for the identified or newly created SOP Instances.

-  A sub-operation is considered a Failure if the SCP is required to
   create new SOP Instance, but is unable to do so due to
   inconsistencies in the Frame Range Keys, or if the resulting SOP
   Instance would not be valid.

-  Optionally, the SCP may generate responses to the C-MOVE with status
   equal to Pending during the processing of the C-STORE sub-operations.
   These responses shall indicate the number of Remaining, Completed,
   Failure, and Warning C-STORE sub-operations.

-  When the number of Remaining sub-operations reaches zero, the SCP
   shall generate a final response with a status equal to Success,
   Warning or Failed. The status contained in the C-MOVE response shall
   contain:

   -  Success if all sub-operations were successfully completed

   -  Failure if all sub-operations were unsuccessful

   -  Warning in all other cases.

-  The SCP may receive a C-MOVE-CANCEL request at any time during the
   processing of the C-MOVE request. The SCP shall interrupt all C-STORE
   sub-operation processing and return a status of Canceled in the
   C-MOVE response. The C-MOVE response with a status of Canceled shall
   contain the number of Completed, Failed, and Warning C-STORE
   sub-operations. If present, the Remaining sub-operations count shall
   contain the number of C-STORE sub-operations that were not initiated
   due to the C-MOVE-CANCEL request.

-  If the SCP manages images in multiple alternate encodings (see
   `Alternate Representation Sequence <#sect_C.6.1.1.5.1>`__), only one
   of the alternate encodings of an image shall be used as the existing
   SOP Instance from which frames are to be extracted.

.. _sect_Y.4.1.3.2:

Extended Behavior of SCP
''''''''''''''''''''''''

The extended behavior of the SCP shall be as specified in `Extended
Behavior of SCP <#sect_C.4.2.3.2>`__, except that Relational-retrieve
shall not be supported.

.. _sect_Y.4.2:

C-GET Operation
~~~~~~~~~~~~~~~

SCUs of the Composite Instance Root Retrieve Service shall generate
retrievals using the C-GET operation as described in . The C-GET
operation allows an application entity to instruct another application
entity to transfer stored SOP Instances or new SOP Instances derived
from such stored SOP Instances to the initiating application entity
using the C-STORE operation. Support for the C-GET service shall be
agreed upon at Association establishment time by both the SCU and SCP of
the C-GET in order for a C-GET operation to occur over the Association.
The C-STORE Sub-operations shall be accomplished on the same Association
as the C-GET operation. Hence, the SCP of the Query/Retrieve Service
Class serves as the SCU of the Storage Service Class.

.. note::

   The Application Entity that receives the stored SOP Instances is
   always the originator of the C-GET operation.

A C-GET request may be performed to any level of the Composite Instance
Root Retrieve Information Model, and the expected SCP behavior depends
on the level selected.

.. _sect_Y.4.2.1:

C-GET Service Parameters
^^^^^^^^^^^^^^^^^^^^^^^^

.. _sect_Y.4.2.1.1:

SOP Class UID
'''''''''''''

The SOP Class UID identifies the Query/Retrieve Information Model
against which the C-GET is to be performed. Support for the SOP Class
UID is implied by the Abstract Syntax UID of the Presentation Context
used by this C-GET operation.

.. _sect_Y.4.2.1.2:

Priority
''''''''

The Priority Attribute defines the requested priority of the C-GET
operation and corresponding C-STORE sub-operations with respect to other
DIMSE operations being performed by the same SCP.

Processing of priority requests is not required of SCPs. Whether or not
an SCP supports priority processing, and the meaning of the different
priority levels shall be stated in the Conformance Statement of the SCP.
The same priority shall be used for all C-STORE sub-operations.

.. _sect_Y.4.2.1.3:

Identifier
''''''''''

The C-GET request shall contain an Identifier. The C-GET response shall
conditionally contain an Identifier as required in `Response Identifier
Structure <#sect_C.4.3.1.3.2>`__.

.. note::

   The Identifier is specified as U in the definition of the C-GET
   primitive in but is specialized for use with this service.

.. _sect_Y.4.2.1.3.1:

Request Identifier Structure
                            

An Identifier in a C-GET request shall contain:

-  the Query/Retrieve Level (0008,0052) that defines the level of the
   retrieval

-  SOP Instance UID(s) (0008,0018)

-  One of the Frame Range Keys if present in the Information Model for
   the level of the Retrieval

-  Conditionally, the Attribute Query/Retrieve View (0008,0053). This
   Attribute may be included if Enhanced Multi-Frame Image Conversion
   has accepted during Association Extended Negotiation. It shall not be
   included otherwise.

Specific Character Set (0008,0005) shall not be present.

The Keys at each level of the hierarchy and the values allowable for the
level of the retrieval shall be defined in the SOP Class definition for
the Query/Retrieve Information Model.

.. _sect_Y.4.2.1.4:

Status
''''''

The status code values that might be returned in a C-GET response shall
be as specified in `table_title <#table_Y.4-2>`__

.. table:: C-GET Response Status Values for Composite Instance Root
Retrieve

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
   | Failed: None   | AA00           | (0000,0902)  |                |
   | of the frames  |                |              |                |
   | requested were |                |              |                |
   | found in the   |                |              |                |
   | SOP Instance   |                |              |                |
   +----------------+----------------+--------------+----------------+
   | Failed: Unable | AA01           | (0000,0902)  |                |
   | to create new  |                |              |                |
   | object for     |                |              |                |
   | this SOP Class |                |              |                |
   +----------------+----------------+--------------+----------------+
   | Failed: Unable | AA02           | (0000,0902)  |                |
   | to extract     |                |              |                |
   | frames         |                |              |                |
   +----------------+----------------+--------------+----------------+
   | Failed:        | AA03           | (0000,0902)  |                |
   | Time-based     |                |              |                |
   | request        |                |              |                |
   | received for a |                |              |                |
   | non-time-based |                |              |                |
   | original SOP   |                |              |                |
   | Instance.      |                |              |                |
   +----------------+----------------+--------------+----------------+
   | Failed:        | AA04           | (0000,0901)  |                |
   | Invalid        |                |              |                |
   | Request        |                | (0000,0902)  |                |
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

.. _sect_Y.4.2.1.5:

Number of Remaining Sub-Operations
''''''''''''''''''''''''''''''''''

Inclusion of the Number of Remaining Sub-operations shall be as
specified in `Number of Remaining Sub-Operations <#sect_C.4.3.1.5>`__

.. _sect_Y.4.2.1.6:

Number of Completed Sub-Operations
''''''''''''''''''''''''''''''''''

Inclusion of the Number of Completed Sub-operations shall be as
specified in `Number of Completed Sub-Operations <#sect_C.4.3.1.6>`__

.. _sect_Y.4.2.1.7:

Number of Failed Sub-Operations
'''''''''''''''''''''''''''''''

Inclusion of the Number of Failed Sub-operations shall be as specified
in `Number of Failed Sub-Operations <#sect_C.4.3.1.7>`__

.. _sect_Y.4.2.1.8:

Number of Warning Sub-Operations
''''''''''''''''''''''''''''''''

Inclusion of the Number of Warning Sub-operations shall be as specified
in `Number of Warning Sub-Operations <#sect_C.4.3.1.8>`__.

.. _sect_Y.4.2.2:

C-GET SCU Behavior
^^^^^^^^^^^^^^^^^^

.. _sect_Y.4.2.2.1:

Baseline Behavior of SCU
''''''''''''''''''''''''

An SCU conveys the following semantics with a C-GET request:

-  If the Retrieve Level (0000,0052) is IMAGE, the SCU shall specify one
   SOP Instance UID or a list of SOP Instance UIDs.

-  If the Retrieve Level (0000,0052) is FRAME, the SCU shall specify the
   single SOP Instance UID of the item from which the new Composite SOP
   Instance should be extracted and the Requested Frame List. The
   Requested Frame List shall be constructed as a Frame List as defined
   in `Construction and Interpretation of Frame Range
   Keys <#sect_Y.3.2>`__.

-  The SCU shall have proposed sufficient presentation contexts at
   Association establishment time to accommodate expected C-STORE
   sub-operations that will occur over the same Association. The SCU of
   the Query/Retrieve Service Class shall serve as the SCP of the
   Storage Service Class.

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

.. _sect_Y.4.2.2.2:

Extended Behavior of SCU
''''''''''''''''''''''''

The extended behavior of the SCU shall be as specified in `Extended
Behavior of SCU <#sect_C.4.3.2.2>`__, except that Relational-retrieve
shall not be supported.

.. _sect_Y.4.2.3:

C-GET SCP Behavior
^^^^^^^^^^^^^^^^^^

.. _sect_Y.4.2.3.1:

Baseline Behavior of SCP
''''''''''''''''''''''''

An SCP conveys the following semantics with a C-GET response:

-  If the Retrieve Level (0000,0052) is IMAGE the SCP shall identify a
   set of Entities at the level of the transfer based upon the values in
   the Unique Keys in the Identifier of the C-GET request.

-  If the Retrieve Level (0000,0052) is FRAME, the SCP shall create a
   new Composite Instance according to the rules in section `New
   Instance Creation At the Frame Level <#sect_Y.3.3>`__. The newly
   created SOP Instance shall be treated in the same manner as the set
   of Entities identified above.

-  The SCP shall initiate C-STORE sub-operations for the identified or
   newly created SOP Instances. The SCP of the Query/Retrieve Service
   Class shall serve as an SCU of the Storage Service Class.

-  The SCP shall initiate C-STORE sub-operations over the same
   Association for all identified or newly created SOP Instances
   specified in the C-GET request.

-  A sub-operation is considered a Failure if the SCP is required to
   create new SOP Instance, but is unable to do so due to
   inconsistencies in the Frame Range Keys, or if the resulting SOP
   Instance would not be valid.

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

.. _sect_Y.4.2.3.2:

Extended Behavior of SCP
''''''''''''''''''''''''

The extended behavior of the SCP shall be as specified in `Extended
Behavior of SCP <#sect_C.4.3.3.2>`__, except that Relational-retrieve
shall not be supported.

.. _sect_Y.5:

Association Negotiation
-----------------------

Association establishment is the first phase of any instance of
communication between peer DICOM AEs. AEs supporting DICOM
Query/Retrieve SOP Classes utilize Association establishment negotiation
by defining the use of Application Association Information. See for an
overview of Association negotiation.

SOP Classes of the Composite Instance Root Retrieve Service, which
include retrieval services based on the C-MOVE and C-GET operations, use
the SCP/SCU Role Selection Sub-Item to identify the SOP Classes that may
be used for retrieval.

.. _sect_Y.5.1:

Association Negotiation for C-MOVE and C-GET SOP Classes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Rules are as specified in `Association Negotiation for C-GET SOP
Classes <#sect_C.5.3>`__, except that the extended negotiation sub-item,
if used, shall be used as defined in `SOP Class Extended
Negotiation <#sect_Y.5.1.1>`__.

.. note::

   1. Though converted images may be specified by their SOP Instance UID
      in the Request Identifier, which is always at or below the
      instance level, there remains a need for extended negotiation and
      specification of the Query/Retrieve View in order to assure that
      referential integrity is maintained within the returned SOP
      Instances (e.g., that a reference to a SOP Instance UID is to a
      converted image or not, as appropriate).

   2. Relational-retrieval is not applicable to these SOP Classes, hence
      the Extended Negotiation Sub-Item does not include the use of that
      byte.

.. _sect_Y.5.1.1:

SOP Class Extended Negotiation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The SOP Class Extended Negotiation allows, at Association establishment,
peer DICOM AEs to exchange application Association information defined
by specific SOP Classes. This is achieved by defining the
Service-class-application-information field. The
Service-class-application-information field is used to define support
for Enhanced Multi-Frame Image Conversion.

This negotiation is optional. If absent, the default condition shall be:

-  no Enhanced Multi-Frame Image Conversion support

The Association-requester, for each SOP Class, may use one SOP Class
Extended Negotiation Sub-Item. The SOP Class is identified by the
corresponding Abstract Syntax Name (as defined by ) followed by the
Service-class-application-information field. This field defines:

-  Enhanced Multi-Frame Image Conversion support by the
   Association-requester

The Association-acceptor, for each SOP Class Extended Negotiation
Sub-Item offered, either accepts the Association-requester proposal by
returning the same value (1) or turns down the proposal by returning the
value (0).

If the SOP Class Extended Negotiation Sub-Item is not returned by the
Association-acceptor then Enhanced Multi-Frame Image Conversion is not
supported (default condition).

If the SOP Class Extended Negotiation Sub-Items do not exist in the
A-ASSOCIATE indication they shall be omitted in the A-ASSOCIATE
response.

.. _sect_Y.5.1.1.1:

SOP Class Extended Negotiation Sub-Item Structure (A-ASSOCIATE-RQ)
''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''

The SOP Class Extended Negotiation Sub-Item consists of a sequence of
mandatory fields as defined by . `table_title <#table_Y.5.1-1>`__
defines the Service-class-application-information field for the C-MOVE
and C-GET operations.

.. table:: SOP Class Extended Negotiation Sub-Item
(Service-Class-Application-Information Field) - A-ASSOCIATE-RQ

   +------------+---------------------------+---------------------------+
   | Item Bytes | Field Name                | Description of Field      |
   +============+===========================+===========================+
   | 1          | Unused                    | Reserved - shall be 0     |
   +------------+---------------------------+---------------------------+
   | 2          | Enhanced Multi-Frame      | This byte field defines   |
   |            | Image Conversion          | whether or not the        |
   |            |                           | Attribute Query/Retrieve  |
   |            |                           | View (0008,0053) shall be |
   |            |                           | used to adjust the view   |
   |            |                           | returned in queries to    |
   |            |                           | consider conversion to or |
   |            |                           | from Enhanced Multi-Frame |
   |            |                           | Images. It shall be       |
   |            |                           | encoded as an unsigned    |
   |            |                           | binary integer and shall  |
   |            |                           | use one of the following  |
   |            |                           | values                    |
   |            |                           |                           |
   |            |                           | 0 - Query/Retrieve View   |
   |            |                           | not supported             |
   |            |                           |                           |
   |            |                           | 1 - Query/Retrieve View   |
   |            |                           | supported                 |
   +------------+---------------------------+---------------------------+

.. _sect_Y.5.1.1.2:

SOP Class Extended Negotiation Sub-Item Structure (A-ASSOCIATE-AC)
''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''

The SOP Class Extended Negotiation Sub-Item consists of a sequence of
mandatory fields as defined by . `table_title <#table_Y.5.1-2>`__
defines the Service-class-application-information field for the C-MOVE
and C-GET operations.

.. table:: SOP Class Extended Negotiation Sub-Item
(Service-Class-Application-Information Field) - A-ASSOCIATE-AC

   +------------+---------------------------+---------------------------+
   | Item Bytes | Field Name                | Description of Field      |
   +============+===========================+===========================+
   | 1          | Unused                    | Reserved - shall not be   |
   |            |                           | tested.                   |
   +------------+---------------------------+---------------------------+
   | 2          | Enhanced Multi-Frame      | This byte field defines   |
   |            | Image Conversion          | whether or not the        |
   |            |                           | Attribute Query/Retrieve  |
   |            |                           | View (0008,0053) shall be |
   |            |                           | used to adjust the view   |
   |            |                           | returned in queries to    |
   |            |                           | consider conversion to or |
   |            |                           | from Enhanced Multi-Frame |
   |            |                           | Images. It shall be       |
   |            |                           | encoded as an unsigned    |
   |            |                           | binary integer and shall  |
   |            |                           | use one of the following  |
   |            |                           | values                    |
   |            |                           |                           |
   |            |                           | 0 - Query/Retrieve View   |
   |            |                           | not supported             |
   |            |                           |                           |
   |            |                           | 1 - Query/Retrieve View   |
   |            |                           | supported                 |
   +------------+---------------------------+---------------------------+

.. _sect_Y.6:

SOP Class Definitions
---------------------

.. _sect_Y.6.1:

Composite Instance Root SOP Class Group
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In the Composite Instance Root Retrieve Only Information Model, the
information is arranged into two levels that correspond to one of the
two values in element (0008,0052) shown in
`table_title <#table_Y.6.1-1>`__.

.. table:: Retrieve Level Values for Composite Instance Root Retrieve

   ================== ====================
   Retrieve Level     Value in (0008,0052)
   ================== ====================
   Composite Instance IMAGE
   Frame              FRAME
   ================== ====================

.. note::

   The use of the word "IMAGE" rather than "Composite Instance" is
   historical to allow backward compatibility with previous editions of
   the Standard. It should not be taken to mean that Composite Instances
   of other than image type are not included at the level indicated by
   the value IMAGE.

.. _sect_Y.6.1.1:

Composite Instance Root Retrieve Only Information Model
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. _sect_Y.6.1.1.1:

E/R Model
'''''''''

The Composite Instance Root Retrieve Only Information Model may be
represented by the entity relationship diagram shown in
`figure_title <#figure_Y.6-1>`__

.. _sect_Y.6.1.1.2:

Composite Instance Level
''''''''''''''''''''''''

`table_title <#table_Y.6-1>`__ defines the keys at the Composite
Instance level of the Composite Instance Root Query/Retrieve Information
model.

.. table:: Composite Instance Level Keys for the Composite Instance Root
Retrieve Information Model

   ================ =========== =================
   Attribute Name   Tag         Matching Key Type
   ================ =========== =================
   SOP Instance UID (0008,0018) U
   ================ =========== =================

.. _sect_Y.6.1.1.3:

Frame Level
'''''''''''

`table_title <#table_Y.6-2>`__ defines the keys at the Frame level of
the Composite Instance Root Query/Retrieve Information Model. One and
only one of the frame level keys listed in
`table_title <#table_Y.6-2>`__ shall be present in a FRAME level request

.. table:: Frame Level Keys for the Composite Instance Root Retrieve
Information Model

   +-----------------------+-------------+--------------------------+
   | Attribute Name        | Tag         | Condition                |
   +=======================+=============+==========================+
   | Simple Frame List     | (0008,1161) | Required if Calculated   |
   |                       |             | Frame List and Time      |
   |                       |             | Range are not present    |
   +-----------------------+-------------+--------------------------+
   | Calculated Frame List | (0008,1162) | Required if Simple Frame |
   |                       |             | List and Approximate     |
   |                       |             | Frame Range are not      |
   |                       |             | present                  |
   +-----------------------+-------------+--------------------------+
   | Time Range            | (0008,1163) | Required if Simple Frame |
   |                       |             | List and Calculated      |
   |                       |             | Frame List are not       |
   |                       |             | present                  |
   +-----------------------+-------------+--------------------------+

.. _sect_Y.6.1.1.4:

Scope of the C-MOVE or C-GET Commands and Sub-Operations
''''''''''''''''''''''''''''''''''''''''''''''''''''''''

A C-MOVE or C-GET request may be performed to any level of the
Query/Retrieve Model. A C-MOVE or C-GET where the Query/Retrieve level
is the:

IMAGE level indicates that selected individual Composite Instances shall
be transferred

FRAME level indicates that a single new Composite Instance shall be
created and transferred

.. note::

   More than one entity may be retrieved if the Query/Retrieve Level is
   IMAGE using List of UID matching, but if the Query/Retrieve Level is
   FRAME then only a single entity may be retrieved.

.. _sect_Y.6.1.2:

Conformance Requirements
^^^^^^^^^^^^^^^^^^^^^^^^

An implementation may conform to one of the Composite Instance Root
Retrieve SOP Classes as an SCU, SCP or both. The Conformance Statement
shall be in the format defined in .

.. _sect_Y.6.1.2.1:

SCU Conformance
'''''''''''''''

.. _sect_Y.6.1.2.1.1:

C-MOVE SCU Conformance
                      

An implementation that conforms to one of the Composite Instance Root
Retrieve SOP Classes as an SCU shall support transfers against the
Retrieve Information Model described in `Composite Instance Root
Retrieve Only Information Model <#sect_Y.6.1.1>`__ using the C-MOVE SCU
Behavior described in `C-MOVE SCU Behavior <#sect_Y.4.1.2>`__. An
implementation that conforms to one of the SOP Classes of the Composite
Instance Root SOP Class Group as an SCU, and that generates retrievals
using the C-MOVE operation, shall state in its Conformance Statement the
Storage Service Class SOP Classes under which it shall support the
C-STORE sub-operations generated by the C- MOVE.

.. _sect_Y.6.1.2.1.2:

C-GET SCU Conformance
                     

An implementation that conforms to one of the Composite Instance Root
Retrieve SOP Classes as an SCU shall support retrievals against the
Retrieve Information Model described in `Composite Instance Root
Retrieve Only Information Model <#sect_Y.6.1.1>`__ using the C-GET SCU
Behavior described in `C-GET SCU Behavior <#sect_Y.4.2.2>`__. An
implementation that conforms to one of the SOP Classes of the Composite
Instance Root SOP Class Group as an SCU, which generates retrievals
using the C-GET operation shall state in its Conformance Statement the
Storage Service Class SOP Classes under which it shall support the
C-STORE sub-operations generated by the C-GET.

.. _sect_Y.6.1.2.2:

SCP Conformance
'''''''''''''''

An implementation that conforms to one of the Composite Instance Root
Retrieve SOP Classes as an SCP for C-GET operations shall:1) support
both levels of the Composite Instance Root Retrieve Only Information
Model

2) support all three Frame Level keys

3) describe in its conformance statement the transformations it applies
to a multi-frame Composite Instance when creating a new Composite
Instance as defined in `New Instance Creation At the Frame
Level <#sect_Y.3.3>`__.

.. _sect_Y.6.1.2.2.1:

C-MOVE SCP Conformance
                      

An implementation that conforms to one of the Composite Instance Root
Retrieve SOP Classes as an SCP shall support retrievals against both
levels of the Retrieve Information Model described in `Composite
Instance Root Retrieve Only Information Model <#sect_Y.6.1.1>`__ using
the C-MOVE SCP Behavior described in `C-MOVE SCP
Behavior <#sect_Y.4.1.3>`__. An implementation that conforms to one of
the SOP Classes of the Composite Instance Root SOP Class Group as an
SCP, which satisfies retrievals using the C- MOVE operation shall state
in its Conformance Statement the Storage Service Class SOP Classes under
which it shall support the C-STORE sub-operations generated by the C-
MOVE.

.. _sect_Y.6.1.2.2.2:

C-GET SCP Conformance
                     

An implementation that conforms to one of the Composite Instance Root
Retrieve SOP Classes as an SCP shall support retrievals against both
levels of the Retrieve Information Model described in `Composite
Instance Root Retrieve Only Information Model <#sect_Y.6.1.1>`__ using
the C-GET SCP Behavior described in `C-GET SCP
Behavior <#sect_Y.4.2.3>`__. An implementation that conforms to one of
the SOP Classes of the Composite Instance Root SOP Class Group as an
SCP, and that satisfies retrievals using the C-GET operation, shall
state in its Conformance Statement the Storage Service Class SOP Classes
under which it shall support the C-STORE sub-operations generated by the
C-GET.

.. _sect_Y.6.1.3:

SOP Classes
^^^^^^^^^^^

The SOP Classes in the Composite Instance Root SOP Class Group of the
Query/Retrieve Service Class identify the Composite Instance Root
Retrieve Only Information Model, and the DIMSE-C operations supported.
The Standard SOP Classes are listed in
`table_title <#table_Y.6.1.3-1>`__.

.. table:: SOP Classes for Composite Instance Root Retrieve

   ======================================= ===========================
   SOP Class Name                          SOP Class UID
   ======================================= ===========================
   Composite Instance Root Retrieve - MOVE 1.2.840.10008.5.1.4.1.2.4.2
   Composite Instance Root Retrieve - GET  1.2.840.10008.5.1.4.1.2.4.3
   ======================================= ===========================

