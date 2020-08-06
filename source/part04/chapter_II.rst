.. _chapter_II:

Protocol Approval Query/Retrieve Service Classes
================================================

.. _sect_II.1:

Overview
--------

.. _sect_II.1.1:

Scope
~~~~~

The Protocol Approval Query/Retrieve Service Classes define
application-level classes-of-service that facilitate access to Protocol
Approval composite objects.

.. _sect_II.1.2:

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

   Matching Keys are typically used in an SQL 'where' clause. Return
   Keys are typically used in an SQL 'select' clause to convey the
   Attribute Values.

Matching Key Attributes may be of Type "required" (R) or "optional" (O).
Return Key Attributes may be of Type 1, 1C, 2, 2C, 3 as defined in .

.. _sect_II.1.3:

Query/Retrieve Information Model
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In order to serve as an SCP of the Protocol Approval Query/Retrieve
Service Class, a DICOM AE possesses information about the Attributes of
a number of Protocol Approval composite SOP Instances. The information
is organized into an Information Model. The Information Models for the
different SOP Classes specified in this Annex are defined in `SOP Class
Definitions <#sect_II.6>`__.

.. _sect_II.1.4:

Service Definition
~~~~~~~~~~~~~~~~~~

Two peer DICOM AEs implement a SOP Class of a Protocol Approval
Query/Retrieve Service Class with one serving in the SCU role and one
serving in the SCP role. SOP Classes of the Protocol Approval
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

.. _sect_II.2:

Protocol Approval Information Models Definitions
------------------------------------------------

The Protocol Approval Information Models are identified by the SOP Class
negotiated at Association establishment time. Each SOP Class is composed
of both an Information Model and a DIMSE-C Service Group.

The Protocol Approval Information Models are defined in `SOP Class
Definitions <#sect_II.6>`__, with the Entity-Relationship Model
Definition and Key Attributes Definition analogous to those defined in
the Worklist Information Model Definition of the Basic Worklist
Management Service.

.. _sect_II.3:

Protocol Approval Information Models
------------------------------------

The Protocol Approval Information Models are based upon a one level
entity:

-  Protocol Approval object instance.

The Protocol Approval object instance contains Attributes associated
with the Approval IE of the Composite IODs as defined in .

.. _sect_II.4:

DIMSE-C Service Groups
----------------------

.. _sect_II.4.1:

C-FIND Operation
~~~~~~~~~~~~~~~~

See the C-FIND Operation definition for the Basic Worklist Management
Service Class (`C-FIND Operation <#sect_K.4.1>`__) , and substitute
"Approval" for "Worklist". The "Worklist" Search Method shall be used.

The SOP Class UID identifies the Protocol Approval Information Model
against which the C-FIND is to be performed. The Key Attributes and
values allowable for the query are defined in the SOP Class definitions
for the Protocol Approval Information Model.

.. _sect_II.4.1.1:

Service Class User Behavior
^^^^^^^^^^^^^^^^^^^^^^^^^^^

No SOP Class specific SCU behavior is defined.

.. _sect_II.4.1.2:

Service Class Provider Behavior
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

No SOP Class specific SCP behavior is defined.

.. _sect_II.4.2:

C-MOVE Operation
~~~~~~~~~~~~~~~~

See the C-MOVE Operation definition for the Query/Retrieve Service Class
(`C-MOVE Operation <#sect_C.4.2>`__). No Extended Behavior or
Relational-Retrieve is defined for the Protocol Approval Query/Retrieve
Service Classes.

Query/Retrieve Level (0008,0052) is not relevant to the Protocol
Approval Query/Retrieve Service Classes, and therefore shall not be
present in the Identifier. The only Unique Key Attribute of the
Identifier shall be SOP Instance UID (0008,0018). The SCU shall supply
one UID or a list of UIDs.

.. note::

   More than one entity may be retrieved, using List of UID matching.

.. _sect_II.4.3:

C-GET Operation
~~~~~~~~~~~~~~~

See the C-GET Operation definition for the Query/Retrieve Service Class
(`C-MOVE Operation <#sect_C.4.2>`__). No Extended Behavior or
Relational-Retrieve is defined for the Protocol Approval Query/Retrieve
Service Classes.

.. note::

   More than one entity may be retrieved, using List of UID matching.

.. _sect_II.5:

Association Negotiation
-----------------------

See the Association Negotiation definition for the Basic Worklist
Management Service Class (`Association Negotiation <#sect_K.5>`__).

.. _sect_II.6:

SOP Class Definitions
---------------------

.. _sect_II.6.1:

Protocol Approval Information Model
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. _sect_II.6.1.1:

E/R Models
^^^^^^^^^^

The Protocol Approval Information Model consists of a single entity. In
response to a given C-FIND request, the SCP shall send one C-FIND
response per matching Protocol Approval Instance.

.. _sect_II.6.1.2:

Protocol Approval Attributes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

`table_title <#table_II.6-1>`__ defines the Attributes of the Protocol
Approval Information Model.

.. note::

   Since protocol approvals are generally relevant only in the context
   of the protocol instance being approved, many searches will be
   looking for approvals that list a particular protocol instance in the
   Approval Subject Sequence (0044,0109).

.. table:: Attributes for the Protocol Approval Information Model

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
   | **Protocol  |             |             |             |             |
   | Approval**  |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Approval    | (0044,0109) | R           | 1           |             |
   | Subject     |             |             |             |             |
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
   | Approval    | (0044,0100) | R           | 1           |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Assertion  | (0044,0101) | R           | 1           |             |
   | Code        |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | *>>Includ   |             |             |             |             |
   | e*\ `table_ |             |             |             |             |
   | title <#tab |             |             |             |             |
   | le_8-1a>`__ |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Assertion  | (0044,0102) | -           | 1           |             |
   | UID         |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Asserter   | (0044,0103) | R           | 1           |             |
   | Ide         |             |             |             |             |
   | ntification |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Observer  | (0040,A084) | -           | 1           |             |
   | Type        |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Person    | (0040,A123) | R           | 1           |             |
   | Name        |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Person    | (0040,1101) | R           | 1           |             |
   | Ide         |             |             |             |             |
   | ntification |             |             |             |             |
   | Code        |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | *>>>Includ  |             |             |             |             |
   | e*\ `table_ |             |             |             |             |
   | title <#tab |             |             |             |             |
   | le_8-1a>`__ |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Org       | (0044,010A) | R           | 2           |             |
   | anizational |             |             |             |             |
   | Role Code   |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | *>>>Includ  |             |             |             |             |
   | e*\ `table_ |             |             |             |             |
   | title <#tab |             |             |             |             |
   | le_8-1a>`__ |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Station   | (0008,1010) | -           | 3           |             |
   | Name        |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Device    | (0018,1002) | -           | 3           |             |
   | UID         |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>M         | (0008,0070) | -           | 3           |             |
   | anufacturer |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Man       | (0008,1090) | -           | 3           |             |
   | ufacturer's |             |             |             |             |
   | Model Name  |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Station   | (0008,0055) | -           | 3           |             |
   | AE Title    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>          | (0008,0080) | R           | 1           |             |
   | Institution |             |             |             |             |
   | Name        |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>          | (0008,0082) | R           | 1           |             |
   | Institution |             |             |             |             |
   | Code        |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | *>>>Includ  |             |             |             |             |
   | e*\ `table_ |             |             |             |             |
   | title <#tab |             |             |             |             |
   | le_8-1a>`__ |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>In        | (0008,1040) | U           | 2           |             |
   | stitutional |             |             |             |             |
   | Department  |             |             |             |             |
   | Name        |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>In        | (0008,1041) | U           | 3           |             |
   | stitutional |             |             |             |             |
   | Department  |             |             |             |             |
   | Type Code   |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | *>>>Includ  |             |             |             |             |
   | e*\ `table_ |             |             |             |             |
   | title <#tab |             |             |             |             |
   | le_8-1a>`__ |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Assertion  | (0044,0104) | R           | 1           | This        |
   | DateTime    |             |             |             | Attribute   |
   |             |             |             |             | shall be    |
   |             |             |             |             | retrieved   |
   |             |             |             |             | with Single |
   |             |             |             |             | Value or    |
   |             |             |             |             | Range       |
   |             |             |             |             | Matching.   |
   +-------------+-------------+-------------+-------------+-------------+
   | >Assertion  | (0044,0105) | R           | 2           | This        |
   | Expiration  |             |             |             | Attribute   |
   | DateTime    |             |             |             | shall be    |
   |             |             |             |             | retrieved   |
   |             |             |             |             | with Single |
   |             |             |             |             | Value or    |
   |             |             |             |             | Range       |
   |             |             |             |             | Matching.   |
   +-------------+-------------+-------------+-------------+-------------+
   | >Assertion  | (0044,0106) | -           | 2           |             |
   | Comments    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Related    | (0044,0107) | U           | 1           |             |
   | Assertion   |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | (0044,0108) | U           | 1           |             |
   | >Referenced |             |             |             |             |
   | Assertion   |             |             |             |             |
   | UID         |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | **Enhanced  |             |             |             |             |
   | General     |             |             |             |             |
   | Equipment** |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | M           | (0008,0070) | -           | 1           |             |
   | anufacturer |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Man         | (0008,1090) | -           | 2           |             |
   | ufacturer's |             |             |             |             |
   | Model Name  |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Software    | (0018,1020) | -           | 2           |             |
   | Versions    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+

.. note::

   The Enhanced General Equipment Module describes the equipment that
   created the Protocol Approval instance, not the equipment on which a
   referenced Protocol will be performed.

.. _sect_II.6.1.3:

Conformance Requirements
^^^^^^^^^^^^^^^^^^^^^^^^

An implementation may conform to one or more of the Protocol Approval
Query/Retrieve SOP Classes as an SCU or SCP. The Conformance Statement
shall be in the format defined in .

.. _sect_II.6.1.3.1:

SCU Conformance
'''''''''''''''

.. _sect_II.6.1.3.1.1:

C-FIND SCU Conformance
                      

An implementation that conforms to the Protocol Approval Information
Model - FIND SOP Class shall support queries against the Protocol
Approval Information Model using the C-FIND SCU Behavior described for
the Basic Worklist Management Service Class (see `C-FIND SCU
Behavior <#sect_K.4.1.2>`__ and `C-FIND Operation <#sect_II.4.1>`__).

An implementation that conforms to the Protocol Approval Information
Model - FIND SOP Class as an SCU shall state in its Conformance
Statement whether it requests Type 3 Return Key Attributes, and shall
list these Optional Return Key Attributes.

An implementation that conforms to the Protocol Approval Information
Model - FIND SOP Class as an SCU shall state in its Conformance
Statement how it makes use of Specific Character Set (0008,0005) when
encoding queries and interpreting responses.

.. _sect_II.6.1.3.1.2:

C-MOVE SCU Conformance
                      

An implementation that conforms to the Protocol Approval Information
Model - MOVE SOP Class as an SCU shall support transfers against the
Protocol Approval Information Model, using the C-MOVE SCU baseline
behavior described for the Query/Retrieve Service Class (see `Baseline
Behavior of SCU <#sect_C.4.2.2.1>`__ and `C-MOVE
Operation <#sect_II.4.2>`__).

.. _sect_II.6.1.3.1.3:

C-GET SCU Conformance
                     

An implementation that conforms to the Protocol Approval Information
Model - GET SOP Class as an SCU shall support transfers against the
Protocol Approval Information Model, using the C-GET SCU baseline
behavior described for the Query/Retrieve Service Class (see `C-GET SCU
Behavior <#sect_C.4.3.2>`__).

.. _sect_II.6.1.3.2:

SCP Conformance
'''''''''''''''

.. _sect_II.6.1.3.2.1:

C-FIND SCP Conformance
                      

An implementation that conforms to the Protocol Approval Information
Model - FIND SOP Class as an SCP shall support queries against the
Protocol Approval Information Model, using the C-FIND SCP Behavior
described for the Basic Worklist Management Service Class (see `C-FIND
SCP Behavior <#sect_K.4.1.3>`__).

.. note::

   The contents of the Referenced SOP Instance UID (0008,1155) in the
   Approval Subject Sequence (0044,0109) would be useful to index since
   querying for approvals of a specific Protocol instance will be very
   common.

An implementation that conforms to the Protocol Approval Information
Model - FIND SOP Class as an SCP shall state in its Conformance
Statement:

-  whether it supports Type 3 Return Key Attributes, and shall list
   these Optional Return Key Attributes.

-  how it makes use of Specific Character Set (0008,0005) when
   interpreting queries, performing matching and encoding responses.

-  any behaviors that involve not returning matching instances (e.g. not
   returning an older approval instance that has been
   superceded/overridden by a newer approval instance).

.. _sect_II.6.1.3.2.2:

C-MOVE SCP Conformance
                      

An implementation that conforms to the Protocol Approval Information
Model - MOVE SOP Class as an SCP shall support transfers against the
Protocol Approval Information Model, using the C-MOVE SCP baseline
behavior described for the Query/Retrieve Service Class (see `Baseline
Behavior of SCP <#sect_C.4.2.3.1>`__).

An implementation that conforms to the Protocol Approval Information
Model - MOVE SOP Class as an SCP, which generates transfers using the
C-MOVE operation, shall state in its Conformance Statement appropriate
Storage Service Class, under which it shall support the C-STORE
sub-operations generated by the C-MOVE.

.. _sect_II.6.1.3.2.3:

C-GET SCP Conformance
                     

An implementation that conforms to the Protocol Approval Information
Model - GET SOP Class as an SCP shall support retrievals against the
Protocol Approval Information Model using the C-GET SCP baseline
behavior described for the Query/Retrieve Service Class in `C-GET SCP
Behavior <#sect_C.4.3.3>`__.

.. _sect_II.6.1.4:

SOP Classes
^^^^^^^^^^^

The SOP Classes of the Protocol Approval Query/Retrieve Service Class
identify the Information Models, and the DIMSE-C operations supported.

.. table:: Protocol Approval SOP Classes

   ========================================== =============================
   SOP Class Name                             SOP Class UID
   ========================================== =============================
   Protocol Approval Information Model - FIND 1.2.840.10008.5.1.4.1.1.200.4
   Protocol Approval Information Model - MOVE 1.2.840.10008.5.1.4.1.1.200.5
   Protocol Approval Information Model - GET  1.2.840.10008.5.1.4.1.1.200.6
   ========================================== =============================
