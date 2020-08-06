.. _chapter_3:

Definitions
===========

Attribute
A property of an Information Object. An Attribute has a name and a value
that are independent of any encoding scheme.

Command
A request to operate on information across a network.

Command Element
An encoding of a parameter of a command that conveys this parameter's
value.

Command Stream
The result of encoding a set of DICOM Command Elements using the DICOM
encoding scheme.

Conformance Statement
A formal statement that describes a specific implementation of the DICOM
Standard. It specifies the Service Classes, Information Objects,
Communication Protocols, Security Profiles, and Media Storage
Application Profiles supported by the implementation.

Data Dictionary
A registry of DICOM Data Elements that assigns a unique tag, a name,
value characteristics, and semantics to each Data Element.

Data Element
A unit of information as defined by a single entry in the data
dictionary.

Data Set
Exchanged information consisting of a structured set of Attributes. The
value of each Attribute in a Data Set is expressed as a Data Element.

Data Stream
The result of encoding a Data Set using the DICOM encoding scheme (Data
Element Numbers and representations as specified by the Data
Dictionary).

Information Object
An abstraction of a real information entity (e.g., CT Image, Structured
Report, etc.) that is acted upon by one or more DICOM Commands.

.. note::

   This term is primarily used in PS3.1, with a few references in . It
   is an informal term corresponding to a formal term that is introduced
   in . In all other parts of the DICOM Standard this formal term is
   known as an Information Object Definition.

Information Object Class
A formal description of an Information Object, which includes a
description of its purpose and the Attributes it possesses. It does not
include values for these attributes.

.. note::

   This term is only used in PS3.1. It is an informal term corresponding
   to a formal term that is introduced in . This formal term is known as
   a Service-Object Pair Class or more commonly as a SOP Class.

Information Object Instance
A representation of an occurrence of a real-world entity, which includes
values for the Attributes of the Information Object Class to which the
entity belongs.

.. note::

   This term is only used in PS3.1. It is an informal term corresponding
   to a formal term that is introduced in . This formal term is known as
   a Service-Object Pair Instance or more commonly as a SOP Instance.

Message
A data unit of the Message Exchange Protocol exchanged between two
cooperating DICOM Applications. A Message is composed of a Command
Stream followed by an optional Data Stream.

Part
Subdivision of the DICOM Standard that covers related subject material.

Service Class
A structured description of a service that is supported by cooperating
DICOM Applications using specific DICOM Commands acting on a specific
class of Information Object.

Service-Object Pair Class
SOP Class
The pair of an Information Object and either a DIMSE Service Group, a
Media Storage Service, or a Web Service.

Essence
Video, audio or data type of source, as defined in
`biblioentry_title <#biblio_EBU-SMPTE-VSF_JT-NM_Phase2Report>`__.

Flow
A sequence of Grains from a Source; a concrete representation of content
emanating from the Source, as defined in
`biblioentry_title <#biblio_EBU-SMPTE-VSF_JT-NM_Phase2Report>`__.

Grain
Represents an element of Essence or other data associated with a
specific time, such as a frame, or a group of consecutive audio samples,
or captions, as defined in
`biblioentry_title <#biblio_EBU-SMPTE-VSF_JT-NM_Phase2Report>`__.

Rendition
A collection of time-synchronized Flows intended for simultaneous
presentation, providing a complete experience of a Source Group, as
defined in
`biblioentry_title <#biblio_EBU-SMPTE-VSF_JT-NM_Phase2Report>`__.

Source
An abstract concept that represents the primary origin of a Flow or set
of Flows, as defined in
`biblioentry_title <#biblio_EBU-SMPTE-VSF_JT-NM_Phase2Report>`__.

