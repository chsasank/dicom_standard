.. _chapter_HH:

Defined Procedure Protocol Query/Retrieve Service Classes
=========================================================

.. _sect_HH.1:

Overview
--------

.. _sect_HH.1.1:

Scope
~~~~~

The Defined Procedure Protocol Query/Retrieve Service Classes define
application-level classes-of-service that facilitate access to Defined
Procedure Protocol composite objects.

.. _sect_HH.1.2:

Conventions
~~~~~~~~~~~

Key Attributes serve two purposes; they may be used as Matching Key
Attributes or as Return Key Attributes. Matching Key Attributes may be
used for matching (criteria to be used in the C-FIND request to
determine whether an entity matches the query). Return Key Attributes
may be used to specify desired return Attributes (what elements in
addition to the Matching Key Attributes have to be returned in the
C-FIND response).

.. note::

   Matching Keys are typically used in an SQL 'WHERE' clause. Return
   Keys are typically used in an SQL 'SELECT' clause to convey the
   Attribute Values.

Matching Key Attributes may be of Type "required" (R) or "optional" (O).
Return Key Attributes may be of Type 1, 1C, 2, 2C, 3 as defined in .

.. _sect_HH.1.3:

Query/Retrieve Information Model
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In order to serve as an SCP of the Defined Procedure Protocol
Query/Retrieve Service Class, a DICOM AE possesses information about the
Attributes of a number of Defined Procedure Protocol composite SOP
Instances. The information is organized into an Information Model. The
Information Models for the different SOP Classes specified in this Annex
are defined in `SOP Class Definitions <#sect_HH.6>`__.

.. _sect_HH.1.4:

Service Definition
~~~~~~~~~~~~~~~~~~

Two peer DICOM AEs implement a SOP Class of a Defined Procedure Protocol
Query/Retrieve Service Class with one serving in the SCU role and one
serving in the SCP role. SOP Classes of the Defined Procedure Protocol
Query/Retrieve Service Classes are implemented using the DIMSE-C C-FIND,
C-MOVE and C-GET services as defined in .

An SCP of this SOP Class shall support Level-2 conformance as defined in
`Conformance as an SCP <#sect_B.4.1>`__.

The semantics of the C-FIND service are the same as those defined in the
Service Definition of the Basic Worklist Management Service Class.

The semantics of the C-MOVE service are the same as those defined in the
Service Definition of the Query/Retrieve Service Class, with the
exception that there is only one level of retrieval.

The semantics of the C-GET service are the same as those defined in the
Service Definition of the Query/Retrieve Service Class, with the
exception that there is only one level of retrieval.

.. _sect_HH.2:

Defined Procedure Protocol Information Models Definitions
---------------------------------------------------------

The Defined Procedure Protocol Information Models are identified by the
SOP Class negotiated at Association establishment time. Each SOP Class
is composed of both an Information Model and a DIMSE-C Service Group.

The Defined Procedure Protocol Information Models are defined in `SOP
Class Definitions <#sect_HH.6>`__, with the Entity-Relationship Model
Definition and Key Attributes Definition analogous to those defined in
the Worklist Information Model Definition of the Basic Worklist
Management Service.

.. _sect_HH.3:

Defined Procedure Protocol Information Models
---------------------------------------------

The Defined Procedure Protocol Information Models are based upon a one
level entity:

-  Defined Procedure Protocol object instance.

The Defined Procedure Protocol object instance contains Attributes
associated with the Procedure Protocol IE of the Composite IODs as
defined in .

.. _sect_HH.4:

DIMSE-C Service Groups
----------------------

.. _sect_HH.4.1:

C-FIND Operation
~~~~~~~~~~~~~~~~

See the C-FIND Operation definition for the `"Worklist" Search
Method <#sect_K.4.1.3.1>`__, and substitute "Defined Procedure Protocol"
for "Worklist". The "Worklist" Search Method shall be used.

The SOP Class UID identifies the Defined Procedure Protocol Information
Model against which the C-FIND is to be performed. The Key Attributes
and values allowable for the query are defined in the SOP Class
definitions for the Defined Procedure Protocol Information Model.

.. _sect_HH.4.1.1:

Service Class User Behavior
^^^^^^^^^^^^^^^^^^^^^^^^^^^

No SOP Class specific SCU behavior is defined.

.. _sect_HH.4.1.2:

Service Class Provider Behavior
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

No SOP Class specific SCP behavior is defined.

.. _sect_HH.4.2:

C-MOVE Operation
~~~~~~~~~~~~~~~~

See the C-MOVE Operation definition for the `C-MOVE
Operation <#sect_C.4.2>`__. No Extended Behavior or Relational-Retrieve
is defined for the Defined Procedure Protocol Query/Retrieve Service
Classes.

Query/Retrieve Level (0008,0052) is not relevant to the Defined
Procedure Protocol Query/Retrieve Service Classes, and therefore shall
not be present in the Identifier. The only Unique Key Attribute of the
Identifier shall be SOP Instance UID (0008,0018). The SCU shall supply
one UID or a list of UIDs.

.. note::

   More than one entity may be retrieved, using List of UID matching.

.. _sect_HH.4.3:

C-GET Operation
~~~~~~~~~~~~~~~

See the C-GET Operation definition for the `C-MOVE
Operation <#sect_C.4.2>`__. No Extended Behavior or Relational-Retrieve
is defined for the Defined Procedure Protocol Query/Retrieve Service
Classes.

.. note::

   More than one entity may be retrieved, using List of UID matching.

.. _sect_HH.5:

Association Negotiation
-----------------------

See the Association Negotiation definition for the `Association
Negotiation <#sect_K.5>`__.

.. _sect_HH.6:

SOP Class Definitions
---------------------

.. _sect_HH.6.1:

Defined Procedure Protocol Information Model
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. _sect_HH.6.1.1:

E/R Models
^^^^^^^^^^

The Defined Procedure Protocol Information Model consists of a single
entity. In response to a given C-FIND request, the SCP shall send one
C-FIND response per matching Defined Procedure Protocol Instance.

.. _sect_HH.6.1.2:

Defined Procedure Protocol Attributes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

`table_title <#table_HH.6-1>`__ defines the Attributes of the Defined
Procedure Protocol Information Model.

.. table:: Attributes for the Defined Procedure Protocol Information
Model

   +-------------+-------------+-------------+-------------+-------------+
   | Description | Tag         | Matching    | Return Key  | Remark /    |
   | / Module    |             | Key Type    | Type        | Matching    |
   |             |             |             |             | Type        |
   +=============+=============+=============+=============+=============+
   | **SOP       |             |             |             |             |
   | Common**    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Specific    | (0008,0005) | -           | 1C          | This        |
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
   |             |             |             |             | and `C-FIND |
   |             |             |             |             | Service     |
   |             |             |             |             | Paramete    |
   |             |             |             |             | rs <#sect_C |
   |             |             |             |             | .4.1.1>`__. |
   +-------------+-------------+-------------+-------------+-------------+
   | SOP Class   | (0008,0016) | R           | 1           |             |
   | UID         |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | SOP         | (0008,0018) | U           | 1           |             |
   | Instance    |             |             |             |             |
   | UID         |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | **Protocol  |             |             |             |             |
   | Context**   |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Custodial   | (0040,A07C) | R           | 2           |             |
   | O           |             |             |             |             |
   | rganization |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | (0008,0080) | R           | 2           |             |
   | Institution |             |             |             |             |
   | Name        |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | (0008,0082) | R           | 2           | This        |
   | Institution |             |             |             | Attribute   |
   | Code        |             |             |             | shall be    |
   | Sequence    |             |             |             | retrieved   |
   |             |             |             |             | with        |
   |             |             |             |             | Sequence or |
   |             |             |             |             | Universal   |
   |             |             |             |             | matching.   |
   +-------------+-------------+-------------+-------------+-------------+
   | *>>Includ   |             |             |             |             |
   | e*\ `table_ |             |             |             |             |
   | title <#tab |             |             |             |             |
   | le_8-1a>`__ |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Responsible | (0008,0220) | R           | 2           | This        |
   | Group Code  |             |             |             | Attribute   |
   | Sequence    |             |             |             | shall be    |
   |             |             |             |             | retrieved   |
   |             |             |             |             | with        |
   |             |             |             |             | Sequence or |
   |             |             |             |             | Universal   |
   |             |             |             |             | matching.   |
   +-------------+-------------+-------------+-------------+-------------+
   | *>Includ    |             |             |             |             |
   | e*\ `table_ |             |             |             |             |
   | title <#tab |             |             |             |             |
   | le_8-1a>`__ |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Protocol    | (0018,1030) | R           | 1           | Shall be    |
   | Name        |             |             |             | retrieved   |
   |             |             |             |             | with Single |
   |             |             |             |             | Value, Wild |
   |             |             |             |             | Card, or    |
   |             |             |             |             | Universal   |
   |             |             |             |             | Matching.   |
   +-------------+-------------+-------------+-------------+-------------+
   | Potential   | (0018,9906) | R           | 1           | This        |
   | Scheduled   |             |             |             | Attribute   |
   | Protocol    |             |             |             | shall be    |
   | Code        |             |             |             | retrieved   |
   | Sequence    |             |             |             | with        |
   |             |             |             |             | Sequence or |
   |             |             |             |             | Universal   |
   |             |             |             |             | matching.   |
   +-------------+-------------+-------------+-------------+-------------+
   | *>Includ    |             |             |             |             |
   | e*\ `table_ |             |             |             |             |
   | title <#tab |             |             |             |             |
   | le_8-1a>`__ |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Potential   | (0018,9907) | R           | 1           | This        |
   | Requested   |             |             |             | Attribute   |
   | Procedure   |             |             |             | shall be    |
   | Code        |             |             |             | retrieved   |
   | Sequence    |             |             |             | with        |
   |             |             |             |             | Sequence or |
   |             |             |             |             | Universal   |
   |             |             |             |             | matching.   |
   +-------------+-------------+-------------+-------------+-------------+
   | *>Includ    |             |             |             |             |
   | e*\ `table_ |             |             |             |             |
   | title <#tab |             |             |             |             |
   | le_8-1a>`__ |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Potential   | (0018,9908) | -           | 2           |             |
   | Reasons for |             |             |             |             |
   | Procedure   |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Potential   | (0018,9909) | R           | 2           | This        |
   | Reasons for |             |             |             | Attribute   |
   | Procedure   |             |             |             | shall be    |
   | Code        |             |             |             | retrieved   |
   | Sequence    |             |             |             | with        |
   |             |             |             |             | Sequence or |
   |             |             |             |             | Universal   |
   |             |             |             |             | matching.   |
   +-------------+-------------+-------------+-------------+-------------+
   | *>Includ    |             |             |             |             |
   | e*\ `table_ |             |             |             |             |
   | title <#tab |             |             |             |             |
   | le_8-1a>`__ |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Potential   | (0018,990A) | -           | 2           |             |
   | Diagnostic  |             |             |             |             |
   | Tasks       |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Predecessor | (0018,990E) | R           | 2           |             |
   | Protocol    |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Referenced | (0008,1150) | R           | 1           | Shall be    |
   | SOP Class   |             |             |             | retrieved   |
   | UID         |             |             |             | with List   |
   |             |             |             |             | of UID      |
   |             |             |             |             | Matching.   |
   +-------------+-------------+-------------+-------------+-------------+
   | >Referenced | (0008,1155) | R           | 1           | Shall be    |
   | SOP         |             |             |             | retrieved   |
   | Instance    |             |             |             | with List   |
   | UID         |             |             |             | of UID      |
   |             |             |             |             | Matching.   |
   +-------------+-------------+-------------+-------------+-------------+
   | Content     | (0070,0084) | R           | 1           | Shall be    |
   | Creator's   |             |             |             | retrieved   |
   | Name        |             |             |             | with Single |
   |             |             |             |             | Value, Wild |
   |             |             |             |             | Card, or    |
   |             |             |             |             | Universal   |
   |             |             |             |             | Matching.   |
   +-------------+-------------+-------------+-------------+-------------+
   | Instance    | (0008,0012) | R           | 1           | Shall be    |
   | Creation    |             |             |             | retrieved   |
   | Date        |             |             |             | with Single |
   |             |             |             |             | Value or    |
   |             |             |             |             | Range       |
   |             |             |             |             | Matching.   |
   |             |             |             |             |             |
   |             |             |             |             | See         |
   |             |             |             |             | Instance    |
   |             |             |             |             | Creation    |
   |             |             |             |             | Time for    |
   |             |             |             |             | further     |
   |             |             |             |             | details.    |
   +-------------+-------------+-------------+-------------+-------------+
   | Instance    | (0008,0013) | R           | 1           | Shall be    |
   | Creation    |             |             |             | retrieved   |
   | Time        |             |             |             | with Single |
   |             |             |             |             | Value or    |
   |             |             |             |             | Range       |
   |             |             |             |             | Matching.   |
   |             |             |             |             |             |
   |             |             |             |             | If both     |
   |             |             |             |             | Instance    |
   |             |             |             |             | Creation    |
   |             |             |             |             | Date and    |
   |             |             |             |             | Instance    |
   |             |             |             |             | Creation    |
   |             |             |             |             | Time are    |
   |             |             |             |             | specified   |
   |             |             |             |             | for Range   |
   |             |             |             |             | Matching,   |
   |             |             |             |             | they are to |
   |             |             |             |             | be treated  |
   |             |             |             |             | as as if    |
   |             |             |             |             | they were a |
   |             |             |             |             | single      |
   |             |             |             |             | DateTime    |
   |             |             |             |             | Attribute   |
   |             |             |             |             | e.g.,the    |
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
   +-------------+-------------+-------------+-------------+-------------+
   | **Clinical  |             |             |             |             |
   | Trial       |             |             |             |             |
   | Context**   |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Clinical    | (0012,0010) | R           | 1           | Shall be    |
   | Trial       |             |             |             | retrieved   |
   | Sponsor     |             |             |             | with Single |
   | Name        |             |             |             | Value, Wild |
   |             |             |             |             | Card, or    |
   |             |             |             |             | Universal   |
   |             |             |             |             | Matching.   |
   +-------------+-------------+-------------+-------------+-------------+
   | Clinical    | (0012,0020) | R           | 1           | Shall be    |
   | Trial       |             |             |             | retrieved   |
   | Protocol ID |             |             |             | with Single |
   |             |             |             |             | Value, Wild |
   |             |             |             |             | Card, or    |
   |             |             |             |             | Universal   |
   |             |             |             |             | Matching.   |
   +-------------+-------------+-------------+-------------+-------------+
   | **Equipment |             |             |             |             |
   | Spec        |             |             |             |             |
   | ification** |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Equipment   | (0008,0221) | R           | 1           |             |
   | Modality    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Model       | (0018,9912) | R           | 2           |             |
   | Sp          |             |             |             |             |
   | ecification |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >M          | (0008,0070) | R           | 1           | Shall be    |
   | anufacturer |             |             |             | retrieved   |
   |             |             |             |             | with Single |
   |             |             |             |             | Value, Wild |
   |             |             |             |             | Card, or    |
   |             |             |             |             | Universal   |
   |             |             |             |             | Matching.   |
   +-------------+-------------+-------------+-------------+-------------+
   | >Man        | (0008,0222) | R           | 2           | Shall be    |
   | ufacturer's |             |             |             | retrieved   |
   | Related     |             |             |             | with Single |
   | Model Group |             |             |             | Value, Wild |
   |             |             |             |             | Card, or    |
   |             |             |             |             | Universal   |
   |             |             |             |             | Matching.   |
   +-------------+-------------+-------------+-------------+-------------+
   | >Man        | (0008,1090) | R           | 2           | Shall be    |
   | ufacturer's |             |             |             | retrieved   |
   | Model Name  |             |             |             | with Single |
   |             |             |             |             | Value, Wild |
   |             |             |             |             | Card, or    |
   |             |             |             |             | Universal   |
   |             |             |             |             | Matching.   |
   +-------------+-------------+-------------+-------------+-------------+
   | >Software   | (0018,1020) | R           | 2           | Shall be    |
   | Versions    |             |             |             | retrieved   |
   |             |             |             |             | with Single |
   |             |             |             |             | Value, Wild |
   |             |             |             |             | Card, or    |
   |             |             |             |             | Universal   |
   |             |             |             |             | Matching.   |
   +-------------+-------------+-------------+-------------+-------------+
   | >Device     | (0018,1000) | -           | 2           |             |
   | Serial      |             |             |             |             |
   | Number      |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | **Patient   |             |             |             |             |
   | Po          |             |             |             |             |
   | sitioning** |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Anatomic    | (0008,2218) | R           | 2           | This        |
   | Region      |             |             |             | Attribute   |
   | Sequence    |             |             |             | shall be    |
   |             |             |             |             | retrieved   |
   |             |             |             |             | with        |
   |             |             |             |             | Sequence or |
   |             |             |             |             | Universal   |
   |             |             |             |             | matching.   |
   +-------------+-------------+-------------+-------------+-------------+
   | *>Includ    |             |             |             |             |
   | e*\ `table_ |             |             |             |             |
   | title <#tab |             |             |             |             |
   | le_8-1a>`__ |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Primary     | (0008,2228) | R           | 2           | This        |
   | Anatomic    |             |             |             | Attribute   |
   | Structure   |             |             |             | shall be    |
   | Sequence    |             |             |             | retrieved   |
   |             |             |             |             | with        |
   |             |             |             |             | Sequence or |
   |             |             |             |             | Universal   |
   |             |             |             |             | matching.   |
   +-------------+-------------+-------------+-------------+-------------+
   | *>Includ    |             |             |             |             |
   | e*\ `table_ |             |             |             |             |
   | title <#tab |             |             |             |             |
   | le_8-1a>`__ |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+

.. _sect_HH.6.1.3:

Conformance Requirements
^^^^^^^^^^^^^^^^^^^^^^^^

An implementation may conform to one or more of the Defined Procedure
Protocol Query/Retrieve SOP Classes as an SCU or SCP. The Conformance
Statement shall be in the format defined in .

.. _sect_HH.6.1.3.1:

SCU Conformance
'''''''''''''''

.. _sect_HH.6.1.3.1.1:

C-FIND SCU Conformance
                      

An implementation that conforms to the Defined Procedure Protocol
Information Model - FIND SOP Class shall support queries against the
Defined Procedure Protocol Information Model using the C-FIND SCU
Behavior described for the Basic Worklist Management Service Class (see
`C-FIND SCU Behavior <#sect_K.4.1.2>`__ and `C-FIND
Operation <#sect_HH.4.1>`__).

An implementation that conforms to the Defined Procedure Protocol
Information Model - FIND SOP Class as an SCU shall state in its
Conformance Statement whether it requests Type 3 Return Key Attributes,
and shall list these Optional Return Key Attributes.

An implementation that conforms to the Defined Procedure Protocol
Information Model - FIND SOP Class as an SCU shall state in its
Conformance Statement how it makes use of Specific Character Set
(0008,0005) when encoding queries and interpreting responses.

.. _sect_HH.6.1.3.1.2:

C-MOVE SCU Conformance
                      

An implementation that conforms to the Defined Procedure Protocol
Information Model - MOVE SOP Class as an SCU shall support transfers
against the Defined Procedure Protocol Information Model, using the
C-MOVE SCU baseline behavior described for the Query/Retrieve Service
Class (see `Baseline Behavior of SCU <#sect_C.4.2.2.1>`__ and `C-MOVE
Operation <#sect_HH.4.2>`__).

.. _sect_HH.6.1.3.1.3:

C-GET SCU Conformance
                     

An implementation that conforms to the Defined Procedure Protocol
Information Model - GET SOP Class as an SCU shall support transfers
against the Defined Procedure Protocol Information Model, using the
C-GET SCU baseline behavior described for the Query/Retrieve Service
Class (see `C-GET SCU Behavior <#sect_C.4.3.2>`__).

.. _sect_HH.6.1.3.2:

SCP Conformance
'''''''''''''''

.. _sect_HH.6.1.3.2.1:

C-FIND SCP Conformance
                      

An implementation that conforms to the Defined Procedure Protocol
Information Model - FIND SOP Class as an SCP shall support queries
against the Defined Procedure Protocol Information Model, using the
C-FIND SCP Behavior described for the Basic Worklist Management Service
Class (see `C-FIND SCP Behavior <#sect_K.4.1.3>`__).

.. note::

   The contents of the Model Specification Sequence (0018,9912) would be
   useful to index for systems that support query or selection of
   appropriate Protocols for specific systems.

An implementation that conforms to the Defined Procedure Protocol
Information Model - FIND SOP Class as an SCP shall state in its
Conformance Statement whether it supports Type 3 Return Key Attributes,
and shall list these Optional Return Key Attributes.

An implementation that conforms to the Defined Procedure Protocol
Information Model - FIND SOP Class as an SCP shall state in its
Conformance Statement how it makes use of Specific Character Set
(0008,0005) when interpreting queries, performing matching and encoding
responses.

.. _sect_HH.6.1.3.2.2:

C-MOVE SCP Conformance
                      

An implementation that conforms to the Defined Procedure Protocol
Information Model - MOVE SOP Class as an SCP shall support transfers
against the Defined Procedure Protocol Information Model, using the
C-MOVE SCP baseline behavior described for the Query/Retrieve Service
Class (see `Baseline Behavior of SCP <#sect_C.4.2.3.1>`__).

.. note::

   It is expected that a device that does not match the contents of the
   Model Specification Sequence (0018,9912) will not execute the
   Protocol.

An implementation that conforms to the Defined Procedure Protocol
Information Model - MOVE SOP Class as an SCP, which generates transfers
using the C-MOVE operation, shall state in its Conformance Statement
appropriate Storage Service Class, under which it shall support the
C-STORE sub-operations generated by the C-MOVE.

.. _sect_HH.6.1.3.2.3:

C-GET SCP Conformance
                     

An implementation that conforms to the Defined Procedure Protocol
Information Model - GET SOP Class as an SCP shall support retrievals
against the Defined Procedure Protocol Information Model using the C-GET
SCP baseline behavior described for the Query/Retrieve Service Class in
`C-GET SCP Behavior <#sect_C.4.3.3>`__.

.. _sect_HH.6.1.4:

SOP Classes
^^^^^^^^^^^

The SOP Classes of the Defined Procedure Protocol Query/Retrieve Service
Class identify the Information Models, and the DIMSE-C operations
supported.

.. table:: Defined Procedure Protocol SOP Classes

   +------------------------------------------+--------------------------+
   | SOP Class Name                           | SOP Class UID            |
   +==========================================+==========================+
   | Defined Procedure Protocol Information   | 1.2.840.10008.5.1.4.20.1 |
   | Model - FIND                             |                          |
   +------------------------------------------+--------------------------+
   | Defined Procedure Protocol Information   | 1.2.840.10008.5.1.4.20.2 |
   | Model - MOVE                             |                          |
   +------------------------------------------+--------------------------+
   | Defined Procedure Protocol Information   | 1.2.840.10008.5.1.4.20.3 |
   | Model - GET                              |                          |
   +------------------------------------------+--------------------------+

