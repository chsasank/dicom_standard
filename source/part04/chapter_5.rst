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
representation (such as IOD or Module). An entity is depicted as a box
within this Part of the DICOM Standard as shown in Figure 5-1.

.. _sect_5.1.2:

Relationship
~~~~~~~~~~~~

A relationship, which defines how entities are related, is depicted as a
diamond within this Standard as shown in Figure 5-2.

The relationship is read from source to destination entity as indicated
by the arrows. The a and b show the source and destination cardinality
of the relationship respectively. The following cardinalities are
permitted:

a. (a = 1, b = 1) -one source entity is related to one destination
   entity

b. (a = 1, b = 0-n) -one source entity is related to zero or more
   destination entities

c. (a = 1, b = 1-n) -one source entity is related to one or more
   destination entities

d. (a = 1-n, b = 1) -one or more source entities are related to one
   destination entity

e. (a = 1-n, b = 0-n) -one or more source entities are related to zero
   or more destination entities

f. (a = 1-n, b = 1-n) -one or more source entities are related to one or
   more destination entities

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

Certain tables in this Part of the DICOM Standard denote a Sequence of
Items by using the symbol: '>.'

In `Verification Service Class (Normative) <#chapter_A>`__, '>' is used
to identify a 'Sequence of Modules.' Nested Sequences of Modules are
identified by '>>'. In `Storage Service Class
(Normative) <#chapter_B>`__ and `Query/Retrieve Service Class
(Normative) <#chapter_C>`__, '>' is used to identify a 'Sequence of
Attributes'. See for the complete specification of how Sequences of
Items shall be encoded.

.. note::

   Information Object Definitions (IODs) that include the Sequence of
   Module construct are often called folders. The use of 'Sequences of
   Attributes' is not limited to 'Folders.'

.. _sect_5.3:

Response Status Values
----------------------

Certain tables in this Part of the DICOM Standard denote an
implementation specific response status code by using the symbol 'xx' or
'xxx' as part of the code.

.. note::

   Each 'x' symbol may be replaced by an implementation with a
   hexadecimal digit in the range from 0 to F.

.. _sect_5.4:

Usage Specification
-------------------

The building blocks of SOP Classes are Modules and DIMSE Services. The
DIMSE Services associated with a SOP Class may be Mandatory (M) or
Optional (U). The usage may be different for the SCU and SCP. The usage
is specified as a pair of letters: the former indicating the SCU usage,
the latter indicating the SCP usage.

.. _sect_5.4.1:

Use of DIMSE Services
~~~~~~~~~~~~~~~~~~~~~

The meaning and behavior of the usage specification for DIMSE Services
are:

M/M
   The SCU shall support the DIMSE Service but is not required to use it
   on an Association. The SCP shall support the DIMSE Service.

U/M
   The SCU may support and use the DIMSE Service. The SCP shall support
   the DIMSE Service.

U/U
   The SCU may support and use the DIMSE Service. The SCP may support
   the DIMSE Service. If the SCP does not support the DIMSE Service used
   by the SCU, it shall return a Failure status.

.. _sect_5.4.2:

Use of Attributes in Normalized Services
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Modules and their usage in Composite IODs are defined in . Normalized
IODs are also constructed from Modules but usage is specified on an
Attribute basis in this Part of the DICOM Standard. The following usage
specification applies to all Attributes of Normalized IODs unless
superseded by a usage specification in a particular SOP Class
Specification.

The term ‘receive’ means the following: the value shall be stored; under
certain circumstances (e.g. coercion) the value returned may have
changed.

.. _sect_5.4.2.1:

DIMSE Service N-CREATE, N-SET, N-ACTION
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The following Requirements apply when specifying the use of DIMSE
services N-CREATE, N-SET, N-ACTION.

The convention used in the table below are as follows:

Mandatory
   The SCU shall provide the Attribute.

Optional
   The SCU may or may not provide the Attribute.

Undefined
   The SCU's usage of the Attribute is undefined.

Mandatory
   The SCP shall support receiving the Attribute.

Mandatory with Default
   The SCP shall support receiving the Attribute. Upon receiving
   zero-length values, the SCP shall assign values as defined by the
   specification of the Service Class.

Optional
   The SCP may or may not support receiving the Attribute.

Undefined
   The SCP’s support of the Attribute is undefined.

=== ========= ============= ======================
\   SCU       SCP           
=== ========= ============= ======================
1/1 Mandatory Not Permitted Mandatory
2/1 Mandatory Permitted     Mandatory with Default
2/2 Mandatory Permitted     Mandatory
3/1 Optional  Not Permitted Mandatory
3/2 Optional  Not Permitted Optional
3/3 Optional  Not Permitted Optional
-/- Undefined Undefined     Undefined
=== ========= ============= ======================

If the SCU does not provide an Attribute that is Mandatory for the SCU,
the SCP shall respond with the error code "Missing Attribute" (0120H).

If the SCU provides a zero-length value for a Mandatory Attribute when
zero length is not permitted, the SCP shall respond with the error code
"Missing Attribute Value" (0121H).

.. _sect_5.4.2.2:

DIMSE Service N-GET, N-EVENT-REPORT
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The following Requirements apply when specifying the use of DIMSE
services N-GET, N-EVENT-REPORT.

The convention used in the table below are as follows:

Optional
   The SCU may retrieve the Attribute.

Undefined
   The SCU's usage of the Attribute is undefined.

Mandatory
   The SCP shall support retrieval of the Attribute.

Optional
   The SCP may or may not support retrieval of the Attribute.

Undefined
   The SCP’s support of the Attribute is undefined.

=== ========= ========= =============
\   SCU       SCP       
=== ========= ========= =============
3/1 Optional  Mandatory Not Permitted
3/2 Optional  Mandatory Permitted
3/3 Optional  Optional  Not Permitted
-/1 Undefined Mandatory Not Permitted
-/2 Undefined Mandatory Permitted
-/3 Undefined Optional  Not Permitted
=== ========= ========= =============

If support of an Attribute by the SCP is optional and the SCP does not
support the Attribute and the Attribute is requested by the SCU, the SCP
shall respond with the error code "Invalid Attribute Value" (0106H) or
"Attribute Value out of range" (0116H).

.. _sect_5.4.2.3:

Other Requirements
^^^^^^^^^^^^^^^^^^

If the SCP usage type designation is modified by a "C" (e.g., 3/1C) the
specification stated above shall be modified to include the requirement
that the SCP shall support the Attribute if the specified condition is
met.

For all N-CREATE, N-SET, N-GET, N-DELETE, N-ACTION and N-EVENT-REPORT
operations, the SOP Class is conveyed in the request primitive in
Affected SOP Class UID (0000,0002). The SOP Class UID (0008,0016)
Attribute shall not be present in the Data Set.

For N-CREATE operations and N-EVENT-REPORT notifications, the SOP
Instance is conveyed in Affected SOP Instance UID (0000,1000). The SOP
Instance UID (0008,0018) Attribute shall not be present in the Data Set.

.. note::

   In some Service Classes, the SOP Class definition may override the
   general provision in that allows the SOP Instance UID to be specified
   or omitted in the N-CREATE request primitive, and require that the
   SCU be responsible for specifying the SOP Instance UID.

For N-SET, N-GET, N-ACTION and N-DELETE operations, the SOP Instance is
conveyed in Requested SOP Instance UID (0000,1001). The SOP Instance UID
(0008,0018) Attribute shall not be present in the Data Set.

