.. _chapter_U:

Hanging Protocol Query/Retrieve Service Class
=============================================

.. _sect_U.1:

Overview
--------

.. _sect_U.1.1:

Scope
~~~~~

The Hanging Protocol Query/Retrieve Service Class defines an
application-level class-of-service that facilitates access to Hanging
Protocol composite objects. It provides query and retrieve/transfer
capabilities similar to the Basic Worklist Management Service Class and
Query/Retrieve Service Class.

.. _sect_U.1.2:

Conventions
~~~~~~~~~~~

See Conventions for the Basic Worklist Management Service (K.1.2).

.. _sect_U.1.3:

Query/Retrieve Information Model
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In order to serve as an SCP of the Hanging Protocol Query/Retrieve
Service Class, a DICOM AE possesses information about the Attributes of
a number of Hanging Protocol composite SOP Instances. The information is
organized into a Hanging Protocol Information Model.

.. _sect_U.1.4:

Service Definition
~~~~~~~~~~~~~~~~~~

Two peer DICOM AEs implement a SOP Class of the Hanging Protocol
Query/Retrieve Service Class with one serving in the SCU role and one
serving in the SCP role. SOP Classes of the Hanging Protocol
Query/Retrieve Service Class are implemented using the DIMSE-C C-FIND,
C-MOVE and C-GET services as defined in .

The semantics of the C-FIND and C-GET services are the same as those
defined in the Service Definition of the Basic Worklist Management
Service Class.

The semantics of the C-MOVE service are the same as those defined in the
Service Definition of the Query/Retrieve Service Class, with the
exception that there is only one level of retrieval.

.. _sect_U.2:

Hanging Protocol Information Model Definition
---------------------------------------------

The Hanging Protocol Information Model is identified by the SOP Class
negotiated at Association establishment time. The SOP Class is composed
of both an Information Model and a DIMSE-C Service Group.

The Hanging Protocol Information Model is defined, with the
Entity-Relationship Model Definition and Key Attributes Definition
analogous to those defined in the Worklist Information Model Definition
of the Basic Worklist Management Service.

.. _sect_U.3:

Hanging Protocol Information Model
----------------------------------

The Hanging Protocol Information Model is based upon a one level entity:

-  Hanging Protocol object instance

The Hanging Protocol object instance contains Attributes associated with
the Hanging Protocol object IE of the Composite IODs as defined in .

.. _sect_U.4:

DIMSE-C Service Groups
----------------------

.. _sect_U.4.1:

C-FIND Operation
~~~~~~~~~~~~~~~~

See the C-FIND Operation definition for the Basic Worklist Management
Service Class (K.4.1), and substitute "Hanging Protocol" for "Worklist.
The "Worklist" Search Method shall be used.

The SOP Class UID identifies the Hanging Protocol Information Model
against which the C-FIND is to be performed. The Key Attributes and
values allowable for the query are defined in the SOP Class definition
for the Hanging Protocol Information Model.

.. _sect_U.4.2:

C-MOVE Operation
~~~~~~~~~~~~~~~~

See the C-MOVE Operation definition for the Query/Retrieve Service Class
(C.4.2). No Extended Behavior or Relational-Retrieve is defined for the
Hanging Protocol Query/Retrieve Service Class.

Query/Retrieve Level (0008,0052) is not relevant to the Hanging Protocol
Query/Retrieve Service Class, and therefore shall not be present in the
Identifier. The only Unique Key Attribute of the Identifier shall be SOP
Instance UID (0008,0018). The SCU shall supply one UID or a list of
UIDs.

.. note::

   More than one entity may be retrieved, using List of UID matching.

.. _sect_U.4.3:

C-GET Operation
~~~~~~~~~~~~~~~

See the C-GET Operation definition for the Query/Retrieve Service Class
(C.4.3). No Extended Behavior or Relational-Retrieve is defined for the
Hanging Protocol Query/Retrieve Service Class.

Query/Retrieve Level (0008,0052) is not relevant to the Hanging Protocol
Query/Retrieve Service Class, and therefore shall not be present in the
Identifier. The only Unique Key Attribute of the Identifier shall be SOP
Instance UID (0008,0018). The SCU shall supply one UID or a list of
UIDs.

.. note::

   More than one entity may be retrieved, using List of UID matching.

.. _sect_U.5:

Association Negotiation
-----------------------

See the Association Negotiation definition for the Basic Worklist
Management Service Class (K.5).

.. _sect_U.6:

SOP Class Definitions
---------------------

.. _sect_U.6.1:

Hanging Protocol Information Model
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. _sect_U.6.1.1:

E/R Model
^^^^^^^^^

The Hanging Protocol Information Model consists of a single entity. In
response to a given C-FIND request, the SCP shall send one C-FIND
response per matching Hanging Protocol Instance.

.. _sect_U.6.1.2:

Hanging Protocol Attributes
^^^^^^^^^^^^^^^^^^^^^^^^^^^

`table_title <#table_U.6-1>`__ defines the Attributes of the Hanging
Protocol Information Model:

.. table:: Attributes for the Hanging Protocol Information Model

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
   | **Hanging   |             |             |             |             |
   | Protocol    |             |             |             |             |
   | D           |             |             |             |             |
   | efinition** |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Hanging     | (0072,0002) | R           | 1           | This        |
   | Protocol    |             |             |             | Attribute   |
   | Name        |             |             |             | shall be    |
   |             |             |             |             | retrieved   |
   |             |             |             |             | with Single |
   |             |             |             |             | Value, Wild |
   |             |             |             |             | Card or     |
   |             |             |             |             | Universal   |
   |             |             |             |             | matching.   |
   +-------------+-------------+-------------+-------------+-------------+
   | Hanging     | (0072,0004) | -           | 1           |             |
   | Protocol    |             |             |             |             |
   | Description |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Hanging     | (0072,0006) | R           | 1           | This        |
   | Protocol    |             |             |             | Attribute   |
   | Level       |             |             |             | shall be    |
   |             |             |             |             | retrieved   |
   |             |             |             |             | with Single |
   |             |             |             |             | Value or    |
   |             |             |             |             | Universal   |
   |             |             |             |             | matching.   |
   +-------------+-------------+-------------+-------------+-------------+
   | Hanging     | (0072,0008) | -           | 1           |             |
   | Protocol    |             |             |             |             |
   | Creator     |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Hanging     | (0072,000A) | -           | 1           |             |
   | Protocol    |             |             |             |             |
   | Creation    |             |             |             |             |
   | DateTime    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Hanging     | (0072,000C) | R           | 1           | This        |
   | Protocol    |             |             |             | Attribute   |
   | Definition  |             |             |             | shall be    |
   | Sequence    |             |             |             | retrieved   |
   |             |             |             |             | with        |
   |             |             |             |             | Sequence or |
   |             |             |             |             | Universal   |
   |             |             |             |             | matching.   |
   +-------------+-------------+-------------+-------------+-------------+
   | >Modality   | (0008,0060) | R           | 2           | This        |
   |             |             |             |             | Attribute   |
   |             |             |             |             | shall be    |
   |             |             |             |             | retrieved   |
   |             |             |             |             | with Single |
   |             |             |             |             | Value or    |
   |             |             |             |             | Universal   |
   |             |             |             |             | matching.   |
   +-------------+-------------+-------------+-------------+-------------+
   | >Anatomic   | (0008,2218) | R           | 2           | This        |
   | Region      |             |             |             | Attribute   |
   | Sequence    |             |             |             | shall be    |
   |             |             |             |             | retrieved   |
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
   | >Laterality | (0020,0060) | R           | 2           | This        |
   |             |             |             |             | Attribute   |
   |             |             |             |             | shall be    |
   |             |             |             |             | retrieved   |
   |             |             |             |             | with Single |
   |             |             |             |             | Value or    |
   |             |             |             |             | Universal   |
   |             |             |             |             | matching.   |
   +-------------+-------------+-------------+-------------+-------------+
   | >Procedure  | (0008,1032) | R           | 2           | This        |
   | Code        |             |             |             | Attribute   |
   | Sequence    |             |             |             | shall be    |
   |             |             |             |             | retrieved   |
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
   | >Reason for | (0040,100A) | R           | 2           | This        |
   | Requested   |             |             |             | Attribute   |
   | Procedure   |             |             |             | shall be    |
   | Code        |             |             |             | retrieved   |
   | Sequence    |             |             |             | with        |
   |             |             |             |             | Sequence or |
   |             |             |             |             | Universal   |
   |             |             |             |             | matching.   |
   +-------------+-------------+-------------+-------------+-------------+
   | *>>Includ   |             |             |             |             |
   | e*\ `table_ |             |             |             |             |
   | title <#tab |             |             |             |             |
   | le_8-1a>`__ |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Number of   | (0072,0014) | R           | 1           | This        |
   | Priors      |             |             |             | Attribute   |
   | Referenced  |             |             |             | shall be    |
   |             |             |             |             | retrieved   |
   |             |             |             |             | with Single |
   |             |             |             |             | Value or    |
   |             |             |             |             | Universal   |
   |             |             |             |             | matching.   |
   +-------------+-------------+-------------+-------------+-------------+
   | Hanging     | (0072,000E) | R           | 2           | This        |
   | Protocol    |             |             |             | Attribute   |
   | User        |             |             |             | shall be    |
   | Ide         |             |             |             | retrieved   |
   | ntification |             |             |             | with        |
   | Code        |             |             |             | Sequence or |
   | Sequence    |             |             |             | Universal   |
   |             |             |             |             | matching.   |
   +-------------+-------------+-------------+-------------+-------------+
   | *>Includ    |             |             |             |             |
   | e*\ `table_ |             |             |             |             |
   | title <#tab |             |             |             |             |
   | le_8-1a>`__ |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Hanging     | (0072,0010) | R           | 3           |             |
   | Protocol    |             |             |             |             |
   | User Group  |             |             |             |             |
   | Name        |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | **Hanging   |             |             |             |             |
   | Protocol    |             |             |             |             |
   | En          |             |             |             |             |
   | vironment** |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Number of   | (0072,0100) | R           | 2           |             |
   | Screens     |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Nominal     | (0072,0102) | -           | 2           |             |
   | Screen      |             |             |             |             |
   | Definition  |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Number of  | (0072,0104) | -           | 1           |             |
   | Vertical    |             |             |             |             |
   | Pixels      |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Number of  | (0072,0106) | -           | 1           |             |
   | Horizontal  |             |             |             |             |
   | Pixels      |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Display    | (0072,0108) | -           | 1           |             |
   | Environment |             |             |             |             |
   | Spatial     |             |             |             |             |
   | Position    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Screen     | (0072,010A) | -           | 1C          | Required if |
   | Minimum     |             |             |             | Screen      |
   | Grayscale   |             |             |             | Minimum     |
   | Bit Depth   |             |             |             | Color Bit   |
   |             |             |             |             | Depth       |
   |             |             |             |             | (0072,010C) |
   |             |             |             |             | is not      |
   |             |             |             |             | present.    |
   +-------------+-------------+-------------+-------------+-------------+
   | >Screen     | (0072,010C) | -           | 1C          | Required if |
   | Minimum     |             |             |             | Screen      |
   | Color Bit   |             |             |             | Minimum     |
   | Depth       |             |             |             | Grayscale   |
   |             |             |             |             | Bit Depth   |
   |             |             |             |             | (0072,010A) |
   |             |             |             |             | is not      |
   |             |             |             |             | present.    |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | (0072,010E) | -           | 3           |             |
   | Application |             |             |             |             |
   | Maximum     |             |             |             |             |
   | Repaint     |             |             |             |             |
   | Time        |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+

.. _sect_U.6.1.3:

Conformance Requirements
^^^^^^^^^^^^^^^^^^^^^^^^

An implementation may conform to one of the Hanging Protocol Information
Model SOP Classes as an SCU, SCP or both. The Conformance Statement
shall be in the format defined in .

.. _sect_U.6.1.3.1:

SCU Conformance
'''''''''''''''

.. _sect_U.6.1.3.1.1:

C-FIND SCU Conformance
                      

An implementation that conforms to one of the Hanging Protocol
Information Model SOP Classes shall support queries against the Hanging
Protocol Information Model using the C-FIND SCU Behavior described for
the Basic Worklist Management Service Class (see `C-FIND SCU
Behavior <#sect_K.4.1.2>`__ and `C-FIND Operation <#sect_U.4.1>`__).

An implementation that conforms to one of the Hanging Protocol
Information Model SOP Classes as an SCU shall state in its Conformance
Statement whether it requests Type 3 Return Key Attributes, and shall
list these Optional Return Key Attributes.

An implementation that conforms to one of the Hanging Protocol
Information Model SOP Classes as an SCU shall state in its Conformance
Statement how it makes use of Specific Character Set (0008,0005) when
encoding queries and interpreting responses.

.. _sect_U.6.1.3.1.2:

C-MOVE SCU Conformance
                      

An implementation that conforms to one of the Hanging Protocol
Information Model SOP Classes as an SCU shall support transfers against
the Hanging Protocol Information Model using the C-MOVE SCU baseline
behavior described for the Query/Retrieve Service Class (see `Baseline
Behavior of SCU <#sect_C.4.2.2.1>`__ and `C-MOVE
Operation <#sect_U.4.2>`__).

.. _sect_U.6.1.3.1.3:

C-GET SCU Conformance
                     

An implementation that conforms to the Hanging Protocol Information
Model - GET SOP Class as an SCU shall support transfers against the
Hanging Protocol Information Model using the C-GET SCU baseline behavior
described for the Query/Retrieve Service Class (see `Baseline Behavior
of SCU <#sect_C.4.3.2.1>`__ and `C-GET Operation <#sect_U.4.3>`__).

.. _sect_U.6.1.3.2:

SCP Conformance
'''''''''''''''

.. _sect_U.6.1.3.2.1:

C-FIND SCP Conformance
                      

An implementation that conforms to one of the Hanging Protocol
Information Model SOP Classes as an SCP shall support queries against
the Hanging Protocol Information Model using the C-FIND SCP Behavior
described for the Basic Worklist Management Service Class (see `C-FIND
SCP Behavior <#sect_K.4.1.3>`__).

An implementation that conforms to one of the Hanging Protocol
Information Model SOP Classes as an SCP shall state in its Conformance
Statement whether it supports Type 3 Return Key Attributes, and shall
list these Optional Return Key Attributes.

An implementation that conforms to one of the Hanging Protocol
Information Model SOP Classes as an SCP shall state in its Conformance
Statement how it makes use of Specific Character Set (0008,0005) when
interpreting queries, performing matching and encoding responses.

.. _sect_U.6.1.3.2.2:

C-MOVE SCP Conformance
                      

An implementation that conforms to one of the Hanging Protocol
Information Model SOP Classes as an SCP shall support transfers against
the Hanging Protocol Information Model using the C-MOVE SCP baseline
behavior described for the Query/Retrieve Service Class (see `Baseline
Behavior of SCP <#sect_C.4.2.3.1>`__).

An implementation that conforms to one of the Hanging Protocol
Information Model SOP Classes as an SCP, which generates transfers using
the C-MOVE operation, shall state in its Conformance Statement the
Hanging Protocol Storage Service Class SOP Class under which it shall
support the C-STORE sub-operations generated by the C-MOVE.

.. _sect_U.6.1.3.2.3:

C-GET SCP Conformance
                     

An implementation that conforms to the Hanging Protocol Information
Model - GET SOP Class as an SCP shall support transfers against the
Hanging Protocol Information Model using the C-GET SCP baseline behavior
described for the Query/Retrieve Service Class (see `Baseline Behavior
of SCP <#sect_C.4.3.3.1>`__).

An implementation that conforms to the Hanging Protocol Information
Model - GET SOP Class as an SCP, which generates transfers using the
C-GET operation, shall state in its Conformance Statement the Hanging
Protocol Storage Service Class SOP Class under which it will support the
C-STORE sub-operations generated by the C-GET.

.. _sect_U.6.1.4:

SOP Classes
^^^^^^^^^^^

The SOP Classes of the Hanging Protocol Information Model in the Hanging
Protocol Query/Retrieve Service Class identify the Hanging Protocol
Information Model, and the DIMSE-C operations supported. The following
Standard SOP Classes are identified:

.. table:: Hanging Protocol SOP Classes

   ========================================= ========================
   SOP Class Name                            SOP Class UID
   ========================================= ========================
   Hanging Protocol Information Model - FIND 1.2.840.10008.5.1.4.38.2
   Hanging Protocol Information Model - MOVE 1.2.840.10008.5.1.4.38.3
   Hanging Protocol Information Model - GET  1.2.840.10008.5.1.4.38.4
   ========================================= ========================

