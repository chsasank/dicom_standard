.. _chapter_M:

Vascular Ultrasound Reports (Informative)
=========================================

.. _sect_M.1:

Vascular Report Structure
-------------------------

The vascular procedure report partitions numeric measurements into
section headings by anatomic region and by laterality. A laterality
concept modifier of the section heading concept name specifies whether
laterality is left or right. Therefore, laterally paired anatomy
sections may appear two times, once for each laterality. Findings of
unpaired anatomy, are separately contained in a separate "unilateral"
section container. Therefore, in vascular ultrasound, laterality is
always expressed at the section heading level with one of three states:
left, right, or unilateral (unpaired). There is no provision for anatomy
of unknown laterality other than as a TEXT content item in the summary.

Note that expressing laterality at the heading level differs from OB-GYN
Pelvic and fetal vasculature, which expresses laterality as concept
modifiers of the anatomic containers.

================================ ==============================
**Section Heading Concept Name** **Section Heading Laterality**
================================ ==============================
Cerebral Vessels                 Left, Right or Unilateral
Artery of Neck                   Left, Right
Artery of Lower Extremity        Left, Right
Vein of Lower Extremity          Left, Right
Artery of Upper Extremity        Left, Right
Vein of Upper Extremity          Left, Right
Vascular Structure of Kidney     Left, Right
Artery of Abdomen                Left, Right or Unilateral
Vein of Abdomen                  Left, Right or Unilateral
================================ ==============================

The common vascular pattern is a battery of measurements and
calculations repeatedly applied to various anatomic locations. The
anatomic location is the acquisition context of the measurement group.
For example, a measurement group may have a measurement source of Common
Iliac Artery with several measurement instances and measurement types
such as mean velocity, peak systolic velocity, acceleration time, etc.

There are distinct anatomic concepts to modify the base anatomy concept.
The modification expression is a content item with a modifier concept
name and value selected from a Context Group as the table shows below.

+-----------------------+-------------------+-----------------------+
| **Anatomic Modifier   | **Context Group** | **Usage**             |
| Concept Name**        |                   |                       |
+=======================+===================+=======================+
| `(272741003, SCT,     |                   | Distinguishes         |
| "Lateral              |                   | laterality            |
| ity") <http://snomed. |                   |                       |
| info/id/272741003>`__ |                   |                       |
+-----------------------+-------------------+-----------------------+
| `(106233006, SCT,     |                   | Distinguishes the     |
| "Topographical        |                   | location along a      |
| Modif                 |                   | segment: prox, mid,   |
| ier") <http://snomed. |                   | distal, …             |
| info/id/106233006>`__ |                   |                       |
+-----------------------+-------------------+-----------------------+
| (125101, DCM, "Vessel |                   | Distinguishes between |
| Branch")              |                   | one of multiple       |
|                       |                   | branches: inferior,   |
|                       |                   | middle                |
+-----------------------+-------------------+-----------------------+

.. _sect_M.2:

Vascular Examples
-----------------

The following are simple, non-comprehensive illustrations of significant
report sections.

.. _sect_M.2.1:

Example 1: Renal Vessels
~~~~~~~~~~~~~~~~~~~~~~~~

+---------+-------------------------+-------------------------+-----+
| Nest    | Code Meaning of Concept | Code Meaning or Example | TID |
|         | Name                    | Value                   |     |
+=========+=========================+=========================+=====+
| 1       | Vascular Ultrasound     |                         |     |
|         | Procedure Report        |                         |     |
+---------+-------------------------+-------------------------+-----+
| 1.1     | Language of Content     | English                 |     |
|         | Item and Descendants    |                         |     |
+---------+-------------------------+-------------------------+-----+
| 1.2     | Subject Name            | John Doe                |     |
+---------+-------------------------+-------------------------+-----+
| 1.3     | Subject ID              | 123-45-9876             |     |
+---------+-------------------------+-------------------------+-----+
| 1.4     | Procedure Study         | 1.                      |     |
|         | Instance UID            | 2.842.111724.7678.12.33 |     |
+---------+-------------------------+-------------------------+-----+
| 1.5     | Procedure Study         | 1.                      |     |
|         | Component UID           | 2.842.111724.7678.55.33 |     |
+---------+-------------------------+-------------------------+-----+
| 1.6     | Procedure Accession     | 20011007-21             |     |
|         | Number                  |                         |     |
+---------+-------------------------+-------------------------+-----+
| 1.7     | Patient Characteristics |                         |     |
+---------+-------------------------+-------------------------+-----+
| 1.7.n   | …                       |                         |     |
+---------+-------------------------+-------------------------+-----+
| 1.8     | Summary                 |                         |     |
+---------+-------------------------+-------------------------+-----+
| 1.8.n   | …                       |                         |     |
+---------+-------------------------+-------------------------+-----+
| 1.9     | Findings                |                         |     |
+---------+-------------------------+-------------------------+-----+
| 1.9.1   | Finding Site            | Vascular Structure Of   |     |
|         |                         | Kidney                  |     |
+---------+-------------------------+-------------------------+-----+
| 1.9.2   | Laterality              | Right                   |     |
+---------+-------------------------+-------------------------+-----+
| 1.9.3   | Renal Artery            |                         |     |
+---------+-------------------------+-------------------------+-----+
| 1.9.3.1 | Topographical Modifier  | Origin                  |     |
+---------+-------------------------+-------------------------+-----+
| 1.9.3.2 | Peak Systolic Velocity  | 420 cm/s                |     |
+---------+-------------------------+-------------------------+-----+
| 1.9.3.3 | End Diastolic Velocity  | 120 cm/s                |     |
+---------+-------------------------+-------------------------+-----+
| 1.9.3.4 | Resistive Index         | 3.7                     |     |
+---------+-------------------------+-------------------------+-----+
| 1.9.3.5 | Pulsatility Index       | 0.7                     |     |
+---------+-------------------------+-------------------------+-----+
| 1.9.3.6 | Systolic to Diastolic   | 3.5                     |     |
|         | Velocity Ratio          |                         |     |
+---------+-------------------------+-------------------------+-----+
| 1.9.4   | Renal Artery            |                         |     |
+---------+-------------------------+-------------------------+-----+
| 1.9.4.1 | Topographical Modifier  | Proximal                |     |
+---------+-------------------------+-------------------------+-----+
| 1.9.4.n | . . . *other            |                         |     |
|         | measurements*           |                         |     |
+---------+-------------------------+-------------------------+-----+
| 1.9.5   | Renal Artery            |                         |     |
+---------+-------------------------+-------------------------+-----+
| 1.9.5.1 | Topographical Modifier  | Middle                  |     |
+---------+-------------------------+-------------------------+-----+
| 1.9.5.n | . . . *other            |                         |     |
|         | measurements*           |                         |     |
+---------+-------------------------+-------------------------+-----+
| 1.9.6   | Renal Artery            |                         |     |
+---------+-------------------------+-------------------------+-----+
| 1.9.6.1 | Topographical Modifier  | Distal                  |     |
+---------+-------------------------+-------------------------+-----+
| 1.9.6.n | . . . *other            |                         |     |
|         | measurements*           |                         |     |
+---------+-------------------------+-------------------------+-----+
| 1.9.7   | Renal Vein              |                         |     |
+---------+-------------------------+-------------------------+-----+
| 1.9.7.1 | Topographical Modifier  | Middle                  |     |
+---------+-------------------------+-------------------------+-----+
| 1.9.7.2 | Peak Systolic Velocity  | 120 cm/s                |     |
+---------+-------------------------+-------------------------+-----+
| 1.9.7.n | . . . *other            |                         |     |
|         | measurements*           |                         |     |
+---------+-------------------------+-------------------------+-----+
| 1.9.8   | Renal Artery/Aorta      | 2.9                     |     |
|         | Velocity Ratio          |                         |     |
+---------+-------------------------+-------------------------+-----+
| 1.9.n   | *other* *renal vessels* |                         |     |
+---------+-------------------------+-------------------------+-----+
| 1.10    | Findings                |                         |     |
+---------+-------------------------+-------------------------+-----+
| 1.10.1  | Finding Site            | Vascular Structure of   |     |
|         |                         | Kidney                  |     |
+---------+-------------------------+-------------------------+-----+
| 1.10.2  | Laterality              | Left                    |     |
+---------+-------------------------+-------------------------+-----+
|         | …                       |                         |     |
+---------+-------------------------+-------------------------+-----+

.. _sect_M.2.2:

Example 2: Carotids Extracranial
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+------------+-----------------------+-----------------------+-----+
| Nest       | Code Meaning of       | Code Meaning or       | TID |
|            | Concept Name          | Example Value         |     |
+============+=======================+=======================+=====+
| 1          | Vascular Ultrasound   |                       |     |
|            | Procedure Report      |                       |     |
+------------+-----------------------+-----------------------+-----+
| 1.n        | *….*                  |                       |     |
+------------+-----------------------+-----------------------+-----+
| 1.10       | Findings              |                       |     |
+------------+-----------------------+-----------------------+-----+
| 1.10.1     | Findings Site         | Artery of neck        |     |
+------------+-----------------------+-----------------------+-----+
| 1.10.2     | Laterality            | Right                 |     |
+------------+-----------------------+-----------------------+-----+
| 1.10.3     | Common Carotid Artery |                       |     |
+------------+-----------------------+-----------------------+-----+
| 1.10.3.1   | Topographical         | Proximal              |     |
|            | Modifier              |                       |     |
+------------+-----------------------+-----------------------+-----+
| 1.10.3.2   | Peak Systolic         | 80 cm/s               |     |
|            | Velocity              |                       |     |
+------------+-----------------------+-----------------------+-----+
| 1.10.3.3   | Peak Systolic         | 88 cm/s               |     |
|            | Velocity              |                       |     |
+------------+-----------------------+-----------------------+-----+
| 1.10.3.4   | Peak Systolic         | 84 cm/s               |     |
|            | Velocity              |                       |     |
+------------+-----------------------+-----------------------+-----+
| 1.10.3.4.1 | Derivation            | Mean                  |     |
+------------+-----------------------+-----------------------+-----+
| 1.10.4     | Common Carotid Artery |                       |     |
+------------+-----------------------+-----------------------+-----+
| 1.10.4.1   | Topographical         | Middle                |     |
|            | Modifier              |                       |     |
+------------+-----------------------+-----------------------+-----+
| 1.10.4.2   | Peak Systolic         | 180 cm/s              |     |
|            | Velocity              |                       |     |
+------------+-----------------------+-----------------------+-----+
| 1.10.5     | Common Carotid Artery |                       |     |
+------------+-----------------------+-----------------------+-----+
| 1.10.5.1   | Topographical         | Distal                |     |
|            | Modifier              |                       |     |
+------------+-----------------------+-----------------------+-----+
| 1.10.5.2   | Peak Systolic         | 180 cm/s              |     |
|            | Velocity              |                       |     |
+------------+-----------------------+-----------------------+-----+
| 1.10.6     | Carotid bulb          |                       |     |
+------------+-----------------------+-----------------------+-----+
| 1.10.6.1   | Peak Systolic         | 190 cm/s              |     |
|            | Velocity              |                       |     |
+------------+-----------------------+-----------------------+-----+
| 1.10.7     | Internal Carotid      |                       |     |
|            | Artery                |                       |     |
+------------+-----------------------+-----------------------+-----+
| 1.10.7.1   | Topographical         | Proximal              |     |
|            | Modifier              |                       |     |
+------------+-----------------------+-----------------------+-----+
| 1.10.7.2   | Peak Systolic         | 180 cm/s              |     |
|            | Velocity              |                       |     |
+------------+-----------------------+-----------------------+-----+
| 1.10.8     | Internal Carotid      |                       |     |
|            | Artery                |                       |     |
+------------+-----------------------+-----------------------+-----+
| 1.10.8.1   | Topographical         | Distal                |     |
|            | Modifier              |                       |     |
+------------+-----------------------+-----------------------+-----+
| 1.10.8.2   | Peak Systolic         | 180 cm/s              |     |
|            | Velocity              |                       |     |
+------------+-----------------------+-----------------------+-----+
| 1.10.9     | ICA/CCA velocity      | 1.5                   |     |
|            | ratio                 |                       |     |
+------------+-----------------------+-----------------------+-----+
| 1.10.n     | *….*                  |                       |     |
+------------+-----------------------+-----------------------+-----+
| 1.11       | Findings              |                       |     |
+------------+-----------------------+-----------------------+-----+
| 1.11.1     | Finding Site          | Artery of neck        |     |
+------------+-----------------------+-----------------------+-----+
| 1.11.2     | Laterality            | Left                  |     |
+------------+-----------------------+-----------------------+-----+
|            | *….*                  |                       |     |
+------------+-----------------------+-----------------------+-----+

