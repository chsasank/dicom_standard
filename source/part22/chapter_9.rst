.. _chapter_9:

Conformance
===========

An implementation claiming conformance to PS3.22 shall function in
accordance with all its mandatory sections.

DICOM-RTV Services are used to transmit in real-time Composite SOP
Instances. All Composite SOP Instances transmitted shall conform to the
requirements specified in other Parts of the Standard.

An implementation may conform to the DICOM-RTV Services by supporting
the role of origin device or receiving device, or both, for any of the
Services defined in PS3.22.

The structure of Conformance Statements is specified in .

An implementation shall describe in its Conformance Statement the
Real-World Activity associated with its use of DICOM-RTV Services,
including any proxy functionality between a DICOM-RTV and another
service provided through DIMSE Service or RESTful (i.e.; storage of
received video and audio with associated metadata).

In addition, the Conformance Statement document for a DICOM-RTV sending
device shall specify how the receivers can get the content of the SDP
objects describing the metadata and associated video and/or audio flows.
