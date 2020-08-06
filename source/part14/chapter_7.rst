.. _chapter_7:

The Grayscale Standard Display Function
=======================================

As explained in greater detail in `Derivation of the Grayscale Standard
Display Function (Informative) <#chapter_A>`__, the Grayscale Standard
Display Function is based on human Contrast Sensitivity. Human Contrast
Sensitivity is distinctly non-linear within the Luminance Range of the
Grayscale Standard Display Function . The human eye is relatively less
sensitive in the dark areas of an image than it is in the bright areas
of an image. This variation in sensitivity makes it much easier to see
small relative changes in Luminance in the bright areas of the image
than in the dark areas of the image. A Display Function that adjusts the
brightness such that equal changes in P-Values will result in the same
level of perceptibility at all driving levels is "perceptually
linearized". The Grayscale Standard Display Function incorporates the
notion of perceptual linearization without making it an explicit
objective of PS3.14.

The employed data for Contrast Sensitivity are derived from Barten's
model of the human visual system (Ref. 1, 2 and `Table of the Grayscale
Standard Display Function (Informative) <#chapter_B>`__). Specifically,
the Grayscale Standard Display Function refers to Contrast Sensitivity
for the Standard Target consisting of a 2-deg x 2-deg square filled with
a horizontal or vertical grating with sinusoidal modulation of 4 cycles
per degree. The square is placed in a uniform background of Luminance
equal to the mean Luminance L of the Target. The Contrast Sensitivity is
defined by the Threshold Modulation at which the grating becomes just
visible to the average human observer. The Luminance modulation
represents the Just-Noticeable Difference (JND) for the Target at the
Luminance L.

.. note::

   The academic nature of the Standard Target is recognized. With the
   simple target, the essential objectives of PS3.14 appear to be
   realizable. Only spurious results with more realistic targets in
   complex surroundings were known at the time of writing PS3.14 and
   these were not assessed.

The Grayscale Standard Display Function is defined for the Luminance
Range from 0.05 to 4000 cd/m\ :sup:`2`. The minimum Luminance
corresponds to the lowest practically useful Luminance of
cathode-ray-tube (CRT) monitors and the maximum exceeds the unattenuated
Luminance of very bright light-boxes used for interpreting X-Ray
mammography. The Grayscale Standard Display Function explicitly includes
the effects of the diffused ambient Illuminance.

Within the Luminance Range happen to fall 1023 JNDs (see `Derivation of
the Grayscale Standard Display Function (Informative) <#chapter_A>`__).

.. _sect_7.1:

General Formulas
----------------

The Grayscale Standard Display Function is defined by a mathematical
interpolation of the 1023 Luminance levels derived from Barten's model.
The Grayscale Standard Display Function allows us to calculate
luminance, L, in candelas per square meter, as a function of the
Just-Noticeable Difference (JND) Index, j:

with:

-  Ln referring to the natural logarithm

-  j the index (1 to 1023) of the Luminance levels L\ :sub:`j` of the
   JNDs

-  a = -1.3011877

-  b = -2.5840191E-2

-  c = 8.0242636E-2

-  d = -1.0320229E-1

-  e = 1.3646699E-1

-  f = 2.8745620E-2

-  g = -2.5468404E-2

-  h = -3.1978977E-3

-  k = 1.2992634E-4

-  m = 1.3635334E-3

The logarithms to the base 10 of the Luminance L\ :sub:`j` are very well
interpolated by this function over the entire Luminance Range. The
relative deviation of any log(Luminance) -value from the function is at
most 0.3%, and the root-mean-square-error is 0.0003. The continuous
representation of the Grayscale Standard Display Function permits a user
to compute discrete JNDs for arbitrary start levels and over any desired
Luminance Range.

.. note::

   1. To apply `equation_title <#equation_7-1>`__ to a device with a
      specific range of L values, it is convenient to also have the
      inverse of this relationship, which is given by:

      where:

      -  Log\ :sub:`10` represents logarithm to the base 10

      -  A = 71.498068

      -  B = 94.593053

      -  C = 41.912053

      -  D = 9.8247004

      -  E = 0.28175407

      -  F = -1.1878455

      -  G = -0.18014349

      -  H = 0.14710899

      -  I = - 0.017046845

   2. When incorporating the formulas for L(j) and j(L) into a computer
      program, the use of double precision is recommended.

   3. Alternative methods may be used to calculate the JND Index values.
      One method is use a numerical algorithm such as the Van
      Vijngaarden-Dekker-Brent method described in *Numerical Recipes in
      C*\ (Cambridge University press, 1991). The value j may be
      calculated from L iteratively given the Grayscale Standard Display
      Function's formula for L(j). Another method would be to use the
      Grayscale Standard Display Function's tabulated values of j and L
      to calculate the j corresponding to an arbitrary L by linearly
      interpolating between the two nearest tabulated L,j pairs.

   4. No specification is intended as to how these formulas are
      implemented. These could be implemented dynamically, by executing
      the equation directly, or through discrete values, such as a LUT,
      etc.

`Table of the Grayscale Standard Display Function
(Informative) <#chapter_B>`__ lists the Luminance levels computed with
this equation for the 1023 integer JND Indices and
`figure_title <#figure_7-1>`__ shows a plot of the Grayscale Standard
Display Function. The exact value of the Luminance levels, of course,
depends on the start level of 0.05 cd/m :sup:`2`.

The Characteristic Curve of a Display System represents the Luminance
produced by a Display System as a function of DDL and the effect of
ambient Illuminance. The Characteristic Curve is measured with Standard
Test Patterns (see `Illustrations for Achieving Conformance with the
Grayscale Standard Display Function (Informative) <#chapter_D>`__). In
general, the Display Function describes, for example,

a. the Luminance (including ambient Illuminance) measured as a function
   of DDL for emissive displays such as a CRT-monitor/digital display
   controller system,

b. the Luminance (including ambient Illuminance) as a function of DDL
   measured for a transmissive medium hung in front of a light-box after
   a printer produced an optical density, depending on DDL, on the
   medium,

c. the Luminance (including ambient light) as a function of DDL measured
   for a diffusely reflective medium illuminated by a office lights
   after a printer produced a reflective density, depending on DDL, on
   the medium.

By internal or external means, the system may have been configured (or
calibrated) such that the Characteristic Curve is consistent with the
Grayscale Standard Display Function.

Some Display Systems adapt themselves to ambient light conditions. Such
a system may conform to the Grayscale Standard Display Function for one
level of ambient Illuminance only, unless it had the capability of
adjusting its Display Function without user-intervention so that it
remains in conformance with the Grayscale Standard Display Function.

.. _sect_7.2:

Transmissive Hardcopy Printers
------------------------------

For transmissive hardcopy printing, the relationship between luminance,
L, and the printed optical density, D, is:

where:

-  L\ :sub:`0` is the luminance of the light box with no film present

-  L\ :sub:`a` is the luminance contribution due to ambient illuminance
   reflected off the film

If film is to be printed with a density ranging from D\ :sub:`min` to
D\ :sub:`max`, the final luminance will range between and and the j
values will correspondingly range from j\ :sub:`min` = j(Lmin) to
j\ :sub:`max` = j(L\ :sub:`max`).

If this span of j values is represented by an N-bit P-Value, ranging
from 0 for j\ :sub:`min` to 2N-1 for j\ :sub:`max`, the j values will
correspond to P-Values as follows:

and the corresponding L values will be L(j(p)).

Finally, converting the L(j(p)) values to densities results in:

.. note::

   Typical values for the parameters used in transmissive hardcopy
   printing are L\ :sub:`0` = 2000 cd/m\ :sup:`2`, L\ :sub:`a` = 10
   cd/m\ :sup:`2`.

.. _sect_7.3:

Reflective Hardcopy Printers
----------------------------

For reflective hardcopy printing, the relationship between luminance, L,
and the printed optical density, D, is:

where:

-  L\ :sub:`0` is the maximum luminance obtainable from diffuse
   reflection of the illumination that is present.

If film is to be printed with a density ranging from D\ :sub:`min` to
D\ :sub:`max`, the final luminance will range between and and the j
values will correspondingly range from j\ :sub:`min` = j(Lmin) to
j\ :sub:`max` = j(L\ :sub:`max`).

If this span of j values is represented by an N-bit P-Value, ranging
from 0 for j\ :sub:`min` to 2N-1 for j\ :sub:`max`, the j values will
correspond to P-Values as follows:

and the corresponding L values will be L(j(p)).

Finally, converting the L(j(p)) values to densities results in

.. note::

   Typical values for the parameters used in reflective hardcopy
   printing are L\ :sub:`0` = 150 cd/m\ :sup:`2`.

