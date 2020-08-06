.. _chapter_Q:

Relevant Patient Information Query Service Class (Normative)
============================================================

.. _sect_Q.1:

Overview
--------

The Relevant Patient Information Query Service Class defines an
application-level class-of-service that facilitates the access to
relevant patient information such as it is known at the time of query.

The query information model consists of two entities with a one-to-one
relationship: the Patient and the Patient Information.

The Patient Information may be general, or specific to a particular
imaging or procedure domain. A general SOP Class is defined along with
some additional domain specific SOP Classes.

.. _sect_Q.2:

DIMSE-C Service Group
---------------------

One DIMSE-C Service is used in the construction of SOP Classes of the
Relevant Patient Information Query Service Class. The following DIMSE-C
operation is used.

-  C-FIND

.. _sect_Q.2.1:

C-FIND Operation
~~~~~~~~~~~~~~~~

SCPs of the Relevant Patient Information Query Service Class are capable
of processing queries using the C-FIND operation as described in . The
C-FIND operation is the mechanism by which queries are performed. The
SCP shall provide Relevant Patient Information for at most one matching
patient in the C-FIND response.

.. _sect_Q.2.1.1:

C-FIND Service Parameters
^^^^^^^^^^^^^^^^^^^^^^^^^

.. _sect_Q.2.1.1.1:

SOP Class UID
'''''''''''''

The SOP Class UID identifies the Relevant Patient Information Model and
Template against which the C-FIND is to be performed. Support for the
SOP Class UID is implied by the Abstract Syntax UID of the Presentation
Context used by this C-FIND operation.

.. _sect_Q.2.1.1.2:

Priority
''''''''

The Priority Attribute defines the requested priority of the C-FIND
operation with respect to other DIMSE operations being performed by the
same SCP.

Processing of priority requests is not required of SCPs. Whether or not
an SCP supports priority processing and the meaning of the different
priority levels shall be stated in the Conformance Statement of the SCP.

.. _sect_Q.2.1.1.3:

Identifier
''''''''''

Both the C-FIND request and response contain an Identifier encoded as a
Data Set (see ).

.. _sect_Q.2.1.1.3.1:

Request Identifier Structure
                            

An Identifier in a C-FIND request shall contain:

-  Key Attributes with values to be matched against the values of
   Attributes specified in the SOP Class.

-  Content Template Sequence (0040,A504), which shall include a single
   sequence item containing the Template Identifier (0040,DB00) and
   Mapping Resource (0008,0105) Attributes, to identify the template
   structure to use in the matching C-FIND responses.

-  Conditionally, the Attribute Specific Character Set (0008,0005). This
   Attribute shall be included if expanded or replacement character sets
   may be used in any of the Attributes in the Request Identifier. It
   shall not be included otherwise.

The Key Attributes and values allowable for the query are defined in the
SOP Class definition for the Relevant Patient Information Model.

.. _sect_Q.2.1.1.3.2:

Response Identifier Structure
                             

The C-FIND response shall not contain Attributes that were not in the
request or specified in this section.

An Identifier in a C-FIND response shall contain:

-  Key Attributes with values corresponding to Key Attributes contained
   in the Identifier of the request.

-  Content Template Sequence (0040,A504), which shall include a single
   sequence item containing the Template Identifier (0040,DB00) and
   Mapping Resource (0008,0105) Attributes, to identify the template
   structure used in the C-FIND response. The values shall be the same
   as specified in the Request Identifier.

-  Conditionally, the Attribute Specific Character Set (0008,0005). This
   Attribute shall be included if expanded or replacement character sets
   may be used in any of the Attributes in the Response Identifier. It
   shall not be included otherwise. The C-FIND SCP is not required to
   return responses in the Specific Character Set requested by the SCU
   if that character set is not supported by the SCP. The SCP may return
   responses with a different Specific Character Set.

.. _sect_Q.2.1.1.3.3:

Relevant Patient Information Templates
                                      

Templates used in the Relevant Patient Information query are defined in
.

The template specified in the Request Identifier shall not use
by-reference relationships.

.. _sect_Q.2.1.1.4:

Status
''''''

`table_title <#table_Q.2-1>`__ defines the status code values that might
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
   | Failed: Unable | C000           | (0000,0901)  |                |
   | to process     |                |              |                |
   |                |                | (0000,0902)  |                |
   +----------------+----------------+--------------+----------------+
   | Failed: More   | C100           | (0000,0901)  |                |
   | than one match |                |              |                |
   | found          |                | (0000,0902)  |                |
   +----------------+----------------+--------------+----------------+
   | Failed: Unable | C200           | (0000,0901)  |                |
   | to support     |                |              |                |
   | requested      |                | (0000,0902)  |                |
   | template       |                |              |                |
   +----------------+----------------+--------------+----------------+
   | Cancel         | Matching       | FE00         | None           |
   |                | terminated due |              |                |
   |                | to Cancel      |              |                |
   |                | request        |              |                |
   +----------------+----------------+--------------+----------------+
   | Success        | Success.       | 0000         | None           |
   |                | Matching is    |              |                |
   |                | complete - No  |              |                |
   |                | final          |              |                |
   |                | Identifier is  |              |                |
   |                | supplied.      |              |                |
   +----------------+----------------+--------------+----------------+
   | Pending        | Current Match  | FF00         | Identifier     |
   |                | is supplied.   |              |                |
   +----------------+----------------+--------------+----------------+

.. note::

   Status Codes are returned in DIMSE response messages (see ). The code
   values stated in column "Status Codes" are returned in Status Command
   Element (0000,0900).

.. _sect_Q.3:

Association Negotiation
-----------------------

Association establishment is the first phase of any instance of
communication between peer DICOM AEs. The Association negotiation
procedure specified in shall be used to negotiate the supported SOP
Class.

SOP Class Extended Negotiation is not defined for this Service Class.

.. _sect_Q.4:

DIMSE-C C-FIND Service
----------------------

The DIMSE-C C-FIND service is the operation by which relevant patient
information is queried and provided.

.. _sect_Q.4.1:

Conventions
~~~~~~~~~~~

Key Attributes in the Request Identifier serve two purposes. They may be
used as Matching Key Attributes and Return Key Attributes. Matching Key
Attributes may be used for matching (criteria to be used in the C-FIND
request to determine whether an entity matches the query). Return Key
Attributes may be used to specify desired return Attributes (what
elements in addition to the Matching Key Attributes have to be returned
in the C-FIND response).

Matching Key Attributes may be of Type "required" (R) or "optional" (O).
Return Key Attributes may be of Type 1, 1C, 2, 2C, 3 as defined in .

.. _sect_Q.4.2:

Service Definition
~~~~~~~~~~~~~~~~~~

Two peer DICOM AEs implement this Relevant Patient Information Query
Service Class with one serving in the SCU role and one serving in the
SCP role. The SOP Class is implemented using the DIMSE-C C-FIND service
as defined in .

Only a baseline behavior of the DIMSE-C C-FIND is used in this Service
Class.

A C-FIND service conveys the following semantics:

-  The SCU requests that the SCP perform a match for the Matching Keys
   and return values for the Return Keys that have been specified in the
   Identifier of the request, against the Relevant Patient Information
   that the SCP possesses.

   .. note::

      In this Annex, the term "Identifier" refers to the Identifier
      service parameter of the C-FIND service as defined in .

-  The SCP generates a C-FIND response for at most one match with an
   Identifier containing the values of all Matching Key Attributes and
   all known Return Key Attributes requested. The response contains one
   relevant patient information instance in the form that matches the
   Template that was requested. This response shall contain a status of
   Pending.

-  When the process of matching is complete, with zero or one match, a
   C-FIND response is sent with a status of Success and no Identifier.

-  A Failed response to a C-FIND request indicates that the SCP is
   unable to process the request. This shall be used to indicate that
   the requested template is not supported by the SCP, or that more than
   one match was found by the SCP.

-  The SCU may cancel the C-FIND service by issuing a C-FIND-CANCEL
   request at any time during the processing of the C-FIND service. The
   SCP will interrupt all matching and return a status of Canceled.

   .. note::

      The SCU needs to be prepared to receive C-FIND responses sent by
      the SCP until the SCP finally processes the C-FIND-CANCEL request.

.. _sect_Q.4.3:

Relevant Patient Information Model SOP Classes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. _sect_Q.4.3.1:

Relevant Patient Information Model
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In order to serve as a Service Class Provider (SCP) of one or more
Relevant Patient Information Model SOP Classes, a DICOM Application
Entity (AE) possesses relevant information about patients. This
information is organized into a Relevant Patient Information Model.

The SOP Classes are composed of both the Information Model and a DIMSE-C
Service Group.

.. _sect_Q.4.3.1.1:

E/R Model
'''''''''

The E/R Model consists of Patient and Structured Information, with no
relationship to other Information Entities in the DICOM Information
model.

The Patient IE includes the Attributes of the Patient Identification and
Patient Demographics Modules.

The Structured Information IE includes Attributes that are not
inherently related to a real-world entity, but are interpreted through
their coded content. This includes the Attributes of the Structured
Document Content Module, which in the case of the Relevant Patient
Information Query Service has its content constrained by specified
templates to convey patient related information. Also included in the
Structured Information IE are Attributes of the SOP Common and Common
Instance Reference Modules that support the interpretation of coded
data, or support access to referenced information objects identified in
the coded data.

.. _sect_Q.4.3.1.2:

Relevant Patient Information Attributes
'''''''''''''''''''''''''''''''''''''''

`table_title <#table_Q.4-1>`__ defines the Attributes of the Relevant
Patient Information Model:

.. table:: Attributes for the Relevant Patient Information Model

   +-------------+-------------+-------------+-------------+-------------+
   | Description | Tag         | Matching    | Return Key  | Remark /    |
   | / Module    |             | Key Type    | Type        | Matching    |
   |             |             |             |             | Type        |
   +=============+=============+=============+=============+=============+
   | **Patient** |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Patient's   | (0010,0010) | -           | 1           |             |
   | Name        |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Patient ID  | (0010,0020) | R           | 1           | Shall be    |
   |             |             |             |             | present in  |
   |             |             |             |             | the Request |
   |             |             |             |             | Identifier. |
   |             |             |             |             |             |
   |             |             |             |             | Shall be    |
   |             |             |             |             | retrieved   |
   |             |             |             |             | with Single |
   |             |             |             |             | Value       |
   |             |             |             |             | Matching.   |
   |             |             |             |             |             |
   |             |             |             |             | .. note::   |
   |             |             |             |             |             |
   |             |             |             |             |    Since    |
   |             |             |             |             |    only one |
   |             |             |             |             |    response |
   |             |             |             |             |    is       |
   |             |             |             |             |             |
   |             |             |             |             |   expected, |
   |             |             |             |             |    this is  |
   |             |             |             |             |    a unique |
   |             |             |             |             |    key.     |
   +-------------+-------------+-------------+-------------+-------------+
   | Issuer of   | (0010,0021) | R           | 2           | Shall be    |
   | Patient ID  |             |             |             | retrieved   |
   |             |             |             |             | with Single |
   |             |             |             |             | Value       |
   |             |             |             |             | Matching.   |
   |             |             |             |             |             |
   |             |             |             |             | In          |
   |             |             |             |             | situations  |
   |             |             |             |             | where there |
   |             |             |             |             | are         |
   |             |             |             |             | multiple    |
   |             |             |             |             | issuers,    |
   |             |             |             |             | this key    |
   |             |             |             |             | constrains  |
   |             |             |             |             | matching of |
   |             |             |             |             | Patient ID  |
   |             |             |             |             | (0010,0020) |
   |             |             |             |             | to a domain |
   |             |             |             |             | in which    |
   |             |             |             |             | the Patient |
   |             |             |             |             | ID          |
   |             |             |             |             | (0010,0020) |
   |             |             |             |             | is unique.  |
   +-------------+-------------+-------------+-------------+-------------+
   | Patient's   | (0010,0030) | -           | 2           |             |
   | Birth Date  |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Patient's   | (0010,0040) | -           | 2           |             |
   | Sex         |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | *All other  |             | -           | 3           |             |
   | Attributes  |             |             |             |             |
   | of the*     |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | *All other  |             | -           | 3           |             |
   | Attributes  |             |             |             |             |
   | of the*     |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | *           |             |             |             |             |
   | *Structured |             |             |             |             |
   | Information |             |             |             |             |
   | (SR         |             |             |             |             |
   | Document    |             |             |             |             |
   | Content     |             |             |             |             |
   | Module)**   |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Observation | (0040,A032) | -           | 1           |             |
   | DateTime    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Value Type  | (0040,A040) | -           | 1           | See         |
   |             |             |             |             | `Relevant   |
   |             |             |             |             | Patient     |
   |             |             |             |             | Information |
   |             |             |             |             | Attribute   |
   |             |             |             |             | Des         |
   |             |             |             |             | criptions < |
   |             |             |             |             | #sect_Q.4.3 |
   |             |             |             |             | .1.2.1>`__. |
   +-------------+-------------+-------------+-------------+-------------+
   | Concept     | (0040,A043) | -           | 1           | See         |
   | Name Code   |             |             |             | `Relevant   |
   | Sequence    |             |             |             | Patient     |
   |             |             |             |             | Information |
   |             |             |             |             | Attribute   |
   |             |             |             |             | Des         |
   |             |             |             |             | criptions < |
   |             |             |             |             | #sect_Q.4.3 |
   |             |             |             |             | .1.2.1>`__. |
   +-------------+-------------+-------------+-------------+-------------+
   | *>Includ    |             |             |             |             |
   | e*\ `table_ |             |             |             |             |
   | title <#tab |             |             |             |             |
   | le_8-3a>`__ |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Content     | (0040,A730) | -           | 2           | See         |
   | Sequence    |             |             |             | `Relevant   |
   |             |             |             |             | Patient     |
   |             |             |             |             | Information |
   |             |             |             |             | Attribute   |
   |             |             |             |             | Des         |
   |             |             |             |             | criptions < |
   |             |             |             |             | #sect_Q.4.3 |
   |             |             |             |             | .1.2.1>`__. |
   +-------------+-------------+-------------+-------------+-------------+
   | >All        |             | -           | -           | Content     |
   | Attributes  |             |             |             | Items as    |
   | of the      |             |             |             | provided by |
   | Content     |             |             |             | the SCP.    |
   | Sequence    |             |             |             | R           |
   |             |             |             |             | equirements |
   |             |             |             |             | on Content  |
   |             |             |             |             | Item        |
   |             |             |             |             | Attribute   |
   |             |             |             |             | Types shall |
   |             |             |             |             | be in       |
   |             |             |             |             | accordance  |
   |             |             |             |             | with the    |
   |             |             |             |             | definitions |
   |             |             |             |             | in the SR   |
   |             |             |             |             | Document    |
   |             |             |             |             | Content     |
   |             |             |             |             | Module.     |
   +-------------+-------------+-------------+-------------+-------------+
   | HL7         | (0040,A390) | -           | 1C          |             |
   | Structured  |             |             |             |             |
   | Document    |             |             |             |             |
   | Reference   |             |             |             |             |
   | Sequence    |             |             |             |             |
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
   | *           |             |             |             |             |
   | *Structured |             |             |             |             |
   | Information |             |             |             |             |
   | (Common     |             |             |             |             |
   | Instance    |             |             |             |             |
   | Reference   |             |             |             |             |
   | Module)**   |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Studies     | (0008,1200) | -           | 1C          | Required if |
   | Containing  |             |             |             | Content     |
   | Other       |             |             |             | Sequence    |
   | Referenced  |             |             |             | (0040,A390) |
   | Instances   |             |             |             | includes    |
   | Sequence    |             |             |             | Content     |
   |             |             |             |             | Items that  |
   |             |             |             |             | reference   |
   |             |             |             |             | SOP         |
   |             |             |             |             | Instances   |
   |             |             |             |             | that use    |
   |             |             |             |             | the         |
   |             |             |             |             | Patient     |
   |             |             |             |             | /Study/Seri |
   |             |             |             |             | es/Instance |
   |             |             |             |             | information |
   |             |             |             |             | model.      |
   +-------------+-------------+-------------+-------------+-------------+
   | >Referenced | (0008,1115) | -           | 1           |             |
   | Series      |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Series    | (0020,000E) | -           | 1           |             |
   | Instance    |             |             |             |             |
   | UID         |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | (0008,114A) | -           | 1           |             |
   | >Referenced |             |             |             |             |
   | Instance    |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>          | (0008,1150) | -           | 1           |             |
   | >Referenced |             |             |             |             |
   | SOP Class   |             |             |             |             |
   | UID         |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>          | (0008,1155) | -           | 1           |             |
   | >Referenced |             |             |             |             |
   | SOP         |             |             |             |             |
   | Instance    |             |             |             |             |
   | UID         |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+

The Attributes in `table_title <#table_Q.4-2>`__ are not part of the
Information Model; their inclusion in the C-FIND request and response
identifier are governed by rules in sections `Request Identifier
Structure <#sect_Q.2.1.1.3.1>`__ and `Response Identifier
Structure <#sect_Q.2.1.1.3.2>`__, respectively.

.. table:: Additional C-FIND Identifier Attributes

   +-------------+-------------+-------------+-------------+-------------+
   | Attribute   | Tag         | Type in     | Type in     | Remark      |
   | Name        |             | Request     | Response    |             |
   |             |             | Identifier  | Identifier  |             |
   +=============+=============+=============+=============+=============+
   | Content     | (0040,A504) | 1           | 1           |             |
   | Template    |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Mapping    | (0008,0105) | 1           | 1           |             |
   | Resource    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Template   | (0040,DB00) | 1           | 1           |             |
   | Identifier  |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Specific    | (0008,0005) | 1C          | 1C          | Required if |
   | Character   |             |             |             | expanded or |
   | Set         |             |             |             | replacement |
   |             |             |             |             | character   |
   |             |             |             |             | sets are    |
   |             |             |             |             | used. See   |
   |             |             |             |             | `Identifier |
   |             |             |             |             |  <#sect_Q.2 |
   |             |             |             |             | .1.1.3>`__, |
   +-------------+-------------+-------------+-------------+-------------+

.. _sect_Q.4.3.1.2.1:

Relevant Patient Information Attribute Descriptions
'''''''''''''''''''''''''''''''''''''''''''''''''''

Concept Name Code Sequence (0040,A043) in a C-FIND Response shall have
one sequence item that identifies the Root node concept of the returned
structure. This shall be the same as the Concept Name of the first row
of the template identified in the Content Template Sequence (0040,A504)
in the Identifier. The Concept Name Code Sequence (0040,A043) shall
always be sent zero length in the Request Identifier.

The Value Type (0040,A040) applies to the Concept Name Code Sequence
(0040,A043), and shall be the same as the Value Type (0040,A040) of the
first row of the template identified in the Content Template Sequence
(0040,A504) in the Identifier.

The Content Sequence (0040,A730) is a potentially recursively nested
Sequence of Items, as described in , SR Document Content Module. The
Content Sequence shall always be sent zero length in the Request
Identifier. The Content Sequence in the Data Set of the Response shall
contain the content items of the requested template.

.. _sect_Q.4.3.2:

Conformance Requirements
^^^^^^^^^^^^^^^^^^^^^^^^

An implementation may conform to the Relevant Patient Information Model
SOP Classes as an SCU and/or as an SCP.

The Conformance Statement shall be in the format defined in .

.. _sect_Q.4.3.2.1:

SCU Conformance
'''''''''''''''

An implementation that conforms to one or more of the Relevant Patient
Information Model SOP Classes shall support queries against the Relevant
Patient Information Model described in `Relevant Patient Information
Model <#sect_Q.4.3.1>`__ using the baseline C-FIND SCU Behavior
described in `Service Definition <#sect_Q.4.2>`__.

An implementation that conforms to one or more of the Relevant Patient
Information Model SOP Classes as an SCU shall state in its Conformance
Statement which SOP Class(es) it supports, and which Root template(s) it
may request in a query if not specified by the SOP Class. The
Conformance Statement shall also state the definition of any supported
template extensions.

.. _sect_Q.4.3.2.2:

SCP Conformance
'''''''''''''''

An implementation that conforms to one or more of the Relevant Patient
Information Model SOP Classes shall support queries against the Relevant
Patient Information Model described in `Relevant Patient Information
Model <#sect_Q.4.3.1>`__ using the baseline C-FIND SCP Behavior
described in `Service Definition <#sect_Q.4.2>`__.

An implementation that conforms to one or more of the Relevant Patient
Information Model SOP Classes as an SCP shall state in its Conformance
Statement which SOP Class(es) it supports, and which Root template(s) it
will support in a query response if not specified by the SOP Class. The
Conformance Statement shall also state the definition of any supported
template extensions.

An implementation that conforms to one or more of the Relevant Patient
Information Model SOP Classes as an SCP shall state in its Conformance
Statement how it makes use of Specific Character Set (0008,0005) when
interpreting queries, performing matching, and encoding responses.

.. _sect_Q.4.3.3:

SOP Classes
^^^^^^^^^^^

The Relevant Patient Information Model SOP Classes in the Relevant
Patient Information Query Service Class identify the Relevant Patient
Information Model, and the DIMSE-C operation supported. In some
instances a Root template is specified. The Standard SOP Classes are
defined in `table_title <#table_Q.4-3>`__:

.. table:: SOP Classes for the Relevant Patient Information Model

   +----------------------+----------------------+----------------------+
   | SOP Class Name       | SOP Class UID        | Root Template        |
   +======================+======================+======================+
   | General Relevant     | 1.2.                 | TID 9007 General     |
   | Patient Information  | 840.10008.5.1.4.37.1 | Relevant Patient     |
   | Query                |                      | Information, or from |
   |                      |                      | the list in          |
   +----------------------+----------------------+----------------------+
   | Breast Imaging       | 1.2.                 | TID 9000 Relevant    |
   | Relevant Patient     | 840.10008.5.1.4.37.2 | Patient Information  |
   | Information Query    |                      | for Breast Imaging   |
   +----------------------+----------------------+----------------------+
   | Cardiac Relevant     | 1.2.                 | TID 3802             |
   | Patient Information  | 840.10008.5.1.4.37.3 | Cardiovascular       |
   | Query                |                      | Patient History      |
   +----------------------+----------------------+----------------------+

.. note::

   The list of Root templates for the General Relevant Patient
   Information Query is extensible.

.. _sect_Q.5:

Relevant Patient Information Query Example (Informative)
--------------------------------------------------------

Moved to .

