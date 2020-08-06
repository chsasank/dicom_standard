.. _chapter_1:

Scope and Field of Application
==============================

This Part of the DICOM Standard specifies application specific subsets
of the DICOM Standard to which an implementation may claim conformance.
Such a conformance statement applies to the interoperable interchange of
medical images and related information on storage media for specific
clinical uses. It follows the framework, defined in , for the
interchange of various types of information on storage media.

This Part is related to other parts of the DICOM Standard in that:

-  , Conformance, specifies the general rules for assuring
   interoperability, which are applied for media interchange through the
   Application Profiles of this Part

-  , Information Object Definitions, specifies a number of Information
   Object Definitions (e.g., various types of images) that may be used
   in conjunction with this Part. It also defines a medical Directory
   structure to facilitate access to the objects stored on media

-  , Service Class Specifications, specifies the Media Storage Service
   Class upon which Application Profiles are built

-  , Data Structure and Encoding, addresses the encoding rules necessary
   to construct a Data Set that is encapsulated in a file as specified
   in

-  , Data Dictionary, contains an index by Tag of all Data Elements
   related to the Attributes of Information Objects defined in . This
   index includes the Value Representation and Value Multiplicity for
   each Data Element

-  , Media Storage and File Formats for Media Interchange, standardizes
   the overall open Storage Media architecture used by this Part,
   including the definition of a generic File Format, a Basic File
   Service and a Directory concept

-  , Media Formats and Physical Media, defines a number of standard
   Physical Media and corresponding Media Formats. These Media Formats
   and Physical Media selections are referenced by one or more of the
   Application Profiles of this Part. is intended to be extended as the
   technologies related to Physical Medium evolve

-  , Security Profiles defines a number of profiles for use with Secure
   DICOM Media Storage Application Profiles. The Media Storage Security
   Profiles specify the cryptographic techniques to be used for each
   Secure DICOM File in a Secure Media Storage Application Profile.

