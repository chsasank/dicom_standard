.. _chapter_RRR:

Measurement Report SR Document for Planar and Volumetric ROI (Informative)
==========================================================================

This Annex contains examples of the use of ROI templates within
Measurement Report SR Documents.

.. _sect_RRR.1:

Measurement Report SR Document Volumetric ROI on CT Example
-----------------------------------------------------------

This CT example describes the minimum content necessary to encode a
single measurement (volume) made from a single volumetric ROI encoded as
a single segment that spans two source CT images.

.. note::

   1. References to Segmentation Image or Surface Segmentation objects
      are encoded as IMAGE references, with a single value specified in
      Referenced Segment Number.

   2. The method of volume calculation is not described in this example.

.. table:: Volumetric ROI on CT Example

   +---------+-------------------------+-------------------------+-----+
   | Node    | Code Meaning of Concept | Code Meaning or Example | TID |
   |         | Name                    | Value                   |     |
   +=========+=========================+=========================+=====+
   | 1       | Oncology Measurement    |                         |     |
   |         | Report                  |                         |     |
   +---------+-------------------------+-------------------------+-----+
   | 1.1     | Language of Content     | English                 |     |
   |         | Item and Descendants    |                         |     |
   +---------+-------------------------+-------------------------+-----+
   | **1.2** | Observation Context     |                         |     |
   +---------+-------------------------+-------------------------+-----+
   | 1.2.1   | Person Observer Name    | Doe^Jane                |     |
   +---------+-------------------------+-------------------------+-----+
   | 1.3     | Procedure Reported      | Chest+Abd CT W+WO contr |     |
   |         |                         | IV                      |     |
   +---------+-------------------------+-------------------------+-----+
   | 1.4     | Measurements            |                         |     |
   +---------+-------------------------+-------------------------+-----+
   | 1.4.1   | Measurement Group       |                         |     |
   +---------+-------------------------+-------------------------+-----+
   | 1.4.1.1 | Tracking Identifier     | Object1                 |     |
   +---------+-------------------------+-------------------------+-----+
   | 1.4.1.2 | Tracking Unique         | 1.2.276.0.7230010...    |     |
   |         | Identifier              |                         |     |
   +---------+-------------------------+-------------------------+-----+
   | 1.4.1.3 | Referenced Segment      | IMAGE - Segmentation,   |     |
   |         |                         | Segment #1              |     |
   +---------+-------------------------+-------------------------+-----+
   | 1.4.1.4 | Source image for        | IMAGE - CT image #1     |     |
   |         | segmentation            |                         |     |
   +---------+-------------------------+-------------------------+-----+
   | 1.4.1.5 | Source image for        | IMAGE - CT image #2     |     |
   |         | segmentation            |                         |     |
   +---------+-------------------------+-------------------------+-----+
   | 1.4.1.6 | Volume                  | 3267.46 mm3             |     |
   +---------+-------------------------+-------------------------+-----+

.. _sect_RRR.2:

Measurement Report SR Document Volumetric ROI on CT Example
-----------------------------------------------------------

This CT example describes a set of measurements (volume. long axis and
mean attenuation coefficient) made from a single volumetric ROI encoded
as a single segment that spans two source CT images, and includes a
description of the measurement methods and the finding site, as well as
an image library to describe characteristics of the images used, and
categorical observations at the measurement group and entire subject
level.

.. note::

   1. For a different modality than CT, the choice of measurement for
      the mean intensity would not be (122713, DCM, "Attenuation
      Coefficient").

   2. For MR one might use (110852, DCM, "MR signal intensity"), or
      (110804, DCM, "T1 Weighted MR Signal Intensity"), etc. See also
      for various appropriate signal intensity types for MR and other
      modalities.

   3. For PET one might use (110821, DCM, "Nuclear Medicine Tomographic
      Activity"), in which case the specific type of signal would be
      apparent from the units, e.g., ({SUVbw}g/ml, UCUM, "Standardized
      Uptake Value body weight") or for activity-concentration, (Bq/ml,
      UCUM, "Becquerels/milliliter"). See also .

   4. Care should be taken when selecting modifiers such as `(370129005,
      SCT, "Measurement Method") <http://snomed.info/id/370129005>`__
      versus (121401, DCM, "Derivation").

   5. The finding site and laterality within the measurement template ()
      are factored out and shared by both measurements.

   6. The pattern used for the image library uses , though commonality
      may be refactored.

   7. The length of the long axis of the volumetric ROI is encoded, but
      the end points of the line segment used to make that measurement
      are not recorded, since only the volumetric spatial description of
      is used. For an alternative encoding, see `Measurement Report SR
      Document Volumetric ROI with RECIST Linear Distance Specified by
      Coordinates on CT Example <#sect_RRR.5>`__.

.. table:: Volumetric ROI on CT Example

   +-----------+------------------------+------------------------+-----+
   | Node      | Code Meaning of        | Code Meaning or        | TID |
   |           | Concept Name           | Example Value          |     |
   +===========+========================+========================+=====+
   | 1         | Oncology Measurement   |                        |     |
   |           | Report                 |                        |     |
   +-----------+------------------------+------------------------+-----+
   | 1.1       | Language of Content    | English                |     |
   |           | Item and Descendants   |                        |     |
   +-----------+------------------------+------------------------+-----+
   | **1.2**   | Observation Context    |                        |     |
   +-----------+------------------------+------------------------+-----+
   | 1.2.1     | Person Observer Name   | Doe^Jane               |     |
   +-----------+------------------------+------------------------+-----+
   | 1.3       | Procedure Reported     | Chest+Abd CT W+WO      |     |
   |           |                        | contr IV               |     |
   +-----------+------------------------+------------------------+-----+
   | 1.4       | Image Library          |                        |     |
   +-----------+------------------------+------------------------+-----+
   | 1.4.1     |                        | IMAGE - CT image #1    |     |
   +-----------+------------------------+------------------------+-----+
   | 1.4.1.1   | Study Date             | 20030417               |     |
   +-----------+------------------------+------------------------+-----+
   | 1.4.1.2   | Study Time             | 104607                 |     |
   +-----------+------------------------+------------------------+-----+
   | 1.4.1.3   | Horizontal Pixel       | 0.810547 mm            |     |
   |           | Spacing                |                        |     |
   +-----------+------------------------+------------------------+-----+
   | 1.4.1.j   | ...                    | ...                    |     |
   +-----------+------------------------+------------------------+-----+
   | 1.4.1.n   | Pixel Data Columns     | 512 pixels             |     |
   +-----------+------------------------+------------------------+-----+
   | 1.4.2     |                        | IMAGE - CT image #2    |     |
   +-----------+------------------------+------------------------+-----+
   | 1.4.2.j   | ...                    | ...                    |     |
   +-----------+------------------------+------------------------+-----+
   | 1.5       | Measurements           |                        |     |
   +-----------+------------------------+------------------------+-----+
   | 1.5.1     | Measurement Group      |                        |     |
   +-----------+------------------------+------------------------+-----+
   | 1.5.1.1   | Tracking Identifier    | Object1                |     |
   +-----------+------------------------+------------------------+-----+
   | 1.5.1.2   | Tracking Unique        | 1.2.276.0.7230010...   |     |
   |           | Identifier             |                        |     |
   +-----------+------------------------+------------------------+-----+
   | 1.5.1.3   | Referenced Segment     | IMAGE - Segmentation,  |     |
   |           |                        | Segment #1             |     |
   +-----------+------------------------+------------------------+-----+
   | 1.5.1.4   | Source image for       | IMAGE - CT image #1    |     |
   |           | segmentation           |                        |     |
   +-----------+------------------------+------------------------+-----+
   | 1.5.1.5   | Source image for       | IMAGE - CT image #2    |     |
   |           | segmentation           |                        |     |
   +-----------+------------------------+------------------------+-----+
   | 1.5.1.6   | Finding Site           | Adrenal Gland          |     |
   +-----------+------------------------+------------------------+-----+
   | 1.5.1.6.1 | Laterality             | Right                  |     |
   +-----------+------------------------+------------------------+-----+
   | 1.5.1.7   | Volume                 | 3267.46 mm3            |     |
   +-----------+------------------------+------------------------+-----+
   | 1.5.1.7.1 | Measurement Method     | Sum of segmented voxel |     |
   |           |                        | volumes                |     |
   +-----------+------------------------+------------------------+-----+
   | 1.5.1.8   | Long Axis              | 9.21 mm                |     |
   +-----------+------------------------+------------------------+-----+
   | 1.5.1.8.1 | Measurement Method     | RECIST 1.1             |     |
   +-----------+------------------------+------------------------+-----+
   | 1.5.1.9   | Attenuation            | 70.978 Hounsfield unit |     |
   |           | Coefficient            |                        |     |
   +-----------+------------------------+------------------------+-----+
   | 1.5.1.9.1 | Derivation             | Mean                   |     |
   +-----------+------------------------+------------------------+-----+
   | 1.5.1.10  | Necrosis               | Present                |     |
   +-----------+------------------------+------------------------+-----+
   | 1.5.1.11  | Hemorrhage             | Absent                 |     |
   +-----------+------------------------+------------------------+-----+
   | 1.6       | Qualitative            |                        |     |
   |           | Evaluations            |                        |     |
   +-----------+------------------------+------------------------+-----+
   | 1.6.1     | Renal Vein Involvement | Absent                 |     |
   +-----------+------------------------+------------------------+-----+

.. _sect_RRR.3:

Measurement Report SR Document Planar ROI on DCE-MR Tracer Kinetic Model Example
--------------------------------------------------------------------------------

This DCE-MR example illustrates encoding measurements of mean and
standard deviation Ktrans values in a planar ROI.

.. note::

   1. The measurement method and finding site and laterality within the
      measurement template () are factored out and shared by both
      measurements.

.. table:: Planar ROI on DCE-MR Example

   +-----------+------------------------+------------------------+-----+
   | Node      | Code Meaning of        | Code Meaning or        | TID |
   |           | Concept Name           | Example Value          |     |
   |           |                        |                        | CID |
   +===========+========================+========================+=====+
   | 1         | Oncology Measurement   |                        |     |
   |           | Report                 |                        |     |
   +-----------+------------------------+------------------------+-----+
   | 1.1       | Language of Content    | English                |     |
   |           | Item and Descendants   |                        |     |
   +-----------+------------------------+------------------------+-----+
   | **1.2**   | Observation Context    |                        |     |
   +-----------+------------------------+------------------------+-----+
   | 1.2.1     | Person Observer Name   | Doe^Jane               |     |
   +-----------+------------------------+------------------------+-----+
   | 1.3       | Procedure Reported     | Breast - bilateral MRI |     |
   |           |                        | dynamic W contrast IV  |     |
   +-----------+------------------------+------------------------+-----+
   | 1.4       | Measurements           |                        |     |
   +-----------+------------------------+------------------------+-----+
   | 1.4.1     | Measurement Group      |                        |     |
   +-----------+------------------------+------------------------+-----+
   | 1.4.1.1   | Tracking Identifier    | Object1                |     |
   +-----------+------------------------+------------------------+-----+
   | 1.4.1.2   | Tracking Unique        | 1.2.276.0.7230010...   |     |
   |           | Identifier             |                        |     |
   +-----------+------------------------+------------------------+-----+
   | 1.4.1.3   | Referenced Segment     | IMAGE - Segmentation,  |     |
   |           |                        | Segment #1             |     |
   +-----------+------------------------+------------------------+-----+
   | 1.4.1.4   | Source image for       | IMAGE - MR image #1    |     |
   |           | segmentation           |                        |     |
   +-----------+------------------------+------------------------+-----+
   | 1.4.1.5   | Measurement Method     | Extended Tofts Model   |     |
   +-----------+------------------------+------------------------+-----+
   | 1.4.1.6   | Finding Site           | Breast                 |     |
   +-----------+------------------------+------------------------+-----+
   | 1.4.1.6.1 | Laterality             | Right                  |     |
   +-----------+------------------------+------------------------+-----+
   | 1.4.1.7   | Ktrans                 | 0.0185 /min            |     |
   +-----------+------------------------+------------------------+-----+
   | 1.4.1.7.1 | Derivation             | Mean                   |     |
   +-----------+------------------------+------------------------+-----+
   | 1.4.1.8   | Ktrans                 | 0.0102 /min            |     |
   +-----------+------------------------+------------------------+-----+
   | 1.4.1.8.1 | Derivation             | Standard Deviation     |     |
   +-----------+------------------------+------------------------+-----+

.. _sect_RRR.4:

Measurement Report SR Document Volumetric and SUV ROI on FDG PET Example
------------------------------------------------------------------------

This FDG PET example illustrates encoding measurements of various SUVbw
related measurements.

.. note::

   1. The real world value map reference (for intensity, not size
      measurements) and finding site within the measurement template ()
      are factored out and shared by measurements.

   2. The time point is described in this case only with a simple label.

.. table:: SUV ROI on FDG PET Example

   +------------+-----------------------+-----------------------+-----+
   | Node       | Code Meaning of       | Code Meaning or       | TID |
   |            | Concept Name          | Example Value         |     |
   |            |                       |                       | CID |
   +============+=======================+=======================+=====+
   | 1          | Oncology Measurement  |                       |     |
   |            | Report                |                       |     |
   +------------+-----------------------+-----------------------+-----+
   | 1.1        | Language of Content   | English               |     |
   |            | Item and Descendants  |                       |     |
   +------------+-----------------------+-----------------------+-----+
   | 1.2        | Observation Context   |                       |     |
   +------------+-----------------------+-----------------------+-----+
   | 1.2.1      | Person Observer Name  | Doe^Jane              |     |
   +------------+-----------------------+-----------------------+-----+
   | 1.3        | Procedure Reported    | PET/CT FDG imaging of |     |
   |            |                       | whole body            |     |
   +------------+-----------------------+-----------------------+-----+
   | 1.4        | Measurements          |                       |     |
   +------------+-----------------------+-----------------------+-----+
   | 1.4.1      | Measurement Group     |                       |     |
   +------------+-----------------------+-----------------------+-----+
   | 1.4.1.1    | Tracking Identifier   | Liver                 |     |
   +------------+-----------------------+-----------------------+-----+
   | 1.4.1.2    | Tracking Unique       | 1.2.276.0.7230010...  |     |
   |            | Identifier            |                       |     |
   +------------+-----------------------+-----------------------+-----+
   | 1.4.1.3    | Time Point            | TP0                   |     |
   +------------+-----------------------+-----------------------+-----+
   | 1.4.1.4    | Referenced Segment    | IMAGE - Segmentation, |     |
   |            |                       | Segment #1            |     |
   +------------+-----------------------+-----------------------+-----+
   | 1.4.1.5    | Source image for      | IMAGE - PET image #1  |     |
   |            | segmentation          |                       |     |
   +------------+-----------------------+-----------------------+-----+
   | 1.4.1.6    | Source image for      | IMAGE - CT image #1   |     |
   |            | segmentation          |                       |     |
   +------------+-----------------------+-----------------------+-----+
   | 1.4.1.7    | Finding Site          | Liver                 |     |
   +------------+-----------------------+-----------------------+-----+
   | 1.4.1.8    | Real World Value Map  | RWVM - UID            |     |
   |            | used for measurement  |                       |     |
   +------------+-----------------------+-----------------------+-----+
   | 1.4.1.9    | SUVbw                 | 3.90557 {SUVbw}g/ml   |     |
   +------------+-----------------------+-----------------------+-----+
   | 1.4.1.9.1  | Derivation            | Max                   |     |
   +------------+-----------------------+-----------------------+-----+
   | 1.4.1.10   | SUVbw                 | 3.25653 {SUVbw}g/ml   |     |
   +------------+-----------------------+-----------------------+-----+
   | 1.4.1.10.1 | Derivation            | Peak Value Within ROI |     |
   +------------+-----------------------+-----------------------+-----+
   | 1.4.1.11   | SUVbw                 | 2.34467 {SUVbw}g/ml   |     |
   +------------+-----------------------+-----------------------+-----+
   | 1.4.1.11.1 | Derivation            | Root Mean Square      |     |
   +------------+-----------------------+-----------------------+-----+
   | 1.4.1.12   | Standardized Added    | 20400.3 g             |     |
   |            | Metabolic Activity    |                       |     |
   |            | (SAM)                 |                       |     |
   +------------+-----------------------+-----------------------+-----+
   | 1.4.1.12.1 | Measurement Method    | SUV body weight       |     |
   |            |                       | calculation method    |     |
   +------------+-----------------------+-----------------------+-----+
   | 1.4.1.13   | Volume                | 395512 mm3            |     |
   +------------+-----------------------+-----------------------+-----+
   | 1.4.1.13.1 | Measurement Method    | Sum of segmented      |     |
   |            |                       | voxel volumes         |     |
   +------------+-----------------------+-----------------------+-----+

.. _sect_RRR.5:

Measurement Report SR Document Volumetric ROI with RECIST Linear Distance Specified by Coordinates on CT Example
----------------------------------------------------------------------------------------------------------------

This CT example describes a set of measurements (volume, long axis
(RECIST), short axis (WHO bi-dimensional) and mean attenuation
coefficient) made from a single volumetric ROI encoded as a single
segment, including specification of the end points of the line segment
used to make the linear distance measurements.

.. note::

   1. The lengths of the long axis and the short axis of the lesion are
      not encoded as characteristics of the volumetric ROI, but rather
      the long axis and the short axis are encoded explicitly as the end
      points of line segments used to make those measurements. The
      commonality of the Tracking Unique Identifier establishes that
      they are measurements of the same ROI. If multiple measurements
      were to be made of the same ROI over time or by different
      observers, other content items such as those related to Timepoint,
      Activity Session and Observer may be used. For an alternative
      encoding, see `Measurement Report SR Document Volumetric ROI on CT
      Example <#sect_RRR.2>`__.

   2. The pattern of using multiple sibling linear distance measurements
      within is similar to and not incompatible with the pattern used
      for length, width and height in the OB/GYN Ultrasound template .

   3. The Finding Site information is duplicated in the second
      measurement template invocation in this example, though it is not
      required to be.

.. table:: Volumetric ROI on CT Example

   +-------------+-----------------------+-----------------------+-----+
   | Node        | Code Meaning of       | Code Meaning or       | TID |
   |             | Concept Name          | Example Value         |     |
   +=============+=======================+=======================+=====+
   | 1           | Oncology Measurement  |                       |     |
   |             | Report                |                       |     |
   +-------------+-----------------------+-----------------------+-----+
   | ...         | ...                   | ...                   | ... |
   +-------------+-----------------------+-----------------------+-----+
   | 1.5         | Measurements          |                       |     |
   +-------------+-----------------------+-----------------------+-----+
   | 1.5.1       | Measurement Group     |                       |     |
   +-------------+-----------------------+-----------------------+-----+
   | 1.5.1.1     | Tracking Identifier   | Object1 (same for     |     |
   |             |                       | both Measurement      |     |
   |             |                       | Groups)               |     |
   +-------------+-----------------------+-----------------------+-----+
   | 1.5.1.2     | Tracking Unique       | 1.2.276.0.7230010...  |     |
   |             | Identifier            | (same for both        |     |
   |             |                       | Measurement Groups)   |     |
   +-------------+-----------------------+-----------------------+-----+
   | 1.5.1.3     | Referenced Segment    | IMAGE - Segmentation, |     |
   |             |                       | Segment #1            |     |
   +-------------+-----------------------+-----------------------+-----+
   | 1.5.1.4     | Source image for      | IMAGE - CT image #1   |     |
   |             | segmentation          |                       |     |
   +-------------+-----------------------+-----------------------+-----+
   | 1.5.1.5     | Source image for      | IMAGE - CT image #2   |     |
   |             | segmentation          |                       |     |
   +-------------+-----------------------+-----------------------+-----+
   | 1.5.1.6     | Finding Site          | Adrenal Gland (same   |     |
   |             |                       | for both Measurement  |     |
   |             |                       | Groups)               |     |
   +-------------+-----------------------+-----------------------+-----+
   | 1.5.1.6.1   | Laterality            | Right (same for both  |     |
   |             |                       | Measurement Groups)   |     |
   +-------------+-----------------------+-----------------------+-----+
   | 1.5.1.7     | Volume                | 3267.46 mm3           |     |
   +-------------+-----------------------+-----------------------+-----+
   | 1.5.1.7.1   | Measurement Method    | Sum of segmented      |     |
   |             |                       | voxel volumes         |     |
   +-------------+-----------------------+-----------------------+-----+
   | 1.5.1.8     | Attenuation           | 70.978 Hounsfield     |     |
   |             | Coefficient           | unit                  |     |
   +-------------+-----------------------+-----------------------+-----+
   | 1.5.1.8.1   | Derivation            | Mean                  |     |
   +-------------+-----------------------+-----------------------+-----+
   | 1.6.1       | Measurement Group     |                       |     |
   +-------------+-----------------------+-----------------------+-----+
   | 1.6.1.1     | Tracking Identifier   | Object1 (same for     |     |
   |             |                       | both Measurement      |     |
   |             |                       | Groups)               |     |
   +-------------+-----------------------+-----------------------+-----+
   | 1.6.1.2     | Tracking Unique       | 1.2.276.0.7230010...  |     |
   |             | Identifier            | (same for both        |     |
   |             |                       | Measurement Groups)   |     |
   +-------------+-----------------------+-----------------------+-----+
   | 1.6.1.3     | Finding Site          | Adrenal Gland (same   |     |
   |             |                       | for both Measurement  |     |
   |             |                       | Groups)               |     |
   +-------------+-----------------------+-----------------------+-----+
   | 1.6.1.3.1   | Laterality            | Right (same for both  |     |
   |             |                       | Measurement Groups)   |     |
   +-------------+-----------------------+-----------------------+-----+
   | 1.6.1.4     | Long Axis             | 9.21 mm               |     |
   +-------------+-----------------------+-----------------------+-----+
   | 1.6.1.4.1   | Measurement Method    | RECIST 1.1            |     |
   +-------------+-----------------------+-----------------------+-----+
   | 1.6.1.4.2   | Source of Measurement | SCOORD GraphicType    |     |
   |             |                       | POLYLINE with two     |     |
   |             |                       | coordinates, the      |     |
   |             |                       | beginning and end of  |     |
   |             |                       | a line segment        |     |
   +-------------+-----------------------+-----------------------+-----+
   | 1.6.1.4.2.1 | (none)                | IMAGE - CT image #1   |     |
   +-------------+-----------------------+-----------------------+-----+
   | 1.6.1.5     | Short Axis            | 6.8 mm                |     |
   +-------------+-----------------------+-----------------------+-----+
   | 1.6.1.5.1   | Measurement Method    | WHO                   |     |
   +-------------+-----------------------+-----------------------+-----+
   | 1.6.1.5.2   | Source of Measurement | SCOORD GraphicType    |     |
   |             |                       | POLYLINE with two     |     |
   |             |                       | coordinates, the      |     |
   |             |                       | beginning and end of  |     |
   |             |                       | a line segment        |     |
   +-------------+-----------------------+-----------------------+-----+
   | 1.6.1.5.2.1 | (none)                | IMAGE - CT image #1   |     |
   +-------------+-----------------------+-----------------------+-----+

