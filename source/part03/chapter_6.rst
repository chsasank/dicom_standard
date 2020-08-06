.. _chapter_6:

DICOM Information Model
=======================

The DICOM Information Model defines the structure and organization of
the information related to the communication of medical images.
`figure_title <#figure_6-1>`__ shows the relationships between the major
structures of the DICOM Information Model.

.. _sect_6.1:

Information Object Definition
-----------------------------

An Information Object Definition (IOD) is an object-oriented abstract
data model used to specify information about Real-World Objects. An IOD
provides communicating Application Entities with a common view of the
information to be exchanged.

An IOD does not represent a specific Instance of a Real-World Object,
but rather a class of Real-World Objects that share the same properties.
An IOD used to generally represent a single class of Real-World Objects
is called a Normalized Information Object. An IOD that includes
information about related Real-World Objects is called a Composite
Information Object.

.. _sect_6.1.1:

Composite IOD
~~~~~~~~~~~~~

A Composite IOD is an Information Object Definition that represents
parts of several entities included in the DICOM Model of the Real World.
This Model is introduced in `DICOM Model of the Real
World <#chapter_7>`__. Such an IOD includes Attributes that are not
inherent in the Real-World Object that the IOD represents but rather are
inherent in related Real-World Objects.

These related Real-World Objects provide a complete context for the
exchanged information. When an Instance of a Composite IOD is
communicated, this entire context is exchanged between Application
Entities. Relationships between Composite IOD Instances shall be
conveyed in this contextual information.

The Composite IODs are specified in `Composite Information Object
Definitions (Normative) <#chapter_A>`__.

.. _sect_6.1.2:

Normalized IOD
~~~~~~~~~~~~~~

A Normalized IOD is an Information Object Definition that generally
represents a single entity in the DICOM Model of the Real World.

When an Instance of a Normalized IOD is communicated, the context for
that Instance is not actually exchanged. Instead, the context is
provided through the use of pointers to related Normalized IOD
Instances.

The Normalized IODs are specified in `Normalized Information Object
Definitions (Normative) <#chapter_B>`__.

.. _sect_6.2:

Attributes
----------

The Attributes of an IOD describe the properties of a Real-World Object
Instance. Related Attributes are grouped into Modules that represent a
higher level of semantics documented in the Module Specifications found
in `Information Module Definitions (Normative) <#chapter_C>`__.

Attributes are encoded as Data Elements using the rules, the Value
Representation and the Value Multiplicity concepts specified in . For
specific Data Elements, the Value Representation and Value Multiplicity
are specified in the Data Dictionary in .

When multiple Modules containing the same Attributes(s) are included in
an IOD, the Attribute shall be encoded only once into a Data Element.

.. _sect_6.3:

On-line Communication and Media Storage Services
------------------------------------------------

For on-line communication the DIMSE Services allow a DICOM Application
Entity to invoke an operation or notification across a network or a
point-to-point interface. DIMSE Services are defined in .

For media storage interchange, Media Storage Services allow a DICOM
Application Entity to invoke media storage related operations.

.. note::

   These Media Storage Services are discussed in .

.. _sect_6.3.1:

DIMSE-C Services
~~~~~~~~~~~~~~~~

DIMSE-C Services are services applicable only to a Composite IOD, except
for C-FIND that may apply to both normalized and Composite Instances.
DIMSE-C Services provide only operation services.

.. _sect_6.3.2:

DIMSE-N Services
~~~~~~~~~~~~~~~~

DIMSE-N Services are services applicable only to a Normalized IOD.
DIMSE-N Services provide both operation and notification services.

.. _sect_6.4:

DIMSE Service Group
-------------------

A DIMSE Service Group specifies one or more operations/notifications
defined in that are applicable to an IOD.

DIMSE Service Groups are defined in in the specification of a
Service-Object Pair Class.

.. _sect_6.5:

Service-Object Pair Class (SOP Class)
-------------------------------------

The SOP Class definitions in contain the rules and semantics that may
restrict the use of the services in the DIMSE Service Group and/or the
Attributes of the IOD. and contain the rules and semantics that may
restrict the attributes of the IOD or the use of the services in the
Media Storage Services and the Web Services respectively.

The selection of SOP Classes is used by Application Entities to
establish an agreed set of capabilities to support their interaction for
SOP Classes based on DIMSE Services. This negotiation is performed at
association establishment time as described in . An extended negotiation
allows Application Entities to further agree on specific options within
a SOP Class.

.. note::

   The SOP Class as defined in the DICOM Information Model is equivalent
   in ISO/OSI terminology to the Managed Object Class. Readers familiar
   with object-oriented terminology will recognize the SOP Class
   operations (and notifications) as comprising the methods of an object
   class.

.. _sect_6.5.1:

Normalized and Composite SOP Classes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

DICOM defines two types of SOP Classes, Normalized and Composite. For
DIMSE Services, Normalized SOP Classes are defined as the union of a
Normalized IOD and a set of DIMSE-N Services, while Composite SOP
Classes are defined as the union of a Composite IOD and a set of DIMSE-C
Services. Media Storage Services only support Composite IODs and Web
Services supports both Normalized and Composite SOP Classes.

.. note::

   SOP Class Specifications play a central role for defining DICOM
   conformance requirements. It allows DICOM Application Entities to
   select a well-defined application level subset of the DICOM V3.0
   Standard to which they may claim conformance. See .

.. _sect_6.6:

Association Negotiation
-----------------------

Association establishment is the first phase of communication between
peer DICOM compliant Application Entities. The Application Entities
shall use association establishment to negotiate which SOP Classes can
be exchanged and how this data will be encoded.

Association Negotiation is defined in .

.. _sect_6.7:

Service Class Specification
---------------------------

A Service Class Specification defines a group of one or more SOP Classes
related to a specific function that is to be accomplished by
communicating Application Entities. A Service Class Specification also
defines rules that allow implementations to state some pre-defined level
of conformance to one or more SOP Classes. Applications may conform to
SOP Classes as either or both a Service Class User (SCU) or Service
Class Provider (SCP).

Service Class Specifications are defined in .

.. note::

   Such interaction between peer Application Entities work on a
   'client/server model'. The SCU acts as the 'client', while the SCP
   acts as the 'server'. The SCU/SCP roles are determined during
   association establishment.

