.. _chapter_D:

Illustrations for Achieving Conformance with the Grayscale Standard Display Function (Informative)
==================================================================================================

The following sections illustrate how conformance with the Grayscale
Standard Display Function may be achieved for emissive (soft-copy)
Display Systems as well as systems producing image presentations
(hard-copies) on transmissive and reflective media. Each section
contains four sub-sections on 1) a procedure for measuring the system
Characteristic Curve, 2) the application of the Grayscale Standard
Display Function to the Luminance Range of the Display System, 3) the
implementation of the Grayscale Standard Display Function, and 4) the
application of the conformance metrics as proposed in `Measuring the
Accuracy With Which a Display System Matches the Grayscale Standard
Display Function (Informative) <#chapter_C>`__.

It is emphasized that there are different ways to configure a Display
System or to change its performance so that it conforms to the Grayscale
Standard Display Function. In fact, conceivably, a Display System may
calibrate itself automatically to maintain conformance with the
Standard. Hence, the following three illustrations are truly only
examples.

Luminance of any Display System, hard-copy or softcopy, may be measured
with a photometer. The photometer should have the following
characteristics:

-  be accurate to within 3% or less of the absolute Luminance level
   across its full range of operation;

-  have a relative accuracy of at least two times the least significant
   digit at any Luminance level in its range of operation;

-  maintain this accuracy at Luminance levels that are one-tenth of the
   minimum measured Luminance of the Display System;

-  have an acceptance angle that is small enough to incorporate only the
   measurement field without overlapping the surrounding background.

.. note::

   The photometer may be of the type that attaches directly to the
   display face (with a suction cup) or of the type that is held away
   from the display face. If of the latter type, the photometer should
   be well baffled to exclude extraneous light sources, including light
   from the background area of the test pattern.

For a film Display System the photometer may be appropriately used to
measure the background Illuminance and the Luminance of the light-box on
which the film will be displayed. The Luminance characteristics of the
film Display System may be measured directly with the photometer or
indirectly using measured optical density of the film and the values for
the measured background Illuminance and the light-box Luminance.

.. _sect_D.1:

Emissive Display Systems
------------------------

.. _sect_D.1.1:

Measuring the System Characteristic Curve
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Before the characteristic Luminance response of the emissive Display
System is measured, it is allowed to warm up as recommended by the
manufacturer and is adjusted such that it conforms to the manufacturer's
performance specifications. In particular, adjustment procedures for
setting the black and white levels of the display should be obtained
from the Display System manufacturer. The goal is to maximize the
dynamic Luminance Range of the display without introducing artifacts,
resulting in the highest possible number of Just-Noticeable Differences
(JNDs).

.. note::

   A simple test that the system is set up properly can be performed by
   viewing the 5% and 95% squares in the SMPTE pattern. The perceived
   contrast between the 5% square and its 0% surrounding should be equal
   to the perceived contrast between the 95% square and a white square.

Measurement of the Characteristic Curve of the Display System may be
accomplished using a test pattern (`figure_title <#figure_D.1-1>`__)
consisting of:

-  a square measurement field comprising 10% of the total number of
   pixels displayed by the system positioned in the center of the
   display;

-  a full-screen uniform background of 20% of maximum Luminance
   surrounding the target.

.. note::

   With a measurement field of 10% of the total number of displayed
   pixels and a surrounding set to 20% of maximum Luminance, internal
   light scatter in the monitor causes the Luminance Range to be
   typically comparable to that found in radiographs, such as a thorax
   radiograph, when displayed on the CRT monitor.

.. note::

   1. For example, on a 5-megapixel Display System with a matrix of 2048
      by 2560 pixels, the target would be a square with 724 pixels on
      each side.

   2. Ideally, the test pattern should fill the entire screen. Under
      certain windowed operating environments, it may be difficult to
      eliminate certain user-interface objects from the display, in
      particular, menu bars at the top of the screen. In this case, the
      background should fill as much of the screen as possible.

The Characteristic Curve of the Display System may be determined by

-  turning off all ambient lighting (necessary only when a suction cup
   photometer is used or when a handheld photometer casts a shadow on
   the display screen);

-  displaying the above test pattern;

-  setting the DDL for the measurement field to a sequence of different
   values, starting with 0 and increasing at each step until the maximum
   DDL is reached;

-  using a photometer to measure and record the Luminance of the
   measurement field at each command value.

As discussed in `Measuring the Accuracy With Which a Display System
Matches the Grayscale Standard Display Function
(Informative) <#chapter_C>`__, the number and distribution of DDLs at
which measurements are taken must be sufficient to accurately model the
Characteristic Curve of the Display System over the entire Luminance
Range.

.. note::

   1. If a handheld photometer is used, it should be placed at a
      distance from the display screen so that Luminance is measured in
      the center of the measurement field, without overlapping the
      surrounding background. This distance can be calculated using the
      acceptance angle specification provided by the photometer
      manufacturer.

   2. The exact number and distribution of DDLs should be based both on
      the characteristics of the Display System and on the mathematical
      technique used to interpolate the Characteristic Curve of the
      system. It is recommended that at least 64 different command
      values be used in the procedure.

   3. Successive Luminance measurements should be spaced in time such
      that the Display System always reaches a steady state. It may be
      particularly important to allow the system to settle before taking
      the initial measurement at DDL 0.

As stated in the normative section, the effect of ambient light on the
apparent Characteristic Curve must always be included when configuring a
Display System to conform with the Grayscale Standard Display Function.

If a handheld photometer that does not cast a shadow on the display
screen is used to measure the Characteristic Curve, then the Luminance
produced by the display plus the effect of ambient light may be measured
simultaneously.

When a suction cup photometer is used to take the Luminance measurements
or when a handheld photometer casts a shadow on the display screen, all
ambient lighting should be turned off while measuring the Characteristic
Curve. The effect of ambient light is determined separately: The Display
System is turned off, the ambient light is turned on, and the Luminance
produced by scattering of ambient light at the display screen is
measured by placing the photometer at a distance from the display screen
so that its acceptance angle includes a major portion of the screen and
that the measurement is not affected by direct illumination from areas
outside the display screen. The Luminance related to ambient light is
added to the previously measured Luminance levels produced by the
Display System to determine the effective Characteristic Curve of the
system.

.. note::

   Changes in ambient lighting conditions may require recalibration of
   the display subsystem in order to maintain conformance to this
   Standard.

In the following, an example for measurements and transformation of a
Display Function is presented. The Display System for this example is a
CRT monitor with display controller. It is assumed that the display
controller allows a transformation of the DDLs with 8-bit input
precision and 10-bit output precision.

The Luminance is measured with a photometer with a narrow (1°)
acceptance angle. The ambient light level was adjusted as low as
possible. No localized highlights were visible.

1. The maximum Luminance was measured when setting the DDL for the
   measurement field to the value that yielded the highest Luminance and
   the DDL of the surrounding to the middle DDL range. From this
   measurement, the Luminance - 20% of the maximum Luminance - for the
   surrounding of the measurement field was calculated.

2. The ambient light was turned off. With the photometer centered on the
   measurement field of the test pattern of
   `figure_title <#figure_D.1-1>`__, the Luminance was measured when
   varying the input level D\ :sub:`m` in increments of 1 from 0 to 255.
   The transformation operator of the hypothetical display controller
   linearly mapped 8 bits on the input to 10 bits on the output. The
   measured data represent the Characteristic Curve L = F(D\ :sub:`m`)
   for the given operating conditions and this test pattern.

3. Next, the CRT was turned off and the ambient light turned on. The
   photometer was placed on the center axis of the CRT sufficiently far
   away so that it did not cast a shadow on the CRT face and its
   aperture intercepted light scattered from a major portion of the CRT
   face. The measured Luminance of 0.3 cd/m\ :sup:`2`\ produced by the
   ambient light on the CRT face was added to the measured Luminance
   values of the Characteristic Curve without ambient light. The result
   is listed in `table_title <#table_D.1-1>`__ and plotted in
   `figure_title <#figure_D.1-2>`__.

.. table:: Measured Characteristic Curve plus Ambient Light

   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | *      | *      |   | *      | *      |   | *      | *      |   | *      | *      |
   | *DDL** | *Lumin |   | *DDL** | *Lumin |   | *DDL** | *Lumin |   | *DDL** | *Lumin |
   |        | ance** |   |        | ance** |   |        | ance** |   |        | ance** |
   +========+========+===+========+========+===+========+========+===+========+========+
   | 0      | 0.305  |   | 1      | 0.305  |   | 2      | 0.305  |   | 3      | 0.305  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 4      | 0.305  |   | 5      | 0.305  |   | 6      | 0.305  |   | 7      | 0.305  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 8      | 0.305  |   | 9      | 0.305  |   | 10     | 0.305  |   | 11     | 0.307  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 12     | 0.307  |   | 13     | 0.307  |   | 14     | 0.307  |   | 15     | 0.307  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 16     | 0.307  |   | 17     | 0.307  |   | 18     | 0.307  |   | 19     | 0.307  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 20     | 0.307  |   | 21     | 0.307  |   | 22     | 0.310  |   | 23     | 0.310  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 24     | 0.310  |   | 25     | 0.310  |   | 26     | 0.310  |   | 27     | 0.320  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 28     | 0.320  |   | 29     | 0.320  |   | 30     | 0.330  |   | 31     | 0.330  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 32     | 0.340  |   | 33     | 0.350  |   | 34     | 0.360  |   | 35     | 0.370  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 36     | 0.380  |   | 37     | 0.392  |   | 38     | 0.410  |   | 39     | 0.424  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 40     | 0.442  |   | 41     | 0.464  |   | 42     | 0.486  |   | 43     | 0.512  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 44     | 0.534  |   | 45     | 0.562  |   | 46     | 0.594  |   | 47     | 0.626  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 48     | 0.674  |   | 49     | 0.710  |   | 50     | 0.750  |   | 51     | 0.796  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 52     | 0.842  |   | 53     | 0.888  |   | 54     | 0.938  |   | 55     | 0.994  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 56     | 1.048  |   | 57     | 1.108  |   | 58     | 1.168  |   | 59     | 1.232  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 60     | 1.294  |   | 61     | 1.366  |   | 62     | 1.438  |   | 63     | 1.512  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 64     | 1.620  |   | 65     | 1.702  |   | 66     | 1.788  |   | 67     | 1.876  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 68     | 1.960  |   | 69     | 2.056  |   | 70     | 2.154  |   | 71     | 2.248  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 72     | 2.350  |   | 73     | 2.456  |   | 74     | 2.564  |   | 75     | 2.670  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 76     | 2.790  |   | 77     | 2.908  |   | 78     | 3.022  |   | 79     | 3.146  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 80     | 3.328  |   | 81     | 3.460  |   | 82     | 3.584  |   | 83     | 3.732  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 84     | 3.870  |   | 85     | 4.006  |   | 86     | 4.156  |   | 87     | 4.310  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 88     | 4.456  |   | 89     | 4.608  |   | 90     | 4.766  |   | 91     | 4.944  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 92     | 5.104  |   | 93     | 5.268  |   | 94     | 5.444  |   | 95     | 5.630  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 96     | 5.864  |   | 97     | 6.050  |   | 98     | 6.238  |   | 99     | 6.438  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 100    | 6.610  |   | 101    | 6.820  |   | 102    | 7.024  |   | 103    | 7.224  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 104    | 7.428  |   | 105    | 7.644  |   | 106    | 7.872  |   | 107    | 8.066  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 108    | 8.298  |   | 109    | 8.528  |   | 110    | 8.752  |   | 111    | 8.982  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 112    | 9.330  |   | 113    | 9.574  |   | 114    | 9.796  |   | 115    | 10.060 |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 116    | 10.314 |   | 117    | 10.560 |   | 118    | 10.820 |   | 119    | 11.080 |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 120    | 11.340 |   | 121    | 11.620 |   | 122    | 11.880 |   | 123    | 12.180 |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 124    | 12.460 |   | 125    | 12.700 |   | 126    | 13.020 |   | 127    | 13.300 |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 128    | 13.720 |   | 129    | 14.020 |   | 130    | 14.360 |   | 131    | 14.640 |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 132    | 14.940 |   | 133    | 15.300 |   | 134    | 15.600 |   | 135    | 15.900 |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 136    | 16.240 |   | 137    | 16.560 |   | 138    | 16.920 |   | 139    | 17.220 |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 140    | 17.600 |   | 141    | 17.940 |   | 142    | 18.240 |   | 143    | 18.640 |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 144    | 19.120 |   | 145    | 19.460 |   | 146    | 19.800 |   | 147    | 20.260 |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 148    | 20.560 |   | 149    | 20.920 |   | 150    | 21.360 |   | 151    | 21.760 |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 152    | 22.060 |   | 153    | 22.520 |   | 154    | 22.960 |   | 155    | 23.300 |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 156    | 23.700 |   | 157    | 24.080 |   | 158    | 24.600 |   | 159    | 24.980 |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 160    | 25.520 |   | 161    | 26.040 |   | 162    | 26.480 |   | 163    | 26.700 |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 164    | 27.380 |   | 165    | 27.620 |   | 166    | 28.040 |   | 167    | 28.580 |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 168    | 28.980 |   | 169    | 29.400 |   | 170    | 29.840 |   | 171    | 30.540 |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 172    | 30.800 |   | 173    | 31.380 |   | 174    | 31.880 |   | 175    | 32.400 |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 176    | 33.060 |   | 177    | 33.400 |   | 178    | 34.040 |   | 179    | 34.400 |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 180    | 34.840 |   | 181    | 35.360 |   | 182    | 35.900 |   | 183    | 36.400 |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 184    | 37.060 |   | 185    | 37.400 |   | 186    | 38.300 |   | 187    | 38.420 |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 188    | 39.160 |   | 189    | 39.760 |   | 190    | 39.980 |   | 191    | 40.840 |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 192    | 41.540 |   | 193    | 41.900 |   | 194    | 42.800 |   | 195    | 43.060 |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 196    | 43.620 |   | 197    | 44.520 |   | 198    | 44.620 |   | 199    | 45.500 |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 200    | 46.100 |   | 201    | 46.380 |   | 202    | 47.400 |   | 203    | 47.600 |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 204    | 48.320 |   | 205    | 49.060 |   | 206    | 49.380 |   | 207    | 50.320 |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 208    | 50.920 |   | 209    | 51.600 |   | 210    | 52.420 |   | 211    | 52.680 |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 212    | 53.520 |   | 213    | 54.220 |   | 214    | 54.620 |   | 215    | 55.420 |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 216    | 56.100 |   | 217    | 56.600 |   | 218    | 57.400 |   | 219    | 57.820 |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 220    | 58.660 |   | 221    | 59.320 |   | 222    | 59.800 |   | 223    | 60.720 |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 224    | 61.520 |   | 225    | 62.240 |   | 226    | 63.040 |   | 227    | 63.480 |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 228    | 64.460 |   | 229    | 65.020 |   | 230    | 65.500 |   | 231    | 66.500 |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 232    | 66.960 |   | 233    | 67.840 |   | 234    | 68.600 |   | 235    | 68.980 |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 236    | 70.040 |   | 237    | 70.520 |   | 238    | 71.420 |   | 239    | 72.180 |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 240    | 72.900 |   | 241    | 73.980 |   | 242    | 74.580 |   | 243    | 75.320 |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 244    | 76.200 |   | 245    | 76.540 |   | 246    | 77.720 |   | 247    | 78.220 |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 248    | 79.200 |   | 249    | 79.880 |   | 250    | 80.420 |   | 251    | 81.560 |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 252    | 81.960 |   | 253    | 83.140 |   | 254    | 83.720 |   | 255    | 84.340 |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+

.. _sect_D.1.2:

Application of the Standard Formula
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The section of the Grayscale Standard Display Function for the Luminance
Range of the CRT monitor Display System is shown in
`figure_title <#figure_D.1-3>`__. Minimum and maximum Luminance levels
correspond to JND indices of JND\ :sub:`min` = 32.54 and JND\ :sub:`max`
= 453.85, respectively. Thus, there are theoretically about 420
just-noticeable Luminance differences for the Standard Target (see
Normative `Overview <#chapter_6>`__). Obviously, with 8-bit input
digitization resolution, at best 256 noticeable Luminance increments can
be realized.

.. _sect_D.1.3:

Implementation of the Standard
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The measured Characteristic Curve is interpolated for the available
output levels D\ :sub:`output`, in this case, yielding 1024 Luminance
levels L\ :sub:`I,m`. The Grayscale Standard Display Function is also
interpolated between JND\ :sub:`min` and JND\ :sub:`max` ((JND=
[JND\ :sub:`max` - JND\ :sub:`min`]/1023 = [453.85 - 32.54]/1023)
yielding 1024 Standard Luminance levels L\ :sub:`I,STD`. Interpolations
can be performed by a variety of techniques. Here, a cubic spline
technique was employed.

For every L\ :sub:`I,STD`, the closest L\ :sub:`J,m` is determined. The
data pair I,J defines the transformation between D\ :sub:`input` and
D\ :sub:`output` (`table_title <#table_D.1-2>`__) by which the Luminance
response of the Display System is made to approximate the Grayscale
Standard Display Function.

.. table:: Look-Up Table for Calibrating Display System

   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | **I    | **Ou   |   | **I    | **Ou   |   | **I    | **Ou   |   | **I    | **Ou   |
   | nput** | tput** |   | nput** | tput** |   | nput** | tput** |   | nput** | tput** |
   +========+========+===+========+========+===+========+========+===+========+========+
   | 0      | 0      |   | 1      | 118    |   | 2      | 131    |   | 3      | 140    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 4      | 148    |   | 5      | 153    |   | 6      | 160    |   | 7      | 164    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 8      | 169    |   | 9      | 173    |   | 10     | 178    |   | 11     | 182    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 12     | 185    |   | 13     | 189    |   | 14     | 191    |   | 15     | 194    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 16     | 198    |   | 17     | 201    |   | 18     | 204    |   | 19     | 207    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 20     | 210    |   | 21     | 214    |   | 22     | 217    |   | 23     | 219    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 24     | 222    |   | 25     | 225    |   | 26     | 228    |   | 27     | 231    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 28     | 234    |   | 29     | 237    |   | 30     | 240    |   | 31     | 243    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 32     | 245    |   | 33     | 248    |   | 34     | 251    |   | 35     | 253    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 36     | 255    |   | 37     | 257    |   | 38     | 260    |   | 39     | 263    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 40     | 265    |   | 41     | 268    |   | 42     | 271    |   | 43     | 274    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 44     | 276    |   | 45     | 279    |   | 46     | 282    |   | 47     | 284    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 48     | 287    |   | 49     | 290    |   | 50     | 292    |   | 51     | 295    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 52     | 298    |   | 53     | 301    |   | 54     | 303    |   | 55     | 306    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 56     | 308    |   | 57     | 311    |   | 58     | 314    |   | 59     | 317    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 60     | 319    |   | 61     | 320    |   | 62     | 323    |   | 63     | 326    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 64     | 329    |   | 65     | 331    |   | 66     | 334    |   | 67     | 336    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 68     | 339    |   | 69     | 342    |   | 70     | 345    |   | 71     | 347    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 72     | 350    |   | 73     | 353    |   | 74     | 356    |   | 75     | 359    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 76     | 361    |   | 77     | 364    |   | 78     | 367    |   | 79     | 370    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 80     | 372    |   | 81     | 375    |   | 82     | 378    |   | 83     | 381    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 84     | 383    |   | 85     | 385    |   | 86     | 388    |   | 87     | 391    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 88     | 393    |   | 89     | 396    |   | 90     | 399    |   | 91     | 402    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 92     | 405    |   | 93     | 407    |   | 94     | 410    |   | 95     | 413    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 96     | 416    |   | 97     | 419    |   | 98     | 422    |   | 99     | 425    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 100    | 428    |   | 101    | 431    |   | 102    | 434    |   | 103    | 437    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 104    | 440    |   | 105    | 443    |   | 106    | 445    |   | 107    | 448    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 108    | 450    |   | 109    | 452    |   | 110    | 456    |   | 111    | 459    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 112    | 462    |   | 113    | 465    |   | 114    | 468    |   | 115    | 471    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 116    | 474    |   | 117    | 477    |   | 118    | 480    |   | 119    | 483    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 120    | 486    |   | 121    | 490    |   | 122    | 492    |   | 123    | 495    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 124    | 499    |   | 125    | 502    |   | 126    | 505    |   | 127    | 509    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 128    | 511    |   | 129    | 513    |   | 130    | 516    |   | 131    | 519    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 132    | 522    |   | 133    | 526    |   | 134    | 529    |   | 135    | 532    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 136    | 535    |   | 137    | 539    |   | 138    | 542    |   | 139    | 545    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 140    | 549    |   | 141    | 552    |   | 142    | 555    |   | 143    | 559    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 144    | 562    |   | 145    | 565    |   | 146    | 569    |   | 147    | 572    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 148    | 575    |   | 149    | 578    |   | 150    | 581    |   | 151    | 585    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 152    | 588    |   | 153    | 591    |   | 154    | 595    |   | 155    | 599    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 156    | 602    |   | 157    | 605    |   | 158    | 609    |   | 159    | 613    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 160    | 616    |   | 161    | 619    |   | 162    | 623    |   | 163    | 627    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 164    | 631    |   | 165    | 633    |   | 166    | 637    |   | 167    | 640    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 168    | 643    |   | 169    | 646    |   | 170    | 650    |   | 171    | 655    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 172    | 657    |   | 173    | 663    |   | 174    | 666    |   | 175    | 669    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 176    | 674    |   | 177    | 678    |   | 178    | 682    |   | 179    | 684    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 180    | 688    |   | 181    | 693    |   | 182    | 696    |   | 183    | 700    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 184    | 703    |   | 185    | 706    |   | 186    | 711    |   | 187    | 714    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 188    | 719    |   | 189    | 723    |   | 190    | 727    |   | 191    | 731    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 192    | 735    |   | 193    | 738    |   | 194    | 743    |   | 195    | 745    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 196    | 752    |   | 197    | 754    |   | 198    | 758    |   | 199    | 764    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 200    | 766    |   | 201    | 769    |   | 202    | 775    |   | 203    | 777    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 204    | 783    |   | 205    | 787    |   | 206    | 789    |   | 207    | 796    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 208    | 799    |   | 209    | 805    |   | 210    | 808    |   | 211    | 811    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 212    | 818    |   | 213    | 821    |   | 214    | 827    |   | 215    | 830    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 216    | 834    |   | 217    | 838    |   | 218    | 841    |   | 219    | 848    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 220    | 851    |   | 221    | 856    |   | 222    | 861    |   | 223    | 864    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 224    | 870    |   | 225    | 874    |   | 226    | 880    |   | 227    | 883    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 228    | 889    |   | 229    | 893    |   | 230    | 897    |   | 231    | 901    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 232    | 905    |   | 233    | 911    |   | 234    | 915    |   | 235    | 922    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 236    | 925    |   | 237    | 931    |   | 238    | 935    |   | 239    | 941    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 240    | 945    |   | 241    | 951    |   | 242    | 955    |   | 243    | 960    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 244    | 964    |   | 245    | 969    |   | 246    | 975    |   | 247    | 979    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 248    | 985    |   | 249    | 991    |   | 250    | 995    |   | 251    | 1002   |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 252    | 1006   |   | 253    | 1012   |   | 254    | 1016   |   | 255    | 1023   |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+

.. _sect_D.1.4:

Measures of Conformance
~~~~~~~~~~~~~~~~~~~~~~~

The FIT and the LUM metrics proposed in `Measuring the Accuracy With
Which a Display System Matches the Grayscale Standard Display Function
(Informative) <#chapter_C>`__ are applied to determine the macroscopic
and microscopic approximation of the L :sub:`J,m`\ to the L
:sub:`I,STD`. `figure_title <#figure_D.1-3>`__ shows the perceptually
linearized Display Function superimposed on the Grayscale Standard
Display Function and `figure_title <#figure_D.1-4>`__ summarizes the
results of the two metrics. A good global fit was achieved as
demonstrated by the nearly horizontal-line fit as best fit obtained with
the FIT metric. The RMSE is acceptable. All 255 P-Value intervals lead
to JNDs on the transformed Display Function for the Standard Target.

.. _sect_D.2:

Transparent Hardcopy Devices
----------------------------

.. _sect_D.2.1:

Measuring the System Characteristic Curve
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A transparent hardcopy device is exemplified by a laser printer
(including processor) that prints (exposes and processes) one or more
images on a sheet of transparent film (typically a 14" x 17" film). This
film is eventually placed over a high Luminance light-box in a darkened
room for viewing.

The Characteristic Curve for such a transparent hardcopy device is
obtained by printing a test image consisting of a pattern of n bars,
each bar having a specific numeric value (DDL). The optical density of
each printed bar is then measured, using a transmission densitometer,
for each of the printed bars.

To accurately define a printer's Characteristic Curve, it is desirable
that n be as large as possible (to capture as many points as possible on
the Characteristic Curve). However, the limitations on absolute
quantitative repeatability imposed by the printer, processor, or media
technologies may dictate that a much smaller value of n be used (to
prevent a conformance metric that is sensitive to differences from
becoming unstable and meaningless, as the density differences between
adjacent bars become "in the noise" as the number of bars becomes
large).

One example of a test image is a pattern of 32 approximately
equal-height bars, spanning the usable printable region of the film,
having 32 approximately equi-spaced DDLs as follows:

To define a test pattern with n DDLs for a printer with an N-bit input,
the DDL of step # i can be set to

.. math:: DDL<subscript>i</subscript> = (2<superscript>N-1</superscript>)i/(n-1)

rounded to the nearest integer.

The tabulated values of DDLi and the corresponding measured optical
densities ODi constitute a Characteristic Curve of the printer.

.. _sect_D.2.2:

Application of the Grayscale Standard Display Function
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The films that are produced by transparent hardcopy printers are often
brought to a variety of locations, where they may be viewed on different
light-boxes and under a variety of viewing conditions. Accordingly, the
approach of PS3.14 is to define, for hardcopy transparent printers, what
densities (rather than Luminances) should be produced, and to provide
here a method of applying the Grayscale Standard Display Function to the
transparent hardcopy case, based on parameters that are typical of the
expected range of light-box Luminances and other viewing parameters.

The specific parameters that are used in the following example are as
follows:

-  L\ :sub:`0` (Luminance of light-box with no film present): 2000
   cd/m\ :sup:`2`

-  L\ :sub:`a` (ambient room light reflected by film): 10 cd/m\ :sup:`2`

-  D\ :sub:`min` (minimum optical density obtainable on film): 0.20

-  D\ :sub:`max` (maximum optical density desirable on film): 3.00.

The process of constructing a table of desired OD values from the
Grayscale Standard Display Function begins with defining the Luminance
Range and the corresponding range of the Just-Noticeable Difference
Index, j. The minimum and maximum Luminance values are given
respectively by

.. math::

   Lmin= L<subscript>a</subscript> + L<subscript>0</subscript>10<superscript>-D<subscript>max</subscript>
   </superscript>= 12.0 cd/m<superscript>2</superscript>
               

.. math::

   L<subscript>max</subscript>= L<subscript>a</subscript> + L<subscript>0</subscript>10<superscript>-D<subscript>min</subscript>
   </superscript>= 1271.9 cd/m<superscript>2</superscript>
               

Next, calculate the corresponding Just-Noticeable Difference Index
values, j\ :sub:`min` and j\ :sub:`max`. For the current example, we
obtain

.. math:: j<subscript>min</subscript> = 233.32

.. math:: j<subscript>max</subscript> = 848.75

This gives us the range of j-values that the printer should cover. The
printer should map its minimum input (P-Value = 0) to j\ :sub:`min` and
the corresponding Lmin. It should map its maximum input (P-Value = 2N-1
where N is the number of input bits) to j\ :sub:`max` and the
corresponding L\ :sub:`max`. At any intermediate input it should map its
input proportionately:

.. math::

   j(PV) = j<subscript>min</subscript> + (j<subscript>max</subscript>-j<subscript>min</subscript>)
                 <inlinemediaobject>
   <imageobject>
   <imagedata fileref="part14_fromword_files/image056.png" />
   </imageobject>
   </inlinemediaobject>

and target values for the Luminance given by the Standard's formula:
L(j(P-Value)). This "targeting" consists of producing an optical density
OD for this P-Value that will give the desired Luminance L(j(P-Value))
under the conditions of L\ :sub:`0` and L\ :sub:`a` previously defined.
The required density can thus be calculated as follows:

.. _sect_D.2.3:

Implementation of the Grayscale Standard Display Function
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Carrying this example into the even more specific case of a printer with
an 8-bit input leads to the following table, which defines the OD's to
be generated for each of the 256 possible P-Values.

.. table:: Optical Densities for Each P-Value for an 8-Bit Printer

   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | **P-V  | **O    |   | **P-V  | **O    |   | **P-V  | **O    |   | **P-V  | **O    |
   | alue** | ptical |   | alue** | ptical |   | alue** | ptical |   | alue** | ptical |
   |        | D      |   |        | D      |   |        | D      |   |        | D      |
   |        | ensity |   |        | ensity |   |        | ensity |   |        | ensity |
   |        | (OD)** |   |        | (OD)** |   |        | (OD)** |   |        | (OD)** |
   +========+========+===+========+========+===+========+========+===+========+========+
   | 0      | 3.000  |   | 1      | 2.936  |   | 2      | 2.880  |   | 3      | 2.828  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 4      | 2.782  |   | 5      | 2.739  |   | 6      | 2.700  |   | 7      | 2.662  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 8      | 2.628  |   | 9      | 2.595  |   | 10     | 2.564  |   | 11     | 2.534  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 12     | 2.506  |   | 13     | 2.479  |   | 14     | 2.454  |   | 15     | 2.429  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 16     | 2.405  |   | 17     | 2.382  |   | 18     | 2.360  |   | 19     | 2.338  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 20     | 2.317  |   | 21     | 2.297  |   | 22     | 2.277  |   | 23     | 2.258  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 24     | 2.239  |   | 25     | 2.221  |   | 26     | 2.203  |   | 27     | 2.185  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 28     | 2.168  |   | 29     | 2.152  |   | 30     | 2.135  |   | 31     | 2.119  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 32     | 2.103  |   | 33     | 2.088  |   | 34     | 2.073  |   | 35     | 2.058  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 36     | 2.043  |   | 37     | 2.028  |   | 38     | 2.014  |   | 39     | 2.000  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 40     | 1.986  |   | 41     | 1.973  |   | 42     | 1.959  |   | 43     | 1.946  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 44     | 1.933  |   | 45     | 1.920  |   | 46     | 1.907  |   | 47     | 1.894  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 48     | 1.882  |   | 49     | 1.870  |   | 50     | 1.857  |   | 51     | 1.845  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 52     | 1.833  |   | 53     | 1.821  |   | 54     | 1.810  |   | 55     | 1.798  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 56     | 1.787  |   | 57     | 1.775  |   | 58     | 1.764  |   | 59     | 1.753  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 60     | 1.742  |   | 61     | 1.731  |   | 62     | 1.720  |   | 63     | 1.709  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 64     | 1.698  |   | 65     | 1.688  |   | 66     | 1.677  |   | 67     | 1.667  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 68     | 1.656  |   | 69     | 1.646  |   | 70     | 1.636  |   | 71     | 1.626  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 72     | 1.616  |   | 73     | 1.605  |   | 74     | 1.595  |   | 75     | 1.586  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 76     | 1.576  |   | 77     | 1.566  |   | 78     | 1.556  |   | 79     | 1.547  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 80     | 1.537  |   | 81     | 1.527  |   | 82     | 1.518  |   | 83     | 1.508  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 84     | 1.499  |   | 85     | 1.490  |   | 86     | 1.480  |   | 87     | 1.471  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 88     | 1.462  |   | 89     | 1.453  |   | 90     | 1.444  |   | 91     | 1.434  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 92     | 1.425  |   | 93     | 1.416  |   | 94     | 1.407  |   | 95     | 1.398  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 96     | 1.390  |   | 97     | 1.381  |   | 98     | 1.372  |   | 99     | 1.363  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 100    | 1.354  |   | 101    | 1.346  |   | 102    | 1.337  |   | 103    | 1.328  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 104    | 1.320  |   | 105    | 1.311  |   | 106    | 1.303  |   | 107    | 1.294  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 108    | 1.286  |   | 109    | 1.277  |   | 110    | 1.269  |   | 111    | 1.260  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 112    | 1.252  |   | 113    | 1.244  |   | 114    | 1.235  |   | 115    | 1.227  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 116    | 1.219  |   | 117    | 1.211  |   | 118    | 1.202  |   | 119    | 1.194  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 120    | 1.186  |   | 121    | 1.178  |   | 122    | 1.170  |   | 123    | 1.162  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 124    | 1.154  |   | 125    | 1.146  |   | 126    | 1.138  |   | 127    | 1.130  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 128    | 1.122  |   | 129    | 1.114  |   | 130    | 1.106  |   | 131    | 1.098  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 132    | 1.090  |   | 133    | 1.082  |   | 134    | 1.074  |   | 135    | 1.066  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 136    | 1.058  |   | 137    | 1.051  |   | 138    | 1.043  |   | 139    | 1.035  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 140    | 1.027  |   | 141    | 1.020  |   | 142    | 1.012  |   | 143    | 1.004  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 144    | 0.996  |   | 145    | 0.989  |   | 146    | 0.981  |   | 147    | 0.973  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 148    | 0.966  |   | 149    | 0.958  |   | 150    | 0.951  |   | 151    | 0.943  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 152    | 0.935  |   | 153    | 0.928  |   | 154    | 0.920  |   | 155    | 0.913  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 156    | 0.905  |   | 157    | 0.898  |   | 158    | 0.890  |   | 159    | 0.883  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 160    | 0.875  |   | 161    | 0.868  |   | 162    | 0.860  |   | 163    | 0.853  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 164    | 0.845  |   | 165    | 0.838  |   | 166    | 0.831  |   | 167    | 0.823  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 168    | 0.816  |   | 169    | 0.808  |   | 170    | 0.801  |   | 171    | 0.794  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 172    | 0.786  |   | 173    | 0.779  |   | 174    | 0.772  |   | 175    | 0.764  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 176    | 0.757  |   | 177    | 0.750  |   | 178    | 0.742  |   | 179    | 0.735  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 180    | 0.728  |   | 181    | 0.721  |   | 182    | 0.713  |   | 183    | 0.706  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 184    | 0.699  |   | 185    | 0.692  |   | 186    | 0.684  |   | 187    | 0.677  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 188    | 0.670  |   | 189    | 0.663  |   | 190    | 0.656  |   | 191    | 0.648  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 192    | 0.641  |   | 193    | 0.634  |   | 194    | 0.627  |   | 195    | 0.620  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 196    | 0.613  |   | 197    | 0.606  |   | 198    | 0.598  |   | 199    | 0.591  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 200    | 0.584  |   | 201    | 0.577  |   | 202    | 0.570  |   | 203    | 0.563  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 204    | 0.556  |   | 205    | 0.549  |   | 206    | 0.542  |   | 207    | 0.534  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 208    | 0.527  |   | 209    | 0.520  |   | 210    | 0.513  |   | 211    | 0.506  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 212    | 0.499  |   | 213    | 0.492  |   | 214    | 0.485  |   | 215    | 0.478  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 216    | 0.471  |   | 217    | 0.464  |   | 218    | 0.457  |   | 219    | 0.450  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 220    | 0.443  |   | 221    | 0.436  |   | 222    | 0.429  |   | 223    | 0.422  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 224    | 0.415  |   | 225    | 0.408  |   | 226    | 0.401  |   | 227    | 0.394  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 228    | 0.387  |   | 229    | 0.380  |   | 230    | 0.373  |   | 231    | 0.366  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 232    | 0.359  |   | 233    | 0.352  |   | 234    | 0.345  |   | 235    | 0.338  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 236    | 0.331  |   | 237    | 0.324  |   | 238    | 0.317  |   | 239    | 0.311  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 240    | 0.304  |   | 241    | 0.297  |   | 242    | 0.290  |   | 243    | 0.283  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 244    | 0.276  |   | 245    | 0.269  |   | 246    | 0.262  |   | 247    | 0.255  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 248    | 0.248  |   | 249    | 0.241  |   | 250    | 0.234  |   | 251    | 0.228  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 252    | 0.221  |   | 253    | 0.214  |   | 254    | 0.207  |   | 255    | 0.200  |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+

Plotting these values gives the curve of
`figure_title <#figure_D.2-3>`__.

.. _sect_D.2.4:

Measures of Conformance
~~~~~~~~~~~~~~~~~~~~~~~

As an example, a bar pattern with 32 optical densities was printed on
transmissive media (film). Beforehand, the printer had been set up to
print over a density range from 0.2 (D\ :sub:`min`) to 3.0
(D\ :sub:`max`) and had been pre-configured by the manufacturer to use
the Grayscale Standard Display Function, converted by the manufacturer
into the table of target density values vs. P-Values described earlier.

The test pattern that was used for this was an 8-bit image consisting
essentially of 32 horizontal bars. The 32 P-Values used for the bars
were as follows: 0, 8, 16, 25, 33, 41, 49, 58, 66, 74, 82, 90,99, 107,
115, 123, 132, 140, 148, 156, 165, 173, 181, 189, 197, 206, 214,222,
230, 239, 247, 255.

For a given film, the 32 bars' optical densities were measured (near the
middle of the film), converted to Luminances (using the standard
parameters of light-box Luminance and reflected ambient light described
earlier),and converted to Just-Noticeable Difference Indices by
mathematically computing j(L) from L(j), where L(j) is the Grayscale
Standard Display Function of Luminance L as a function of the
Just-Noticeable Difference Index j. For each of the 31 intervals between
consecutive measured values, a calculated value of "JNDs per increment
in P-Values" was obtained by dividing the difference in Just-Noticeable
Difference Index by the difference in P-Values for that interval. (In
these calculations, density, L, and j are all floating-point variables.
No rounding to integer values is done, so no truncation error is
introduced.)

In this example, the film's data could be reasonably well fit by a
horizontal straight line. That is, the calculated "JNDs per increment in
P-Values was essentially constant at 2.4. A mathematical fit yielded a
slight non-zero slope (specifically, dropping from 2.5 to 2.3 as the
P-Value went from 0 to 255), but the 0.2 total difference was
considerably smaller than the noise that was present in the 31
individual values of "JNDs per increment in P-Value" so is of doubtful
significance. (The "noise" referred to here consists of the random,
non-repeatable variations that are seen if a new set of measured data
(e.g., from a second print of the same test pattern) is compared with a
previous set of measurements.)

No visual tests were done to see if a slope that small could be detected
by a human observer in side-by-side film comparisons.

Incidentally, if one considers just the 32 original absolute measured
densities (rather than differential values based on small differences),
one finds, in this case, quite reasonable agreement between the target
and measured optical densities (within the manufacturer's norms for
density accuracy, at a given density). But if one uses any metric that
is based on differential information over small intervals, the results
must be considered more cautiously, since they can be strongly affected
by (and may be dominated by) various imperfections that are independent
of a device's "true" (or averaged over many cases) characteristic
behavior.

.. _sect_D.3:

Reflective Display Systems
--------------------------

This last example illustrates how conformance with the Grayscale
Standard Display Function may be achieved for a thermal-dye-transfer
paper printer/office-light system. The thermal-dye-transfer printer
produces black-and-white grayscale prints on a semi-glossy 8-inch x
10-inch heavy-gauge paper. The print is illuminated uniformly by
fluorescent lamps so that the minimum reflective density produces a
Luminance of 150 cd/m\ :sup:`2`. The hypothetical transformation
operator is assumed to have equal input and output digitization
resolution of 8 bits.

.. _sect_D.3.1:

Measuring the System Characteristic Curve
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A print with a 64-step grayscale tablet was printed for DDLs 4, 8, 12,
...,248, 252, 255. The reflection optical densities (from 0.08 to 2.80)
were measured with a densitometer. The Luminance levels corresponding to
the measured optical densities and illumination conditions are plotted
in `figure_title <#figure_D.3-1>`__.

.. _sect_D.3.2:

Application of the Grayscale Standard Display Function
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This last example illustrates how conformance with the Grayscale
Standard Display Function may be achieved for a thermal-dye-transfer
paper printer/office-light system. The thermal-dye-transfer printer
produces black-and-white grayscale prints on a semi-glossy 8-inch x
10-inch heavy-gauge paper. The print is illuminated uniformly by
fluorescent lamps so that the minimum reflective density produces a
Luminance of 150 cd/m\ :sup:`2`. The hypothetical transformation
operator is assumed to have equal input and output digitization
resolution of 8 bits.

.. _sect_D.3.3:

Implementation of the Grayscale Standard Display Function
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The measured Characteristic Curve is interpolated for the available DDLs
yielding 256 Luminance levels L\ :sub:`I,m`. The Grayscale Standard
Display Function is also interpolated between JND\ :sub:`min` and
JND\ :sub:`max` (DJND = [JND\ :sub:`max` - JND\ :sub:`min`]/255)
yielding 256 Standard Luminance levels L\ :sub:`I,STD`.

For every L\ :sub:`I,STD`, the closest L\ :sub:`J,m` is determined. The
data pair I,J defines the transformation between D\ :sub:`input` and
D\ :sub:`output` (`table_title <#table_D.3-1>`__ and
`figure_title <#figure_D.3-2>`__) by which the Luminance response of the
Display System is made to approximates the Grayscale Standard Display
Function.

.. table:: Look-Up Table for Calibrating Reflection Hardcopy System

   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | **P-V  | *      |   | **P-V  | *      |   | **P-V  | *      |   | **P-V  | *      |
   | alue** | *DDL** |   | alue** | *DDL** |   | alue** | *DDL** |   | alue** | *DDL** |
   +========+========+===+========+========+===+========+========+===+========+========+
   | 0      | 6      |   | 1      | 9      |   | 2      | 12     |   | 3      | 15     |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 4      | 18     |   | 5      | 20     |   | 6      | 27     |   | 7      | 29     |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 8      | 30     |   | 9      | 31     |   | 10     | 31     |   | 11     | 32     |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 12     | 33     |   | 13     | 33     |   | 14     | 34     |   | 15     | 36     |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 16     | 38     |   | 17     | 40     |   | 18     | 41     |   | 19     | 42     |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 20     | 43     |   | 21     | 44     |   | 22     | 45     |   | 23     | 59     |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 24     | 60     |   | 25     | 61     |   | 26     | 62     |   | 27     | 62     |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 28     | 63     |   | 29     | 63     |   | 30     | 64     |   | 31     | 64     |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 32     | 65     |   | 33     | 65     |   | 34     | 65     |   | 35     | 66     |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 36     | 66     |   | 37     | 67     |   | 38     | 67     |   | 39     | 68     |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 40     | 70     |   | 41     | 74     |   | 42     | 75     |   | 43     | 76     |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 44     | 78     |   | 45     | 84     |   | 46     | 85     |   | 47     | 86     |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 48     | 87     |   | 49     | 87     |   | 50     | 88     |   | 51     | 89     |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 52     | 89     |   | 53     | 91     |   | 54     | 92     |   | 55     | 94     |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 56     | 95     |   | 57     | 96     |   | 58     | 97     |   | 59     | 97     |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 60     | 98     |   | 61     | 99     |   | 62     | 99     |   | 63     | 100    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 64     | 101    |   | 65     | 102    |   | 66     | 103    |   | 67     | 104    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 68     | 105    |   | 69     | 106    |   | 70     | 107    |   | 71     | 108    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 72     | 109    |   | 73     | 110    |   | 74     | 112    |   | 75     | 114    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 76     | 116    |   | 77     | 118    |   | 78     | 119    |   | 79     | 120    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 80     | 121    |   | 81     | 122    |   | 82     | 122    |   | 83     | 123    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 84     | 123    |   | 85     | 124    |   | 86     | 125    |   | 87     | 125    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 88     | 126    |   | 89     | 126    |   | 90     | 127    |   | 91     | 127    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 92     | 128    |   | 93     | 129    |   | 94     | 130    |   | 95     | 131    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 96     | 133    |   | 97     | 134    |   | 98     | 135    |   | 99     | 136    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 100    | 136    |   | 101    | 137    |   | 102    | 138    |   | 103    | 138    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 104    | 139    |   | 105    | 139    |   | 106    | 140    |   | 107    | 141    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 108    | 143    |   | 109    | 145    |   | 110    | 147    |   | 111    | 148    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 112    | 149    |   | 113    | 150    |   | 114    | 151    |   | 115    | 152    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 116    | 153    |   | 117    | 154    |   | 118    | 154    |   | 119    | 155    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 120    | 156    |   | 121    | 156    |   | 122    | 157    |   | 123    | 158    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 124    | 159    |   | 125    | 160    |   | 126    | 160    |   | 127    | 162    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 128    | 163    |   | 129    | 164    |   | 130    | 165    |   | 131    | 166    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 132    | 167    |   | 133    | 168    |   | 134    | 169    |   | 135    | 170    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 136    | 170    |   | 137    | 171    |   | 138    | 172    |   | 139    | 172    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 140    | 173    |   | 141    | 174    |   | 142    | 175    |   | 143    | 175    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 144    | 176    |   | 145    | 177    |   | 146    | 178    |   | 147    | 179    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 148    | 179    |   | 149    | 180    |   | 150    | 181    |   | 151    | 182    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 152    | 182    |   | 153    | 183    |   | 154    | 184    |   | 155    | 184    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 156    | 185    |   | 157    | 186    |   | 158    | 186    |   | 159    | 187    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 160    | 187    |   | 161    | 188    |   | 162    | 188    |   | 163    | 189    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 164    | 189    |   | 165    | 190    |   | 166    | 190    |   | 167    | 190    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 168    | 191    |   | 169    | 191    |   | 170    | 192    |   | 171    | 192    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 172    | 192    |   | 173    | 193    |   | 174    | 194    |   | 175    | 194    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 176    | 195    |   | 177    | 195    |   | 178    | 196    |   | 179    | 197    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 180    | 198    |   | 181    | 199    |   | 182    | 199    |   | 183    | 200    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 184    | 200    |   | 185    | 201    |   | 186    | 202    |   | 187    | 202    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 188    | 203    |   | 189    | 203    |   | 190    | 204    |   | 191    | 204    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 192    | 205    |   | 193    | 205    |   | 194    | 206    |   | 195    | 207    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 196    | 207    |   | 197    | 208    |   | 198    | 209    |   | 199    | 210    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 200    | 211    |   | 201    | 212    |   | 202    | 213    |   | 203    | 214    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 204    | 214    |   | 205    | 215    |   | 206    | 216    |   | 207    | 216    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 208    | 217    |   | 209    | 218    |   | 210    | 219    |   | 211    | 219    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 212    | 220    |   | 213    | 220    |   | 214    | 221    |   | 215    | 222    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 216    | 222    |   | 217    | 223    |   | 218    | 223    |   | 219    | 224    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 220    | 224    |   | 221    | 225    |   | 222    | 226    |   | 223    | 226    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 224    | 227    |   | 225    | 228    |   | 226    | 228    |   | 227    | 230    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 228    | 231    |   | 229    | 232    |   | 230    | 234    |   | 231    | 235    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 232    | 236    |   | 233    | 238    |   | 234    | 238    |   | 235    | 239    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 236    | 240    |   | 237    | 241    |   | 238    | 242    |   | 239    | 242    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 240    | 243    |   | 241    | 244    |   | 242    | 245    |   | 243    | 246    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 244    | 247    |   | 245    | 248    |   | 246    | 249    |   | 247    | 250    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 248    | 250    |   | 249    | 251    |   | 250    | 251    |   | 251    | 252    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+
   | 252    | 252    |   | 253    | 253    |   | 254    | 253    |   | 255    | 254    |
   +--------+--------+---+--------+--------+---+--------+--------+---+--------+--------+

.. _sect_D.3.4:

Measures of Conformance
~~~~~~~~~~~~~~~~~~~~~~~

The FIT and LUM metrics as proposed in `Measuring the Accuracy With
Which a Display System Matches the Grayscale Standard Display Function
(Informative) <#chapter_C>`__ are applied to determine the macroscopic
and microscopic approximation of the L\ :sub:`J,m` to the
L\ :sub:`I,STD`. `figure_title <#figure_D.3-3>`__ shows the perceptually
linearized Display Function superimposed on the Grayscale Standard
Display Function and `figure_title <#figure_D.3-4>`__ summarizes the
results of the two metrics. FIT provides as best fit of the
JNDs/Luminance interval a straight line almost perfectly parallel to the
horizontal axis indicating good global fit of the transformed Display
Function with the Grayscale Standard Display Function. The RMSE computed
by LUM is relatively large indicating more pronounced local deviations
from the Grayscale Standard Display Function as, for example, with the
soft-copy Display System illustrated in `Emissive Display
Systems <#sect_D.1>`__. At least in part, the larger RMSE is due to the
fact that the input and output digitization resolution for the transform
are equal. The transformation table (`table_title <#table_D.3-1>`__) and
`figure_title <#figure_D.3-2>`__ show that several P-Values lead to the
same Luminance levels on the transformed Display Function. In fact, only
205 of the 255 Luminance intervals lead to JNDs for the Standard Target.

