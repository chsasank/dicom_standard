.. _chapter_OOO:

Radiopharmaceutical Radiation Dose Structured Report (Informative)
==================================================================

.. _sect_OOO.1:

Purpose of This Annex
---------------------

This Annex describes the use of the Radiopharmaceutical Radiation Dose
(RRD) object. PET, Nuclear Medicine and other non-imaging procedures
necessitate that radiopharmaceuticals are administered to patients. The
RRD records the amount of activity and estimates patient dose.
Radiopharmaceuticals are often administered to patients several minutes
before the imaging step begins. A dose management system records the
amount of activity administered to the patients. Currently these systems
can be configured to receive patient information from HIS/RIS systems
via HL7 or DICOM messaging. `figure_title <#figure_OOO-1>`__
demonstrates a workflow for a "typical" Nuclear Medicine or PET
department.

.. _sect_OOO.2:

Real-World Nuclear Medicine and PET Radiopharmaceutical Radiation Dose (RRD) SR Workflow
----------------------------------------------------------------------------------------

`figure_title <#figure_OOO-2>`__ demonstrates a Hot Lab management
system as the RRD creator. It records the activity amount and the
administration time. It creates the RRD report and sends it to the
modality. Consistent time is required to accurately communicate activity
amount. The consistent time region highlights systems and steps where
accurate time reporting is essential. A DICOM Store moves the report to
the modality.

`figure_title <#figure_OOO-3>`__ demonstrates RRD workflow where a
radiopharmaceutical is administered to a patient for a non-imaging
procedure. The report is sent to the image manager/image archive for
storage and reporting.

`figure_title <#figure_OOO-4>`__ demonstrates when an infusion system or
a radioisotope generator is the RRD creator.

`figure_title <#figure_OOO-5>`__ is a UML sequence diagram to illustrate
steps for creation and downstream use case for Radiopharmaceutical
Radiation Dose report and CT dose report for the PET-CT system. The RRD
is stored to an image archive and retrieved by the PET-CT scanner.

`figure_title <#figure_OOO-6>`__ is a UML sequence diagram to illustrate
steps for creation and downstream use for radiopharmaceutical that is
administered when the modality starts acquisition. The diagram
illustrates that the dose report is reconciled with the image at later
time by an image processing step.

.. _sect_OOO.3:

Real-World Radiopharmaceutical and Radiopharmaceutical Components Identification
--------------------------------------------------------------------------------

The Radiopharmaceutical Radiation Dose (RRD) template provides a means
to report the radiopharmaceutical identification number and the
identification numbers of its components.

A typical use case is that when a radio-pharmacist elutes a radionuclide
from a generator into a vial. The radionuclide elution is given an
identification number (Radionuclide Vial Identifier). The pharmacists
then draws some radionuclide from the vial to compound with a reagent
(Reagent Vial Identifier) creating a multidose vial of a
radiopharmaceutical. The multidose vial is given identification number
(Radiopharmaceutical Lot Identifier). Individual doses are drawn from
the multidose vial for administration to patients. Each of the doses is
given an identification number (Radiopharmaceutical Identifier).

A second use case is that when a patient is prescribed 2 MBq of an oral
radiopharmaceutical. The radio-pharmacist dispenses two 1 MBq capsules.
Each capsule may have different lot number (Radiopharmaceutical Lot
Identifier). The two capsules are administered at the same time as one
dose (Radiopharmaceutical Identifier). The report may contain two
Radiopharmaceutical Lot Identifiers one for each capsule and one
radiopharmaceutical identifier for the dose.

`figure_title <#figure_OOO-7>`__ is a diagram the displays the
hierarchical relationship between the radiopharmaceutical dispense unit
identifier, radiopharmaceutical lot identifier, reagent vial identifier
and the radionuclide vial identifier.

