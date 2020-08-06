.. _chapter_CCCC:

Populating The Simplified Echo Procedure Report Template (Informative)
======================================================================

This Annex provides guidance to understand and populate the and its
sub-templates. For implementers familiar with the , which is largely
replaced by , some relationships and differences are also explained.

.. _sect_CCCC.1:

Structure Overview
------------------

Measurements in this template (except for the Wall Motion Analysis) are
collected into one of three containers, each with a specific
sub-template and constraints appropriate to the purpose of the
container.

-  Pre-coordinated Measurements

   -  Are fully standardized measurements (many taken from the ASE
      practice guidelines).

   -  Each has a single pre-coordinated standard code that fully
      captures the semantics of the measurement.

   -  The only modifiers permitted are to indicate coordinates where the
      measurement was taken, provide a brief display label, and indicate
      which of a set of repeated measurements is the preferred value.
      Other modifiers are not permitted.

-  Post-coordinated Measurements

   -  Are measurements for which DICOM has not established
      pre-coordinated codes, but that are performed with enough
      regularity to merit configuration and capturing the full semantics
      of the measurement. For example these measurements may include
      those configured on the Ultrasound System by the vendor or user
      site. Some of these may be variants of the Pre-coordinated
      Measurements.

   -  A set of mandatory and conditional modifiers with controlled
      vocabularies capture the essential semantics in a uniform way.

   -  A single pre-coordinated code is also provided so that when the
      same type of measurement is encountered in the future, it is not
      necessary to parse and evaluate the full constellation of modifer
      values. Since this measurement has not been fully standardized,
      the pre-coordinated code may use a private coding scheme (e.g.,
      from the vendor or user site).

-  Adhoc Measurements

   -  Are non-standardized measurements that do not merit the effort to
      track or configure all the details necessary to populate the set
      of modifiers required for a post-coordinated measurement.

   -  The measurement code describes the elementary property measured.

   -  Modifiers provide a brief display label and indicate coordinates
      where the measurement was taken. Other modifiers are not
      permitted.

.. _sect_CCCC.2:

Use Cases
---------

.. _sect_CCCC.2.1:

Use Case 1: Store and Extract Specific Measurement
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The user wishes to perform measurements on the Ultrasound System, store
them to the PACS and later have a specific measurement (say ABC)
automatically displayed in the overlay or automatically inserted into a
report page on the review system. This does not require the receiver to
understand any of the semantics of the measurement.

.. _sect_CCCC.2.1.1:

Configuration
^^^^^^^^^^^^^

The Ultrasound System is configured to encode a particular measurement
using a specific pre-coordinated code (and code meaning).

In the case of measurements from the Core Set, it is a well-known
pre-coordinated code (i.e., the code is in ), the full semantics are
well-known and the measurement will be recorded in . Likely most, if not
all, of the Core Set measurements come pre-configured on the Ultrasound
System.

In the case of vendor-specific or site-specific measurements, it is a
pre-coordinated code managed by the site or the vendor which is entered
and persisted on the Ultrasound System. Since the code is not
well-known, the measurement will be recorded in along with the modifiers
describing its semantics.

The receiver (i.e., the PACS display package or the reporting package)
is configured to associate the specific pre-coordinated code with a
location on the overlay or a slot in the report.

The form of the user interface for these capabilities is up to the
implementer.

.. _sect_CCCC.2.1.2:

Operation
^^^^^^^^^

The user takes measurements on the Ultrasound System, including
measurement ABC. All these measurements are recorded in the Simplified
Adult Echo SR object. If multiple instances of measurement ABC are
included, one of them may be flagged by the Ultrasound System by setting
the Selection Status for that instance to the reason it was selected as
the preferred value.

The Ultrasound System stores the SR object to the PACS.

The PACS or the reporting package retrieves the SR object and scans the
contents looking for measurements with the pre-coordinated code for
measurement ABC. If multiple instances are found, the receiver takes the
one for which the Selection Status has been set.

The receiver renders the measurement value to the display or report,
annotating it with the recorded Units, Code Meaning, and/or Short Label
as appropriate.

Note that in this use case the receiver handles the measurement in a
mechanical way. As long as the measurement can be unambiguously
identified, the semantics do not need to be understood by the receiver.

.. _sect_CCCC.2.2:

Use Case 2: Store and Process Measurements
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The user wishes to perform measurements on the Ultrasound System, store
them to the PACS and later perform processing of some or all of the
measurements on a CVIS (Cardiovascular Information System) or other
system. Processing may include incorporating measurements into a
database, performing trend analysis, plotting graphs, driving decision
support, etc. One measurement taken at end systole may be compared to
the "same" measurement that is taken at end diastole, etc. Measurements
at the same Finding Site might be collected together.

.. _sect_CCCC.2.2.1:

Configuration
^^^^^^^^^^^^^

As in Use Case 1, the Ultrasound System is configured to encode each
measurement using a specific pre-coordinated code (and code meaning).

Again, measurements from the Core Set use a well-known pre-coordinated
code and are recorded in while vendor-specific or site-specific
measurements use locally managed codes and are recorded in along with
the modifiers describing their semantics.

.. _sect_CCCC.2.2.2:

Operation
^^^^^^^^^

The user again takes measurements on the Ultrasound System which are
recorded in the Simplified Adult Echo SR object and if multiple
instances of a measurement are included, one of them may be flagged by
the Ultrasound System by setting the Selection Status for that instance
to the reason it was selected as the preferred value.

The Ultrasound System stores the SR object to the PACS.

The receiving database or processing system retrieves the SR object and
parses the contents. The contents of have known semantics and are
processed accordingly.

On first encounter, measurements in will likely have unfamiliar
pre-coordinated codes (since the pre-coordinated code in Row 1 of is not
taken from , but rather was likely produced by the vendor of the
Ultrasound System). Depending on the sophistication of the receiver,
parsing the modifiers may provide sufficient information for the
receiver to automatically handle the new measurement. If not, the
measurement can be put in an exception queue for a human operator to
review the values of the modifiers and decide how the measurement should
be handled. In between those two possibilities, the receiver may be able
to compare the modifier values of known measurements and provide the
operator with a partially categorized measurement.

In any case, once the semantics of the measurement are understood by the
receiver, the corresponding pre-coordinated code can be logged so that
future encounters with that measurement can be handled in an automated
fashion.

The receiver may also make use of the Selection Status values or may
database all the provided measurement values or allow the human to
select from the provided set.

Note that in this use case the receiver handles the measurements based
on the semantics associated with the measurement.

.. _sect_CCCC.3:

Differences of Note Between TID_5200 and TID 5300
-------------------------------------------------

.. _sect_CCCC.3.1:

Report Sections
~~~~~~~~~~~~~~~

In , containers and headings were used to facilitate the layout of
printed/displayed reports by collecting measurements into groups based
on concepts like anatomical region. Further, permitted Ultrasound
Systems to add new sections freely, does not. Section usage was a source
of problematic variability for receivers of . constrains this. When such
groupings are useful, for example when printing reports, it makes more
sense to configure it in one place (in the receiving database/reporting
system) rather than configuring such groupings independently (and
possibly inconsistently) on each ultrasound device in a department.
Receivers may choose to group measurements based on Finding Site or some
other logic as they see fit. This avoids the problem of trying to keep
many Ultrasound Systems in sync. SR objects are considered acquisition
data/evidence. If the findings are transcoded into CDA reports, sections
will likely be introduced in the CDA as appropriate.

.. _sect_CCCC.3.2:

Finding Observation Type
~~~~~~~~~~~~~~~~~~~~~~~~

The Finding Site is the location at which the measurement was taken.
While some measurements will be an observation of the structure of the
finding site itself, other measurements will be an observation of
something like flow, in which case the Finding Site is simply the
location, not the actual thing being observed/measured. To clarify this
distinction, Finding Observation Type was introduced in . For example,
when the measurement is a peak velocity and the Finding Site is a valve,
to distinguish between a measurement of the velocity of the blood
through the valve, and a measurement of the velocity of the valve
tissue, the Finding Observation Type would be set to "Hemodynamic
Measurement" or "Behavior of Finding Site" respectively.

.. _sect_CCCC.4:

Usage Guidance
--------------

.. _sect_CCCC.4.1:

Finding Site
~~~~~~~~~~~~

Modifiers are not permitted on the Finding Site in since such modifiers
resulted in different ways of encoding the same concept. requires the
use of a single anatomical code that fully pre-coordinates the location
details of the measurement. has proven to be sufficient to encode the
ASE Core Set of measurements. Implementers are strongly recommended to
using codes from that list. If there is a truly significant location
detail that needs to be captured, e.g., to identify a specific segment
of the atrial wall, or a specific leaf of a valve as the location of the
measurement, then the implementer may introduce a new code ( is
extensible) or better yet, new codes can be added to through a DICOM
Change Proposal.

.. _sect_CCCC.4.2:

Measured Property
~~~~~~~~~~~~~~~~~

The codes in have also proven to be sufficient to encode the ASE Core
Set of measurements. It is expected that the majority of vendor-specific
or site-specific measurements can also be encoded using these
properties, but it is understandable that some additional codes may be
needed. When introducing new codes, implementers should be careful not
to introduce elements of the other modifiers, such as Finding Site or
Cardiac Cycle Point, into the Measured Property. For example, do not
introduce a property for Diastolic Atrial Length to be used for the left
and right atria, rather for such a measurement, use Property=Length,
Cardiac Cycle Point=End Diastole and Finding Site=Left Atrium or Right
Atrium respectively.

.. _sect_CCCC.4.3:

Image View
~~~~~~~~~~

Implementers may use codes for image views beyond those listed in D as
needed, but note that Image View is only recorded if it is significant
to the interpretation of the measurement. Inclusion of the Image View
will likely isolate the measurement from other measurements of the same
feature taken in different views.

.. _sect_CCCC.4.4:

Cardiac Cycle Point
~~~~~~~~~~~~~~~~~~~

Note that (111973004, SCT, "Systole") is used here to refer to the
entire duration of ventricular systole, while (416430001, SCT, "End
Systole") is used to refer to the point in time where the aortic valve
closes (or in the case of the right ventricle, the pulmonary valve).
Therefore, a Vmax measurement for systole would mean the maximum
velocity over the period of systole, and a Vmax measurement for end
systole would mean the maximum velocity at the time point of end
systole.

.. _sect_CCCC.4.5:

Measurement Method
~~~~~~~~~~~~~~~~~~

This distinguishes between two measurements that convey the same
concept, but are obtained or derived in a different way. As with the
Image View, this is only recorded if it is significant to the
interpretation of the measurement.

.. _sect_CCCC.4.6:

Selection Status
~~~~~~~~~~~~~~~~

This is used to flag the preferred value when multiple instances of the
same measurement are recorded in the SR object. Using this to
communicate the value preferred by the operator or the Ultrasound System
is very useful for receivers that lack the logic to make a selection
themselves. In cases where there is no need or value in sending multiple
instances of the same measurement, the issue can be avoided by only
sending a single instance of any given measurement in the SR object.

.. _sect_CCCC.4.7:

Additional Modifiers
~~~~~~~~~~~~~~~~~~~~

The concept modifiers in the template are sufficient to accurately
encode all the best practice echo measurements recommended by the ASE.
Although is extensible and adding new modifiers is not prohibited, the
meaning and significance of such new modifiers will generally not be
understood by receiving systems, delaying or preventing import of such
measurements. Further, adding modifiers that replicate the meaning of an
existing modifier is prohibited.

.. _sect_CCCC.5:

Example
-------

+------+---------------+------------+---------------+---------------+
| Nest | Relationship  | Value Type | Concept Name  | Example Value |
+======+===============+============+===============+===============+
|      |               | CONTAINER  | Adult         |               |
|      |               |            | Ech           |               |
|      |               |            | ocardiography |               |
|      |               |            | Procedure     |               |
|      |               |            | Report        |               |
+------+---------------+------------+---------------+---------------+
| >    | CONTAINS      | CONTAINER  | (125301, DCM, |               |
|      |               |            | "Pr           |               |
|      |               |            | e-coordinated |               |
|      |               |            | M             |               |
|      |               |            | easurements") |               |
+------+---------------+------------+---------------+---------------+
| >>   | CONTAINS      | NUM        | `(79969-2,    | 1.00          |
|      |               |            | LN,           | (             |
|      |               |            | "Int          | cm,UCUM,"cm") |
|      |               |            | erventricular |               |
|      |               |            | septum        |               |
|      |               |            | diastolic     |               |
|      |               |            | dim           |               |
|      |               |            | ension") <htt |               |
|      |               |            | p://loinc.org |               |
|      |               |            | /79969-2/>`__ |               |
+------+---------------+------------+---------------+---------------+
| >>>  | HAS           | TEXT       | (125309, DCM, | "IVSd (2D) "  |
|      | PROPERTIES    |            | "Short        |               |
|      |               |            | Label")       |               |
+------+---------------+------------+---------------+---------------+
| >>   | CONTAINS      | NUM        | `(79991-6,    | 70.3          |
|      |               |            | LN, "Left     | (%,UCUM,"%")  |
|      |               |            | ventricular   |               |
|      |               |            | ejection      |               |
|      |               |            | fraction      |               |
|      |               |            | biplane (MOD) |               |
|      |               |            | ") <htt       |               |
|      |               |            | p://loinc.org |               |
|      |               |            | /79991-6/>`__ |               |
+------+---------------+------------+---------------+---------------+
| >>>  | HAS           | TEXT       | (125309, DCM, | "LV EF (MOD)  |
|      | PROPERTIES    |            | "Short        | "             |
|      |               |            | Label")       |               |
+------+---------------+------------+---------------+---------------+
| >>   | CONTAINS      | NUM        | `(79996-5,    | 118           |
|      |               |            | LN, "Left     | (             |
|      |               |            | ventricular   | ml,UCUM,"ml") |
|      |               |            | end diastolic |               |
|      |               |            | volume        |               |
|      |               |            | biplane (MOD) |               |
|      |               |            | ") <htt       |               |
|      |               |            | p://loinc.org |               |
|      |               |            | /79996-5/>`__ |               |
+------+---------------+------------+---------------+---------------+
| >>>  | HAS           | TEXT       | (125309, DCM, | "LV EDV (MOD) |
|      | PROPERTIES    |            | "Short        | "             |
|      |               |            | Label")       |               |
+------+---------------+------------+---------------+---------------+
| >>   | CONTAINS      | NUM        | `(80001-1,    | 35.0          |
|      |               |            | LN, "Left     | (             |
|      |               |            | ventricular   | ml,UCUM,"ml") |
|      |               |            | end systolic  |               |
|      |               |            | volume        |               |
|      |               |            | biplane (MOD) |               |
|      |               |            | ") <htt       |               |
|      |               |            | p://loinc.org |               |
|      |               |            | /80001-1/>`__ |               |
+------+---------------+------------+---------------+---------------+
| >>>  | HAS           | TEXT       | (125309, DCM, | "LV ESV (MOD) |
|      | PROPERTIES    |            | "Short        | "             |
|      |               |            | Label")       |               |
+------+---------------+------------+---------------+---------------+
| >>   | CONTAINS      | NUM        | `(80007-8,    | 5.00          |
|      |               |            | LN, "Left     | (             |
|      |               |            | ventricular   | cm,UCUM,"cm") |
|      |               |            | internal      |               |
|      |               |            | diastolic     |               |
|      |               |            | dimension -   |               |
|      |               |            | 2D") <htt     |               |
|      |               |            | p://loinc.org |               |
|      |               |            | /80007-8/>`__ |               |
+------+---------------+------------+---------------+---------------+
| >>>  | HAS           | CODE       | (121404, DCM, | (121410, DCM, |
|      | PROPERTIES    |            | "Selection    | "User chosen  |
|      |               |            | Status")      | value")       |
+------+---------------+------------+---------------+---------------+
| >>>  | HAS           | TEXT       | (125309, DCM, | "LVIDd (2D) " |
|      | PROPERTIES    |            | "Short        |               |
|      |               |            | Label")       |               |
+------+---------------+------------+---------------+---------------+
| >>   | CONTAINS      | NUM        | `(80007-8,    | 5.50          |
|      |               |            | LN, "Left     | (             |
|      |               |            | ventricular   | cm,UCUM,"cm") |
|      |               |            | internal      |               |
|      |               |            | diastolic     |               |
|      |               |            | dimension -   |               |
|      |               |            | 2D") <htt     |               |
|      |               |            | p://loinc.org |               |
|      |               |            | /80007-8/>`__ |               |
+------+---------------+------------+---------------+---------------+
| >>>  | HAS           | TEXT       | (125309, DCM, | "LVIDd (2D) " |
|      | PROPERTIES    |            | "Short        |               |
|      |               |            | Label")       |               |
+------+---------------+------------+---------------+---------------+
| >>   | CONTAINS      | NUM        | `(80007-8,    | 6.00          |
|      |               |            | LN, "Left     | (             |
|      |               |            | ventricular   | cm,UCUM,"cm") |
|      |               |            | internal      |               |
|      |               |            | diastolic     |               |
|      |               |            | dimension -   |               |
|      |               |            | 2D") <htt     |               |
|      |               |            | p://loinc.org |               |
|      |               |            | /80007-8/>`__ |               |
+------+---------------+------------+---------------+---------------+
| >>>  | HAS           | TEXT       | (125309, DCM, | "LVIDd (2D) " |
|      | PROPERTIES    |            | "Short        |               |
|      |               |            | Label")       |               |
+------+---------------+------------+---------------+---------------+
| >>   | CONTAINS      | NUM        | `(80011-0,    | 3.00          |
|      |               |            | LN, "Left     | (             |
|      |               |            | ventricular   | cm,UCUM,"cm") |
|      |               |            | internal      |               |
|      |               |            | systolic      |               |
|      |               |            | dimension -   |               |
|      |               |            | 2D") <htt     |               |
|      |               |            | p://loinc.org |               |
|      |               |            | /80011-0/>`__ |               |
+------+---------------+------------+---------------+---------------+
| >>>  | HAS           | TEXT       | (125309, DCM, | "LVIDs (2D) " |
|      | PROPERTIES    |            | "Short        |               |
|      |               |            | Label")       |               |
+------+---------------+------------+---------------+---------------+
| >>   | CONTAINS      | NUM        | `(80031-8,    | 1.00          |
|      |               |            | LN, "Left     | (             |
|      |               |            | ventricular   | cm,UCUM,"cm") |
|      |               |            | posterior     |               |
|      |               |            | wall          |               |
|      |               |            | diastolic     |               |
|      |               |            | thi           |               |
|      |               |            | ckness") <htt |               |
|      |               |            | p://loinc.org |               |
|      |               |            | /80031-8/>`__ |               |
+------+---------------+------------+---------------+---------------+
| >>>  | HAS           | TEXT       | (125309, DCM, | "LVPWd (2D) " |
|      | PROPERTIES    |            | "Short        |               |
|      |               |            | Label")       |               |
+------+---------------+------------+---------------+---------------+
| >>   | CONTAINS      | NUM        | `(80068-0,    | 4.82          |
|      |               |            | LN, "Mitral   | (cm           |
|      |               |            | valve area    | 2,UCUM,"cm2") |
|      |               |            | (Planimetry)  |               |
|      |               |            | ") <htt       |               |
|      |               |            | p://loinc.org |               |
|      |               |            | /80068-0/>`__ |               |
+------+---------------+------------+---------------+---------------+
| >>>  | HAS           | TEXT       | (125309, DCM, | "MV Area      |
|      | PROPERTIES    |            | "Short        | (Planim) "    |
|      |               |            | Label")       |               |
+------+---------------+------------+---------------+---------------+
| >    | CONTAINS      | CONTAINER  | (125302, DCM, |               |
|      |               |            | "Pos          |               |
|      |               |            | t-coordinated |               |
|      |               |            | M             |               |
|      |               |            | easurements") |               |
+------+---------------+------------+---------------+---------------+
| >>   | CONTAINS      | NUM        | (L            | 39            |
|      |               |            | VSIMOD,99Comp | (ml/m2,       |
|      |               |            | anyName,"Left | UCUM,"ml/m2") |
|      |               |            | Ventricle     |               |
|      |               |            | Stroke Index  |               |
|      |               |            | (MOD) ")      |               |
+------+---------------+------------+---------------+---------------+
| >>>  | HAS CONCEPT   | CODE       | (125306, DCM, | (125313, DCM, |
|      | MOD           |            | "Measurement  | "Indexed")    |
|      |               |            | Type")        |               |
+------+---------------+------------+---------------+---------------+
| >>>  | HAS CONCEPT   | CODE       | `(363698007,  | `(87878005,   |
|      | MOD           |            | SCT, "Finding | SCT, "Left    |
|      |               |            | Site          | Ventricl      |
|      |               |            | ") <http://sn | e") <http://s |
|      |               |            | omed.info/id/ | nomed.info/id |
|      |               |            | 363698007>`__ | /87878005>`__ |
+------+---------------+------------+---------------+---------------+
| >>>  | HAS CONCEPT   | CODE       | (125305, DCM, | `(44324008,   |
|      | MOD           |            | "Finding      | SCT,          |
|      |               |            | Observation   | "Hemodynamic  |
|      |               |            | Type")        | Measurement   |
|      |               |            |               | s") <http://s |
|      |               |            |               | nomed.info/id |
|      |               |            |               | /44324008>`__ |
+------+---------------+------------+---------------+---------------+
| >>>  | HAS CONCEPT   | CODE       | (125307, DCM, | `(90096001,   |
|      | MOD           |            | "Measured     | SCT, "Stroke  |
|      |               |            | Property")    | Volum         |
|      |               |            |               | e") <http://s |
|      |               |            |               | nomed.info/id |
|      |               |            |               | /90096001>`__ |
+------+---------------+------------+---------------+---------------+
| >>>  | HAS CONCEPT   | CODE       | `(370129005,  | (125207, DCM, |
|      | MOD           |            | SCT,          | "Method of    |
|      |               |            | "Measurement  | Disks         |
|      |               |            | Method        | Biplane")     |
|      |               |            | ") <http://sn |               |
|      |               |            | omed.info/id/ |               |
|      |               |            | 370129005>`__ |               |
+------+---------------+------------+---------------+---------------+
| >>>  | HAS CONCEPT   | CODE       | `(399264008,  | `(399064001,  |
|      | MOD           |            | SCT, "Image   | SCT, "2D      |
|      |               |            | Mode          | Mode          |
|      |               |            | ") <http://sn | ") <http://sn |
|      |               |            | omed.info/id/ | omed.info/id/ |
|      |               |            | 399264008>`__ | 399064001>`__ |
+------+---------------+------------+---------------+---------------+
| >>>  | HAS CONCEPT   | CODE       | (125308, DCM, | `(8277-6, LN, |
|      | MOD           |            | "Measurement  | "Body Surface |
|      |               |            | Divisor")     | Area") <ht    |
|      |               |            |               | tp://loinc.or |
|      |               |            |               | g/8277-6/>`__ |
+------+---------------+------------+---------------+---------------+
| >>>  | HAS           | TEXT       | (125309, DCM, | "LV SI (MOD)  |
|      | PROPERTIES    |            | "Short        | "             |
|      |               |            | Label")       |               |
+------+---------------+------------+---------------+---------------+
| >>   | CONTAINS      | NUM        | `(29469-4,    | 3.0           |
|      |               |            | LN, "Left     | (             |
|      |               |            | Atrium        | cm,UCUM,"cm") |
|      |               |            | Ant           |               |
|      |               |            | ero-posterior |               |
|      |               |            | Systolic      |               |
|      |               |            | Dim           |               |
|      |               |            | ension") <htt |               |
|      |               |            | p://loinc.org |               |
|      |               |            | /29469-4/>`__ |               |
+------+---------------+------------+---------------+---------------+
| >>>  | HAS CONCEPT   | CODE       | (125306, DCM, | (125316, DCM, |
|      | MOD           |            | "Measurement  | "Directly     |
|      |               |            | Type")        | measured")    |
+------+---------------+------------+---------------+---------------+
| >>>  | HAS CONCEPT   | CODE       | `(363698007,  | `(82471001,   |
|      | MOD           |            | SCT, "Finding | SCT, "Left    |
|      |               |            | Site          | Atriu         |
|      |               |            | ") <http://sn | m") <http://s |
|      |               |            | omed.info/id/ | nomed.info/id |
|      |               |            | 363698007>`__ | /82471001>`__ |
+------+---------------+------------+---------------+---------------+
| >>>  | HAS CONCEPT   | CODE       | (125305, DCM, | (125311, DCM, |
|      | MOD           |            | "Finding      | "Structure of |
|      |               |            | Observation   | the Finding   |
|      |               |            | Type")        | Site")        |
+------+---------------+------------+---------------+---------------+
| >>>  | HAS CONCEPT   | CODE       | (125307, DCM, | `(81827009,   |
|      | MOD           |            | "Measured     | SCT,          |
|      |               |            | Property")    | "Diamete      |
|      |               |            |               | r") <http://s |
|      |               |            |               | nomed.info/id |
|      |               |            |               | /81827009>`__ |
+------+---------------+------------+---------------+---------------+
| >>>  | HAS CONCEPT   | CODE       | `(370129005,  | (122675, DCM, |
|      | MOD           |            | SCT,          | "Anterio      |
|      |               |            | "Measurement  | r-Posterior") |
|      |               |            | Method        |               |
|      |               |            | ") <http://sn |               |
|      |               |            | omed.info/id/ |               |
|      |               |            | 370129005>`__ |               |
+------+---------------+------------+---------------+---------------+
| >>>  | HAS CONCEPT   | CODE       | `(399264008,  | `(399064001,  |
|      | MOD           |            | SCT, "Image   | SCT, "2D      |
|      |               |            | Mode          | Mode          |
|      |               |            | ") <http://sn | ") <http://sn |
|      |               |            | omed.info/id/ | omed.info/id/ |
|      |               |            | 399264008>`__ | 399064001>`__ |
+------+---------------+------------+---------------+---------------+
| >>>  | HAS CONCEPT   | CODE       | `(272518008,  | `(416430001,  |
|      | MOD           |            | SCT, "Cardiac | SCT, "End     |
|      |               |            | Cycle         | Systole       |
|      |               |            | Point         | ") <http://sn |
|      |               |            | ") <http://sn | omed.info/id/ |
|      |               |            | omed.info/id/ | 416430001>`__ |
|      |               |            | 272518008>`__ |               |
+------+---------------+------------+---------------+---------------+
| >>>  | HAS           | TEXT       | (125309, DCM, | "LA Dimen     |
|      | PROPERTIES    |            | "Short        | (2D) "        |
|      |               |            | Label")       |               |
+------+---------------+------------+---------------+---------------+
| >    | CONTAINS      | CONTAINER  | (125303, DCM, |               |
|      |               |            | "Adhoc        |               |
|      |               |            | M             |               |
|      |               |            | easurements") |               |
+------+---------------+------------+---------------+---------------+
| >>   | CONTAINS      | NUM        | `(385673002,  | 15.0          |
|      |               |            | SCT,          | (             |
|      |               |            | "Interval     | ms,UCUM,"ms") |
|      |               |            | ") <http://sn |               |
|      |               |            | omed.info/id/ |               |
|      |               |            | 385673002>`__ |               |
+------+---------------+------------+---------------+---------------+
| >>>  | HAS           | TEXT       | (125309, DCM, | "MV Jet       |
|      | PROPERTIES    |            | "Short        | Duration"     |
|      |               |            | Label")       |               |
+------+---------------+------------+---------------+---------------+
| >>   | CONTAINS      | NUM        | `(1483009,    | 27.0          |
|      |               |            | SCT,          | (de           |
|      |               |            | "Ang          | g,UCUM,"deg") |
|      |               |            | le") <http:// |               |
|      |               |            | snomed.info/i |               |
|      |               |            | d/1483009>`__ |               |
+------+---------------+------------+---------------+---------------+
| >>>  | HAS           | TEXT       | (125309, DCM, | "MV Leaf      |
|      | PROPERTIES    |            | "Short        | Angle"        |
|      |               |            | Label")       |               |
+------+---------------+------------+---------------+---------------+

