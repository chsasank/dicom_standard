.. _chapter_BB:

Implant Template Query/Retrieve Service Classes
===============================================

.. _sect_BB.1:

Overview
--------

.. _sect_BB.1.1:

Scope
~~~~~

The Implant Template Query/Retrieve Service Classes define
application-level classes-of-service that facilitate access to Implant
Template and Implant Assembly Template composite objects.

.. _sect_BB.1.2:

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

.. _sect_BB.1.3:

Query/Retrieve Information Model
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In order to serve as an SCP of the Implant Template Query/Retrieve
Service Class, a DICOM AE possesses information about the Attributes of
a number of Implant Template or Implant Assembly Template composite SOP
Instances. The information is organized into an Information Model. The
Information Models for the different SOP Classes specified in this Annex
are defined in `SOP Class Definitions <#sect_BB.6>`__.

.. _sect_BB.1.4:

Service Definition
~~~~~~~~~~~~~~~~~~

Two peer DICOM AEs implement a SOP Class of an Implant Template or
Implant Assembly Template Query/Retrieve Service Class with one serving
in the SCU role and one serving in the SCP role. SOP Classes of the
Implant Template and Implant Assembly Template Query/Retrieve Service
Classes are implemented using the DIMSE-C C-FIND, C-MOVE and C-GET
services as defined in .

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

.. _sect_BB.2:

Implant Template Information Models Definitions
-----------------------------------------------

The Implant Template, Implant Assembly Template, and Implant Template
Group Information Models are identified by the SOP Class negotiated at
Association establishment time. Each SOP Class is composed of both an
Information Model and a DIMSE-C Service Group.

The Implant Template, Implant Assembly Template, and Implant Template
Group Information Models are defined in `SOP Class
Definitions <#sect_BB.6>`__, with the Entity-Relationship Model
Definition and Key Attributes Definition analogous to those defined in
the Worklist Information Model Definition of the Basic Worklist
Management Service.

.. _sect_BB.3:

Implant Template Information Models
-----------------------------------

The Implant Template Information Models are based upon a one level
entity:

-  Implant Template object instance.

The Implant Template object instance contains Attributes associated with
the Implant Template object IE of the Composite IODs as defined in .

The Implant Assembly Template Information Model is based upon a one
level entity:

-  Implant Assembly Template object instance.

The Implant Assembly Template object instance contains Attributes
associated with the Implant Assembly Template object IE of the Composite
IODs as defined in .

The Implant Assembly Group Information Model is based upon a one level
entity:

-  Implant Template Group object instance.

The Implant Template Group object instance contains Attributes
associated with the Implant Template Group object IE of the Composite
IODs as defined in .

.. _sect_BB.4:

DIMSE-C Service Groups
----------------------

.. _sect_BB.4.1:

C-FIND Operation
~~~~~~~~~~~~~~~~

See the C-FIND Operation definition for the Basic Worklist Management
Service Class (K.4.1), and substitute "Implant Template" for "Worklist".
The "Worklist" Search Method shall be used.

The SOP Class UID identifies the Implant Template or Implant Assembly
Template, respectively Information Model against which the C-FIND is to
be performed. The Key Attributes and values allowable for the query are
defined in the SOP Class definitions for the Implant Template and
Implant Assembly Template Information Model.

.. _sect_BB.4.1.1:

Service Class User Behavior
^^^^^^^^^^^^^^^^^^^^^^^^^^^

When receiving several Implant Template Instances with the same Implant
Part Number, the receiving application shall use Effective DateTime
(0068,6226) to determine the appropriate Instance.

.. _sect_BB.4.1.2:

Service Class Provider Behavior
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

An SCP of this SOP Class shall support Level-2 conformance as defined in
`Conformance as an SCP <#sect_B.4.1>`__.

.. _sect_BB.4.2:

C-MOVE Operation
~~~~~~~~~~~~~~~~

See the C-MOVE Operation definition for the Query/Retrieve Service Class
(C.4.2). No Extended Behavior or Relational-Retrieve is defined for the
Implant Template and Implant Assembly Template Query/Retrieve Service
Classes.

Query/Retrieve Level (0008,0052) is not relevant to the Implant Template
and Implant Assembly Template Query/Retrieve Service Classes, and
therefore shall not be present in the Identifier. The only Unique Key
Attribute of the Identifier shall be SOP Instance UID (0008,0018). The
SCU shall supply one UID or a list of UIDs.

.. note::

   More than one entity may be retrieved, using List of UID matching.

.. _sect_BB.4.3:

C-GET Operation
~~~~~~~~~~~~~~~

See the C-GET Operation definition for the Query/Retrieve Service Class
(C.4.2). No Extended Behavior or Relational-Retrieve is defined for the
Implant Template and Implant Assembly Template Query/Retrieve Service
Classes.

.. note::

   More than one entity may be retrieved, using List of UID matching.

.. _sect_BB.5:

Association Negotiation
-----------------------

See the Association Negotiation definition for the Basic Worklist
Management Service Class (K.5).

.. _sect_BB.6:

SOP Class Definitions
---------------------

.. _sect_BB.6.1:

Implant Template Information Model
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. _sect_BB.6.1.1:

E/R Models
^^^^^^^^^^

The Implant Template Information Model consists of a single entity. In
response to a given C-FIND request, the SCP shall send one C-FIND
response per matching Implant Template Instance.

The Implant Assembly Template Information Model consists of a single
entity. In response to a given C-FIND request, the SCP shall send one
C-FIND response per matching Implant Assembly Template Instance.

The Implant Template Group Information Model consists of a single
entity. In response to a given C-FIND request, the SCP shall send one
C-FIND response per matching Implant Template Group Instance.

.. _sect_BB.6.1.2:

Implant Template Attributes
^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. _sect_BB.6.1.2.1:

Generic Implant Template Attributes
'''''''''''''''''''''''''''''''''''

`table_title <#table_BB.6-1>`__ defines the Attributes of the Generic
Implant Template Information Model:

.. table:: Attributes for the Implant Template Information Model

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
   | **Implant   |             |             |             |             |
   | Template**  |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | M           | (0008,0070) | R           | 1           | Shall be    |
   | anufacturer |             |             |             | retrieved   |
   |             |             |             |             | with Single |
   |             |             |             |             | Value, Wild |
   |             |             |             |             | Card, or    |
   |             |             |             |             | Universal   |
   |             |             |             |             | Matching.   |
   +-------------+-------------+-------------+-------------+-------------+
   | Implant     | (0022,1095) | R           | 1           | Shall be    |
   | Name        |             |             |             | retrieved   |
   |             |             |             |             | with Single |
   |             |             |             |             | Value, Wild |
   |             |             |             |             | Card, or    |
   |             |             |             |             | Universal   |
   |             |             |             |             | Matching.   |
   +-------------+-------------+-------------+-------------+-------------+
   | Implant     | (0068,6210) | R           | 2           | Shall be    |
   | Size        |             |             |             | retrieved   |
   |             |             |             |             | with Single |
   |             |             |             |             | Value, Wild |
   |             |             |             |             | Card, or    |
   |             |             |             |             | Universal   |
   |             |             |             |             | Matching.   |
   +-------------+-------------+-------------+-------------+-------------+
   | Implant     | (0022,1097) | R           | 1           | Shall be    |
   | Part Number |             |             |             | retrieved   |
   |             |             |             |             | with Single |
   |             |             |             |             | Value, Wild |
   |             |             |             |             | Card, or    |
   |             |             |             |             | Universal   |
   |             |             |             |             | Matching.   |
   +-------------+-------------+-------------+-------------+-------------+
   | Replaced    | (0068,6222) | R           | 2           | This        |
   | Implant     |             |             |             | Attribute   |
   | Template    |             |             |             | shall be    |
   | Sequence    |             |             |             | retrieved   |
   |             |             |             |             | with        |
   |             |             |             |             | Sequence or |
   |             |             |             |             | Universal   |
   |             |             |             |             | matching.   |
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
   | Derivation  | (0068,6224) | R           | 2           | This        |
   | Implant     |             |             |             | Attribute   |
   | Template    |             |             |             | shall be    |
   | Sequence    |             |             |             | retrieved   |
   |             |             |             |             | with        |
   |             |             |             |             | Sequence or |
   |             |             |             |             | Universal   |
   |             |             |             |             | matching.   |
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
   | Effective   | (0068,6226) | R           | 1           | Shall be    |
   | DateTime    |             |             |             | retrieved   |
   |             |             |             |             | with Single |
   |             |             |             |             | Value or    |
   |             |             |             |             | Range       |
   |             |             |             |             | Matching.   |
   +-------------+-------------+-------------+-------------+-------------+
   | Original    | (0068,6225) | R           | 2           | This        |
   | Implant     |             |             |             | Attribute   |
   | Template    |             |             |             | shall be    |
   | Sequence    |             |             |             | retrieved   |
   |             |             |             |             | with        |
   |             |             |             |             | Sequence or |
   |             |             |             |             | Universal   |
   |             |             |             |             | matching.   |
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
   | Implant     | (0068,6230) | R           | 2           | This        |
   | Target      |             |             |             | Attribute   |
   | Anatomy     |             |             |             | shall be    |
   | Sequence    |             |             |             | retrieved   |
   |             |             |             |             | with        |
   |             |             |             |             | Sequence or |
   |             |             |             |             | Universal   |
   |             |             |             |             | matching.   |
   +-------------+-------------+-------------+-------------+-------------+
   | >Anatomic   | (0008,2218) | R           | 1           | This        |
   | Region      |             |             |             | Attribute   |
   | Sequence    |             |             |             | shall be    |
   |             |             |             |             | retrieved   |
   |             |             |             |             | with Single |
   |             |             |             |             | Value or    |
   |             |             |             |             | Universal   |
   |             |             |             |             | matching.   |
   +-------------+-------------+-------------+-------------+-------------+
   | *>>Includ   |             |             |             |             |
   | e*\ `table_ |             |             |             |             |
   | title <#tab |             |             |             |             |
   | le_8-1a>`__ |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Implant     | (0068,62A0) | R           | 2           | This        |
   | Regulatory  |             |             |             | Attribute   |
   | Disapproval |             |             |             | shall be    |
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
   | Material    | (0068,63A0) | R           | 1           | This        |
   | Code        |             |             |             | Attribute   |
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
   | Coating     | (0068,63A4) | R           | 1           | This        |
   | Materials   |             |             |             | Attribute   |
   | Code        |             |             |             | shall be    |
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

.. _sect_BB.6.1.2.2:

Implant Assembly Template Attributes
''''''''''''''''''''''''''''''''''''

`table_title <#table_BB.6-2>`__ defines the Attributes of the Implant
Assembly Template Information Model:

.. table:: Attributes for the Implant Assembly Template Information
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
   | **Implant   |             |             |             |             |
   | Assembly    |             |             |             |             |
   | Template**  |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Implant     |             | R           | 1           | Shall be    |
   | Assembly    |             |             |             | retrieved   |
   | Template    |             |             |             | with Single |
   | Name        |             |             |             | Value, Wild |
   |             |             |             |             | Card, or    |
   |             |             |             |             | Universal   |
   |             |             |             |             | Matching.   |
   +-------------+-------------+-------------+-------------+-------------+
   | M           | (0008,0070) | R           | 1           | Shall be    |
   | anufacturer |             |             |             | retrieved   |
   |             |             |             |             | with Single |
   |             |             |             |             | Value, Wild |
   |             |             |             |             | Card, or    |
   |             |             |             |             | Universal   |
   |             |             |             |             | Matching.   |
   +-------------+-------------+-------------+-------------+-------------+
   | Procedure   | (0076,0020) | R           | 1           | This        |
   | Type Code   |             |             |             | Attribute   |
   | Sequence    |             |             |             | shall be    |
   |             |             |             |             | retrieved   |
   |             |             |             |             | with Single |
   |             |             |             |             | Value or    |
   |             |             |             |             | Universal   |
   |             |             |             |             | matching.   |
   +-------------+-------------+-------------+-------------+-------------+
   | *>Includ    |             |             |             |             |
   | e*\ `table_ |             |             |             |             |
   | title <#tab |             |             |             |             |
   | le_8-1a>`__ |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Replaced    | (0076,0008) | R           | 1           | Shall be    |
   | Implant     |             |             |             | retrieved   |
   | Assembly    |             |             |             | with        |
   | Template    |             |             |             | Sequence or |
   | Sequence    |             |             |             | Universal   |
   |             |             |             |             | Matching.   |
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
   | Original    | (0076,000C) | R           | 1           | Shall be    |
   | Implant     |             |             |             | retrieved   |
   | Assembly    |             |             |             | with        |
   | Template    |             |             |             | Sequence or |
   | Sequence    |             |             |             | Universal   |
   |             |             |             |             | Matching.   |
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
   | Derivation  | (0076,000E) | R           | 1           | Shall be    |
   | Implant     |             |             |             | retrieved   |
   | Assembly    |             |             |             | with        |
   | Template    |             |             |             | Sequence or |
   | Sequence    |             |             |             | Universal   |
   |             |             |             |             | Matching.   |
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
   | Surgical    | (0076,0030) | R           | 2           | Shall be    |
   | Technique   |             |             |             | retrieved   |
   |             |             |             |             | with Single |
   |             |             |             |             | Value, Wild |
   |             |             |             |             | Card, or    |
   |             |             |             |             | Universal   |
   |             |             |             |             | Matching.   |
   +-------------+-------------+-------------+-------------+-------------+

.. _sect_BB.6.1.2.3:

Implant Template Group Attributes
'''''''''''''''''''''''''''''''''

`table_title <#table_BB.6-3>`__ defines the Attributes of the Implant
Template Group Information Model:

.. table:: Attributes for the Implant Template Group Information Model

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
   | **Implant   |             |             |             |             |
   | Template    |             |             |             |             |
   | Group**     |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Implant     | (0078,0000) | R           | 1           | Shall be    |
   | Template    |             |             |             | retrieved   |
   | Group Name  |             |             |             | with Single |
   |             |             |             |             | Value, Wild |
   |             |             |             |             | Card, or    |
   |             |             |             |             | Universal   |
   |             |             |             |             | Matching.   |
   +-------------+-------------+-------------+-------------+-------------+
   | Implant     | (0078,0010) | -           | 2           |             |
   | Template    |             |             |             |             |
   | Group       |             |             |             |             |
   | Description |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Implant     | (0078,0020) | R           | 1           | Shall be    |
   | Template    |             |             |             | retrieved   |
   | Group       |             |             |             | with Single |
   | Issuer      |             |             |             | Value, Wild |
   |             |             |             |             | Card, or    |
   |             |             |             |             | Universal   |
   |             |             |             |             | Matching.   |
   +-------------+-------------+-------------+-------------+-------------+
   | Effective   | (0068,6226) | R           | 1           | Shall be    |
   | DateTime    |             |             |             | retrieved   |
   |             |             |             |             | with Single |
   |             |             |             |             | Value or    |
   |             |             |             |             | Range       |
   |             |             |             |             | Matching.   |
   +-------------+-------------+-------------+-------------+-------------+
   | Replaced    | (0078,0026) | R           | 2           | Shall be    |
   | Implant     |             |             |             | retrieved   |
   | Template    |             |             |             | with        |
   | Group       |             |             |             | Sequence or |
   | Sequence    |             |             |             | Universal   |
   |             |             |             |             | Matching    |
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

.. _sect_BB.6.1.3:

Conformance Requirements
^^^^^^^^^^^^^^^^^^^^^^^^

An implementation may conform to one of the Implant Template, Implant
Assembly Template, or Implant Template Group Information Model SOP
Classes as an SCU, SCP, any combination of two of these, or all three.
The Conformance Statement shall be in the format defined in .

.. _sect_BB.6.1.3.1:

SCU Conformance
'''''''''''''''

.. _sect_BB.6.1.3.1.1:

C-FIND SCU Conformance
                      

An implementation that conforms to one of the Implant Template, Implant
Assembly Template, or Implant Template Group Information Model SOP
Classes shall support queries against the appropriate Information Model
using the C-FIND SCU Behavior described for the Basic Worklist
Management Service Class (see `C-FIND SCU Behavior <#sect_K.4.1.2>`__
and `C-FIND Operation <#sect_BB.4.1>`__).

An implementation that conforms to one of the Implant Template, Implant
Assembly Template, or Implant Template Group Information Model SOP
Classes as an SCU shall state in its Conformance Statement whether it
requests Type 3 Return Key Attributes, and shall list these Optional
Return Key Attributes.

An implementation that conforms to one of the Implant Template, Implant
Assembly Template, or Implant Template Group Information Model SOP
Classes as an SCU shall state in its Conformance Statement how it makes
use of Specific Character Set (0008,0005) when encoding queries and
interpreting responses.

.. _sect_BB.6.1.3.1.2:

C-MOVE SCU Conformance
                      

An implementation that conforms to one of the Implant Template, Implant
Assembly Template, or Implant Template Group Information Model SOP
Classes as an SCU shall support transfers against the appropriate
Information Model, using the C-MOVE SCU baseline behavior described for
the Query/Retrieve Service Class (see `Baseline Behavior of
SCU <#sect_C.4.2.2.1>`__ and `C-MOVE Operation <#sect_BB.4.2>`__).

.. _sect_BB.6.1.3.1.3:

C-GET SCU Conformance
                     

An implementation that conforms to one of the Implant Template, Implant
Assembly Template, or Implant Template Group Information Model SOP
Classes as an SCU shall support transfers against the appropriate
Information Model, using the C-GET SCU baseline behavior described for
the Query/Retrieve Service Class (see `C-GET SCU
Behavior <#sect_C.4.3.2>`__).

.. _sect_BB.6.1.3.2:

SCP Conformance
'''''''''''''''

.. _sect_BB.6.1.3.2.1:

C-FIND SCP Conformance
                      

An implementation that conforms to one of the Implant Template, Implant
Assembly Template, or Implant Template Group Information Model SOP
Classes as an SCP shall support queries against the appropriate Template
Information Model, using the C-FIND SCP Behavior described for the Basic
Worklist Management Service Class (see `C-FIND SCP
Behavior <#sect_K.4.1.3>`__).

An implementation that conforms to one of the Implant Template, Implant
Assembly Template, or Implant Template Group Information Model SOP
Classes as an SCP shall state in its Conformance Statement whether it
supports Type 3 Return Key Attributes, and shall list these Optional
Return Key Attributes.

An implementation that conforms to one of the Implant Template, Implant
Assembly Template, or Implant Template Group Information Model SOP
Classes as an SCP shall state in its Conformance Statement how it makes
use of Specific Character Set (0008,0005) when interpreting queries,
performing matching and encoding responses.

.. _sect_BB.6.1.3.2.2:

C-MOVE SCP Conformance
                      

An implementation that conforms to one of the Implant Template, Implant
Assembly Template, or Implant Template Group Information Model SOP
Classes as an SCP shall support transfers against the appropriate
Information Model, using the C-MOVE SCP baseline behavior described for
the Query/Retrieve Service Class (see `Baseline Behavior of
SCP <#sect_C.4.2.3.1>`__).

An implementation that conforms to one of the Implant Template, Implant
Assembly Template, or Implant Template Group Information Model SOP
Classes as an SCP, which generates transfers using the C-MOVE operation,
shall state in its Conformance Statement appropriate Storage Service
Class, under which it shall support the C-STORE sub-operations generated
by the C-MOVE.

.. _sect_BB.6.1.3.2.3:

C-GET SCP Conformance
                     

An implementation that conforms to one of the SOP Classes of the Implant
Template, Implant Assembly Template, or Implant Template Group
Information Model SOP Class Group as an SCP shall support retrievals
against the Query/Retrieve Information Model described in `Patient Root
Query/Retrieve Information Model <#sect_C.6.1.1>`__ using the C-GET SCP
Behavior described in `C-GET SCP Behavior <#sect_C.4.3.3>`__.

.. _sect_BB.6.1.4:

SOP Classes
^^^^^^^^^^^

The SOP Classes of the Implant Template Information Models in the
Implant Template Query/Retrieve Service Class identify the Implant
Template Information Models, and the DIMSE-C operations supported. The
SOP Classes of the Implant Assembly Template Information Models in the
Implant Assembly Template Query/Retrieve Service Class identify the
Implant Assembly Template Information Models, and the DIMSE-C operations
supported. The SOP Classes of the Implant Template Group Information
Models in the Implant Template Group Query/Retrieve Service Class
identify the Implant Template Group Information Models, and the DIMSE-C
operations supported. The following Standard SOP Classes are identified:

.. table:: Implant Template SOP Classes

   +------------------------------------------+--------------------------+
   | SOP Class Name                           | SOP Class UID            |
   +==========================================+==========================+
   | Generic Implant Template Information     | 1.2.840.10008.5.1.4.43.2 |
   | Model - FIND                             |                          |
   +------------------------------------------+--------------------------+
   | Generic Implant Template Information     | 1.2.840.10008.5.1.4.43.3 |
   | Model - MOVE                             |                          |
   +------------------------------------------+--------------------------+
   | Generic Implant Template Information     | 1.2.840.10008.5.1.4.43.4 |
   | Model - GET                              |                          |
   +------------------------------------------+--------------------------+
   | Implant Assembly Template Information    | 1.2.840.10008.5.1.4.44.2 |
   | Model - FIND                             |                          |
   +------------------------------------------+--------------------------+
   | Implant Assembly Template Information    | 1.2.840.10008.5.1.4.44.3 |
   | Model - MOVE                             |                          |
   +------------------------------------------+--------------------------+
   | Implant Assembly Template Information    | 1.2.840.10008.5.1.4.44.4 |
   | Model - GET                              |                          |
   +------------------------------------------+--------------------------+
   | Implant Template Group Information Model | 1.2.840.10008.5.1.4.45.2 |
   | - FIND                                   |                          |
   +------------------------------------------+--------------------------+
   | Implant Template Group Information Model | 1.2.840.10008.5.1.4.45.3 |
   | - MOVE                                   |                          |
   +------------------------------------------+--------------------------+
   | Implant Template Group Information Model | 1.2.840.10008.5.1.4.45.4 |
   | - GET                                    |                          |
   +------------------------------------------+--------------------------+

