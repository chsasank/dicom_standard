.. _chapter_AA:

Radiation Dose Reporting Use Cases (Informative)
================================================

.. _sect_AA.1:

Purpose of This Annex
---------------------

This Annex describes the use of the X-Ray Radiation Dose SR Object.
Multiple systems contributing to patient care during a visit may expose
the patient to irradiation during diagnostic and/ or interventional
procedures. Each of those equipments may record the dose in an X-Ray
Dose Reporting information object. Radiation safety information
reporting systems may take advantage of this information and create dose
reports for a visit, parts of a procedure performed or accumulation for
the patient in total, if information is completely available in a
structured content.

.. _sect_AA.2:

Definitions
-----------

**Irradiation Event**

An irradiation event is the loading of X-Ray equipment caused by a
single continuous actuation of the equipment's irradiation switch, from
the start of the loading time of the first pulse until the loading time
trailing edge of the final pulse. The irradiation event is the
"smallest" information entity to be recorded in the realm of Radiation
Dose reporting. Individual Irradiation Events are described by a set of
accompanying physical parameters that are sufficient to understand the
"quality" of irradiation that is being applied. This set of parameters
may be different for the various types of equipment that are able to
create irradiation events. Any on-off switching of the irradiation
source during the event is not treated as separate events, rather the
event includes the time between start and stop of irradiation as
triggered by the user. E.g., a pulsed fluoro X-Ray acquisition is
treated as a single irradiation event.

Irradiation events include all exposures performed on X-Ray equipment,
independent of whether a DICOM Image Object is being created. That is
why an irradiation event needs to be described with sufficient
Attributes to exchange the physical nature of irradiation applied.

**Accumulated Dose Values**

Accumulated Dose Values describe the integrated results of performing
multiple irradiation events. The scope of accumulation is typically a
study or a performed procedure step. Multiple Radiation Dose objects may
be created for one Study or one Radiation Dose object may be created for
multiple performed procedures.

.. _sect_AA.3:

Use Cases
---------

The following use cases illustrate the information flow between
participating roles and the possible capabilities of the equipment that
is performing in those roles. Each case will include a use case diagram
and denote the integration requirements. The diagrams will denote actors
(persons in role or other systems involved in the process of data
handling and/or storage). Furthermore, in certain cases it is assumed
that the equipment (e.g., Acquisition Modality) is capable of displaying
the contents of any dose reports it creates.

These use cases are only examples of possible uses for the Dose Report,
and are by no means exhaustive.

.. _sect_AA.3.1:

Basic Dose Reporting
~~~~~~~~~~~~~~~~~~~~

This is the basic use case for electronic dose reporting. See
`figure_title <#figure_AA.3-1>`__.

In this use case the user sets up the Acquisition Modality, and performs
the study. The Modality captures the irradiation event exposure
information, and encodes it together with the accumulated values in a
Dose Report. The Modality may allow the user to review the dose report,
and to add comments. The acquired images and Dose Report are sent to a
Long-Term Storage system (e.g., PACS) that is capable of storing Dose
Report objects.

A Display Station may retrieve the Dose Report from the Storage system,
and display it. Because the X-Ray Radiation Dose SR object is a proper
subset of the Enhanced SR object, the Display Station may render it
using the same functionality as used for displaying any Enhanced SR
object.

.. _sect_AA.3.2:

Dose Reporting For Non-digital Imaging
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Dose Report may also be used for image acquisitions using
non-digital Acquisition Modalities. See
`figure_title <#figure_AA.3-2>`__.

In this use case the user may manually enter the irradiation event
exposure information into a Dose Reporting Station, possibly
transcribing it from a dosimeter read-out display. The station encodes
the data in a Dose Report and sends it to a Storage system. The same
Dose Reporting Station may be used to support several acquisition
modalities.

This case may be useful in film-only radiography environments, or in
mixed film and digital environments, where the DICOM X-Ray Radiation
Dose SR Object provides a standard format for recording and storing
irradiation events.

Note that in a non-PACS environment, the Dose Reports may be sent to a
Long-Term Storage function built into a Radiation Safety workstation or
information system.

.. _sect_AA.3.3:

Dose Reporting Post-processing
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A specialized Radiation Safety workstation the may contribute to the
process of dose reporting in terms of more elaborate calculations or
graphical dose data displays, or by aggregating dose data over multiple
studies. See `figure_title <#figure_AA.3-3>`__. The Radiation Safety
workstation may or may not be integrated with the Long-Term Storage
function in a single system; such application entity architectural
decisions are outside the scope of DICOM, but DICOM services and
information objects do facilitate a variety of possible architectures.

The Radiation Safety workstation may be able to create specific reports
to respond to dose registry requirements, as established by local
regulatory authorities. These reports would generally not be in DICOM
format, but would be generated from the data in DICOM X-Ray Radiation
Dose SR objects.

The Radiation Safety workstation may also be used to generate more
elaborate reports on patient applied dose. The workstation may retrieve
the Dose Reports for multiple procedures performed on a particular
patient. A report of the cumulative dose for a specified time period, or
for a visit/admission, may be generated, encoded as a DICOM Dose Report,
and stored in the Long-Term Storage system. Any such further reports
will be stored in addition to the "basic report".

Note that such cumulative Dose Reports may describe irradiation events
that are also documented in other Dose Reports. The assignment of a UID
to each irradiation event allows the application to identify unique
irradiation events that may be reported in multiple objects. The
structure of the X-Ray Radiation Dose SR object also allows a cumulative
report to reference the contributing report objects using the
Predecessor Documents Sequence (0040,A360) Attribute.

An advanced application may be able to use the Dose Report data,
potentially supplemented by the data in the image objects referenced in
the Dose Report, to create a Dose Map that visualizes applied dose. Such
a Dose Map may be sent to the Long-Term Storage system using an
appropriate object format.

Other purposes of the Radiation Safety workstation may include
statistical analyses over all Dose Report Objects in order to gain
information for educational or quality control purposes. This may
include searches for Reports performed in certain time ranges, or with
specific equipment, or using certain protocols.

.. _sect_AA.3.4:

Dose Reporting Workflow Management
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The dose reporting workflow may be managed using the same DICOM services
used for managing the imaging workflow.

In particular, a Dose Report produced for an Acquisition Modality
Performed Procedure Step can be identified in the MPPS Referenced
Non-Image Composite SOP Instance Sequence (0040,0220).

