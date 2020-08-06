.. _chapter_UU:

Macular Grid Thickness and Volume Report Use Cases (Informative)
================================================================

.. _sect_UU.1:

Introduction
------------

Ophthalmologists use OPT data to diagnose and characterize tissues and
abnormalities in transverse and axial locations within the eye. For
example, an ophthalmologist might request an OPT of the macula, the
optic nerve or the cornea in either or both eyes for a given patient.
Serial reports can be compared to monitor disease progression and
response to treatment. OPT devices produce two categories of clinical
data: B-scan images and tissue measurements.

.. _sect_UU.2:

Use of B-scan Images
--------------------

Prior to interpreting an OPT B-scan (or set of B-scans), users must
first determine if the study is of adequate quality to answer the
diagnostic question. Examples of inadequate studies include:

-  The pathology that needs to be visualized does not appear within the
   field of the scan.

-  The image quality is not sufficient to see the tissue layers of
   interest (i.e., media opacity, blink, etc).

-  The scans are not in the expected anatomic order (i.e., due to eye
   movements).

In some cases, inadequate images can be corrected by capturing another
scan in the same area. However, in other cases, the patient's eye
disease interferes with visualization of the tissues of interest making
adequate image quality impossible. Ideally, when choosing between
multiple scans of the same tissue area, physicians would have access to
information about the above questions so they can select only the best
scan(s).

The physician may then choose to view and assess each B-scan in the data
individually. When assessing OPT B-scans, ophthalmologists often
identify normal or expected tissue boundaries first, then proceed to
identify abnormal interfaces or structures next. The identification of
pathology is both qualitative (i.e., does a structure exist) and
quantitative (i.e., how thick is it). If previous scans are present for
this patient, the physician may choose to compare the most recent scan
data with prior visits. Due to workflow constraints, it may be difficult
for B-scan interpretations to happen on the same machine that captures
the images. Therefore, remote image assessment, such as image viewing in
the examining room with the patient, is optimal.

.. _sect_UU.3:

Use of Tissue Measurements
--------------------------

In addition to viewing B-scan image data, clinicians also use
quantitative measurements of tissue thicknesses or volumes extracted
automatically from the OPT images. As with image quality, the accuracy
of automated segmentation must be assessed prior to use of the numerical
measurements based on these boundaries. This is typically accomplished
by visual inspection of boundary lines placed on the OPT images but also
can be inferred from analysis confidence measurements provided by the
device software. In addition to segmentation accuracy, it is also
important to determine if the region of interest has been aligned
appropriately with the intended sampling area of the OPT.

The analysis software application segments OPT images using the raw data
of the instrument to quantify tissue optical reflectivity and location
in longitudinal scan or B-scan images. Many boundaries can be identified
automatically with software algorithms, see
`figure_title <#figure_UU.3-1>`__.

.. _sect_UU.4:

Axial Measurements
------------------

The innermost (anterior) layer of the retina, the internal limiting
membrane (ILM) is often intensely hyperreflective and defines the
innermost border of the nerve fiber layer. The nerve fiber layer (NFL)
is bounded posteriorly by the ganglion cell layer and is not visible
within the central foveal area. In high quality OPT scans, the sublamina
of the inner plexiform layer may be identifiable. The external limiting
membrane is the subtle interface between the outer nuclear layer and the
photoreceptors. The junction between the photoreceptor inner segments
and outer segments (IS/OS junction) is often intensely hyperreflective
and in time domain OPT systems, was thought to represent the outermost
boundary of the retina. Current thought, however, suggests that the
photoreceptors extend up to the next bright interface, often referred to
as the retinal pigment epithelium (RPE) interdigitation. This interface
may be more than 35 micrometers beyond the IS/OS junction. When three
high intensity lines are not present under the retina, however, this
interdigitation area may not be visible. The next bright region
typically represents the RPE cell bodies, which consist of a single
layer of cuboidal cells with reflective melanosomes oriented at the
innermost portion of the cells. Below the RPE cells is a structure
called Bruch's membrane, which is contiguous with the outer RPE cell
membrane.

The axial thickness and volume of tissue layers can be measured using
the boundaries defined above. For example, the nerve fiber layer is
typically measured from the innermost ILM interface to the interface of
the NFL with the retina. Time domain OPT systems measure retinal
thickness as the axial distance between the innermost ILM interface and
the IS/OS junction. However, high resolution OPT systems now offer the
potential to measure true retinal thickness (ILM to outermost
photoreceptor interface) in addition to variants that include tissue and
fluid that may intervene between the retina and the RPE. The RPE layer
is measured from the innermost portion of the RPE cells, which is the
hyper reflective melanin-containing layer to the outermost highly
reflective interface. Pathologic structures that may intervene between
normal tissue layers may obscure their appearance but often can be
measured using the same methods as normal anatomic layers.

.. _sect_UU.5:

En Face Measurements
--------------------

The macular grid is based upon the grid employed by the Early Treatment
of Diabetic Retinopathy Study (ETDRS) to measure area and proximity of
macular edema to the anatomic center of the macula, also called the
fovea. This grid was developed as an overlay for use with 32mm film
color transparencies and fluorescein angiograms in the seminal trials of
laser photocoagulation for the treatment of diabetic retinopathy.
Subsequently, this grid has been in common use at reading centers since
the 1970s, has been incorporated into ophthalmic camera digital
software, and has been employed in grading other macular disease in
addition to diabetic retinopathy. This grid was slightly modified for
use in Time Domain OPT models developed in the 1990s and early 2000s in
that the dimensions of the grid were sized to accommodate a 6 mm
diameter sampling area of the macula.

The grid for macular OPT is bounded by circular area with a diameter of
6 mm. The center point of the grid is the center of the circle. The grid
is divided into 9 standard subfields. The center subfield is a circle
with a diameter of 1 mm. The grid is divided into 4 inner and 4 outer
subfields by a circle concentric to the center with a diameter of 3 mm.
The inner and outer subfields are each divided by 4 radial lines
extending from the center circle to the outermost circle, at 45, 135,
225, and 315 degrees, transecting the 3 mm circle in four places. Each
of the 4 inner and 4 outer subfields is labeled by its orientation with
regard to position relative to the center of the macula - superior,
nasal, inferior, and temporal. For instance, the superior inner subfield
is the region bounded by the center circle and the 3 mm circle the 315
degree radial line, and the 45 degree radial line. The nasal subfields
are those oriented toward the midline of the patient's face, nearest to
the optic nerve head. The grids for the left and right eyes are reversed
with respect to the positions of the nasal and temporal subfields - in
viewing the grid for the left eye along the antero-posterior (Z) axis,
the nasal subfields are on the left side and in the right eye the nasal
subfields are on the right side (nasal as determined by the location of
the subfield closest to the nose).

The OPT macula thickness report consists of the thickness at the center
point of the grid, and the mean retinal thickness calculated for each of
the 9 subfields of the grid. In the context of the macular disease
considered for the diagnosis, and qualitative interpretation of
morphology from examination and OPT and/or other modalities, the
clinician uses the macula thickness report to determine if the center
and the grid subfield averages fall outside the normative range.
Monitoring of macular disease by serial grid measurements allows
assessment of disease progression and response to intervention. Serial
measurements are assessed by comparing OPT thickness or volume reports,
provided that the grids are appropriately centered upon the same
location in the macula for each visit.

The center point of the grid should be aligned with the anatomic center
of the macula, the fovea. This can be approximated by having the patient
fixate upon a target coincident with the center of the grid. However,
erroneous retinal thickness measurements are obtained when the center of
the grid is not aligned with the center of the macula. This may occur in
patients with low vision that cannot fixate upon the target, or in
patients that blink or move fixation during the study. To determine the
expected accuracy of inter-visit comparisons, clinicians would benefit
from knowing the alignment accuracy of the OPT data from the two visits.
Ophthalmologists may also want to customize locations on the fundus to
be monitored at each visit.

The following figure illustrates how the content items of the Macular
Grid Thickness and Volume Report are related to the ETDRS Grid. Figure
shown is not drawn to scale.

.. _sect_UU.6:

Interpretation of OPT
---------------------

The process of evaluation of diabetic macular edema will help illustrate
the role of the OPT macula thickness report. In diabetic macular edema
there is a breakdown in the blood retina barrier, which can lead to
focal and/or diffuse edema (or thickening) of the macula. The report of
the thickness of each subfield area of the macula grid will help direct
treatment. For instance, laser treatment to a specific thickened
quadrant would be expected to reduce the thickness of retina in the
treated zone. Serial comparisons of OPT thicknesses should demonstrate a
reduction in thickness in the successfully treated zone. A zone that
subsequently became thicker on follow-up scans may warrant further
treatment. In addition to an expected local response to specific zonal
treatment such as laser, there are treatments with drugs and biologics
that are less localized. For instance, the injection of intravitreal
drugs in a successfully treated eye would be expected to have a global
reduction of thickness in all zones with DME. Patients with severe
retinal disease may lose the ability to fixate making the acquisition of
OPT images to represent a specific zone less reliable.

