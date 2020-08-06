.. _chapter_6:

Service Context
===============

This section defines the DICOM Message Service Element and Protocol
within the context of the DICOM Application Entity. Specifically, this
section provides a model to clarify a number of concepts for digital
imaging and communications and introduces key terms used throughout the
Standard. This model has been used to partition the Application Layer of
the DICOM Standard into separate parts.

.. _sect_6.1:

DICOM Communication Model for Message Exchange
----------------------------------------------

presents the general communication model of the DICOM Standard, which
spans both network (on-line) and storage media interchange (off-line)
communications. Application Entities may utilize any of the following
transport mechanisms:

-  the DICOM Message Service and Upper Layer Service, which provides
   independence from specific physical networking communication support
   and protocols such as TCP/IP,

-  the DICOM Web Service API and HTTP Service, which allows use of
   common hypertext and associated protocols for transport of DICOM
   services, or

-  the Basic DICOM File Service, which provides access to Storage Media
   independently from specific physical media storage formats and file
   structures.

PS3.7 focuses on the DICOM Message Service and here the OSI Basic
Reference Model is used to model the interconnection of medical imaging
equipment. As shown in `figure_title <#figure_6.1-1>`__ several layers
of communication protocols are distinguished. DICOM uses the OSI Upper
Layer Service to separate the exchange of DICOM Messages at the
Application Layer from the communication support provided by the lower
layers.

This OSI Upper Layer Service boundary allows peer Application Entities
to establish Associations, transfer Messages and terminate Associations.
For this boundary, DICOM has adopted the OSI Standards (Presentation
Service augmented by the Association Control Service Element). It is a
simple service that isolates the DICOM Application Layer from the
specific stack of protocols used in the communication support layers.

The DICOM Upper Layer protocol augments TCP/IP. It combines the OSI
upper layer protocols into a simple-to-implement single protocol while
providing the same services and functions offered by the OSI stack.

The DICOM Upper Layer Service is defined in .

.. _sect_6.2:

The DICOM Application Layer Structure
-------------------------------------

A DICOM Application Entity and the Service Elements it includes are
shown in `figure_title <#figure_6.2-1>`__.

.. note::

   Annexes of this Part define certain aspects of the DICOM Application
   Entity.

The heart of any DICOM Application Entity is specified by the following
parts of the DICOM Standard:

-  , Information Object Definitions, which provides data models and
   Attributes used as a basis for defining SOP Instances that are
   operated upon by the services defined in this [art. Such SOP
   Instances are used to represent real-world occurrences of images,
   studies, patients, etc.

-  , Service Class Specifications, which defines the set of operations
   that can be performed on SOP Instances. Such operations may include
   the storage, retrieval of information, printing, etc.

-  , Data Structure and Encoding, which addresses the encoding of the
   Data Sets exchanged to accomplish the above services

-  , Data Dictionary, which contains the registry of DICOM Data Elements
   used to represent Attributes of SOP Classes

The DICOM Application Entity uses the Association and Presentation data
services of the OSI Upper Layer Service defined in . The Association
Control Service Element (ACSE) augments the Presentation Layer Service
with Association establishment and termination services. In the case of
TCP/IP, the full equivalent of ACSE is provided by the DICOM Upper Layer
Service. For the DICOM point-to-point stack, a minimum subset of ACSE is
provided by the Session/Transport/Network Service.

The DICOM Application Entity uses the services provided by the DICOM
Message Service Element. The DICOM Message Service Element specifies two
sets of services.

-  DIMSE-C supports operations associated with composite SOP Classes and
   provides effective compatibility with the previous versions of the
   DICOM Standard.

-  DIMSE-N supports operations associated with normalized SOP Classes
   and provides an extended set of object-oriented operations and
   notifications. It is based on the OSI System Management Model and
   more specifically on the OSI Common Management Information Services
   (CMIS) Service definition.

The DIMSE-C and DIMSE-N services are supported by a single DIMSE
protocol that uses the DICOM-specific Message formatting and encoding.

.. _sect_6.3:

DICOM Message Structure and Command Set
---------------------------------------

Information is communicated across the DICOM network interface in a
DICOM Message. A Message is composed of a Command Set followed by a
conditional Data Set (see for the definition of a Data Set). The Command
Set is used to indicate the operations/notifications to be performed on
or with the Data Set.

A Command Set is constructed of Command Elements. Command Elements
contain the encoded values for each individual field of the Command Set
per the semantics specified in the DIMSE protocol (see
`Sequencing <#sect_9.2>`__ and `Sequencing <#sect_10.2>`__). Each
Command Element is composed of an explicit Tag, a Value Length, and a
Value Field.

The overall structure of a DICOM Message is shown in
`figure_title <#figure_6.3-1>`__.

.. _sect_6.3.1:

Command Set Structure
~~~~~~~~~~~~~~~~~~~~~

The Command Elements in a Command Set shall be ordered by increasing
Command Element Tag number. A Command Element Tag uniquely identifies a
Command Element and shall occur at most once in a Command Set. The
encoding of the Command Set shall be Little Endian Byte Ordering as
defined in . The requirements for the existence of a Command Element in
a Command Set are defined in the DIMSE protocol.

.. note::

   1. The use of Private Command Elements has been retired in this
      version of the DICOM Standard.

   2. The encoding corresponds to the Implicit VR Data Element encoding
      defined in .

A Command Element is composed of three fields; a Command Element Tag, a
Value Length, and a Value Field.

Command Element Tag: An ordered pair of 16-bit unsigned integers
representing the Group Number followed by Element Number.

Value Length: A 32-bit unsigned integer representing the explicit Length
as the number of bytes (even) that make up the Value. It does not
include the length of the Command Element Tag or Value Length fields.

Value Field: An even number of bytes containing the Value(s) of the
Command Element.

The command type of Value(s) stored in this field is specified by the
Command Element's Value Representation (VR). The VR for a given Command
Element can be determined using the Command Dictionary in `Command
Dictionary (Normative) <#chapter_E>`__. The VR of Command Elements shall
agree with those specified in the Command Dictionary. The VR definitions
are defined in

The Value Multiplicity (VM) specifies how many Values with the VR can be
placed in the Value Field. If the VM is greater than one, multiple
Values shall be delimited within the Value Field as defined in . The VM
for a given Command Element can be determined using the Command
Dictionary in `Command Dictionary (Normative) <#chapter_E>`__.

.. note::

   1. The Message Length-to-End (0000,0001) Command Element is retired.
      Implementations may choose to send it for backward compatibility
      reasons. DICOM V3.0 conformant implementations must not rely on
      its presence for their operation.

   2. The delimitation of the Message length is actually achieved by
      relying on the fact that the Presentation Data Value (conveying
      each Message fragment) is delimited as defined by the OSI Upper
      Layer Service and the associated Message Control Header (see ).
      This results from the fact that the DICOM V3.0 UL protocol or the
      OSI Presentation protocol explicitly conveys the length of a PDV.

