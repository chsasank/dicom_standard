.. _chapter_1:

Scope and Field of Application
==============================

This Part of the DICOM Standard specifies a general model for the
storage of Medical Imaging information on removable media. The purpose
of this Part is to provide a framework allowing the interchange of
various types of medical images and related information on a broad range
of physical storage media.

This Part specifies:

a. a layered model for the storage of medical images and related
   information on storage media. This model introduces the concept of
   Media Storage Application Profiles, which specify application
   specific subsets of the DICOM Standard to which a Media Storage
   implementation may claim conformance. Such a conformance applies only
   to the writing, reading and updating of the content of storage media.
   Specific Application Profiles are not included in this Part but in ;

b. a DICOM File Format supporting the encapsulation of any Information
   Object Definition;

c. a Secure DICOM File Format supporting the encapsulation of a DICOM
   File Format in a cryptographic envelope;

d. a DICOM File Service providing independence from the underlying media
   format and physical media. The policies specific to the DICOMDIR file
   used to store the Media Storage Directory Service/Object Pair Class
   are also addressed.

This Part is related to other parts of the DICOM Standard in that:

-  , Conformance, specifies the requirements that shall be met to
   achieve DICOM Conformance in Media Storage;

-  , Information Object Definitions, specifies a number of Information
   Object Definitions (e.g., various types of images) that may be used
   in conjunction with this Part;

-  , builds upon this Part to define the Media Storage Service Class;

-  , Data Structure and Encoding, addresses the encoding rules necessary
   to construct a Data Set that is encapsulated in a file as specified
   in this Part;

-  , Data Dictionary, contains a registry by Tag of all Data Elements
   related to the Attributes of Information Objects defined in . This
   index includes the Value Representation and Value Multiplicity for
   each Data Element;

-  , Media Storage Application Profiles standardizes a number of choices
   related to a specific clinical need (selection of a Physical Medium
   and Media Format as well as specific Service/Object Pair Classes). It
   aims at facilitating the interoperability between implementations
   that claim conformance to the same Application Profile. is intended
   to be extended as the clinical needs for Media Storage Interchange
   evolve;

-  , Media Formats and Physical Media for Data Interchange, defines a
   number of selected Physical Medium and corresponding Media Formats.
   These Media Formats and Physical Medium selections are referenced by
   one or more of the Application Profiles of . is intended to be
   extended as the technologies related to Physical Medium evolve.

-  , Security Profiles defines a number of profiles for use with Secure
   DICOM Media Storage Application Profiles. The Media Storage Security
   Profiles specify the cryptographic techniques to be used for each
   Secure DICOM File in a Secure Media Storage Application Profile.

PS3.10 lays a foundation for open Media Interchange by standardizing an
overall architecture and addressing some of the major barriers to
interoperability: the definition of a DICOM File Format, a DICOM File
Service and the policies associated with a Media Storage Directory
structure.

.. note::

   specifies a general medical imaging Basic Directory Information
   Object Definition and specifies the corresponding Media Storage
   Directory SOP Class that is a member of the Media Storage Service
   Class.

Adherence to the provisions of PS3.10 by implementations reading,
writing or updating Storage Media represents a key foundation for open
Storage Media Interchange. However, it is only with the selection of
standard Physical Media and corresponding Media Formats in and the use
of specific Application Profiles in that effective Media Storage
Interchange interoperability is achieved. Therefore, claiming
conformance to PS3.10 only, is not a valid DICOM Conformance Statement.
DICOM Media Storage Conformance shall be made in relation to a
Application Profile according to the framework defined by .

