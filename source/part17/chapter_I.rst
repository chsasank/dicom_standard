.. _chapter_I:

Ultrasound Templates (Informative)
==================================

.. _sect_I.1:

SR Content Tree Structure
-------------------------

The templates for ultrasound reports are defined in .
`figure_title <#figure_I.1-1>`__ is an outline of the common elements of
ultrasound structured reports.

The Patient Characteristics Section is for medical data of immediate
relevance to administering the procedure and interpreting the results.
This information may originate outside the procedure.

The Procedure Summary Section contains exam observations of immediate or
primary significance. This is key information a physician typically
expects to see first in the report.

Measurements typically reside in a measurement group container within a
Section. Measurement groups share context such as anatomical location,
protocol or type of analysis. The grouping may be specific to a product
implementation or even to a user configuration. OB-GYN measurement
groups have related measurements, averages and other derived results.

If present, the Image Library contains a list of images from which
observations were derived. These are referenced from the observations
with by-reference relationships.

.. _sect_I.2:

Procedure Summary
-----------------

The Procedure Summary Section contains the observations of most
immediate interest. Observations in the procedure summary may have
by-reference relationships to other content items.

.. _sect_I.3:

Multiple Fetuses
----------------

Where multiple fetuses exist, the observations specific to each fetus
must reside under separate section headings. The section heading must
specify the fetus observation context and designate so using Subject ID
(121030, DCM, "Subject ID") and/or numerical designation (121037, DCM,
"Fetus Number") as shown below. See .

.. _sect_I.4:

Explicitly Specifying Calculation Dependencies
----------------------------------------------

Reports may specify dependencies of a calculation on its dependent
observations using by-reference relationships. This relationship must be
present for the report reader to know the inputs of the derived value.

.. _sect_I.5:

Linking Measurements to Images, Coordinates
-------------------------------------------

Optionally, the relationship of an observation to its image and image
coordinates can be encoded with by-reference content items as
`figure_title <#figure_I.5-1>`__ shows. For conciseness, the
by-reference relationship points to the content item in the Image
Library, rather than directly to the image.

R-INFERRED FROM relationships to IMAGE content items specify that the
image supports the observation. A purpose of reference in an SCOORD
content item may specify an analytic operation (performed on that image)
that supports or produces the observation.

.. _sect_I.6:

Ob Patterns
-----------

A common OB-GYN pattern is that of several instances of one measurement
type (e.g., BPD), the calculated average of those values, and derived
values such as a gestational age calculated according to an equation or
table. The measurements and calculations are all siblings in the
measurement group. A child content item specifies the equation or table
used to calculate the gestational age. All measurement types must relate
to the same biometric type. For example, it is not allowed to mix a BPD
and a Nuchal Fold Thickness measurement in the same biometry group.

The example above is a gestational age calculated from the measured
value. The relationship is to an equation or table. The inferred from
relationship identifies equation or table in the Concept Name. Codes
from identify the specific equation or table.

Another use case is the calculation of a growth parameter's relationship
to that of a referenced distribution and a known or assumed gestational
age. identify the growth table. `figure_title <#figure_I.6-2>`__ shows
the assignment of a percentile for the measured BPD, against the growth
of a referenced population. The dependency relationship to the
gestational age is a by-reference relationship to the established
gestational age. Though the percentile rank is derived from the BPD
measurement, a by-reference relationship is not essential if one BPD has
a concept modifier indicating that it is the mean or has selection
status (see ). A variation of this pattern is the use of Z-score instead
of percentile rank. Not shown is the expression of the normal
distribution mean, standard deviation, or confidence limits.

Estimated fetal weight (EFW) is a fetus summary item as shown below. It
is calculated from one or more growth parameters (the inferred from
relationships are not shown). allows specifying how the value was
derived. Terms from specify the table or equation that yields the EFW
from growth parameters.

"EFW percentile rank" is another summary term. By definition, this term
depends upon the EFW and the population distribution of the ranking. A
Reference Authority content item identifies the distribution. is list of
established reference authorities.

.. _sect_I.7:

Selected Value
--------------

When multiple observations of the same type exist, one of these may be
the selected value. Typically, this value is the average of the others,
or it may be the last entered, or user chosen. provides a content item
with concept name of (121404, DCM, "Selection Status") and a value set
specified by D.

There are multiple ways that a measurement may originate. The
measurement value may result as an output of an image interactive,
system tool. Alternatively, the user may directly enter the value, or
the system may create a value automatically as the mean of multiple
measurement instances. provides that a concept modifier of the numeric
content item specify the derivation of the measurement. The concept name
of the modifier is (121401, DCM, "Derivation"). provides concepts of
appropriate measurement modifiers. `figure_title <#figure_I.7-2>`__
illustrates such a case.

.. _sect_I.8:

OB-GYN Examples
---------------

The following are simple, non-comprehensive illustrations of report
sections.

.. _sect_I.8.1:

Example 1: OB-GYN Root with Observation Context
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The following example shows the highest level of content items for a
second or third trimester OB exam. Subsequent examples show details of
section content,

+--------+-------------------------+-------------------------+-----+
| Nest   | Code Meaning of Concept | Code Meaning or Example | TID |
|        | Name                    | Value                   |     |
+========+=========================+=========================+=====+
| 1      | OB-GYN Ultrasound       |                         |     |
|        | Procedure Report        |                         |     |
+--------+-------------------------+-------------------------+-----+
| 1.1    | Language of Content     | English                 |     |
|        | Item and Descendants    |                         |     |
+--------+-------------------------+-------------------------+-----+
| 1.2    | Subject Name            | Jane Doe                |     |
+--------+-------------------------+-------------------------+-----+
| 1.3    | Subject ID              | 123-45-6789             |     |
+--------+-------------------------+-------------------------+-----+
| 1.4    | Procedure Study         | 1.                      |     |
|        | Instance UID            | 2.842.111724.7678.32.34 |     |
+--------+-------------------------+-------------------------+-----+
| 1.5    | Procedure Study         | 1.                      |     |
|        | Component UID           | 2.842.111724.7678.55.34 |     |
+--------+-------------------------+-------------------------+-----+
| 1.6    | Procedure Accession     | 20011007-21             |     |
|        | Number                  |                         |     |
+--------+-------------------------+-------------------------+-----+
| 1.7    | Image Library           |                         |     |
+--------+-------------------------+-------------------------+-----+
| 1.7.1  |                         | IMAGE 1                 |     |
+--------+-------------------------+-------------------------+-----+
| 1.7.2  |                         | IMAGE 2                 |     |
+--------+-------------------------+-------------------------+-----+
| 1.7.n  |                         | IMAGE N                 |     |
+--------+-------------------------+-------------------------+-----+
| 1.8    | Patient Characteristics |                         |     |
+--------+-------------------------+-------------------------+-----+
| 1.8.n  |                         |                         |     |
+--------+-------------------------+-------------------------+-----+
| 1.9    | Summary                 |                         |     |
+--------+-------------------------+-------------------------+-----+
| 1.9.n  |                         |                         |     |
+--------+-------------------------+-------------------------+-----+
| 1.10   | Fetal Biometry Ratios   |                         |     |
+--------+-------------------------+-------------------------+-----+
| 1.10.n |                         |                         |     |
+--------+-------------------------+-------------------------+-----+
| 1.11   | Long Bones              |                         |     |
+--------+-------------------------+-------------------------+-----+
| 1.11.n |                         |                         |     |
+--------+-------------------------+-------------------------+-----+
| 1.12   | Fetal Cranium           |                         |     |
+--------+-------------------------+-------------------------+-----+
| 1.12.n |                         |                         |     |
+--------+-------------------------+-------------------------+-----+
| 1.13   | Biophysical Profile     |                         |     |
+--------+-------------------------+-------------------------+-----+
| 1.13.n |                         |                         |     |
+--------+-------------------------+-------------------------+-----+
| 1.14   | Amniotic Sac            |                         |     |
+--------+-------------------------+-------------------------+-----+
| 1.14.n |                         |                         |     |
+--------+-------------------------+-------------------------+-----+

The following example shows the highest level of content items for a GYN
exam. Subsequent examples show details of section content.

+-------+------------------------------------+-------------------------------+-----+
| Nest  | Code Meaning of Concept Name       | Code Meaning or Example Value | TID |
+=======+====================================+===============================+=====+
| 1     | OB-GYN Ultrasound Procedure Report |                               |     |
+-------+------------------------------------+-------------------------------+-----+
| 1.1   | Subject Name                       | Jane Doe                      |     |
+-------+------------------------------------+-------------------------------+-----+
| 1.2   | Subject ID                         | 123-45-6789                   |     |
+-------+------------------------------------+-------------------------------+-----+
| 1.3   | Image Library                      |                               |     |
+-------+------------------------------------+-------------------------------+-----+
| 1.3.1 |                                    | IMAGE 1                       |     |
+-------+------------------------------------+-------------------------------+-----+
| 1.3.2 |                                    | IMAGE 2                       |     |
+-------+------------------------------------+-------------------------------+-----+
| 1.3.n |                                    | IMAGE N                       |     |
+-------+------------------------------------+-------------------------------+-----+
| 1.4   | Patient Characteristics            |                               |     |
+-------+------------------------------------+-------------------------------+-----+
| 1.4.n |                                    |                               |     |
+-------+------------------------------------+-------------------------------+-----+
| 1.5   | Findings                           |                               |     |
+-------+------------------------------------+-------------------------------+-----+
| 1.5.1 | Findings Site                      | Ovary                         |     |
+-------+------------------------------------+-------------------------------+-----+
| 1.5.n |                                    |                               |     |
+-------+------------------------------------+-------------------------------+-----+
| 1.6   | Findings                           |                               |     |
+-------+------------------------------------+-------------------------------+-----+
| 1.6.1 | Findings Site                      | Ovarian Follicle              |     |
+-------+------------------------------------+-------------------------------+-----+
| 1.6.2 | Laterality                         | Left                          |     |
+-------+------------------------------------+-------------------------------+-----+
| 1.6.n |                                    |                               |     |
+-------+------------------------------------+-------------------------------+-----+
| 1.7   | Findings                           |                               |     |
+-------+------------------------------------+-------------------------------+-----+
| 1.7.1 | Findings Site                      | Ovarian Follicle              |     |
+-------+------------------------------------+-------------------------------+-----+
| 1.7.2 | Laterality                         | Right                         |     |
+-------+------------------------------------+-------------------------------+-----+
| 1.7.n |                                    |                               |     |
+-------+------------------------------------+-------------------------------+-----+
| 1.8   | Pelvis and Uterus                  |                               |     |
+-------+------------------------------------+-------------------------------+-----+
| 1.8.n |                                    |                               |     |
+-------+------------------------------------+-------------------------------+-----+

.. _sect_I.8.2:

Example 2: OB-GYN Patient Characteristics and Procedure Summary
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+-----------+------------------------+------------------------+-----+
| Nest      | Code Meaning of        | Code Meaning or        | TID |
|           | Concept Name           | Example Value          |     |
+===========+========================+========================+=====+
| 1         | OB-GYN Ultrasound      |                        |     |
|           | Procedure Report       |                        |     |
+-----------+------------------------+------------------------+-----+
|           | ….                     |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.8       | Patient                |                        |     |
|           | Characteristics        |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.8.1     | Gravida                | 5                      |     |
+-----------+------------------------+------------------------+-----+
| 1.8.2     | Para                   | 3                      |     |
+-----------+------------------------+------------------------+-----+
| 1.8.3     | Aborta                 | 2                      |     |
+-----------+------------------------+------------------------+-----+
| 1.8.4     | Ectopic Pregnancies    | 1                      |     |
+-----------+------------------------+------------------------+-----+
| 1.9       | Summary                |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.9.1     | LMP                    | 20010101               |     |
+-----------+------------------------+------------------------+-----+
| 1.9.2     | EDD                    | 20010914               |     |
+-----------+------------------------+------------------------+-----+
| 1.9.3     | EDD from LMP           | 20010914               |     |
+-----------+------------------------+------------------------+-----+
| 1.9.4     | EDD from average       | 20010907               |     |
|           | ultrasound age         |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.9.5     | Gestational age by     | 185 d                  |     |
|           | ovulation date         |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.9.6     | Fetus Summary          |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.9.6.1   | EFW                    | 2222 g                 |     |
+-----------+------------------------+------------------------+-----+
| 1.9.6.1.1 | +/-, range of          | 200 g                  |     |
|           | measurement            |                        |     |
|           | uncertainty            |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.9.6.1.2 | Equation               | EFW by AC, BPD,        |     |
|           |                        | Hadlock 1984           |     |
+-----------+------------------------+------------------------+-----+
| 1.9.6.2   | Comment                | Enlarged cisterna      |     |
|           |                        | magna                  |     |
+-----------+------------------------+------------------------+-----+
| 1.9.6.3   | Comment                | Choroid plexus cyst    |     |
+-----------+------------------------+------------------------+-----+

.. _sect_I.8.3:

Example 3: OB-GYN Multiple Fetus
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+-----------+------------------------+------------------------+-----+
| Nest      | Code Meaning of        | Code Meaning or        | TID |
|           | Concept Name           | Example Value          |     |
+===========+========================+========================+=====+
| 1         | OB-GYN Ultrasound      |                        |     |
|           | Procedure Report       |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.n       | ….                     |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.5       | Summary                |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.5.1     | EDD from LMP           | 20020325               |     |
+-----------+------------------------+------------------------+-----+
| 1.5.2     | Fetus Summary          |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.5.2.1   | Fetus ID               | A                      |     |
+-----------+------------------------+------------------------+-----+
| 1.5.2.2   | EFW                    | 1.6 Kg                 |     |
+-----------+------------------------+------------------------+-----+
| 1.5.2.2.1 | Equation               | EFW by AC, BPD,        |     |
|           |                        | Hadlock 1984           |     |
+-----------+------------------------+------------------------+-----+
| 1.5.2.2.2 | +/-, range of          | 160g                   |     |
|           | measurement            |                        |     |
|           | uncertainty            |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.5.2.3   | Fetal Heart Rate       | 120 {H.B.}/min         |     |
+-----------+------------------------+------------------------+-----+
| 1.5.3     | Fetus Summary          |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.5.3.1   | Fetus ID               | B                      |     |
+-----------+------------------------+------------------------+-----+
| 1.5.3.2   | Comment                | Choroid plexus cyst    |     |
+-----------+------------------------+------------------------+-----+
| 1.5.3.3   | EFW                    | 1.4 kg                 |     |
+-----------+------------------------+------------------------+-----+
| 1.5.3.3.1 | Equation               | EFW by AC, BPD,        |     |
|           |                        | Hadlock 1984           |     |
+-----------+------------------------+------------------------+-----+
| 1.5.3.3.2 | +/-, range of          | 140 g                  |     |
|           | measurement            |                        |     |
|           | uncertainty            |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.5.3.4   | Fetal Heart Rate       | 135 {H.B.}/min         |     |
+-----------+------------------------+------------------------+-----+
| 1.6       | Biophysical Profile    |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.6.1     | Fetus ID               | A                      |     |
+-----------+------------------------+------------------------+-----+
| 1.6.n     | …                      |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.7       | Biophysical Profile    |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.7.1     | Fetus ID               | B                      |     |
+-----------+------------------------+------------------------+-----+
| 1.7.n     | …                      |                        |     |
+-----------+------------------------+------------------------+-----+

.. _sect_I.8.4:

Example 4: Biophysical Profile
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+-------+------------------------------------+-------------------------------+-----+
| Nest  | Code Meaning of Concept Name       | Code Meaning or Example Value | TID |
+=======+====================================+===============================+=====+
| 1     | OB-GYN Ultrasound Procedure Report |                               |     |
+-------+------------------------------------+-------------------------------+-----+
| 1.n   | ….                                 |                               |     |
+-------+------------------------------------+-------------------------------+-----+
| 1.9   | Biophysical Profile                |                               |     |
+-------+------------------------------------+-------------------------------+-----+
| 1.9.1 | Gross Body Movement                | 2 {0:2}                       |     |
+-------+------------------------------------+-------------------------------+-----+
| 1.9.2 | Fetal Breathing                    | 2 {0:2}                       |     |
+-------+------------------------------------+-------------------------------+-----+
| 1.9.3 | Fetal Tone                         | 2 {0:2}                       |     |
+-------+------------------------------------+-------------------------------+-----+
| 1.9.4 | Fetal Heart Reactivity             | 2 {0:2}                       |     |
+-------+------------------------------------+-------------------------------+-----+
| 1.9.5 | Amniotic Fluid Volume              | 2 {0:2}                       |     |
+-------+------------------------------------+-------------------------------+-----+
| 1.9.6 | Biophysical Profile Sum Score      | 10 {0:10}                     |     |
+-------+------------------------------------+-------------------------------+-----+

.. _sect_I.8.5:

Example 5: Biometry Ratios
~~~~~~~~~~~~~~~~~~~~~~~~~~

Optionally, but not shown, the ratios may have by-reference,
inferred-from relationships to the content items holding the numerator
and denominator values.

+---------+-------------------------+-------------------------+-----+
| Nest    | Code Meaning of Concept | Code Meaning or Example | TID |
|         | Name                    | Value                   |     |
+=========+=========================+=========================+=====+
| 1       | OB-GYN Ultrasound       |                         |     |
|         | Procedure Report        |                         |     |
+---------+-------------------------+-------------------------+-----+
| 1.n     | ….                      |                         |     |
+---------+-------------------------+-------------------------+-----+
| 1.9     | Fetal Biometry Ratios   |                         |     |
+---------+-------------------------+-------------------------+-----+
| 1.9.1   | HC/AC                   | 77%                     |     |
+---------+-------------------------+-------------------------+-----+
| 1.9.2   | FL/AC                   | 22 %                    |     |
+---------+-------------------------+-------------------------+-----+
| 1.9.2.1 | Normal Range Lower      | 20 %                    |     |
|         | Limit                   |                         |     |
+---------+-------------------------+-------------------------+-----+
| 1.9.2.2 | Normal Range Upper      | 24 %                    |     |
|         | Limit                   |                         |     |
+---------+-------------------------+-------------------------+-----+
| 1.9.2.3 | Normal Range Authority  | Hadlock, AJR 1983       |     |
+---------+-------------------------+-------------------------+-----+
| 1.9.3   | FL/BPD                  | 79 %                    |     |
+---------+-------------------------+-------------------------+-----+
| 1.9.3.1 | Normal Range Lower      | 71 %                    |     |
|         | Limit                   |                         |     |
+---------+-------------------------+-------------------------+-----+
| 1.9.3.2 | Normal Range Upper      | 81 %                    |     |
|         | Limit                   |                         |     |
+---------+-------------------------+-------------------------+-----+
| 1.9.3.3 | Normal Range Authority  | Hohler, Am J of Ob and  |     |
|         |                         | Gyn 1981                |     |
+---------+-------------------------+-------------------------+-----+
| 1.9.4   | Cephalic Index          | 82 %                    |     |
+---------+-------------------------+-------------------------+-----+
| 1.9.4.1 | Normal Range Lower      | 70 %                    |     |
|         | Limit                   |                         |     |
+---------+-------------------------+-------------------------+-----+
| 1.9.4.2 | Normal Range Upper      | 86 %                    |     |
|         | Limit                   |                         |     |
+---------+-------------------------+-------------------------+-----+
| 1.9.4.3 | Normal Range Authority  | Hadlock, AJR 1981       |     |
+---------+-------------------------+-------------------------+-----+

.. _sect_I.8.6:

Example 6: Biometry
~~~~~~~~~~~~~~~~~~~

This example shows measurements and estimated gestational age.

+-----------+------------------------+------------------------+-----+
| Nest      | Code Meaning of        | Code Meaning or        | TID |
|           | Concept Name           | Example Value          |     |
+===========+========================+========================+=====+
| 1         | OB-GYN Ultrasound      |                        |     |
|           | Procedure Report       |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.n       | ….                     |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.8       | Fetal Biometry         |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.8.1     | Biometry Group         |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.8.1.1   | Biparietal Diameter    | 5.5 cm                 |     |
+-----------+------------------------+------------------------+-----+
| 1.8.1.2   | Biparietal Diameter    | 5.3 cm                 |     |
+-----------+------------------------+------------------------+-----+
| 1.8.1.3   | Biparietal Diameter    | 5.4 cm                 |     |
+-----------+------------------------+------------------------+-----+
| 1.8.1.3.1 | Derivation             | Mean                   |     |
+-----------+------------------------+------------------------+-----+
| 1.8.1.4   | Gestational Age        | 190 d                  |     |
+-----------+------------------------+------------------------+-----+
| 1.8.1.4.1 | Equation               | Jeanty, 1982           |     |
+-----------+------------------------+------------------------+-----+
| 1.8.1.4.2 | 5\ :sup:`th`           | 131 d                  |     |
|           | Percentile Value of    |                        |     |
|           | population             |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.8.1.4.3 | 95\ :sup:`th`          | 173 d                  |     |
|           | Percentile Value of    |                        |     |
|           | population             |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.8.2     | Biometry Group         |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.8.2.1   | Occipital-Frontal      | 18.1 cm                |     |
|           | Diameter               |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.8.3     | Biometry Group         |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.8.3.1   | Head Circumference     | 34.3 cm                |     |
+-----------+------------------------+------------------------+-----+
| 1.8.3.1.1 | Derivation             | Estimated              |     |
+-----------+------------------------+------------------------+-----+
| 1.8.4     | Biometry Group         |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.8.4.1   | Abdominal              | 34.9 cm                |     |
|           | Circumference          |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.8.4.2   | Abdominal              | 34.3 cm                |     |
|           | Circumference          |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.8.4.3   | Abdominal              | 34.3 cm                |     |
|           | Circumference          |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.8.4.4   | Abdominal              | 34.5 cm                |     |
|           | Circumference          |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.8.4.4.1 | Derivation             | Mean                   |     |
+-----------+------------------------+------------------------+-----+
| 1.8.4.5   | Gestational Age        | 190 d                  |     |
+-----------+------------------------+------------------------+-----+
| 1.8.4.5.1 | Equation               | Hadlock, 1984          |     |
+-----------+------------------------+------------------------+-----+
| 1.8.4.5.2 | 2 Sigma Lower Value of | 184 d                  |     |
|           | population             |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.8.4.5.3 | 2 Sigma Upper Value of | 196 d                  |     |
|           | population             |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.8.5     | Biometry Group         |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.8.5.1   | Femur Length           | 4.5 cm                 |     |
+-----------+------------------------+------------------------+-----+
| 1.8.5.n   | …                      |                        |     |
+-----------+------------------------+------------------------+-----+

This example shows measurements and with percentile ranking.

+-----------+------------------------+------------------------+-----+
| Nest      | Code Meaning of        | Code Meaning or        | TID |
|           | Concept Name           | Example Value          |     |
+===========+========================+========================+=====+
| 1         | OB-GYN Ultrasound      |                        |     |
|           | Procedure Report       |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.n       | ….                     |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.8       | Fetal Biometry         |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.8.1     | Biometry Group         |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.8.1.1   | Biparietal Diameter    | 5.5 cm                 |     |
+-----------+------------------------+------------------------+-----+
| 1.8.1.2   | Biparietal Diameter    | 5.3 cm                 |     |
+-----------+------------------------+------------------------+-----+
| 1.8.1.3   | Biparietal Diameter    | 5.4 cm                 |     |
+-----------+------------------------+------------------------+-----+
| 1.8.1.3.1 | Derivation             | Mean                   |     |
+-----------+------------------------+------------------------+-----+
| 1.8.1.4   | Growth Percentile Rank | 63 %                   |     |
+-----------+------------------------+------------------------+-----+
| 1.8.1.4.1 | Equation               | BPD, Jeanty 1982       |     |
+-----------+------------------------+------------------------+-----+
| 1.8.2     | Biometry Group         |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.8.2.n   | …                      |                        |     |
+-----------+------------------------+------------------------+-----+

.. _sect_I.8.7:

Example 7: Amniotic Sac
~~~~~~~~~~~~~~~~~~~~~~~

+-------+------------------------------------+-------------------------------+-----+
| Nest  | Code Meaning of Concept Name       | Code Meaning or Example Value | TID |
+=======+====================================+===============================+=====+
| 1     | OB-GYN Ultrasound Procedure Report |                               |     |
+-------+------------------------------------+-------------------------------+-----+
| 1.n   | ….                                 |                               |     |
+-------+------------------------------------+-------------------------------+-----+
| 1.6   | Findings                           |                               |     |
+-------+------------------------------------+-------------------------------+-----+
| 1.6.1 | Finding Site                       | Amniotic Sac                  |     |
+-------+------------------------------------+-------------------------------+-----+
| 1.6.2 | Amniotic Fluid Index               | 11 cm                         |     |
+-------+------------------------------------+-------------------------------+-----+
| 1.6.3 | First Quadrant Diameter            | 10 cm                         |     |
+-------+------------------------------------+-------------------------------+-----+
| 1.6.4 | Second Quadrant Diameter           | 12 cm                         |     |
+-------+------------------------------------+-------------------------------+-----+
| 1.6.5 | Third Quadrant Diameter            | 11 cm                         |     |
+-------+------------------------------------+-------------------------------+-----+
| 1.6.6 | Fourth Quadrant Diameter           | 12 cm                         |     |
+-------+------------------------------------+-------------------------------+-----+

.. _sect_I.8.8:

Example 8: OB-GYN Ovaries
~~~~~~~~~~~~~~~~~~~~~~~~~

The content structure in the example below conforms to . The example
shows the volume derived from three perpendicular diameters.

+-----------+------------------------+------------------------+-----+
| Nest      | Code Meaning of        | Code Meaning or        | TID |
|           | Concept Name           | Example Value          |     |
+===========+========================+========================+=====+
| 1         | OB-GYN Ultrasound      |                        |     |
|           | Procedure Report       |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.n       | ….                     |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.9       | Findings               |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.9.1     | Finding Site           | Ovary                  |     |
+-----------+------------------------+------------------------+-----+
| 1.9.2     | Ovary                  |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.9.2.1   | Left Ovary Volume      | 6 cm3                  |     |
+-----------+------------------------+------------------------+-----+
| 1.9.2.2   | Left Ovary Length      | 3 cm                   |     |
+-----------+------------------------+------------------------+-----+
| 1.9.2.3   | Left Ovary Length      | 3 cm                   |     |
+-----------+------------------------+------------------------+-----+
| 1.9.2.4   | Left Ovary Length      | 3 cm                   |     |
+-----------+------------------------+------------------------+-----+
| 1.9.2.4.1 | Derivation             | Mean                   |     |
+-----------+------------------------+------------------------+-----+
| 1.9.2.5   | Left Ovary Width       | 2 cm                   |     |
+-----------+------------------------+------------------------+-----+
| 1.9.2.5.1 | Derivation             | Mean                   |     |
+-----------+------------------------+------------------------+-----+
| 1.9.2.6   | Left Ovary Height      | 2 cm                   |     |
+-----------+------------------------+------------------------+-----+
| 1.9.2.6.1 | Derivation             | Mean                   |     |
+-----------+------------------------+------------------------+-----+
| 1.9.3     | Ovary                  |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.9.3.1   | Right Ovary Volume     | 7 cm3                  |     |
+-----------+------------------------+------------------------+-----+
| 1.9.3.2   | …                      |                        |     |
+-----------+------------------------+------------------------+-----+

.. _sect_I.8.9:

Example 9: OB-GYN Follicles
~~~~~~~~~~~~~~~~~~~~~~~~~~~

The content structure in the example below conforms to . It uses
multiple measurements and derived averages for each of the perpendicular
diameters.

+-----------+------------------------+------------------------+-----+
| Nest      | Code Meaning of        | Code Meaning or        | TID |
|           | Concept Name           | Example Value          |     |
+===========+========================+========================+=====+
| 1         | OB-GYN Ultrasound      |                        |     |
|           | Procedure Report       |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.n       | ….                     |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.8       | Findings               |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.8.1     | Finding Site           | Ovarian Follicle       |     |
+-----------+------------------------+------------------------+-----+
| 1.8.2     | Laterality             | Right                  |     |
+-----------+------------------------+------------------------+-----+
| 1.8.3     | Number of follicles in | 2                      |     |
|           | right ovary            |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.8.4     | Measurement Group      |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.8.4.1   | Identifier             | #1                     |     |
+-----------+------------------------+------------------------+-----+
| 1.8.4.2   | Volume                 | 3 cm3                  |     |
+-----------+------------------------+------------------------+-----+
| 1.8.4.3   | Follicle Diameter      | 15 mm                  |     |
+-----------+------------------------+------------------------+-----+
| 1.8.4.4   | Follicle Diameter      | 13 mm                  |     |
+-----------+------------------------+------------------------+-----+
| 1.8.4.5   | Follicle Diameter      | 14 mm                  |     |
+-----------+------------------------+------------------------+-----+
| 1.8.4.5.1 | Derivation             | Mean                   |     |
+-----------+------------------------+------------------------+-----+
| 1.8.5     | Measurement Group      |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.8.5.1   | Identifier             | #2                     |     |
+-----------+------------------------+------------------------+-----+
| 1.8.5.2   | Volume                 | 4 cm3                  |     |
+-----------+------------------------+------------------------+-----+
| 1.8.5.3   | Follicle Diameter      | 18 mm                  |     |
+-----------+------------------------+------------------------+-----+
| 1.9       | Findings               |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.9.1     | Finding Site           | Ovarian Follicle       |     |
+-----------+------------------------+------------------------+-----+
| 1.9.2     | Laterality             | Left                   |     |
+-----------+------------------------+------------------------+-----+
| 1.9.3     | Number of follicles in | 1                      |     |
|           | left ovary             |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.9.4     | Follicle Measurement   |                        |     |
|           | Group                  |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.9.4.1   | Identifier             | #1                     |     |
+-----------+------------------------+------------------------+-----+
| 1.9.4.2   | Volume                 | 3 cm3                  |     |
+-----------+------------------------+------------------------+-----+
| 1.9.4.3   | Follicle Diameter      | 15 mm                  |     |
+-----------+------------------------+------------------------+-----+

.. _sect_I.8.10:

Example 10: Pelvis and Uterus
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+---------+-------------------------+-------------------------+-----+
| Nest    | Code Meaning of Concept | Code Meaning or Example | TID |
|         | Name                    | Value                   |     |
+=========+=========================+=========================+=====+
| 1       | OB-GYN Ultrasound       |                         |     |
|         | Procedure Report        |                         |     |
+---------+-------------------------+-------------------------+-----+
| 1.n     | ….                      |                         |     |
+---------+-------------------------+-------------------------+-----+
| 1.9     | Pelvis and Uterus       |                         |     |
+---------+-------------------------+-------------------------+-----+
| 1.9.1   | Uterus                  |                         |     |
+---------+-------------------------+-------------------------+-----+
| 1.9.1.1 | Uterus Volume           | 136 cm3                 |     |
+---------+-------------------------+-------------------------+-----+
| 1.9.1.2 | Uterus Length           | 9.5 cm                  |     |
+---------+-------------------------+-------------------------+-----+
| 1.9.1.3 | Uterus Width            | 5.9 cm                  |     |
+---------+-------------------------+-------------------------+-----+
| 1.9.1.4 | Uterus Height           | 4.2 cm                  |     |
+---------+-------------------------+-------------------------+-----+
| 1.9.2   | Endometrium Thickness   | 4 mm                    |     |
+---------+-------------------------+-------------------------+-----+
| 1.9.3   | Cervix Length           | 5.3 cm                  |     |
+---------+-------------------------+-------------------------+-----+

