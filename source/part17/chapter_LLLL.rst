.. _chapter_LLLL:

Imaging Agent Administration Report Template (Informative)
==========================================================

.. _sect_LLLL.1:

Purpose of this Annex
---------------------

This Annex describes some use cases of the contrast agent administration
reporting. The contrast agent administration report object records the
planned and performed delivery of contrast agents.

A Planned Imaging Agent Administration SR object is intended for
representing the plan or program to deliver contrast agent to the
patient for a contrast study. It could be prepared and customized for a
patient by the radiologist, prior to the study. The plan may also be
altered by the operating technologist prior to the study. For example,
the injection plan might be adjusted for patient's condition such as
weight. The plan is then loaded into the injector system to be
performed.

A Performed Imaging Agent Administration SR object is for reporting the
actual program that was used to deliver the contrast agent during the
study. During the study, the contrast-delivery system may alter the
original delivery plan as a result of events that occur during the
delivery of Imaging Agent such as limiting the flow rate due to high
pressure, aborting the injection due to adverse events, etc. The
Performed Image Agent Administration SR is then saved.

The infusion manager sends the Performed Imaging Agent Administration SR
to the PACS and optionally to other destinations like an acquisition
modality, RIS, or reporting system.

`figure_title <#figure_LLLL.1-1>`__ illustrates possible consumers of
the Performed Imaging Agent Administration SR object (referred as
"Imaging Agent Administration SR" in the figure) post administration.

.. _sect_LLLL.2:

Use Cases
---------

.. note::

   In the following use cases, the word event means a combination of
   injector and adverse events.

.. _sect_LLLL.2.1:

Use Case 1 - Manual Bolus Injection
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The use case shown in `figure_title <#figure_LLLL.2-1>`__ is an example
of how a performed object can capture a manual contrast infusion. The
operator performs a manual administration of contrast for a study. The
operator selects the patient from the contrast infusion manager
(available through modality worklist) and reports the minimum parameters
about the injection. The contrast infusion manager then generates a
Performed Imaging Administration SR object and sends to the Contrast
Usage Consumer such as PACS.

.. _sect_LLLL.2.2:

Use Case 2 - Automatic Infusion Pump - Contrast Reporting
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The use case shown in `figure_title <#figure_LLLL.2-2>`__ is an example
of how a performed object could be used for capturing an automatic
infusion. The technologist selects a patient at the infusion manager
from the work list available from the scheduling system and then
performs an automated administration of contrast for the selected
patient. The infusion manager records various events during the
administration. The data from the injector events and from the adverse
events that occurred during the administration are captured and obtained
by the infusion manager.

Upon completion of the administration procedure, the infusion manager
generates a Performed Imaging Agent Administration SR object using the
injection data obtained from the injection system and including the
events and updated parameters that were captured during the
administration. The generated report is then sent to the PACS and other
contrast usage consumers.

.. _sect_LLLL.2.3:

Use Case 3 - Protocoling
~~~~~~~~~~~~~~~~~~~~~~~~

The use case shown in `figure_title <#figure_LLLL.2-3>`__ is an example
of how a planned object could be used. The radiologist uses the
protocoling application in order to plan the contrast administration
protocol for a patient. The protocoling application outputs the planned
object into the infusion manager for immediate use or to the RIS or
PACS. The planned object is used by the technologist during the study.

.. _sect_LLLL.2.4:

Use Case 4 - Consumption of the Contrast Information by Reporting Systems for Automated Documentation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This use case gives an example of how a Performed Imaging Agent
Administration SR object could be used for capturing summary values of
contrast into a radiology reporting system. In this case, the radiology
reporting system would be a Contrast Usage Consumer
(`figure_title <#figure_LLLL.2-2>`__).

The most straightforward and ubiquitous need for the contrast
administration record is in the radiologist reporting workflow.
Inclusion of delivered contrast data into templates or sections of the
report is mandated in some regions of the world as evidence for billing
reconciliation. More generally, the radiologist can include this data
for completeness of study documentation. Ostensibly, contrast data
included in reports may be used to construct a longitudinal record of
contrast exposure for a patient undergoing multiple imaging studies.

Data of primary importance in this workflow are the summary values of
contrast administered to the patient (total volume of contrast, saline,
flow rate and concentration/type of contrast used). Often, information
describing the vascular access device used (e.g., catheter gauge) is
clinically relevant and/or mandated.

The guidance from ACR `biblioentry_title <#biblio_ACRCommPractice>`__
about the procedures and materials description in the report body
states, “The report should include a description of the studies and/or
procedures performed and any contrast media and/or radiopharmaceuticals
(including specific administered activities, concentration, volume, and
route of administration when applicable), medications, catheters, or
devices used, if not recorded elsewhere”.

.. _sect_LLLL.3:

Informative References
----------------------

ACR Communication American College of Radiology 2014 Resolution 11
http://www.acr.org/-/media/ACR/Files/Practice-Parameters/CommunicationDiag.pdf

