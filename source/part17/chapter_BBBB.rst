.. _chapter_BBBB:

Color information for Parametric Object (Informative)
=====================================================

.. _sect_BBBB.1:

Introduction
------------

Functional imaging can create Parametric Maps showing a functional
relation between the anatomical region and the specific functional
activity. For display purposes it is useful to show this functional
activity with the use of a color LUT on the related anatomical image. To
be able to do this it is necessary to include a Palette Color Lookup
Table for the Parametric Map and define how to map the (floating point)
values to a specific RGB value.

For a correct mapping it is important to know what range of continuous
values needs to be mapped to the discrete range of RGB values of the
LUT. For this the Minimum Stored Value Mapped (0028,1231) and the
Maximum Stored Value Mapped (0028,1232) are defined. All values between
the minimum and maximum will be distributed in a linear manner to the
Palette Color Lookup Table that is supplied.

The usage of floating point values for the stored values removes the
need for a Real World Value transformation other than the identity
transformation.

This example illustrates BOLD fMRI activation data for a bipolar motor
paradigm stored as a floating point parametric map encoding ‘t’
(statistical) Real World Values. Each voxel’s value represents how well
the BOLD time series information at that location of the brain fits the
general linear model (GLM) of the fMRI block paradigm pattern (right or
left versus control, no movement). Right and left have been encoded as
positive and negative t values, respectively.

The Double Float Minimum Stored Value Mapped and Maximum Stored Value
Mapped in this case are -16.739 and 21.434, respectively. This range
will be mapped to the low and high ends of the LUT applied to this
activation map. In this case the Minimum Stored Value Mapped and Maximum
Stored Value Mapped are equal to the RWV Minimum and Maximum,
respectively, in the activation map data. Note several compelling
reasons for the range to be different from the RWV Minimum and RWV
Maximum:

1. Centering the RWV zero value on some desired index of the LUT; e.g.,
   choosing -21.434 to +21.434 to properly center RWV zero on the middle
   of the LUT (presumably to match the LUT design).

2. Choosing a narrower range of Minimum Stored Value Mapped and/or
   Maximum Stored Value Mapped (negative and/or positive), i.e.,
   windowing, to maximize the dynamic range of the LUT for critical RWV
   range(s).

3. Specifying a predetermined Minimum Stored Value Mapped and Maximum
   Stored Value Mapped regardless of the actual RWV data, in order to
   have key RWV transitions match LUT color effects, e.g., generally
   accepted hyperperfusion and hypoperfusion transition points in
   cerebral blood flow (CBF) maps.

For the purpose of this example, the full RWV range of the activation
map is appropriate to display with the full range of the Spring Color
Palette.

As the activation map without threshold suggests, areas outside the
brain have been masked off. These would be coded with Padding values in
the parametric map.

Thresholding (not part of the parametric map) will be applied for
positive and/or negative ranges. Note that this operation does not
change the color mapping (i.e., RWV x corresponds to LUT entry j) but
only the opacity of voxels outside the range (forcing A=0 or
transparent).

Other visualization methods such as smoothing and overall opacity may be
applied to the colored, thresholded activation map.

.. _sect_BBBB.2:

Encoding Example
----------------

This section illustrates the usage of the Color LUT in the context of a
Parametric Map IOD with the Palette Color Lookup Table for the example
described.

.. table:: Example data for the Floating Point Image Pixel Module

   +-----------------+-------------+-----------------+-----------------+
   | **Attribute**   | **Tag**     | **Value**       | **Comment**     |
   +=================+=============+=================+=================+
   | Samples per     | (0028,0002) | 1               |                 |
   | Pixel           |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Photometric     | (0028,0004) | COLOR_RANGE     |                 |
   | Interpretation  |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Rows            | (0028,0010) | 41              |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Columns         | (0028,0011) | 32              | This case is a  |
   |                 |             |                 | non-square      |
   |                 |             |                 | image           |
   +-----------------+-------------+-----------------+-----------------+
   | Bits Allocated  | (0028,0100) | 32              |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Pixel Aspect    | (0028,0034) | 1\1             |                 |
   | Ratio           |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Float Pixel     | (0028,0122) | -200            |                 |
   | Padding Value   |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Float Pixel     | (0028,0124) | -100            |                 |
   | Padding Range   |             |                 |                 |
   | Limit           |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Float Pixel     | (7FE0,0008) | (44 times)      | For convenience |
   | Data            |             | -150, -0.1356,  | "," is used to  |
   |                 |             | 1.317, (28      | separate the    |
   |                 |             | times) -150,    | values, type is |
   |                 |             | -0.986, 0.4402, | OF              |
   |                 |             | -0.0251,        |                 |
   |                 |             | 0.6077, 0.2982, |                 |
   |                 |             | 0.0872, 2.6927, |                 |
   |                 |             | 2.1434,         |                 |
   |                 |             | -0.5543,        |                 |
   |                 |             | -0.3014, -150   |                 |
   |                 |             | etc.            |                 |
   +-----------------+-------------+-----------------+-----------------+

.. table:: Example data for the Dimension Organization Module

   +-----------------+-----------------+-----------------+-------------+
   | **Attribute**   | **Tag**         | **Value**       | **Comment** |
   +=================+=================+=================+=============+
   | Dimension       | (0020,9221)     |                 |             |
   | Organization    |                 |                 |             |
   | Sequence        |                 |                 |             |
   +-----------------+-----------------+-----------------+-------------+
   | >Dimension      | (0020,9164)     | 1.2.3.5.6       | Sample UID  |
   | Organization    |                 |                 |             |
   | UID             |                 |                 |             |
   +-----------------+-----------------+-----------------+-------------+
   | Dimension       | (0020,9311)     | 3D              |             |
   | Organization    |                 |                 |             |
   | Type            |                 |                 |             |
   +-----------------+-----------------+-----------------+-------------+
   | Dimension Index | (0020,9222)     | 1               |             |
   | Sequence        |                 |                 |             |
   +-----------------+-----------------+-----------------+-------------+
   | Item 1          | First Item      |                 |             |
   |                 | describing      |                 |             |
   |                 | Stack ID        |                 |             |
   +-----------------+-----------------+-----------------+-------------+
   | >Dimension      | (0020,9165)     | (0020,9056)     |             |
   | Index Pointer   |                 |                 |             |
   +-----------------+-----------------+-----------------+-------------+
   | >Functional     | (0020,9167)     | (0020,9111)     |             |
   | Group Pointer   |                 |                 |             |
   +-----------------+-----------------+-----------------+-------------+
   | >Dimension      | (0020,9164)     | 1.2.3.5.6       |             |
   | Organization    |                 |                 |             |
   | UID             |                 |                 |             |
   +-----------------+-----------------+-----------------+-------------+
   | >Dimension      | (0020,9421)     | Stack ID        |             |
   | Description     |                 |                 |             |
   | Label           |                 |                 |             |
   +-----------------+-----------------+-----------------+-------------+
   | Item 2          | Second Item     |                 |             |
   |                 | describing      |                 |             |
   |                 | In-Stack        |                 |             |
   |                 | Position Number |                 |             |
   +-----------------+-----------------+-----------------+-------------+
   | >Dimension      | (0020,9165)     | (0020,9057)     |             |
   | Index Pointer   |                 |                 |             |
   +-----------------+-----------------+-----------------+-------------+
   | >Functional     | (0020,9167)     | (0020,9111)     |             |
   | Group Pointer   |                 |                 |             |
   +-----------------+-----------------+-----------------+-------------+
   | >Dimension      | (0020,9164)     | 1.2.3.5.6       |             |
   | Organization    |                 |                 |             |
   | UID             |                 |                 |             |
   +-----------------+-----------------+-----------------+-------------+
   | >Dimension      | (0020,9421)     | In-Stack        |             |
   | Description     |                 | Position Number |             |
   | Label           |                 |                 |             |
   +-----------------+-----------------+-----------------+-------------+

.. table:: Example data for the Pixel Measures Macro

   ======================= =========== ========= ===========
   **Attribute**           **Tag**     **Value** **Comment**
   ======================= =========== ========= ===========
   Pixel Measures Sequence (0028,9110) 1         
   >Pixel Spacing          (0028,0030) 3.75\3.75 
   >Slice Thickness        (0018,0050) 5         
   ======================= =========== ========= ===========

.. table:: Example data for the Frame Content Macro

   ========================= =========== ========= ===========
   **Attribute**             **Tag**     **Value** **Comment**
   ========================= =========== ========= ===========
   Frame Content Sequence    (0020,9111)           
   >Frame Acquisition Number (0020,9156) 1         
   >Dimension Index Values   (0020,9157) 1\15      
   >Stack ID                 (0020,9056) 1         
   >In-Stack Position Number (0020,9057) 15        
   >Frame Comments           (0020,9158) ...       
   >Frame Label              (0020,9453) ...       
   ========================= =========== ========= ===========

.. table:: Example data for the Identity Pixel Value Transformation
Macro

   +--------------------+-------------+-----------+--------------------+
   | **Attribute**      | **Tag**     | **Value** | **Comment**        |
   +====================+=============+===========+====================+
   | Pixel Value        | (0028,9145) |           | Single item with   |
   | Transformation     |             |           | fixed values       |
   | Sequence           |             |           |                    |
   +--------------------+-------------+-----------+--------------------+
   | >Rescale Intercept | (0028,1052) | 0         |                    |
   +--------------------+-------------+-----------+--------------------+
   | >Rescale Slope     | (0028,1053) | 1         |                    |
   +--------------------+-------------+-----------+--------------------+
   | >Rescale Type      | (0028,1054) | US        |                    |
   +--------------------+-------------+-----------+--------------------+

.. table:: Example data for the Frame VOI LUT With LUT Macro

   ====================== =========== ========= ==================
   **Attribute**          **Tag**     **Value** **Comment**
   ====================== =========== ========= ==================
   Frame VOI LUT Sequence (0028,9132)           
   >Window Center         (0028,1050) 0         
   >Window Width          (0028,1051) 50        Covering -25 to 25
   ====================== =========== ========= ==================

.. table:: Example data for the Real World Value Mapping Macro

   +-----------------+-------------+-----------------+-----------------+
   | **Attribute**   | **Tag**     | **Value**       | **Comment**     |
   +=================+=============+=================+=================+
   | Real World      | (0040,9096) |                 |                 |
   | Value Mapping   |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Double Float   | (0040,9214) | -16.739         |                 |
   | Real World      |             |                 |                 |
   | Value First     |             |                 |                 |
   | Value Mapped    |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Double Float   | (0040,9213) | 21.434          |                 |
   | Real World      |             |                 |                 |
   | Value Last      |             |                 |                 |
   | Value Mapped    |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Real World     | (0040,9224) | 0               | Identity        |
   | Value Intercept |             |                 | transformation  |
   +-----------------+-------------+-----------------+-----------------+
   | >Real World     | (0040,9225) | 1               | Identity        |
   | Value Slope     |             |                 | transformation  |
   +-----------------+-------------+-----------------+-----------------+
   | >Measurement    | (0040,08EA) |                 |                 |
   | Units Code      |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | *>>Include*     |             | (UCUM, {t},     |                 |
   | *Table 8.8-1    |             | "t")            |                 |
   | "Code Sequence  |             |                 |                 |
   | Macro           |             |                 |                 |
   | Attributes"*    |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Quantity       | (0040,9220) |                 |                 |
   | Definition      |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | *>>Include*     |             | (113068, DCM,   |                 |
   | *Table 10-2     |             | "Student's      |                 |
   | "Content Item   |             | T-test")        |                 |
   | Macro           |             |                 |                 |
   | Attributes      |             |                 |                 |
   | Description"*   |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+

The Palette Color Lookup Table used is the Spring Color Palette (see
`figure_title <#figure_BBBB.1-3>`__).

This can be described as follows through the Palette Color Lookup Table:

Red has a constant value of 255

Green has a linear segment that starts at 0 and ends at 255

Blue has a linear segment that starts at 255 and ends at 0

Using the Segmented Color Lookup Table all three can be described by a
discrete segment with length 1 to specify the starting value (0,1,value)
followed by a linear segment of length 255 with the end-value
(1,255,end-value).

.. table:: Example data for the Palette Color Lookup Table Module

   +-----------------+-------------+-----------------+-----------------+
   | **Attribute**   | **Tag**     | **Value**       | **Comment**     |
   +=================+=============+=================+=================+
   | Red Palette     | (0028,1101) | 256\0\8         |                 |
   | Color Lookup    |             |                 |                 |
   | Table           |             |                 |                 |
   | Descriptor      |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Green Palette   | (0028,1102) | 256\0\8         |                 |
   | Color Lookup    |             |                 |                 |
   | Table           |             |                 |                 |
   | Descriptor      |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Blue Palette    | (0028,1103) | 256\0\8         |                 |
   | Color Lookup    |             |                 |                 |
   | Table           |             |                 |                 |
   | Descriptor      |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Segmented Red   | (0028,1221) | 0,              | For convenience |
   | Palette Color   |             | 1,255,1,255,255 | "," is used to  |
   | Lookup Table    |             |                 | separate the    |
   | Data            |             |                 | values, type is |
   |                 |             |                 | OW              |
   +-----------------+-------------+-----------------+-----------------+
   | Segmented Green | (0028,1222) | 0,1,0,1,255,255 | For convenience |
   | Palette Color   |             |                 | "," is used to  |
   | Lookup Table    |             |                 | separate the    |
   | Data            |             |                 | values, type is |
   |                 |             |                 | OW              |
   +-----------------+-------------+-----------------+-----------------+
   | Segmented Blue  | (0028,1223) | 0,1,255,1,255,0 | For convenience |
   | Palette Color   |             |                 | "," is used to  |
   | Lookup Table    |             |                 | separate the    |
   | Data            |             |                 | values, type is |
   |                 |             |                 | OW              |
   +-----------------+-------------+-----------------+-----------------+

The values specifying the range to be mapped to the Color LUT are given
by the Minimum Stored Value Mapped and the Maximum Stored Value mapped.

.. table:: Example data for the Stored Value Color Range Macro

   +--------------------+-------------+-----------+--------------------+
   | **Attribute**      | **Tag**     | **Value** | **Comment**        |
   +====================+=============+===========+====================+
   | Minimum Stored     | (0028,1231) | -16.739   | Corresponds to the |
   | Value Mapped       |             |           | first LUT entry    |
   |                    |             |           | (255,0,255).       |
   +--------------------+-------------+-----------+--------------------+
   | Maximum Stored     | (0028,1232) | 21.434    | Corresponds to the |
   | Value Mapped       |             |           | last LUT entry     |
   |                    |             |           | (255,255,0).       |
   +--------------------+-------------+-----------+--------------------+

.. table:: Example data for the Parametric Map Frame Type Macro

   +-------------------+-------------+-------------------+-------------+
   | **Attribute**     | **Tag**     | **Value**         | **Comment** |
   +===================+=============+===================+=============+
   | Parametric Map    | (0040,9092) |                   |             |
   | Frame Type        |             |                   |             |
   | Sequence          |             |                   |             |
   +-------------------+-------------+-------------------+-------------+
   | >Frame Type       | (0008,9007) | DERIVED\PR        |             |
   |                   |             | IMARY\FMRI\T_TEST |             |
   +-------------------+-------------+-------------------+-------------+

