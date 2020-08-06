.. _chapter_V:

Substance Administration Query Service Class (Normative)
========================================================

.. _sect_V.1:

Overview
--------

.. _sect_V.1.1:

Scope
~~~~~

The Substance Administration Query Service Class defines an
application-level class-of-service that facilitates obtaining detailed
information about substances or devices used in imaging, image-guided
treatment, and related procedures. It also facilitates obtaining
approval for the administration of a specific contrast agent or drug to
a specific patient.

This Service Class is intended as part of a larger workflow that
addresses patient safety in the imaging environment. This Service
addresses only the communication protocol that allows a point of care
device (imaging modality) to interrogate an SCP Application for
information about an administered substance, or for verification of
appropriateness of the substance for the patient. The SCP Application
uses patient safety related data, such as allergies, current
medications, appropriate dosages, patient condition indicated by lab
results, etc., to respond to the queries; however, the mechanism of such
use is beyond the scope of this Standard. How the point of care device
uses the responses to the queries, e.g., by display to a user, or by
locking of certain device functions, is also beyond the scope of this
Standard.

.. note::

   1. The SCP of this Service Class is not necessarily a clinical
      decision support (CDS) system, but may be a gateway system between
      this DICOM Service and an HL7 or proprietary interface of a CDS
      system. Such implementation design is beyond the scope of the
      DICOM Standard.

   2. The Service will result in a Query response containing zero or one
      items. However, to facilitate implementation, the Service uses the
      general query mechanism supporting multiple item responses, as
      used in other DICOM query service classes.

.. _sect_V.1.2:

Conventions
~~~~~~~~~~~

Key Attributes serve two purposes; they may be used as Matching Key
Attributes and Return Key Attributes. Matching Key Attributes may be
used for matching (criteria to be used in the C-FIND request to
determine whether an entity matches the query). Return Key Attributes
may be used to specify desired return Attributes (what elements in
addition to the Matching Key Attributes have to be returned in the
C-FIND response).

Matching Key Attributes may be of Type "required" (R) or "optional" (O).
Return Key Attributes may be of Type 1, 1C, 2, 2C, 3 as defined in .

.. _sect_V.1.3:

Substance Administration Query Information Model
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In order to serve as a Service Class Provider (SCP) of the Substance
Administration Query Service Class, a DICOM Application Entity (AE) must
be able to return information about the Attributes of a substance,
device, or a substance administration act. This information is organized
into well defined Substance Administration Query Information Models.

A specific SOP Class of the Substance Administration Query Service Class
consists of an informative Overview, an Information Model Definition and
a DIMSE-C Service Group. In this Service Class, the Information Model
plays a role similar to an Information Object Definition (IOD) of other
DICOM Service Classes.

.. _sect_V.1.4:

Service Definition
~~~~~~~~~~~~~~~~~~

Two peer DICOM AEs implement a SOP Class of the Substance Administration
Query Service Class with one serving in the SCU role and one serving in
the SCP role. SOP Classes of the Substance Administration Query Service
Class are implemented using the DIMSE-C C-FIND service as defined in .

Only a baseline behavior of the DIMSE-C C-FIND is used in the Service
Class. Extended negotiation is not used.

The following description of the DIMSE-C C-FIND service provides a brief
overview of the SCU/SCP semantics.

A C-FIND service conveys the following semantics:

-  The SCU requests that the SCP perform a match for the Matching Keys
   and return values for the Return Keys that have been specified in the
   Identifier of the request, against the information that the SCP
   possesses relating to the Information Model specified in the SOP
   Class.

.. note::

   In this Annex, the term "Identifier" refers to the Identifier service
   parameter of the C-FIND service as defined in .

-  The SCP generates at most one C-FIND response for a match with an
   Identifier containing the values of all Matching Key Attributes and
   all known Return Key Attributes requested. This response shall
   contain a status of Pending.

-  When the process of matching is complete, with zero or one match, a
   C-FIND response is sent with a status of Success and no Identifier.

-  A Failure response to a C-FIND request indicates that the SCP is
   unable to process the request.

-  The SCU may cancel the C-FIND service by issuing a C-CANCEL-FIND
   request at any time during the processing of the C-FIND service. The
   SCP will interrupt all matching and return a status of Canceled.

.. note::

   The SCU needs to be prepared to receive C-FIND responses sent by the
   SCP until the SCP finally processed the C-CANCEL-FIND request.

.. _sect_V.2:

Substance Administration Query Information Model Definition
-----------------------------------------------------------

The Substance Administration Query Information Model is identified by
the SOP Class negotiated at Association establishment time. The SOP
Class is composed of both an Information Model and a DIMSE-C Service
Group.

Information Model Definitions for Standard SOP Classes of the Substance
Administration Query Service Class are defined in this Annex. A
Substance Administration Query Information Model Definition contains:

-  an Entity-Relationship Model Definition

-  a Key Attributes Definition.

.. _sect_V.2.1:

Entity-Relationship Model Definition
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Substance Administration Query Information Models consist of a single
level that includes all Matching Key Attributes and all Return Key
Attributes that may be sent from the SCU to the SCP in the request, and
whose values are expected to be returned from the SCP to the SCU in the
response (or Query items). The Matching Key Attribute Values in the
request specify the Query items that are to be returned in the response.
All Key Attributes (the Matching Key Attributes and the Return Key
Attributes) in the request determine which Attribute Values are returned
in the response for that Query.

.. _sect_V.2.2:

Attributes Definition
~~~~~~~~~~~~~~~~~~~~~

Attributes are defined for each entity in the internal
Entity-Relationship Model. An Identifier in a C-FIND request shall
contain values to be matched against the Attributes of the Entities in a
Substance Administration Query Information Model. For any Query request,
the set of entities for which Attributes are returned shall be
determined by the set of Matching and Return Key Attributes specified in
the Identifier.

.. _sect_V.2.2.1:

Attribute Types
^^^^^^^^^^^^^^^

All Attributes of entities in a Substance Administration Query
Information Model shall be specified both as a Matching Key Attribute
(either required or optional) and as a Return Key Attribute.

.. _sect_V.2.2.1.1:

Matching Key Attributes
'''''''''''''''''''''''

The Matching Key Attributes are Keys, which select Query items to be
included in a requested Query.

.. _sect_V.2.2.1.1.1:

Required Matching Key Attributes
                                

A Substance Administration Query Service SCP shall support matching
based on values of all Required Matching Key Attributes of the C-FIND
request.

.. _sect_V.2.2.1.1.2:

Optional Matching Key Attributes
                                

In the Substance Administration Query Information Model, a set of
Attributes may be defined as Optional Matching Key Attributes. Optional
Matching Key Attributes contained in the Identifier of a C-FIND request
may induce two different types of behavior depending on support for
matching by the SCP. If the SCP

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

.. _sect_V.2.2.1.2:

Return Key Attributes
'''''''''''''''''''''

The values of Return Key Attributes to be retrieved with the Query are
specified with zero-length (Universal Matching) in the C-FIND request.
SCPs shall support Return Key Attributes defined by a Substance
Administration Query Information Model according to the Data Element
Type (1, 1C, 2, 2C, 3) as defined in .

Every Matching Key Attribute shall also be considered as a Return Key
Attribute. Therefore the C-FIND response shall contain, in addition to
the values of the requested Return Key Attributes, the values of the
requested Matching Key Attributes.

.. note::

   1. The Conformance Statement of the SCP lists the Return Key
      Attributes of Type 3 that are supported.

   2. An SCU may choose to supply any subset of Return Key Attributes.

   3. An SCU can not expect to receive any Type 3 Return Key Attributes.

   4. Return Key Attributes with VR of SQ may be specified either with
      zero-length, or with a zero-length item in the sequence.

.. _sect_V.2.2.2:

Attribute Matching
^^^^^^^^^^^^^^^^^^

The following types of matching, which are defined by the Query/Retrieve
Service Class in `Query/Retrieve Service Class
(Normative) <#chapter_C>`__, may be performed on Matching Key Attributes
in the Substance Administration Query Service Class. Different Matching
Key Attributes may be subject for different matching types. The
Substance Administration Query Information Model defines the type of
matching for each Required Matching Key Attribute. The Conformance
Statement of the SCP shall define the type of matching for each Optional
Matching Key Attribute. The types of matching are:

-  Single Value Matching

-  Sequence Matching

The following type of matching, which is defined by the Query/Retrieve
Service Class in `Query/Retrieve Service Class
(Normative) <#chapter_C>`__ of this Part, shall be performed on Return
Key Attributes in the Substance Administration Query Service Class.

-  Universal Matching

See `Attribute Matching <#sect_C.2.2.2>`__ and subsections for specific
rules governing of Matching Key Attribute encoding for and performing of
different types of matching.

The Specific Character Set (0008,0005) Attribute may be present in the
Identifier but is never matched, i.e., it is not considered a Matching
Key Attribute. See `Attribute Matching <#sect_C.2.2.2>`__ for details.

.. _sect_V.3:

Query Information Models
------------------------

Each Substance Administration Query Information Model is associated with
one SOP Class. The following Substance Administration Query Information
Models are defined:

-  Product Characteristics Query Information Model

-  Substance Approval Query Information Model

.. _sect_V.4:

DIMSE-C Service Group
---------------------

One DIMSE-C Service is used in the construction of SOP Classes of the
Substance Administration Query Service Class. The following DIMSE-C
operation is used.

-  C-FIND

.. _sect_V.4.1:

C-FIND Operation
~~~~~~~~~~~~~~~~

SCPs of SOP Classes of the Substance Administration Query Service Class
are capable of processing queries using the C-FIND operation as
described in . The C-FIND operation is the mechanism by which queries
are performed. Matches against the keys present in the Identifier are
returned in C-FIND responses.

.. _sect_V.4.1.1:

C-FIND Service Parameters
^^^^^^^^^^^^^^^^^^^^^^^^^

.. _sect_V.4.1.1.1:

SOP Class UID
'''''''''''''

The SOP Class UID identifies the Substance Administration Query
Information Model against which the C-FIND is to be performed. Support
for the SOP Class UID is implied by the Abstract Syntax UID of the
Presentation Context used by this C-FIND operation.

.. _sect_V.4.1.1.2:

Priority
''''''''

The Priority Attribute defines the requested priority of the C-FIND
operation with respect to other DIMSE operations being performed by the
same SCP.

Processing of priority requests is not required of SCPs. Whether or not
an SCP supports priority processing and the meaning of the different
priority levels shall be stated in the Conformance Statement of the SCP.

.. _sect_V.4.1.1.3:

Identifier
''''''''''

Both the C-FIND request and response contain an Identifier encoded as a
Data Set (see ).

.. _sect_V.4.1.1.3.1:

Request Identifier Structure
                            

An Identifier in a C-FIND request shall contain

-  Key Attributes values to be matched against the values of Attributes
   specified in that SOP Class.

-  Conditionally, the Attribute Specific Character Set (0008,0005). This
   Attribute shall be included if expanded or replacement character sets
   may be used in any of the Attributes in the Request Identifier. It
   shall not be included otherwise.

.. note::

   This means that Specific Character Set (0008,0005) is included if the
   SCU supports expanded or replacement character sets in the context of
   this service. It will not be included if expanded or replacement
   character sets are not supported by the SCU.

The Key Attributes and values allowable for the query shall be defined
in the SOP Class definition for the corresponding Substance
Administration Query Information Model.

.. _sect_V.4.1.1.3.2:

Response Identifier Structure
                             

The C-FIND response shall not contain Attributes that were not in the
request or specified in this section.

An Identifier in a C-FIND response shall contain:

-  Key Attributes with values corresponding to Key Attributes contained
   in the Identifier of the request (Key Attributes as defined in
   `Attribute Types <#sect_V.2.2.1>`__.)

-  Conditionally, the Attribute Specific Character Set (0008,0005). This
   Attribute shall be included if expanded or replacement character sets
   may be used in any of the Attributes in the Response Identifier. It
   shall not be included otherwise. The C-FIND SCP is not required to
   return responses in the Specific Character Set requested by the SCU
   if that character set is not supported by the SCP. The SCP may return
   responses with a different Specific Character Set.

.. note::

   This means that Specific Character Set (0008,0005) is included if the
   SCP supports expanded or replacement character sets in the context of
   this service. It will not be included if expanded or replacement
   character sets are not supported by the SCP.

-  Conditionally, the Attribute HL7 Structured Document Reference
   Sequence (0040,A390) and its subsidiary Sequence Items as specified
   in the SOP Common Module (see ). This Attribute shall be included if
   HL7 Structured Documents are referenced within the Identifier, e.g.,
   in the Pertinent Documents Sequence (0038,0100).

.. _sect_V.4.1.1.4:

Status
''''''

`table_title <#table_V.4-1>`__ defines the status code values that might
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
"Failed: Unable to process" Failure Meaning shall assign those causes
specific Status Code Values within valid range specified in
`table_title <#table_V.4-1>`__.

An SCU implementation shall recognize any Failure Status Code within the
value range specified in `table_title <#table_V.4-1>`__ as an indicator
of the Failure Meaning stated in the table. There is no requirement for
an SCU implementation to differentiate between specific Status Codes
within the valid range.

.. _sect_V.4.1.2:

C-FIND SCU Behavior
^^^^^^^^^^^^^^^^^^^

All C-FIND SCUs shall be capable of generating query requests that meet
the requirements of the Query Search Method (see `Query Search
Method <#sect_V.4.1.3.1>`__).

Required Keys and Optional Keys associated with the Query may be
contained in the Identifier.

An SCU conveys the following semantics using the C-FIND requests and
responses:

-  The SCU requests that the SCP perform a match of all keys specified
   in the Identifier of the request against the information it possesses
   of the Query specified in the request.

-  The SCU shall interpret Pending responses to convey the Attributes of
   a match of an item.

-  The SCU shall interpret a response with a status equal to Success,
   Failure, or Cancel to convey the end of Pending responses.

-  The SCU shall interpret a Failure response to a C-FIND request as an
   indication that the SCP is unable to process the request.

-  The SCU may cancel the C-FIND service by issuing a C-FIND-CANCEL
   request at any time during the processing of the C-FIND. The SCU
   shall recognize a status of Cancel to indicate that the C-FIND-CANCEL
   was successful.

.. _sect_V.4.1.3:

C-FIND SCP Behavior
^^^^^^^^^^^^^^^^^^^

All C-FIND SCPs shall be capable of processing queries that meet the
requirements of the Query Search (see `Query Search
Method <#sect_V.4.1.3.1>`__).

An SCP conveys the following semantics using the C-FIND requests and
responses:

-  The SCP is requested to perform a match of all the keys specified in
   the Identifier of the request, against the information it possesses.
   Attribute matching is performed using the key values specified in the
   Identifier of the C-FIND request as defined in `Substance
   Administration Query Information Model Definition <#sect_V.2>`__.

-  The SCP generates at most one C-FIND response for a match using the
   "Query" Search method. Such a response shall contain an Identifier
   whose Attributes contain values from the match. The response shall
   contain a status of Pending.

-  When matching is complete and any match has been sent, the SCP
   generates a C-FIND response that contains a status of Success. A
   status of Success shall indicate that a response has been sent for
   any match known to the SCP.

.. note::

   1. No Identifier is contained in a response with a status of Success.
      For a complete definition, see .

   2. When there are no matches, then no responses with a status of
      Pending are sent, only a single response with a status of Success.

-  The SCP shall generate a response with a status of Failure if it is
   unable to process the request. A Failure response shall contain no
   Identifier.

-  If the SCP receives a C-FIND-CANCEL indication before it has
   completed the processing of the matches it shall interrupt the
   matching process and return a status of Cancel.

.. _sect_V.4.1.3.1:

Query Search Method
'''''''''''''''''''

The following procedure is used to generate matches.

The key match Attributes contained in the Identifier of the C-FIND
request are matched against the values of the Key Attributes for each
Query entity. For each entity for which the Attributes match all of the
specified match Attributes, construct an Identifier. This Identifier
shall contain all of the values of the Attributes for this entity that
match those in the C-FIND request. Return a response for each such
Identifier. If there are no matching keys, then there are no matches;
return a response with a status equal to Success and with no Identifier.

.. _sect_V.5:

Association Negotiation
-----------------------

Association establishment is the first phase of any instance of
communication between peer DICOM AEs. The Association negotiation
procedure specified in shall be used to negotiate the supported SOP
Classes.

Support for the SCP/SCU Role Selection Negotiation is optional. The SOP
Class Extended Negotiation is not used by this Service Class.

.. _sect_V.6:

SOP Class Definitions
---------------------

.. _sect_V.6.1:

Product Characteristics Query SOP Class
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. _sect_V.6.1.1:

Product Characteristics Query SOP Class Overview
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Product Characteristics Query SOP Class defines an application-level
class of service that facilitates the communication of detailed
information about drugs, contrast agents, or devices identified by a bar
code or similar identifier. The detailed information is intended to be
used both for automated processing and for presentation to a system
operator.

The Product Characteristics Query SOP Class supports the following
example use cases:

-  Obtain the active ingredient, concentration, or other parameters of a
   contrast agent for inclusion in the image SOP Instances created
   during use of the agent, or for setting up image acquisition
   parameters (e.g., ultrasound transducer frequency)

-  Obtain the size parameters of a device (e.g., a catheter) for use in
   calibrating images that show that device

-  Obtain a network reference for an online copy of the "product label"
   (regulated prescribing and use data) for a drug, contrast agent, or
   device.

.. _sect_V.6.1.2:

Product Characteristics Query Information Model
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. _sect_V.6.1.2.1:

E/R Model
'''''''''

The Product Characteristics Query Information Model is represented by
the Entity Relationship diagram shown in figure `SOP Class
Definitions <#sect_V.6>`__ -1.

There is only one Information Entity in the model, which is the Product.
The Attributes of a Product can be found in the following Module in .

-  Product Characteristics Module

.. _sect_V.6.1.2.2:

Product Characteristics Query Attributes
''''''''''''''''''''''''''''''''''''''''

`table_title <#table_V.6-1>`__ defines the Attributes of the Product
Characteristics Query Information Model:

.. table:: Attributes for the Product Characteristics Query Information
Model

   +-------------+-------------+-------------+-------------+-------------+
   | Description | Tag         | Matching    | Return Key  | Rema        |
   | / Module    |             | Key Type    | Type        | rk/Matching |
   |             |             |             |             | Type        |
   +=============+=============+=============+=============+=============+
   | Product     | (0044,0001) | R           | 1           | Shall be    |
   | Package     |             |             |             | retrieved   |
   | Identifier  |             |             |             | with Single |
   |             |             |             |             | Value       |
   |             |             |             |             | Matching    |
   |             |             |             |             | only.       |
   +-------------+-------------+-------------+-------------+-------------+
   | Product     | (0044,0007) | -           | 1           |             |
   | Type Code   |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | *>Includ    |             |             |             |             |
   | e*\ `table_ |             |             |             |             |
   | title <#tab |             |             |             |             |
   | le_8-3a>`__ |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Product     | (0044,0008) | -           | 1           |             |
   | Name        |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Product     | (0044,000B) | -           | 2           |             |
   | Expiration  |             |             |             |             |
   | DateTime    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Product     | (0044,0013) | -           | 2           |             |
   | Parameter   |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Value Type | (0040,A040) | -           | 1           |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Concept    | (0040,A043) | -           | 1           |             |
   | Name Code   |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | *>>Includ   |             |             |             |             |
   | e*\ `table_ |             |             |             |             |
   | title <#tab |             |             |             |             |
   | le_8-3a>`__ |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | *>All other |             | -           | 1C          | Conditional |
   | Attributes  |             |             |             | on value of |
   | of the      |             |             |             | Value Type  |
   | Product     |             |             |             | (           |
   | Parameter   |             |             |             | 0040,A040); |
   | Sequence*   |             |             |             | See Content |
   |             |             |             |             | Item Macro. |
   +-------------+-------------+-------------+-------------+-------------+
   | *All other  |             | -           | 3           |             |
   | Attributes  |             |             |             |             |
   | of the*     |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+

The Product Package Identifier (0044,0001) might not be globally unique
and might conflict with other identifiers used within the scope of the
institution.

.. note::

   The package identifiers are typically unique within the scope of the
   substance administration management systems. This is a warning that
   they are not UIDs.

.. _sect_V.6.1.3:

Conformance Requirements
^^^^^^^^^^^^^^^^^^^^^^^^

An implementation may conform to the Product Characteristics Query SOP
Class as an SCU or an SCP. The Conformance Statement shall be in the
format defined in .

.. _sect_V.6.1.3.1:

SCU Conformance
'''''''''''''''

An implementation that conforms to the Product Characteristics Query SOP
Class shall support queries against the Information Model described in
`Product Characteristics Query Information Model <#sect_V.6.1.2>`__
using the baseline C-FIND SCU Behavior described in `C-FIND SCU
Behavior <#sect_V.4.1.2>`__.

An implementation that conforms to the Product Characteristics Query SOP
Class as an SCU shall state in its Conformance Statement the Return Key
Attributes it requests, and how those Attributes are used in the
application.

An implementation that conforms to the Product Characteristics Query SOP
Class as an SCU shall state in its Conformance Statement how it makes
use of Specific Character Set (0008,0005) when encoding queries and
interpreting responses.

.. _sect_V.6.1.3.2:

SCP Conformance
'''''''''''''''

An implementation that conforms to the Product Characteristics Query SOP
Class shall support queries against the Product Characteristics Query
Information Model described in `Product Characteristics Query
Information Model <#sect_V.6.1.2>`__ using the C-FIND SCP Behavior
described in `C-FIND SCP Behavior <#sect_V.4.1.3>`__.

An implementation that conforms to the Product Characteristics Query SOP
Class as an SCP shall state in its Conformance Statement the Return Key
Attributes that it supports.

An implementation that conforms to the Product Characteristics Query SOP
Class as an SCP shall state in its Conformance Statement how it makes
use of Specific Character Set (0008,0005) when encoding responses.

.. _sect_V.6.1.4:

SOP Class
^^^^^^^^^

The Product Characteristics Query SOP Class in the Substance
Administration Service Class identifies the Product Characteristics
Query Information Model, and the DIMSE-C operations supported. The
following Standard SOP Class is identified:

.. table:: Product Characteristics Query SOP Classes

   +--------------------------------------------+------------------------+
   | SOP Class Name                             | SOP Class UID          |
   +============================================+========================+
   | Product Characteristics Query Information  | 1.2.840.10008.5.1.4.41 |
   | Model - FIND                               |                        |
   +--------------------------------------------+------------------------+

.. _sect_V.6.2:

Substance Approval Query SOP Class
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. _sect_V.6.2.1:

Substance Approval Query SOP Class Overview
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Substance Approval Query SOP Class defines an application-level
class of service that allows a device at the point of care to obtain
verification of the appropriateness of contrast agents and other drugs
administered during a procedure, based on the substance label barcode
and the patient ID. The response is an authorization to proceed, or a
warning, or a contra-indication for presentation to the system operator.

The Substance Approval Query SOP Class supports the following example
use cases:

-  Obtain verification that administration of a specific drug or
   contrast agent for an image acquisition is appropriate for the
   patient

-  Obtain verification that the implantation of a specific device under
   imaging guidance is appropriate for the patient

The Substance Approval Query SOP Class does not specify the mechanism
used by the SCP to verify such appropriateness of administration (e.g.,
by comparison to allergy information in the patient's electronic health
record). The duration of validity of an approval beyond the time of the
response is not defined by the Standard.

.. _sect_V.6.2.2:

Substance Approval Query Information Model
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. _sect_V.6.2.2.1:

E/R Model
'''''''''

The Substance Approval Query Information Model is represented by the
Entity Relationship diagram shown in `figure_title <#figure_V.6-2>`__.

`figure_title <#figure_V.6-2>`__

The Attributes of the Information Entities can be found in the following
Modules in .

-  Patient Identification Module

-  Patient Demographics Module

-  Visit Identification Module

-  Substance Administration Module

-  Substance Approval Module

-  Product Characteristics Module

Only selected Attributes of these Modules are used in the Substance
Approval Query Information Model.

The Information Model is used in a bottom-up manner in the query; i.e.,
given a Product and a Patient, or alternatively a Product and a Visit,
for a proposed Substance Administration act at the current time, find
the Approval.

The Visit IE is included in the Information Model to support those
institutions that identify patients (e.g., on a bar coded wristband) by
Admission ID (i.e., the ID of the Visit), rather than Patient ID. This
allows automation of query construction using a scan of the Admission
ID. The Admission ID can be mapped to the Patient ID by the SCP for the
purpose of the performing the query matching.

.. note::

   1. The Visit is identified by the Admission ID (0038,0010) Attribute,
      but in the "Model of the Real World for the Purpose of Modality-IS
      Interface" (see ), the Visit is subsidiary to the Patient; hence
      the Admission ID may only be unique within the context of the
      patient, not within the context of the institution. The use of the
      Admission ID Attribute to identify the Visit (and hence the
      Patient) is only effective if the Admission ID is unique within
      the context of the institution.

   2. Certain institutions, e.g., ambulatory imaging centers that do not
      "admit" patients, may use the Imaging Service Request Identifier,
      or Accession Number, as an equivalent of the Admission ID. The SCU
      of this Query Service does not need to know the true origin or
      nature of the identifier, only that it is passed in the Query in
      the Admission ID (0038,0010) Attribute.

   3. There is conceptually a datetime of administration Attribute of
      the Substance Administration act, which is implicitly assumed to
      be approximately the time of the query in this SOP Class.

   4. There is conceptually a dose Attribute of the Product entity,
      which is the entire product identified by the bar code, and the
      request is for approval of administration of the entire product.

.. _sect_V.6.2.2.2:

Substance Approval Query Attributes
'''''''''''''''''''''''''''''''''''

`table_title <#table_V.6-2>`__ defines the Attributes of the Substance
Approval Query Information Model.

.. table:: Attributes for the Substance Approval Query Information Model

   +-------------+-------------+-------------+-------------+-------------+
   | Description | Tag         | Matching    | Return Key  | Rema        |
   | / Module    |             | Key Type    | Type        | rk/Matching |
   |             |             |             |             | Type        |
   +=============+=============+=============+=============+=============+
   | **Patient** |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Patient's   | (0010,0010) | O           | 2           |             |
   | Name        |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Patient ID  | (0010,0020) | R           | 1           | Shall be    |
   |             |             |             |             | retrieved   |
   |             |             |             |             | with Single |
   |             |             |             |             | Value       |
   |             |             |             |             | Matching    |
   |             |             |             |             | only.       |
   |             |             |             |             |             |
   |             |             |             |             | One or both |
   |             |             |             |             | of Patient  |
   |             |             |             |             | ID          |
   |             |             |             |             | (0010,0020) |
   |             |             |             |             | and         |
   |             |             |             |             | Admission   |
   |             |             |             |             | ID          |
   |             |             |             |             | (0038,0010) |
   |             |             |             |             | shall be    |
   |             |             |             |             | present as  |
   |             |             |             |             | a Matching  |
   |             |             |             |             | Key in the  |
   |             |             |             |             | Query       |
   +-------------+-------------+-------------+-------------+-------------+
   | Issuer of   | (0010,0021) | O           | 2           |             |
   | Patient ID  |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Issuer of   | (0010,0024) | O           | 3           |             |
   | Patient ID  |             |             |             |             |
   | Qualifiers  |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >All        |             | O           | 3           |             |
   | Attributes  |             |             |             |             |
   | of the      |             |             |             |             |
   | Issuer of   |             |             |             |             |
   | Patient ID  |             |             |             |             |
   | Qualifiers  |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Patient's   | (0010,0030) | -           | 2           |             |
   | Birth Date  |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Patient's   | (0010,0040) | -           | 2           |             |
   | Sex         |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | **Visit**   |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Admission   | (0038,0010) | R           | 2           | Shall be    |
   | ID          |             |             |             | retrieved   |
   |             |             |             |             | with Single |
   |             |             |             |             | Value       |
   |             |             |             |             | Matching    |
   |             |             |             |             | only.       |
   |             |             |             |             |             |
   |             |             |             |             | One or both |
   |             |             |             |             | of Patient  |
   |             |             |             |             | ID          |
   |             |             |             |             | (0010,0020) |
   |             |             |             |             | and         |
   |             |             |             |             | Admission   |
   |             |             |             |             | ID          |
   |             |             |             |             | (0038,0010) |
   |             |             |             |             | shall be    |
   |             |             |             |             | present as  |
   |             |             |             |             | a Matching  |
   |             |             |             |             | Key in the  |
   |             |             |             |             | Query       |
   +-------------+-------------+-------------+-------------+-------------+
   | Issuer of   | (0038,0014) | O           | 3           |             |
   | Admission   |             |             |             |             |
   | ID Sequence |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Local      | (0040,0031) | O           | 1C          | Required if |
   | Namespace   |             |             |             | Universal   |
   | Entity ID   |             |             |             | Entity ID   |
   |             |             |             |             | (0040,0032) |
   |             |             |             |             | is not      |
   |             |             |             |             | present;    |
   |             |             |             |             | may be      |
   |             |             |             |             | present     |
   |             |             |             |             | otherwise   |
   +-------------+-------------+-------------+-------------+-------------+
   | >Universal  | (0040,0032) | O           | 1C          | Required if |
   | Entity ID   |             |             |             | Local       |
   |             |             |             |             | Namespace   |
   |             |             |             |             | Entity ID   |
   |             |             |             |             | (0040,0031) |
   |             |             |             |             | is not      |
   |             |             |             |             | present;    |
   |             |             |             |             | may be      |
   |             |             |             |             | present     |
   |             |             |             |             | otherwise.  |
   +-------------+-------------+-------------+-------------+-------------+
   | >Universal  | (0040,0033) | O           | 1C          | Required if |
   | Entity ID   |             |             |             | Universal   |
   | Type        |             |             |             | Entity ID   |
   |             |             |             |             | (0040,0032) |
   |             |             |             |             | is present. |
   +-------------+-------------+-------------+-------------+-------------+
   | **Product** |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Product     | (0044,0001) | R           | 1           | Shall be    |
   | Package     |             |             |             | retrieved   |
   | Identifier  |             |             |             | with Single |
   |             |             |             |             | Value       |
   |             |             |             |             | Matching    |
   |             |             |             |             | only. Shall |
   |             |             |             |             | be present  |
   |             |             |             |             | as a        |
   |             |             |             |             | Matching    |
   |             |             |             |             | Key in the  |
   |             |             |             |             | Query.      |
   +-------------+-------------+-------------+-------------+-------------+
   | **Substance |             |             |             |             |
   | Admin       |             |             |             |             |
   | istration** |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Adm         | (0054,0302) | R           | 1           | Shall be    |
   | inistration |             |             |             | present as  |
   | Route Code  |             |             |             | a Matching  |
   | Sequence    |             |             |             | Key in the  |
   |             |             |             |             | Query.      |
   +-------------+-------------+-------------+-------------+-------------+
   | *>Includ    |             |             |             |             |
   | e*\ `table_ |             |             |             |             |
   | title <#tab |             |             |             |             |
   | le_8-1a>`__ |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | *           |             |             |             |             |
   | *Approval** |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Substance   | (0044,0002) | -           | 1           |             |
   | Adm         |             |             |             |             |
   | inistration |             |             |             |             |
   | Approval    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Approval    | (0044,0003) | -           | 2           |             |
   | Status      |             |             |             |             |
   | Further     |             |             |             |             |
   | Description |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Approval    | (0044,0004) | -           | 1           |             |
   | Status      |             |             |             |             |
   | DateTime    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+

One or both of Patient ID (0010,0020) and Admission ID (0038,0010) shall
be present as a Matching Key in the Query.

Product Package Identifier (0044,0001) shall be present as a Matching
Key in the Query. The Product Package Identifier might not be globally
unique and might conflict with other identifiers used within the scope
of the institution.

.. note::

   The package identifiers are typically unique within the scope of the
   substance administration management systems. This is a warning that
   they are not UIDs.

Administration Route Code Sequence (0054,0302) shall be present as a
Matching Key in the Query, and a single Item shall be present in that
Sequence with Code Value (0008,0100) and Coding Scheme Designator
(0008,0102) as Matching Keys.

.. _sect_V.6.2.2.3:

Substance Approval Query Responses
''''''''''''''''''''''''''''''''''

A Query response may have a status of Success or Failure (see
`Status <#sect_V.4.1.1.4>`__). A Failure Query response carries no
semantics about the existence or status of approval of the Substance
Administration.

A successful Query response will contain zero or one Pending response
items. The case of zero Pending responses carries the semantics of no
matching Approval Information Entity found, i.e., that the SCP cannot
determine an approval, rather than that the substance administration is
approved or disapproved. In this case a decision on substance
administration needs to be made by the healthcare provider.

.. note::

   Zero Pending responses may occur due do inability of the SCP to match
   the patient ID, product ID or route of administration.

In the case of one Pending response, the matching Approval Information
Entity will explicitly convey the Substance Administration Approval
(0044,0002) value of APPROVED, WARNING, or CONTRA_INDICATED.

.. _sect_V.6.2.3:

Conformance Requirements
^^^^^^^^^^^^^^^^^^^^^^^^

An implementation may conform to the Substance Approval Query SOP Class
as an SCU or an SCP. The Conformance Statement shall be in the format
defined in .

.. _sect_V.6.2.3.1:

SCU Conformance
'''''''''''''''

An implementation that conforms to the Substance Approval Query SOP
Class shall support queries against the Information Model described in
`Substance Approval Query Information Model <#sect_V.6.2.2>`__ using the
baseline C-FIND SCU Behavior described in `C-FIND SCU
Behavior <#sect_V.4.1.2>`__.

An implementation that conforms to the Substance Approval Query SOP
Class as an SCU shall state in its Conformance Statement how the Query
Attributes are used in the application, and how the application displays
the returned Attributes, in particular the values of Substance
Administration Approval (0044,0002) and Approval Status Further
Description (0044,0003). It shall state how it indicates a Query
response with zero Pending items, or a Failure status.

An implementation that conforms to the Substance Approval Query SOP
Class as an SCU shall state in its Conformance Statement how it makes
use of Specific Character Set (0008,0005) when encoding queries and
interpreting responses.

.. _sect_V.6.2.3.2:

SCP Conformance
'''''''''''''''

An implementation that conforms to the Substance Approval Query SOP
Class shall support queries against the Substance Approval Query
Information Model described in `Substance Approval Query Information
Model <#sect_V.6.2.2>`__ using the C-FIND SCP Behavior described in
`C-FIND SCP Behavior <#sect_V.4.1.3>`__. It shall support all of the
Attributes specified in the Information Model.

An implementation that conforms to the Substance Approval Query SOP
Class as an SCP shall state in its Conformance Statement how it
processes Required and Optional Matching Key Attributes. It shall state
how it obtains the values for the Return Key Attributes.

An implementation that conforms to the Substance Approval Query SOP
Class as an SCP shall state in its Conformance Statement how it makes
use of Specific Character Set (0008,0005) when interpreting queries,
performing matching and encoding responses.

.. _sect_V.6.2.4:

SOP Class
^^^^^^^^^

The Substance Approval Query SOP Class in the Substance Administration
Service Class identifies the Substance Approval Query Information Model,
and the DIMSE-C operations supported. The following Standard SOP Class
is identified:

.. table:: Substance Approval Query SOP Classes

   ================================================= ======================
   SOP Class Name                                    SOP Class UID
   ================================================= ======================
   Substance Approval Query Information Model - FIND 1.2.840.10008.5.1.4.42
   ================================================= ======================

