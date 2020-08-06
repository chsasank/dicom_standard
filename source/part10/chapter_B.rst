.. _chapter_B:

HL7 Structured Document Files
=============================

Structured Documents as defined by an HL7 standard may be stored on
DICOM Interchange Media, and may be referenced from within DICOM SOP
Instances (including the DICOMDIR Media Storage Directory).

An Encapsulated CDA is referenced from the Media Storage Directory like
any other DICOM SOP Instance.

An HL7 Structured Document is an aggregate multimedia object, consisting
of a base XML-encoded document, plus zero or more multimedia components
(e.g., graphics) that are considered an integral part of the object. The
multimedia components shall be encoded in-line in the encapsulated XML
document unless they are references to other DICOM SOP Instances
contained on the media.
