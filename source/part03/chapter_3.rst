.. _chapter_3:

Definitions
===========

For the purposes of this Standard the following definitions apply.

Application Entity
   See `biblioentry_title <#biblio_ISO7498-1>`__.

Service
   See `biblioentry_title <#biblio_ISO7498-1>`__.

Primitive
   See `biblioentry_title <#biblio_ISO8509>`__.

Attribute
   .

Command
   .

Data Dictionary
   .

Message
   .

Service-Object Pair Class
   .

Real-World Activity
   .

Real-World Object
   .

Service Class
   .

Service Class User
   .

Service Class Provider
   .

Service-Object Pair Instance
   .

Preformatted Grayscale Image
   .

Preformatted Color Image
   .

Related General SOP Class
   .

Basic Offset Table
   .

Data Element
   .

Data Element Tag
   .

Data Element Type
   .

Data Set
   .

Defined Term
   .

Enumerated Value
   .

Extended Offset Table
   .

Sequence of Items
   .

Unique Identifier
   .

DICOM Message Service Element
   .

DIMSE-N Services
   .

DIMSE-C Services
   .

DICOM Upper Layer Service
   .

Acquisition Context
   A description of the conditions present during data acquisition.

Acquisition Protocol Element
   A sequential component of an acquisition protocol, that contains the
   SCANNING PARAMETERS necessary to perform a single SCAN. In the case
   of CT this would correspond to tube voltage, tube current, rotation
   time, spatial location, etc. and an Acquisition Protocol Element also
   corresponds to an XR-25 PROTOCOL ELEMENT.

Assertion
   An affirmative statement or declaration by a specified entity about a
   specified or implied subject for a specified or implied purpose.

Attribute Tag
   A unique identifier for an Attribute of an Information Object
   composed of an ordered pair of numbers (a Group Number followed by an
   Element number).

Basic Directory IOD
   The Basic Directory Information Object Definition is an abstraction
   of the information to identify a File-set and facilitate access to
   the information stored in the files of a File-set based on key
   medical information.

Basic Directory Information Model
   A model that defines the relationship between the various types of
   Directory Records that may be used in constructing DICOM Directories.

Cine Run
   A set of temporally related frames acquired at constant or variable
   frame rates. This term incorporates the general class of
   serialography.

   .. note::

      A Cine Run is typically encoded as a multi-frame image.

Code Sequence Attribute
   Attribute that (usually) includes the string "Code Sequence" in the
   Attribute Name and has a VR of SQ (Sequence of Items). Its purpose is
   to encode concepts using code values and optional text meanings from
   coding schemes. `Code Value <#sect_8.1>`__ through `Standard
   Attribute Sets for Code Sequence Attributes <#sect_8.8>`__ specify
   the Attributes of which the Sequence Items (Attribute Sets) of Code
   Sequence Attributes are constructed.

Composite IOD
   An Information Object Definition that represents parts of several
   entities in the DICOM Application Model. Such an IOD includes
   Attributes that are not inherent in the Real-World Object that the
   IOD represents but rather are inherent in related Real-World Objects.

Derived Image
   An image in which the pixel data was constructed from pixel data of
   one or more other images (source images).

DICOM Application Model
   An Entity-Relationship diagram used to model the relationships
   between Real-World Objects that are within the area of interest of
   the DICOM Standard.

DICOM Information Model
   An Entity-Relationship diagram that is used to model the
   relationships between the Information Object Definitions representing
   classes of Real-World Objects defined by the DICOM Application Model.

Functional Group
   A set of logically related Attributes that are likely to vary
   together. May be used in Multi-frame IODs to describe parameters that
   change on a per frame basis.

Information Entity
   That portion of information defined by a Composite IOD that is
   related to one specific class of Real-World Object. There is a
   one-to-one correspondence between Information Entities and entities
   in the DICOM Application Model.

Information Object Definition
   A data abstraction of a class of similar Real-World Objects that
   defines the nature and Attributes relevant to the class of Real-World
   Objects represented.

Module
   A set of Attributes within an Information Entity or Normalized IOD
   that are logically related to each other.

Multi-frame Image
   Image that contains multiple two-dimensional pixel planes.

Normalized IOD
   An Information Object Definition that represents a single entity in
   the DICOM Application Model. Such an IOD includes Attributes that are
   only inherent in the Real-World Object that the IOD represents.

Protocol Element
   A sequential component of a protocol, consisting of all the
   parameters necessary to perform that component of the protocol.

ReconstructionProtocolElement
   A sequential component of a reconstruction protocol, such as
   generating CT thin images or multiplanar reformats.

Specialization
   Specialization is the replacement of the Type, value range and/or
   description of an Attribute in a general Module of an IOD, by its
   Type, value range and/or description defined in a modality-specific
   Module of an IOD.

   .. note::

      The same Attribute may be present in multiple Modules in the same
      IOD but not specified to be "Specialized".

StorageProtocolElement
   A sequential component of a storage protocol, such as sending a
   Series of images to a PACS or an archive or a processing workstation.

Coded Character Set
   See `biblioentry_title <#biblio_ISOIEC2022>`__.

Code Extension
   See `biblioentry_title <#biblio_ISOIEC2022>`__.

Escape Sequence
   See `biblioentry_title <#biblio_ISOIEC2022>`__.

FIXED REFERENCE System
   See `biblioentry_title <#biblio_IEC61217-2>`__.

GANTRY System
   See `biblioentry_title <#biblio_IEC61217-2>`__.

BEAM LIMITING DEVICE System
   See `biblioentry_title <#biblio_IEC61217-2>`__.

WEDGE FILTER system
   See `biblioentry_title <#biblio_IEC61217-2>`__.

X-RAY IMAGE RECEPTOR System
   See `biblioentry_title <#biblio_IEC61217-2>`__.

PATIENT SUPPORT System
   See `biblioentry_title <#biblio_IEC61217-2>`__.

TABLE TOP ECCENTRIC System
   See `biblioentry_title <#biblio_IEC61217-2>`__.

TABLE TOP System
   See `biblioentry_title <#biblio_IEC61217-2>`__.

Attribute Macro
   A set of Attributes that are described in a single table that is
   referenced by multiple Module or other tables.

P-Value
   .

Profile Connection Space Value
   A device independent color value that is created by the application
   of the transformation specified in an ICC profile.

Baseline Context Group Identifier
   .

Defined Context Group Identifier
   .

Context Group
   .

Context Group Version
   .

Context ID
   .

Mapping Resource
   .

Relationship Type
   .

DICOM Content Mapping Resource
   .

Template
   .

Template ID
   .

Value Set
   .

Baseline Template Identifier
   .

Defined Template Identifier
   .

Coding Scheme
   .

Digital Signature
   The definition is "Data appended to, or a cryptographic
   transformation of, a data unit that allows a recipient of the data
   unit to prove the source and integrity of that unit and protect
   against forgery e.g., by the recipient."

Data Confidentiality
   The definition is "the property that information is not made
   available or disclosed to unauthorized individuals, entities or
   processes."

Data Origin Authentication
   The definition is "the corroboration that the source of data received
   is as claimed."

Data Integrity
   The definition is "the property that data has not been altered or
   destroyed in an unauthorized manner."

Key Management
   The definition is "the generation, storage, distribution, deletion,
   archiving and application of keys in accordance with a security
   policy."

Security Context
   The definition is "security information that represents, or will
   represent a Security Association to an initiator or acceptor that has
   formed, or is attempting to form such an association."

Message Authentication Code
   .

Certificate
   .

Reference Coordinate System
   The RCS is the spatial coordinate system in a DICOM Frame of
   Reference. It is the chosen origin, orientation and spatial scale of
   an Image IE in a Cartesian space. The RCS is a right-handed Cartesian
   coordinate system i.e., the vector cross product of a unit vector
   along the positive x-axis and a unit vector along the positive y-axis
   is equal to a unit vector along the positive z-axis. The unit length
   is one millimeter. Typically, the Image IE contains a spatial mapping
   that specifies the relationship of the image samples to the Cartesian
   spatial domains of the RCS.

Ophthalmic Coordinate System
   The Ophthalmic Coordinate System is used as the Frame of Reference
   that establishes the spatial relationship relative to the corneal
   vertex. The corneal vertex is the point located at the intersection
   of the patient's line of sight (visual axis) and the corneal surface.
   See `Corneal Vertex Location <#sect_C.8.30.3.1.4>`__ for further
   explanation.

Fiducial
   A fiducial is some unique feature or landmark suitable as a spatial
   reference or correlation between similar objects. The fiducial may
   contribute to the definition of the origin and orientation of a
   chosen coordinate system. Identifying fiducials in different
   collections of data is a common means to establish the spatial
   relationship between similar objects.

Fiducial Point
   A Fiducial Point defines a specific location of a Fiducial. A
   Fiducial Point is relative to an image or to an RCS.

Multi-Planar Reconstruction
   Also called Multi-Planar Reformatting. A data visualization created
   by sampling volume data, typically represented by a stack of image
   planes, that lies in the neighborhood of the intersection of the
   volume with a plane, curved plane, slab or curved slab.

Planar Multi-Planar Reconstruction
   An MPR where the samples are centered on a single plane intersected
   with the volume.

Volumetric Presentation State
   A Presentation State that defines a transformation from 3D spatial
   input data (volume) to 2D spatial output data, with or without
   affecting other dimensions such as temporal.

Volumetric Presentation State Reference Coordinate System
   The Reference Coordinate System to which inputs to a Volumetric
   Presentation State are registered and to which Attribute Values of a
   Volumetric Presentation State are referenced (unless stated
   otherwise).

Volumetric Presentation View
   A presentation, with two spatial dimensions, of volume data.

Display System
   .

Display Subsystem
   A part of a Display System. A Display Subsystem consists of one
   Display Device and zero or more other devices (such as controllers).
   A Display System has one or more Display Subsystems.

Display Device
   See `biblioentry_title <#biblio_IEC62563-1>`__.

   .. note::

      The definition is "specific hardware/medium used to display images
      presented through an analogue or digital interface".

Digital Driving Level
   .

Unique Device Identifier
   An alphanumeric identifier issued by the unique device identification
   system established by the FDA to label and identify devices through
   distribution and use. See http://www.fda.gov/udi.

Content Item
   A node in the Content Tree of a DICOM SR document, consisting of
   either a container with a coded Concept Name, or a name-value pair
   with a coded Concept Name and a Concept Value.

Content Tree
   The tree of Content Items of a DICOM SR document.

Externally-Sourced Data Set
   A collection of data that has been obtained from or is defined by an
   entity separate from the system creating an object.

