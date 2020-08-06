.. _chapter_K:

Basic Worklist Management Service (Normative)
=============================================

.. _sect_K.1:

Overview
--------

.. _sect_K.1.1:

Scope
~~~~~

The Basic Worklist Management Service Class defines an application-level
class-of-service that facilitates the access to worklists.

A worklist is the structure to present information related to a
particular set of tasks. It specifies particular details for each task.
The information supports the selection of the task to be performed
first, and supports the performance of that task.

.. note::

   One example is the worklist used to present information about
   scheduled imaging procedures at an imaging modality and to the
   operator of that modality. Another example is the worklist presented
   at a radiological reporting station to indicate which studies have
   been performed and are waiting to be reported.

This annex defines a service for communicating such worklists. The
following are characteristics for this Service Class:

-  The worklist has to be queried by the Application Entity (AE)
   associated with the application on which, or by which, the tasks
   included in the worklist have to be performed. In this query, a
   number of search keys can be used, defined for each particular
   worklist SOP Class.

-  The worklist consists of worklist items, each item is related to one
   task. A worklist item contains Attributes from different objects
   related to the task.

.. note::

   1. This Service Class is not intended to provide a comprehensive
      generalized database query mechanism such as SQL. Instead, the
      Basic Worklist Management Service Class is focused towards basic
      queries using a small set of common Key Attributes used as
      Matching Keys or Return Attributes. Basic Worklist Information
      Models are not hierarchical.

   2. Basic Worklist Information Models always consist of one query
      level, which may consist of one or more entities. There is no
      distinction between hierarchical and relational use of C-Find in
      the Basic Worklist Management Service Class.

.. _sect_K.1.2:

Conventions
~~~~~~~~~~~

Key Attributes serve two purposes, they may be used as: Matching Key
Attributes and Return Key Attributes. Matching Key Attributes may be
used for matching (criteria to be used in the C-FIND request to
determine whether an entity matches the query). Return Key Attributes
may be used to specify desired return Attributes (what elements in
addition to the Matching Key Attributes have to be returned in the
C-FIND response).

.. note::

   Matching Keys are typically used in an SQL 'where' clause. Return
   Keys are typically used in an SQL 'select' clause to convey the
   Attribute Values.

Matching Key Attributes may be of Type "required" (R) or "optional" (O).
Return Key Attributes may be of Type 1, 1C, 2, 2C, 3 as defined in .

.. _sect_K.1.3:

Worklist Information Model
~~~~~~~~~~~~~~~~~~~~~~~~~~

In order to serve as a Service Class Provider (SCP) of the Basic
Worklist Service Class, a DICOM Application Entity (AE) possesses
information about the Attributes of a number of managed worklist
entries. This information is organized into Worklist Information Models.

Worklists are implemented against well defined Information Models. A
specific SOP Class of the Basic Worklist Service Class consists of an
informative Overview, an Information Model Definition and a DIMSE-C
Service Group. In this Service Class, the Information Model plays a role
similar to an Information Object Definition (IOD) of most other DICOM
Service Classes.

.. _sect_K.1.4:

Service Definition
~~~~~~~~~~~~~~~~~~

Two peer DICOM AEs implement a SOP Class of the Basic Worklist Service
Class with one serving in the SCU role and one serving in the SCP role.
SOP Classes of the Basic Worklist Service Class are implemented using
the DIMSE-C C-FIND service as defined in .

Both a baseline and extended behavior are defined for the DIMSE-C
C-FIND. Baseline behavior specifies a minimum level of conformance for
all implementations to facilitate interoperability. Extended behavior
enhances the baseline behavior to provide additional features that may
be negotiated independently at Association establishment time.

The following description of the DIMSE-C C-FIND service provides a brief
overview of the SCU/SCP semantics.

A C-FIND service conveys the following semantics:

-  The SCU requests that the SCP perform a match for the Matching Keys
   and return values for the Return Keys that have been specified in the
   Identifier of the request, against the information that the SCP
   possesses, to the objects specified in the SOP Class.

   .. note::

      In this Annex, the term "Identifier" refers to the Identifier
      service parameter of the C-FIND service as defined in .

-  The SCP generates a C-FIND response for each match with an Identifier
   containing the values of all Matching Key Attributes and all known
   Return Key Attributes requested. Each response contains one worklist
   item. All such responses will contain a status of Pending. A status
   of Pending indicates that the process of matching is not complete.

-  When the process of matching is complete a C-FIND response is sent
   with a status of Success and no Identifier.

-  A Refused or Failed response to a C-FIND request indicates that the
   SCP is unable to process the request.

-  The SCU may cancel the C-FIND service by issuing a C-CANCEL-FIND
   request at any time during the processing of the C-FIND service. The
   SCP will interrupt all matching and return a status of Canceled.

   .. note::

      The SCU needs to be prepared to receive C-FIND responses sent by
      the SCP until the SCP finally processed the C-CANCEL-FIND request.

.. _sect_K.2:

Worklist Information Model Definition
-------------------------------------

The Worklist Information Model is identified by the SOP Class negotiated
at Association establishment time. The SOP Class is composed of both an
Information Model and a DIMSE-C Service Group.

Information Model Definitions for Standard SOP Classes of the Worklist
Service Class are defined in this Annex. A Worklist Information Model
Definition contains:

-  an Entity-Relationship Model Definition

-  a Key Attributes Definition;

.. _sect_K.2.1:

Entity-Relationship Model Definition
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Basic Worklist Information Models consist of a single level, that
includes all Matching Key Attributes and all Return Key Attributes,
which may be sent from the SCU to the SCP in the request and whose
values are expected to be returned from the SCP to the SCU in each of
the responses (or worklist items). The Matching Key Attribute Values in
the request specify the worklist items that are to be returned in the
responses. All Key Attributes (the Matching Key Attributes and the
Return Key Attributes) in the request determine which Attribute Values
are returned in the responses for that worklist.

A Worklist Item has a one-to-one relationship with the real-world object
defining the root for the Basic Worklist Information Model. In addition
the worklist item is related to a number of other objects from the
real-world model. Each of these real-world objects is represented by a
hierarchy of entities organized in an (internal) Entity-Relationship
Model.

.. _sect_K.2.2:

Attributes Definition
~~~~~~~~~~~~~~~~~~~~~

Attributes are defined for each entity in the internal
Entity-Relationship Model. An Identifier in a C-FIND request shall
contain values to be matched against the Attributes of the Entities in a
Worklist Information Model. For any worklist request, the set of
entities for which Attributes are returned, shall be determined by the
set of Matching and Return Key Attributes specified in the Identifier.

.. _sect_K.2.2.1:

Attribute Types
^^^^^^^^^^^^^^^

All Attributes of entities in a Worklist Information Model shall be
specified both as a Matching Key Attribute (either required or optional)
and as a Return Key Attribute.

.. _sect_K.2.2.1.1:

Matching Key Attributes
'''''''''''''''''''''''

The Matching Key Attributes are Keys, which select worklist items to be
included in a requested Worklist.

.. _sect_K.2.2.1.1.1:

Required Matching Key Attributes
                                

A Basic Worklist Management SCP shall support matching based on values
of all Required Matching Key Attributes of the C-FIND request. Multiple
entities may match a given value for a Required Key.

If an SCP manages an entity with an unknown Attribute Value (i.e., zero
length), the unknown value shall fail to match any Matching Key value.

.. note::

   1. Even though there is no means to perform matching on such
      entities, they may be queried as a Return Key Attribute using a
      C-FIND request with a zero length value (Universal Match) or by a
      single wild card (Wild Card Match).

   2. An SCU may choose to supply any subset of Required Matching Key
      Attributes.

.. _sect_K.2.2.1.1.2:

Optional Matching Key Attributes
                                

In the Worklist Information Model, a set of Attributes may be defined as
Optional Matching Key Attributes. Optional Matching Key Attributes
contained in the Identifier of a C-FIND request may induce two different
types of behavior depending on support for matching by the SCP. If the
SCP

-  does not support matching on the Optional Matching Key Attribute,
   then the Optional Matching Key Attribute shall be ignored for
   matching but shall be processed in the same manner as a Return Key
   Attribute.

-  supports matching of the Optional Matching Key Attribute, then the
   Optional Matching Key Attribute shall be processed in the same manner
   as a Required Matching Key.

.. note::

   1. The Conformance Statement of the SCP lists the Optional Matching
      Key Attributes that are supported for matching.

   2. An SCU can not expect the SCP to support a match on an Optional
      Matching Key.

.. _sect_K.2.2.1.2:

Return Key Attributes
'''''''''''''''''''''

The values of Return Key Attributes to be retrieved with the Worklist
are specified with zero-length (Universal Matching) in the C-FIND
request. SCPs shall support Return Key Attributes defined by a Worklist
Information Model according to the Data Element Type (1, 1C, 2, 2C, 3)
as defined in .

Every Matching Key Attribute shall also be considered as a Return Key
Attribute. Therefore the C-FIND response shall contain in addition to
the values of the requested Return Key Attributes the values of the
requested Matching Key Attributes.

.. note::

   1. The Conformance Statement of the SCP lists the Return Key
      Attributes of Type 3, which are supported.

   2. An SCU may choose to supply any subset of Return Key Attributes.

   3. An SCU can not expect to receive any Type 3 Return Key Attributes.

   4. Return Key Attributes with VR of SQ may be specified either with
      zero-length or with the zero-length item in the sequence.

.. _sect_K.2.2.2:

Attribute Matching
^^^^^^^^^^^^^^^^^^

The following types of matching, which are defined by the Query/Retrieve
Service Class in `Query/Retrieve Service Class
(Normative) <#chapter_C>`__ may be performed on Matching Key Attributes
in the Basic Worklist Service Class. Different Matching Key Attributes
may be subject for different matching types. The Worklist Information
Model defines the type of matching for each Required Matching Key
Attribute. The Conformance Statement of the SCP shall define the type of
matching for each Optional Matching Key Attribute. The types of matching
are:

-  Single Value Matching

-  List of UID Matching

-  Wild Card Matching

-  Range Matching

-  Sequence Matching

The following type of matching, which is defined by the Query/Retrieve
Service Class in `Query/Retrieve Service Class
(Normative) <#chapter_C>`__ of this Part shall be performed on Return
Key Attributes in the Basic Worklist Service Class.

-  Universal Matching

See `Attribute Matching <#sect_C.2.2.2>`__ and subsections for specific
rules governing of Matching Key Attribute encoding for and performing of
different types of matching.

The Specific Character Set (0008,0005) Attribute and/or the Timezone
Offset From UTC (0008,0201) Attribute may be present in the Identifier
but are never matched, i.e., they are not considered Matching Key
Attributes. See `Attribute Matching <#sect_C.2.2.2>`__ for details.

Single value matching of Attributes with a VR of PN may be affected by
extended negotiation of fuzzy semantic matching of person names.

.. _sect_K.2.2.3:

Matching Multiple Values
^^^^^^^^^^^^^^^^^^^^^^^^

When matching an Attribute that has a value multiplicity of greater than
one, if any of the values match, then all values shall be returned.

.. _sect_K.3:

Worklist Information Model
--------------------------

Each Worklist Information Model is associated with one SOP Class. The
following Worklist Information Model is defined:

-  Modality Worklist Information Model

.. _sect_K.4:

DIMSE-C Service Group
---------------------

One DIMSE-C Service is used in the construction of SOP Classes of the
Basic Worklist Management Service Class. The following DIMSE-C operation
is used.

-  C-FIND

.. _sect_K.4.1:

C-FIND Operation
~~~~~~~~~~~~~~~~

SCPs of some SOP Classes of the Basic Worklist Management Service Class
are capable of processing queries using the C-FIND operation as
described in . The C-FIND operation is the mechanism by which queries
are performed. Matches against the keys present in the Identifier are
returned in C-FIND responses.

.. _sect_K.4.1.1:

C-FIND Service Parameters
^^^^^^^^^^^^^^^^^^^^^^^^^

.. _sect_K.4.1.1.1:

SOP Class UID
'''''''''''''

The SOP Class UID identifies the Worklist Information Model against
which the C-FIND is to be performed. Support for the SOP Class UID is
implied by the Abstract Syntax UID of the Presentation Context used by
this C-FIND operation.

.. _sect_K.4.1.1.2:

Priority
''''''''

The Priority Attribute defines the requested priority of the C-FIND
operation with respect to other DIMSE operations being performed by the
same SCP.

Processing of priority requests is not required of SCPs. Whether or not
an SCP supports priority processing and the meaning of the different
priority levels shall be stated in the Conformance Statement of the SCP.

.. _sect_K.4.1.1.3:

Identifier
''''''''''

Both the C-FIND request and response contain an Identifier encoded as a
Data Set (see ).

.. _sect_K.4.1.1.3.1:

Request Identifier Structure
                            

An Identifier in a C-FIND request shall contain

-  Key Attributes values to be matched against the values of Attributes
   specified in that SOP Class.

-  Conditionally, the Attribute Specific Character Set (0008,0005). This
   Attribute shall be included if expanded or replacement character sets
   may be used in any of the Attributes in the Request Identifier. It
   shall not be included otherwise.

   .. note::

      This means that Specific Character Set (0008,0005) is included if
      the SCU supports expanded or replacement character sets in the
      context of this service. It will not be included if expanded or
      replacement character sets are not supported by the SCU.

-  Conditionally, the Attribute Timezone Offset From UTC (0008,0201).
   This Attribute shall be included if Key Attributes of time are to be
   interpreted explicitly in the designated local time zone. It shall
   not be present otherwise, i.e., it shall not be sent with a
   zero-length value.

The Key Attributes and values allowable for the query shall be defined
in the SOP Class definition for the corresponding Worklist Information
Model.

.. _sect_K.4.1.1.3.2:

Response Identifier Structure
                             

The C-FIND response shall not contain Attributes that were not in the
request or specified in this section.

An Identifier in a C-FIND response shall contain:

-  Key Attributes with values corresponding to Key Attributes contained
   in the Identifier of the request (Key Attributes as defined in
   `Attribute Types <#sect_K.2.2.1>`__.)

-  Conditionally, the Attribute Specific Character Set (0008,0005). This
   Attribute shall be included if expanded or replacement character sets
   may be used in any of the Attributes in the Response Identifier. It
   shall not be included otherwise. The C-FIND SCP is not required to
   return responses in the Specific Character Set requested by the SCU
   if that character set is not supported by the SCP. The SCP may return
   responses with a different Specific Character Set.

   .. note::

      This means that Specific Character Set (0008,0005) is included if
      the SCP supports expanded or replacement character sets in the
      context of this service. It will not be included if expanded or
      replacement character sets are not supported by the SCP.

-  Conditionally, the Attribute Timezone Offset From UTC (0008,0201).
   This Attribute shall be included if any Attributes of time in the
   Response Identifier are to be interpreted explicitly in the
   designated local time zone. It shall not be present otherwise, i.e.,
   it shall not be sent with a zero-length value.

-  Conditionally, the Attribute HL7 Structured Document Reference
   Sequence (0040,A390) and its subsidiary Sequence Items. This
   Attribute shall be included if HL7 Structured Documents are
   referenced within the Identifier, e.g., in the Pertinent Documents
   Sequence (0038,0100).

.. _sect_K.4.1.1.4:

Status
''''''

`table_title <#table_K.4-1>`__ defines the status code values that might
be returned in a C-FIND response. General status code values and fields
related to status code values are defined for C-FIND DIMSE Service in .

.. table:: C-FIND Response Status Values

   +----------------+----------------+--------------+----------------+
   | Service Status | Further        | Status Codes | Related Fields |
   |                | Meaning        |              |                |
   +================+================+==============+================+
   | Failure        | Refused: Out   | A700         | (0000,0902)    |
   |                | of resources   |              |                |
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
   | Cancel         | Matching       | FE00         | None           |
   |                | terminated due |              |                |
   |                | to Cancel      |              |                |
   |                | request        |              |                |
   +----------------+----------------+--------------+----------------+
   | Success        | Matching is    | 0000         | None           |
   |                | complete - No  |              |                |
   |                | final          |              |                |
   |                | Identifier is  |              |                |
   |                | supplied.      |              |                |
   +----------------+----------------+--------------+----------------+
   | Pending        | Matches are    | FF00         | Identifier     |
   |                | continuing -   |              |                |
   |                | Current Match  |              |                |
   |                | is supplied    |              |                |
   |                | and any        |              |                |
   |                | Optional Keys  |              |                |
   |                | were supported |              |                |
   |                | in the same    |              |                |
   |                | manner as      |              |                |
   |                | Required Keys. |              |                |
   +----------------+----------------+--------------+----------------+
   | Matches are    | FF01           | Identifier   |                |
   | continuing -   |                |              |                |
   | Warning that   |                |              |                |
   | one or more    |                |              |                |
   | Optional Keys  |                |              |                |
   | were not       |                |              |                |
   | supported for  |                |              |                |
   | existence for  |                |              |                |
   | this           |                |              |                |
   | Identifier.    |                |              |                |
   +----------------+----------------+--------------+----------------+

.. note::

   Status Codes are returned in DIMSE response messages (see ). The code
   values stated in column "Status Codes" are returned in Status Command
   Element (0000,0900).

Some Failure Status Codes are implementation specific.

An SCP implementation shall assign specific failure status codes by
replacing each 'x' symbol with a hexadecimal digit in the range from 0
to F. An SCP implementation wishing to differentiate between causes of
“Failed: Unable to process” Failure Meaning shall assign those causes
specific Status Code Values within valid range specified in
`table_title <#table_K.4-1>`__.

An SCU implementation shall recognize any Failure Status Code within the
value range specified in `table_title <#table_K.4-1>`__ as an indicator
of the Failure Meaning stated in the table. There is no requirement for
an SCU implementation to differentiate between specific Status Codes
within the valid range.

.. _sect_K.4.1.2:

C-FIND SCU Behavior
^^^^^^^^^^^^^^^^^^^

All C-FIND SCUs shall be capable of generating query requests that meet
the requirements of the "Worklist" Search Method (see `"Worklist" Search
Method <#sect_K.4.1.3.1>`__).

Required Keys, and Optional Keys associated with the Worklist may be
contained in the Identifier.

An SCU conveys the following semantics using the C-FIND requests and
responses:

-  The SCU requests that the SCP perform a match of all keys specified
   in the Identifier of the request against the information it possesses
   of the Worklist specified in the request.

-  The SCU shall interpret Pending responses to convey the Attributes of
   a match of an Entity.

-  The SCU shall interpret a response with a status equal to Success,
   Failed, Refused or Cancel to convey the end of Pending responses.

-  The SCU shall interpret a Refused or Failed response to a C-FIND
   request as an indication that the SCP is unable to process the
   request.

-  The SCU may cancel the C-FIND service by issuing a C-FIND-CANCEL
   request at any time during the processing of the C-FIND. The SCU
   shall recognize a status of Cancel to indicate that the C-FIND-CANCEL
   was successful.

.. _sect_K.4.1.3:

C-FIND SCP Behavior
^^^^^^^^^^^^^^^^^^^

All C-FIND SCPs shall be capable of processing queries that meet the
requirements of the "Worklist" Search (see `"Worklist" Search
Method <#sect_K.4.1.3.1>`__).

An SCP conveys the following semantics using the C-FIND requests and
responses:

-  The SCP is requested to perform a match of all the keys specified in
   the Identifier of the request, against the information it possesses.
   Attribute matching is performed using the key values specified in the
   Identifier of the C-FIND request as defined in `Worklist Information
   Model Definition <#sect_K.2>`__.

-  The SCP generates a C-FIND response for each match using the
   "Worklist" Search method. All such responses shall contain an
   Identifier whose Attributes contain values from a single match. All
   such responses shall contain a status of Pending.

-  When all matches have been sent, the SCP generates a C-FIND response
   that contains a status of Success. A status of Success shall indicate
   that a response has been sent for each match known to the SCP.

   .. note::

      1. No ID is contained in a response with a status of Success. For
         a complete definition, see .

      2. When there are no matches, then no responses with a status of
         Pending are sent, only a single response with a status of
         Success.

-  The SCP shall generate a response with a status of Refused or Failed
   if it is unable to process the request. A Refused or Failed response
   shall contain no Identifier.

-  If the SCP receives C-FIND-CANCEL indication before it has completed
   the processing of the matches it shall interrupt the matching process
   and return a status of Cancel.

.. _sect_K.4.1.3.1:

"Worklist" Search Method
''''''''''''''''''''''''

The following procedure is used to generate matches.

The key match strings contained in the Identifier of the C-FIND request
are matched against the values of the Key Attributes for each worklist
entity. For each entity for which the Attributes match all of the
specified match strings, construct an Identifier. This Identifier shall
contain all of the values of the Attributes for this entity that match
those in the C-FIND request. Return a response for each such Identifier.
If there are no matching keys, then there are no matches, return a
response with a status equal to Success and with no Identifier.

.. _sect_K.5:

Association Negotiation
-----------------------

Association establishment is the first phase of any instance of
communication between peer DICOM AEs. The Association negotiation
procedure specified in shall be used to negotiate the supported SOP
Classes or Meta SOP Classes.

Support for the SCP/SCU Role Selection Negotiation is optional. The SOP
Class Extended Negotiation is optional.

.. _sect_K.5.1:

SOP Class Extended Negotiation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The SOP Class Extended Negotiation allows, at Association establishment,
peer DICOM AEs to exchange application Association information defined
by specific SOP Classes. This is achieved by defining the
Service-class-application-information field. The
Service-class-application-information field is used to define support
for fuzzy semantic matching of person names.

This negotiation is optional. If absent, the default conditions shall
be:

-  literal matching of person names with case sensitivity unspecified

-  timezone query adjustment unspecified

The Association-requester, for each SOP Class, may use one SOP Class
Extended Negotiation Sub-Item. The SOP Class is identified by the
corresponding Abstract Syntax Name (as defined by ) followed by the
Service-class-application-information field. This field defines three or
more sub-fields:

-  reserved; shall always be 1

-  reserved; shall always be 1

-  literal or fuzzy semantic matching of person names by the
   Association-requester

-  timezone query adjustment by the Association-requester

The meaning of fuzzy semantic person name matching and of timezone query
adjustment is as defined in `Attribute Matching <#sect_K.2.2.2>`__ and
`Single Value Matching <#sect_C.2.2.2.1>`__.

The Association-acceptor shall return a three byte field (three
sub-fields) if offered a three byte field (three sub-fields) by the
Association-requester. The Association-acceptor may return more than
three bytes if offered more than three bytes by the
Association-requester. A three byte response to a more than three byte
request means that the missing sub-field shall be treated as 0 values.

The Association-acceptor, for each sub-field of the SOP Class Extended
Negotiation Sub-Item offered, either accepts the Association-requester
proposal by returning the same value (1) or turns down the proposal by
returning the value (0)..

If the SOP Class Extended Negotiation Sub-Item is not returned by the
Association-acceptor then fuzzy semantic matching of person names is not
supported and timezone query adjustment is unspecified over the
Association (default condition).

If the SOP Class Extended Negotiation Sub-Items do not exist in the
A-ASSOCIATE indication they shall be omitted in the A-ASSOCIATE
response.

.. _sect_K.5.1.1:

SOP Class Extended Negotiation Sub-Item Structure (A-ASSOCIATE-RQ)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The SOP Class Extended Negotiation Sub-Item consists of a sequence of
mandatory fields as defined by . This field shall be three or four bytes
in length.

.. table:: SOP Class Extended Negotiation Sub-Item
(Service-Class-Application-Information Field) - A-ASSOCIATE-RQ

   +------------+---------------------------+---------------------------+
   | Item Bytes | Field Name                | Description of Field      |
   +============+===========================+===========================+
   | 1          | reserved                  | This byte field shall     |
   |            |                           | always be 1               |
   +------------+---------------------------+---------------------------+
   | 2          | reserved                  | This byte field shall     |
   |            |                           | always be 1               |
   +------------+---------------------------+---------------------------+
   | 3          | Fuzzy semantic matching   | This byte field defines   |
   |            | of person names           | whether or not fuzzy      |
   |            |                           | semantic person name      |
   |            |                           | Attribute is requested by |
   |            |                           | the                       |
   |            |                           | Association-requester. It |
   |            |                           | shall be encoded as an    |
   |            |                           | unsigned binary integer   |
   |            |                           | and shall use one of the  |
   |            |                           | following values          |
   |            |                           |                           |
   |            |                           | 0 - fuzzy semantic        |
   |            |                           | matching not requested    |
   |            |                           |                           |
   |            |                           | 1 - fuzzy semantic        |
   |            |                           | matching requested        |
   +------------+---------------------------+---------------------------+
   | 4          | Timezone query adjustment | This byte field defines   |
   |            |                           | whether or not the        |
   |            |                           | Attribute Timezone Offset |
   |            |                           | From UTC (0008,0201)      |
   |            |                           | shall be used to adjust   |
   |            |                           | the query meaning for     |
   |            |                           | time and datetime fields  |
   |            |                           | in queries.               |
   |            |                           |                           |
   |            |                           | 0 - Timezone query        |
   |            |                           | adjustment not requested  |
   |            |                           |                           |
   |            |                           | 1 - Timezone query        |
   |            |                           | adjustment requested      |
   +------------+---------------------------+---------------------------+

.. note::

   This Sub-Item is identical to Extended Negotiation Sub-Items as used
   by the Query/Retrieve SOP Classes. However, relational queries (Byte
   1) are not relevant since the worklist information models are single
   level, and date-time matching (Byte 2) is already required by the
   worklist information models and Enhanced Multi-Frame Image Conversion
   support is not applicable (Byte 5).

.. _sect_K.5.1.2:

SOP Class Extended Negotiation Sub-Item Structure (A-ASSOCIATE-AC)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The SOP Class Extended Negotiation Sub-Item is made of a sequence of
mandatory fields as defined by . This field shall be three or four bytes
in length.

.. table:: SOP Class Extended Negotiation Sub-Item
(Service-Class-Application-Information Field) - A-ASSOCIATE-AC

   +------------+---------------------------+---------------------------+
   | Item Bytes | Field Name                | Description of Field      |
   +============+===========================+===========================+
   | 1          | reserved                  | This byte field shall     |
   |            |                           | always be 1               |
   +------------+---------------------------+---------------------------+
   | 2          | reserved                  | This byte field shall     |
   |            |                           | always be 1               |
   +------------+---------------------------+---------------------------+
   | 3          | Fuzzy semantic matching   | This byte field defines   |
   |            | of person names           | whether or not fuzzy      |
   |            |                           | semantic person name      |
   |            |                           | Attribute matching will   |
   |            |                           | be performed by the       |
   |            |                           | Association-acceptor. It  |
   |            |                           | shall be encoded as an    |
   |            |                           | unsigned binary integer   |
   |            |                           | and shall use one of the  |
   |            |                           | following values          |
   |            |                           |                           |
   |            |                           | 0 - fuzzy semantic        |
   |            |                           | matching not performed    |
   |            |                           |                           |
   |            |                           | 1 - fuzzy semantic        |
   |            |                           | matching performed        |
   +------------+---------------------------+---------------------------+
   | 4          | Timezone query adjustment | This byte field defines   |
   |            |                           | whether or not the        |
   |            |                           | Attribute Timezone Offset |
   |            |                           | From UTC (0008,0201)      |
   |            |                           | shall be used to adjust   |
   |            |                           | the query meaning for     |
   |            |                           | time and datetime fields  |
   |            |                           | in queries.               |
   |            |                           |                           |
   |            |                           | 0 - Timezone adjustment   |
   |            |                           | of queries not performed  |
   |            |                           |                           |
   |            |                           | 1 - Timezone adjustment   |
   |            |                           | of queries performed      |
   +------------+---------------------------+---------------------------+

.. _sect_K.6:

SOP Class Definitions
---------------------

.. _sect_K.6.1:

Modality Worklist SOP Class
~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. _sect_K.6.1.1:

Modality Worklist SOP Class Overview
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Modality Worklist SOP Class defined within the Basic Worklist
Management Service Class defines an application-level class of service
that facilitates the communication of information to the imaging
modality about Scheduled Procedure Steps, and entities related to the
Scheduled Procedure Steps. As will be detailed below, part of the
information carried by the worklist mechanism is intended to be used by
the imaging modality itself, but much of the information is intended to
be presented to the modality operator.

This worklist is structured according to Scheduled Procedure Steps. A
procedure step is a unit of service in the context of a requested
imaging procedure.

The Modality Worklist SOP Class supports the following requirements:

-  Verify patient (e.g., download patient demographic information from
   IS to Modality, to verify that the person to be examined is the
   intended subject).

-  Select a Scheduled Procedure Step from the IS (e.g., download
   procedure step information from the IS to the Modality). The Modality
   Worklist SOP Class supports two alternatives for the realization of
   this requirement, supporting different organization methods of the
   department:

   -  The Modality may obtain the list of Scheduled Procedure Steps from
      the IS. Display of the list and selection from the list is done at
      the Modality.

   -  The list is displayed and selection is performed on the IS. This
      implies, that the information is obtained by the Modality just
      before the Scheduled Procedure Step starts.

-  Prepare the performance of a Scheduled Procedure Step.

-  Couple DICOM images unambiguously with related information from the
   IS (e.g., patient demographics, procedure description, ID data
   structure from the IS, contextual IS information).

-  Capture all the Attributes from the IS, that are mandatory to be
   inserted into the DICOM Image Object

The Modality Worklist SOP Class is not intended to provide access to all
IS information and services that may be of interest to a Modality
operator or attending physician. Its primary focus is the efficient
operation of the image acquisition equipment. DICOM SOP Classes such as
the Relevant Patient Information Query SOP Class and non-DICOM Services
that fall beyond the scope of the Modality Worklist SOP Class may be
needed.

The Modality Worklist SOP Class does not support the transmission of
information from the Modality to the information system.

.. _sect_K.6.1.2:

Modality Worklist Information Model
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. _sect_K.6.1.2.1:

E/R Model
'''''''''

In response to a given C-FIND request, the SCP might have to send
several C-FIND responses, (i.e., one C-FIND response per matching
worklist item). Each worklist item focuses on one Scheduled Procedure
Step and the related information. The E-R diagram presented in
`figure_title <#figure_K.6-1>`__ depicts the content of one C-FIND
request, that is:

-  the matching Scheduled Procedure Step, the Requested Procedure to
   which the Scheduled Procedure Step contributes, the Imaging Service
   Request in which the associated Requested Procedure is ordered, any
   associated Visit, and the Patient who is to be the subject of the
   Procedure.

Therefore, for a given C-FIND request, a given Scheduled Procedure Step
will appear in only one of the resulting C-FIND responses. Obviously,
information about the Requested Procedure, Imaging Service Request,
Visit and Patient may be mentioned in several of these C-FIND responses.

The Modality Worklist Information Model is represented by the Entity
Relationship diagram shown in figure `SOP Class
Definitions <#sect_K.6>`__ -1.

.. note::

   The entities appearing in messages related to the Modality Worklist
   SOP Class are required to comply to the Modality Worklist model.
   However, DICOM does not define the internal structure of the
   database.

The entry point of the Modality Worklist is the Scheduled Procedure Step
entity.

The Attributes of a Scheduled Procedure Step Worklist can be found in
the following Modules in .

-  Patient Relationship Module

-  Patient Identification Module

-  Patient Demographic Module

-  Patient Medical Module

-  Visit Relationship Module

-  Visit Identification Module

-  Visit Status Module

-  Visit Admission Module

-  Scheduled Procedure Step Module

-  Requested Procedure Module

-  Imaging Service Request Module

.. _sect_K.6.1.2.2:

Modality Worklist Attributes
''''''''''''''''''''''''''''

`table_title <#table_K.6-1>`__ defines the Attributes of the Modality
Worklist Information Model:

.. table:: Attributes for the Modality Worklist Information Model

   +-------------+-------------+-------------+-------------+-------------+
   | Description | Tag         | Matching    | Return Key  | Remark /    |
   | / Module    |             | Key Type    | Type        | Matching    |
   |             |             |             |             | Type        |
   +=============+=============+=============+=============+=============+
   | **Scheduled |             |             |             |             |
   | Procedure   |             |             |             |             |
   | Step**      |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Scheduled   | (0040,0100) | R           | 1           | The         |
   | Procedure   |             |             |             | Attributes  |
   | Step        |             |             |             | of the      |
   | Sequence    |             |             |             | Scheduled   |
   |             |             |             |             | Procedure   |
   |             |             |             |             | Step shall  |
   |             |             |             |             | only be     |
   |             |             |             |             | retrieved   |
   |             |             |             |             | with        |
   |             |             |             |             | Sequence    |
   |             |             |             |             | Matching.   |
   |             |             |             |             |             |
   |             |             |             |             | The         |
   |             |             |             |             | Scheduled   |
   |             |             |             |             | Procedure   |
   |             |             |             |             | Step        |
   |             |             |             |             | Sequence    |
   |             |             |             |             | shall       |
   |             |             |             |             | contain     |
   |             |             |             |             | only a      |
   |             |             |             |             | single      |
   |             |             |             |             | Item.       |
   +-------------+-------------+-------------+-------------+-------------+
   | >Scheduled  | (0040,0001) | R           | 1           | Scheduled   |
   | Station AE  |             |             |             | Station AE  |
   | Title       |             |             |             | Title shall |
   |             |             |             |             | be          |
   |             |             |             |             | retrieved   |
   |             |             |             |             | with Single |
   |             |             |             |             | Value       |
   |             |             |             |             | Matching    |
   |             |             |             |             | only.       |
   +-------------+-------------+-------------+-------------+-------------+
   | >Scheduled  | (0040,0002) | R           | 1           | Scheduled   |
   | Procedure   |             |             |             | Step Start  |
   | Step Start  |             |             |             | Date shall  |
   | Date        |             |             |             | be          |
   |             |             |             |             | retrieved   |
   |             |             |             |             | with Single |
   |             |             |             |             | Value       |
   |             |             |             |             | Matching or |
   |             |             |             |             | Range       |
   |             |             |             |             | Matching.   |
   |             |             |             |             |             |
   |             |             |             |             | See remark  |
   |             |             |             |             | under       |
   |             |             |             |             | Scheduled   |
   |             |             |             |             | Procedure   |
   |             |             |             |             | Step Start  |
   |             |             |             |             | Time        |
   |             |             |             |             | (           |
   |             |             |             |             | 0040,0003). |
   +-------------+-------------+-------------+-------------+-------------+
   | >Scheduled  | (0040,0003) | R           | 1           | Scheduled   |
   | Procedure   |             |             |             | Step Start  |
   | Step Start  |             |             |             | Time shall  |
   | Time        |             |             |             | be          |
   |             |             |             |             | retrieved   |
   |             |             |             |             | with Single |
   |             |             |             |             | Value       |
   |             |             |             |             | Matching or |
   |             |             |             |             | Range       |
   |             |             |             |             | Matching.   |
   |             |             |             |             | Scheduled   |
   |             |             |             |             | Step Start  |
   |             |             |             |             | Date and    |
   |             |             |             |             | Scheduled   |
   |             |             |             |             | Step Start  |
   |             |             |             |             | Time are    |
   |             |             |             |             | subject to  |
   |             |             |             |             | Range       |
   |             |             |             |             | Matching.   |
   |             |             |             |             | If both     |
   |             |             |             |             | keys are    |
   |             |             |             |             | specified   |
   |             |             |             |             | for Range   |
   |             |             |             |             | Matching,   |
   |             |             |             |             | e.g., the   |
   |             |             |             |             | date range  |
   |             |             |             |             | July 5 to   |
   |             |             |             |             | July 7 and  |
   |             |             |             |             | the time    |
   |             |             |             |             | range 10am  |
   |             |             |             |             | to 6pm      |
   |             |             |             |             | specifies   |
   |             |             |             |             | the time    |
   |             |             |             |             | period      |
   |             |             |             |             | starting on |
   |             |             |             |             | July 5,     |
   |             |             |             |             | 10am until  |
   |             |             |             |             | July 7,     |
   |             |             |             |             | 6pm.        |
   |             |             |             |             |             |
   |             |             |             |             | .. note::   |
   |             |             |             |             |             |
   |             |             |             |             |    If the   |
   |             |             |             |             |             |
   |             |             |             |             | Information |
   |             |             |             |             |    System   |
   |             |             |             |             |    does not |
   |             |             |             |             |    provide  |
   |             |             |             |             |             |
   |             |             |             |             |  scheduling |
   |             |             |             |             |    for      |
   |             |             |             |             |             |
   |             |             |             |             |  individual |
   |             |             |             |             |             |
   |             |             |             |             |   Procedure |
   |             |             |             |             |    Steps,   |
   |             |             |             |             |    it may   |
   |             |             |             |             |    use the  |
   |             |             |             |             |    closest  |
   |             |             |             |             |             |
   |             |             |             |             |  scheduling |
   |             |             |             |             |             |
   |             |             |             |             | information |
   |             |             |             |             |    it       |
   |             |             |             |             |             |
   |             |             |             |             |   possesses |
   |             |             |             |             |    (e.g.,   |
   |             |             |             |             |             |
   |             |             |             |             |  Procedures |
   |             |             |             |             |    are      |
   |             |             |             |             |    subject  |
   |             |             |             |             |    to       |
   |             |             |             |             |             |
   |             |             |             |             |  scheduling |
   |             |             |             |             |    instead  |
   |             |             |             |             |    of       |
   |             |             |             |             |             |
   |             |             |             |             |   Procedure |
   |             |             |             |             |    Steps).  |
   +-------------+-------------+-------------+-------------+-------------+
   | >Modality   | (0008,0060) | R           | 1           | The         |
   |             |             |             |             | Modality    |
   |             |             |             |             | shall be    |
   |             |             |             |             | retrieved   |
   |             |             |             |             | with Single |
   |             |             |             |             | Value       |
   |             |             |             |             | Matching.   |
   +-------------+-------------+-------------+-------------+-------------+
   | >Scheduled  | (0040,0006) | R           | 2           | Scheduled   |
   | Performing  |             |             |             | Performing  |
   | Physician's |             |             |             | Physician's |
   | Name        |             |             |             | Name shall  |
   |             |             |             |             | be          |
   |             |             |             |             | retrieved   |
   |             |             |             |             | with Single |
   |             |             |             |             | Value       |
   |             |             |             |             | Matching or |
   |             |             |             |             | Wild Card   |
   |             |             |             |             | Matching.   |
   +-------------+-------------+-------------+-------------+-------------+
   | >Scheduled  | (0040,0007) | O           | 1C          | Either the  |
   | Procedure   |             |             |             | Scheduled   |
   | Step        |             |             |             | Procedure   |
   | Description |             |             |             | Step        |
   |             |             |             |             | Description |
   |             |             |             |             | (0040,0007) |
   |             |             |             |             | or the      |
   |             |             |             |             | Scheduled   |
   |             |             |             |             | Protocol    |
   |             |             |             |             | Code        |
   |             |             |             |             | Sequence    |
   |             |             |             |             | (0040,0008) |
   |             |             |             |             | or both     |
   |             |             |             |             | shall be    |
   |             |             |             |             | supported   |
   |             |             |             |             | by the SCP. |
   +-------------+-------------+-------------+-------------+-------------+
   | >Scheduled  | (0040,0010) | O           | 2           |             |
   | Station     |             |             |             |             |
   | Name        |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Scheduled  | (0040,0011) | O           | 2           |             |
   | Procedure   |             |             |             |             |
   | Step        |             |             |             |             |
   | Location    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Referenced | (0018,990C) | O           | 3           |             |
   | Defined     |             |             |             |             |
   | Protocol    |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | (0008,1150) | O           | 1           |             |
   | >Referenced |             |             |             |             |
   | SOP Class   |             |             |             |             |
   | UID         |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | (0008,1155) | O           | 1           |             |
   | >Referenced |             |             |             |             |
   | SOP         |             |             |             |             |
   | Instance    |             |             |             |             |
   | UID         |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Referenced | (0018,990D) | O           | 3           |             |
   | Performed   |             |             |             |             |
   | Protocol    |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | (0008,1150) | O           | 1           |             |
   | >Referenced |             |             |             |             |
   | SOP Class   |             |             |             |             |
   | UID         |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | (0008,1155) | O           | 1           |             |
   | >Referenced |             |             |             |             |
   | SOP         |             |             |             |             |
   | Instance    |             |             |             |             |
   | UID         |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Scheduled  | (0040,0008) | O           | 1C          | Either the  |
   | Protocol    |             |             |             | Scheduled   |
   | Code        |             |             |             | Procedure   |
   | Sequence    |             |             |             | Step        |
   |             |             |             |             | Description |
   |             |             |             |             | (0040,0007) |
   |             |             |             |             | or the      |
   |             |             |             |             | Scheduled   |
   |             |             |             |             | Protocol    |
   |             |             |             |             | Code        |
   |             |             |             |             | Sequence    |
   |             |             |             |             | (0040,0008) |
   |             |             |             |             | or both     |
   |             |             |             |             | shall be    |
   |             |             |             |             | supported   |
   |             |             |             |             | by the SCP. |
   |             |             |             |             |             |
   |             |             |             |             | The         |
   |             |             |             |             | Scheduled   |
   |             |             |             |             | Protocol    |
   |             |             |             |             | Code        |
   |             |             |             |             | Sequence    |
   |             |             |             |             | contains    |
   |             |             |             |             | one or more |
   |             |             |             |             | Items.      |
   +-------------+-------------+-------------+-------------+-------------+
   | *>>Includ   |             |             |             |             |
   | e*\ `table_ |             |             |             |             |
   | title <#tab |             |             |             |             |
   | le_8-2a>`__ |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Protocol  | (0040,0440) | -           | 3           | The         |
   | Context     |             |             |             | Protocol    |
   | Sequence    |             |             |             | Context     |
   |             |             |             |             | Sequence    |
   |             |             |             |             | and its     |
   |             |             |             |             | Items shall |
   |             |             |             |             | not be used |
   |             |             |             |             | for         |
   |             |             |             |             | matching    |
   +-------------+-------------+-------------+-------------+-------------+
   | >>>Value    | (0040,A040) | -           | 1           |             |
   | Type        |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>>Concept  | (0040,A043) | -           | 1           |             |
   | Name Code   |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | *>>>>Includ |             |             |             |             |
   | e*\ `table_ |             |             |             |             |
   | title <#tab |             |             |             |             |
   | le_8-3a>`__ |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>>DateTime | (0040,A120) | -           | 1C          | Required if |
   |             |             |             |             | Value Type  |
   |             |             |             |             | (0040,A040) |
   |             |             |             |             | is          |
   |             |             |             |             | DATETIME.   |
   +-------------+-------------+-------------+-------------+-------------+
   | >>>Person   | (0040,A123) | -           | 1C          | Required if |
   | Name        |             |             |             | Value Type  |
   |             |             |             |             | (0040,A040) |
   |             |             |             |             | is PNAME.   |
   +-------------+-------------+-------------+-------------+-------------+
   | >>>Text     | (0040,A160) | -           | 1C          | Required if |
   | Value       |             |             |             | Value Type  |
   |             |             |             |             | (0040,A040) |
   |             |             |             |             | is TEXT.    |
   +-------------+-------------+-------------+-------------+-------------+
   | >>>Concept  | (0040,A168) | -           | 1C          | Required if |
   | Code        |             |             |             | Value Type  |
   | Sequence    |             |             |             | (0040,A040) |
   |             |             |             |             | is CODE.    |
   +-------------+-------------+-------------+-------------+-------------+
   | *>>>>Includ |             |             |             |             |
   | e*\ `table_ |             |             |             |             |
   | title <#tab |             |             |             |             |
   | le_8-3a>`__ |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>>Numeric  | (0040,A30A) | -           | 1C          | Required if |
   | Value       |             |             |             | Value Type  |
   |             |             |             |             | (0040,A040) |
   |             |             |             |             | is NUMERIC. |
   +-------------+-------------+-------------+-------------+-------------+
   | >>>         | (0040,08EA) | -           | 1C          | Required if |
   | Measurement |             |             |             | Value Type  |
   | Units Code  |             |             |             | (0040,A040) |
   | Sequence    |             |             |             | is NUMERIC. |
   +-------------+-------------+-------------+-------------+-------------+
   | *>>>>Includ |             |             |             |             |
   | e*\ `table_ |             |             |             |             |
   | title <#tab |             |             |             |             |
   | le_8-3a>`__ |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | *>>>All     |             | -           | 3           |             |
   | other       |             |             |             |             |
   | Attributes  |             |             |             |             |
   | of the      |             |             |             |             |
   | Protocol    |             |             |             |             |
   | Context     |             |             |             |             |
   | Sequence*   |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Pre        | (0040,0012) | O           | 2C          | Required if |
   | -Medication |             |             |             | Pre         |
   |             |             |             |             | -Medication |
   |             |             |             |             | is to be    |
   |             |             |             |             | applied to  |
   |             |             |             |             | that        |
   |             |             |             |             | Scheduled   |
   |             |             |             |             | Procedure   |
   |             |             |             |             | Step.       |
   +-------------+-------------+-------------+-------------+-------------+
   | >Scheduled  | (0040,0009) | O           | 1           |             |
   | Procedure   |             |             |             |             |
   | Step ID     |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Requested  | (0032,1070) | O           | 2C          | Required if |
   | Contrast    |             |             |             | Contrast    |
   | Agent       |             |             |             | Media is to |
   |             |             |             |             | be applied  |
   |             |             |             |             | to that     |
   |             |             |             |             | Scheduled   |
   |             |             |             |             | Procedure   |
   |             |             |             |             | Step.       |
   +-------------+-------------+-------------+-------------+-------------+
   | >Scheduled  | (0040,0020) | O           | 3           |             |
   | Procedure   |             |             |             |             |
   | Step Status |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | *>All other |             | O           | 3           |             |
   | Attributes  |             |             |             |             |
   | of the      |             |             |             |             |
   | Scheduled   |             |             |             |             |
   | Procedure   |             |             |             |             |
   | Step        |             |             |             |             |
   | Sequence*   |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Scheduled   | (0040,0500) | O           | 3           | One or more |
   | Specimen    |             |             |             | Items may   |
   | Sequence    |             |             |             | be returned |
   |             |             |             |             | in this     |
   |             |             |             |             | Sequence.   |
   +-------------+-------------+-------------+-------------+-------------+
   | >Container  | (0040,0512) | O           | 1           |             |
   | Identifier  |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Container  | (0040,0518) | -           | 2           | Zero or one |
   | Type Code   |             |             |             | Item shall  |
   | Sequence    |             |             |             | be returned |
   |             |             |             |             | in this     |
   |             |             |             |             | Sequence.   |
   +-------------+-------------+-------------+-------------+-------------+
   | *>>Includ   |             |             |             |             |
   | e*\ `table_ |             |             |             |             |
   | title <#tab |             |             |             |             |
   | le_8-3a>`__ |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Specimen   | (0040,0560) | O           | 1           | One or more |
   | Description |             |             |             | Items shall |
   | Sequence    |             |             |             | be returned |
   |             |             |             |             | in this     |
   |             |             |             |             | Sequence.   |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Specimen  | (0040,0551) | O           | 1           |             |
   | Identifier  |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Specimen  | (0040,0554) | O           | 1           |             |
   | UID         |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | *>>All      |             | O           | 3           | Specimen    |
   | other       |             |             |             | Preparation |
   | Attributes  |             |             |             | Sequence    |
   | of the      |             |             |             | (           |
   | Specimen    |             |             |             | 0040,0610), |
   | Description |             |             |             | if present, |
   | Sequence*   |             |             |             | describes   |
   |             |             |             |             | preparation |
   |             |             |             |             | steps       |
   |             |             |             |             | already     |
   |             |             |             |             | performed,  |
   |             |             |             |             | not         |
   |             |             |             |             | scheduled   |
   |             |             |             |             | procedure   |
   |             |             |             |             | steps       |
   +-------------+-------------+-------------+-------------+-------------+
   | *>All other |             | O           | 3           |             |
   | Attributes  |             |             |             |             |
   | of the      |             |             |             |             |
   | Scheduled   |             |             |             |             |
   | Specimen    |             |             |             |             |
   | Sequence*   |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Barcode     | (2200,0005) | O           | 3           | This may be |
   | Value       |             |             |             | the same as |
   |             |             |             |             | Container   |
   |             |             |             |             | Identifier  |
   |             |             |             |             | (           |
   |             |             |             |             | 0040,0512). |
   +-------------+-------------+-------------+-------------+-------------+
   | **Requested |             |             |             |             |
   | Procedure** |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Requested   | (0040,1001) | O           | 1           |             |
   | Procedure   |             |             |             |             |
   | ID          |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Requested   | (0032,1060) | O           | 1C          | The         |
   | Procedure   |             |             |             | Requested   |
   | Description |             |             |             | Procedure   |
   |             |             |             |             | Description |
   |             |             |             |             | (0032,1060) |
   |             |             |             |             | or the      |
   |             |             |             |             | Requested   |
   |             |             |             |             | Procedure   |
   |             |             |             |             | Code        |
   |             |             |             |             | Sequence    |
   |             |             |             |             | (0032,1064) |
   |             |             |             |             | or both     |
   |             |             |             |             | shall be    |
   |             |             |             |             | supported   |
   |             |             |             |             | by the SCP. |
   +-------------+-------------+-------------+-------------+-------------+
   | Requested   | (0032,1064) | O           | 1C          | The         |
   | Procedure   |             |             |             | Requested   |
   | Code        |             |             |             | Procedure   |
   | Sequence    |             |             |             | Description |
   |             |             |             |             | (0032,1060) |
   |             |             |             |             | or the      |
   |             |             |             |             | Requested   |
   |             |             |             |             | Procedure   |
   |             |             |             |             | Code        |
   |             |             |             |             | Sequence    |
   |             |             |             |             | (0032,1064) |
   |             |             |             |             | or both     |
   |             |             |             |             | shall be    |
   |             |             |             |             | supported   |
   |             |             |             |             | by the SCP. |
   |             |             |             |             |             |
   |             |             |             |             | The         |
   |             |             |             |             | Requested   |
   |             |             |             |             | Procedure   |
   |             |             |             |             | Code        |
   |             |             |             |             | Sequence    |
   |             |             |             |             | shall       |
   |             |             |             |             | contain     |
   |             |             |             |             | only a      |
   |             |             |             |             | single      |
   |             |             |             |             | Item.       |
   +-------------+-------------+-------------+-------------+-------------+
   | *>Includ    |             |             |             |             |
   | e*\ `table_ |             |             |             |             |
   | title <#tab |             |             |             |             |
   | le_8-2a>`__ |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Study       | (0020,000D) | O           | 1           |             |
   | Instance    |             |             |             |             |
   | UID         |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Study Date  | (0008,0020) | O           | 3           | See note 5. |
   +-------------+-------------+-------------+-------------+-------------+
   | Study Time  | (0008,0030) | O           | 3           | See note 5. |
   +-------------+-------------+-------------+-------------+-------------+
   | Referenced  | (0008,1110) | O           | 2           |             |
   | Study       |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Referenced | (0008,1150) | O           | 1           |             |
   | SOP Class   |             |             |             |             |
   | UID         |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Referenced | (0008,1155) | O           | 1           |             |
   | SOP         |             |             |             |             |
   | Instance    |             |             |             |             |
   | UID         |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Requested   | (0040,1003) | O           | 2           |             |
   | Procedure   |             |             |             |             |
   | Priority    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Patient     | (0040,1004) | O           | 2           |             |
   | Transport   |             |             |             |             |
   | A           |             |             |             |             |
   | rrangements |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | *All other  |             | O           | 3           |             |
   | Attributes  |             |             |             |             |
   | of the*     |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | **Imaging   |             |             |             |             |
   | Service     |             |             |             |             |
   | Request**   |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Accession   | (0008,0050) | O           | 2           |             |
   | Number      |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Issuer of   | (0008,0051) | O           | 3           |             |
   | Accession   |             |             |             |             |
   | Number      |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Requesting  | (0032,1032) | O           | 2           |             |
   | Physician   |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Referring   | (0008,0090) | O           | 2           |             |
   | Physician's |             |             |             |             |
   | Name        |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | *All other  |             | O           | 3           |             |
   | Attributes  |             |             |             |             |
   | of the*     |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | **Visit     |             |             |             |             |
   | Ident       |             |             |             |             |
   | ification** |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Admission   | (0038,0010) | O           | 2           |             |
   | ID          |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Issuer of   | (0038,0014) | O           | 3           |             |
   | Admission   |             |             |             |             |
   | ID Sequence |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | *All other  |             | O           | 3           |             |
   | Attributes  |             |             |             |             |
   | of the*     |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | **Visit     |             |             |             |             |
   | Status**    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Current     | (0038,0300) | O           | 2           |             |
   | Patient     |             |             |             |             |
   | Location    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | *All other  |             | O           | 3           |             |
   | Attributes  |             |             |             |             |
   | of the*     |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | **Visit     |             |             |             |             |
   | Rel         |             |             |             |             |
   | ationship** |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Referenced  | (0008,1120) | O           | 2           |             |
   | Patient     |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Referenced | (0008,1150) | O           | 1           |             |
   | SOP Class   |             |             |             |             |
   | UID         |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Referenced | (0008,1155) | O           | 1           |             |
   | SOP         |             |             |             |             |
   | Instance    |             |             |             |             |
   | UID         |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | *All other  |             | O           | 3           |             |
   | Attributes  |             |             |             |             |
   | of the      |             |             |             |             |
   | except      |             |             |             |             |
   | those       |             |             |             |             |
   | explicitly  |             |             |             |             |
   | included in |             |             |             |             |
   | this table  |             |             |             |             |
   | (see Note   |             |             |             |             |
   | 3)*         |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | **Visit     |             |             |             |             |
   | Admission** |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | All         |             | O           | 3           |             |
   | Attributes  |             |             |             |             |
   | from the    |             |             |             |             |
   | Visit       |             |             |             |             |
   | Admission   |             |             |             |             |
   | Module      |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | **Patient   |             |             |             |             |
   | Rel         |             |             |             |             |
   | ationship** |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | All         |             | O           | 3           |             |
   | Attributes  |             |             |             |             |
   | from the    |             |             |             |             |
   | Patient     |             |             |             |             |
   | R           |             |             |             |             |
   | elationship |             |             |             |             |
   | Module      |             |             |             |             |
   | except      |             |             |             |             |
   | those       |             |             |             |             |
   | explicitly  |             |             |             |             |
   | included in |             |             |             |             |
   | this table  |             |             |             |             |
   | (see Note   |             |             |             |             |
   | 3)          |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | **Patient   |             |             |             |             |
   | Ident       |             |             |             |             |
   | ification** |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Patient's   | (0010,0010) | R           | 1           | Patient     |
   | Name        |             |             |             | Name shall  |
   |             |             |             |             | be          |
   |             |             |             |             | retrieved   |
   |             |             |             |             | with Single |
   |             |             |             |             | Value       |
   |             |             |             |             | Matching or |
   |             |             |             |             | Wild Card   |
   |             |             |             |             | Matching.   |
   +-------------+-------------+-------------+-------------+-------------+
   | Patient ID  | (0010,0020) | R           | 1           | Patient ID  |
   |             |             |             |             | shall be    |
   |             |             |             |             | retrieved   |
   |             |             |             |             | with Single |
   |             |             |             |             | Value       |
   |             |             |             |             | Matching.   |
   +-------------+-------------+-------------+-------------+-------------+
   | Issuer of   | (0010,0021) | O           | 3           |             |
   | Patient ID  |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Issuer of   | (0010,0024) | O           | 3           |             |
   | Patient ID  |             |             |             |             |
   | Qualifiers  |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Other       | (0010,1002) | O           | 3           |             |
   | Patient IDs |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | *All other  |             | O           | 3           |             |
   | Attributes  |             |             |             |             |
   | of the*     |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | **Patient   |             |             |             |             |
   | De          |             |             |             |             |
   | mographic** |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Patient's   | (0010,0030) | O           | 2           |             |
   | Birth Date  |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Patient's   | (0010,0040) | O           | 2           |             |
   | Sex         |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Patient's   | (0010,0101) | O           | 3           | The         |
   | Primary     |             |             |             | languages   |
   | Language    |             |             |             | that can be |
   | Code        |             |             |             | used to     |
   | Sequence    |             |             |             | communicate |
   |             |             |             |             | with the    |
   |             |             |             |             | patient.    |
   |             |             |             |             |             |
   |             |             |             |             | If          |
   |             |             |             |             | returned,   |
   |             |             |             |             | the         |
   |             |             |             |             | Patient's   |
   |             |             |             |             | Primary     |
   |             |             |             |             | Language    |
   |             |             |             |             | Code        |
   |             |             |             |             | Sequence    |
   |             |             |             |             | shall       |
   |             |             |             |             | contain one |
   |             |             |             |             | or more     |
   |             |             |             |             | Items. The  |
   |             |             |             |             | items are   |
   |             |             |             |             | ordered by  |
   |             |             |             |             | preference  |
   |             |             |             |             | (most       |
   |             |             |             |             | preferred   |
   |             |             |             |             | language to |
   |             |             |             |             | least       |
   |             |             |             |             | preferred   |
   |             |             |             |             | language).  |
   +-------------+-------------+-------------+-------------+-------------+
   | *>Includ    |             |             |             |             |
   | e*\ `table_ |             |             |             |             |
   | title <#tab |             |             |             |             |
   | le_8-4a>`__ |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Patient's  | (0010,0102) | O           | 3           | A modifier  |
   | Primary     |             |             |             | for a       |
   | Language    |             |             |             | Patient's   |
   | Modifier    |             |             |             | Primary     |
   | Code        |             |             |             | Language.   |
   | Sequence    |             |             |             | Can be used |
   |             |             |             |             | to specify  |
   |             |             |             |             | a national  |
   |             |             |             |             | language    |
   |             |             |             |             | variant.    |
   |             |             |             |             |             |
   |             |             |             |             | If          |
   |             |             |             |             | returned,   |
   |             |             |             |             | the         |
   |             |             |             |             | Patient's   |
   |             |             |             |             | Primary     |
   |             |             |             |             | Language    |
   |             |             |             |             | Modifier    |
   |             |             |             |             | Code        |
   |             |             |             |             | Sequence    |
   |             |             |             |             | shall       |
   |             |             |             |             | contain     |
   |             |             |             |             | only a      |
   |             |             |             |             | single      |
   |             |             |             |             | Item.       |
   +-------------+-------------+-------------+-------------+-------------+
   | *>>Includ   |             |             |             |             |
   | e*\ `table_ |             |             |             |             |
   | title <#tab |             |             |             |             |
   | le_8-4a>`__ |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Patient's   | (0010,1030) | O           | 2           |             |
   | Weight      |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Patient's   | (0010,1020) | O           | 3           |             |
   | Size        |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Conf        | (0040,3001) | O           | 2           |             |
   | identiality |             |             |             |             |
   | constraint  |             |             |             |             |
   | on patient  |             |             |             |             |
   | data        |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | *All other  |             | O           | 3           |             |
   | Attributes  |             |             |             |             |
   | of the*     |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | **Patient   |             |             |             |             |
   | Medical**   |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Patient     | (0038,0500) | O           | 2           |             |
   | State       |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Pregnancy   | (0010,21C0) | O           | 2           |             |
   | Status      |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Medical     | (0010,2000) | O           | 2           |             |
   | Alerts      |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Allergies   | (0010,2110) | O           | 2           |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Special     | (0038,0050) | O           | 2           |             |
   | Needs       |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Pertinent   | (0038,0100) | O           | 3           | Pertinent   |
   | Documents   |             |             |             | Documents   |
   | Sequence    |             |             |             | Sequence    |
   |             |             |             |             | shall be    |
   |             |             |             |             | retrieved   |
   |             |             |             |             | with        |
   |             |             |             |             | Universal   |
   |             |             |             |             | Matching    |
   |             |             |             |             | only        |
   +-------------+-------------+-------------+-------------+-------------+
   | >Referenced | (0008,1150) | -           | 1           |             |
   | SOP Class   |             |             |             |             |
   | UID         |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Referenced | (0008,1155) | -           | 1           |             |
   | SOP         |             |             |             |             |
   | Instance    |             |             |             |             |
   | UID         |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Purpose of | (0040,A170) | -           | 2           |             |
   | Reference   |             |             |             |             |
   | Code        |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | *>>Includ   |             |             |             |             |
   | e*\ `table_ |             |             |             |             |
   | title <#tab |             |             |             |             |
   | le_8-3a>`__ |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Document   | (0042,0010) | -           | 2           |             |
   | Title       |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | *All other  |             | O           | 3           |             |
   | Attributes  |             |             |             |             |
   | of the*     |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+

.. note::

   1. Just like Series and Image Entities specified in the
      Query/Retrieve Service Class either an SCU or an SCP may support
      optional Matching Key Attributes and/or Type 3 Return Key
      Attributes that are not included in the Worklist Information Model
      (i.e., Standard or Private Attributes). This is considered a
      Standard Extended SOP Class (see ).

   2. Each Module contains a Comment Attribute. This may be used to
      transmit non-structured information, which may be displayed to the
      operator of the Modality.

   3. The reason for this exclusion is to assure that the Attributes
      that may be present in multiple Modules are included only once
      with the meaning pertaining to only one Module (for example,
      Referenced Study Sequence (0008,1110) shall be included once with
      the meaning as defined in the Requested Procedure Module).

   4. The use of Specific Character Set is discussed in section `Request
      Identifier Structure <#sect_K.4.1.1.3.1>`__ and `Response
      Identifier Structure <#sect_K.4.1.1.3.2>`__.

   5. The values of Study Date (0008,0020) and Study Time (0008,0030)
      may be provided in order to achieve consistency of Study level
      Attributes in composite instances generated in multiple performed
      procedure steps on different devices, and the worklist values may
      be updated by the SCP based on information received from Modality
      Performed Procedure Steps or by examining the composite instances
      generated.

The Attributes in `table_title <#table_K.6-1a>`__ are not part of the
Worklist Information Model; their inclusion in the C-FIND request and
response identifier are governed by rules in sections `Request
Identifier Structure <#sect_K.4.1.1.3.1>`__ and `Response Identifier
Structure <#sect_K.4.1.1.3.2>`__, respectively.

.. table:: Attributes for the Modality Worklist C-FIND Identifier

   +-------------+-------------+-------------+-------------+-------------+
   | Attribute   | Tag         | Request     | Response    | Remark Type |
   | Name        |             | Identifier  | Identifier  |             |
   +=============+=============+=============+=============+=============+
   | Specific    | (0008,0005) | 1C          | 1C          | This        |
   | Character   |             |             |             | Attribute   |
   | Set         |             |             |             | is required |
   |             |             |             |             | if expanded |
   |             |             |             |             | or          |
   |             |             |             |             | replacement |
   |             |             |             |             | character   |
   |             |             |             |             | sets are    |
   |             |             |             |             | used. See   |
   |             |             |             |             | `Attribute  |
   |             |             |             |             | Match       |
   |             |             |             |             | ing <#sect_ |
   |             |             |             |             | C.2.2.2>`__ |
   |             |             |             |             | and         |
   |             |             |             |             | `Identifie  |
   |             |             |             |             | r <#sect_K. |
   |             |             |             |             | 4.1.1.3>`__ |
   +-------------+-------------+-------------+-------------+-------------+
   | Timezone    | (0008,0201) | 1C          | 1C          | This        |
   | Offset From |             |             |             | Attribute   |
   | UTC         |             |             |             | is required |
   |             |             |             |             | if times    |
   |             |             |             |             | are to be   |
   |             |             |             |             | interpreted |
   |             |             |             |             | explicitly  |
   |             |             |             |             | in the      |
   |             |             |             |             | designated  |
   |             |             |             |             | local       |
   |             |             |             |             | timezone.   |
   |             |             |             |             | See         |
   |             |             |             |             | `Attribute  |
   |             |             |             |             | Match       |
   |             |             |             |             | ing <#sect_ |
   |             |             |             |             | C.2.2.2>`__ |
   |             |             |             |             | and         |
   |             |             |             |             | `Identifie  |
   |             |             |             |             | r <#sect_K. |
   |             |             |             |             | 4.1.1.3>`__ |
   +-------------+-------------+-------------+-------------+-------------+
   | HL7         | (0040,A390) | -           | 1C          | One or more |
   | Structured  |             |             |             | Items may   |
   | Document    |             |             |             | be included |
   | Reference   |             |             |             | in this     |
   | Sequence    |             |             |             | sequence.   |
   |             |             |             |             |             |
   |             |             |             |             | Required if |
   |             |             |             |             | HL7         |
   |             |             |             |             | Structured  |
   |             |             |             |             | Documents   |
   |             |             |             |             | are         |
   |             |             |             |             | referenced  |
   |             |             |             |             | within the  |
   |             |             |             |             | Identifier. |
   |             |             |             |             | See         |
   |             |             |             |             | `Identifie  |
   |             |             |             |             | r <#sect_K. |
   |             |             |             |             | 4.1.1.3>`__ |
   +-------------+-------------+-------------+-------------+-------------+
   | >Referenced | (0008,1150) | -           | 1           |             |
   | SOP Class   |             |             |             |             |
   | UID         |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Referenced | (0008,1155) | -           | 1           |             |
   | SOP         |             |             |             |             |
   | Instance    |             |             |             |             |
   | UID         |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >HL7        | (0040,E001) | -           | 1           |             |
   | Instance    |             |             |             |             |
   | Identifier  |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Retrieve   | (0040,E010) | -           | 3           |             |
   | URI         |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+

.. _sect_K.6.1.3:

Conformance Requirements
^^^^^^^^^^^^^^^^^^^^^^^^

An implementation may conform to the Modality Worklist SOP Class as an
SCU or an SCP. The Conformance Statement shall be in the format defined
in .

.. _sect_K.6.1.3.1:

SCU Conformance
'''''''''''''''

An implementation that conforms to the Modality Worklist SOP Class shall
support queries against the Worklist Information Model described in
`Modality Worklist Information Model <#sect_K.6.1.2>`__ of this Annex
using the baseline C-FIND SCU Behavior described in `C-FIND SCU
Behavior <#sect_K.4.1.2>`__ of this Part.

An implementation that conforms to the Modality Worklist SOP Class as an
SCU shall state in its Conformance Statement whether it requests
matching on Optional Matching Key Attributes. If it requests Type 3
Return Key Attributes, then it shall list these Optional Return Key
Attributes. It shall identify any Templates it supports for the Protocol
Context Sequence.

An implementation that conforms to the Modality Worklist SOP Class as an
SCU shall state in its Conformance Statement whether or not it supports
extended negotiation of fuzzy semantic matching of person names.

An implementation that conforms to the Modality Worklist SOP Class as an
SCU shall state in its Conformance Statement how it makes use of
Specific Character Set (0008,0005) and Timezone Offset From UTC
(0008,0201) when encoding queries and interpreting responses.

.. _sect_K.6.1.3.2:

SCP Conformance
'''''''''''''''

An implementation that conforms to the Modality Worklist SOP Class shall
support queries against the Worklist Information Model described in
`Modality Worklist Information Model <#sect_K.6.1.2>`__ of this Annex
using the C-FIND SCP Behavior described in `C-FIND SCP
Behavior <#sect_K.4.1.3>`__ of this Part.

An implementation that conforms to the Modality Worklist SOP Class as an
SCP shall state in its Conformance Statement whether it supports
matching on Optional Matching Key Attributes. If it supports Type 3
Return Key Attributes, then it shall list the Optional Return Key
Attributes that it supports. It shall identify any Templates it supports
for the Protocol Context Sequence.

An implementation that conforms to the Modality Worklist SOP Class as an
SCP shall state in its Conformance Statement whether it supports
case-insensitive matching for PN VR Attributes and list Attributes for
which this applies.

An implementation that conforms to the Modality Worklist SOP Class as an
SCP shall state in its Conformance Statement whether or not it supports
extended negotiation of fuzzy semantic matching of person names. If
fuzzy semantic matching of person names is supported, then the mechanism
for fuzzy semantic matching shall be specified.

An implementation that conforms to the Modality Worklist SOP Class as an
SCP shall state in its Conformance Statement how it makes use of
Specific Character Set (0008,0005) and Timezone Offset From UTC
(0008,0201) when interpreting queries, performing matching and encoding
responses.

.. _sect_K.6.1.4:

SOP Class
^^^^^^^^^

The Modality Worklist SOP Class in the Basic Worklist Service Class
identifies the Modality Worklist Information Model, and the DIMSE-C
operations supported. The following Standard SOP Class is identified:

.. table:: Modality Worklist SOP Class

   ========================================== ======================
   SOP Class Name                             SOP Class UID
   ========================================== ======================
   Modality Worklist Information Model - FIND 1.2.840.10008.5.1.4.31
   ========================================== ======================

.. _sect_K.6.2:

General Purpose Worklist SOP Class (Retired)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Retired. See PS 3.4-2011.

.. _sect_K.7:

Examples for the Usage of the Modality Worklist (Informative)
-------------------------------------------------------------

Moved to

.. _sect_K.8:

General Purpose Worklist Example (Informative) (Retired)
--------------------------------------------------------

Retired. See PS 3.17-2011.

