.. _chapter_6:

Overview of The Content of The DICOM Standard
=============================================

.. _sect_6.1:

Document Structure
------------------

DICOM consists of the following parts:

-  PS3.1: Introduction and Overview (this document)

-  PS3.2: Conformance

-  PS3.3: Information Object Definitions

-  PS3.4: Service Class Specifications

-  PS3.5: Data Structures and Encoding

-  PS3.6: Data Dictionary

-  PS3.7: Message Exchange

-  PS3.8: Network Communication Support for Message Exchange

-  PS3.9: Retired

-  PS3.10: Media Storage and File Format for Media Interchange

-  PS3.11: Media Storage Application Profiles

-  PS3.12: Formats and Physical Media

-  PS3.13: Retired

-  PS3.14: Grayscale Standard Display Function

-  PS3.15: Security and System Management Profiles

-  PS3.16: Content Mapping Resource

-  PS3.17: Explanatory Information

-  PS3.18: Web Services

-  PS3.19: Application Hosting

-  PS3.20: Imaging Reports using HL7 Clinical Document Architecture

-  PS3.21: Transformations between DICOM and other Representations

-  PS3.22: Real-Time Communication (DICOM-RTV)

These parts of the Standard are related but independent documents. A
brief description of each Part is provided in this section.

.. _sect_6.2:

PS3.2: Conformance
------------------

of the DICOM Standard defines principles that implementations claiming
conformance to the Standard shall follow:

-  Conformance requirements. specifies the general requirements that
   must be met by any implementation claiming conformance. It references
   the conformance sections of other parts of the Standard.

-  Conformance Statement. defines the structure of a Conformance
   Statement. It specifies the information that must be present in a
   Conformance Statement. It references the Conformance Statement
   sections of other parts of the Standard.

does not specify a testing/validation procedure to assess an
implementation's conformance to the Standard.

`figure_title <#figure_6.2-1>`__ and `figure_title <#figure_6.2-2>`__
depict the construction process for a Conformance Statement for both
network communication and media exchange. A Conformance Statement
consists of the following parts:

-  Set of Information Objects that is recognized by this implementation

-  Set of Service Classes that this implementation supports

-  Set of communications protocols or physical media that this
   implementation supports

-  Set of security measures that this implementation supports.

.. _sect_6.3:

PS3.3: Information Object Definitions
-------------------------------------

of the DICOM Standard specifies a number of Information Object Classes
that provide an abstract definition of real-world entities applicable to
communication of digital medical images and related information (e.g.,
waveforms, structured reports, radiation therapy dose, etc.). Each
Information Object Class definition consists of a description of its
purpose and the Attributes that define it. An Information Object Class
does not include the values for the Attributes that comprise its
definition.

Two types of Information Object Classes are defined: normalized and
composite.

Normalized Information Object Classes include only those Attributes
inherent in the real-world entity represented. For example the study
Information Object Class, which is defined as normalized, contains study
date and study time Attributes because they are inherent in an actual
study. Patient name, however, is not an Attribute of the study
Information Object Class because it is inherent in the patient on which
the study was performed and not the study itself.

Composite Information Object Classes may additionally include Attributes
that are related to but not inherent in the real-world entity. For
example, the Computed Tomography Image Information Object Class, which
is defined as composite, contains both Attributes that are inherent in
the image (e.g., image date) and Attributes that are related to but not
inherent in the image (e.g., patient name). Composite Information Object
Classes provide a structured framework for expressing the communication
requirements of images where image data and related data needs to be
closely associated.

To simplify the Information Object Class definitions, the Attributes of
each Information Object Class are partitioned with similar Attributes
being grouped together. These groupings of Attributes are specified as
independent modules and may be reused by other Composite Information
Object Classes.

defines a model of the Real World along with the corresponding
Information Model that is reflected in the Information Object
Definitions. Future editions of this Standard may extend this set of
Information Objects to support new functionality.

To represent an occurrence of a real-world entity, an Information Object
Instance is created, which includes values for the Attributes of the
Information Object Class. The Attribute values of this Information
Object Instance may change over time to accurately reflect the changing
state of the entity that it represents. This is accomplished by
performing different basic operations upon the Information Object
Instance to render a specific set of services defined as a Service
Class. These Service Classes are defined in of the Standard.

.. _sect_6.4:

PS3.4: Service Class Specifications
-----------------------------------

of the DICOM Standard defines a number of Service Classes. A Service
Class associates one or more Information Objects with one or more
Commands to be performed upon these objects. Service Class
Specifications state requirements for Command Elements and how resulting
Commands are applied to Information Objects. Service Class
Specifications state requirements for both providers and users of
communications services.

of the DICOM Standard defines the characteristics shared by all Service
Classes, and how a Conformance Statement to an individual Service Class
is structured. It contains a number of normative annexes that describe
individual Service Classes in detail.

Examples of Service Classes include the following:

-  Storage Service Class

-  Query/Retrieve Service Class

-  Basic Worklist Management Service Class

-  Print Management Service Class.

defines the operations performed upon the Information Objects defined in
. defines the Commands and protocols for using the Commands to
accomplish the operations and notifications described in .

.. _sect_6.5:

PS3.5: Data Structure and Semantics
-----------------------------------

of the DICOM Standard specifies how DICOM applications construct and
encode the Data Set information resulting from the use of the
Information Objects and Services Classes defined in and of the DICOM
Standard. The support of a number of standard image compression
techniques (e.g., JPEG lossless and lossy) is specified.

addresses the encoding rules necessary to construct a Data Stream to be
conveyed in a Message as specified in of the DICOM Standard. This Data
Stream is produced from the collection of Data Elements making up the
Data Set.

also defines the semantics of a number of generic functions that are
common to many Information Objects. defines the encoding rules for
international character sets used within DICOM.

.. _sect_6.6:

PS3.6: Data Dictionary
----------------------

of the DICOM Standard is the centralized registry that defines the
collection of all DICOM Data Elements available to represent
information, along with elements utilized for interchangeable media
encoding and a list of uniquely identified items that are assigned by
DICOM.

For each element, specifies:

-  its unique tag, which consists of a group and element number,

-  its name,

-  its value representation (character string, integer, etc),

-  its value multiplicity (how many values per attribute),

-  whether it is retired.

For each uniquely identified item, specifies:

-  its unique value, which is numeric with multiple components separated
   by decimal points and limited to 64 characters,

-  its name,

-  its type, either Information Object Class, definition of encoding for
   data transfer, or certain well known Information Object Instances,

-  in which Part of the DICOM Standard it is defined.

.. _sect_6.7:

PS3.7: Message Exchange
-----------------------

of the DICOM Standard specifies both the service and protocol used by an
application in a medical imaging environment to exchange Messages over
the communications support services defined in . A Message is composed
of a Command Stream defined in followed by an optional Data Stream as
defined in .

specifies:

-  the operations and notifications (DIMSE Services) made available to
   Service Classes defined in ,

-  rules to establish and terminate associations provided by the
   communications support specified in , and the impact on outstanding
   transactions,

-  rules that govern the exchange of Command requests and responses,

-  encoding rules necessary to construct Command Streams and Messages.

.. _sect_6.8:

PS3.8: Network Communication Support For Message Exchange
---------------------------------------------------------

of the DICOM Standard specifies the communication services and the upper
layer protocols necessary to support, in a networked environment,
communication between DICOM applications as specified in , , , , and .
These communication services and protocols ensure that communication
between DICOM applications is performed in an efficient and coordinated
manner across the network.

The communication services specified in are a proper subset of the
services offered by the OSI Presentation Service (ISO 8822) and of the
OSI Association Control Service Element (ACSE) (ISO 8649). They are
referred to as the Upper Layer Service, which allows peer applications
to establish associations, transfer messages and terminate associations.

This definition of the Upper Layer Service specifies the use of the
DICOM Upper Layer Protocol in conjunction with TCP/IP transport
protocols.

The TCP/IP communication protocol specified by is a general purpose
communication protocol not specific to the DICOM Standard.
`figure_title <#figure_5-1>`__ shows this protocol stack.

.. _sect_6.9:

PS3.9: Retired (formerly Point-to-point Communication Support For Message Exchange)
-----------------------------------------------------------------------------------

PS3.9 of the DICOM Standard previously specified the services and
protocols used for point-to-point communications in a manner compatible
with ACR-NEMA 2.0. It has been retired.

.. _sect_6.10:

PS3.10 Media Storage and File Format for Media Interchange
----------------------------------------------------------

of the DICOM Standard specifies a general model for the storage of
medical imaging information on removable media (see
`figure_title <#figure_6.10-1>`__). The purpose of this Part is to
provide a framework allowing the interchange of various types of medical
images and related information on a broad range of physical storage
media.

.. note::

   See `figure_title <#figure_5-1>`__ for understanding how the media
   interchange model relates to the network model.

specifies:

-  a layered model for the storage of medical images and related
   information on storage media. This model introduces the concept of
   media storage application profiles, which specify application
   specific subsets of the DICOM Standard to which a media storage
   implementation may claim conformance. Such a conformance applies only
   to the writing, reading and updating of the content of storage media.

-  a DICOM file format supporting the encapsulation of any Information
   Object;

-  a secure DICOM file format supporting the encapsulation of a DICOM
   file format in a cryptographic envelope;

-  a DICOM file service providing independence from the underlying media
   format and physical media.

defines various media storage concepts:

-  the method to identify a set of files on a single medium;

-  the method for naming a DICOM file within a specific file system.

.. _sect_6.11:

PS3.11: Media Storage Application Profiles
------------------------------------------

of the DICOM Standard specifies application specific subsets of the
DICOM Standard to which an implementation may claim conformance. These
application specific subsets will be referred to as Application Profiles
in this section. Such a conformance statement applies to the
interoperable interchange of medical images and related information on
storage media for specific clinical uses. It follows the framework,
defined in , for the interchange of various types of information on
storage media.

An Application Profile annex is organized into the following major
parts:

-  The name of the Application Profile, or the list of Application
   Profiles grouped in a related class

-  A description of the clinical context of the Application Profile

-  The definition of the media storage Service Class with the device
   roles for the Application Profile and associated options

-  Informative section describing the operational requirements of the
   Application Profile

-  Specification of the Information Object Classes and associated
   Information Objects supported and the encoding to be used for the
   data transfer

-  The selection of media formats and physical media to be used

-  Other parameters that need to be specified to ensure interoperable
   media interchange

-  Security parameters that select the cryptographic techniques to be
   used with secure media storage Application Profiles

The structure of DICOM and the design of the Application Profile
mechanism is such that extension to additional Information Object
Classes and the new exchange media is straightforward.

.. note::

   `figure_title <#figure_6.11-1>`__ shows how individual aspects of an
   Application profile map to the various parts of the DICOM Standard.

.. _sect_6.12:

PS3.12: Storage Functions and Media Formats For Data Interchange
----------------------------------------------------------------

of the DICOM Standard facilitates the interchange of information between
applications in medical environments by specifying:

-  A structure for describing the relationship between the media storage
   model and a specific physical media and media format.

-  Specific physical media characteristics and associated media formats.

.. _sect_6.13:

PS3.13: Retired (formerly Print Management Point-to-point Communication Support)
--------------------------------------------------------------------------------

PS3.13 previously specified the services and protocols used for
point-to-point communication of print management services. It has been
retired.

.. _sect_6.14:

PS3.14: Grayscale Standard Display Function
-------------------------------------------

specifies a standardized display function for consistent display of
grayscale images. This function provides methods for calibrating a
particular display system for the purpose of presenting images
consistently on different display media (e.g., monitors and printers).

The chosen display function is based on human visual perception. Human
eye contrast sensitivity is distinctly non-linear within the luminance
range of display devices. This Standard uses Barten's model of the human
visual system.

.. _sect_6.15:

PS3.15: Security and System Management Profiles
-----------------------------------------------

of the DICOM Standard specifies security and system management profiles
to which implementations may claim conformance. Security and system
management profiles are defined by referencing externally developed
standard protocols, such as DHCP, LDAP, TLS and ISCL. Security protocols
may use security techniques like public keys and "smart cards". Data
encryption can use various standardized data encryption schemes.

This Part does not address issues of security policies. The Standard
only provides mechanisms that can be used to implement security policies
with regard to the interchange of DICOM objects. It is the local
administrator's responsibility to establish appropriate security
policies.

.. _sect_6.16:

PS3.16: Content Mapping Resource
--------------------------------

of the DICOM Standard specifies:

-  templates for structuring documents as DICOM Information Objects

-  sets of coded terms for use in Information Objects

-  a lexicon of terms defined and maintained by DICOM

-  country specific translations of coded terms

.. _sect_6.17:

PS3.17: Explanatory Information
-------------------------------

PS3.17 of the DICOM Standard specifies:

-  informative and normative annexes containing explanatory information

.. _sect_6.18:

PS3.18: Web Services
--------------------

of the DICOM Standard specifies the means whereby Web Services can be
used for retrieving or storing a DICOM object.

Requests that retrieve data specify the media type (format) of the
response body. Requests that store data specify the media type of the
request body.

The HTTP requests as defined within this Standard are sufficient for the
HTTP server to act as a DICOM SCU (Service Class User) to retrieve or
store the requested objects from an appropriate DICOM SCP (Service Class
Provider) using baseline DICOM functionality as defined in and , which
is to say that the HTTP server can act as a proxy for the DICOM SCP.

.. _sect_6.19:

PS3.19: Application Hosting
---------------------------

of the DICOM Standard specifies an Application Programming Interface
(API) to a DICOM based medical computing system into which programs
written to that standardized interface can "plug-in" (see
`figure_title <#figure_6.19-1>`__). A Hosting System implementer only
needs to create the standardized API once to support a wide variety of
add-on Hosted Applications.

In the traditional "plug-in" model, the "plug-in" is dedicated to a
particular host system (e.g., a web browsing program), and might not run
under other host systems (e.g., other web browsing programs). defines an
API that may be implemented by any Hosting System. A "plug-in" Hosted
Application written to the API would be able run in any environment
provided by a Hosting System that implements that API (see
`figure_title <#figure_6.19-2>`__).

specifies both the interactions and the Application Programming
Interfaces (API) between Hosting Systems and Hosted Applications. also
defines the data models that are used by the API.

.. _sect_6.20:

PS3.20: Imaging Reports using HL7 Clinical Document Architecture
----------------------------------------------------------------

of the DICOM Standard specifies templates for the encoding of imaging
reports using the HL7 Clinical Document Architecture Release 2 (CDA R2,
or simply CDA) Standard. Within this scope are clinical procedure
reports for specialties that use imaging for screening, diagnostic, or
therapeutic purposes.

constitutes an implementation guide for CDA, and is harmonized with the
approach to standardized templates for CDA implementation guides
developed by HL7. It also provides Business Names for data elements that
link data in user terminology, e.g., collected by a report authoring
application, to specific CDA encoded elements.

As an implementation guide for imaging reports, particular attention is
given to the use and reference of data collected in imaging procedures
as explicit evidence within reports. This data includes images,
waveforms, measurements, annotations, and other analytic results managed
as DICOM SOP Instances. Specifically, this Part includes a specification
for transformation into CDA documents of DICOM Structured Report
instances that represent imaging reports.

.. _sect_6.21:

PS3.21: Transformations between DICOM and other Representations
---------------------------------------------------------------

of the DICOM Standard specifies the transformations between DICOM and
other representations of the same information. Within its scope are
transformations to and from the NCI Annotation and Image Markup format.

.. _sect_6.22:

PS3.22: Real-Time Communication (DICOM-RTV)
-------------------------------------------

of the DICOM Standard specifies an
`biblioentry_title <#biblio_SMPTE_ST2110-10>`__ based service for the
real-time transport of DICOM metadata. It provides a mechanism for the
transport of DICOM metadata associated with a video or an audio flow
based on the `biblioentry_title <#biblio_SMPTE_ST2110-20>`__ and
`biblioentry_title <#biblio_SMPTE_ST2110-30>`__, respectively.

