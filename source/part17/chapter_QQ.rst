.. _chapter_QQ:

Enhanced US Data Type Blending Examples (Informative)
=====================================================

.. _sect_QQ.1:

Enhanced US Volume Use of the Blending and Display Pipeline
-----------------------------------------------------------

This Annex contains a number of examples illustrating Ultrasound's use
of the Blending and Display Pipeline. An overview of the examples
included is found in `table_title <#table_QQ.1-1>`__.

.. table:: Enhanced US Data Type Blending Examples (Informative)

   +----------+----------+----------+----------+----------+----------+
   | **E      | **Data   | **       | **M      | **       | **       |
   | xample** | Types**  | Blending | apping** | Blending | Blending |
   |          |          | RGB      |          | Ope      | Weight   |
   |          |          | Inputs** |          | ration** | Inputs** |
   +==========+==========+==========+==========+==========+==========+
   | 1        | TISSUE_I | NA       | Identity | None     | NA       |
   |          | NTENSITY |          |          |          |          |
   +----------+----------+----------+----------+----------+----------+
   | 2        | TISSUE_I | RGB1 =   | G        | Output = | Weight 1 |
   |          | NTENSITY | g        | rayscale | RGB1     | = 1.0    |
   |          |          | rayscale |          |          | (c       |
   |          |          | TISSUE_I |          |          | onstant) |
   |          |          | NTENSITY |          |          |          |
   +----------+----------+----------+----------+----------+----------+
   | Weight 2 |          |          |          |          |          |
   | = 0.0    |          |          |          |          |          |
   | (c       |          |          |          |          |          |
   | onstant) |          |          |          |          |          |
   +----------+----------+----------+----------+----------+----------+
   | 3        | TISSUE_I | RGB1 =   | C        | Output = | Weight 1 |
   |          | NTENSITY | f(T      | olorized | RGB1     | = 1.0    |
   |          |          | ISSUE_IN |          |          | (c       |
   |          |          | TENSITY) |          |          | onstant) |
   +----------+----------+----------+----------+----------+----------+
   | Weight 2 |          |          |          |          |          |
   | = 0.0    |          |          |          |          |          |
   | (c       |          |          |          |          |          |
   | onstant) |          |          |          |          |          |
   +----------+----------+----------+----------+----------+----------+
   | 4        | TISSUE_I | RGB1 =   | G        | Output = | Weight 1 |
   |          | NTENSITY | g        | rayscale | prop     | =        |
   |          |          | rayscale |          | ortional | constant |
   |          |          | TISSUE_I |          | s        |          |
   |          |          | NTENSITY |          | ummation |          |
   |          |          |          |          | of RGB1  |          |
   |          |          |          |          | and RGB2 |          |
   +----------+----------+----------+----------+----------+----------+
   | FLOW_    | RGB2 =   | C        | Weight 2 |          |          |
   | VELOCITY | g(FLOW_V | olorized | =        |          |          |
   |          | ELOCITY) |          | constant |          |          |
   +----------+----------+----------+----------+----------+----------+
   | 5        | TISSUE_I | RGB1 =   | G        | T        | Weight 1 |
   |          | NTENSITY | g        | rayscale | hreshold | = 1 -    |
   |          |          | rayscale |          | based on | Alpha 2  |
   |          |          | TISSUE_I |          | FLOW_    |          |
   |          |          | NTENSITY |          | VELOCITY |          |
   +----------+----------+----------+----------+----------+----------+
   | FLOW_    | RGB2 =   | C        | Weight 2 |          |          |
   | VELOCITY | g(FLOW_V | olorized | =        |          |          |
   |          | ELOCITY) |          | constant |          |          |
   +----------+----------+----------+----------+----------+----------+
   | 6        | TISSUE_I | RGB1 =   | G        | T        | Weight 1 |
   |          | NTENSITY | g        | rayscale | hreshold | = 1 -    |
   |          |          | rayscale |          | based on | Alpha 2  |
   |          |          | TISSUE_I |          | FLOW_    |          |
   |          |          | NTENSITY |          | VELOCITY |          |
   |          |          |          |          | (MSB)    |          |
   |          |          |          |          | and      |          |
   |          |          |          |          | FLOW_    |          |
   |          |          |          |          | VARIANCE |          |
   |          |          |          |          | (LSB)    |          |
   |          |          |          |          | with     |          |
   |          |          |          |          | 2-dim    |          |
   |          |          |          |          | ensional |          |
   |          |          |          |          | color    |          |
   |          |          |          |          | mapping  |          |
   +----------+----------+----------+----------+----------+----------+
   | FLOW_    | RGB2 =   | C        | Weight 2 |          |          |
   | VELOCITY | g(FLOW_V | olorized | = Alpha  |          |          |
   |          | ELOCITY, |          | 2        |          |          |
   |          | FLOW\_   |          |          |          |          |
   |          | V        |          |          |          |          |
   |          | ARIANCE) |          |          |          |          |
   +----------+----------+----------+----------+----------+----------+
   | FLOW\_   | C        |          |          |          |          |
   | VARIANCE | olorized |          |          |          |          |
   +----------+----------+----------+----------+----------+----------+
   | 7        | TISSUE_I | RGB1 =   | C        | Com      | Weight 1 |
   |          | NTENSITY | f(T      | olorized | bination | = Alpha  |
   |          |          | ISSUE_IN |          | based on | 1        |
   |          |          | TENSITY) |          | all data |          |
   |          |          |          |          | value    |          |
   |          |          |          |          | inputs   |          |
   |          |          |          |          | with     |          |
   |          |          |          |          | c        |          |
   |          |          |          |          | olorized |          |
   |          |          |          |          | tissue   |          |
   |          |          |          |          | and      |          |
   |          |          |          |          | c        |          |
   |          |          |          |          | olorized |          |
   |          |          |          |          | 2-dim    |          |
   |          |          |          |          | ensional |          |
   |          |          |          |          | color    |          |
   |          |          |          |          | mapping  |          |
   |          |          |          |          | of flow  |          |
   |          |          |          |          | and      |          |
   |          |          |          |          | v        |          |
   |          |          |          |          | ariance. |          |
   +----------+----------+----------+----------+----------+----------+
   | FLOW_    | RGB2 =   | C        | Weight 2 |          |          |
   | VELOCITY | g(FLOW_V | olorized | = Alpha  |          |          |
   |          | ELOCITY, |          | 2        |          |          |
   |          | FLOW\_   |          |          |          |          |
   |          | V        |          |          |          |          |
   |          | ARIANCE) |          |          |          |          |
   +----------+----------+----------+----------+----------+----------+
   | FLOW\_   | C        |          |          |          |          |
   | VARIANCE | olorized |          |          |          |          |
   +----------+----------+----------+----------+----------+----------+

In the examples below, the following Attributes are referenced:

-  Data Type (0018,9808)

-  Data Path Assignment (0028,1402)

-  Bits Mapped to Color Lookup Table (0028,1403)

-  Blending LUT 1 Transfer Function (0028,1405)

-  Blending LUT 2 Transfer Function (0028,140D)

-  Blending Weight Constant (0028,1406)

-  RGB LUT Transfer Function (0028,140F)

-  Alpha LUT Transfer Function (0028,1410)

-  Red Palette Color Lookup Table Descriptor (0028,1101)

-  Red Palette Color Lookup Table Data (0028,1201)

-  Green Palette Color Lookup Table Descriptor (0028,1102)

-  Green Palette Color Lookup Table Data (0028,1202)

-  Blue Palette Color Lookup Table Descriptor (0028,1103)

-  Blue Palette Color Lookup Table Data (0028,1203)

-  Alpha Palette Color Lookup Table Descriptor (0028,1104)

-  Alpha Palette Color Lookup Table Data (0028,1204)

.. _sect_QQ.1.1:

Example 1 - Grayscale P-Values Output
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Grayscale pass through for 1 data frame using identity Presentation LUT:

================ ======================== =========
**Data Type**    **Data Path Assignment** **Usage**
================ ======================== =========
TISSUE_INTENSITY PRIMARY_PVALUES          Grayscale
================ ======================== =========

.. _sect_QQ.1.2:

Example 2 - Grayscale-only Color Output
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Grayscale mapping only from 1 data frame:

-  Weight 1:

   -  Blending LUT 1 Transfer Function = CONSTANT

   -  Blending Weight Constant = 1.0

-  Weight 2:

   -  Blending LUT 2 Transfer Function = CONSTANT

   -  Blending Weight Constant = 0.0

-  Primary Palette Color Lookup Table

   -  RGB LUT Transfer Function = EQUAL_RGB

   -  Alpha LUT Transfer Function = not significant with these Blending
      LUT Transfer Function values

-  Secondary Palette Color Lookup Table

   -  <none>

.. note::

   Compared to Example 1, the perceived contrast of the displayed
   grayscale image will likely be different as a consequence of the use
   of PCS-Values as opposed to P-Values unless color management software
   interpreting the PCS-Values attempts to approximate the Grayscale
   Standard Display Function. This is true regardless of whether a color
   or grayscale display is used.

================ ======================== ===================
**Data Type**    **Data Path Assignment** **Usage**
================ ======================== ===================
TISSUE_INTENSITY PRIMARY_SINGLE           Mapped to Grayscale
================ ======================== ===================

.. _sect_QQ.1.3:

Example 3 - Color Tissue (Pseudo-color) Mapping
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Grayscale mapping only from 1 data frame:

-  Weight 1:

   -  Blending LUT 1 Transfer Function = CONSTANT

   -  Blending Weight Constant = 1.0

-  Weight 2:

   -  Blending LUT 2 Transfer Function = CONSTANT

   -  Blending Weight Constant = 0.0

-  Primary Palette Color Lookup Table

   -  RGB LUT Transfer Function = TABLE

   -  Alpha LUT Transfer Function = not significant with these Blending
      LUT Transfer Function values

   -  Red, Green, and Blue Palette Color Lookup Table Descriptors and
      Data included

-  Secondary Palette Color Lookup Table

   -  <none>

+------------------+------------------------+------------------------+
| **Data Type**    | **Data Path            | **Usage**              |
|                  | Assignment**           |                        |
+==================+========================+========================+
| TISSUE_INTENSITY | PRIMARY_SINGLE         | Mapped through Palette |
|                  |                        | Color Lookup Table     |
+------------------+------------------------+------------------------+

.. _sect_QQ.1.4:

Example 4 - Fixed Proportion Additive Grayscale Tissue and Color Flow
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Grayscale mapping from primary data frame and color mapping from
secondary data frame:

-  Weight 1:

   -  Blending LUT 1 Transfer Function = CONSTANT

   -  Blending Weight Constant = value between 0.0 and 1.0, inclusive

-  Weight 2:

   -  Blending LUT 2 Transfer Function = CONSTANT

   -  Blending Weight Constant = value between 0.0 and 1.0, inclusive

-  Primary Palette Color Lookup Table

   -  RGB LUT Transfer Function = EQUAL_RGB

   -  Alpha LUT Transfer Function = not significant with these Blending
      LUT Transfer Function values

-  Secondary Palette Color Lookup Table

   -  RGB LUT Transfer Function = TABLE

   -  Alpha LUT Transfer Function = not significant with these Blending
      LUT Transfer Function values

   -  Red, Green, and Blue Palette Color Lookup Table Descriptors and
      Data included

+------------------+------------------------+------------------------+
| **Data Type**    | **Data Path            | **Usage**              |
|                  | Assignment**           |                        |
+==================+========================+========================+
| TISSUE_INTENSITY | PRIMARY_SINGLE         | Mapped to Grayscale    |
+------------------+------------------------+------------------------+
| FLOW_VELOCITY    | SECONDARY_SINGLE       | Mapped through Palette |
|                  |                        | Color Lookup Table     |
+------------------+------------------------+------------------------+

.. _sect_QQ.1.5:

Example 5 - Threshold Based On Flow_velocity
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Each output value is either the grayscale tissue intensity value or the
colorized flow velocity value based on the magnitude of the flow
velocity sample value:

-  Weight 1:

   -  Blending LUT 1 Transfer Function = ALPHA_2

-  Weight 2:

   -  Blending LUT 2 Transfer Function = ONE_MINUS

-  Primary Palette Color Lookup Table

   -  RGB LUT Transfer Function = EQUAL_RGB

   -  Alpha LUT Transfer Function = not significant with these Blending
      LUT Transfer Function values

-  Secondary Palette Color Lookup Table

   -  RGB LUT Transfer Function = TABLE

   -  Alpha LUT Transfer Function = TABLE

   -  Red, Green, Blue, and Alpha Palette Color Lookup Table Descriptors
      and Data included

   -  All Alpha Palette Color Lookup Table Data values (normalized) are
      either 0.0 or 1.0

+------------------+------------------------+------------------------+
| **Data Type**    | **Data Path            | **Usage**              |
|                  | Assignment**           |                        |
+==================+========================+========================+
| TISSUE_INTENSITY | PRIMARY_SINGLE         | Mapped to Grayscale    |
+------------------+------------------------+------------------------+
| FLOW_VELOCITY    | SECONDARY_SINGLE       | Mapped through Palette |
|                  |                        | Color Lookup Table     |
+------------------+------------------------+------------------------+

.. _sect_QQ.1.6:

Example 6 - Threshold Based On Flow_velocity and Flow_variance W/2d Color Mapping
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Each output value is either the grayscale tissue intensity value or a
colorized flow/variance value determined by a 2-dimensional Secondary
RGB Palette Color Lookup Table, based on flow/variance values. The
colorized flow/variance value comes from a 2-dimensional Secondary RGB
Palette Color LUT:

-  Weight 1:

   -  Blending LUT 1 Transfer Function = ALPHA_2

-  Weight 2:

   -  Blending LUT 2 Transfer Function = ONE_MINUS

-  Primary Palette Color Lookup Table

   -  RGB LUT Transfer Function = EQUAL_RGB

   -  Alpha LUT Transfer Function = not significant with these Blending
      LUT Transfer Function values

-  Secondary Palette Color Lookup Table

   -  RGB LUT Transfer Function = TABLE

   -  Alpha LUT Transfer Function = TABLE

   -  Red, Green, Blue, and Alpha Palette Color Lookup Table Descriptors
      and Data included

   -  All Alpha Palette Color Lookup Table Data values (normalized) are
      either 0.0 or 1.0

+------------------+------------------------+------------------------+
| **Data Type**    | **Data Path            | **Usage**              |
|                  | Assignment**           |                        |
+==================+========================+========================+
| TISSUE_INTENSITY | PRIMARY_SINGLE         | Mapped to Grayscale    |
+------------------+------------------------+------------------------+
| FLOW_VELOCITY    | SECONDARY_HIGH         | MSBs of index to       |
|                  |                        | Palette Color LUT      |
+------------------+------------------------+------------------------+
| FLOW_VARIANCE    | SECONDARY_LOW          | LSBs of index to       |
|                  |                        | Palette Color LUT      |
+------------------+------------------------+------------------------+

.. _sect_QQ.1.7:

Example 7 - Color Tissue / Velocity / Variance Mapping - Blending Considers Both Data Paths
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Each output value is a combination of colorized tissue intensity and a
colorized flow/variance value determined by a 2-dimensional Secondary
RGB Palette Color Lookup Table using the upper 5 bits of the
FLOW_VELOCITY value and upper 3 bits of the FLOW_VARIANCE value to allow
the use of 256-value Secondary Palette Color Lookup Tables. The blending
proportion is based on values from both data paths. If the sum of the
two RGB values exceeds 1.0, the value is clamped to 1.0. The colorized
flow/variance value comes from a 2-dimensional Secondary RGB Palette
Color LUT:

-  Weight 1:

   -  Blending LUT 1 Transfer Function = ALPHA_1

-  Weight 2:

   -  Blending LUT 2 Transfer Function = ALPHA_2

-  Primary Palette Color Lookup Table

   -  RGB LUT Transfer Function = TABLE

   -  Alpha LUT Transfer Function = TABLE

   -  Red, Green, Blue, and Alpha Palette Color Lookup Table Descriptors
      and Data included

-  Secondary Palette Color Lookup Table

   -  RGB LUT Transfer Function = TABLE

   -  Alpha LUT Transfer Function = TABLE

   -  Red, Green, Blue, and Alpha Palette Color Lookup Table Descriptors
      and Data included

+----------------+----------------+----------------+----------------+
| **Data Type**  | **Data Path    | **Bits Mapped  | **Usage**      |
|                | Assignment**   | To Color       |                |
|                |                | Lookup Table** |                |
+================+================+================+================+
| TI             | PRIMARY_SINGLE | 8              | Mapped through |
| SSUE_INTENSITY |                |                | Palette Color  |
|                |                |                | Lookup Table   |
+----------------+----------------+----------------+----------------+
| FLOW_VELOCITY  | SECONDARY_HIGH | 5              | MSBs of index  |
|                |                |                | to Palette     |
|                |                |                | Color LUT      |
+----------------+----------------+----------------+----------------+
| FLOW_VARIANCE  | SECONDARY_LOW  | 3              | LSBs of index  |
|                |                |                | to Palette     |
|                |                |                | Color LUT      |
+----------------+----------------+----------------+----------------+

