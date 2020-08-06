.. _chapter_CCC:

Ophthalmic Axial Measurements and Intraocular Lens Calculations Use Cases (Informative)
=======================================================================================

.. _sect_CCC.1:

Axial Measurements
------------------

An axial measurements device is used to take axial measurements of the
eye, from the anterior surface of the cornea to either the surface of
the retina (ultrasound) or the retinal photoreceptors (optical). The
axial measurements are typically expressed in mm (Ophthalmic Axial
Length (0022,1010). Currently these measurements are taken using
ultrasound or laser light. The measurements are used in calculation of
intraocular lens power for cataract surgery. Axial measurements devices
and software on other systems perform intraocular lens power
calculations using the axial measurements in addition to measurements
from other sources (currently by manual data entry, although importation
from other software systems is expected in the future).

When the natural lens of the eye turns opaque it is called a cataract.
The cataract is surgically removed, and a synthetic intraocular lens is
placed where the natural lens was before. The power of the lens that is
placed determines what the patient's refractive error will be, meaning
what power his glasses will need to be to maximize vision after surgery.

Axial measurements devices provide graphical displays that help
clinicians to determine whether or not the probe used in taking the
measurements is aligned properly. Annotations on the display provide
information such as location of gates that assists the clinician in
assessing measurement quality. High, fairly even waveform spikes suggest
that the measurement producing a given graph is likely to be reliable.
The quality of the graphical display is one of the factors that a
clinician considers when choosing which axial length measurement to use
in calculating the correct intraocular lens power for a given patient.

.. _sect_CCC.2:

Intraocular Lens Calculations Introduction
------------------------------------------

Axial measurements devices and software on other systems perform
intraocular lens power calculations for cataract surgery patients. The
power selection of intraocular lens to place in a patient's eye
determines the refractive correction (e.g., glasses, contact lenses,
etc.) the patient will require after cataract surgery.

The data input for these calculations consists of ophthalmic axial
length measurements (one dimensional ultrasound scans that are called
"A-scans" in the eye care domain) and keratometry (corneal curvature)
measurements in addition to constants and sometimes others kinds of
measurements. The data may come from measurements performed by the
device, on which the intraocular lens calculation software resides, or
from manual data entry, or from an external source. There are a number
of different formulas and constants available for doing these
calculations. The selection of formula to use is based on clinician
preference and on patient factors such as the axial length of the eye.
The most commonly used constants, encoded by Concept Name Code Sequence
(0040,A043) using , are a function of the model of intraocular lens to
be used.

The most commonly used formulas, encoded by IOL Formula Code Sequence
(0022,1029) using , for intraocular lens calculation are inaccurate in a
patient who has had refractive surgery, and numerous other formulas are
available for these patients. Since most of them have not been validated
to date, they were not included in this document.

Intraocular lens calculation software typically provides tabular
displays of intraocular lens power in association with each lens's
predicted refractive error (e.g., glasses, contact lenses, etc).

Courtesy; National Eye Institute, National Institutes of Health;
ftp://ftp.nei.nih.gov/eyean/eye_72.tif

Courtesy; National Eye Institute, National Institutes of Health;
ftp://ftp.nei.nih.gov/eyedis/EDA13_72.tif

This file is licensed under the Creative Commons Attribution Share Alike
2.5 License, Author is Rakesh Ahuja, MD
(http://en.wikipedia.org/wiki/Image:Posterior_capsular_opacification_on_retroillumination.jpg)

.. _sect_CCC.3:

Output of An Ultrasound A-scan Device
-------------------------------------

`figure_title <#figure_CCC.3-1>`__ demonstrates an A-scan waveform -
produced by an ultrasound device used for ophthalmic axial length
measurement. This is referenced in the Ophthalmic Axial Measurements IOD
in Referenced Ophthalmic Axial Length Measurement QC Image Sequence
(0022,1033).

Time (translated into distance using an assumed velocity) is on the
x-axis, and signal strength is on the y-axis. This waveform allows
clinicians to judge the quality of an axial length measurement for use
in calculating the power of intraocular lens to place in a patient's eye
in cataract surgery. `figure_title <#figure_CCC.3-1>`__ above
demonstrates a high quality scan, with tall, even spikes representing
the ocular structures of interest. This tells the clinician that the
probe was properly aligned with the eye. The first, double spike on the
left represents anterior cornea followed by posterior cornea. The second
two, more widely spaced spikes represent anterior and posterior lens.
The first tall spike on the right side of the display is the retinal
spike, and the next tall spike to the right is the sclera. Smaller
spikes to the far right are produced by orbital tissues. Arrows at the
bottom of the waveform indicate the location of gates, which may be
manually adjusted to limit the range of accepted values. Note that in
the lower right corner of the display two measurements are recorded. In
the column labeled AXL is an axial length measurement, which on this
device is the sum of the measurements for ACD (anterior chamber depth),
lens, and VCD (vitreous chamber depth). The measured time value for each
of the segments and a presumed velocity of sound for that segment are
used to calculate the axial length for that segment. An average value
for each column is displayed below along with the standard deviation of
measurements in that column. The average axial length is the axial
length value selected by this machine, although often a clinician will
make an alternative selection.

.. _sect_CCC.4:

Output of An Optical A-scan Device
----------------------------------

`figure_title <#figure_CCC.4-1>`__ demonstrates the waveform-output of a
partial coherence interferometry (PCI) device used for optical
ophthalmic axial length measurement. This is referenced in the
Ophthalmic Axial Measurements IOD in Referenced Ophthalmic Axial Length
Measurement QC Image Sequence (0022,1033).

Physical distance is on the x axis, and signal strength is on the y
axis. What is actually measured is phase shift, determined by looking at
interference patterns of coherent light. Physical distance is calculated
by dividing "optical path length" by the "refractive group index" -
using an assumed average refractive group index for the entire eye. The
"optical path length" is derived from the phase shift that is actually
observed. Similar to ultrasound, this waveform allows clinicians to
judge the quality of an axial length measurement.

`figure_title <#figure_CCC.4-1>`__ above demonstrates a high quality
scan, with tall, straight spikes representing the ocular axial length.
The corneal spike is suppressed (outside the frame on the left hand
side) and represents the reference 0 mm. The single spike on this
display represents the signal from the retinal pigment epithelium (RPE)
and provides the axial length measurement value (position of the circle
marker). Sometimes smaller spikes can be observed on the left or right
side of the RPE peak. Those spikes represent reflections from the
internal limiting membrane (ILM,150-350 µm before RPE) or from the
choroid (150-250 µm behind RPE) respectively.

Because all classical IOL power calculation formulas expect axial
lengths measured to the internal limiting membrane (as provided by
ultrasound devices), axial length measurements obtained with an optical
device to the retinal pigment epithelium are converted to this
convention by subtracting the retinal thickness.

`figure_title <#figure_CCC.4-1>`__ above displays five axial length
measurements obtained for each eye (one column for each eye) and the
selected axial length value is shown below the line.

.. _sect_CCC.5:

IOL Calculation Results Example
-------------------------------

`figure_title <#figure_CCC.5-1>`__ demonstrates a typical display of IOL
(intraocular lens) calculation results.

On the right the selected target refractive correction (e.g., glasses,
contact lenses, etc.) is -0.25 diopters. At the top of the table three
possible intraocular lens models are displayed, along with the constants
() specific to those lens models. Each row in that part of the table
displays constants required for a particular formula. In this example
the Holladay formula has been selected by the operator, and results are
displayed in the body of the table below. Calculated intraocular lens
powers are displayed with the predicted postoperative refractive error
(e.g., glasses, contact lenses, etc.) for each lens. K1 and K2 on the
right refer to the keratometry values (corneal curvature), in diopters,
used for these calculations.

