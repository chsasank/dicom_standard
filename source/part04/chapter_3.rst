.. _chapter_3:

Definitions
===========

For the purposes of this Standard the following definitions apply.

Application Entity
   See `biblioentry_title <#biblio_ISO7498-1>`__.

Service
   See `biblioentry_title <#biblio_ISO7498-1>`__.

Application Entity Title
   See `biblioentry_title <#biblio_ISO7498-1>`__.

Primitive
   See `biblioentry_title <#biblio_ISO8509>`__.

Attribute
   .

Command
   .

Data Dictionary
   .

Information Object
   .

Message
   .

Service-Object Pair Class
   .

DICOM Upper Layer Service
   .

DICOM Message Service Element
   .

DIMSE-N Services
   .

DIMSE-C Services
   .

DIMSE Service Group
   .

Attribute Tag
   .

Composite IOD
   .

DICOM Application Model
   .

DICOM Information Model
   .

Information Object Definition
   .

Module
   .

Normalized IOD
   .

Functional Group
   .

Conformance Statement
   .

Standard SOP Class
   .

Specialized SOP Class
   .

Standard Extended SOP Class
   .

Private SOP Class
   .

Standard Attribute
   .

Private Attribute
   .

Data Element
   .

Data Set
   .

Unique Identifier
   .

Classic Image Storage SOP Class
   An Image Storage SOP Class that is defined by an IOD that stores a
   single frame and defines the majority of the Attributes in the
   top-level Data Set.

Combined Print Image
   A pixel matrix created by superimposing an image and an overlay, the
   size of which is defined by the smallest rectangle enclosing the
   superimposed image and overlay.

Enhanced Image Storage SOP Class
   An Image Storage SOP Class that is defined by an IOD that stores
   multiple frames and defines the majority of the Attributes in
   Functional Group Sequences.

Legacy Converted Enhanced Image Storage SOP Class
   A modality-specific Enhanced Image Storage SOP Class that is defined
   by an IOD that defines only generic Functional Group Sequences, which
   does not require information that is not present in Classic Image
   Storage SOP Class Instances, and is intended for storage of converted
   Classic Image Storage SOP Class Instances when there is insufficient
   information to use a True Enhanced Image Storage SOP Class.

Meta Service-Object Pair Class
   A pre-defined set of SOP Classes that may be associated under a
   single SOP for the purpose of negotiating the use of the set with a
   single item.

Performed Procedure Step SOP Class
   Any SOP Class that encodes the details about the performance of a
   procedure step.

Performed Procedure Step SOP Instance
   An instance of a Performed Procedure Step SOP Class. Note that all
   UPS instances are instances of the UPS Push SOP Class, which is
   capable of encoding details about the performance of a procedure step
   (in addition to details about the scheduled procedure step) and thus
   qualify as an instance of a Performed Procedure Step SOP Class.

Preformatted Grayscale Image
   An image where all annotation, graphics, and grayscale
   transformations (up to and including the VOI LUT) expected in the
   printed image have been burnt in or applied before being sent to the
   SCP. It is a displayable image where the polarity of the intended
   display is specified by Photometric Interpretation (0028,0004).

Preformatted Color Image
   An image where all annotation, graphics, and color transformations
   expected in the printed image have been burnt in or applied before
   being sent to the SCP.

Real-World Activity
   That which exists in the real world that pertains to specific area of
   information processing within the area of interest of the DICOM
   Standard. Such a Real-World Activity may be represented by one or
   more computer information metaphors called SOP Classes.

Real-World Object
   That which exists in the real world upon which operations may be
   performed that are within the area of interest of the DICOM Standard.
   Such a Real-World Object may be represented through a computer
   information metaphor called a SOP Instance.

Related General SOP Class
   A SOP Class that is related to another SOP Class as being more
   generalized in terms of behavior defined in the Standard, and that
   may be used to identically encode an instance with the same
   Attributes and values, other than the SOP Class UID. In particular,
   this may be the SOP Class from which a Specialized SOP Class (see )
   is derived.

Service Class User
   The role played by a DICOM Application Entity (DIMSE-Service-User)
   that invokes operations and performs notifications on a specific
   Association.

Service Class Provider
   The role played by a DICOM Application Entity (DIMSE-Service-User)
   that performs operations and invokes notifications on a specific
   Association.

Service Class
   A collection of SOP Classes and/or Meta SOP Classes that are related
   in that they are described together to accomplish a single
   application.

Service-Object Pair Instance
   A concrete occurrence of an Information Object that is managed by a
   DICOM Application Entity and may be operated upon in a communication
   context defined by a specific set of DIMSE Services (on a network or
   interchange media). A SOP Instance is persistent beyond the context
   of its communication.

True Enhanced Image Storage SOP Class
   A modality-specific Enhanced Image Storage SOP Class that is defined
   by an IOD that defines modality-specific Functional Group Sequences,
   Attributes and sets of values, and is intended for creation by
   acquisition devices.

P-Value
   .

Profile Connection Space Value
   .

Origin-Server
   See `biblioentry_title <#biblio_RFC_7230>`__.

User-Agent
   See `biblioentry_title <#biblio_RFC_7230>`__.

