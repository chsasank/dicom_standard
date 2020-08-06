.. _chapter_N:

Echocardiography Procedure Reports (Informative)
================================================

The templates for ultrasound reports are defined in .
`figure_title <#figure_N.1-1>`__ is an outline of the echocardiography
report.

.. _sect_N.1:

Echo Patterns
-------------

The common echocardiography measurement pattern is a group of
measurements obtained in the context of a protocol.
`figure_title <#figure_N.1-2>`__ shows the pattern.

.. _sect_N.2:

Measurement Terminology Composition
-----------------------------------

DICOM identifies echocardiography observations with various degrees of
pre- and post-coordination. The concept name of the base content item
typically specifies both anatomy and property for commonly used terms,
or purely a property. Pure property concepts require an anatomic site
concept modifier. Pure property concepts such as those in and use
concept modifiers shown below.

+-----------------------------------------------------+---------------+
| **Concept Name of Modifier**                        | **Value Set** |
+=====================================================+===============+
| `(370129005, SCT, "Measurement                      |               |
| Method") <http://snomed.info/id/370129005>`__       |               |
+-----------------------------------------------------+---------------+
| `(363698007, SCT, "Finding                          |               |
| Site") <http://snomed.info/id/363698007>`__         |               |
+-----------------------------------------------------+---------------+
| `(106233006, SCT, "Topographical                    |               |
| Modifier") <http://snomed.info/id/106233006>`__     |               |
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

.. _sect_N.3:

Illustrative Mapping to ASE Concepts
------------------------------------

The content of this section provides recommendations on how to express
the concepts from draft ASE guidelines with measurement type concept
names and concept name modifiers.

The leftmost column is the name of the ASE concept. The Base Measurement
Concept Name is the concept name of the numeric measurement content
item. The modifiers column specifies a set of modifiers for the base
measurement concept name. Each modifier consists of a modifier concept
name (e.g., method or mode) and its value (e.g., Continuity). Where no
Concept Modifier appears, the base concept matches the ASE concept.

.. _sect_N.3.1:

Aorta
~~~~~

+----------------------+----------------------+----------------------+
| Name of ASE Concept  | Base Measurement     | Concept or           |
|                      | Concept Name         | Acquisition Context  |
|                      |                      | Modifiers            |
+======================+======================+======================+
| Aortic Root Diameter | `(18015-8, LN,       |                      |
|                      | "Aortic Root         |                      |
|                      | D                    |                      |
|                      | iameter") <http://lo |                      |
|                      | inc.org/18015-8/>`__ |                      |
+----------------------+----------------------+----------------------+
| Ascending Aortic     | `(18012-5, LN,       |                      |
| Diameter             | "Ascending Aortic    |                      |
|                      | D                    |                      |
|                      | iameter") <http://lo |                      |
|                      | inc.org/18012-5/>`__ |                      |
+----------------------+----------------------+----------------------+
| Aortic Arch Diameter | `(18011-7, LN,       |                      |
|                      | "Aortic Arch         |                      |
|                      | D                    |                      |
|                      | iameter") <http://lo |                      |
|                      | inc.org/18011-7/>`__ |                      |
+----------------------+----------------------+----------------------+
| Descending Aortic    | `(18013-3, LN,       |                      |
| Diameter             | "Descending Aortic   |                      |
|                      | D                    |                      |
|                      | iameter") <http://lo |                      |
|                      | inc.org/18013-3/>`__ |                      |
+----------------------+----------------------+----------------------+

.. _sect_N.3.2:

Aortic Valve
~~~~~~~~~~~~

+----------------------+----------------------+----------------------+
| Name of ASE Concept  | Base Measurement     | Concept or           |
|                      | Concept Name         | Acquisition Context  |
|                      |                      | Modifiers            |
+======================+======================+======================+
| Aortic Valve Cusp    | `(17996-0, LN,       |                      |
| Separation           | "Aortic Valve Cusp   |                      |
|                      | Sep                  |                      |
|                      | aration") <http://lo |                      |
|                      | inc.org/17996-0/>`__ |                      |
+----------------------+----------------------+----------------------+
| Aortic Valve         | `(11726-7, LN, "Peak | `(260674002, SCT,    |
| Systolic Peak        | V                    | "Direction of        |
| Velocity             | elocity") <http://lo | Flo                  |
|                      | inc.org/11726-7/>`__ | w") <http://snomed.i |
|                      |                      | nfo/id/260674002>`__ |
|                      |                      | = `(263677008, SCT,  |
|                      |                      | "Antegrade           |
|                      |                      | Flo                  |
|                      |                      | w") <http://snomed.i |
|                      |                      | nfo/id/263677008>`__ |
+----------------------+----------------------+----------------------+
| Aortic Valve         | `(20354-7, LN,       | `(260674002, SCT,    |
| Systolic Velocity    | "Velocity Time       | "Direction of        |
| Time Integral        | I                    | Flo                  |
|                      | ntegral") <http://lo | w") <http://snomed.i |
|                      | inc.org/20354-7/>`__ | nfo/id/260674002>`__ |
|                      |                      | = `(263677008, SCT,  |
|                      |                      | "Antegrade           |
|                      |                      | Flo                  |
|                      |                      | w") <http://snomed.i |
|                      |                      | nfo/id/263677008>`__ |
+----------------------+----------------------+----------------------+
| Aortic Valve         | `(399367004, SCT,    | `(260674002, SCT,    |
| Systolic Area        | "Cardiovascular      | "Direction of        |
|                      | Orifice              | Flo                  |
|                      | Are                  | w") <http://snomed.i |
|                      | a") <http://snomed.i | nfo/id/260674002>`__ |
|                      | nfo/id/399367004>`__ | = `(263677008, SCT,  |
|                      |                      | "Antegrade           |
|                      |                      | Flo                  |
|                      |                      | w") <http://snomed.i |
|                      |                      | nfo/id/263677008>`__ |
+----------------------+----------------------+----------------------+
| Aortic Valve         | `(399367004, SCT,    | `(260674002, SCT,    |
| Planimetered         | "Cardiovascular      | "Direction of        |
| Systolic Area        | Orifice              | Flo                  |
|                      | Are                  | w") <http://snomed.i |
|                      | a") <http://snomed.i | nfo/id/260674002>`__ |
|                      | nfo/id/399367004>`__ | = `(263677008, SCT,  |
|                      |                      | "Antegrade           |
|                      |                      | Flo                  |
|                      |                      | w") <http://snomed.i |
|                      |                      | nfo/id/263677008>`__ |
|                      |                      |                      |
|                      |                      | `(370129005, SCT,    |
|                      |                      | "Measurement         |
|                      |                      | Metho                |
|                      |                      | d") <http://snomed.i |
|                      |                      | nfo/id/370129005>`__ |
|                      |                      | = (125220, DCM,      |
|                      |                      | "Planimetry")        |
+----------------------+----------------------+----------------------+
| Aortic Valve         | `(399367004, SCT,    | `(260674002, SCT,    |
| Systolic Area by     | "Cardiovascular      | "Direction of        |
| Continuity           | Orifice              | Flo                  |
|                      | Are                  | w") <http://snomed.i |
|                      | a") <http://snomed.i | nfo/id/260674002>`__ |
|                      | nfo/id/399367004>`__ | = `(263677008, SCT,  |
|                      |                      | "Antegrade           |
|                      |                      | Flo                  |
|                      |                      | w") <http://snomed.i |
|                      |                      | nfo/id/263677008>`__ |
|                      |                      |                      |
|                      |                      | `(370129005, SCT,    |
|                      |                      | "Measurement         |
|                      |                      | Metho                |
|                      |                      | d") <http://snomed.i |
|                      |                      | nfo/id/370129005>`__ |
|                      |                      | = (125212, DCM,      |
|                      |                      | "Continuity          |
|                      |                      | Equation")           |
+----------------------+----------------------+----------------------+
| Aortic Valve         | `(399367004, SCT,    | `(260674002, SCT,    |
| Systolic Area by     | "Cardiovascular      | "Direction of        |
| Continuity of Peak   | Orifice              | Flo                  |
| Velocity             | Are                  | w") <http://snomed.i |
|                      | a") <http://snomed.i | nfo/id/260674002>`__ |
|                      | nfo/id/399367004>`__ | = `(263677008, SCT,  |
|                      |                      | "Antegrade           |
|                      |                      | Flo                  |
|                      |                      | w") <http://snomed.i |
|                      |                      | nfo/id/263677008>`__ |
|                      |                      |                      |
|                      |                      | `(370129005, SCT,    |
|                      |                      | "Measurement         |
|                      |                      | Metho                |
|                      |                      | d") <http://snomed.i |
|                      |                      | nfo/id/370129005>`__ |
|                      |                      | = (125214. DCM,      |
|                      |                      | "Continuity Equation |
|                      |                      | Peak Velocity")      |
+----------------------+----------------------+----------------------+
| Aortic Valve         | `(399367004, SCT,    | `(260674002, SCT,    |
| Systolic Area by     | "Cardiovascular      | "Direction of        |
| Continuity of Mean   | Orifice              | Flo                  |
| Velocity             | Are                  | w") <http://snomed.i |
|                      | a") <http://snomed.i | nfo/id/260674002>`__ |
|                      | nfo/id/399367004>`__ | = `(263677008, SCT,  |
|                      |                      | "Antegrade           |
|                      |                      | Flo                  |
|                      |                      | w") <http://snomed.i |
|                      |                      | nfo/id/263677008>`__ |
|                      |                      |                      |
|                      |                      | `(370129005, SCT,    |
|                      |                      | "Measurement         |
|                      |                      | Metho                |
|                      |                      | d") <http://snomed.i |
|                      |                      | nfo/id/370129005>`__ |
|                      |                      | = (125213. DCM,      |
|                      |                      | "Continuity Equation |
|                      |                      | by Mean Velocity")   |
+----------------------+----------------------+----------------------+
| Aortic Valve         | `(399367004, SCT,    | `(260674002, SCT,    |
| Systolic Area by     | "Cardiovascular      | "Direction of        |
| Continuity of VTI    | Orifice              | Flo                  |
|                      | Are                  | w") <http://snomed.i |
|                      | a") <http://snomed.i | nfo/id/260674002>`__ |
|                      | nfo/id/399367004>`__ | = `(263677008, SCT,  |
|                      |                      | "Antegrade           |
|                      |                      | Flo                  |
|                      |                      | w") <http://snomed.i |
|                      |                      | nfo/id/263677008>`__ |
|                      |                      |                      |
|                      |                      | `(370129005, SCT,    |
|                      |                      | "Measurement         |
|                      |                      | Metho                |
|                      |                      | d") <http://snomed.i |
|                      |                      | nfo/id/370129005>`__ |
|                      |                      | = (125215, DCM,      |
|                      |                      | "Continuity Equation |
|                      |                      | by Velocity Time     |
|                      |                      | Integral")           |
+----------------------+----------------------+----------------------+
| Aortic Valve         | (20247-3 LN, "Peak   | `(260674002, SCT,    |
| Systolic Peak        | Gradient")           | "Direction of        |
| Instantaneous        |                      | Flo                  |
| Gradient             |                      | w") <http://snomed.i |
|                      |                      | nfo/id/260674002>`__ |
|                      |                      | = `(263677008, SCT,  |
|                      |                      | "Antegrade           |
|                      |                      | Flo                  |
|                      |                      | w") <http://snomed.i |
|                      |                      | nfo/id/263677008>`__ |
+----------------------+----------------------+----------------------+
| Aortic Valve         | `(20256-4, LN, "Mean | `(260674002, SCT,    |
| Systolic Mean        | G                    | "Direction of        |
| Gradient             | radient") <http://lo | Flo                  |
|                      | inc.org/20256-4/>`__ | w") <http://snomed.i |
|                      |                      | nfo/id/260674002>`__ |
|                      |                      | = `(263677008, SCT,  |
|                      |                      | "Antegrade           |
|                      |                      | Flo                  |
|                      |                      | w") <http://snomed.i |
|                      |                      | nfo/id/263677008>`__ |
+----------------------+----------------------+----------------------+
| Aortic Annulus       | `(399027007, SCT,    | `(363698007, SCT,    |
| Systolic Diameter    | "Cardiovascular      | "Finding             |
|                      | Orifice              | Sit                  |
|                      | Diamete              | e") <http://snomed.i |
|                      | r") <http://snomed.i | nfo/id/363698007>`__ |
|                      | nfo/id/399027007>`__ | = `(77583004, SCT,   |
|                      |                      | "Aortic Valve        |
|                      |                      | Ri                   |
|                      |                      | ng") <http://snomed. |
|                      |                      | info/id/77583004>`__ |
|                      |                      | `(260674002, SCT,    |
|                      |                      | "Direction of        |
|                      |                      | Flo                  |
|                      |                      | w") <http://snomed.i |
|                      |                      | nfo/id/260674002>`__ |
|                      |                      | = `(263677008, SCT,  |
|                      |                      | "Antegrade           |
|                      |                      | Flo                  |
|                      |                      | w") <http://snomed.i |
|                      |                      | nfo/id/263677008>`__ |
+----------------------+----------------------+----------------------+
| Aortic Valve         | `(20216-8, LN,       | `(260674002, SCT,    |
| Regurgitant          | "Deceleration        | "Direction of        |
| Diastolic            | Slope") <http://lo   | Flo                  |
| Deceleration Slope   | inc.org/20216-8/>`__ | w") <http://snomed.i |
|                      |                      | nfo/id/260674002>`__ |
|                      |                      | = `(312004007, SCT,  |
|                      |                      | "Regurgitant         |
|                      |                      | Flo                  |
|                      |                      | w") <http://snomed.i |
|                      |                      | nfo/id/312004007>`__ |
+----------------------+----------------------+----------------------+
| Aortic Valve         | `(20217-6, LN,       | `(260674002, SCT,    |
| Regurgitant          | "Deceleration        | "Direction of        |
| Diastolic            | Time") <http://lo    | Flo                  |
| Deceleration Time    | inc.org/20217-6/>`__ | w") <http://snomed.i |
|                      |                      | nfo/id/260674002>`__ |
|                      |                      | = `(312004007, SCT,  |
|                      |                      | "Regurgitant         |
|                      |                      | Flo                  |
|                      |                      | w") <http://snomed.i |
|                      |                      | nfo/id/312004007>`__ |
+----------------------+----------------------+----------------------+
| Aortic Valve         | `(20280-4, LN,       | `(260674002, SCT,    |
| Regurgitant          | "Pressure            | "Direction of        |
| Diastolic Pressure   | Ha                   | Flo                  |
| Half-time            | lf-Time") <http://lo | w") <http://snomed.i |
|                      | inc.org/20280-4/>`__ | nfo/id/260674002>`__ |
|                      |                      | = `(312004007, SCT,  |
|                      |                      | "Regurgitant         |
|                      |                      | Flo                  |
|                      |                      | w") <http://snomed.i |
|                      |                      | nfo/id/312004007>`__ |
+----------------------+----------------------+----------------------+
| Aortic               | `(20247-3, LN, "Peak | `(260674002, SCT,    |
| Insufficiency,       | G                    | "Direction of        |
| End-Diastolic        | radient") <http://lo | Flo                  |
| Pressure Gradient    | inc.org/20247-3/>`__ | w") <http://snomed.i |
|                      |                      | nfo/id/260674002>`__ |
|                      |                      | = `(312004007, SCT,  |
|                      |                      | "Regurgitant         |
|                      |                      | Flo                  |
|                      |                      | w") <http://snomed.i |
|                      |                      | nfo/id/312004007>`__ |
+----------------------+----------------------+----------------------+
| Aortic               | `(11653-3, LN, "End  | `(260674002, SCT,    |
| Insufficiency, End   | Diastolic            | "Direction of        |
| Diastolic Velocity   | V                    | Flo                  |
|                      | elocity") <http://lo | w") <http://snomed.i |
|                      | inc.org/11653-3/>`__ | nfo/id/260674002>`__ |
|                      |                      | = `(312004007, SCT,  |
|                      |                      | "Regurgitant         |
|                      |                      | Flo                  |
|                      |                      | w") <http://snomed.i |
|                      |                      | nfo/id/312004007>`__ |
+----------------------+----------------------+----------------------+

.. note::

   Aortic Valve measurements appear in , which specifies the Finding
   Site to be Aortic Valve with the concept modifier `(363698007, SCT,
   "Finding Site") <http://snomed.info/id/363698007>`__ = `(34202007,
   SCT, "Aortic Valve") <http://snomed.info/id/34202007>`__.Therefore,
   the Finding Site modifier does not appear in the right column.

.. _sect_N.3.3:

Left Ventricle - Linear
~~~~~~~~~~~~~~~~~~~~~~~

+----------------------+----------------------+----------------------+
| Name of ASE Concept  | Base Measurement     | Concept or           |
|                      | Concept Name         | Acquisition Context  |
|                      |                      | Modifiers            |
+======================+======================+======================+
| Left Ventricle       | (29436-3, LN "Left   |                      |
| Internal End         | Ventricle Internal   |                      |
| Diastolic Dimension  | End Diastolic        |                      |
|                      | Dimension")          |                      |
+----------------------+----------------------+----------------------+
| Left Ventricle       | `(29438-9, LN, "Left |                      |
| Internal Systolic    | Ventricle Internal   |                      |
| Dimension            | Systolic             |                      |
|                      | Di                   |                      |
|                      | mension") <http://lo |                      |
|                      | inc.org/29438-9/>`__ |                      |
+----------------------+----------------------+----------------------+
| Left Ventricle       | `(18077-8, LN, "Left |                      |
| Diastolic Major Axis | Ventricle Diastolic  |                      |
|                      | Major                |                      |
|                      | Axis") <http://lo    |                      |
|                      | inc.org/18077-8/>`__ |                      |
+----------------------+----------------------+----------------------+
| Left Ventricle       | `(18076-0, LN, "Left |                      |
| Systolic Major Axis  | Ventricle Systolic   |                      |
|                      | Major                |                      |
|                      | Axis") <http://lo    |                      |
|                      | inc.org/18076-0/>`__ |                      |
+----------------------+----------------------+----------------------+
| Left Ventricular     | `(18051-3, LN, "Left |                      |
| Fractional           | Ventricular          |                      |
| Shortening           | Fractional           |                      |
|                      | Sho                  |                      |
|                      | rtening") <http://lo |                      |
|                      | inc.org/18051-3/>`__ |                      |
+----------------------+----------------------+----------------------+
| Interventricular     | `(18154-5, LN,       |                      |
| Septum Diastolic     | "Interventricular    |                      |
| Thickness            | Septum Diastolic     |                      |
|                      | Th                   |                      |
|                      | ickness") <http://lo |                      |
|                      | inc.org/18154-5/>`__ |                      |
+----------------------+----------------------+----------------------+
| Interventricular     | `(18158-6, LN,       |                      |
| Septum Systolic      | "Interventricular    |                      |
| Thickness            | Septum Systolic      |                      |
|                      | Th                   |                      |
|                      | ickness") <http://lo |                      |
|                      | inc.org/18158-6/>`__ |                      |
+----------------------+----------------------+----------------------+
| Interventricular     | `(18054-7, LN,       |                      |
| Septum % Thickening  | "Interventricular    |                      |
|                      | Septum %             |                      |
|                      | Thi                  |                      |
|                      | ckening") <http://lo |                      |
|                      | inc.org/18054-7/>`__ |                      |
+----------------------+----------------------+----------------------+
| Left Ventricle       | `(18152-9, LN, "Left |                      |
| Posterior Wall       | Ventricle Posterior  |                      |
| Diastolic Thickness  | Wall Diastolic       |                      |
|                      | Th                   |                      |
|                      | ickness") <http://lo |                      |
|                      | inc.org/18152-9/>`__ |                      |
+----------------------+----------------------+----------------------+
| Left Ventricle       | `(18156-0, LN, "Left |                      |
| Posterior Wall       | Ventricle Posterior  |                      |
| Systolic Thickness   | Wall Systolic        |                      |
|                      | Th                   |                      |
|                      | ickness") <http://lo |                      |
|                      | inc.org/18156-0/>`__ |                      |
+----------------------+----------------------+----------------------+
| Left Ventricle       | `(18053-9, LN, "Left |                      |
| Posterior Wall %     | Ventricle Posterior  |                      |
| Thickening           | Wall %               |                      |
|                      | Thi                  |                      |
|                      | ckening") <http://lo |                      |
|                      | inc.org/18053-9/>`__ |                      |
+----------------------+----------------------+----------------------+
| Interventricular     | `(18155-2, LN,       |                      |
| Septum to Posterior  | "Interventricular    |                      |
| Wall Thickness ratio | Septum to Posterior  |                      |
|                      | Wall Thickness       |                      |
|                      | Ratio") <http://lo   |                      |
|                      | inc.org/18155-2/>`__ |                      |
+----------------------+----------------------+----------------------+
| Left Ventricular     | `(29436-3, LN, "Left | `(399264008, SCT,    |
| Internal End         | Ventricle Internal   | "Image               |
| Diastolic Dimension  | End Diastolic        | Mod                  |
| by 2-D               | Di                   | e") <http://snomed.i |
|                      | mension") <http://lo | nfo/id/399264008>`__ |
|                      | inc.org/29436-3/>`__ | = `(399064001, SCT,  |
|                      |                      | "2D                  |
|                      |                      | mod                  |
|                      |                      | e") <http://snomed.i |
|                      |                      | nfo/id/399064001>`__ |
+----------------------+----------------------+----------------------+
| Left Ventricular     | `(29438-9, LN, "Left | `(399264008, SCT,    |
| Internal Systolic    | Ventricle Internal   | "Image               |
| Dimension by 2-D     | Systolic             | Mod                  |
|                      | Di                   | e") <http://snomed.i |
|                      | mension") <http://lo | nfo/id/399264008>`__ |
|                      | inc.org/29438-9/>`__ | = `(399064001, SCT,  |
|                      |                      | "2D                  |
|                      |                      | mod                  |
|                      |                      | e") <http://snomed.i |
|                      |                      | nfo/id/399064001>`__ |
+----------------------+----------------------+----------------------+
| Left Ventricular     | `(18051-3, LN, "Left | `(399264008, SCT,    |
| Fractional           | Ventricular          | "Image               |
| Shortening by 2-D    | Fractional           | Mod                  |
|                      | Sho                  | e") <http://snomed.i |
|                      | rtening") <http://lo | nfo/id/399264008>`__ |
|                      | inc.org/18051-3/>`__ | = `(399064001, SCT,  |
|                      |                      | "2D                  |
|                      |                      | mod                  |
|                      |                      | e") <http://snomed.i |
|                      |                      | nfo/id/399064001>`__ |
+----------------------+----------------------+----------------------+
| Interventricular     | `(18154-5, LN,       | `(399264008, SCT,    |
| Septum Diastolic     | "Interventricular    | "Image               |
| Thickness by 2-D     | Septum Diastolic     | Mod                  |
|                      | Th                   | e") <http://snomed.i |
|                      | ickness") <http://lo | nfo/id/399264008>`__ |
|                      | inc.org/18154-5/>`__ | = `(399064001, SCT,  |
|                      |                      | "2D                  |
|                      |                      | mod                  |
|                      |                      | e") <http://snomed.i |
|                      |                      | nfo/id/399064001>`__ |
+----------------------+----------------------+----------------------+
| Interventricular     | `(18158-6, LN,       | `(399264008, SCT,    |
| Septum Systolic      | "Interventricular    | "Image               |
| Thickness by 2-D     | Septum Systolic      | Mod                  |
|                      | Th                   | e") <http://snomed.i |
|                      | ickness") <http://lo | nfo/id/399264008>`__ |
|                      | inc.org/18158-6/>`__ | = `(399064001, SCT,  |
|                      |                      | "2D                  |
|                      |                      | mod                  |
|                      |                      | e") <http://snomed.i |
|                      |                      | nfo/id/399064001>`__ |
+----------------------+----------------------+----------------------+
| Interventricular     | `(18054-7, LN,       | `(399264008, SCT,    |
| Septum % Thickening  | "Interventricular    | "Image               |
| by 2-D               | Septum %             | Mod                  |
|                      | Thi                  | e") <http://snomed.i |
|                      | ckening") <http://lo | nfo/id/399264008>`__ |
|                      | inc.org/18054-7/>`__ | = `(399064001, SCT,  |
|                      |                      | "2D                  |
|                      |                      | mod                  |
|                      |                      | e") <http://snomed.i |
|                      |                      | nfo/id/399064001>`__ |
+----------------------+----------------------+----------------------+
| Left Ventricular     | `(18152-9, LN, "Left | `(399264008, SCT,    |
| Posterior Wall       | Ventricle Posterior  | "Image               |
| Diastolic Thickness  | Wall Diastolic       | Mod                  |
| by 2-D               | Th                   | e") <http://snomed.i |
|                      | ickness") <http://lo | nfo/id/399264008>`__ |
|                      | inc.org/18152-9/>`__ | = `(399064001, SCT,  |
|                      |                      | "2D                  |
|                      |                      | mod                  |
|                      |                      | e") <http://snomed.i |
|                      |                      | nfo/id/399064001>`__ |
+----------------------+----------------------+----------------------+
| Left Ventricle       | `(18156-0, LN, "Left | `(399264008, SCT,    |
| Posterior Wall       | Ventricle Posterior  | "Image               |
| Systolic Thickness   | Wall Systolic        | Mod                  |
| by 2-D               | Th                   | e") <http://snomed.i |
|                      | ickness") <http://lo | nfo/id/399264008>`__ |
|                      | inc.org/18156-0/>`__ | = `(399064001, SCT,  |
|                      |                      | "2D                  |
|                      |                      | mod                  |
|                      |                      | e") <http://snomed.i |
|                      |                      | nfo/id/399064001>`__ |
+----------------------+----------------------+----------------------+
| Left Ventricle       | `(18053-9, LN, "Left | `(399264008, SCT,    |
| Posterior Wall %     | Ventricle Posterior  | "Image               |
| Thickening by 2-D    | Wall %               | Mod                  |
|                      | Thi                  | e") <http://snomed.i |
|                      | ckening") <http://lo | nfo/id/399264008>`__ |
|                      | inc.org/18053-9/>`__ | = `(399064001, SCT,  |
|                      |                      | "2D                  |
|                      |                      | mod                  |
|                      |                      | e") <http://snomed.i |
|                      |                      | nfo/id/399064001>`__ |
+----------------------+----------------------+----------------------+
| Interventricular     | `(18155-2, LN,       | `(399264008, SCT,    |
| Septum/ Left         | "Interventricular    | "Image               |
| Ventricular          | Septum to Posterior  | Mod                  |
| Posterior Wall       | Wall Thickness       | e") <http://snomed.i |
| Diastolic Thickness  | Ratio") <http://lo   | nfo/id/399264008>`__ |
| Ratio by 2-D         | inc.org/18155-2/>`__ | = `(399064001, SCT,  |
|                      |                      | "2D                  |
|                      |                      | mod                  |
|                      |                      | e") <http://snomed.i |
|                      |                      | nfo/id/399064001>`__ |
+----------------------+----------------------+----------------------+
| Left Ventricular     | `(29436-3, LN, "Left | `(399264008, SCT,    |
| Internal End         | Ventricle Internal   | "Image               |
| Diastolic Dimension  | End Diastolic        | Mod                  |
| by M-Mode            | Di                   | e") <http://snomed.i |
|                      | mension") <http://lo | nfo/id/399264008>`__ |
|                      | inc.org/29436-3/>`__ | = `(399155008, SCT,  |
|                      |                      | "M                   |
|                      |                      | mod                  |
|                      |                      | e") <http://snomed.i |
|                      |                      | nfo/id/399155008>`__ |
+----------------------+----------------------+----------------------+
| Left Ventricular     | `(29438-9, LN, "Left | `(399264008, SCT,    |
| Internal Systolic    | Ventricle Internal   | "Image               |
| Dimension by M-Mode  | Systolic             | Mod                  |
|                      | Di                   | e") <http://snomed.i |
|                      | mension") <http://lo | nfo/id/399264008>`__ |
|                      | inc.org/29438-9/>`__ | = `(399155008, SCT,  |
|                      |                      | "M                   |
|                      |                      | mod                  |
|                      |                      | e") <http://snomed.i |
|                      |                      | nfo/id/399155008>`__ |
+----------------------+----------------------+----------------------+
| Left Ventricular     | `(18051-3, LN, "Left | `(399264008, SCT,    |
| Systolic Fractional  | Ventricular          | "Image               |
| Shortening by M-Mode | Fractional           | Mod                  |
|                      | Sho                  | e") <http://snomed.i |
|                      | rtening") <http://lo | nfo/id/399264008>`__ |
|                      | inc.org/18051-3/>`__ | = `(399155008, SCT,  |
|                      |                      | "M                   |
|                      |                      | mod                  |
|                      |                      | e") <http://snomed.i |
|                      |                      | nfo/id/399155008>`__ |
+----------------------+----------------------+----------------------+
| Interventricular     | `(18154-5, LN,       | `(399264008, SCT,    |
| Septum Diastolic     | "Interventricular    | "Image               |
| Thickness by M-Mode  | Septum Diastolic     | Mod                  |
|                      | Th                   | e") <http://snomed.i |
|                      | ickness") <http://lo | nfo/id/399264008>`__ |
|                      | inc.org/18154-5/>`__ | = `(399155008, SCT,  |
|                      |                      | "M                   |
|                      |                      | mod                  |
|                      |                      | e") <http://snomed.i |
|                      |                      | nfo/id/399155008>`__ |
+----------------------+----------------------+----------------------+
| Interventricular     | `(18158-6, LN,       | `(399264008, SCT,    |
| Septum Systolic      | "Interventricular    | "Image               |
| Thickness by M-Mode  | Septum Systolic      | Mod                  |
|                      | Th                   | e") <http://snomed.i |
|                      | ickness") <http://lo | nfo/id/399264008>`__ |
|                      | inc.org/18158-6/>`__ | = `(399155008, SCT,  |
|                      |                      | "M                   |
|                      |                      | mod                  |
|                      |                      | e") <http://snomed.i |
|                      |                      | nfo/id/399155008>`__ |
+----------------------+----------------------+----------------------+
| Interventricular     | `(18054-7, LN,       | `(399264008, SCT,    |
| Septum % Thickening  | "Interventricular    | "Image               |
| by M-Mode            | Septum %             | Mod                  |
|                      | Thi                  | e") <http://snomed.i |
|                      | ckening") <http://lo | nfo/id/399264008>`__ |
|                      | inc.org/18054-7/>`__ | = `(399155008, SCT,  |
|                      |                      | "M                   |
|                      |                      | mod                  |
|                      |                      | e") <http://snomed.i |
|                      |                      | nfo/id/399155008>`__ |
+----------------------+----------------------+----------------------+
| Left Ventricular     | `(18152-9, LN, "Left | `(399264008, SCT,    |
| Posterior Wall       | Ventricle Posterior  | "Image               |
| Diastolic Thickness  | Wall Diastolic       | Mod                  |
| by M-Mode            | Th                   | e") <http://snomed.i |
|                      | ickness") <http://lo | nfo/id/399264008>`__ |
|                      | inc.org/18152-9/>`__ | = `(399155008, SCT,  |
|                      |                      | "M                   |
|                      |                      | mod                  |
|                      |                      | e") <http://snomed.i |
|                      |                      | nfo/id/399155008>`__ |
+----------------------+----------------------+----------------------+
| Left Ventricle       | `(18156-0, LN, "Left | `(399264008, SCT,    |
| Posterior Wall       | Ventricle Posterior  | "Image               |
| Systolic Thickness   | Wall Systolic        | Mod                  |
| by M-Mode            | Th                   | e") <http://snomed.i |
|                      | ickness") <http://lo | nfo/id/399264008>`__ |
|                      | inc.org/18156-0/>`__ | = `(399155008, SCT,  |
|                      |                      | "M                   |
|                      |                      | mod                  |
|                      |                      | e") <http://snomed.i |
|                      |                      | nfo/id/399155008>`__ |
+----------------------+----------------------+----------------------+
| Left Ventricle       | `(18053-9, LN, "Left | `(399264008, SCT,    |
| Posterior Wall %     | Ventricle Posterior  | "Image               |
| Thickening by M-Mode | Wall %               | Mod                  |
|                      | Thi                  | e") <http://snomed.i |
|                      | ckening") <http://lo | nfo/id/399264008>`__ |
|                      | inc.org/18053-9/>`__ | = `(399155008, SCT,  |
|                      |                      | "M                   |
|                      |                      | mod                  |
|                      |                      | e") <http://snomed.i |
|                      |                      | nfo/id/399155008>`__ |
+----------------------+----------------------+----------------------+
| Interventricular     | `(18155-2, LN,       | `(399264008, SCT,    |
| Septum to Left       | "Interventricular    | "Image               |
| Ventricular          | Septum to Posterior  | Mod                  |
| Posterior Wall Ratio | Wall Thickness       | e") <http://snomed.i |
| by M-Mode            | Ratio") <http://lo   | nfo/id/399264008>`__ |
|                      | inc.org/18155-2/>`__ | = `(399155008, SCT,  |
|                      |                      | "M                   |
|                      |                      | mod                  |
|                      |                      | e") <http://snomed.i |
|                      |                      | nfo/id/399155008>`__ |
+----------------------+----------------------+----------------------+

.. _sect_N.3.4:

Left Ventricle Volumes and Ejection Fraction
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------------+----------------------+----------------------+
| Name of ASE Concept  | Base Measurement     | Concept or           |
|                      | Concept Name         | Acquisition Context  |
|                      |                      | Modifiers            |
+======================+======================+======================+
| Left Ventricular End | `(18026-5, LN, "Left |                      |
| Diastolic Volume     | Ventricular End      |                      |
|                      | Diastolic            |                      |
|                      | Volume") <http://lo  |                      |
|                      | inc.org/18026-5/>`__ |                      |
+----------------------+----------------------+----------------------+
| Left Ventricular End | `(18026-5, LN, "Left | `(370129005, SCT,    |
| Diastolic Volume by  | Ventricular End      | "Measurement         |
| Teichholz Method     | Diastolic            | Metho                |
|                      | Volume") <http://lo  | d") <http://snomed.i |
|                      | inc.org/18026-5/>`__ | nfo/id/370129005>`__ |
|                      |                      | = (125209, DCM,      |
|                      |                      | "Teichholz")         |
+----------------------+----------------------+----------------------+
| Left Ventricular End | `(18026-5, LN, "Left | (111031, DCM, "Image |
| Diastolic Volume by  | Ventricular End      | View") =             |
| 2-D Single Plane by  | Diastolic            | `(399214001, SCT,    |
| Method of Disks      | Volume") <http://lo  | "Apical Four         |
| (4-Chamber)          | inc.org/18026-5/>`__ | Chambe               |
|                      |                      | r") <http://snomed.i |
|                      |                      | nfo/id/399214001>`__ |
|                      |                      | `(370129005, SCT,    |
|                      |                      | "Measurement         |
|                      |                      | Metho                |
|                      |                      | d") <http://snomed.i |
|                      |                      | nfo/id/370129005>`__ |
|                      |                      | = (125208, DCM,      |
|                      |                      | "Method of Disks,    |
|                      |                      | Single Plane")       |
+----------------------+----------------------+----------------------+
| Left Ventricular End | `(18026-5, LN, "Left | `(370129005, SCT,    |
| Diastolic Volume by  | Ventricular End      | "Measurement         |
| 2-D Biplane by       | Diastolic            | Metho                |
| Method of Disks      | Volume") <http://lo  | d") <http://snomed.i |
|                      | inc.org/18026-5/>`__ | nfo/id/370129005>`__ |
|                      |                      | = (125207, DCM,      |
|                      |                      | "Method of Disks,    |
|                      |                      | Biplane")            |
+----------------------+----------------------+----------------------+
| Left Ventricular End | `(18148-7, LN, "Left |                      |
| Systolic Volume      | Ventricular End      |                      |
|                      | Systolic             |                      |
|                      | Volume") <http://lo  |                      |
|                      | inc.org/18148-7/>`__ |                      |
+----------------------+----------------------+----------------------+
| Left Ventricular End | `(18148-7, LN, "Left | `(370129005, SCT,    |
| Systolic Volume by   | Ventricular End      | "Measurement         |
| Teichholz Method     | Systolic             | Metho                |
|                      | Volume") <http://lo  | d") <http://snomed.i |
|                      | inc.org/18148-7/>`__ | nfo/id/370129005>`__ |
|                      |                      | = (125209, DCM,      |
|                      |                      | "Teichholz")         |
+----------------------+----------------------+----------------------+
| Left Ventricular End | `(18148-7, LN, "Left | (111031, DCM, "Image |
| Systolic Volume by   | Ventricular End      | View") =             |
| 2D Single Plane by   | Systolic             | `(399214001, SCT,    |
| Method of Disks      | Volume") <http://lo  | "Apical Four         |
| (4-Chamber)          | inc.org/18148-7/>`__ | Chambe               |
|                      |                      | r") <http://snomed.i |
|                      |                      | nfo/id/399214001>`__ |
|                      |                      | `(370129005, SCT,    |
|                      |                      | "Measurement         |
|                      |                      | Metho                |
|                      |                      | d") <http://snomed.i |
|                      |                      | nfo/id/370129005>`__ |
|                      |                      | = (125208, DCM,      |
|                      |                      | "Method of Disks,    |
|                      |                      | Single Plane")       |
+----------------------+----------------------+----------------------+
| Left Ventricular End | `(18148-7, LN, "Left | `(370129005, SCT,    |
| Systolic Volume by   | Ventricular End      | "Measurement         |
| 2-D Biplane by       | Systolic             | Metho                |
| Method of Disks      | Volume") <http://lo  | d") <http://snomed.i |
|                      | inc.org/18148-7/>`__ | nfo/id/370129005>`__ |
|                      |                      | = (125207, DCM,      |
|                      |                      | "Method of Disks,    |
|                      |                      | Biplane")            |
+----------------------+----------------------+----------------------+
| Left Ventricular EF  | `(18043-0, LN, "Left |                      |
|                      | Ventricular Ejection |                      |
|                      | F                    |                      |
|                      | raction") <http://lo |                      |
|                      | inc.org/18043-0/>`__ |                      |
+----------------------+----------------------+----------------------+
| Left Ventricular EF  | `(18043-0, LN, "Left | `(370129005, SCT,    |
| by Teichholz Method  | Ventricular Ejection | "Measurement         |
|                      | F                    | Metho                |
|                      | raction") <http://lo | d") <http://snomed.i |
|                      | inc.org/18043-0/>`__ | nfo/id/370129005>`__ |
|                      |                      | = (125209, DCM,      |
|                      |                      | "Teichholz")         |
+----------------------+----------------------+----------------------+
| Left Ventricular EF  | `(18043-0, LN, "Left | (111031, DCM, "Image |
| by 2D Single Plane   | Ventricular Ejection | View") =             |
| by Method of Disks   | F                    | `(399214001, SCT,    |
| (4-Chamber)          | raction") <http://lo | "Apical Four Chamber |
|                      | inc.org/18043-0/>`__ | ") <http://snomed.i  |
|                      |                      | nfo/id/399214001>`__ |
|                      |                      | `(370129005, SCT,    |
|                      |                      | "Measurement         |
|                      |                      | Metho                |
|                      |                      | d") <http://snomed.i |
|                      |                      | nfo/id/370129005>`__ |
|                      |                      | = (125208, DCM,      |
|                      |                      | "Method Of Disks,    |
|                      |                      | Single Plane")       |
+----------------------+----------------------+----------------------+
| Left Ventricular EF  | `(18043-0, LN, "Left | `(370129005, SCT,    |
| by 2-D Biplane by    | Ventricular Ejection | "Measurement         |
| Method of Disks      | F                    | Metho                |
|                      | raction") <http://lo | d") <http://snomed.i |
|                      | inc.org/18043-0/>`__ | nfo/id/370129005>`__ |
|                      |                      | = (125207, DCM,      |
|                      |                      | "Method of Disks,    |
|                      |                      | Biplane")            |
+----------------------+----------------------+----------------------+

.. _sect_N.3.5:

Left Ventricle Output
~~~~~~~~~~~~~~~~~~~~~

+----------------------+----------------------+----------------------+
| Name of ASE Concept  | Base Measurement     | Concept or           |
|                      | Concept Name         | Acquisition Context  |
|                      |                      | Modifiers            |
+======================+======================+======================+
| Left Ventricular     | `(90096001, SCT,     |                      |
| Stroke Volume        | "Stroke              |                      |
|                      | Volu                 |                      |
|                      | me") <http://snomed. |                      |
|                      | info/id/90096001>`__ |                      |
+----------------------+----------------------+----------------------+
| Left Ventricular     | `(90096001, SCT,     | `(370129005, SCT,    |
| Stroke Volume by     | "Stroke              | "Measurement         |
| Doppler Volume Flow  | Volu                 | Metho                |
|                      | me") <http://snomed. | d") <http://snomed.i |
|                      | info/id/90096001>`__ | nfo/id/370129005>`__ |
|                      |                      | = (125219, DCM,      |
|                      |                      | "Doppler Volume      |
|                      |                      | Flow") `(363698007,  |
|                      |                      | SCT, "Finding        |
|                      |                      | Sit                  |
|                      |                      | e") <http://snomed.i |
|                      |                      | nfo/id/363698007>`__ |
|                      |                      | = `(13418002, SCT,   |
|                      |                      | "Left Ventricle      |
|                      |                      | Outflow              |
|                      |                      | Tra                  |
|                      |                      | ct") <http://snomed. |
|                      |                      | info/id/13418002>`__ |
+----------------------+----------------------+----------------------+
| Left Ventricular     | `(90096001, SCT,     | `(370129005, SCT,    |
| Stroke Volume by     | "Stroke              | "Measurement         |
| Teichholz Method     | Volu                 | Metho                |
|                      | me") <http://snomed. | d") <http://snomed.i |
|                      | info/id/90096001>`__ | nfo/id/370129005>`__ |
|                      |                      | = (125209, DCM,      |
|                      |                      | "Teichholz")         |
+----------------------+----------------------+----------------------+
| Left Ventricular     | `(90096001, SCT,     | (1110321 DCM, "Image |
| Stroke Volume by 2-D | "Stroke              | View")= `(399214001, |
| Single Plane by      | Volu                 | SCT, "Apical Four    |
| Method of Disks      | me") <http://snomed. | Chambe               |
| (4-Chamber)          | info/id/90096001>`__ | r") <http://snomed.i |
|                      |                      | nfo/id/399214001>`__ |
|                      |                      | `(370129005, SCT,    |
|                      |                      | "Measurement         |
|                      |                      | Metho                |
|                      |                      | d") <http://snomed.i |
|                      |                      | nfo/id/370129005>`__ |
|                      |                      | = (125208, DCM,      |
|                      |                      | "Method of Disks,    |
|                      |                      | Single Plane")       |
+----------------------+----------------------+----------------------+
| Left Ventricular     | `(90096001, SCT,     | `(370129005, SCT,    |
| Stroke Volume by 2-D | "Stroke              | "Measurement         |
| Biplane by Method of | Volu                 | Metho                |
| Disks                | me") <http://snomed. | d") <http://snomed.i |
|                      | info/id/90096001>`__ | nfo/id/370129005>`__ |
|                      |                      | = (125207, DCM,      |
|                      |                      | "Method of Disks,    |
|                      |                      | Biplane")            |
+----------------------+----------------------+----------------------+
| Left Ventricular     | `(82799009, SCT,     |                      |
| Cardiac Output       | "Cardiac             |                      |
|                      | Outp                 |                      |
|                      | ut") <http://snomed. |                      |
|                      | info/id/82799009>`__ |                      |
+----------------------+----------------------+----------------------+
| Left Ventricular     | `(82799009, SCT,     | `(370129005, SCT,    |
| Cardiac Output by    | "Cardiac             | "Measurement         |
| Doppler Volume       | Outp                 | Metho                |
| Outflow              | ut") <http://snomed. | d") <http://snomed.i |
|                      | info/id/82799009>`__ | nfo/id/370129005>`__ |
|                      |                      | = (125219, DCM,      |
|                      |                      | "Doppler Volume      |
|                      |                      | Flow") `(363698007,  |
|                      |                      | SCT, "Finding        |
|                      |                      | Sit                  |
|                      |                      | e") <http://snomed.i |
|                      |                      | nfo/id/363698007>`__ |
|                      |                      | = `(13418002, SCT,   |
|                      |                      | "Left Ventricle      |
|                      |                      | Outflow              |
|                      |                      | Tra                  |
|                      |                      | ct") <http://snomed. |
|                      |                      | info/id/13418002>`__ |
+----------------------+----------------------+----------------------+
| Left Ventricular     | `(82799009, SCT,     | `(370129005, SCT,    |
| Cardiac Output by    | "Cardiac             | "Measurement         |
| Teichholz Method     | Outp                 | Metho                |
|                      | ut") <http://snomed. | d") <http://snomed.i |
|                      | info/id/82799009>`__ | nfo/id/370129005>`__ |
|                      |                      | = (125209, DCM,      |
|                      |                      | "Teichholz")         |
+----------------------+----------------------+----------------------+
| Left Ventricular     | `(82799009, SCT,     | (111031, DCM, "Image |
| Cardiac Output by    | "Cardiac             | View") =             |
| 2-D Single Plane by  | Outp                 | `(399214001, SCT,    |
| Method of Disks      | ut") <http://snomed. | "Apical Four         |
| (4-Chamber)          | info/id/82799009>`__ | Chambe               |
|                      |                      | r") <http://snomed.i |
|                      |                      | nfo/id/399214001>`__ |
|                      |                      | `(370129005, SCT,    |
|                      |                      | "Measurement         |
|                      |                      | Metho                |
|                      |                      | d") <http://snomed.i |
|                      |                      | nfo/id/370129005>`__ |
|                      |                      | = (125208, DCM,      |
|                      |                      | "Method of Disks,    |
|                      |                      | Single Plane")       |
+----------------------+----------------------+----------------------+
| Left Ventricular     | `(82799009, SCT,     | `(370129005, SCT,    |
| Cardiac Output by    | "Cardiac             | "Measurement         |
| 2-D Biplane by       | Outp                 | Metho                |
| Method of Disks      | ut") <http://snomed. | d") <http://snomed.i |
|                      | info/id/82799009>`__ | nfo/id/370129005>`__ |
|                      |                      | = (125207, DCM,      |
|                      |                      | "Method of Disks,    |
|                      |                      | Biplane")            |
+----------------------+----------------------+----------------------+
| Left Ventricular     | `(54993008, SCT,     |                      |
| Cardiac Index        | "Cardiac             |                      |
|                      | Ind                  |                      |
|                      | ex") <http://snomed. |                      |
|                      | info/id/54993008>`__ |                      |
+----------------------+----------------------+----------------------+
| Left Ventricular     | `(54993008, SCT,     | `(370129005, SCT,    |
| Cardiac Index by     | "Cardiac             | "Measurement         |
| Doppler Volume Flow  | Ind                  | Metho                |
|                      | ex") <http://snomed. | d") <http://snomed.i |
|                      | info/id/54993008>`__ | nfo/id/370129005>`__ |
|                      |                      | = (125219, DCM,      |
|                      |                      | "Doppler Volume      |
|                      |                      | Flow")               |
+----------------------+----------------------+----------------------+
| Left Ventricular     | `(54993008, SCT,     | `(370129005, SCT,    |
| Cardiac Index by     | "Cardiac             | "Measurement         |
| Teichholz Method     | Ind                  | Metho                |
|                      | ex") <http://snomed. | d") <http://snomed.i |
|                      | info/id/54993008>`__ | nfo/id/370129005>`__ |
|                      |                      | = (125209, DCM,      |
|                      |                      | "Teichholz")         |
+----------------------+----------------------+----------------------+
| Left Ventricular     | `(54993008, SCT,     | (111031, DCM, "Image |
| Cardiac Index by 2-D | "Cardiac             | View") =             |
| Single Plane by      | Ind                  | `(399214001, SCT,    |
| Method of Disks      | ex") <http://snomed. | "Apical Four         |
| (4-Chamber)          | info/id/54993008>`__ | Chambe               |
|                      |                      | r") <http://snomed.i |
|                      |                      | nfo/id/399214001>`__ |
|                      |                      | `(370129005, SCT,    |
|                      |                      | "Measurement         |
|                      |                      | Metho                |
|                      |                      | d") <http://snomed.i |
|                      |                      | nfo/id/370129005>`__ |
|                      |                      | = (125208, DCM,      |
|                      |                      | "Method Of Disks,    |
|                      |                      | Single Plane")       |
+----------------------+----------------------+----------------------+
| Left Ventricular     | `(54993008, SCT,     | `(370129005, SCT,    |
| Cardiac Index by 2-D | "Cardiac             | "Measurement         |
| Biplane by Method of | Ind                  | Metho                |
| Disks                | ex") <http://snomed. | d") <http://snomed.i |
|                      | info/id/54993008>`__ | nfo/id/370129005>`__ |
|                      |                      | = (125207, DCM,      |
|                      |                      | "Method of Disks,    |
|                      |                      | Biplane")            |
+----------------------+----------------------+----------------------+

.. note::

   Measurements in the Left Ventricle section have context of Left
   Ventricle and do not require a Finding Site modifier `(363698007,
   SCT, "Finding Site") <http://snomed.info/id/363698007>`__ =
   `(87878005, SCT, "Left
   Ventricle") <http://snomed.info/id/87878005>`__ to specify the site.
   The Finding Site modifier appears for more specificity.

.. _sect_N.3.6:

Left Ventricular Outflow Tract
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------------+----------------------+----------------------+
| Name of ASE Concept  | Base Measurement     | Concept or           |
|                      | Concept Name         | Acquisition Context  |
|                      |                      | Modifiers            |
+======================+======================+======================+
| Left Ventricular     | `(399027007, SCT,    | `(363698007, SCT,    |
| Outflow Tract        | "Cardiovascular      | "Finding             |
| Systolic Diameter    | Orifice              | Sit                  |
|                      | Diamete              | e") <http://snomed.i |
|                      | r") <http://snomed.i | nfo/id/363698007>`__ |
|                      | nfo/id/399027007>`__ | = `(13418002, SCT,   |
|                      |                      | "Left Ventricular    |
|                      |                      | Outflow              |
|                      |                      | Tra                  |
|                      |                      | ct") <http://snomed. |
|                      |                      | info/id/13418002>`__ |
+----------------------+----------------------+----------------------+
| Left Ventricular     | `(399367004, SCT,    | `(363698007, SCT,    |
| Outflow Tract        | "Cardiovascular      | "Finding             |
| Systolic Cross       | Orifice              | Sit                  |
| Sectional Area       | Are                  | e") <http://snomed.i |
|                      | a") <http://snomed.i | nfo/id/363698007>`__ |
|                      | nfo/id/399367004>`__ | = `(13418002, SCT,   |
|                      |                      | "Left Ventricular    |
|                      |                      | Outflow              |
|                      |                      | Tra                  |
|                      |                      | ct") <http://snomed. |
|                      |                      | info/id/13418002>`__ |
+----------------------+----------------------+----------------------+
| Left Ventricular     | `(11726-7, LN, "Peak | `(363698007, SCT,    |
| Outflow Tract        | V                    | "Finding             |
| Systolic Peak        | elocity") <http://lo | Sit                  |
| Velocity             | inc.org/11726-7/>`__ | e") <http://snomed.i |
|                      |                      | nfo/id/363698007>`__ |
|                      |                      | = `(13418002, SCT,   |
|                      |                      | "Left Ventricular    |
|                      |                      | Outflow              |
|                      |                      | Tra                  |
|                      |                      | ct") <http://snomed. |
|                      |                      | info/id/13418002>`__ |
+----------------------+----------------------+----------------------+
| Left Ventricular     | `(20247-3, LN, "Peak | `(363698007, SCT,    |
| Outflow Tract        | G                    | "Finding             |
| Systolic Peak        | radient") <http://lo | Sit                  |
| Instantaneous        | inc.org/20247-3/>`__ | e") <http://snomed.i |
| Gradient             |                      | nfo/id/363698007>`__ |
|                      |                      | = `(13418002, SCT,   |
|                      |                      | "Left Ventricular    |
|                      |                      | Outflow              |
|                      |                      | Tra                  |
|                      |                      | ct") <http://snomed. |
|                      |                      | info/id/13418002>`__ |
+----------------------+----------------------+----------------------+
| Left Ventricular     | `(20352-1, LN, "Mean | `(363698007, SCT,    |
| Outflow Tract        | V                    | "Finding             |
| Systolic Mean        | elocity") <http://lo | Sit                  |
| Velocity             | inc.org/20352-1/>`__ | e") <http://snomed.i |
|                      |                      | nfo/id/363698007>`__ |
|                      |                      | = `(13418002, SCT,   |
|                      |                      | "Left Ventricular    |
|                      |                      | Outflow              |
|                      |                      | Tra                  |
|                      |                      | ct") <http://snomed. |
|                      |                      | info/id/13418002>`__ |
+----------------------+----------------------+----------------------+
| Left Ventricular     | `(20256-4, LN, "Mean | `(363698007, SCT,    |
| Outflow Tract        | G                    | "Finding             |
| Systolic Mean        | radient") <http://lo | Sit                  |
| Gradient             | inc.org/20256-4/>`__ | e") <http://snomed.i |
|                      |                      | nfo/id/363698007>`__ |
|                      |                      | = `(13418002, SCT,   |
|                      |                      | "Left Ventricular    |
|                      |                      | Outflow              |
|                      |                      | Tra                  |
|                      |                      | ct") <http://snomed. |
|                      |                      | info/id/13418002>`__ |
+----------------------+----------------------+----------------------+
| Left Ventricular     | `(20354-7, LN,       | `(363698007, SCT,    |
| Outflow Tract        | "Velocity Time       | "Finding             |
| Systolic Velocity    | I                    | Sit                  |
| Time Integral        | ntegral") <http://lo | e") <http://snomed.i |
|                      | inc.org/20354-7/>`__ | nfo/id/363698007>`__ |
|                      |                      | = `(13418002, SCT,   |
|                      |                      | "Left Ventricular    |
|                      |                      | Outflow              |
|                      |                      | Tra                  |
|                      |                      | ct") <http://snomed. |
|                      |                      | info/id/13418002>`__ |
+----------------------+----------------------+----------------------+

.. _sect_N.3.7:

Left Ventricle Mass
~~~~~~~~~~~~~~~~~~~

+----------------------+----------------------+----------------------+
| Name of ASE Concept  | Base Measurement     | Concept or           |
|                      | Concept Name         | Acquisition Context  |
|                      |                      | Modifiers            |
+======================+======================+======================+
| Left Ventricle Mass  | `(18087-7, LN, "Left |                      |
|                      | Ventricle            |                      |
|                      | Mass") <http://lo    |                      |
|                      | inc.org/18087-7/>`__ |                      |
+----------------------+----------------------+----------------------+
| Left Ventricular     | `(18087-7, LN, "Left | `(399264008, SCT,    |
| Mass by 2-D Method   | Ventricle            | "Image               |
| of Disks, Single     | Mass") <http://lo    | Mod                  |
| Plane (4-Chamber)    | inc.org/18087-7/>`__ | e") <http://snomed.i |
|                      |                      | nfo/id/399264008>`__ |
|                      |                      | = `(399064001, SCT,  |
|                      |                      | "2D                  |
|                      |                      | mod                  |
|                      |                      | e") <http://snomed.i |
|                      |                      | nfo/id/399064001>`__ |
|                      |                      | `(370129005, SCT,    |
|                      |                      | "Measurement         |
|                      |                      | Metho                |
|                      |                      | d") <http://snomed.i |
|                      |                      | nfo/id/370129005>`__ |
|                      |                      | = (125208, DCM,      |
|                      |                      | "Method Of Disks,    |
|                      |                      | single plane")       |
+----------------------+----------------------+----------------------+
| Left Ventricular     | `(18087-7, LN, "Left | `(399264008, SCT,    |
| Mass by 2-D Biplane  | Ventricle            | "Image               |
| by Method of Disks   | Mass") <http://lo    | Mod                  |
|                      | inc.org/18087-7/>`__ | e") <http://snomed.i |
|                      |                      | nfo/id/399264008>`__ |
|                      |                      | = `(399064001, SCT,  |
|                      |                      | "2D                  |
|                      |                      | mod                  |
|                      |                      | e") <http://snomed.i |
|                      |                      | nfo/id/399064001>`__ |
|                      |                      | `(370129005, SCT,    |
|                      |                      | "Measurement         |
|                      |                      | Metho                |
|                      |                      | d") <http://snomed.i |
|                      |                      | nfo/id/370129005>`__ |
|                      |                      | = (125207, DCM,      |
|                      |                      | "Method of disks,    |
|                      |                      | biplane")            |
+----------------------+----------------------+----------------------+
| Left Ventricular     | `(18087-7, LN, "Left | `(399264008, SCT,    |
| Mass by M-Mode       | Ventricle            | "Image               |
|                      | Mass") <http://lo    | Mod                  |
|                      | inc.org/18087-7/>`__ | e") <http://snomed.i |
|                      |                      | nfo/id/399264008>`__ |
|                      |                      | = `(399155008, SCT,  |
|                      |                      | "M                   |
|                      |                      | mod                  |
|                      |                      | e") <http://snomed.i |
|                      |                      | nfo/id/399155008>`__ |
+----------------------+----------------------+----------------------+

.. _sect_N.3.8:

Left Ventricle Miscellaneous
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------------+----------------------+----------------------+
| Name of ASE Concept  | Base Measurement     | Concept or           |
|                      | Concept Name         | Acquisition Context  |
|                      |                      | Modifiers            |
+======================+======================+======================+
| Left Ventricular     | `(18071-1, LN, "Left |                      |
| Isovolumic           | Ventricular          |                      |
| Relaxation Time      | Isovolumic           |                      |
|                      | Relaxation           |                      |
|                      | Time") <http://lo    |                      |
|                      | inc.org/18071-1/>`__ |                      |
+----------------------+----------------------+----------------------+
| Left Ventricular     | `(399051002, SCT,    |                      |
| Isovolumic           | "Left Ventricular    |                      |
| Contraction Time     | Isovolumic           |                      |
|                      | Contraction          |                      |
|                      | Tim                  |                      |
|                      | e") <http://snomed.i |                      |
|                      | nfo/id/399051002>`__ |                      |
+----------------------+----------------------+----------------------+
| Left Ventricular     | `(399133000, SCT,    | `(363698007, SCT,    |
| Peak Early Diastolic | "Left Ventricular    | "Finding             |
| Tissue Velocity at   | Peak Early Diastolic | Sit                  |
| the Medial Mitral    | Tissue               | e") <http://snomed.i |
| Annulus              | Velocit              | nfo/id/363698007>`__ |
|                      | y") <http://snomed.i | = `(399093001, SCT,  |
|                      | nfo/id/399133000>`__ | "Medial Mitral       |
|                      |                      | Annulu               |
|                      |                      | s") <http://snomed.i |
|                      |                      | nfo/id/399093001>`__ |
+----------------------+----------------------+----------------------+
| Left Ventricular     | `(399133000, SCT,    | `(363698007, SCT,    |
| Peak Early Diastolic | "Left Ventricular    | "Finding             |
| Tissue Velocity at   | Peak Early Diastolic | Sit                  |
| the Lateral Mitral   | Tissue               | e") <http://snomed.i |
| Annulus              | Velocit              | nfo/id/363698007>`__ |
|                      | y") <http://snomed.i | = `(399086000, SCT,  |
|                      | nfo/id/399133000>`__ | "Lateral Mitral      |
|                      |                      | Annulu               |
|                      |                      | s") <http://snomed.i |
|                      |                      | nfo/id/399086000>`__ |
+----------------------+----------------------+----------------------+
| Ratio of Mitral      | `(399140004, SCT,    | `(363698007, SCT,    |
| Valve E-Wave Peak    | "Ratio of MV Peak    | "Finding             |
| Velocity to Left     | Velocity to LV Peak  | Sit                  |
| Ventricular Peak     | Tissue Velocity      | e") <http://snomed.i |
| Early Diastolic      | E-Wav                | nfo/id/363698007>`__ |
| Tissue Velocity at   | e") <http://snomed.i | = `(399093001, SCT,  |
| the Medial Mitral    | nfo/id/399140004>`__ | "Medial Mitral       |
| Annulus              |                      | Annulu               |
|                      |                      | s") <http://snomed.i |
|                      |                      | nfo/id/399093001>`__ |
+----------------------+----------------------+----------------------+
| Ratio of Mitral      | `(399140004, SCT,    | `(363698007, SCT,    |
| Valve E-Wave Peak    | "Ratio of MV Peak    | "Finding             |
| Velocity to Left     | Velocity to LV Peak  | Sit                  |
| Ventricular Peak     | Tissue Velocity      | e") <http://snomed.i |
| Early Diastolic      | E-Wav                | nfo/id/363698007>`__ |
| Tissue Velocity at   | e") <http://snomed.i | = `(399086000, SCT,  |
| the Lateral Mitral   | nfo/id/399140004>`__ | "Lateral Mitral      |
| Annulus              |                      | Annulu               |
|                      |                      | s") <http://snomed.i |
|                      |                      | nfo/id/399086000>`__ |
+----------------------+----------------------+----------------------+
| Left Ventricular     | `(399007006, SCT,    | `(363698007, SCT,    |
| Peak Diastolic       | "LV Peak Diastolic   | "Finding             |
| Tissue Velocity at   | Tissue Velocity      | Sit                  |
| the Medial Mitral    | During Atrial        | e") <http://snomed.i |
| Annulus During       | Systol               | nfo/id/363698007>`__ |
| Atrial Systole       | e") <http://snomed.i | = `(399093001, SCT,  |
|                      | nfo/id/399007006>`__ | "Medial Mitral       |
|                      |                      | Annulu               |
|                      |                      | s") <http://snomed.i |
|                      |                      | nfo/id/399093001>`__ |
+----------------------+----------------------+----------------------+
| Left Ventricular     | `(399007006, SCT,    | `(363698007, SCT,    |
| Peak Diastolic       | "LV Peak Diastolic   | "Finding             |
| Tissue Velocity at   | Tissue Velocity      | Sit                  |
| the Lateral Mitral   | During Atrial        | e") <http://snomed.i |
| Annulus During       | Systol               | nfo/id/363698007>`__ |
| Atrial Systole       | e") <http://snomed.i | = `(399086000, SCT,  |
|                      | nfo/id/399007006>`__ | "Lateral Mitral      |
|                      |                      | Annulu               |
|                      |                      | s") <http://snomed.i |
|                      |                      | nfo/id/399086000>`__ |
+----------------------+----------------------+----------------------+
| Left Ventricular     | `(399167005, SCT,    | `(363698007, SCT,    |
| Peak Systolic Tissue | "Left Ventricular    | "Finding             |
| Velocity at the      | Peak Systolic Tissue | Sit                  |
| Medial Mitral        | Velocit              | e") <http://snomed.i |
| Annulus              | y") <http://snomed.i | nfo/id/363698007>`__ |
|                      | nfo/id/399167005>`__ | = `(399093001, SCT,  |
|                      |                      | "Medial Mitral       |
|                      |                      | Annulu               |
|                      |                      | s") <http://snomed.i |
|                      |                      | nfo/id/399093001>`__ |
+----------------------+----------------------+----------------------+
| Left Ventricular     | `(399167005, SCT,    | `(363698007, SCT,    |
| Peak Systolic Tissue | "Left Ventricular    | "Finding             |
| Velocity at the      | Peak Systolic Tissue | Sit                  |
| Lateral Mitral       | Velocit              | e") <http://snomed.i |
| Annulus              | y") <http://snomed.i | nfo/id/363698007>`__ |
|                      | nfo/id/399167005>`__ | = `(399086000, SCT,  |
|                      |                      | "Lateral Mitral      |
|                      |                      | Annulu               |
|                      |                      | s") <http://snomed.i |
|                      |                      | nfo/id/399086000>`__ |
+----------------------+----------------------+----------------------+

.. _sect_N.3.9:

Mitral Valve
~~~~~~~~~~~~

+----------------------+----------------------+----------------------+
| Name of ASE Concept  | Base Measurement     | Concept or           |
|                      | Concept Name         | Acquisition Context  |
|                      |                      | Modifiers            |
+======================+======================+======================+
| Mitral Valve Area    | `(399367004, SCT,    | `(260674002, SCT,    |
|                      | "Cardiovascular      | "Direction of        |
|                      | Orifice              | Flo                  |
|                      | Are                  | w") <http://snomed.i |
|                      | a") <http://snomed.i | nfo/id/260674002>`__ |
|                      | nfo/id/399367004>`__ | = `(263677008, SCT,  |
|                      |                      | "Antegrade           |
|                      |                      | Flo                  |
|                      |                      | w") <http://snomed.i |
|                      |                      | nfo/id/263677008>`__ |
+----------------------+----------------------+----------------------+
| Mitral Valve Area by | `(399367004, SCT,    | `(260674002, SCT,    |
| Continuity           | "Cardiovascular      | "Direction of        |
|                      | Orifice              | Flo                  |
|                      | Are                  | w") <http://snomed.i |
|                      | a") <http://snomed.i | nfo/id/260674002>`__ |
|                      | nfo/id/399367004>`__ | = `(263677008, SCT,  |
|                      |                      | "Antegrade           |
|                      |                      | Flo                  |
|                      |                      | w") <http://snomed.i |
|                      |                      | nfo/id/263677008>`__ |
|                      |                      | `(370129005, SCT,    |
|                      |                      | "Measurement         |
|                      |                      | Metho                |
|                      |                      | d") <http://snomed.i |
|                      |                      | nfo/id/370129005>`__ |
|                      |                      | = (125212. DCM,      |
|                      |                      | "Continuity          |
|                      |                      | Equation")           |
+----------------------+----------------------+----------------------+
| Mitral Valve Area by | `(399367004, SCT,    | `(260674002, SCT,    |
| Planimetry           | "Cardiovascular      | "Direction of        |
|                      | Orifice              | Flo                  |
|                      | Are                  | w") <http://snomed.i |
|                      | a") <http://snomed.i | nfo/id/260674002>`__ |
|                      | nfo/id/399367004>`__ | = `(263677008, SCT,  |
|                      |                      | "Antegrade           |
|                      |                      | Flo                  |
|                      |                      | w") <http://snomed.i |
|                      |                      | nfo/id/263677008>`__ |
|                      |                      | `(370129005, SCT,    |
|                      |                      | "Measurement         |
|                      |                      | Metho                |
|                      |                      | d") <http://snomed.i |
|                      |                      | nfo/id/370129005>`__ |
|                      |                      | = (125220, DCM,      |
|                      |                      | "Planimetry")        |
+----------------------+----------------------+----------------------+
| Mitral Valve Area by | `(399367004, SCT,    | `(260674002, SCT,    |
| Pressure Half-time   | "Cardiovascular      | "Direction of        |
|                      | Orifice              | Flo                  |
|                      | Are                  | w") <http://snomed.i |
|                      | a") <http://snomed.i | nfo/id/260674002>`__ |
|                      | nfo/id/399367004>`__ | = `(263677008, SCT,  |
|                      |                      | "Antegrade           |
|                      |                      | Flo                  |
|                      |                      | w") <http://snomed.i |
|                      |                      | nfo/id/263677008>`__ |
|                      |                      | `(370129005, SCT,    |
|                      |                      | "Measurement         |
|                      |                      | Metho                |
|                      |                      | d") <http://snomed.i |
|                      |                      | nfo/id/370129005>`__ |
|                      |                      | = (125210, DCM,      |
|                      |                      | "Area by PHT")       |
+----------------------+----------------------+----------------------+
| Mitral Valve Area by | `(399367004, SCT,    | `(260674002, SCT,    |
| Proximal Isovelocity | "Cardiovascular      | "Direction of        |
| Surface Area         | Orifice              | Flo                  |
|                      | Are                  | w") <http://snomed.i |
|                      | a") <http://snomed.i | nfo/id/260674002>`__ |
|                      | nfo/id/399367004>`__ | = `(263677008, SCT,  |
|                      |                      | "Antegrade           |
|                      |                      | Flo                  |
|                      |                      | w") <http://snomed.i |
|                      |                      | nfo/id/263677008>`__ |
|                      |                      | `(370129005, SCT,    |
|                      |                      | "Measurement         |
|                      |                      | Metho                |
|                      |                      | d") <http://snomed.i |
|                      |                      | nfo/id/370129005>`__ |
|                      |                      | = (125216, DCM,      |
|                      |                      | "Proximal            |
|                      |                      | Isovelocity Surface  |
|                      |                      | Area")               |
+----------------------+----------------------+----------------------+
| Mitral Valve         | `(20280-4, LN,       | `(260674002, SCT,    |
| Pressure Half-time   | "Pressure            | "Direction of        |
|                      | Ha                   | Flo                  |
|                      | lf-Time") <http://lo | w") <http://snomed.i |
|                      | inc.org/20280-4/>`__ | nfo/id/260674002>`__ |
|                      |                      | = `(263677008, SCT,  |
|                      |                      | "Antegrade           |
|                      |                      | Flo                  |
|                      |                      | w") <http://snomed.i |
|                      |                      | nfo/id/263677008>`__ |
+----------------------+----------------------+----------------------+
| Mitral Valve A-Wave  | `(17978-8, LN,       |                      |
| Peak Velocity        | "Mitral Valve A-Wave |                      |
|                      | Peak                 |                      |
|                      | V                    |                      |
|                      | elocity") <http://lo |                      |
|                      | inc.org/17978-8/>`__ |                      |
+----------------------+----------------------+----------------------+
| Mitral Valve E-Wave  | `(18037-2, LN,       |                      |
| Peak Velocity        | "Mitral Valve E-Wave |                      |
|                      | Peak                 |                      |
|                      | V                    |                      |
|                      | elocity") <http://lo |                      |
|                      | inc.org/18037-2/>`__ |                      |
+----------------------+----------------------+----------------------+
| Mitral Valve E to A  | `(18038-0, LN,       |                      |
| Ratio                | "Mitral Valve E to A |                      |
|                      | Ratio") <http://lo   |                      |
|                      | inc.org/18038-0/>`__ |                      |
+----------------------+----------------------+----------------------+
| Mitral Valve E-Wave  | `(399354002, SCT,    |                      |
| Deceleration Time    | "Mitral Valve E-Wave |                      |
|                      | Deceleration         |                      |
|                      | Tim                  |                      |
|                      | e") <http://snomed.i |                      |
|                      | nfo/id/399354002>`__ |                      |
+----------------------+----------------------+----------------------+
| Mitral Valve E-F     | `(18040-6, LN,       |                      |
| Slope by M-Mode      | "Mitral Valve E-F    |                      |
|                      | Slope by             |                      |
|                      | M-Mode") <http://lo  |                      |
|                      | inc.org/18040-6/>`__ |                      |
+----------------------+----------------------+----------------------+
| Mitral Valve         | `(20354-7, LN,       | `(260674002, SCT,    |
| Velocity Time        | "Velocity Time       | "Direction of        |
| Integral             | I                    | Flo                  |
|                      | ntegral") <http://lo | w") <http://snomed.i |
|                      | inc.org/20354-7/>`__ | nfo/id/260674002>`__ |
|                      |                      | = `(263677008, SCT,  |
|                      |                      | "Antegrade           |
|                      |                      | Flo                  |
|                      |                      | w") <http://snomed.i |
|                      |                      | nfo/id/263677008>`__ |
+----------------------+----------------------+----------------------+
| Mitral Valve         | `(20247-3, LN, "Peak | `(260674002, SCT,    |
| Diastolic Peak       | G                    | "Direction of        |
| Instantaneous        | radient") <http://lo | Flo                  |
| Gradient             | inc.org/20247-3/>`__ | w") <http://snomed.i |
|                      |                      | nfo/id/260674002>`__ |
|                      |                      | = `(263677008, SCT,  |
|                      |                      | "Antegrade           |
|                      |                      | Flo                  |
|                      |                      | w") <http://snomed.i |
|                      |                      | nfo/id/263677008>`__ |
+----------------------+----------------------+----------------------+
| Mitral Valve         | `(20256-4, LN, "Mean | `(260674002, SCT,    |
| Diastolic Mean       | G                    | "Direction of        |
| Gradient             | radient") <http://lo | Flo                  |
|                      | inc.org/20256-4/>`__ | w") <http://snomed.i |
|                      |                      | nfo/id/260674002>`__ |
|                      |                      | = `(263677008, SCT,  |
|                      |                      | "Antegrade           |
|                      |                      | Flo                  |
|                      |                      | w") <http://snomed.i |
|                      |                      | nfo/id/263677008>`__ |
+----------------------+----------------------+----------------------+
| Mitral Valve Annulus | `(20354-7, LN,       | `(363698007, SCT,    |
| Diastolic Velocity   | "Velocity Time       | "Finding             |
| Time Integral        | I                    | Sit                  |
|                      | ntegral") <http://lo | e") <http://snomed.i |
|                      | inc.org/20354-7/>`__ | nfo/id/363698007>`__ |
|                      |                      | = `(279174006, SCT,  |
|                      |                      | "Mitral              |
|                      |                      | Annulu               |
|                      |                      | s") <http://snomed.i |
|                      |                      | nfo/id/279174006>`__ |
|                      |                      | `(260674002, SCT,    |
|                      |                      | "Direction of        |
|                      |                      | Flo                  |
|                      |                      | w") <http://snomed.i |
|                      |                      | nfo/id/260674002>`__ |
|                      |                      | = `(263677008, SCT,  |
|                      |                      | "Antegrade           |
|                      |                      | Flo                  |
|                      |                      | w") <http://snomed.i |
|                      |                      | nfo/id/263677008>`__ |
+----------------------+----------------------+----------------------+
| Mitral Valve Annulus | `(399027007, SCT,    | `(363698007, SCT,    |
| Diastolic Diameter   | "Cardiovascular      | "Finding             |
|                      | Orifice              | Sit                  |
|                      | Diamete              | e") <http://snomed.i |
|                      | r") <http://snomed.i | nfo/id/363698007>`__ |
|                      | nfo/id/399027007>`__ | = `(279174006, SCT,  |
|                      |                      | "Mitral              |
|                      |                      | Annulu               |
|                      |                      | s") <http://snomed.i |
|                      |                      | nfo/id/279174006>`__ |
|                      |                      | `(260674002, SCT,    |
|                      |                      | "Direction of        |
|                      |                      | Flo                  |
|                      |                      | w") <http://snomed.i |
|                      |                      | nfo/id/260674002>`__ |
|                      |                      | = `(263677008, SCT,  |
|                      |                      | "Antegrade           |
|                      |                      | Flo                  |
|                      |                      | w") <http://snomed.i |
|                      |                      | nfo/id/263677008>`__ |
+----------------------+----------------------+----------------------+
| Mitral Regurgitant   | `(11726-7, LN, "Peak | `(260674002, SCT,    |
| Peak Velocity        | V                    | "Direction of        |
|                      | elocity") <http://lo | Flo                  |
|                      | inc.org/11726-7/>`__ | w") <http://snomed.i |
|                      |                      | nfo/id/260674002>`__ |
|                      |                      | = `(312004007, SCT,  |
|                      |                      | "Regurgitant         |
|                      |                      | Flo                  |
|                      |                      | w") <http://snomed.i |
|                      |                      | nfo/id/312004007>`__ |
+----------------------+----------------------+----------------------+
| Mitral Valve         | `(399367004, SCT,    | `(260674002, SCT,    |
| Effective            | "Cardiovascular      | "Direction of        |
| Regurgitant Orifice  | Orifice              | Flo                  |
| by Proximal          | Are                  | w") <http://snomed.i |
| Isovelocity Surface  | a") <http://snomed.i | nfo/id/260674002>`__ |
| Area Method          | nfo/id/399367004>`__ | = `(312004007, SCT,  |
|                      |                      | "Regurgitant         |
|                      |                      | Flo                  |
|                      |                      | w") <http://snomed.i |
|                      |                      | nfo/id/312004007>`__ |
|                      |                      | `(370129005, SCT,    |
|                      |                      | "Measurement         |
|                      |                      | Metho                |
|                      |                      | d") <http://snomed.i |
|                      |                      | nfo/id/370129005>`__ |
|                      |                      | = (125216, DCM,      |
|                      |                      | "Proximal            |
|                      |                      | Isovelocity Surface  |
|                      |                      | Area")               |
+----------------------+----------------------+----------------------+
| Mitral Valve         | `(33878-0, LN,       | `(363698007, SCT,    |
| Regurgitant Volume   | "Volume              | "Finding             |
| by Proximal          | Flow") <http://lo    | Sit                  |
| Isovelocity Surface  | inc.org/33878-0/>`__ | e") <http://snomed.i |
| Area Method          |                      | nfo/id/363698007>`__ |
|                      |                      | = `(279174006, SCT,  |
|                      |                      | "Mitral              |
|                      |                      | Annulu               |
|                      |                      | s") <http://snomed.i |
|                      |                      | nfo/id/279174006>`__ |
|                      |                      | `(260674002, SCT,    |
|                      |                      | "Direction of        |
|                      |                      | Flo                  |
|                      |                      | w") <http://snomed.i |
|                      |                      | nfo/id/260674002>`__ |
|                      |                      | = `(312004007, SCT,  |
|                      |                      | "Regurgitant         |
|                      |                      | Flo                  |
|                      |                      | w") <http://snomed.i |
|                      |                      | nfo/id/312004007>`__ |
|                      |                      | `(370129005, SCT,    |
|                      |                      | "Measurement         |
|                      |                      | Metho                |
|                      |                      | d") <http://snomed.i |
|                      |                      | nfo/id/370129005>`__ |
|                      |                      | = (125216, DCM,      |
|                      |                      | "Proximal            |
|                      |                      | Isovelocity Surface  |
|                      |                      | Area")               |
+----------------------+----------------------+----------------------+
| Mitral Valve         | `(399301000, SCT,    |                      |
| Regurgitant Fraction | "Regurgitant         |                      |
|                      | Fractio              |                      |
|                      | n") <http://snomed.i |                      |
|                      | nfo/id/399301000>`__ |                      |
+----------------------+----------------------+----------------------+
| Mitral Valve         | `(399301000, SCT,    | `(370129005, SCT,    |
| Regurgitant Fraction | "Regurgitant         | "Measurement         |
| by PISA              | Fractio              | Metho                |
|                      | n") <http://snomed.i | d") <http://snomed.i |
|                      | nfo/id/399301000>`__ | nfo/id/370129005>`__ |
|                      |                      | = (125216, DCM,      |
|                      |                      | "Proximal            |
|                      |                      | Isovelocity Surface  |
|                      |                      | Area")               |
+----------------------+----------------------+----------------------+
| Mitral Valve         | `(399301000, SCT,    | `(363698007, SCT,    |
| Regurgitant Fraction | "Regurgitant         | "Finding             |
| by Mitral Annular    | Fractio              | Sit                  |
| Flow                 | n") <http://snomed.i | e") <http://snomed.i |
|                      | nfo/id/399301000>`__ | nfo/id/363698007>`__ |
|                      |                      | = `(279174006, SCT,  |
|                      |                      | "Mitral              |
|                      |                      | Annulu               |
|                      |                      | s") <http://snomed.i |
|                      |                      | nfo/id/279174006>`__ |
|                      |                      | `(370129005, SCT,    |
|                      |                      | "Measurement         |
|                      |                      | Metho                |
|                      |                      | d") <http://snomed.i |
|                      |                      | nfo/id/370129005>`__ |
|                      |                      | = (125219, DCM,      |
|                      |                      | "Doppler Volume      |
|                      |                      | Flow")               |
+----------------------+----------------------+----------------------+
| Mitral Regurgitation | `(20247-3, LN, "Peak | `(260674002, SCT,    |
| Peak Gradient        | G                    | "Direction of        |
|                      | radient") <http://lo | Flo                  |
|                      | inc.org/20247-3/>`__ | w") <http://snomed.i |
|                      |                      | nfo/id/260674002>`__ |
|                      |                      | = `(312004007, SCT,  |
|                      |                      | "Regurgitant         |
|                      |                      | Flo                  |
|                      |                      | w") <http://snomed.i |
|                      |                      | nfo/id/312004007>`__ |
+----------------------+----------------------+----------------------+
| Left Ventricular     | `(18035-6, LN,       |                      |
| dP/dt derived from   | "Mitral              |                      |
| Mitral Regurgitation | Regurgitation dP/dt  |                      |
| velocity             | derived from Mitral  |                      |
|                      | Regurgitation        |                      |
|                      | v                    |                      |
|                      | elocity") <http://lo |                      |
|                      | inc.org/18035-6/>`__ |                      |
+----------------------+----------------------+----------------------+

.. note::

   Mitral Valve measurements appear in , which specifies the Finding
   Site to be Mitral Valve with the concept modifier `(363698007, SCT,
   "Finding Site") <http://snomed.info/id/363698007>`__ = `(91134007,
   SCT, "Mitral Valve") <http://snomed.info/id/91134007>`__.Therefore,
   the Finding Site modifier does not appear in the right column.

.. _sect_N.3.10:

Pulmonary Vein
~~~~~~~~~~~~~~

+----------------------+----------------------+----------------------+
| Name of ASE Concept  | Base Measurement     | Concept or           |
|                      | Concept Name         | Acquisition Context  |
|                      |                      | Modifiers            |
+======================+======================+======================+
| Pulmonary Vein       | `(29450-4, LN,       |                      |
| Systolic Peak        | "Pulmonary Vein      |                      |
| Velocity             | Systolic Peak        |                      |
|                      | V                    |                      |
|                      | elocity") <http://lo |                      |
|                      | inc.org/29450-4/>`__ |                      |
+----------------------+----------------------+----------------------+
| Pulmonary Vein       | `(29451-2, LN,       |                      |
| Diastolic Peak       | "Pulmonary Vein      |                      |
| Velocity             | Diastolic Peak       |                      |
|                      | V                    |                      |
|                      | elocity") <http://lo |                      |
|                      | inc.org/29451-2/>`__ |                      |
+----------------------+----------------------+----------------------+
| Pulmonary Vein       | `(29452-0, LN,       |                      |
| Systolic to          | "Pulmonary Vein      |                      |
| Diastolic Ratio      | Systolic to          |                      |
|                      | Diastolic            |                      |
|                      | Ratio") <http://lo   |                      |
|                      | inc.org/29452-0/>`__ |                      |
+----------------------+----------------------+----------------------+
| Pulmonary Vein       | `(29453-8, LN,       |                      |
| Atrial Contraction   | "Pulmonary Vein      |                      |
| Reversal Peak        | Atrial Contraction   |                      |
| Velocity             | Reversal Peak        |                      |
|                      | V                    |                      |
|                      | elocity") <http://lo |                      |
|                      | inc.org/29453-8/>`__ |                      |
+----------------------+----------------------+----------------------+
| Right Upper          | `(29450-4, LN,       | `(106233006, SCT,    |
| Pulmonary Vein Peak  | "Pulmonary Vein      | "Topographical       |
| Systolic Velocity    | Systolic Peak        | Modifie              |
|                      | V                    | r") <http://snomed.i |
|                      | elocity") <http://lo | nfo/id/106233006>`__ |
|                      | inc.org/29450-4/>`__ | = `(255499006, SCT,  |
|                      |                      | "Right Upper         |
|                      |                      | Segmen               |
|                      |                      | t") <http://snomed.i |
|                      |                      | nfo/id/255499006>`__ |
+----------------------+----------------------+----------------------+
| Right Upper          | `(29451-2, LN,       | `(106233006, SCT,    |
| Pulmonary Vein       | "Pulmonary Vein      | "Topographical       |
| Diastolic Peak       | Diastolic Peak       | Modifie              |
| Velocity             | V                    | r") <http://snomed.i |
|                      | elocity") <http://lo | nfo/id/106233006>`__ |
|                      | inc.org/29451-2/>`__ | = `(255499006, SCT,  |
|                      |                      | "Right Upper         |
|                      |                      | Segmen               |
|                      |                      | t") <http://snomed.i |
|                      |                      | nfo/id/255499006>`__ |
+----------------------+----------------------+----------------------+
| Right Upper          | `(29452-0, LN,       | `(106233006, SCT,    |
| Pulmonary Vein       | "Pulmonary Vein      | "Anatomic Site       |
| Systolic to          | Systolic to          | Modifie              |
| Diastolic Velocity   | Diastolic            | r") <http://snomed.i |
| Ratio                | Ratio") <http://lo   | nfo/id/106233006>`__ |
|                      | inc.org/29452-0/>`__ | = `(255499006, SCT,  |
|                      |                      | "Right Upper         |
|                      |                      | Segmen               |
|                      |                      | t") <http://snomed.i |
|                      |                      | nfo/id/255499006>`__ |
+----------------------+----------------------+----------------------+
| Right Lower          | `(29450-4, LN,       | `(106233006, SCT,    |
| Pulmonary Vein Peak  | "Pulmonary Vein      | "Topographical       |
| Systolic Velocity    | Systolic Peak        | Modifie              |
|                      | V                    | r") <http://snomed.i |
|                      | elocity") <http://lo | nfo/id/106233006>`__ |
|                      | inc.org/29450-4/>`__ | = `(255496004, SCT,  |
|                      |                      | "Right Lower         |
|                      |                      | Segmen               |
|                      |                      | t") <http://snomed.i |
|                      |                      | nfo/id/255496004>`__ |
+----------------------+----------------------+----------------------+
| Right Lower          | `(29451-2, LN,       | `(106233006, SCT,    |
| Pulmonary Vein       | "Pulmonary Vein      | "Topographical       |
| Diastolic Peak       | Diastolic Peak       | Modifie              |
| Velocity             | V                    | r") <http://snomed.i |
|                      | elocity") <http://lo | nfo/id/106233006>`__ |
|                      | inc.org/29451-2/>`__ | = `(255496004, SCT,  |
|                      |                      | "Right Lower         |
|                      |                      | Segmen               |
|                      |                      | t") <http://snomed.i |
|                      |                      | nfo/id/255496004>`__ |
+----------------------+----------------------+----------------------+
| Right Lower          | `(29452-0, LN,       | `(106233006, SCT,    |
| Pulmonary Vein       | "Pulmonary Vein      | "Topographical       |
| Systolic to          | Systolic to          | Modifie              |
| Diastolic Velocity   | Diastolic            | r") <http://snomed.i |
| Ratio                | Ratio") <http://lo   | nfo/id/106233006>`__ |
|                      | inc.org/29452-0/>`__ | = `(255496004, SCT,  |
|                      |                      | "Right Lower         |
|                      |                      | Segmen               |
|                      |                      | t") <http://snomed.i |
|                      |                      | nfo/id/255496004>`__ |
+----------------------+----------------------+----------------------+
| Left Upper Pulmonary | `(29450-4, LN,       | `(106233006, SCT,    |
| Vein Peak Systolic   | "Pulmonary Vein      | "Topographical       |
| Velocity             | Systolic Peak        | Modifie              |
|                      | V                    | r") <http://snomed.i |
|                      | elocity") <http://lo | nfo/id/106233006>`__ |
|                      | inc.org/29450-4/>`__ | = `(255482005, SCT,  |
|                      |                      | "Left Upper          |
|                      |                      | Segmen               |
|                      |                      | t") <http://snomed.i |
|                      |                      | nfo/id/255482005>`__ |
+----------------------+----------------------+----------------------+
| Left Upper Pulmonary | `(29451-2, LN,       | `(106233006, SCT,    |
| Vein Velocity Peak   | "Pulmonary Vein      | "Topographical       |
| Diastolic            | Diastolic Peak       | Modifie              |
|                      | V                    | r") <http://snomed.i |
|                      | elocity") <http://lo | nfo/id/106233006>`__ |
|                      | inc.org/29451-2/>`__ | = `(255482005, SCT,  |
|                      |                      | "Left Upper          |
|                      |                      | Segmen               |
|                      |                      | t") <http://snomed.i |
|                      |                      | nfo/id/255482005>`__ |
+----------------------+----------------------+----------------------+
| Left Upper Pulmonary | `(29452-0, LN,       | `(106233006, SCT,    |
| Vein Systolic to     | "Pulmonary Vein      | "Topographical       |
| Diastolic Velocity   | Systolic to          | Modifie              |
| Ratio                | Diastolic            | r") <http://snomed.i |
|                      | Ratio") <http://lo   | nfo/id/106233006>`__ |
|                      | inc.org/29452-0/>`__ | = `(255482005, SCT,  |
|                      |                      | "Left Upper          |
|                      |                      | Segmen               |
|                      |                      | t") <http://snomed.i |
|                      |                      | nfo/id/255482005>`__ |
+----------------------+----------------------+----------------------+
| Left Lower Pulmonary | `(29450-4, LN,       | `(106233006, SCT,    |
| Vein Peak Systolic   | "Pulmonary Vein      | "Topographical       |
| Velocity             | Systolic Peak        | Modifie              |
|                      | V                    | r") <http://snomed.i |
|                      | elocity") <http://lo | nfo/id/106233006>`__ |
|                      | inc.org/29450-4/>`__ | = `(264068005, SCT,  |
|                      |                      | "Left Lower          |
|                      |                      | Segmen               |
|                      |                      | t") <http://snomed.i |
|                      |                      | nfo/id/264068005>`__ |
+----------------------+----------------------+----------------------+
| Left Lower Pulmonary | `(29451-2, LN,       | `(106233006, SCT,    |
| Vein Diastolic Peak  | "Pulmonary Vein      | "Topographical       |
| Velocity             | Diastolic Peak       | Modifie              |
|                      | V                    | r") <http://snomed.i |
|                      | elocity") <http://lo | nfo/id/106233006>`__ |
|                      | inc.org/29451-2/>`__ | = `(264068005, SCT,  |
|                      |                      | "Left Lower          |
|                      |                      | Segmen               |
|                      |                      | t") <http://snomed.i |
|                      |                      | nfo/id/264068005>`__ |
+----------------------+----------------------+----------------------+
| Left Lower Pulmonary | `(29452-0, LN,       | `(106233006, SCT,    |
| Vein Systolic to     | "Pulmonary Vein      | "Topographical       |
| Diastolic Velocity   | Systolic to          | Modifie              |
| Ratio                | Diastolic            | r") <http://snomed.i |
|                      | Ratio") <http://lo   | nfo/id/106233006>`__ |
|                      | inc.org/29452-0/>`__ | = `(264068005, SCT,  |
|                      |                      | "Left Lower          |
|                      |                      | Segmen               |
|                      |                      | t") <http://snomed.i |
|                      |                      | nfo/id/264068005>`__ |
+----------------------+----------------------+----------------------+

.. _sect_N.3.11:

Left Atrium / Appendage
~~~~~~~~~~~~~~~~~~~~~~~

+----------------------+----------------------+----------------------+
| Name of ASE Concept  | Base Measurement     | Concept or           |
|                      | Concept Name         | Acquisition Context  |
|                      |                      | Modifiers            |
+======================+======================+======================+
| Left Atrium          | `(29469-4, LN, "Left |                      |
| Antero-posterior     | Atrium               |                      |
| Systolic Dimension   | Antero-posterior     |                      |
|                      | Systolic             |                      |
|                      | Di                   |                      |
|                      | mension") <http://lo |                      |
|                      | inc.org/29469-4/>`__ |                      |
+----------------------+----------------------+----------------------+
| Left Atrial          | `(29469-4, LN, "Left | `(399264008, SCT,    |
| Antero-posterior     | Atrium               | "Image               |
| Systolic Dimension   | Antero-posterior     | Mod                  |
| by M-Mode            | Systolic             | e") <http://snomed.i |
|                      | Di                   | nfo/id/399264008>`__ |
|                      | mension") <http://lo | = `(399155008, SCT,  |
|                      | inc.org/29469-4/>`__ | "M                   |
|                      |                      | mod                  |
|                      |                      | e") <http://snomed.i |
|                      |                      | nfo/id/399155008>`__ |
+----------------------+----------------------+----------------------+
| Left Atrial          | `(29469-4, LN, "Left | `(399264008, SCT,    |
| Antero-posterior     | Atrium               | "Image               |
| Systolic Dimension   | Antero-posterior     | Mod                  |
| by 2-D               | Systolic             | e") <http://snomed.i |
|                      | Di                   | nfo/id/399264008>`__ |
|                      | mension") <http://lo | = `(399064001, SCT,  |
|                      | inc.org/29469-4/>`__ | "2D                  |
|                      |                      | mod                  |
|                      |                      | e") <http://snomed.i |
|                      |                      | nfo/id/399064001>`__ |
+----------------------+----------------------+----------------------+
| Left Atrium to       | `(17985-3, LN, "Left |                      |
| Aortic Root Ratio    | Atrium to Aortic     |                      |
|                      | Root                 |                      |
|                      | Ratio") <http://lo   |                      |
|                      | inc.org/17985-3/>`__ |                      |
+----------------------+----------------------+----------------------+
| Left Atrial          | `(29486-8, LN, "Left |                      |
| Appendage Peak       | Atrial Appendage     |                      |
| Velocity             | Peak                 |                      |
|                      | V                    |                      |
|                      | elocity") <http://lo |                      |
|                      | inc.org/29486-8/>`__ |                      |
+----------------------+----------------------+----------------------+
| Left Atrium Systolic | `(17977-0, LN, "Left | `(272518008, SCT,    |
| Area                 | Atrium Area A4C      | "Cardiac Cycle       |
|                      | view") <http://lo    | Poin                 |
|                      | inc.org/17977-0/>`__ | t") <http://snomed.i |
|                      |                      | nfo/id/272518008>`__ |
|                      |                      | = `(111973004, SCT,  |
|                      |                      | "Systol              |
|                      |                      | e") <http://snomed.i |
|                      |                      | nfo/id/111973004>`__ |
+----------------------+----------------------+----------------------+
| Left Atrium Systolic | `(399235004, SCT,    |                      |
| Volume               | "Left Atrium         |                      |
|                      | Systolic             |                      |
|                      | Volum                |                      |
|                      | e") <http://snomed.i |                      |
|                      | nfo/id/399235004>`__ |                      |
+----------------------+----------------------+----------------------+

.. _sect_N.3.12:

Right Ventricle
~~~~~~~~~~~~~~~

+----------------------+----------------------+----------------------+
| Name of ASE Concept  | Base Measurement     | Concept or           |
|                      | Concept Name         | Acquisition Context  |
|                      |                      | Modifiers            |
+======================+======================+======================+
| Right Ventricular    | `(20304-2, LN,       | `(399264008, SCT,    |
| Internal Diastolic   | "Right Ventricular   | "Image               |
| Dimension by M-Mode  | Internal Diastolic   | Mod                  |
|                      | Di                   | e") <http://snomed.i |
|                      | mension") <http://lo | nfo/id/399264008>`__ |
|                      | inc.org/20304-2/>`__ | = `(399155008, SCT,  |
|                      |                      | "M                   |
|                      |                      | mod                  |
|                      |                      | e") <http://snomed.i |
|                      |                      | nfo/id/399155008>`__ |
+----------------------+----------------------+----------------------+
| Right Ventricular    | `(20304-2, LN,       | `(399264008, SCT,    |
| Internal Diastolic   | "Right Ventricular   | "Image               |
| Dimension by 2-D     | Internal Diastolic   | Mod                  |
|                      | Di                   | e") <http://snomed.i |
|                      | mension") <http://lo | nfo/id/399264008>`__ |
|                      | inc.org/20304-2/>`__ | = `(399064001, SCT,  |
|                      |                      | "2D                  |
|                      |                      | mod                  |
|                      |                      | e") <http://snomed.i |
|                      |                      | nfo/id/399064001>`__ |
+----------------------+----------------------+----------------------+
| Right Ventricular    | `(11726-7, LN, "Peak | `(363698007, SCT,    |
| Outflow Tract        | V                    | "Finding             |
| Systolic Peak        | elocity") <http://lo | Sit                  |
| Velocity             | inc.org/11726-7/>`__ | e") <http://snomed.i |
|                      |                      | nfo/id/363698007>`__ |
|                      |                      | = `(44627009, SCT,   |
|                      |                      | "Right Ventricular   |
|                      |                      | Outflow              |
|                      |                      | Tra                  |
|                      |                      | ct") <http://snomed. |
|                      |                      | info/id/44627009>`__ |
+----------------------+----------------------+----------------------+
| Right Ventricular    | `(20354-7, LN,       | `(363698007, SCT,    |
| Outflow Tract        | "Velocity Time       | "Finding             |
| Systolic Velocity    | I                    | Sit                  |
| Time Integral        | ntegral") <http://lo | e") <http://snomed.i |
|                      | inc.org/20354-7/>`__ | nfo/id/363698007>`__ |
|                      |                      | = `(44627009, SCT,   |
|                      |                      | "Right Ventricular   |
|                      |                      | Outflow              |
|                      |                      | Tra                  |
|                      |                      | ct") <http://snomed. |
|                      |                      | info/id/44627009>`__ |
+----------------------+----------------------+----------------------+
| Right Ventricular    | `(399027007, SCT,    | `(363698007, SCT,    |
| Outflow Systolic     | "Cardiovascular      | "Finding             |
| Diameter by 2-D      | Orifice              | Sit                  |
|                      | Diamete              | e") <http://snomed.i |
|                      | r") <http://snomed.i | nfo/id/363698007>`__ |
|                      | nfo/id/399027007>`__ | = `(44627009, SCT,   |
|                      |                      | "Right Ventricular   |
|                      |                      | Outflow              |
|                      |                      | Tra                  |
|                      |                      | ct") <http://snomed. |
|                      |                      | info/id/44627009>`__ |
|                      |                      |                      |
|                      |                      | `(399264008, SCT,    |
|                      |                      | "Image               |
|                      |                      | Mod                  |
|                      |                      | e") <http://snomed.i |
|                      |                      | nfo/id/399264008>`__ |
|                      |                      | = `(399064001, SCT,  |
|                      |                      | "2D                  |
|                      |                      | mod                  |
|                      |                      | e") <http://snomed.i |
|                      |                      | nfo/id/399064001>`__ |
+----------------------+----------------------+----------------------+
| Right Ventricular    | `(20247-3, LN, "Peak | `(363698007, SCT,    |
| Outflow Tract        | G                    | "Finding             |
| Systolic Peak        | radient") <http://lo | Sit                  |
| Instantaneous        | inc.org/20247-3/>`__ | e") <http://snomed.i |
| Gradient             |                      | nfo/id/363698007>`__ |
|                      |                      | = `(44627009, SCT,   |
|                      |                      | "Right Ventricular   |
|                      |                      | Outflow              |
|                      |                      | Tra                  |
|                      |                      | ct") <http://snomed. |
|                      |                      | info/id/44627009>`__ |
+----------------------+----------------------+----------------------+
| Right Ventricular    | `(20256-4, LN, "Mean | `(363698007, SCT,    |
| Outflow Tract        | G                    | "Finding             |
| Systolic Mean        | radient") <http://lo | Sit                  |
| Gradient             | inc.org/20256-4/>`__ | e") <http://snomed.i |
|                      |                      | nfo/id/363698007>`__ |
|                      |                      | = `(44627009, SCT,   |
|                      |                      | "Right Ventricular   |
|                      |                      | Outflow              |
|                      |                      | Tra                  |
|                      |                      | ct") <http://snomed. |
|                      |                      | info/id/44627009>`__ |
+----------------------+----------------------+----------------------+
| Right Ventricular    | `(90096001, SCT,     | `(370129005, SCT,    |
| Stroke Volume by     | "Stroke              | "Measurement         |
| Doppler Volume       | Volu                 | Metho                |
| Outflow              | me") <http://snomed. | d") <http://snomed.i |
|                      | info/id/90096001>`__ | nfo/id/370129005>`__ |
|                      |                      | = (125219, DCM,      |
|                      |                      | "Doppler Volume      |
|                      |                      | Flow") `(363698007,  |
|                      |                      | SCT, "Finding        |
|                      |                      | Sit                  |
|                      |                      | e") <http://snomed.i |
|                      |                      | nfo/id/363698007>`__ |
|                      |                      | = `(44627009, SCT,   |
|                      |                      | "Right Ventricular   |
|                      |                      | Outflow              |
|                      |                      | Tra                  |
|                      |                      | ct") <http://snomed. |
|                      |                      | info/id/44627009>`__ |
+----------------------+----------------------+----------------------+
| Right Ventricular    | `(399367004, SCT,    | `(363698007, SCT,    |
| Outflow Tract Area   | "Cardiovascular      | "Finding             |
|                      | Orifice              | Sit                  |
|                      | Are                  | e") <http://snomed.i |
|                      | a") <http://snomed.i | nfo/id/363698007>`__ |
|                      | nfo/id/399367004>`__ | = `(44627009, SCT,   |
|                      |                      | "Right Ventricular   |
|                      |                      | Outflow              |
|                      |                      | Tra                  |
|                      |                      | ct") <http://snomed. |
|                      |                      | info/id/44627009>`__ |
+----------------------+----------------------+----------------------+
| Right Ventricular    | `(20352-1, LN, "Mean | `(363698007, SCT,    |
| Outflow Tract Mean   | V                    | "Finding             |
| Velocity             | elocity") <http://lo | Sit                  |
|                      | inc.org/20352-1/>`__ | e") <http://snomed.i |
|                      |                      | nfo/id/363698007>`__ |
|                      |                      | = `(44627009, SCT,   |
|                      |                      | "Right Ventricular   |
|                      |                      | Outflow              |
|                      |                      | Tra                  |
|                      |                      | ct") <http://snomed. |
|                      |                      | info/id/44627009>`__ |
+----------------------+----------------------+----------------------+
| Right Ventricle      | `(18153-7, LN,       |                      |
| Anterior Wall        | "Right Ventricle     |                      |
| Diastolic Thickness  | Anterior Wall        |                      |
|                      | Diastolic            |                      |
|                      | Th                   |                      |
|                      | ickness") <http://lo |                      |
|                      | inc.org/18153-7/>`__ |                      |
+----------------------+----------------------+----------------------+
| Right Ventricular    | `(18157-8, LN,       |                      |
| Anterior Wall        | "Right Ventricular   |                      |
| Systolic Thickness   | Anterior Wall        |                      |
|                      | Systolic             |                      |
|                      | Th                   |                      |
|                      | ickness") <http://lo |                      |
|                      | inc.org/18157-8/>`__ |                      |
+----------------------+----------------------+----------------------+
| Right Ventricular    | `(399023006, SCT,    |                      |
| Peak Systolic        | "Right Ventricular   |                      |
| Pressure             | Peak Systolic        |                      |
|                      | Pressur              |                      |
|                      | e") <http://snomed.i |                      |
|                      | nfo/id/399023006>`__ |                      |
+----------------------+----------------------+----------------------+

.. _sect_N.3.13:

Pulmonic Valve / Pulmonic Artery
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------------+----------------------+----------------------+
| Name of ASE Concept  | Base Measurement     | Concept or           |
|                      | Concept Name         | Acquisition Context  |
|                      |                      | Modifiers            |
+======================+======================+======================+
| Main Pulmonary       | `(18020-8, LN, "Main |                      |
| Artery Diameter      | Pulmonary Artery     |                      |
|                      | D                    |                      |
|                      | iameter") <http://lo |                      |
|                      | inc.org/18020-8/>`__ |                      |
+----------------------+----------------------+----------------------+
| Main Pulmonary       | `(399048009, SCT,    |                      |
| Artery Velocity      | "Main Pulmonary      |                      |
|                      | Artery               |                      |
|                      | Velocit              |                      |
|                      | y") <http://snomed.i |                      |
|                      | nfo/id/399048009>`__ |                      |
+----------------------+----------------------+----------------------+
| Right Pulmonary      | `(18021-6, LN,       |                      |
| Artery Diameter      | "Right Pulmonary     |                      |
|                      | Artery               |                      |
|                      | D                    |                      |
|                      | iameter") <http://lo |                      |
|                      | inc.org/18021-6/>`__ |                      |
+----------------------+----------------------+----------------------+
| Left Pulmonary       | `(18019-0, LN, "Left |                      |
| Artery Diameter      | Pulmonary Artery     |                      |
|                      | D                    |                      |
|                      | iameter") <http://lo |                      |
|                      | inc.org/18019-0/>`__ |                      |
+----------------------+----------------------+----------------------+
| Pulmonic Valve       | `(20247-3, LN, "Peak | `(260674002, SCT,    |
| Systolic Peak        | G                    | "Direction of        |
| Instantaneous        | radient") <http://lo | Flo                  |
| Gradient             | inc.org/20247-3/>`__ | w") <http://snomed.i |
|                      |                      | nfo/id/260674002>`__ |
|                      |                      | = `(263677008, SCT,  |
|                      |                      | "Antegrade           |
|                      |                      | Flo                  |
|                      |                      | w") <http://snomed.i |
|                      |                      | nfo/id/263677008>`__ |
+----------------------+----------------------+----------------------+
| Pulmonic Valve       | `(20256-4, LN, "Mean | `(260674002, SCT,    |
| Systolic Mean        | G                    | "Direction of        |
| Gradient             | radient") <http://lo | Flo                  |
|                      | inc.org/20256-4/>`__ | w") <http://snomed.i |
|                      |                      | nfo/id/260674002>`__ |
|                      |                      | = `(263677008, SCT,  |
|                      |                      | "Antegrade           |
|                      |                      | Flo                  |
|                      |                      | w") <http://snomed.i |
|                      |                      | nfo/id/263677008>`__ |
+----------------------+----------------------+----------------------+
| Pulmonic Valve       | (20354-7, LN,        | `(260674002, SCT,    |
| Systolic Peak        | 11726-7, LN, "Peak   | "Direction of        |
| Velocity             | Velocity")           | Flo                  |
|                      |                      | w") <http://snomed.i |
|                      |                      | nfo/id/260674002>`__ |
|                      |                      | = `(263677008, SCT,  |
|                      |                      | "Antegrade           |
|                      |                      | Flo                  |
|                      |                      | w") <http://snomed.i |
|                      |                      | nfo/id/263677008>`__ |
+----------------------+----------------------+----------------------+
| Pulmonic Valve       | `(20354-7, LN,       | `(260674002, SCT,    |
| Systolic Velocity    | "Velocity Time       | "Direction of        |
| Time Integral        | I                    | Flo                  |
|                      | ntegral") <http://lo | w") <http://snomed.i |
|                      | inc.org/20354-7/>`__ | nfo/id/260674002>`__ |
|                      |                      | = `(263677008, SCT,  |
|                      |                      | "Antegrade           |
|                      |                      | Flo                  |
|                      |                      | w") <http://snomed.i |
|                      |                      | nfo/id/263677008>`__ |
+----------------------+----------------------+----------------------+
| Pulmonic Valve Area  | `(18096-8, LN,       |                      |
| by Continuity        | "Pulmonic valve Area |                      |
|                      | by                   |                      |
|                      | Con                  |                      |
|                      | tinuity") <http://lo |                      |
|                      | inc.org/18096-8/>`__ |                      |
+----------------------+----------------------+----------------------+
| Pulmonic Valve       | `(20168-1, LN,       | `(260674002, SCT,    |
| Acceleration Time    | "Acceleration        | "Direction of        |
|                      | Time") <http://lo    | Flo                  |
|                      | inc.org/20168-1/>`__ | w") <http://snomed.i |
|                      |                      | nfo/id/260674002>`__ |
|                      |                      | = `(312004007, SCT,  |
|                      |                      | "Regurgitant         |
|                      |                      | Flo                  |
|                      |                      | w") <http://snomed.i |
|                      |                      | nfo/id/312004007>`__ |
+----------------------+----------------------+----------------------+
| Pulmonic Valve       | `(11653-3, LN, "End  | `(260674002, SCT,    |
| Regurgitant End      | Diastolic            | "Direction of        |
| Diastolic Velocity   | V                    | Flo                  |
|                      | elocity") <http://lo | w") <http://snomed.i |
|                      | inc.org/11653-3/>`__ | nfo/id/260674002>`__ |
|                      |                      | = `(312004007, SCT,  |
|                      |                      | "Regurgitant         |
|                      |                      | Flo                  |
|                      |                      | w") <http://snomed.i |
|                      |                      | nfo/id/312004007>`__ |
+----------------------+----------------------+----------------------+
| Pulmonic Valve       | `(11726-7, LN, "Peak | `(260674002, SCT,    |
| Regurgitant          | V                    | "Direction of        |
| Diastolic Peak       | elocity") <http://lo | Flo                  |
| Velocity             | inc.org/11726-7/>`__ | w") <http://snomed.i |
|                      |                      | nfo/id/260674002>`__ |
|                      |                      | = `(312004007, SCT,  |
|                      |                      | "Regurgitant         |
|                      |                      | Flo                  |
|                      |                      | w") <http://snomed.i |
|                      |                      | nfo/id/312004007>`__ |
+----------------------+----------------------+----------------------+

.. note::

   Pulmonic Valve measurements appear in , which specifies the Finding
   Site to be Pulmonic Valve with the concept modifier `(363698007, SCT,
   "Finding Site") <http://snomed.info/id/363698007>`__ = `(46030003,
   SCT, "Pulmonic Valve") <http://snomed.info/id/46030003>`__.
   Therefore, this Finding Site concept modifier does not appear in the
   right column.

.. _sect_N.3.14:

Tricuspid Valve
~~~~~~~~~~~~~~~

+----------------------+----------------------+----------------------+
| Name of ASE Concept  | Base Measurement     | Concept or           |
|                      | Concept Name         | Acquisition Context  |
|                      |                      | Modifiers            |
+======================+======================+======================+
| Tricuspid Valve Mean | `(20352-1, LN, "Mean | `(260674002, SCT,    |
| Diastolic Velocity   | V                    | "Direction of        |
|                      | elocity") <http://lo | Flo                  |
|                      | inc.org/20352-1/>`__ | w") <http://snomed.i |
|                      |                      | nfo/id/260674002>`__ |
|                      |                      | = `(263677008, SCT,  |
|                      |                      | "Antegrade           |
|                      |                      | Flo                  |
|                      |                      | w") <http://snomed.i |
|                      |                      | nfo/id/263677008>`__ |
+----------------------+----------------------+----------------------+
| Tricuspid Valve E    | `(18031-5, LN,       |                      |
| Wave Peak Velocity   | "Tricuspid Valve E   |                      |
|                      | Wave Peak            |                      |
|                      | V                    |                      |
|                      | elocity") <http://lo |                      |
|                      | inc.org/18031-5/>`__ |                      |
+----------------------+----------------------+----------------------+
| Tricuspid Valve A    | `(18030-7, LN,       |                      |
| Wave Peak Velocity   | "Tricuspid Valve A   |                      |
|                      | Wave Peak            |                      |
|                      | V                    |                      |
|                      | elocity") <http://lo |                      |
|                      | inc.org/18030-7/>`__ |                      |
+----------------------+----------------------+----------------------+
| Tricuspid Valve      | `(20354-7, LN,       | `(260674002, SCT,    |
| Diastolic Velocity   | "Velocity Time       | "Direction of        |
| Time Integral        | I                    | Flo                  |
|                      | ntegral") <http://lo | w") <http://snomed.i |
|                      | inc.org/20354-7/>`__ | nfo/id/260674002>`__ |
|                      |                      | = `(263677008, SCT,  |
|                      |                      | "Antegrade           |
|                      |                      | Flo                  |
|                      |                      | w") <http://snomed.i |
|                      |                      | nfo/id/263677008>`__ |
+----------------------+----------------------+----------------------+
| Tricuspid Valve Peak | (20247-3, LN, Peak   | `(260674002, SCT,    |
| Diastolic Gradient   | Gradient")           | "Direction of        |
|                      |                      | Flo                  |
|                      |                      | w") <http://snomed.i |
|                      |                      | nfo/id/260674002>`__ |
|                      |                      | = `(263677008, SCT,  |
|                      |                      | "Antegrade           |
|                      |                      | Flo                  |
|                      |                      | w") <http://snomed.i |
|                      |                      | nfo/id/263677008>`__ |
+----------------------+----------------------+----------------------+
| Tricuspid Valve Mean | (20256-4, LN, Mean   | `(260674002, SCT,    |
| Diastolic Gradient   | Gradient")           | "Direction of        |
|                      |                      | Flo                  |
|                      |                      | w") <http://snomed.i |
|                      |                      | nfo/id/260674002>`__ |
|                      |                      | = `(263677008, SCT,  |
|                      |                      | "Antegrade           |
|                      |                      | Flo                  |
|                      |                      | w") <http://snomed.i |
|                      |                      | nfo/id/263677008>`__ |
+----------------------+----------------------+----------------------+
| Tricuspid Valve      | (399027007, SCT,     | `(363698007, SCT,    |
| Annulus Diastolic    | Cardiovascular       | "Finding             |
| Diameter             | Orifice Diameter")   | Sit                  |
|                      |                      | e") <http://snomed.i |
|                      |                      | nfo/id/363698007>`__ |
|                      |                      | = `(279170002, SCT,  |
|                      |                      | "Tricuspid           |
|                      |                      | Annulu               |
|                      |                      | s") <http://snomed.i |
|                      |                      | nfo/id/279170002>`__ |
|                      |                      |                      |
|                      |                      | `(260674002, SCT,    |
|                      |                      | "Direction of        |
|                      |                      | Flo                  |
|                      |                      | w") <http://snomed.i |
|                      |                      | nfo/id/260674002>`__ |
|                      |                      | = `(263677008, SCT,  |
|                      |                      | "Antegrade           |
|                      |                      | Flo                  |
|                      |                      | w") <http://snomed.i |
|                      |                      | nfo/id/263677008>`__ |
+----------------------+----------------------+----------------------+
| Tricuspid Valve      | `(11726-7, LN, "Peak | `(260674002, SCT,    |
| Regurgitant Peak     | V                    | "Direction of        |
| Velocity             | elocity") <http://lo | Flo                  |
|                      | inc.org/11726-7/>`__ | w") <http://snomed.i |
|                      |                      | nfo/id/260674002>`__ |
|                      |                      | = `(312004007, SCT,  |
|                      |                      | "Regurgitant         |
|                      |                      | Flo                  |
|                      |                      | w") <http://snomed.i |
|                      |                      | nfo/id/312004007>`__ |
+----------------------+----------------------+----------------------+
| Tricuspid            | `(20247-3, LN, "Peak | `(260674002, SCT,    |
| Regurgitation Peak   | G                    | "Direction of        |
| Pressure Gradient    | radient") <http://lo | Flo                  |
|                      | inc.org/20247-3/>`__ | w") <http://snomed.i |
|                      |                      | nfo/id/260674002>`__ |
|                      |                      | = `(312004007, SCT,  |
|                      |                      | "Regurgitant         |
|                      |                      | Flo                  |
|                      |                      | w") <http://snomed.i |
|                      |                      | nfo/id/312004007>`__ |
+----------------------+----------------------+----------------------+
| Tricuspid            | `(20354-7, LN,       | `(260674002, SCT,    |
| Regurgitation        | "Velocity Time       | "Direction of        |
| Velocity Time        | I                    | Flo                  |
| Integral             | ntegral") <http://lo | w") <http://snomed.i |
|                      | inc.org/20354-7/>`__ | nfo/id/260674002>`__ |
|                      |                      | = `(312004007, SCT,  |
|                      |                      | "Regurgitant         |
|                      |                      | Flo                  |
|                      |                      | w") <http://snomed.i |
|                      |                      | nfo/id/312004007>`__ |
+----------------------+----------------------+----------------------+
| Tricuspid Valve      | `(20217-6, LN,       | `(260674002, SCT,    |
| Deceleration Time    | "Deceleration        | "Direction of        |
|                      | Time") <http://lo    | Flo                  |
|                      | inc.org/20217-6/>`__ | w") <http://snomed.i |
|                      |                      | nfo/id/260674002>`__ |
|                      |                      | = `(263677008, SCT,  |
|                      |                      | "Antegrade           |
|                      |                      | Flo                  |
|                      |                      | w") <http://snomed.i |
|                      |                      | nfo/id/263677008>`__ |
+----------------------+----------------------+----------------------+

.. note::

   TRICUSPID Valve measurements appear in , which specifies the Finding
   Site to be Tricuspid Valve with the concept modifier `(363698007,
   SCT, "Finding Site") <http://snomed.info/id/363698007>`__ =
   `(46030003, SCT, "Tricuspid
   Valve") <http://snomed.info/id/46030003>`__. Therefore, the Finding
   Site modifier does not appear in the right column.

.. _sect_N.3.15:

Right Atrium / Inferior Vena Cava
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------------+----------------------+----------------------+
| Name of ASE Concept  | Base Measurement     | Concept or           |
|                      | Concept Name         | Acquisition Context  |
|                      |                      | Modifiers            |
+======================+======================+======================+
| Right Atrium         | `(18070-3, LN,       |                      |
| Systolic Pressure    | "Right Atrium        |                      |
|                      | Systolic             |                      |
|                      | P                    |                      |
|                      | ressure") <http://lo |                      |
|                      | inc.org/18070-3/>`__ |                      |
+----------------------+----------------------+----------------------+
| Right Atrium         | `(17988-7, LN,       | `(272518008, SCT,    |
| Systolic Area        | "Right Atrium Area   | "Cardiac Cycle       |
|                      | A4C                  | Poin                 |
|                      | view") <http://lo    | t") <http://snomed.i |
|                      | inc.org/17988-7/>`__ | nfo/id/272518008>`__ |
|                      |                      | = `(111973004, SCT,  |
|                      |                      | "Systol              |
|                      |                      | e") <http://snomed.i |
|                      |                      | nfo/id/111973004>`__ |
+----------------------+----------------------+----------------------+
| Inferior Vena Cava   | `(18006-7, LN,       |                      |
| Diameter             | "Inferior Vena Cava  |                      |
|                      | D                    |                      |
|                      | iameter") <http://lo |                      |
|                      | inc.org/18006-7/>`__ |                      |
+----------------------+----------------------+----------------------+
| Inferior Vena Cava   | `(18006-7, LN,       | `(272517003, SCT,    |
| Diameter at          | "Inferior Vena Cava  | "Respiratory Cycle   |
| Inspiration          | D                    | Poin                 |
|                      | iameter") <http://lo | t") <http://snomed.i |
|                      | inc.org/18006-7/>`__ | nfo/id/272517003>`__ |
|                      |                      | = `(14910006, SCT,   |
|                      |                      | "During              |
|                      |                      | Inspirati            |
|                      |                      | on") <http://snomed. |
|                      |                      | info/id/14910006>`__ |
+----------------------+----------------------+----------------------+
| Inferior Vena Cava   | `(18006-7, LN,       | `(272517003, SCT,    |
| Diameter at          | "Inferior Vena Cava  | "Respiratory Cycle   |
| Expiration           | D                    | Poin                 |
|                      | iameter") <http://lo | t") <http://snomed.i |
|                      | inc.org/18006-7/>`__ | nfo/id/272517003>`__ |
|                      |                      | = `(58322009, SCT,   |
|                      |                      | "During              |
|                      |                      | Expirati             |
|                      |                      | on") <http://snomed. |
|                      |                      | info/id/58322009>`__ |
+----------------------+----------------------+----------------------+
| Inferior Vena Cava % | `(18050-5, LN,       |                      |
| Collapse             | "Inferior Vena Cava  |                      |
|                      | %                    |                      |
|                      | C                    |                      |
|                      | ollapse") <http://lo |                      |
|                      | inc.org/18050-5/>`__ |                      |
+----------------------+----------------------+----------------------+
| Hepatic Vein         | `(29471-0, LN,       |                      |
| Systolic Peak        | "Hepatic Vein        |                      |
| Velocity             | Systolic Peak        |                      |
|                      | V                    |                      |
|                      | elocity") <http://lo |                      |
|                      | inc.org/29471-0/>`__ |                      |
+----------------------+----------------------+----------------------+
| Hepatic Vein         | `(29472-8, LN,       |                      |
| Diastolic Peak       | "Hepatic Vein        |                      |
| Velocity             | Diastolic Peak       |                      |
|                      | V                    |                      |
|                      | elocity") <http://lo |                      |
|                      | inc.org/29472-8/>`__ |                      |
+----------------------+----------------------+----------------------+
| Hepatic Vein         | `(29473-6, LN,       |                      |
| Systolic to          | "Hepatic Vein        |                      |
| Diastolic Ratio      | Systolic to          |                      |
|                      | Diastolic            |                      |
|                      | Ratio") <http://lo   |                      |
|                      | inc.org/29473-6/>`__ |                      |
+----------------------+----------------------+----------------------+
| Hepatic Vein Atrial  | `(29474-4, LN,       |                      |
| Contraction Reversal | "Hepatic Vein Atrial |                      |
| Peak Velocity        | Contraction Reversal |                      |
|                      | Peak                 |                      |
|                      | V                    |                      |
|                      | elocity") <http://lo |                      |
|                      | inc.org/29474-4/>`__ |                      |
+----------------------+----------------------+----------------------+
| Hepatic Vein Peak    | `(29471-0, LN,       | `(272517003, SCT,    |
| Systolic Velocity at | "Hepatic Vein        | "Respiratory Cycle   |
| Inspiration          | Systolic Peak        | Poin                 |
|                      | V                    | t") <http://snomed.i |
|                      | elocity") <http://lo | nfo/id/272517003>`__ |
|                      | inc.org/29471-0/>`__ | = `(14910006, SCT,   |
|                      |                      | "During              |
|                      |                      | Inspirati            |
|                      |                      | on") <http://snomed. |
|                      |                      | info/id/14910006>`__ |
+----------------------+----------------------+----------------------+
| Hepatic Vein Peak    | `(29472-8, LN,       | `(272517003, SCT,    |
| Diastolic Velocity   | "Hepatic Vein        | "Respiratory Cycle   |
| at Inspiration       | Diastolic Peak       | Poin                 |
|                      | V                    | t") <http://snomed.i |
|                      | elocity") <http://lo | nfo/id/272517003>`__ |
|                      | inc.org/29472-8/>`__ | = `(14910006, SCT,   |
|                      |                      | "During              |
|                      |                      | Inspirati            |
|                      |                      | on") <http://snomed. |
|                      |                      | info/id/14910006>`__ |
+----------------------+----------------------+----------------------+
| Hepatic Vein         | `(29473-6, LN,       | `(272517003, SCT,    |
| Systolic to          | "Hepatic Vein        | "Respiratory Cycle   |
| Diastolic Ratio at   | Systolic to          | Poin                 |
| Inspiration          | Diastolic            | t") <http://snomed.i |
|                      | Ratio") <http://lo   | nfo/id/272517003>`__ |
|                      | inc.org/29473-6/>`__ | = `(14910006, SCT,   |
|                      |                      | "During              |
|                      |                      | Inspirati            |
|                      |                      | on") <http://snomed. |
|                      |                      | info/id/14910006>`__ |
+----------------------+----------------------+----------------------+
| Hepatic Vein Peak    | `(29474-4, LN,       | `(272517003, SCT,    |
| Atrial Contraction   | "Hepatic Vein Atrial | "Respiratory Cycle   |
| Reversal Velocity at | Contraction Reversal | Poin                 |
| Inspiration          | Peak                 | t") <http://snomed.i |
|                      | V                    | nfo/id/272517003>`__ |
|                      | elocity") <http://lo | = `(14910006, SCT,   |
|                      | inc.org/29474-4/>`__ | "During              |
|                      |                      | Inspirati            |
|                      |                      | on") <http://snomed. |
|                      |                      | info/id/14910006>`__ |
+----------------------+----------------------+----------------------+
| Hepatic Vein Peak    | `(29471-0, LN,       | `(272517003, SCT,    |
| Systolic Velocity at | "Hepatic Vein        | "Respiratory Cycle   |
| Expiration           | Systolic Peak        | Poin                 |
|                      | V                    | t") <http://snomed.i |
|                      | elocity") <http://lo | nfo/id/272517003>`__ |
|                      | inc.org/29471-0/>`__ | = `(58322009, SCT,   |
|                      |                      | "During              |
|                      |                      | Expirati             |
|                      |                      | on") <http://snomed. |
|                      |                      | info/id/58322009>`__ |
+----------------------+----------------------+----------------------+
| Hepatic Vein Peak    | `(29472-8, LN,       | `(272517003, SCT,    |
| Diastolic Velocity   | "Hepatic Vein        | "Respiratory Cycle   |
| at Expiration        | Diastolic Peak       | Poin                 |
|                      | V                    | t") <http://snomed.i |
|                      | elocity") <http://lo | nfo/id/272517003>`__ |
|                      | inc.org/29472-8/>`__ | = `(58322009, SCT,   |
|                      |                      | "During              |
|                      |                      | Expirati             |
|                      |                      | on") <http://snomed. |
|                      |                      | info/id/58322009>`__ |
+----------------------+----------------------+----------------------+
| Hepatic Vein         | `(29473-6, LN,       | `(272517003, SCT,    |
| Systolic to          | "Hepatic Vein        | "Respiratory Cycle   |
| Diastolic Ratio at   | Systolic to          | Poin                 |
| Expiration           | Diastolic            | t") <http://snomed.i |
|                      | Ratio") <http://lo   | nfo/id/272517003>`__ |
|                      | inc.org/29473-6/>`__ | = `(58322009, SCT,   |
|                      |                      | "During              |
|                      |                      | Expirati             |
|                      |                      | on") <http://snomed. |
|                      |                      | info/id/58322009>`__ |
+----------------------+----------------------+----------------------+
| Hepatic Vein Peak    | `(29474-4, LN,       | `(272517003, SCT,    |
| Atrial Contraction   | "Hepatic Vein Atrial | "Respiratory Cycle   |
| Reversal Velocity at | Contraction Reversal | Poin                 |
| Expiration           | Peak                 | t") <http://snomed.i |
|                      | V                    | nfo/id/272517003>`__ |
|                      | elocity") <http://lo | = `(58322009, SCT,   |
|                      | inc.org/29474-4/>`__ | "During              |
|                      |                      | Expirati             |
|                      |                      | on") <http://snomed. |
|                      |                      | info/id/58322009>`__ |
+----------------------+----------------------+----------------------+

.. _sect_N.3.16:

Congenital/Pediatric
~~~~~~~~~~~~~~~~~~~~

+----------------------+----------------------+----------------------+
| Name of ASE Concept  | Base Measurement     | Concept or           |
|                      | Concept Name         | Acquisition Context  |
|                      |                      | Modifiers            |
+======================+======================+======================+
| Thoracic Aorta       | `(29460-3, LN,       |                      |
| Coarctation Systolic | "Thoracic Aorta      |                      |
| Peak Velocity        | Coarctation Systolic |                      |
|                      | Peak                 |                      |
|                      | V                    |                      |
|                      | elocity") <http://lo |                      |
|                      | inc.org/29460-3/>`__ |                      |
+----------------------+----------------------+----------------------+
| Thoracic Aorta       | `(20256-4, LN, "Mean | `(363698007, SCT,    |
| Coarctation Systolic | G                    | "Finding             |
| Peak Instantaneous   | radient") <http://lo | Sit                  |
| Gradient             | inc.org/20256-4/>`__ | e") <http://snomed.i |
|                      |                      | nfo/id/363698007>`__ |
|                      |                      | = `(253678000, SCT,  |
|                      |                      | "Thoracic Aortic     |
|                      |                      | Coarctatio           |
|                      |                      | n") <http://snomed.i |
|                      |                      | nfo/id/253678000>`__ |
+----------------------+----------------------+----------------------+
| Thoracic Aorta       | `(17995-2, LN,       |                      |
| Coarctation Systolic | "Thoracic Aorta      |                      |
| Mean Gradient        | Coarctation Systolic |                      |
|                      | Peak Instantaneous   |                      |
|                      | G                    |                      |
|                      | radient") <http://lo |                      |
|                      | inc.org/17995-2/>`__ |                      |
+----------------------+----------------------+----------------------+
| Ventricular Septal   | `(399027007, SCT,    | `(363698007, SCT,    |
| Defect Diameter      | "Cardiovascular      | "Finding             |
|                      | Orifice              | Sit                  |
|                      | Diamete              | e") <http://snomed.i |
|                      | r") <http://snomed.i | nfo/id/363698007>`__ |
|                      | nfo/id/399027007>`__ | = `(30288003, SCT,   |
|                      |                      | "Ventricular Septal  |
|                      |                      | Defe                 |
|                      |                      | ct") <http://snomed. |
|                      |                      | info/id/30288003>`__ |
+----------------------+----------------------+----------------------+
| Ventricular Septal   | `(20247-3, LN, "Peak | `(363698007, SCT,    |
| Defect Systolic Peak | G                    | "Finding             |
| Instantaneous        | radient") <http://lo | Sit                  |
| Gradient             | inc.org/20247-3/>`__ | e") <http://snomed.i |
|                      |                      | nfo/id/363698007>`__ |
|                      |                      | = `(30288003, SCT,   |
|                      |                      | "Ventricular Septal  |
|                      |                      | Defe                 |
|                      |                      | ct") <http://snomed. |
|                      |                      | info/id/30288003>`__ |
+----------------------+----------------------+----------------------+
| Ventricular Septal   | `(20256-4, LN, "Mean | `(363698007, SCT,    |
| Defect Systolic Mean | G                    | "Finding             |
| Gradient             | radient") <http://lo | Sit                  |
|                      | inc.org/20256-4/>`__ | e") <http://snomed.i |
|                      |                      | nfo/id/363698007>`__ |
|                      |                      | = `(30288003, SCT,   |
|                      |                      | "Ventricular Septal  |
|                      |                      | Defe                 |
|                      |                      | ct") <http://snomed. |
|                      |                      | info/id/30288003>`__ |
+----------------------+----------------------+----------------------+
| Ventricular Septum   | `(11726-7, LN, "Peak | `(363698007, SCT,    |
| Defect Systolic Peak | V                    | "Finding             |
| Velocity             | elocity") <http://lo | Sit                  |
|                      | inc.org/11726-7/>`__ | e") <http://snomed.i |
|                      |                      | nfo/id/363698007>`__ |
|                      |                      | = `(30288003, SCT,   |
|                      |                      | "Ventricular Septal  |
|                      |                      | Defe                 |
|                      |                      | ct") <http://snomed. |
|                      |                      | info/id/30288003>`__ |
+----------------------+----------------------+----------------------+
| Atrial Septal Defect | `(399027007, SCT,    | `(363698007, SCT,    |
| Diameter             | "Cardiovascular      | "Finding             |
|                      | Orifice              | Sit                  |
|                      | Diamete              | e") <http://snomed.i |
|                      | r") <http://snomed.i | nfo/id/363698007>`__ |
|                      | nfo/id/399027007>`__ | = `(70142008, SCT,   |
|                      |                      | "Atrial Septal       |
|                      |                      | Defe                 |
|                      |                      | ct") <http://snomed. |
|                      |                      | info/id/70142008>`__ |
+----------------------+----------------------+----------------------+
| P                    | `(29462-9, LN,       |                      |
| ulmonary-to-Systemic | "P                   |                      |
| Shunt Flow Ratio     | ulmonary-to-Systemic |                      |
|                      | Shunt Flow           |                      |
|                      | Ratio") <http://lo   |                      |
|                      | inc.org/29462-9/>`__ |                      |
+----------------------+----------------------+----------------------+
| P                    | `(29462-9, LN,       | `(370129005, SCT,    |
| ulmonary-to-Systemic | "P                   | "Measurement         |
| Shunt Flow Ratio by  | ulmonary-to-Systemic | Metho                |
| Doppler Volume Flow  | Shunt Flow           | d") <http://snomed.i |
|                      | Ratio") <http://lo   | nfo/id/370129005>`__ |
|                      | inc.org/29462-9/>`__ | = (125219, DCM,      |
|                      |                      | "Doppler Volume      |
|                      |                      | Flow")               |
+----------------------+----------------------+----------------------+

.. _sect_N.4:

Encoding Examples
-----------------

.. _sect_N.4.1:

Example 1: Patient Characteristics
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+------+--------------------------+--------------------------+-----+
| Nest | Code Meaning of Concept  | Code Meaning or Example  | TID |
|      | Name                     | Value                    |     |
+======+==========================+==========================+=====+
|      | Adult Echocardiography   |                          |     |
|      | Procedure Report         |                          |     |
+------+--------------------------+--------------------------+-----+
| >    | ….                       |                          | …   |
+------+--------------------------+--------------------------+-----+
| >    | Patient Characteristics  |                          |     |
+------+--------------------------+--------------------------+-----+
| >>   | Subject Age              | 39 years                 |     |
+------+--------------------------+--------------------------+-----+
| >>   | Subject Sex              | M                        |     |
+------+--------------------------+--------------------------+-----+
| >>   | Patient Height           | 167 cm                   |     |
+------+--------------------------+--------------------------+-----+
| >>   | Patient Weight           | 72.6 kg                  |     |
+------+--------------------------+--------------------------+-----+
| >>   | Body Surface Area        | 1.82 m2                  |     |
+------+--------------------------+--------------------------+-----+
| >>>  | Body Surface Area        | Code: 122240             |     |
|      | Formula                  |                          |     |
+------+--------------------------+--------------------------+-----+

.. _sect_N.4.2:

Example 2: LV Dimensions and Fractional Shortening
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+------+--------------------------+--------------------------+-----+
| Nest | Code Meaning of Concept  | Code Meaning or Example  | TID |
|      | Name                     | Value                    |     |
+======+==========================+==========================+=====+
|      | Adult Echocardiography   |                          |     |
|      | Procedure Report         |                          |     |
+------+--------------------------+--------------------------+-----+
| >    | ….                       |                          | …   |
+------+--------------------------+--------------------------+-----+
| >    | Findings                 |                          |     |
+------+--------------------------+--------------------------+-----+
| >>   | Finding Site             | Left Ventricle           |     |
+------+--------------------------+--------------------------+-----+
| >>   | Measurement Group        |                          |     |
+------+--------------------------+--------------------------+-----+
| >>   | Acquisition Protocol     | 2D Dimensions            |     |
+------+--------------------------+--------------------------+-----+
| >>>  | Heart Rate               | 45 bpm                   |     |
+------+--------------------------+--------------------------+-----+
| >>>  | Left Ventricle Internal  | 5.09 cm                  |     |
|      | End Diastolic Dimension  |                          |     |
+------+--------------------------+--------------------------+-----+
| >>>> | Image Mode               | 2d                       |     |
+------+--------------------------+--------------------------+-----+
| >>>  | Left Ventricle Internal  | 5.34 cm                  |     |
|      | End Diastolic Dimension  |                          |     |
+------+--------------------------+--------------------------+-----+
| >>>> | Image Mode               | 2d                       |     |
+------+--------------------------+--------------------------+-----+
| >>>  | Left Ventricle Internal  | 5.22 cm                  |     |
|      | End Diastolic Dimension  |                          |     |
+------+--------------------------+--------------------------+-----+
| >>>> | Image Mode               | 2d                       |     |
+------+--------------------------+--------------------------+-----+
| >>>> | Derivation               | Mean                     |     |
+------+--------------------------+--------------------------+-----+
| >>>  | Left Ventricle Internal  | 5.09 cm                  |     |
|      | Systolic Dimension       |                          |     |
+------+--------------------------+--------------------------+-----+
| >>>> | Image Mode               | 2d                       |     |
+------+--------------------------+--------------------------+-----+
| >>>  | Left Ventricle Internal  | 5.34 cm                  |     |
|      | Systolic Dimension       |                          |     |
+------+--------------------------+--------------------------+-----+
| >>>> | Image Mode               | 2d                       |     |
+------+--------------------------+--------------------------+-----+
| >>>  | Left Ventricle Internal  | 5.22 cm                  |     |
|      | Systolic Dimension       |                          |     |
+------+--------------------------+--------------------------+-----+
| >>>> | Image Mode               | 2d                       |     |
+------+--------------------------+--------------------------+-----+
| >>>> | Derivation               | Mean                     |     |
+------+--------------------------+--------------------------+-----+
| >>>  | Interventricular Septum  | 1.20 cm                  |     |
|      | Diastolic Thickness      |                          |     |
+------+--------------------------+--------------------------+-----+
| >>>  | Interventricular Septum  | 1.20 cm                  |     |
|      | Diastolic Thickness      |                          |     |
+------+--------------------------+--------------------------+-----+
| >>>> | Derivation               | Mean                     |     |
+------+--------------------------+--------------------------+-----+
| >>>  | Left Ventricle Internal  | 5.09 cm                  |     |
|      | Systolic Dimension       |                          |     |
+------+--------------------------+--------------------------+-----+
| >>>  | Left Ventricle Internal  | 5.30 cm                  |     |
|      | Systolic Dimension       |                          |     |
+------+--------------------------+--------------------------+-----+
| >>>> | Derivation               | Mean                     |     |
+------+--------------------------+--------------------------+-----+
| >>>  | Left Ventricular         | 54.8%                    |     |
|      | Fractional Shortening    |                          |     |
+------+--------------------------+--------------------------+-----+
| >>>  | …                        |                          | …   |
+------+--------------------------+--------------------------+-----+

.. _sect_N.4.3:

Example 3: Left Atrium / Aortic Root Ratio
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+------+--------------------------+--------------------------+-----+
| Nest | Code Meaning of Concept  | Code Meaning or Example  | TID |
|      | Name                     | Value                    |     |
+======+==========================+==========================+=====+
|      | Adult Echocardiography   |                          |     |
|      | Procedure Report         |                          |     |
+------+--------------------------+--------------------------+-----+
| >    | ….                       |                          | …   |
+------+--------------------------+--------------------------+-----+
| >    | Findings                 |                          |     |
+------+--------------------------+--------------------------+-----+
| >>   | Finding Site             | Left Atrium              |     |
+------+--------------------------+--------------------------+-----+
| >>   | Measurement Group        |                          |     |
+------+--------------------------+--------------------------+-----+
| >>>  | Acquisition Protocol     | 2D Dimensions            |     |
+------+--------------------------+--------------------------+-----+
| >>>  | Left Atrium              | 3.45 cm                  |     |
|      | Antero-posterior         |                          |     |
|      | Systolic Dimension       |                          |     |
+------+--------------------------+--------------------------+-----+
| >>>  | Left Atrium              | 3.45 cm                  |     |
|      | Antero-posterior         |                          |     |
|      | Systolic Dimension       |                          |     |
+------+--------------------------+--------------------------+-----+
| >>>> | Derivation               | Mean                     |     |
+------+--------------------------+--------------------------+-----+
| >>>  | Left Atrium to Aortic    | 1.35                     |     |
|      | Root Ratio               |                          |     |
+------+--------------------------+--------------------------+-----+
| >    | Findings                 |                          |     |
+------+--------------------------+--------------------------+-----+
| >>   | Finding Site             | Aorta                    |     |
+------+--------------------------+--------------------------+-----+
| >>   | Measurement Group        |                          |     |
+------+--------------------------+--------------------------+-----+
| >>   | Acquisition Protocol     | 2D Dimensions            |     |
+------+--------------------------+--------------------------+-----+
| >>>  | Aortic Root Diameter     | 2.55 cm                  |     |
+------+--------------------------+--------------------------+-----+
| >>>  | …                        |                          | …   |
+------+--------------------------+--------------------------+-----+

.. _sect_N.4.4:

Example 4: Pressures
~~~~~~~~~~~~~~~~~~~~

+------+--------------------------+--------------------------+-----+
| Nest | Code Meaning of Concept  | Code Meaning or Example  | TID |
|      | Name                     | Value                    |     |
+======+==========================+==========================+=====+
|      | Adult Echocardiography   |                          |     |
|      | Procedure Report         |                          |     |
+------+--------------------------+--------------------------+-----+
| >    | ….                       |                          | …   |
+------+--------------------------+--------------------------+-----+
| >    | Findings                 |                          |     |
+------+--------------------------+--------------------------+-----+
| >>   | Finding Site             | Right Atrium             |     |
+------+--------------------------+--------------------------+-----+
| >>   | Measurement Group        |                          |     |
+------+--------------------------+--------------------------+-----+
| >>>  | Acquisition Protocol     | Pressure Predictions     |     |
+------+--------------------------+--------------------------+-----+
| >>>  | Right Atrium Systolic    | 10 mmHg                  |     |
|      | Pressure                 |                          |     |
+------+--------------------------+--------------------------+-----+
| >>>> | Derivation               | User estimate            |     |
+------+--------------------------+--------------------------+-----+
| >>   | Finding Site             | Right Ventricle          |     |
+------+--------------------------+--------------------------+-----+
| >>   | Measurement Group        |                          |     |
+------+--------------------------+--------------------------+-----+
| >>>  | Acquisition Protocol     | Pressure Predictions     |     |
+------+--------------------------+--------------------------+-----+
| >>>  | Right Ventricular Peak   | 49.3 mmHg                |     |
|      | Systolic Pressure        |                          |     |
+------+--------------------------+--------------------------+-----+

.. _sect_N.4.5:

Example 5: Cardiac Output
~~~~~~~~~~~~~~~~~~~~~~~~~

+------+--------------------------+--------------------------+-----+
| Nest | Code Meaning of Concept  | Code Meaning or Example  | TID |
|      | Name                     | Value                    |     |
+======+==========================+==========================+=====+
|      | Adult Echocardiography   |                          |     |
|      | Procedure Report         |                          |     |
+------+--------------------------+--------------------------+-----+
| >    | ….                       |                          | …   |
+------+--------------------------+--------------------------+-----+
| >    | Findings                 |                          |     |
+------+--------------------------+--------------------------+-----+
| >>   | Finding Site             | Left Ventricle           |     |
+------+--------------------------+--------------------------+-----+
| >>   | Measurement Group        |                          |     |
+------+--------------------------+--------------------------+-----+
| >>   | Image Mode               | 2D                       |     |
+------+--------------------------+--------------------------+-----+
| >>>  | Heart Rate               | 89 bpm                   |     |
+------+--------------------------+--------------------------+-----+
| >>>  | Left Ventricular End     | 38.914 ml                |     |
|      | Diastolic Volume         |                          |     |
+------+--------------------------+--------------------------+-----+
| >>>> | Measurement Method       | Teichholz                |     |
+------+--------------------------+--------------------------+-----+
| >>>  | Left Ventricular End     | 12.304 ml                |     |
|      | Systolic Volume          |                          |     |
+------+--------------------------+--------------------------+-----+
| >>>> | Measurement Method       | Teichholz                |     |
+------+--------------------------+--------------------------+-----+
| …    | …                        | …                        | …   |
+------+--------------------------+--------------------------+-----+
| >>>  | Stroke Volume            | 26.6 ml                  |     |
+------+--------------------------+--------------------------+-----+
| >>>> | Anatomic Site            | Left Ventricle           |     |
+------+--------------------------+--------------------------+-----+
| >>>  | Stroke Index             | 13.49 ml/m2              |     |
+------+--------------------------+--------------------------+-----+
| >>>> | Anatomic Site            | Left Ventricle           |     |
+------+--------------------------+--------------------------+-----+
| >>>  | Cardiac Output           | 2.37 l/min               |     |
+------+--------------------------+--------------------------+-----+
| >>>> | Anatomic Site            | Left Ventricle           |     |
+------+--------------------------+--------------------------+-----+
| >>>  | Cardiac Index            | 1.20 l/min/m2            |     |
+------+--------------------------+--------------------------+-----+
| >>>> | Anatomic Site            | Left Ventricle           |     |
+------+--------------------------+--------------------------+-----+
| >>>> | Index                    | BSA                      |     |
+------+--------------------------+--------------------------+-----+
| >>>  | Left Ventricular         | 68.4 %                   |     |
|      | Ejection Fraction        |                          |     |
+------+--------------------------+--------------------------+-----+
| >>>  | …                        |                          | …   |
+------+--------------------------+--------------------------+-----+

.. _sect_N.4.6:

Example 6: Wall Scoring
~~~~~~~~~~~~~~~~~~~~~~~

+------+--------------------------+--------------------------+-----+
| Nest | Code Meaning of Concept  | Code Meaning or Example  | TID |
|      | Name                     | Value                    |     |
+======+==========================+==========================+=====+
|      | Adult Echocardiography   |                          |     |
|      | Procedure Report         |                          |     |
+------+--------------------------+--------------------------+-----+
| >    | ….                       |                          | …   |
+------+--------------------------+--------------------------+-----+
| >    | Findings                 |                          |     |
+------+--------------------------+--------------------------+-----+
| >>   | Procedure Reported       | Echocardiography for     |     |
|      |                          | Determining Ventricular  |     |
|      |                          | Contraction              |     |
+------+--------------------------+--------------------------+-----+
| >>   | Stage                    | Pre-stress image         |     |
|      |                          | acquisition              |     |
+------+--------------------------+--------------------------+-----+
| >>   | LV Wall Motion Score     | 1.0                      |     |
|      | Index                    |                          |     |
+------+--------------------------+--------------------------+-----+
| >>>  | Assessment Scale         | 5 Point Segment Finding  |     |
|      |                          | Scale                    |     |
+------+--------------------------+--------------------------+-----+
| >>   | Findings                 |                          |     |
+------+--------------------------+--------------------------+-----+
| >>>  | Wall Segment             | Basal anterior           |     |
+------+--------------------------+--------------------------+-----+
| >>>> | Wall motion finding      | Normal                   |     |
+------+--------------------------+--------------------------+-----+
| >>>  | Wall Segment             | Basal anteroseptal       |     |
+------+--------------------------+--------------------------+-----+
| >>>> | Wall motion finding      | Normal                   |     |
+------+--------------------------+--------------------------+-----+
| >>>  | Wall Segment             | Basal inferoseptal       |     |
+------+--------------------------+--------------------------+-----+
| >>>> | Wall motion finding      | Akinetic                 |     |
+------+--------------------------+--------------------------+-----+
| …    | … remaining segments …   |                          |     |
+------+--------------------------+--------------------------+-----+
| >    | Wall Motion Analysis     |                          |     |
+------+--------------------------+--------------------------+-----+
| >>   | Stage                    | Peak-stress image        |     |
|      |                          | acquisition              |     |
+------+--------------------------+--------------------------+-----+
| >>   | LV Wall Motion Score     | 1.23                     |     |
|      | Index                    |                          |     |
+------+--------------------------+--------------------------+-----+
| >>>  | Assessment Scale         | 5 Point Segment Finding  |     |
|      |                          | Scale                    |     |
+------+--------------------------+--------------------------+-----+
| >>   | Findings                 |                          |     |
+------+--------------------------+--------------------------+-----+
| >>>  | Wall Segment             | Basal anterior           |     |
+------+--------------------------+--------------------------+-----+
| >>>> | Score                    | Hypokinesis              |     |
+------+--------------------------+--------------------------+-----+
| >>>  | Wall Segment             | Basal anteroseptal       |     |
+------+--------------------------+--------------------------+-----+
| >>>> | Score                    | Akinetic                 |     |
+------+--------------------------+--------------------------+-----+
| >>>> | Morphology               | Scar / Thinning          |     |
+------+--------------------------+--------------------------+-----+
| >>>  | Wall Segment             | Basal inferoseptal       |     |
+------+--------------------------+--------------------------+-----+
| >>>> | Score                    | Normal                   |     |
+------+--------------------------+--------------------------+-----+
| …    | … remaining segments …   |                          |     |
+------+--------------------------+--------------------------+-----+

.. _sect_N.5:

IVUS Report
-----------

The IVUS Report contains one or more vessel containers, each
corresponding to the vessel (arterial location) being imaged. Each
vessel is associated with one or more IVUS image pullbacks (Ultrasound
Multi-frame Images), acquired during a phase of a catheterization
procedure. Each vessel may contain one or more sub-containers, each
associated with a single lesion. Each lesion container includes a set of
IVUS measurements and qualitative assessments. The resulting
hierarchical structure is depicted in `figure_title <#figure_N.5-1>`__.

