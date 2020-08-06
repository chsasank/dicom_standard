.. _chapter_7:

Conformance Requirements
========================

An implementation claiming DICOM conformance may choose to support one
of the following:

-  network conformance according to `DICOM Networking Conformance
   Requirements <#sect_7.1>`__ (DICOM Network Conformance Requirements);

-  media storage conformance according to `DICOM Media Interchange
   Conformance Requirements <#sect_7.2>`__ (DICOM Media Storage
   Conformance Requirements);

-  both of the above.

.. _sect_7.1:

DICOM Networking Conformance Requirements
-----------------------------------------

An implementation claiming DICOM network conformance shall:

-  conform to the minimum conformance requirements defined in this
   section;

-  provide with the implementation a Conformance Statement structured
   according to the rules and policies in this Part including Annex A;

-  conform to at least one Standard or Standard Extended SOP class as
   defined in ;

.. note::

   Conformance to a Standard or Standard Extended SOP class implies
   conformance to the related IOD outlined in , the Data Elements
   defined in , and the operations and notifications defined in .

-  comply with the rules governing SOP Class types outlined in `Rules
   Governing Types of SOP Classes <#sect_7.3>`__;

-  accept a Presentation Context for the Verification SOP Class as an
   SCP if the implementation accepts any DICOM association requests;

-  produce and/or process Data Sets as defined in ;

.. note::

   Conformance to also implies conformance to .

-  obtain legitimate right to a registered <org id> for creating UIDs
   (see ) if an implementation utilizes Privately Defined UIDs (i.e.,
   UIDs not defined in the DICOM Standard);

-  support the following communication mode:

   -  TCP/IP (See ).

.. _sect_7.2:

DICOM Media Interchange Conformance Requirements
------------------------------------------------

An implementation claiming DICOM Media Interchange conformance shall:

-  conform to the minimum conformance requirements defined in this
   section;

-  provide with the implementation a Conformance Statement structured
   according to the rules and policies in this Part including
   `Conformance Statement Sample DICOMRis Interface
   (Informative) <#chapter_C>`__;

-  conform to at least one Standard Application Profile as defined in ;

-  support one of the Physical Media and associated Media Format, as
   specified by ;

-  comply with the rules governing SOP Class types outlined in `Rules
   Governing Types of SOP Classes <#sect_7.3>`__;

-  comply with the specific rules governing media storage Application
   Profile according to their types as specified in `Rules Governing
   Types of Application Profiles <#sect_7.4>`__. No other types of
   Application Profiles may be used;

-  read as an FSR or FSU all SOP Classes defined as mandatory by each of
   the supported Application Profiles encoded in any of the mandatory
   Transfer Syntaxes.

-  write as an FSC or FSU all SOP Classes defined as mandatory by each
   of the supported Application Profiles in one of the mandatory
   Transfer Syntaxes;

-  be able to gracefully ignore any Standard, Standard Extended,
   Specialized or Private SOP Classes that may be present on the Storage
   Medium but are not defined in any of the Application Profiles to
   which conformance is claimed.

.. note::

   There may be more than one Application Profile used to create or read
   a File-set on a single physical medium (e.g., a medium may have a
   File-set created with Standard and Augmented Application Profiles).

-  be able to gracefully ignore Directory Records in the DICOMDIR file
   that do not correspond to Directory Records defined in any of the
   Application Profiles to which conformance is claimed.

-  access the File-set(s) on media using the standard roles defined in ;

-  produce and/or process Data Sets as defined in encapsulated in DICOM
   Files;

.. note::

   Conformance to also implies conformance to

-  obtain legitimate right to a registered <org id> for creating UIDs
   (see ) if an implementation utilizes Privately Defined UIDs (i.e.,
   UIDs not defined in the DICOM Standard).

An implementation that does not meet all the above requirements shall
not claim conformance to DICOM for Media Storage Interchange.

.. _sect_7.3:

Rules Governing Types of SOP Classes
------------------------------------

Each SOP Class published in a Conformance Statement is one of four basic
types. Each SOP Class in an implementation claiming conformance to the
DICOM Standard shall be handled in accordance with the following rules,
as dictated by the type of SOP Class.

Standard SOP Classes conform to all relevant Parts of the DICOM Standard
with no additions or changes.

To claim conformance to a Standard SOP Class, an implementation shall
make a declaration of this fact in its Conformance Statement, and
identify its selected options, roles, and behavior.

Standard Extended SOP Classes shall:

a. be a proper super set of one Standard SOP Class;

b. not change the semantics of any Standard Attribute of that Standard
   SOP Class;

c. not contain any Private Type 1, 1C, 2, or 2C Attributes, nor add
   additional Standard Type 1, 1C, 2 or 2C Attributes;

d. not change any Standard Type 3 Attributes to Type 1, 1C, 2, or 2C;

e. use the same UID as the Standard SOP Class on which it is based.

A Standard Extended SOP Class may include Standard and/or Private Type 3
Attributes beyond those defined in the IOD on which it is based as long
as the Conformance Statement identifies the added Attributes and defines
their relationship with the information model. If additional Type 3
Attributes drawn from the Data Dictionary in are sent that affect the
encoding of other Attributes, or whose encoding depends on the values of
other Attributes, their presence and use shall be consistent.

.. note::

   E.g., An Attribute such as Pixel Padding Value (0028,0120) with a
   dictionary VR of US or SS would not be allowed to be present without
   Pixel Representation (0028,0103) also being present to resolve the
   encoding ambiguity. Further, Pixel Padding Value would not be allowed
   to be present in the absence of the Pixel Data (7FE0,0010) to which
   it applies.

An implementation claiming conformance with a Standard Extended SOP
Class shall identify in its Conformance Statement the Standard SOP Class
being extended, the options, roles, and behavior selected, and describe
the Attributes being added with the Standard SOP Class's IOD Model and
Modules.

Specialized SOP Classes shall:

a. be completely conformant to relevant Parts of the DICOM Standard;

b. be based on a Standard SOP Class, i.e.:

   -  contain all the Type 1, 1C, 2, and 2C Attributes of Standard SOP
      Class on which it is based;

   -  not change the semantics of any Standard Attribute;

   -  use a Privately Defined UID for its SOP Class (i.e., shall not be
      identified with a DICOM Defined UID);

c. be based on the DICOM Information Model in and .

Specialized SOP Classes may:

a. contain additional Standard and/or Private Type 1, 1C, 2, or 2C
   Attributes;

b. add Private and Standard Type 3 Attributes, which may or may not be
   published in the Conformance Statement.

   .. note::

      The usage of any unpublished Attributes may be ignored by other
      users and providers of the Specialized SOP Class.

c. enumerate the permitted values for Attributes within the set allowed
   by the Standard SOP Class;

d. enumerate the permitted Templates for Content Items within the set
   allowed by the Standard SOP Class.

An implementation claiming conformance with a Specialized SOP Class
shall include in its Conformance Statement the identity of the Standard
SOP Class being specialized, a description of usage of all Standard and
Private Type 1, 1C, 2, and 2C Attributes in the Specialized SOP Class, a
description of the constraints on Attributes values and Templates, and
the associated Privately Defined UID.

Private SOP Classes shall:

a. be completely conformant to relevant Parts of the DICOM Standard with
   the possible exception that support of the DICOM Default Transfer
   Syntax or a Transfer Syntax mandated by a media storage Application
   Profile is not required;

b. not change the specification of any Standard Attributes;

c. use a Privately Defined UID for its SOP Class (i.e., shall not be
   identified with a DICOM Defined UID);

d. not change existing DIMSE Services or create new ones;

e. not change existing DICOM File Services defined in or extend them in
   a manner that jeopardizes interoperability.

Private SOP Classes may:

a. use or apply DIMSE Services to privately defined or altered IODs
   (i.e., not necessarily be based on a Standard SOP Class);

b. use or apply Media Storage Operations to privately defined or altered
   IODs (i.e., not necessarily be based on a Standard SOP Class);

c. designate any Standard Attribute as Type 1, 1C, 2, or 2C regardless
   of the Type of the Attribute in other IODs;

d. define Private Attributes as Type 1, 1C, 2, or 2C;

e. include Private and Standard Type 3 Attributes, which may or may not
   be published in the Conformance Statement.

An implementation claiming conformance with a Private SOP Class shall
provide a , , and -like description of the Private SOP Class in the
implementation's Conformance Statement, including descriptions of the
usage of all Standard and Private Type 1, 1C, 2, or 2C Attributes in the
SOP Class, the DICOM Information Model, and the Privately Defined UIDs.

.. note::

   Unpublished SOP Classes (i.e., SOP Classes that are not defined in
   the DICOM Standard and are not defined in the Conformance Statement)
   are permitted in order to allow an implementation to support other
   abstract syntaxes within the DICOM Application Context. Such
   unpublished SOP Classes would utilize Privately Defined UIDs. The
   presence of an unpublished SOP Class does not prevent the
   implementation from being DICOM conformant but would have no meaning
   to other implementations and may be ignored.

.. _sect_7.4:

Rules Governing Types of Application Profiles
---------------------------------------------

Application Profile used in a Conformance Statement shall be of one of
three basic types. Each Application Profile in an implementation
claiming conformance to the DICOM Standard shall be handled in
accordance with the following rules, as dictated by the type of
Application Profile.

.. _sect_7.4.1:

Standard Application Profile
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A Standard Application Profile shall:

a. conform to all relevant Parts of DICOM with no changes;

b. support only one of the Physical Media and associated Media Format,
   as specified by .

To claim conformance to a Standard Application Profile, an
implementation shall make a declaration of this fact in its Conformance
Statement, and identify its selected options, roles, and behavior.

An implementation of a Standard Application Profile may extend Standard
SOP Classes of this Standard application profile. Such Standard Extended
SOP Classes shall meet the requirements specified in `Rules Governing
Types of SOP Classes <#sect_7.3>`__.

.. _sect_7.4.2:

Augmented Application Profile
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

An Augmented Application Profile shall:

a. be a proper super set of the Standard Application Profile. It adds
   the support of additional Standard or Standard Extended SOP Classes;

b. use the same Physical Media and its associated Media Format specified
   in the corresponding Standard Application Profile;

c. not include Specialized or Private SOP Classes.

An Augmented Application Profile may:

a. include one or more Standard or Standard Extended SOP Classes in
   addition to those of the corresponding Standard Application Profile.
   These additional SOP Classes may be mandatory or optional;

b. include the extensions (e.g., additional required keys, additional
   directory records) to the Basic Directory Information Object
   corresponding to the SOP Classes defined in a);

c. add one or more new roles (FSC, FSR, FSU).

To claim conformance to an Augmented Application Profile, an
implementation shall make a declaration of this fact in its Conformance
Statement, and shall identify the Standard Application Profile from
which it is derived and specify the augmentations. The implementation
shall also identify its selected options, roles, and behavior.

An implementation of a Augmented Application Profile may:

a. extend Standard SOP Classes of the corresponding Standard application
   profile. Such Standard Extended SOP Classes shall meet the
   requirements specified in `Rules Governing Types of SOP
   Classes <#sect_7.3>`__;

b. also claim conformance to the Standard Application Profile on which
   this Augmented Profile is based. In this case, FSC and FSU
   implementations shall be able to restrict their behavior to the
   Standard Application Profile (i.e., provide a means to write only the
   Standard or Standard Extended SOP Classes defined in the
   corresponding Standard Application Profile).

.. _sect_7.4.3:

Private Application Profile
~~~~~~~~~~~~~~~~~~~~~~~~~~~

A Private Application Profile:

-  conforms to and to the Media Storage Service Class specified in ;

-  support only one of the Physical Media and associated Media Format,
   as specified by ;

   .. note::

      The intent of these two conditions is to ensure that at least the
      DICOMDIR is readable by other APs.

-  complies with the rules governing SOP Classes in `Rules Governing
   Types of SOP Classes <#sect_7.3>`__.

To claim conformance to a Private Application Profile, an implementation
shall make a declaration of this fact in its Conformance Statement, and
shall provide a description of the Application Profile patterned after
the descriptions in . The implementation shall also identify its
selected options, roles, and behavior.

.. note::

   An implementation that does not meet the provisions of Section 7,
   including the types of Application Profile, is not conformant to
   DICOM and so is outside the scope of DICOM conformance. Such an
   implementation is not an Application Profile in DICOM terminology.
   For example, if an implementation chooses to write DICOM files onto
   media that is not in , or use a file system not defined for a
   specific media type in , then that implementation cannot claim that
   it conforms to the DICOM Standard using that media or file system.

.. _sect_7.5:

Conformance of DICOM Media
--------------------------

DICOM does not define conformance of a piece of medium in a generic
sense. DICOM conformance of a piece of medium can only be evaluated
within the scope of one or more media storage Application Profiles that
define specific contexts for interoperability.

.. note::

   One may accept the statement "this is a DICOM CD-R" when pointing to
   a storage medium. However, one should not state "this CD-R is DICOM
   conformant", but rather "this CD-R conforms to the Basic Cardiac
   X-ray Angiographic DICOM Application Profile".

.. _sect_7.6:

Security Profiles
-----------------

DICOM specifies methods for providing security at different levels of
the ISO OSI Basic Reference Model through the use of mechanisms specific
to a particular layer. The methods for applying these mechanisms are
described in the various parts of the DICOM Standard. Some mechanisms
and algorithms are specified in as Security Profiles. An
implementation's Conformance Statement describes which Security Profiles
can be used by that application.

.. note::

   For example, the Basic TLS Secure Transport Connection Profile
   defines a mechanism for authenticating entities participating in the
   exchange of data, and for protecting the integrity and
   confidentiality of information during interchange.

An implementation shall list in its Conformance Statement any Security
Profiles that it supports, how it selects which Security Profiles it
uses, how it uses features of that Security Profile, and any extensions
it makes to that Security Profile.

An implementation shall list in its Conformance Statement any additional
use of the User Identity association negotiation sub-item that is not
specified in a standard Security Profile.

.. _sect_7.7:

Transformation of DICOM SR to CDA
---------------------------------

DICOM specifies the transformation of DICOM SR objects to CDA documents
in .

This transformation is unidirectional (DICOM SR to HL7 CDA). Conformance
statements shall at a minimum state conformance to the top level
templates used for the SR document and the CDA document.

