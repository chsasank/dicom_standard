.. _chapter_KKKK:

Encoding Quantitative Image Family Parameters (Informative)
===========================================================

.. _sect_KKKK.1:

Encoding of Quantitative Image Family Parameters With RWVM
----------------------------------------------------------

In this example, the real-world value mapped pixel value represents
attenuation of water. The pixel values range from 0 to 4095 like a
conventional CT Image and are mapped starting from -1024.

.. table:: Example Material Specific Images for the Real World Value
Mapping Macro

   +----------------+----------------+----------------+----------------+
   | Attribute      | Tag            | Value          | Comment        |
   +================+================+================+================+
   | Real World     | (0040,9096)    |                |                |
   | Value Mapping  |                |                |                |
   | Sequence       |                |                |                |
   +----------------+----------------+----------------+----------------+
   | ITEM 1         |                |                |                |
   +----------------+----------------+----------------+----------------+
   | >Real World    | (0040,9216)    | 0              |                |
   | Value First    |                |                |                |
   | Value Mapped   |                |                |                |
   +----------------+----------------+----------------+----------------+
   | >Real World    | (0040,9211)    | 4095           |                |
   | Value Last     |                |                |                |
   | Value Mapped   |                |                |                |
   +----------------+----------------+----------------+----------------+
   | >Real World    | (0040,9224)    | -1024          |                |
   | Value          |                |                |                |
   | Intercept      |                |                |                |
   +----------------+----------------+----------------+----------------+
   | >Real World    | (0040,9225)    | 1              |                |
   | Value Slope    |                |                |                |
   +----------------+----------------+----------------+----------------+
   | >LUT           | (0028,3003)    | "Water         |                |
   | Explanation    |                | component of   |                |
   |                |                | image with     |                |
   |                |                | water and      |                |
   |                |                | iodine as base |                |
   |                |                | materials"     |                |
   +----------------+----------------+----------------+----------------+
   | >LUT Label     | (0040,9210)    | MAT_SPECIFIC   | Per guidance   |
   |                |                |                | in this        |
   |                |                |                | corresponds to |
   |                |                |                | Image Type     |
   |                |                |                | Value 4        |
   +----------------+----------------+----------------+----------------+
   | >Measurement   | (0040,08EA)    |                |                |
   | Units Code     |                |                |                |
   | Sequence       |                |                |                |
   +----------------+----------------+----------------+----------------+
   | >>Include      | ([hnsf'U],     |                |                |
   |                | UCUM,          |                |                |
   |                | "Hounsfield    |                |                |
   |                | unit")         |                |                |
   +----------------+----------------+----------------+----------------+
   | >Quantity      | (0040,9220)    |                |                |
   | Definition     |                |                |                |
   | Sequence       |                |                |                |
   +----------------+----------------+----------------+----------------+
   | >>CODE         | `(11713004,    |                |                |
   | `(105590001,   | SCT,           |                |                |
   | SCT,           | "W             |                |                |
   | "Substa        | ater") <http:/ |                |                |
   | nce") <http:// | /snomed.info/i |                |                |
   | snomed.info/id | d/11713004>`__ |                |                |
   | /105590001>`__ |                |                |                |
   +----------------+----------------+----------------+----------------+
   | >>CODE         | (129323, DCM,  |                |                |
   | `(370129005,   | "Material      |                |                |
   | SCT,           | Specific       |                |                |
   | "Measurement   | image")        |                |                |
   | Met            |                |                |                |
   | hod") <http:// |                |                |                |
   | snomed.info/id |                |                |                |
   | /370129005>`__ |                |                |                |
   +----------------+----------------+----------------+----------------+

This example shows how to use the to describe pixel values of the
encoding of Quantitative Image Family parameters, by adding coded
concepts to the RWVM that describe the material, the method and the
value range in case of Value-based images.

In this example, a Value-based material map image has been created where
pixel values between 0 and 20 correspond to voxels that are associated
with Uric Acid and pixel values between 20 and 40 correspond to voxels
that are associated with Calcium:

-  In the Quantity Definition Sequence `(105590001, SCT,
   "Substance") <http://snomed.info/id/105590001>`__ is used to indicate
   that the pixel value in the specified range is deemed to represent
   the presence of that substance, regardless of the actual pixel value
   within that range. It would be inappropriate to use `(246205007, SCT,
   "Quantity") <http://snomed.info/id/246205007>`__ since the
   transformed pixel values do not represent a quantitative value.

-  The measurement method of (113250, DCM, "Value-based material image")
   might be replaced by a more specific code that actually described the
   method of computation such as "Gaussian distribution".

-  For the sake of illustration, in this image a pixel value of 20 maps
   to both "Uric Acid" and "Calcium".

.. table:: Example Value Based Images for the Real World Value Mapping
Macro

   +------------------+------------------+------------------+---------+
   | Attribute        | Tag              | Value            | Comment |
   +==================+==================+==================+=========+
   | Real World Value | (0040,9096)      |                  |         |
   | Mapping Sequence |                  |                  |         |
   +------------------+------------------+------------------+---------+
   | ITEM 1           |                  |                  |         |
   +------------------+------------------+------------------+---------+
   | >Real World      | (0040,9216)      | 0                |         |
   | Value First      |                  |                  |         |
   | Value Mapped     |                  |                  |         |
   +------------------+------------------+------------------+---------+
   | >Real World      | (0040,9211)      | 20               |         |
   | Value Last Value |                  |                  |         |
   | Mapped           |                  |                  |         |
   +------------------+------------------+------------------+---------+
   | >Real World      | (0040,9224)      | 0                |         |
   | Value Intercept  |                  |                  |         |
   +------------------+------------------+------------------+---------+
   | >Real World      | (0040,9225)      | 1                |         |
   | Value Slope      |                  |                  |         |
   +------------------+------------------+------------------+---------+
   | >LUT Explanation | (0028,3003)      | "Value-based     |         |
   |                  |                  | substance map    |         |
   |                  |                  | for kidney       |         |
   |                  |                  | stone"           |         |
   +------------------+------------------+------------------+---------+
   | >LUT Label       | (0040,9210)      | MAT\_            |         |
   |                  |                  | VALUE_BASED      |         |
   +------------------+------------------+------------------+---------+
   | >Measurement     | (0040,08EA)      |                  |         |
   | Units Code       |                  |                  |         |
   | Sequence         |                  |                  |         |
   +------------------+------------------+------------------+---------+
   | >>Include        | (1, UCUM, "no    |                  |         |
   |                  | units")          |                  |         |
   +------------------+------------------+------------------+---------+
   | >Quantity        | (0040,9220)      |                  |         |
   | Definition       |                  |                  |         |
   | Sequence         |                  |                  |         |
   +------------------+------------------+------------------+---------+
   | >>CODE           | `(1710001, SCT,  |                  |         |
   | `(105590001,     | "Uric            |                  |         |
   | SCT,             | Acid") <h        |                  |         |
   | "                | ttp://snomed.inf |                  |         |
   | Substance") <htt | o/id/1710001>`__ |                  |         |
   | p://snomed.info/ |                  |                  |         |
   | id/105590001>`__ |                  |                  |         |
   +------------------+------------------+------------------+---------+
   | >>CODE           | (129322, DCM,    |                  |         |
   | `(370129005,     | "Value-based     |                  |         |
   | SCT,             | image")          |                  |         |
   | "Measurement     |                  |                  |         |
   | Method") <htt    |                  |                  |         |
   | p://snomed.info/ |                  |                  |         |
   | id/370129005>`__ |                  |                  |         |
   +------------------+------------------+------------------+---------+
   | ITEM 2           |                  |                  |         |
   +------------------+------------------+------------------+---------+
   | >Real World      | (0040,9216)      | 20               |         |
   | Value First      |                  |                  |         |
   | Value Mapped     |                  |                  |         |
   +------------------+------------------+------------------+---------+
   | >Real World      | (0040,9211)      | 40               |         |
   | Value Last Value |                  |                  |         |
   | Mapped           |                  |                  |         |
   +------------------+------------------+------------------+---------+
   | >Real World      | (0040,9224)      | 0                |         |
   | Value Intercept  |                  |                  |         |
   +------------------+------------------+------------------+---------+
   | >Real World      | (0040,9225)      | 1                |         |
   | Value Slope      |                  |                  |         |
   +------------------+------------------+------------------+---------+
   | >LUT Explanation | (0028,3003)      | "Value-based     |         |
   |                  |                  | substance map    |         |
   |                  |                  | for kidney       |         |
   |                  |                  | stone"           |         |
   +------------------+------------------+------------------+---------+
   | >LUT Label       | (0040,9210)      | MAT\_            |         |
   |                  |                  | VALUE_BASED      |         |
   +------------------+------------------+------------------+---------+
   | >Measurement     | (0040,08EA)      | (1, UCUM, "no    |         |
   | Units Code       |                  | units")          |         |
   | Sequence         |                  |                  |         |
   +------------------+------------------+------------------+---------+
   | >>Include        |                  |                  |         |
   +------------------+------------------+------------------+---------+
   | >Quantity        | (0040,9220)      |                  |         |
   | Definition       |                  |                  |         |
   | Sequence         |                  |                  |         |
   +------------------+------------------+------------------+---------+
   | >>CODE           | `(5540006, SCT,  |                  |         |
   | `(105590001,     | "Calcium") <h    |                  |         |
   | SCT,             | ttp://snomed.inf |                  |         |
   | "                | o/id/5540006>`__ |                  |         |
   | Substance") <htt |                  |                  |         |
   | p://snomed.info/ |                  |                  |         |
   | id/105590001>`__ |                  |                  |         |
   +------------------+------------------+------------------+---------+
   | >>CODE           | (129322, DCM,    |                  |         |
   | `(370129005,     | "Value-based     |                  |         |
   | SCT,             | image")          |                  |         |
   | "Measurement     |                  |                  |         |
   | Method") <htt    |                  |                  |         |
   | p://snomed.info/ |                  |                  |         |
   | id/370129005>`__ |                  |                  |         |
   +------------------+------------------+------------------+---------+

