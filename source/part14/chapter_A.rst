.. _chapter_A:

Derivation of the Grayscale Standard Display Function (Informative)
===================================================================

.. _sect_A.1:

Rationale For Selecting the Grayscale Standard Display Function
---------------------------------------------------------------

In choosing the Grayscale Standard Display Function, it was considered
mandatory to have only one continuous, monotonically behaving
mathematical function for the entire Luminance Range of interest.
Correspondingly, for simplicity of implementing the Grayscale Standard
Display Function, it was felt to be useful to define it by only one
table of data pairs. As a secondary objective, it was considered
desirable that the Grayscale Standard Display Function provide
similarity in grayscale rendition on Display Systems of different
Luminance Range and that good use of the available DDLs of a Display
System was facilitated.

Perceptual linearization was thought to be a useful concept for arriving
at a Grayscale Standard Display Function for meeting the above secondary
objectives; however, it is not considered an objective by itself. Apart
from the fact that is probably an elusive goal to perceptually linearize
all types of medical images under various viewing conditions by one
mathematical function, medical images are mostly presented by
application-specific Display Functions that assign contrast
non-uniformly according to clinical needs.

Intuitively, one would assume that perceptually linearized images on
different Display Systems will be judged to be similar. To achieve
perceptual linearization, a model of the human visual system response
was required and the Barten model [A1] was chosen.

Early experiments showed that an appealing degree of contrast
equalization and similarity could be obtained with a Display Function
derived from Barten's model of human visual system response. The
employed images were square patterns, the SMPTE pattern, and the Briggs'
pattern [A2].

It was wished to relate DDLs of a Display System to some perceptually
linear scale, primarily, to gain efficient utilization of the available
input levels. If digitization levels lead to luminance or optical
density levels that are perceptually indistinguishable, they are wasted.
If they are too far apart, the observer may see contours. Hence, the
concept of perceptual linearization was retained, not as a goal for the
Grayscale Standard Display Function, but to obtain a concept for a
measure of how well these objectives have been met.

Perceptual linearization is realizable, in a strict sense, only for
rather simple images like square patterns or gratings in a uniform
surrounding. Nevertheless, the concept of a perceptually linearized
Display Function derived from experiments with simple test patterns has
been successfully applied to complex images as described in the
literature [A3-A8]. While it was clearly recognized that perceptual
linearization can never be achieved for all details or spatial
frequencies and object sizes at once, perceptual linearization for
frequencies and object sizes near the peak of human Contrast Sensitivity
seemed to do a ìreasonable jobî also in complex images.

Limited (unpublished) experiments have indicated that perceptual
linearization for a particular detail in a complex image with a wide
Luminance Range and heterogeneous surround required Display Functions
that are rather strongly bent in the dark regions of the image and that
such Display Functions for a low-luminance and a high-luminance display
system would not be part of a continuous, monotonic function. This
experience may underly the considerations of the CIELab curve [A9]
proposed by other standards groups.

Other experiments and observations with computed radiographs seemed to
suggest that similarity could also be obtained between grayscale
renditions on Display Systems of different Luminance when the same
application-specific function is combined with log-linear Characteristic
Curves of the Display Systems. Thus similarity, if not contrast
equalization, could be gained by a straight, luminance-independent shape
for the Display Function.

While it might have been equally sensible to choose the rather simple
log-linear Display Function as a standard, this was not done for the
following reason, among others.

For high-resolution Display Systems with high intrinsic video bandwidth,
digitization resolution is limited to 8 or 10 bits because of technology
and other constraints. The more a Grayscale Standard Display Function
deviates from the Characteristic Curve of a Display System, the poorer
the utilization of DDLs typically is from a perception point of view.
The Characteristic Curve of CRT Display Systems has a convex curvature
with respect to a log-linear straight line. It differs much less from
Display Functions derived from human vision models and the concept of
perceptual linearization than from a log-linear Display Function.

When using application-specific display processes that cause the
resultant Display Function to deviate strongly from the Grayscale
Standard Display Function, the function conceivably does not provide
good similarity. In this case, other functions may yield better
similarity.

In summary, a Display Function was derived from Barten's model of the
human visual system to gain a single continuous mathematical function
which in its curvature falls between a log-linear response and a Display
Function that may yield perceptual linearization in complex scenery with
a wide luminance range within the image. Other models of human contrast
sensitivity may potentially provide a better function, but were not
evaluated. The notion of perceptual linearization was chosen to meet the
secondary objectives of the Grayscale Standard Display Function, but not
as an explicit goal of the Grayscale Standard Display Function itself.
It is recognized that better functions may exist to meet these
objectives. It is believed that almost any single mathematically defined
Standard Function will greatly improve image presentations on Display
Systems in communication networks.

.. _sect_A.2:

Details of the Barten Model
---------------------------

Barten's model considers neural noise, lateral inhibition, photon noise,
external noise, limited integration capability, the optical modulation
transfer function, orientation, and temporal filtering. Neuron noise
represents the upper limit of Contrast Sensitivity at high spatial
frequencies. Low spatial frequencies appear to be attenuated by lateral
inhibition in the ganglion cells that seems to be caused by the
subtraction of a spatially low-pass filtered signal from the original.
Photon noise is defined by the fluctuations of the photon flux h, the
pupil diameter d, and quantum detection efficiency η of the eye. At low
light levels, the Contrast Sensitivity is proportional to the
square-root of Luminance according to the de Vries-Rose law. The
temporal integration capability in the model used here is simply
represented by a time constant of T = 0.1 sec. Temporal filtering
effects are not included. Next to the temporal integration capability,
the eye also has limited spatial integration capability: There is a
maximum angular size X\ :sub:`E` x Y\ :sub:`E` as well as a maximum
number of cycles N\ :sub:`E` over which the eye can integrate
information in the presence of various noise sources. The optical
modulation transfer function

(u, spatial frequency in c/deg) is derived from a Gaussian point-spread
function including the optical properties of the eye-lens, stray light
from the optical media, diffusion in the retina, and the discrete nature
of the receptor elements as well as from the spherical aberration,
C\ :sub:`sph`, which is the main pupil-diameter-dependent component.
σ\ :sub:`0` is the value of σ at small pupil sizes. External noise may
stem from Display System noise and image noise. Contrast sensitivity
varies approximately sinusoidally with the orientation of the test
pattern with equal maximum sensitivity at 0 and 90 deg and minimal
sensitivity at 45 de.g., The difference in Contrast Sensitivity is only
present at high spatial frequencies. The effect is modeled by a
variation in integration capability.

The combination of these effects yields the equation for contrast as a
function of spatial frequency:

The effect of noise appears in the first parenthesis within the
square-root as a noise contrast related to the variances of photon
(first term), filtered neuron (second term), and external noise. The
Illuminance, I\ :sub:`L` = π/4 d\ :sup:`2`\ L, of the eye is expressed
in trolands [td], d is the pupil diameter in mm, and L the Luminance of
the Target in cd/m\ :sup:`2`. The pupil diameter is determined by the
formula of de Groot and Gebhard:

.. math:: d = 4.6 - 2.8 . tanh(0.4 . Log<subscript>10</subscript>(0.625 . L))

The term (1 - F(u))\ :sup:`2` = 1 - exp(-u\ :sup:`2`/u\ :sub:`0`
:sup:`2`) describes the low frequency attenuation of neuron noise due to
lateral inhibition (u\ :sub:`0` = 8 c/deg).
`equation_title <#equation_A-2>`__ represents the simplified case of
square targets, X\ :sub:`0` = Y\ :sub:`0` [deg]. Φ\ :sub:`ext` is the
contrast variance corresponding to external noise. k = 3.3, η = 0.025, h
= 357.3600 photons/td sec deg\ :sup:`2`; the contrast variance
corresponding to the neuron noise Φ\ :sub:`0` = 3.10\ :sup:`-8` sec
deg\ :sup:`2`, X\ :sub:`E` = 12 deg, N\ :sub:`E` = 15 cycles (at 0 and
90 deg and N\ :sub:`E` = 7.5 cycles at 45 deg for frequencies above 2
c/deg), σ\ :sub:`0` = 0.0133 deg, C\ :sub:`sph` = 0.0001
deg/mm\ :sup:`3` [A1]. `equation_title <#equation_A-2>`__ provides a
good fit of experimental data for 10\ :sup:`-4` ≤ L ≤ 103
cd/m\ :sup:`2`, 0.5 ≤ X\ :sub:`0` ≤ 60 deg, 0.2 ≤ u ≤ 50 c/deg.

After inserting all constants, `equation_title <#equation_A-2>`__
reduces to

with q1 = 0.1183034375, q2 = 3.962774805 . 10\ :sup:`-5`, and q3 =
1.356243499 . 10\ :sup:`-7`.

When viewed from 250 mm distance, the Standard Target has a size of
about 8.7 mm x 8.7 mm and the spatial frequency of the grid equals about
0.92 line pairs per millimeter.

The Grayscale Standard Display Function is obtained by computing the
Threshold Modulation S\ :sub:`j` as a function of mean grating Luminance
and then stacking these values on top of each other. The mean Luminance
of the next higher level is calculated by adding the peak-to-peak
modulation to the mean Luminance L\ :sub:`j` of the previous level:

Thus, in PS3.14, the peak-to-peak Threshold Modulation is called a
just-noticeable Luminance difference.

When a Display System conforms with the Grayscale Standard Display
Function, it is perceptually linearized when observing the Standard
Target: If a Display System had infinitely fine digitization resolution,
equal increments in P-Value would produce equally perceivable contrast
steps and, under certain conditions, just-noticeable Luminance
differences (displayed one at a time) for the Standard Target (the
grating with sinusoidal modulation of 4 c/degree over a 2 degree x 2
degree area, embedded in a uniform background with a Luminance equal to
the mean target Luminance).

The display of the Standard Target at different Luminance levels one at
a time is an academic display situation. An image containing different
Luminance levels with different targets and Luminance distributions at
the same time is in general not perceptually linearized. It is once more
emphasized that the concept of perceptual linearization of Display
Systems for the Standard Target served as a logical means for deriving a
continuous mathematical function and for meeting the secondary goals of
the Grayscale Standard Display Function. The function may represent a
compromise between perceptual linearization of complex images by
strongly-bent Display Functions and gaining similarity of grayscale
perception within an image on Display Systems of different Luminance by
a log-linear Display Function.

The Characteristic Curve of the Display System is measured and
represented by {Luminance, DDL}-pairs L\ :sub:`m` = F(D\ :sub:`m`). A
discrete transformation may be performed that maps the previously used
DDLs, D\ :sub:`input`, to D\ :sub:`output` according to Equations (A6)
and (A7) such that the available ensemble of discrete Luminance levels
is used to approximate the Grayscale Standard Display Function L = G(j).
The transformation is illustrated in Fig. A1. By such an operation,
conformance with the Grayscale Standard Display Function may be reached.

.. math:: D<subscript>output</subscript> = s . F<superscript>-1</superscript>[G(j)]

s is a scale factor for accommodating different input and output
digitization resolutions.

The index j (which in general will be a non-integer number) of the
Standard Luminance Levels is determined from the starting index
j\ :sub:`0` of the Standard Luminance level at the minimum Luminance of
the Display System (including ambient light), the number of Standard
JNDs, N\ :sub:`JND`, over the Luminance Range of the Display System, the
digitization resolution DR, and the DDLs, D\ :sub:`input`, of the
Display System:

.. math::

   I = I<subscript>0</subscript> + N<subscript>JND</subscript> / DR . D<subscript>input</subscript>

A detailed example for executing such a transformation is given in
`Illustrations for Achieving Conformance with the Grayscale Standard
Display Function (Informative) <#chapter_D>`__.

.. _sect_A.3:

References
----------

[A1] P.G.J. Barten: Physical model for the Contrast Sensitivity of the
human eye. Proc. SPIE **1666**, 57-72 (1992) and Spatio-temporal model
for the Contrast Sensitivity of the human eye and its temporal aspects.
Proc. SPIE **1913**-01 (1993)

[A2] S.J. Briggs: Digital test target for display evaluation *.*\ Proc.
SPIE **253**, 237-246 (1980)

[A3] S.J. Briggs: Photometric technique for deriving a "best gamma" for
displays *.*\ Proc. SPIE **199**, Paper 26 (1979) and Opt. Eng.
**20,**\ 651-657 (1981)

[A4] S.M. Pizer: Intensity mappings: linearization, image-based,
user-controlled *.*\ Proc. SPIE **271**, 21-27 (1981)

[A5] S.M. Pizer: Intensity mappings to linearize display devices
*.*\ Comp. Graph. Image. Proc. **17**, 262-268 (1981)

[A6] R.E. Johnston, J.B. Zimmerman, D.C. Rogers, and S.M. Pizer:
Perceptual standardization *.*\ Proc. SPIE **536**, 44-49 (1985)

[A7] R.C. Cromartie, R.E. Johnston, S.M. Pizer, D.C. Rogers:
Standardization of electronic display devices based on human perception
*.*\ University of North Carolina at Chapel Hill, Technical Report
88-002, Dec. 1987

[A8] B. M. Hemminger, R.E. Johnston, J.P. Rolland, K.E. Muller:
Perceptual linearization of video display monitors for medical image
presentation *.*\ Proc. SPIE **2164**, 222-241 (1994)

[A9] CIE 1976

