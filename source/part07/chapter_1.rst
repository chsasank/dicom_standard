.. _chapter_1:

Scope and Field of Application
==============================

This Part of the DICOM Standard specifies the DICOM Message Service
Element (DIMSE). The DIMSE defines an Application Service Element (both
the service and protocol) used by peer DICOM Application Entities for
the purpose of exchanging medical images and related information.

The DIMSE provides its services by relying on the DIMSE protocol. The
DIMSE protocol defines the encoding rules necessary to construct
Messages. A Message is composed of a Command Set (defined in this Part
of the DICOM Standard) followed by a conditional Data Set (defined in ).

This Part specifies:

-  a set of service primitives provided by the DIMSE Application Service
   Element

-  the parameters that are passed in each service primitive

-  any necessary information for the semantic description of each
   service primitive

-  the procedures applicable to the service primitives

-  the Abstract Syntax of the DICOM composite and normalized command
   protocol and the associated encoding rules to be applied

-  procedures for the correct interpretation of protocol control
   information

-  the conformance requirements to be met by implementation of this Part
   of the Standard

-  the Application Context required for DICOM Application Entities

-  the Association requirements of DICOM Application Entities

-  the Application Association Information for DICOM Application
   Entities

This Part is related to other parts of the DICOM Standard in that:

-  , Information Object Definitions, specifies the set of Information
   Object Definitions to which the services defined in this Part may be
   applied

-  , Data Structure and Encoding, addresses the encoding rules necessary
   to construct a conditional Data Set that is conveyed in a Message as
   specified in this Part

-  This Part defines the protocols and services required to accomplish
   the Service Classes described in

