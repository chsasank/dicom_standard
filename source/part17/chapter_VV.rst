.. _chapter_VV:

Pediatric, Fetal and Congenital Cardiac Ultrasound Reports (Informative)
========================================================================

.. _sect_VV.1:

Content Structure
-----------------

`figure_title <#figure_VV.1-1>`__ is an outline of the Pediatric, Fetal
and Congenital Cardiac Ultrasound Reports.

.. _sect_VV.2:

Pediatric, Fetal and Congenital Cardiac Ultrasound Patterns
-----------------------------------------------------------

The common Pediatric, Fetal and Congenital Cardiac Ultrasound
measurement pattern is a group of measurements obtained in the context
of a protocol. `figure_title <#figure_VV.2-1>`__ shows the pattern.

.. _sect_VV.3:

Measurement Terminology Composition
-----------------------------------

Because of the wide variety of congenital issues in fetal and pediatric
cardiology, DICOM identifies these findings primarily with
post-coordination. The concept name of the base content item typically
specifies a property, which then requires an anatomic site concept
modifier.

+-----------------------------------------------------+---------------+
| **Concept Name of Modifier**                        | **Value Set** |
+=====================================================+===============+
| `(370129005, SCT, "Measurement                      |               |
| Method") <http://snomed.info/id/370129005>`__       |               |
+-----------------------------------------------------+---------------+
| `(363698007, SCT, "Finding                          |               |
| Site") <http://snomed.info/id/363698007>`__         |               |
+-----------------------------------------------------+---------------+
| `(260674002, SCT, "Flow                             |               |
| Direction") <http://snomed.info/id/260674002>`__    |               |
+-----------------------------------------------------+---------------+
| `(272517003, SCT, "Respiratory Cycle                |               |
| Point") <http://snomed.info/id/272517003>`__        |               |
+-----------------------------------------------------+---------------+
| `(272518008, SCT, "Cardiac Cycle                    |               |
| Point") <http://snomed.info/id/272518008>`__        |               |
+-----------------------------------------------------+---------------+
| (121401, DCM, "Derivation")                         |               |
+-----------------------------------------------------+---------------+

Further qualification specifies the image mode and the image plane using
HAS ACQ CONTEXT with the value sets shown below.

+-----------------------------------------------------+---------------+
| **Concept Name**                                    | **Value Set** |
+=====================================================+===============+
| `(399264008, SCT, "Image                            |               |
| Mode") <http://snomed.info/id/399264008>`__         |               |
+-----------------------------------------------------+---------------+
| (111031, DCM, "Image View")                         |               |
+-----------------------------------------------------+---------------+

