.. _chapter_B:

Integration of Modality Worklist and Modality Performed Procedure Step in The Original DICOM Standard (Informative)
===================================================================================================================

This Annex was formerly located in in the 2003 and earlier revisions of
the Standard.

DICOM was published in 1993 and effectively addresses image
communication for a number of modalities and Image Management functions
for a significant part of the field of medical imaging. Since then, many
additional medical imaging specialties have contributed to the extension
of the DICOM Standard and developed additional Image Object Definitions.
Furthermore, there have been discussions about the harmonization of the
DICOM Real-World domain model with other standardization bodies. This
effort has resulted in a number of extensions to the DICOM Standard. The
integration of the Modality Worklist and Modality Performed Procedure
Step address an important part of the domain area that was not included
initially in the DICOM Standard. At the same time, the Modality Worklist
and Modality Performed Procedure Step integration make steps in the
direction of harmonization with other standardization bodies (CEN TC
251, HL7, etc.).

The purpose of this Annex is to show how the original DICOM Standard
relates to the extension for Modality Worklist Management and Modality
Performed Procedure Step. The two included figures outline the void
filled by the Modality Worklist Management and Modality Performed
Procedure Step specification, and the relationship between the original
DICOM Data Model and the extended model.

The management of a patient starts when the patient enters a physical
facility (e.g., a hospital, a clinic, an imaging center) or even before
that time. The DICOM Patient Management SOP Class provides many of the
functions that are of interest to imaging departments.
`figure_title <#figure_B-1>`__ is an example where one presumes that an
order for a procedure has been issued for a patient. The order for an
imaging procedure results in the creation of a Study Instance within the
DICOM Study Management SOP Class. At the same time (A) the Modality
Worklist Management SOP Class enables a modality operator to request the
scheduling information for the ordered procedures. A worklist can be
constructed based on the scheduling information. The handling of the
requested imaging procedure in DICOM Study Management and in DICOM
Worklist Management are closely related. The worklist also conveys
patient/study demographic information that can be incorporated into the
images.

Worklist Management is completed once the imaging procedure has started
and the Scheduled Procedure Step has been removed from the Worklist,
possibly in response to the Modality Performed Procedure Step (B).
However, Study Management continues throughout all stages of the Study,
including interpretation. The actual procedure performed (based on the
request) and information about the images produced are conveyed by the
DICOM Study Component SOP Class or the Modality Performed Procedure Step
SOP Classes.

`figure_title <#figure_B-2>`__ shows the relationship between the
original DICOM Real-World model and the extensions of this Real-World
model required to support the Modality Worklist and the Modality
Performed Procedure Step. The new parts of the model add entities that
are needed to request, schedule, and describe the performance of imaging
procedures, concepts that were not supported in the original model. The
entities required for representing the Worklist form a natural extension
of the original DICOM Real-World model.

Common to both the original model and the extended model is the Patient
entity. The Service Episode is an administrative concept that has been
shown in the extended model in order to pave the way for future
adaptation to a common model supported by other standardization groups
including HL7, CEN TC 251 WG 3, CAP-IEC, etc. The Visit is in the
original model but not shown in the extended model because it is a part
of the Service Episode.

There is a 1 to 1 relationship between a Requested Procedure and the
DICOM Study (A). A DICOM Study is the result of a single Requested
Procedure. A Requested Procedure can result in only one Study.

A n:m relationship exists between a Scheduled Procedure Step and a
Modality Performed Procedure Step (B). The concept of a Modality
Performed Procedure Step is a superset of the Study Component concept
contained in the original DICOM model. The Modality Performed Procedure
Step SOP Classes provide a means to relate Modality Performed Procedure
Steps to Scheduled Procedure Steps.

