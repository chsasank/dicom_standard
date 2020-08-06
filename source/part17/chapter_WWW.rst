.. _chapter_WWW:

Tractography Results (Informative)
==================================

.. _sect_WWW.1:

Introduction
------------

MRI diffusion imaging is able to quantify diffusion of water along
certain directions. The diffusion tensor model is a simple model that is
able to describe the statistical diffusion process accurately at most
white matter positions. To calculate diffusion tensors, a base-line MRI
without diffusion-weighting and at least six differently weighted
diffusion MRIs have to be acquired. After some preprocessing of the
data, at each grid point, a diffusion tensor can be calculated. This
gives rise to a tensor volume that is the basis for tracking.
Refinements to the diffusion model and acquisition method such as HARDI,
Q-Ball, diffusion spectrum imaging (DSI) and diffusion kurtosis imaging
(DKI) are expanding the directionality information available beyond the
simple tensor model, enhancing tracking through crossings, adjacent
fibers, sharp turns, and other difficult scenarios.

A tracking algorithm produces tracks (i.e., fibers), which are collected
into track sets. A track contains the set of x, y and z coordinates of
each point making up the track. Depending upon the algorithm and
software used, additional quantities such as Fractional Anisotropy (FA)
values or color etc. may be associated with the data, by track set,
track or point, either to facilitate further filtering or for clinical
use. Descriptive statistics of quantities such as FA may be associated
with the data by track set or track.

Examples of tractography applications include:

-  Visualization of white matter tracks to aid in resection planning or
   to support image guided (neuro) surgery;

-  Determination of proximity and/or displacement versus infiltration of
   white matter by tumor processes;

-  Assessment of white matter health in neurodegenerative disorders,
   both axonal and myelin integrity, through sampling of derived
   diffusion parameters along the white matter tracks.

.. _sect_WWW.2:

Encoding Example
----------------

This section illustrates the usage of the in the context of the
Tractography Results IOD.

`figure_title <#figure_WWW-1>`__ shows two example track sets. The
example consists of:

-  Two track sets "Track Set Left" and "Track Set Right"

   -  Track Set Sequence (0066,0101) => each item describes one track
      set.

-  Track Set "Track Set Left" contains two tracks "A" and "B"

   -  Track Sequence (0066,0102) => each item describes one track.

-  Track "A" consists of:

   -  4 points

      -  Point Coordinates Data (0066,0016) => describes the coordinates
         for all points in the track.

   -  Different color for each point

      -  Recommended Display CIELab Value List (0066,0103) => describes
         the colors for all points in the track.

   -  Fractional Anisotropy for each point

      -  On how the values are stored, see description in "Encoding of
         Measurement Values" below.

   -  Apparent Diffusion Coefficient for point 1 and 3

      -  On how the values are stored, see description in "Encoding of
         Measurement Values" below.

-  Track "B" consists of:

   -  3 points

      -  Point Coordinates Data (0066,0016) => describes the coordinates
         for all points in the track.

   -  Same color for each point

      -  Recommended Display CIELab Value (0062,000D) => describes the
         color for all points in the track.

   -  Fractional Anisotropy for each point

      -  On how the values are stored, see description in "Encoding of
         Measurement Values" below.

   -  Apparent Diffusion Coefficient for point 2

      -  On how the values are stored, see description in "Encoding of
         Measurement Values" below.

-  Encoding of Measurement Values for Tracks "A" and "B"

   -  For storing measurement values like Fractional Anisotropy or
      Apparent Diffusion Coefficient values on specific points on a
      track the overall view over all tracks of a given track set is
      needed. Only tracks shall be grouped in track sets that share a
      specific type of measurement value.

   -  Measurements Sequence (0066,0121) => each item describes one value
      type of all tracks in the track set (here: "Track Set Left"
      contains two value types: Fractional Anisotropy and Apparent
      Diffusion Coefficient).

   -  Measurement Values Sequence (0066,0132) => one item for each track
      of a track set.

      -  When used to store Fractional Anisotropy values:Since a
         Fractional Anisotropy value is stored for each point in both
         tracks of "Track Set Left", Floating Point Values (0066,0125)
         contains an array of Fractional Anisotropy values for tracks
         "A" and "B" respectively. Track Point Index List (0066,0129) is
         absent since there is a Fractional Anisotropy value associated
         with every point in Point Coordinates Data (0066,0016).

      -  When used to store Apparent Diffusion Coefficient values:Since
         an Apparent Diffusion Coefficient value is stored only for a
         subset of points in both tracks of "Track Set Left", Track
         Point Index List (0066,0129) contains indices to the track
         points in Point Coordinates Data (0066,0016) and Floating Point
         Values (0066,0125) contains a measurement value for every track
         point referenced in Track Point Index List (0066,0129).

-  Track Set "Track Set Right" contains one track "C"

-  Track "C" consists of:

   -  3 points

      -  Point Coordinates Data (0066,0016) => describes the coordinates
         for all points in the track.

   -  Same color for all points

      -  Recommended Display CIELab Value (0062,000D) => describes the
         color for all points in the track set (Note: In this example
         this Attribute is stored on Track Set level).

   -  No measurement values

The table WWW-1 shows the encoding of the Tractography Results module
for the example above. In addition to the two example track sets the
table WWW-1 also encodes the following information:

-  Within "Track Set Left" the mean Fractional Anisotropy values for
   track "A" (0.475) and "B" (0.667).

-  For "Track Set Left" the maximum Fractional Anisotropy value (0.9).

-  Diffusion acquisition, model and tracking algorithm information.

-  Image instance references used to define the Tractography Results
   instance.

.. table:: Example of the Tractography Results Module

   +-------------+-------------+-------------+-------------+-------------+
   | **Name**    | **Tag**     | **Value**   | **Comment** |             |
   +=============+=============+=============+=============+=============+
   | Instance    | (0020,0013) | 1           |             |             |
   | Number      |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Content     | (0070,0080) | Left and    |             |             |
   | Label       |             | Right       |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Content     | (0070,0081) | Two Sample  |             |             |
   | Description |             | Tracksets   |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Content     | (0070,0084) | <empty>     | *Type 2     |             |
   | Creator's   |             |             | Attribute*  |             |
   | Name        |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Content     | (0008,0023) | 20150529    |             |             |
   | Date        |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Content     | (0008,0033) | 12          |             |             |
   | Time        |             | 1933.000000 |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Track Set   | (0066,0101) |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   |             | *Item 1     |             |             |             |
   |             | (First      |             |             |             |
   |             | Track Set   |             |             |             |
   |             | "Track Set  |             |             |             |
   |             | Left")*     |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Track Set  | (0066,0105) | 1           |             |             |
   | Number      |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Track Set  | (0066,0106) | Track Set   |             |             |
   | Label       |             | Left        |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Track Set  | (0066,0108) |             |             |             |
   | Anatomical  |             |             |             |             |
   | Type Code   |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Code      | (0008,0100) | `           |             |             |
   | Sequence    |             | (389080008, |             |             |
   | Macro       | (0008,0102) | SCT, "White |             |             |
   | Values      |             | matter of   |             |             |
   |             | (0008,0104) | brain and   |             |             |
   |             |             | spinal      |             |             |
   |             |             | cord") <ht  |             |             |
   |             |             | tp://snomed |             |             |
   |             |             | .info/id/38 |             |             |
   |             |             | 9080008>`__ |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Modifier  | (0040,A195) |             |             |             |
   | Code        |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   |             | *Item 1*    |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>>Code     | …           | `(7771000,  |             |             |
   | Sequence    |             | SCT,        |             |             |
   | Macro       |             | "Left") <   |             |             |
   | Values      |             | http://snom |             |             |
   |             |             | ed.info/id/ |             |             |
   |             |             | 7771000>`__ |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Track      | (0066,0102) |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   |             | *Item 1     |             |             |             |
   |             | (First      |             |             |             |
   |             | Track "A")* |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Point     | (0066,0016) | 0, 0, 0     | Coordinates |             |
   | Coordinates |             |             | of A1, A2,  |             |
   | Data        |             | 1.5, 0.2, 0 | A3, A4      |             |
   |             |             |             |             |             |
   |             |             | 3.5, -0.1,  |             |             |
   |             |             | 0           |             |             |
   |             |             |             |             |             |
   |             |             | 5.5, 0.5, 0 |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>          | (0066,0103) | 47270/4     | Colors of   |             |
   | Recommended |             | 0385/52501/ | A1, A2, A3, |             |
   | Display     |             |             | A4          |             |
   | CIELab      |             | 34751/5     |             |             |
   | Value List  |             | 3214/49924/ |             |             |
   |             |             |             |             |             |
   |             |             | 57318/      |             |             |
   |             |             | 11632/54042 |             |             |
   |             |             |             |             |             |
   |             |             | 22077/      |             |             |
   |             |             | 53113/5901/ |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | *Item 2     |             |             |             |             |
   | (Second     |             |             |             |             |
   | Track "B")* |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Point     | (0066,0016) | 0, -4, 0    | Coordinates |             |
   | Coordinates |             |             | of B1, B2,  |             |
   | Data        |             | 2,-3.8, 0   | B3          |             |
   |             |             |             |             |             |
   |             |             | 4,-4, 0     |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>          | (0062,000D) | 57318/      | Color of    |             |
   | Recommended |             | 11632/54042 | B1, B2, B3  |             |
   | Display     |             |             |             |             |
   | CIELab      |             |             |             |             |
   | Value       |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >M          | (0066,0121) |             |             |             |
   | easurements |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   |             | *Item 1     |             |             |             |
   |             | (Fractional |             |             |             |
   |             | Anisotropy  |             |             |             |
   |             | (FA) values |             |             |             |
   |             | stored on   |             |             |             |
   |             | each        |             |             |             |
   |             | Track)*     |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Concept   | (0040,A043) |             |             |             |
   | Name Code   |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>>Code     | …           | (110808,    |             |             |
   | Sequence    |             | DCM,        |             |             |
   | Macro       |             | "Fractional |             |             |
   | Values      |             | A           |             |             |
   |             |             | nisotropy") |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>          | (0040,08EA) |             |             |             |
   | Measurement |             |             |             |             |
   | Units Code  |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>>Code     | …           | (1, UCUM,   |             |             |
   | Sequence    |             | "no units") |             |             |
   | Macro       |             |             |             |             |
   | Values      |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>          | (0066,0132) |             |             |             |
   | Measurement |             |             |             |             |
   | Values      |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   |             | *Item 1 (FA |             |             |             |
   |             | Values for  |             |             |             |
   |             | each point  |             |             |             |
   |             | on first    |             |             |             |
   |             | Track "A")* |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>>Floating | (0066,0125) | 0.2,        | FA values   |             |
   | Point       |             | 0.4,0.5,0.8 | of A1, A2,  |             |
   | Values      |             |             | A3, A4      |             |
   +-------------+-------------+-------------+-------------+-------------+
   | *Item 2 (FA |             |             |             |             |
   | Values for  |             |             |             |             |
   | each point  |             |             |             |             |
   | on second   |             |             |             |             |
   | Track "B")* |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>>Floating | (0066,0125) | 0.3, 0.8,   | FA values   |             |
   | Point       |             | 0.9         | of B1, B2,  |             |
   | Values      |             |             | B3          |             |
   +-------------+-------------+-------------+-------------+-------------+
   | *Item 2     |             |             |             |             |
   | (Apparent   |             |             |             |             |
   | Diffusion   |             |             |             |             |
   | Coefficient |             |             |             |             |
   | (ADC)       |             |             |             |             |
   | values      |             |             |             |             |
   | stored on   |             |             |             |             |
   | each        |             |             |             |             |
   | Track)*     |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Concept   | (0040,A043) |             |             |             |
   | Name Code   |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>>Code     | …           | (113041,    |             |             |
   | Sequence    |             | DCM,        |             |             |
   | Macro       |             | "Apparent   |             |             |
   | Values      |             | Diffusion   |             |             |
   |             |             | Co          |             |             |
   |             |             | efficient") |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>          | (0040,08EA) |             |             |             |
   | Measurement |             |             |             |             |
   | Units Code  |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>>Code     | …           | (1, UCUM,   |             |             |
   | Sequence    |             | "no units") |             |             |
   | Macro       |             |             |             |             |
   | Values      |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>          | (0066,0132) |             |             |             |
   | Measurement |             |             |             |             |
   | Values      |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   |             | *Item 1     |             |             |             |
   |             | (ADC Values |             |             |             |
   |             | stored on   |             |             |             |
   |             | 1\ st and   |             |             |             |
   |             | 3\ rd point |             |             |             |
   |             | of first    |             |             |             |
   |             | Track "A")* |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   |             | >>>Floating | (0066,0125) | 0.6,0.7     | ADC values  |
   |             | Point       |             |             | of A1 and   |
   |             | Values      |             |             | A3          |
   +-------------+-------------+-------------+-------------+-------------+
   | >>>Track    | (0066,0129) | 1, 3        |             |             |
   | Point Index |             |             |             |             |
   | List        |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | *Item 2     |             |             |             |             |
   | (ADC Values |             |             |             |             |
   | stored on   |             |             |             |             |
   | 2\ nd point |             |             |             |             |
   | of second   |             |             |             |             |
   | Track "B")* |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>>Floating | (0066,0125) | 0.5         | ADC value   |             |
   | Point       |             |             | of B2       |             |
   | Values      |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>>Track    | (0066,0129) | 2           |             |             |
   | Point Index |             |             |             |             |
   | List        |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Track      | (0066,0130) |             | *           |             |
   | Statistics  |             |             | Statistical |             |
   | Sequence    |             |             | values      |             |
   |             |             |             | derived     |             |
   |             |             |             | from each   |             |
   |             |             |             | Track*      |             |
   +-------------+-------------+-------------+-------------+-------------+
   |             | *Item 1     |             |             |             |
   |             | (Mean FA    |             |             |             |
   |             | values for  |             |             |             |
   |             | Tracks "A"  |             |             |             |
   |             | and "B")*   |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Concept   | (0040,A043) |             |             |             |
   | Name Code   |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>>Code     | …           | (110808,    |             |             |
   | Sequence    |             | DCM,        |             |             |
   | Macro       |             | "Fractional |             |             |
   | Values      |             | A           |             |             |
   |             |             | nisotropy") |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Modifier  | (0040,A195) |             |             |             |
   | Code        |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>>Code     | …           | `           | *(part of   |             |
   | Sequence    |             | (373098007, | )*          |             |
   | Macro       |             | SCT,        |             |             |
   | Values      |             | "Mean") <ht |             |             |
   |             |             | tp://snomed |             |             |
   |             |             | .info/id/37 |             |             |
   |             |             | 3098007>`__ |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>          | (0040,08EA) |             |             |             |
   | Measurement |             |             |             |             |
   | Units Code  |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>>Code     | …           | (1, UCUM,   |             |             |
   | Sequence    |             | "no units") |             |             |
   | Macro       |             |             |             |             |
   | Values      |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Floating  | (0066,0125) | 0.475,      |             |             |
   | Point       |             | 0.667       |             |             |
   | Values      |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Track Set  | (0066,0124) |             | *           |             |
   | Statistics  |             |             | Statistical |             |
   | Sequence    |             |             | values      |             |
   |             |             |             | derived     |             |
   |             |             |             | from whole  |             |
   |             |             |             | track set*  |             |
   +-------------+-------------+-------------+-------------+-------------+
   |             | *Item 1     |             |             |             |
   |             | (Maximum FA |             |             |             |
   |             | value of    |             |             |             |
   |             | whole Track |             |             |             |
   |             | Set "Track  |             |             |             |
   |             | Set Left")* |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Concept   | (0040,A043) |             |             |             |
   | Name Code   |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>>Code     | …           | (110808,    |             |             |
   | Sequence    |             | DCM,        |             |             |
   | Macro       |             | "Fractional |             |             |
   | Values      |             | A           |             |             |
   |             |             | nisotropy") |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Modifier  | (0040,A195) |             |             |             |
   | Code        |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>>Code     | …           | `(56851009, | *(part of   |             |
   | Sequence    |             | SCT,        | )*          |             |
   | Macro       |             | "M          |             |             |
   | Values      |             | aximum") <h |             |             |
   |             |             | ttp://snome |             |             |
   |             |             | d.info/id/5 |             |             |
   |             |             | 6851009>`__ |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>          | (0040,08EA) |             |             |             |
   | Measurement |             |             |             |             |
   | Units Code  |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>>Code     | …           | (1, UCUM,   |             |             |
   | Sequence    |             | "no units") |             |             |
   | Macro       |             |             |             |             |
   | Values      |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Floating  | (0040,A161) | 0.9         |             |             |
   | Point Value |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Diffusion  | (0066,0133) |             |             |             |
   | Acquisition |             |             |             |             |
   | Code        |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Code      | …           | (113223,    |             |             |
   | Sequence    |             | DCM, "DTI") |             |             |
   | Macro       |             |             |             |             |
   | Values      |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Diffusion  | (0066,0134) |             |             |             |
   | Model Code  |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Code      | …           | (113231,    |             |             |
   | Sequence    |             | DCM,        |             |             |
   | Macro       |             | "Single     |             |             |
   | Values      |             | Tensor")    |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Tracking   | (0066,0104) |             |             |             |
   | Algorithm   |             |             |             |             |
   | Ide         |             |             |             |             |
   | ntification |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   |             | *Item 1*    |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Algorithm | (0066,002F) |             |             |             |
   | Family Code |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>>Code     | …           | (113211,    |             |             |
   | Sequence    |             | DCM,        |             |             |
   | Macro       |             | "Dete       |             |             |
   | Values      |             | rministic") |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Algorithm | (0066,0036) | Example     |             |             |
   | Name        |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Algorithm | (0066,0031) | 1.0         |             |             |
   | Version     |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | *Item 2     |             |             |             |             |
   | (Second     |             |             |             |             |
   | Track Set   |             |             |             |             |
   | "Track Set  |             |             |             |             |
   | Right")*    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Track Set  | (0066,0105) | 2           |             |             |
   | Number      |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Track Set  | (0066,0106) | Track Set   |             |             |
   | Label       |             | Right       |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Track Set  | (0066,0108) |             |             |             |
   | Anatomical  |             |             |             |             |
   | Type Code   |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Code      | (0008,0102) | `           |             |             |
   | Sequence    |             | (389080008, |             |             |
   | Macro       | (0008,0100) | SCT, "White |             |             |
   | Values      |             | matter of   |             |             |
   |             | (0008,0104) | brain and   |             |             |
   |             |             | spinal      |             |             |
   |             |             | cord") <ht  |             |             |
   |             |             | tp://snomed |             |             |
   |             |             | .info/id/38 |             |             |
   |             |             | 9080008>`__ |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Modifier  | (0040,A195) |             |             |             |
   | Code        |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   |             | *Item 1*    |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>>Code     | …           | `(24028007, |             |             |
   | Sequence    |             | SCT,        |             |             |
   | Macro       |             | "Right") <h |             |             |
   | Values      |             | ttp://snome |             |             |
   |             |             | d.info/id/2 |             |             |
   |             |             | 4028007>`__ |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Track      | (0066,0102) |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   |             | *Item 1     |             |             |             |
   |             | (Single     |             |             |             |
   |             | Track "C")* |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Point     | (0066,0016) | 6, 0.1, 0   | Coordinates |             |
   | Coordinates |             |             | of C1, C2,  |             |
   | Data        |             | 5.8, -2, 0  | C3          |             |
   |             |             |             |             |             |
   |             |             | 6.2, -4.5,  |             |             |
   |             |             | 0           |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | (0062,000D) | 34751/5     | Color of    |             |
   | Recommended |             | 3214/49924/ | C1, C2, C3  |             |
   | Display     |             |             |             |             |
   | CIELab      |             |             |             |             |
   | Value       |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Diffusion  | (0066,0133) |             |             |             |
   | Acquisition |             |             |             |             |
   | Code        |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Code      | …           | (113223,    |             |             |
   | Sequence    |             | DCM, "DTI") |             |             |
   | Macro       |             |             |             |             |
   | Values      |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Diffusion  | (0066,0134) |             |             |             |
   | Model Code  |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Code      | …           | (113231,    |             |             |
   | Sequence    |             | DCM,        |             |             |
   | Macro       |             | "Single     |             |             |
   | Values      |             | Tensor")    |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Tracking   | (0066,0104) |             |             |             |
   | Algorithm   |             |             |             |             |
   | Ide         |             |             |             |             |
   | ntification |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   |             | *Item 1*    |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Algorithm | (0066,002F) |             |             |             |
   | Family Code |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>>Code     | …           | (113211,    |             |             |
   | Sequence    |             | DCM,        |             |             |
   | Macro       |             | "Dete       |             |             |
   | Values      |             | rministic") |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Algorithm | (0066,0036) | Example     |             |             |
   | Name        |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Algorithm | (0066,0031) | 1.0         |             |             |
   | Version     |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Referenced  | (0008,114A) |             |             |             |
   | Instance    |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   |             | *Item 1*    |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Referenced | …           | 1.2         | *MR Image   |             |
   | SOP Class   |             | .840.10008. | Storage*    |             |
   | UID         |             | 5.1.4.1.1.4 |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Referenced | …           | 1.2.3.4.1   |             |             |
   | SOP         |             |             |             |             |
   | Instance    |             |             |             |             |
   | UID         |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | *Item 2*    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Referenced | …           | 1.2         | *MR Image   |             |
   | SOP Class   |             | .840.10008. | Storage*    |             |
   | UID         |             | 5.1.4.1.1.4 |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Referenced | …           | 1.2.3.4.2   |             |             |
   | SOP         |             |             |             |             |
   | Instance    |             |             |             |             |
   | UID         |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | …           |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | *Item n*    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Referenced | …           | 1.2         | *MR Image   |             |
   | SOP Class   |             | .840.10008. | Storage*    |             |
   | UID         |             | 5.1.4.1.1.4 |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Referenced | …           | 1.5.6.1     |             |             |
   | SOP         |             |             |             |             |
   | Instance    |             |             |             |             |
   | UID         |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+

