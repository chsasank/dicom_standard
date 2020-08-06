.. _chapter_X:

Color Palette Query/Retrieve Service Class
==========================================

.. _sect_X.1:

Overview
--------

.. _sect_X.1.1:

Scope
~~~~~

The Color Palette Query/Retrieve Service Class defines an
application-level class-of-service that facilitates access to Color
Palette composite objects.

.. _sect_X.1.2:

Conventions
~~~~~~~~~~~

See Conventions for the Basic Worklist Management Service (K.1.2).

.. _sect_X.1.3:

Query/Retrieve Information Model
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In order to serve as an SCP of the Color Palette Query/Retrieve Service
Class, a DICOM AE possesses information about the Attributes of a number
of Color Palette composite SOP Instances. The information is organized
into a Color Palette Information Model.

.. _sect_X.1.4:

Service Definition
~~~~~~~~~~~~~~~~~~

Two peer DICOM AEs implement a SOP Class of the Color Palette
Query/Retrieve Service Class with one serving in the SCU role and one
serving in the SCP role. SOP Classes of the Color Palette Query/Retrieve
Service Class are implemented using the DIMSE-C C-FIND, C-MOVE and C-GET
services as defined in .

The semantics of the C-FIND service are the same as those defined in the
Service Definition of the Basic Worklist Management Service Class.

The semantics of the C-MOVE and C-GET services are the same as those
defined in the Service Definition of the Query/Retrieve Service Class,
with the exception that there is only one level of retrieval.

.. _sect_X.2:

Color Palette Information Model Definition
------------------------------------------

The Color Palette Information Model is identified by the SOP Class
negotiated at Association establishment time. The SOP Class is composed
of both an Information Model and a DIMSE-C Service Group.

The Color Palette Information Model is defined, with the
Entity-Relationship Model Definition and Key Attributes Definition
analogous to those defined in the Worklist Information Model Definition
of the Basic Worklist Management Service.

.. _sect_X.3:

Color Palette Information Model
-------------------------------

The Color Palette Information Model is based upon a one level entity:

-  Color Palette object instance

The Color Palette object instance contains Attributes associated with
the Color Palette object IE of the Composite IODs as defined in .

.. _sect_X.4:

DIMSE-C Service Groups
----------------------

.. _sect_X.4.1:

C-FIND Operation
~~~~~~~~~~~~~~~~

See the C-FIND Operation definition for the Basic Worklist Management
Service Class (K.4.1), and substitute "Color Palette" for "Worklist. The
"Worklist" Search Method shall be used.

The SOP Class UID identifies the Color Palette Information Model against
which the C-FIND is to be performed. The Key Attributes and values
allowable for the query are defined in the SOP Class definition for the
Color Palette Information Model.

.. _sect_X.4.2:

C-MOVE Operation
~~~~~~~~~~~~~~~~

See the C-MOVE Operation definition for the Query/Retrieve Service Class
(C.4.2). No Extended Behavior or Relational-Retrieve is defined for the
Color Palette Query/Retrieve Service Class.

Query/Retrieve Level (0008,0052) is not relevant to the Color Palette
Query/Retrieve Service Class, and therefore shall not be present in the
Identifier. The only Unique Key Attribute of the Identifier shall be SOP
Instance UID (0008,0018). The SCU shall supply one UID or a list of
UIDs.

.. note::

   More than one entity may be retrieved, using List of UID matching.

.. _sect_X.4.3:

C-GET Operation
~~~~~~~~~~~~~~~

See the C-GET Operation definition for the Query/Retrieve Service Class
(C.4.3). No Extended Behavior or Relational-Retrieve is defined for the
Color Palette Query/Retrieve Service Class.

Query/Retrieve Level (0008,0052) is not relevant to the Color Palette
Query/Retrieve Service Class, and therefore shall not be present in the
Identifier. The only Unique Key Attribute of the Identifier shall be SOP
Instance UID (0008,0018). The SCU shall supply one UID or a list of
UIDs.

.. note::

   More than one entity may be retrieved, using List of UID matching.

.. _sect_X.5:

Association Negotiation
-----------------------

See the Association Negotiation definition for the Basic Worklist
Management Service Class (K.5).

.. _sect_X.6:

SOP Class Definitions
---------------------

.. _sect_X.6.1:

Color Palette Information Model
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. _sect_X.6.1.1:

E/R Model
^^^^^^^^^

The Color Palette Information Model consists of a single entity. In
response to a given C-FIND request, the SCP shall send one C-FIND
response per matching Color Palette Instance.

.. _sect_X.6.1.2:

Color Palette Attributes
^^^^^^^^^^^^^^^^^^^^^^^^

`table_title <#table_X.6-1>`__ defines the Attributes of the Color
Palette Information Model:

.. table:: Attributes for the Color Palette Information Model

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
   | SOP Class   | (0008,0016) | R           | 1           | This        |
   | UID         |             |             |             | Attribute   |
   |             |             |             |             | shall be    |
   |             |             |             |             | retrieved   |
   |             |             |             |             | with Single |
   |             |             |             |             | Value       |
   |             |             |             |             | matching.   |
   +-------------+-------------+-------------+-------------+-------------+
   | SOP         | (0008,0018) | U           | 1           | This        |
   | Instance    |             |             |             | Attribute   |
   | UID         |             |             |             | shall be    |
   |             |             |             |             | retrieved   |
   |             |             |             |             | with Single |
   |             |             |             |             | Value       |
   |             |             |             |             | matching.   |
   +-------------+-------------+-------------+-------------+-------------+
   | **Color     |             |             |             |             |
   | Palette     |             |             |             |             |
   | D           |             |             |             |             |
   | efinition** |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Content     | (0070,0080) | R           | 1           | This        |
   | Label       |             |             |             | Attribute   |
   |             |             |             |             | shall be    |
   |             |             |             |             | retrieved   |
   |             |             |             |             | with Single |
   |             |             |             |             | Value, Wild |
   |             |             |             |             | Card or     |
   |             |             |             |             | Universal   |
   |             |             |             |             | matching.   |
   +-------------+-------------+-------------+-------------+-------------+
   | Content     | (0070,0081) | -           | 2           |             |
   | Description |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Content     | (0070,0084) | -           | 2           |             |
   | Creator's   |             |             |             |             |
   | Name        |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Alternate   | (0070,0087) | -           | 3           |             |
   | Content     |             |             |             |             |
   | Description |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Content    | (0070,0081) | -           | 1           |             |
   | Description |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Language   | (0008,0006) | -           | 1           |             |
   | Code        |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | *>>Includ   |             |             |             |             |
   | e*\ `table_ |             |             |             |             |
   | title <#tab |             |             |             |             |
   | le_8-3a>`__ |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+

.. _sect_X.6.1.3:

Conformance Requirements
^^^^^^^^^^^^^^^^^^^^^^^^

An implementation may conform to one of the Color Palette Information
Model SOP Classes as an SCU, SCP or both. The Conformance Statement
shall be in the format defined in .

.. _sect_X.6.1.3.1:

SCU Conformance
'''''''''''''''

.. _sect_X.6.1.3.1.1:

C-FIND SCU Conformance
                      

An implementation that conforms to one of the Color Palette Information
Model SOP Classes shall support queries against the Color Palette
Information Model using the C-FIND SCU Behavior described for the Basic
Worklist Management Service Class (see `C-FIND SCU
Behavior <#sect_K.4.1.2>`__ and `C-FIND Operation <#sect_X.4.1>`__).

An implementation that conforms to one of the Color Palette Information
Model SOP Classes as an SCU shall state in its Conformance Statement
whether it requests Type 3 Return Key Attributes, and shall list these
Optional Return Key Attributes.

An implementation that conforms to one of the Color Palette Information
Model SOP Classes as an SCU shall state in its Conformance Statement how
it makes use of Specific Character Set (0008,0005) when encoding queries
and interpreting responses.

.. _sect_X.6.1.3.1.2:

C-MOVE SCU Conformance
                      

An implementation that conforms to one of the Color Palette Information
Model SOP Classes as an SCU shall support transfers against the Color
Palette Information Model using the C-MOVE SCU baseline behavior
described for the Query/Retrieve Service Class (see `Baseline Behavior
of SCU <#sect_C.4.2.2.1>`__ and `C-MOVE Operation <#sect_X.4.2>`__).

.. _sect_X.6.1.3.1.3:

C-GET SCU Conformance
                     

An implementation that conforms to one of the Color Palette Information
Model SOP Classes as an SCU shall support transfers against the Color
Palette Information Model using the C-GET SCU baseline behavior
described for the Query/Retrieve Service Class (see `Baseline Behavior
of SCU <#sect_C.4.3.2.1>`__ and `C-GET Operation <#sect_X.4.3>`__).

.. _sect_X.6.1.3.2:

SCP Conformance
'''''''''''''''

.. _sect_X.6.1.3.2.1:

C-FIND SCP Conformance
                      

An implementation that conforms to one of the Color Palette Information
Model SOP Classes as an SCP shall support queries against the Color
Palette Information Model using the C-FIND SCP Behavior described for
the Basic Worklist Management Service Class (see `C-FIND SCP
Behavior <#sect_K.4.1.3>`__).

An implementation that conforms to one of the Color Palette Information
Model SOP Classes as an SCP shall state in its Conformance Statement
whether it supports Type 3 Return Key Attributes, and shall list these
Optional Return Key Attributes.

An implementation that conforms to one of the Color Palette Information
Model SOP Classes as an SCP shall state in its Conformance Statement how
it makes use of Specific Character Set (0008,0005) when interpreting
queries, performing matching and encoding responses.

.. _sect_X.6.1.3.2.2:

C-MOVE SCP Conformance
                      

An implementation that conforms to one of the Color Palette Information
Model SOP Classes as an SCP shall support transfers against the Color
Palette Information Model using the C-MOVE SCP baseline behavior
described for the Query/Retrieve Service Class (see `Baseline Behavior
of SCP <#sect_C.4.2.3.1>`__).

An implementation that conforms to one of the Color Palette Information
Model SOP Classes as an SCP, which generates transfers using the C-MOVE
operation, shall state in its Conformance Statement the Color Palette
Storage Service Class SOP Class under which it shall support the C-STORE
sub-operations generated by the C-MOVE.

.. _sect_X.6.1.3.2.3:

C-GET SCP Conformance
                     

An implementation that conforms to one of the Color Palette Information
Model SOP Classes as an SCP shall support transfers against the Color
Palette Information Model using the C-GET SCP baseline behavior
described for the Query/Retrieve Service Class (see `Baseline Behavior
of SCP <#sect_C.4.3.3.1>`__).

An implementation that conforms to one of the Color Palette Information
Model SOP Classes as an SCP, which generates transfers using the C-GET
operation, shall state in its Conformance Statement the Color Palette
Storage Service Class SOP Class under which it shall support the C-STORE
sub-operations generated by the C-GET.

.. _sect_X.6.1.4:

SOP Classes
^^^^^^^^^^^

The SOP Classes of the Color Palette Information Model in the Color
Palette Query/Retrieve Service Class identify the Color Palette
Information Model, and the DIMSE-C operations supported. The following
Standard SOP Classes are identified:

.. table:: Color Palette SOP Classes

   ====================================== ========================
   SOP Class Name                         SOP Class UID
   ====================================== ========================
   Color Palette Information Model - FIND 1.2.840.10008.5.1.4.39.2
   Color Palette Information Model - MOVE 1.2.840.10008.5.1.4.39.3
   Color Palette Information Model - GET  1.2.840.10008.5.1.4.39.4
   ====================================== ========================

