.. _chapter_3:

Definitions
===========

For the purposes of this Standard the following definitions apply.

Application Entity
   See `biblioentry_title <#biblio_ISO7498-1>`__.

Application Entity Title
   See `biblioentry_title <#biblio_ISO7498-1>`__.

Protocol Data Unit
   See `biblioentry_title <#biblio_ISO7498-1>`__.

Transfer Syntax
   See `biblioentry_title <#biblio_ISO7498-1>`__.

Association
   See `biblioentry_title <#biblio_ISO8649>`__.

Association Initiator
   See `biblioentry_title <#biblio_ISO8649>`__.

Abstract Syntax
   See `biblioentry_title <#biblio_ISO8822>`__.

Abstract Syntax Name
   See `biblioentry_title <#biblio_ISO8822>`__.

Presentation Context
   See `biblioentry_title <#biblio_ISO8822>`__.

Transfer Syntax Name
   See `biblioentry_title <#biblio_ISO8822>`__.

Conformance Statement
   .

Information Object
   .

Service-Object Pair Class
   .

Information Object Definition
   .

Real-World Activity
   .

Service Class
   .

Service Class User
   .

Service Class Provider
   .

Meta Service-Object Pair Class
   .

Data Set
   .

DICOM Transfer Syntax
   .

Unique Identifier
   .

Extended Negotiation
   .

Implementation Class UID
   .

DICOM Upper Layer Service
   .

Presentation Address
   .

File-set
   .

File-set Creator
   .

File-set Reader
   .

File-set Updater
   .

Application Profile
   .

Standard SOP Class
   A SOP Class defined in the DICOM Standard that is used in an
   implementation with no modifications.

Standard Extended SOP Class
   A SOP Class defined in the DICOM Standard extended in an
   implementation with additional Type 3 Attributes. The additional
   Attributes may either be drawn from the Data Dictionary in , or may
   be Private Attributes. The semantics of the related Standard SOP
   Class shall not be modified by the additional Type 3 Attributes when
   absent. Therefore, the Standard Extended SOP Class utilizes the same
   UID as the related Standard SOP Class.

   .. note::

      IODs from a Standard Extended SOP Class may be freely exchanged
      between DICOM implementations since implementations that do not
      recognize the additional Type 3 Attributes would simply ignore
      them.

Specialized SOP Class
   A SOP Class derived from a Standard SOP Class that has been
   specialized in an implementation by additional Type 1, 1C, 2, 2C, or
   3 Attributes, by enumeration of specific permitted values for
   Attributes, or by enumeration of specific permitted Templates. The
   additional Attributes may either be drawn from the Data Dictionary in
   , or may be Private Attributes. The enumeration of permitted
   Attribute values or Templates shall be a subset of those permitted in
   the related Standard SOP Class. Since the semantics of the related
   Standard SOP Class may be modified by the additional Attributes, a
   Specialized SOP Class utilizes a Privately Defined UID that differs
   from the UID for the related Standard SOP Class.

   .. note::

      1. Since a Specialized SOP Class has a different UID than a
         Standard or Standard Extended SOP Class, other DICOM
         implementations may not recognize the Specialized SOP Class.
         Because of this limitation, a Specialized SOP Class should only
         be used when a Standard or Standard Extended SOP Class would
         not be appropriate. Before different implementations can
         exchange Instances in a Specialized SOP Class, the
         implementations must agree on the UID, content (in particular
         the additional Type 1, 1C, 2, and 2C Attributes), and semantics
         of the Specialized SOP Class. A Specialized SOP Class may be
         used to create a new or experimental SOP Class that is closely
         related to a Standard SOP Class.

      2. The Association Negotiation for a Specialized SOP Class may
         include a SOP Class Common Extended Negotiation Sub-Item (as
         defined in ) for identification of the Service Class and of the
         Related General SOP Class from which it was specialized. This
         may allow a receiving application, without prior agreement on
         the Specialized SOP Class IOD, to process Instances of that
         class as if they were instances of a Related General SOP Class.

Private SOP Class
   A SOP Class that is not defined in the DICOM Standard, but is
   published in an implementation's Conformance Statement.

   .. note::

      Since a Private SOP Class is not defined in the DICOM Standard,
      other DICOM implementations may not recognize the Private SOP
      Class. Because of this limitation, a Private SOP Class should only
      be used when a Standard or Standard Extended SOP Class would not
      be appropriate. In order for different implementations to exchange
      Instances in a Private SOP Class, the implementations must agree
      on the UID, content (in particular the Type 1, 1C, 2, and 2C
      Attributes), and semantics of the Private SOP Class. A Private SOP
      class may be used to create a totally new or experimental SOP
      Class.

Standard Attribute
   An Attribute defined in the Data Dictionary in .

Private Attribute
   An Attribute that is not defined in the DICOM Standard.

Standard Application Profile
   An Application Profile defined in the DICOM Standard that is used in
   an implementation with no modifications.

Augmented Application Profile
   An Application Profile derived from a Standard Application Profile by
   incorporating support for additional Standard or Standard Extended
   SOP Classes.

Private Application Profile
   An Application Profile that is not defined in the DICOM Standard, but
   is published in an implementation's Conformance Statement.

Security Profile
   A mechanism for selecting an appropriate set of choices from the
   Parts of the DICOM Standard along with corresponding security
   mechanisms (e.g., encryption algorithms) for the support of security
   facilities.

Transformation of DICOM SR to CDA
   A mechanism for mapping and transforming DICOM SR objects to HL7 CDA
   documents.

