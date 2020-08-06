.. _chapter_III:

Ophthalmic Thickness Map Use Cases (Informative)
================================================

.. _sect_III.1:

Introduction
------------

Several ophthalmic devices produce thickness and/or height measurements
of certain anatomical features of the posterior eye (e.g., optic nerve
head topography, retinal thickness map, etc.). The measurements are
mapped topographically as monochromatic images with pseudo color maps,
and used extensively for diagnostic purposes by clinicians.

.. _sect_III.2:

Macular Retinal Thickness Example
---------------------------------

Quantitative ophthalmic OCT image analysis provides essential thickness
measurement data of the retina. In the clinical practice two thickness
parameters are commonly used: total retinal thickness (TR) in macular
region and retinal nerve fiber layer thickness (RNFL) in optic nerve
head (ONH) region. TR is widely applied to assess various retinal
pathologies involving macula (e.g., cystoid macular edema, age-related
macular degeneration, macular hole, etc.). The RNFL thickness
measurement is most commonly used for glaucoma assessment.

`figure_title <#figure_III.2-1>`__ is an example of 2D TR map computed
on a 3D OCT cube data from a healthy eye. The color bar on the left
provides a color-to-thickness representation to allow interpretation of
the false color coded 2D thickness map in the middle. The image on the
right shows one OCT frame representing a retinal cross section along the
red line (across the middle of the thickness map). TR is defined as the
thickness between internal limiting membrane (white line on the OCT
frame on the right) and RPE/Choroid interface (blue line on the OCT
frame). These two borders are automatically detected using a
segmentation algorithm applied to the entire 3D volume.

.. _sect_III.3:

RNFL Example
------------

`figure_title <#figure_III.3-1>`__ is an example of a 2D RNFL map
computed on a 3D OCT cube data from a healthy eye. The figure layout is
the same as the previous example. The RNFL thickness is limited to the
thickness of this single layer of the retina that is comprised of the
ganglion cell axons that course to the optic nerve head and exit the eye
as the optic nerve. Note that this image depicts a BMP mask in the
center of the map where the optic nerve head (ONH) exists and no RNFL
measurements can be obtained. In this example, the mask is displayed as
a black area, which does not contain any thickness information (not zero
micron thickness). Since the color bar representation is not relevant at
the ONH, common practice is to mask it to avoid confusion or
misinterpretation due to meaningless thickness data in this area.

.. _sect_III.4:

Diabetic Macular Edema Example
------------------------------

A 48 year old Navajo male with diabetes, decreased visual acuity and
fundoscopic stigmata of diabetic retinopathy receives several tests to
assess his likelihood of macular edema. Optical coherence tomography
(OPT) is performed to assess the thickness of the retina in the macular
area. This is performed with retinal thickness depicted by ophthalmic
mapping. The results is an Ophthalmic Thickness Map SOP instance with
the Ophthalmic Thickness Mapping Type Code Sequence (0022,1436) set to
"Absolute Ophthalmic Thickness" and the Measurements Units Code Sequence
(0040,08EA) in the Real World Value Mapping Macro, set to "micrometer".
The OPT image is also referenced in Attribute Referenced Instance
Sequence (0008,114A).

Since the thickness of the macula varies normally based upon a number of
dependencies such as age, gender, race, etc. Interpretation of the
retinal thickness in any given patient may be done in the context of
normative data that accounts for these variables. The thickness data
used to generate the thickness map is analyzed using a manufacturer
specific algorithm for comparison to normative data relevant to this
specific patient. The results of this analysis is depicted on a second
thickness "map" (second SOP Instance) showing each pixel's variation
from normal in terms of confidence that the variation is real and not
due to chance. Specific confidence levels are then depicted by arbitrary
color mapping registered to the fundus photograph. This is typically
noted as the percent probability that the variation is abnormal e.g., p
>5%, p <5%, p <1% etc. The results is an Ophthalmic Thickness Map SOP
instance with the Ophthalmic Thickness Mapping Type Code Sequence
(0022,1436) set to "Thickness deviation category from normative data".
Mapping the "categories" to a code concept is accomplished via Attribute
Pixel Value Mapping to Coded Concept Sequence (0022,1450).

.. _sect_III.5:

Glaucoma Example
----------------

A patient was presented with normal visual acuity OU (both eyes),
intraocular pressures (IOP) of 18 mm Hg OU (both eyes), and 0.7 C/D OD
(right eye) and 0.6 C/D ratio OS (left eye). Corneal pachymetry showed
slight thinning in both eyes at 523µ OD (right eye) and 530µ OS (left
eye). Static threshold perimetry testing showed nonspecific defects OU
(both eyes) and was unreliable due to multiple fixation losses. Confocal
scanning laser ophthalmoscopy produced OPM topographic representations
of both optic nerves suggestive of glaucoma. The contouring of the optic
nerve head (ONH) in the left eye showed a slightly enlarged cup with
diffuse thinning of the superior neural rim. In the right eye, there was
greater enlargement of the cup and sloping of the cup
superior-temporally with a clear notch of the neural rim at the 12:30
position. Corneal compensated scanning laser polarimetry was performed
bilaterally. Analysis of the OPM representation of the retinal nerve
fiber layer (RNFL) thickness map showed moderate retinal nerve fiber
loss with accentuation at the superior pole bilaterally. The patient was
diagnosed with normal tension glaucoma and started on a glaucoma
medication. Follow-up examinations showed stable reduction in his IOP to
11 mm Hg OU (both eyes) and no further progression of his ONH or RNFL
defects.

.. _sect_III.6:

Retinal Thickness Definition
----------------------------

Using OCT technology, there are typically 2 major highly reflective
bands generally visible; inner and outer highly reflective bands (IHRB
and OHRB).

The inner band corresponds to the inner portion of the retina, which
consists of ILM (internal limiting membrane), RNFL (retinal nerve fiber
layer), GCL (ganglion cell layer), IPL (inner plexiform layer), INL
(inner nuclear layer), and OPL (outer plexiform layer). In terms of the
reflectivity, they present a high-low-high-low-high pattern, in general.
Presumably RNFL, IPL, and OPL are the highly reflective layers and GCL
and INL are of low reflectivity. ILM itself may or may not be visible in
OCT images (depending on the scanning beam incidence angle), but for
convenience it is used to label the vitreo-retinal interface.

The outer band is considered as the RPE (retinal pigment epithelium)
/Choroid complex that consist of portion of photoreceptor, RPE, Bruch's
membrane, and portion of choroid. Within the RPE/Choroid complex, there
are 3 highly reflective interfaces identifiable, presumably
corresponding to IS/OS (photoreceptor inner/out segment junction), RPE,
and Bruch's membrane.

Clinically 3 retinal thickness measurements are generally acknowledged
and utilized; RNFL thickness, GCC (ganglion cell complex) thickness, and
total retinal thickness.

RNFL thickness is defined as the distance between ILM and outer
interface of the inner most highly reflective layer presumably RNFL.

GCC thickness is defined as the distance between ILM and the outer
interface of the second inner highly reflective layer presumably the
outer border of inner plexiform layer (IPL).

Total retinal thickness definition varies among OCT manufacturers. The
classic definition is the distance between ILM and the first highly
reflective interface (presumably IS-OS) in the OHRB (Total retinal
thickness (ILM to IS-OS) ). A second definition is the distance between
ILM and the second highly reflective interface (presumably RPE) in the
OHRB (Total retinal thickness (ILM to RPE) ). A third definition is the
distance between ILM and the third highly reflective interface
(presumably Bruch's membrane) in the OHRB (Total retinal thickness (ILM
to BM) ).

.. _sect_III.7:

Thickness Calculations Between Various Devices
----------------------------------------------

When interpreting quantitative data obtained from imaging devices,
comparing may be an issue. Using different devices manufactured by
different companies usually ends up with non-comparable measurements
because they use different optics and different algorithms to make
measurements.

Currently there are multiple SD-OCT devices independently manufactured,
and data comparability has become problematic. When patients change
doctors or otherwise receive care from more than one provider,
previously acquired data may occur on different devices and become
almost useless simply because the present doctor has no access to the
same device. Another problem occurs with longitudinal assessments on the
same device after it has undergone upgrade to a newer generation. In
this case new baseline measurements must be obtained due to
incomparability of the data (this happens even for the same make
different generation devices). Attempts to normalize the measurements
have been unsuccessful.

The manufacturer, model, serial number, and software version information
are available in the Equipment Module, and is very important for
considering the significant importance of the information to the
quantitative data between various SOP Instances.

