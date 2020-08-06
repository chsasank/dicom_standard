.. _chapter_5:

Conventions
===========

.. _sect_5.1:

Entity-Relationship Model
-------------------------

.. _sect_5.1.1:

Entity
~~~~~~

An entity is used in an Entity-Relationship (E-R) model to represent a
Real-World Object, class of Real-World Objects, or DICOM data
representation (such as an IOD or Module). An entity is depicted as
shown in `figure_title <#figure_5.1-1>`__.

.. _sect_5.1.2:

Relationship
~~~~~~~~~~~~

A relationship, which defines how entities are related, is depicted as a
diamond within this Part of the DICOM Standard as shown in
`figure_title <#figure_5.1-2>`__.

The relationship is read from source to destination entity as indicated
by the arrows. The a and b show the source and destination cardinality
of the relationship respectively. The following cardinalities are
permitted:

a. (a = 1, b = 1) - one source entity is related to one destination
   entity

b. (a = 1, b = 0-n) - one source entity is related to zero or more
   destination entities

c. (a = 1, b = 1-n) - one source entity is related to one or more
   destination entities

d. (a = 1-n, b = 1) - one or more source entities are related to one
   destination entity

e. (a = 1-n, b = 0-n) - one or more source entities are related to zero
   or more destination entities

f. (a = 1-n, b = 1-n) - one or more source entities are related to one
   or more destination entities

In a relationship where (a = 1-n, b = 1-n) the values of the source and
destination cardinalities may be different. The value "n" simply denotes
one or more.

.. note::

   DICOM has added the use of arrows to the E-R diagramming conventions
   often used in other literature. This has been done to avoid the
   possibility of inferring an incorrect relationship that can result
   from reading a relationship in the reverse order of that intended.
   For example, a relationship "Cat Catches Mouse" could be read "Mouse
   Catches Cat" if the arrows were not present.

A relationship may be bi-directional (i.e., the relationship is true in
both directions). In such a case, the convention used is arrows pointing
toward both the source and the destination entities.

.. _sect_5.2:

Sequences
---------

Certain Tables in this Standard describe Sequences of Items by using the
symbol: '>'. The symbol '>' precedes the Attribute (or Module) Name of
the members of an Item. All marked Attributes (or Modules) belong to the
generic description of an Item that may be repeated to form a Sequence
of Items. This Sequence of Items is nested in the Attribute (or Module)
that precedes in the table the first member marked with a '>'.

.. note::

   The following table describes the "Referenced Series Sequences"
   Attribute as a Sequence of one or more Items where each Item contains
   the three Attributes marked by a '>'. The Sequence of Items is nested
   inside the value of the Referenced Series Sequence Attribute. The
   following Attribute (not marked) is not part of the Items of the
   Sequence.

========================== =====
**…**                      **…**
Referenced Series Sequence …
>Series Date               …
>Series Time               …
>Series Instance UID       …
Modality                   …
========================== =====

This notation may be used to create nested hierarchical structures by
using '>>' at the second level of nesting and so on.

The Type of the Sequence Attribute defines whether the Sequence
Attribute itself must be present, and the Attribute Description of the
Sequence Attribute may define whether and how many Items shall be
present in the Sequence. The Types of the Attributes of the Data Set
included in the Sequence, including any conditionality, are specified
within the scope of each Data Set, i.e., for each Item present in the
Sequence. See .

For describing the number of Items in the Attribute description the
following sentences are preferred:

+------------------------+-----------------+------------------------+
| Sequence Attribute     | Number of Items | Sentence               |
| Type                   |                 |                        |
+========================+=================+========================+
| 1 or 1C                | 1               | Only a single Item     |
|                        |                 | shall be included in   |
|                        |                 | this Sequence.         |
+------------------------+-----------------+------------------------+
| 1 or 1C                | 1-n             | One or more Items      |
|                        |                 | shall be included in   |
|                        |                 | this Sequence.         |
+------------------------+-----------------+------------------------+
| 2 or 2C                | 0-1             | Zero or one Item shall |
|                        |                 | be included in this    |
|                        |                 | Sequence.              |
+------------------------+-----------------+------------------------+
| 2 or 2C                | 0-n             | Zero or more Items     |
|                        |                 | shall be included in   |
|                        |                 | this Sequence.         |
+------------------------+-----------------+------------------------+
| 3                      | 1               | Only a single Item is  |
|                        |                 | permitted in this      |
|                        |                 | Sequence.              |
+------------------------+-----------------+------------------------+
| 3                      | 1-n             | One or more Items are  |
|                        |                 | permitted in this      |
|                        |                 | Sequence.              |
+------------------------+-----------------+------------------------+

.. note::

   The encoding of empty Sequence Attributes is described in .

In a number of cases for Normalized IODs, the Data Element Type and
Conditions are defined in the appropriate Service definition in , in
other cases in the Attribute description in . It is not necessary to
specify for any Attribute within a Sequence the condition that it is
"required if a Sequence Item is present", since this is always implicit,
whether or not there are additional requirements.

.. _sect_5.3:

Triplet Encoding of Structured Data (Retired)
---------------------------------------------

This section has been retired. See `Encoding of Coded Entry
Data <#chapter_8>`__.

.. _sect_5.4:

Attribute Macros
----------------

Some tables contain references to Attribute Macros. This convention is
used in cases where the same Attributes are used in multiple tables or
multiple places in one Module. The reference means that the Attributes
of the Attribute Macro shall be included in the Module in place of the
row that contains the reference to the Attribute Macro.

In some cases, the Attribute Macro is used in a Sequence (the VR of the
Data Element in which the Attribute is encoded is SQ, see ). When this
is done, the reference is preceded by one or more ">" characters. The
number of ">" characters indicates the level in the Sequence that all of
the Attributes in the Attribute Macro occupy.

There may be specialization of the description of the Attributes in the
Attribute Macro. In these cases, this specialization is described in the
Description column of the Module.

Following is an example of this convention.

`table_title <#table_5.4-1>`__ is an example of a Module table using the
Attribute Macro convention.

.. table:: Example Module Table

   +-------------------+-------------------+------+-------------------+
   | Attribute Name    | Tag               | Type | Attribute         |
   |                   |                   |      | Description       |
   +===================+===================+======+===================+
   | Attribute A       | (aaaa,aaaa)       | 1    | This is an        |
   |                   |                   |      | example.          |
   +-------------------+-------------------+------+-------------------+
   | Attribute B       | (bbbb,bbbb)       | 1    | This is an        |
   | Sequence          |                   |      | example of a      |
   |                   |                   |      | Sequence          |
   |                   |                   |      | Attribute         |
   +-------------------+-------------------+------+-------------------+
   | *>Includ          | In this Module,   |      |                   |
   | e*\ `table_title  | Attribute D       |      |                   |
   | <#table_5.4-2>`__ | (dddd,dddd) is    |      |                   |
   |                   | Type 1            |      |                   |
   +-------------------+-------------------+------+-------------------+

`table_title <#table_5.4-2>`__ is an example of the Attribute Macro
referenced in `table_title <#table_5.4-1>`__.

.. table:: Example Macro Attributes

   ============== =========== ==== =====================================
   Attribute Name Tag         Type Attribute Description
   ============== =========== ==== =====================================
   Attribute C    (cccc,cccc) 1    This is an example.
   Attribute D    (dddd,dddd) 3    This Attribute is generally a Type 3.
   ============== =========== ==== =====================================

The contents of the Example Module Table, if it had not been described
with the Example Macro would have been as shown in
`table_title <#table_5.4-3>`__.

.. table:: Example Module Table Without The Use of An Attribute Macro

   +----------------------+-------------+------+----------------------+
   | Attribute Name       | Tag         | Type | Attribute            |
   |                      |             |      | Description          |
   +======================+=============+======+======================+
   | Attribute A          | (aaaa,aaaa) | 1    | This is an example.  |
   +----------------------+-------------+------+----------------------+
   | Attribute B Sequence | (bbbb,bbbb) | 1    | This is an example   |
   |                      |             |      | of a Sequence        |
   |                      |             |      | Attribute.           |
   +----------------------+-------------+------+----------------------+
   | >Attribute C         | (cccc,cccc) | 1    | This is an example.  |
   +----------------------+-------------+------+----------------------+
   | >Attribute D         | (dddd,dddd) | 1    | In this Module, this |
   |                      |             |      | Attribute has been   |
   |                      |             |      | specialized to Type  |
   |                      |             |      | 1 as indicated in    |
   |                      |             |      | `table_titl          |
   |                      |             |      | e <#table_5.4-1>`__. |
   +----------------------+-------------+------+----------------------+

.. _sect_5.5:

Types and Conditions in Normalized IODs
---------------------------------------

When a Normalized Information Object Definition in PS3.3 invokes Modules
(e.g., the `SOP Common Module <#sect_C.12.1>`__) or Attribute Macros
that are specified with Data Element Types, those specified Data Element
Types and Conditions do not apply. Rather, the Data Element Types and
Conditions have to be specified for each Attribute for both SCU and SCP
in the appropriate Service definition in .

.. _sect_5.6:

Invocation of Context Groups
----------------------------

The conventions used for Code Sequences are:

-  no Baseline Defined

-  using the Context Group as Baseline Context Group

-  using the Context Group as Defined Context Group

See also .

In combination with the definition of the Context Group as Extensible or
Non-extensible in , the conventions in `table_title <#table_5.6-1>`__
apply.

.. table:: Conventions for Specification of Context Groups

   +----------------------+----------------------+----------------------+
   |                      | Extensible Context   | Non-Extensible       |
   |                      | Group                | Context Group        |
   +======================+======================+======================+
   | No Baseline or       | Any Code may be used |                      |
   | Defined CID          | if its meaning is    |                      |
   | specified            | applicable to the    |                      |
   |                      | context of           |                      |
   |                      | invocation.          |                      |
   +----------------------+----------------------+----------------------+
   | Baseline Context     | Codes in the Context | Non-extensible       |
   | Group Identifier     | Group may be used.   | Context Groups are   |
   | (BCID)               |                      | not used as Baseline |
   |                      | Alternative Codes    | Context Groups.      |
   |                      | for the same Concept |                      |
   |                      | (i.e., with the same |                      |
   |                      | meaning) may be used |                      |
   |                      | instead of the Codes |                      |
   |                      | in the Context       |                      |
   |                      | Group, since this    |                      |
   |                      | can be construed as  |                      |
   |                      | not using the        |                      |
   |                      | Baseline Context     |                      |
   |                      | Group.               |                      |
   |                      |                      |                      |
   |                      | Codes not in the     |                      |
   |                      | Context Group may be |                      |
   |                      | used as an extension |                      |
   |                      | when their meaning   |                      |
   |                      | is within the scope  |                      |
   |                      | of that Context      |                      |
   |                      | Group.               |                      |
   |                      |                      |                      |
   |                      | I.e., any Code may   |                      |
   |                      | be used if its       |                      |
   |                      | meaning is           |                      |
   |                      | applicable to the    |                      |
   |                      | context of           |                      |
   |                      | invocation.          |                      |
   |                      |                      |                      |
   |                      | See also .           |                      |
   +----------------------+----------------------+----------------------+
   | Defined Context      | Codes in the Context | Codes in the Context |
   | Group Identifier     | Group shall be used. | Group shall be used. |
   | (DCID)               |                      |                      |
   |                      | Codes not in the     | Codes not in the     |
   |                      | Context Group may be | Context Group shall  |
   |                      | used as an extension | not be used.         |
   |                      | to the specified     |                      |
   |                      | Context Group when   |                      |
   |                      | their meaning is     |                      |
   |                      | within the scope of  |                      |
   |                      | that Context Group.  |                      |
   |                      |                      |                      |
   |                      | See also .           |                      |
   +----------------------+----------------------+----------------------+

