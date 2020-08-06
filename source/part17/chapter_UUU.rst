.. _chapter_UUU:

Ophthalmology Use Cases (Informative)
=====================================

.. _sect_UUU.1:

Wide Field Ophthalmic Use Cases
-------------------------------

Any 2-dimensional representation of a 3-dimensional object must undergo
some kind of projection or mapping to form the planar image. Within the
context of imaging of the retina, the eye can be approximated as a
sphere and mathematical cartography can be used to understand the impact
of projecting a spherical retina on to a planar image. When projecting a
spherical geometry on a planar geometry, not all metric properties can
be retained at the same time; some distortion will be introduced.
However, if the projection is known it may be possible to perform
calculations "in the background" that can compensate for these
distortions.

The example in `figure_title <#figure_UUU.1-1>`__ shows an ultra-wide
field image of the human retina. The original image has been remapped to
a stereographic projection according to an optical model of the scanning
laser ophthalmoscope it was captured on. Two circles have been annotated
with an identical pixel count. The circle focused on the fovea (A) has
an area of 4.08 mm\ :sup:`2` whereas the circle nasally in the periphery
(B) has an area of 0.97 3mm\ :sup:`2`, both as measured with the Area
Measurement using the Stereographic Projection method. The difference in
measurement is more than 400%, which indicates how measurements on large
views of the retina can be deceiving.

The fact that correct measurement on the retina in physical units is
difficult to do is acknowledged in the original DICOM OP SOP Classes in
the description of the Pixel Spacing (0028,0030) tag.

.. note::

   These values are specified as nominal because the physical distance
   may vary across the field of the images and the lens correction is
   likely to be imperfect.

The following use cases are examples of how the DICOM Wide Field
Ophthalmology Photography objects may be used.

.. _sect_UUU.1.1:

Clinical Use Cases
~~~~~~~~~~~~~~~~~~

.. _sect_UUU.1.1.1:

Routine Wide Field Image For Surveillance For Diabetic Retinopathy
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

On routine wide-field imaging for annual surveillance for diabetic
retinopathy a patient is noted to have no retinopathy, but demonstrates
a pigmented lesion of the mid-periphery of the right eye. Clinically
this appears flat or minimally elevated, irregularly pigmented without
lacunae, indistinct margins on two borders, and has a surface that is
stippled with orange flecks. The lesion is approximately 3 X 5 DD. This
lesion appears clinically benign, but requires serial comparison to rule
out progression requiring further evaluation. Careful measurements are
obtained in 8 cardinal positions using a standard measurement tool in
the reading software that calculates the shortest distance in mm between
these points. The patient was advised to return in six months for repeat
imaging and serial comparison for growth or other evidence of malignant
progression.

.. _sect_UUU.1.1.2:

Patient With Myopia
^^^^^^^^^^^^^^^^^^^

A patient with a history of high myopia has noted recent difficulties
descending stairs. She believes this to be associated with a new onset
blind spot in her inferior visual field of both eyes, right eye greater
than left. On examination she shows a bullous elevation of the retina in
the superior periphery of both eyes due to retinoschisis, OD>OS. There
is no evidence of inner or outer layer breaks, and the maculae are not
threatened, so a decision is made to follow closely for progression
suggesting a need for intervention. Wide field imaging of both fundi is
obtained, with clear depiction of the posterior extension of the
retinoschisis. Careful measurements of the shortest distance in mm
between the posterior edge of the retinal splitting and the fovea is
made using the diagnostic display measurement tool, and the patient was
advised to return in four months for repeat imaging and serial
comparison of the posterior location of the retinoschisis.

.. _sect_UUU.1.1.3:

Patient With Diabetes
^^^^^^^^^^^^^^^^^^^^^

Patients with diabetes are enrolled in a randomized clinical trial to
prospectively test the impact of disco music on the progression of
capillary drop out in the retinal periphery. The retinal capillary
drop-out is demonstrated using wide-field angiography with expanse of
this drop-out determined serially using diagnostic display measurement
tools, and the area of the drop-out reported in mm\ :sup:`2`. Regional
areas of capillary drop out are imaged such that the full expanse of the
defect is captured. In some cases this involves eccentric viewing with
the fovea positioned in other than the center of the image. Exclusion
criteria for patient enrollment include refractive errors greater than
8D of Myopia and 4D of hyperopia.

.. _sect_UUU.1.1.4:

Patient With Age Related Macular Degeneration (ARMD)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Patients with ARMD and subfoveal subretinal neovascular membranes but
refusing intravitreal injections are enrolled in a randomized clinical
trial to test the efficacy of topical anti-VEGF (Vascular Endothelial
Growth Factor) eye drops on progression of their disease. The patients
are selected such that there is a wide range of lesion size (area
measured in mm\ :sup:`2`) and retinal thickening. This includes patients
with significant elevation of the macula due to subretinal fluid.

.. _sect_UUU.1.2:

Stereographic Projection (SP)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Every 2-dimensional image that represents the back of the eye is a
projection of a 3-dimensional object (the retina) into a 2-dimensional
space (the image). Therefore, every image acquired with a fundus camera
or scanning laser ophthalmoscope is a particular projection. In
ophthalmoscopy, part of the spherical retina (the back of the eye can be
approximated by a sphere) is projected to a plane, i.e., a 2-dimensional
image.

The projection used for a specific retinal image depends on the
ophthalmoscope; its optical system comprising lenses, mirrors and other
optical elements, dictates how the image is formed. These projections
are not well-characterized mathematical projections, but they can be
reversed to return to a sphere. Once in spherical geometry, the image
can then be projected once more. This time any mathematical projection
can be used, preferably one that enables correct measurements. Many
projections are described in the literature, so which one should be
choosen?

Certain projections are more suitable for a particular task than others.
Conformal projections preserve angle, which is a property that applies
to points in the plane of projection that are locally distortion-free.
Practically speaking, this means that the projected meridian and
parallel intersect through a point at right angles and are equiscaled.
Therefore, measuring angles on the 2-dimensional image yields the same
results as measuring these on the spherical representation, i.e., the
retina. Conformal projections are particularly suitable for tasks where
the preservation of shapes is important. Therefore, the stereographic
projection explained in `figure_title <#figure_UUU.1.2-1>`__ can be used
for images on which to perform anatomically-correct measurements. The
stereographic projection has the projection plane intersect with the
equator of the eye where the fovea and cornea are poles. The points
Fovea, p and q on the sphere (retina) are projected onto the projection
plane (image in stereographic projection) along lines through the cornea
where they intersect with the project plane creating points *F′*,
*p′*\ and *q′*\ respectively.

Note that in the definition of stereographic projection the fovea is
conceptually in the center of the image. For the mathematics below to
work correctly, it is critical that each image is projected such that
conceptually the fovea is in the center, even if the fovea is not in the
image. This is not difficult to achieve as a similar result is achieved
when creating a montage of fundus images; each image is re-projected
relative to the area it covers on the retina. Most montages place the
fovea in the center. An example of two images of the same eye in
`figure_title <#figure_UUU.1.2-2>`__ and
`figure_title <#figure_UUU.1.2-3>`__ taken from different angles and
then transformed to adhere to this principle are in
`figure_title <#figure_UUU.1.2-4>`__ and
`figure_title <#figure_UUU.1.2-5>`__ respectively.

Furthermore the mathematical "background calculations" are well known
for images in stereographic projection. Given points (pixels) on a
retinal image, these can be directly located as points on the sphere and
geometric measurements, i.e., area and distance measurements, performed
on the sphere to obtain the correct values. The mathematical details
behind the calculations for locating points on a sphere are presented in
.

.. _sect_UUU.1.2.1:

Distance
^^^^^^^^

The shortest distance between two points on a sphere lies on a "great
circle", which is a circle on the sphere's surface that is concentric
with the sphere. The great circle section that connects the points (the
line of shortest distance) is called a geodesic. There are several
equations that approximate the distance between two points on the back
of the eye along the great circle through those points (the arc length
of the geodesic), with varying degrees of accuracy. The simplest method
uses the "spherical law of cosines". Let *λ\ s, ϕ\ s; λ\ f, ϕ\ f* be the
longitude and latitude of two points *s* and *f*, and *∆λ ≡
\|λ\ f\ −λ\ s\ \|* the absolute difference of the longitudes, then the
central angle is defined as

where the central angle is the angle between the two points via the
center of the sphere, e.g., angle *a* in
`figure_title <#figure_UUU.1.2-6>`__. If the central angle is given in
radians, then the distance *d*, known as *arc length*, is defined as
where *R* is the radius of the sphere.

This equation leads to inaccuracies both for small distances and if the
two points are opposite each other on the sphere. A more accurate method
that works for all distances is the use of the Vincenty formulae. Now
the central angle is defined as

`figure_title <#figure_UUU.1.2-6>`__ is an example of a polygon made up
of three geodesic *G\ a*, *G\ b*, *G\ c*, describing the shortest
distances on the sphere between the polygon vertices *x\ 1*, *x\ 2*, *x*
:sub:`3`. Angle\ *γ* is the angle on the surface between geodesics
*G\ a* and *G\ b*. Angle *a* is the central angle (angle via the
sphere's center) of geodesic *G\ a*.

If the length of a path on the image (e.g., tracing of a blood vessel)
is needed, this can be easily implemented using the geodesic distance
defined above, by dividing the traced path into sections with lengths of
the order of 1-5 pixels, and then calculating and summing the geodesic
distance of each section separately. This works because for short enough
distances, the geodesic distance is equal to the on-image distance. Note
that sub-pixel accuracy is required.

.. _sect_UUU.1.2.2:

Area
^^^^

To measure an area *A* defined by a polygon on the surface of the sphere
where surface angle (such as *γ* in
`figure_title <#figure_UUU.1.2-6>`__) α\ :sub:`i` for *i=1,…,n* for *n*
angles internal to the polygon and *R* the radius of the sphere, we use
the following formula, which makes use of the "angle excess".

This yields a result in physical units (e.g., mm\ :sup:`2` if *R* was
given in mm), but if *R\ 2* is omitted in the above formula, a result is
obtained in units relative to the sphere, in steradians (sr), the unit
of solid angle.

.. _sect_UUU.1.2.3:

Angle
^^^^^

In practice, if the length of the straight arms of the calipers used to
measure surface angle (such as *γ* in
`figure_title <#figure_UUU.1.2-6>`__) are short then the angle measured
on the image is equivalent to its representation on the sphere, which is
a direct result of using the stereographic projection as it is
conformal.

.. _sect_UUU.1.3:

Introduction to 2D to 3D Map For Wide Field Ophthalmic Photography
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A 2D to 3D map includes 3D coordinates of all or a subset of pixels
(namely coordinate points) to the 2D image. Implementations choose the
interpolation type used, but it is recommended to use a spline based
interpolation. See `figure_title <#figure_UUU.1.3-1>`__.

Pixels' 3D coordinates could be used for different analyses and
computations e.g., measuring the length of a path, and calculating the
area of region of interest, 3D computer graphics, registration, shortest
distance computation, etc. Some examples of methods using 3D coordinates
are listed in the following subsections.

.. _sect_UUU.1.3.1:

Measuring the Length of a Path
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Let the path between points *A*, and *B* be represented by set of *N*
following pixels *P={p\ i}* and *p\ 0\ =A* and *p\ N\ =B*. The length of
this path can be computed from the partial lengths between path points
by:

where:

and where *x\ i, y\ i, z\ i* are the 3D coordinates of the point *p\ i*
which is either available in the 2D to 3D map if *p\ i* is a coordinate
point or it is computed by interpolation. Here it is assumed that the
sequence of path points is known and the path is 4- or 8-connected
(i.e., the path points are neighbors with no more than one pixel
distance in horizontal, vertical, or diagonal direction). It is
recommendable to support sub-pixel processing by using interpolation.

.. _sect_UUU.1.3.2:

Shortest Distance Between Two Points
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Shortest distance between two points along the surface of a sphere,
known as the great circle or orthodromic distance, can be computed from:

Where *r* is the radius of the sphere and the central angle (Δσ) is
computed from the Cartesian coordinate of the two points in radians.
Here *n\ 1* and *n\ 2* are the normals to the ellipsoid at the two
positions. The above equations can also be computed based on longitudes
and latitudes of the points.

However, the shortest distance in general can be computed by algorithms
such as Dijkstra, which computes the shortest distance on graphs. In
this case the image is represented as a graph in which the nodes refer
to the pixels and the weight of edges is defined based on the
connectivity of the points and their distance.

.. _sect_UUU.1.3.3:

Computing The Area of A Region of Interest
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Let *R* be the region of interest on the 2D image and it is tessellated
by set of unit triangles *T={T\ i}*. By unit triangle we refer to
isosceles right triangle that the two equal sides have one pixel
distance (4-connected neighbors). The area of the region of interest can
be computed as the sum of partial areas of the unit triangles in 3D. Let
*{*\ **a\ i**\ *,\ *\ **b\ i**\ *,\ *\ **c\ i**\ *}* be the 3D
coordinates of the three points of unit triangle *T\ i*. The 3D area of
this triangle is

and the total area of R is:

Where (‖ … ‖) and ( x ) refer to the magnitude and cross product,
respectively.

Consider that **a\ i**, **b\ i** and **c\ i** are the 3D coordinates not
the 2D indices of the unit triangle points on the image.

.. _sect_UUU.1.3.4:

Transformation Method Code Sequence
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

If Transformation Method Code Sequence (0022,1512) is (111791, DCM,
"Spherical projection") is used then all coordinates in the Two
Dimensional to Three Dimensional Map Sequence (0022,1518) are expected
to lie on a sphere with a diameter that is equal to Ophthalmic Axial
Length (0022,1019).

The use of this model for representing the 3D retina enables the
calculation of the shortest distance between two points using great
circles as per section UUU.1.3.2.

.. _sect_UUU.2:

Relationship Between Ophthalmic Tomography Image and Ophthalmic Optical Coherence Tomography B-scan Volume Analysis IODs
------------------------------------------------------------------------------------------------------------------------

This Section provides examples of the relationship between the
Ophthalmic Tomography Image SOP Instance(s) and Ophthalmic Optical
Coherence Tomography B-scan Volume Analysis SOP Instance(s).

Below is a typical example.

-  Ophthalmic Tomography Image SOP Instance UID is "1.2.3.4.5" and
   contains five frames.

-  Ophthalmic Optical Coherence Tomography B-scan Volume Analysis SOP
   Instance encodes five frames (e.g., one frame for each ophthalmic
   tomography frame).

-  References are encoded via the Per-frame Functional Groups Sequence
   (5200,9230) using Attributes Derivation Image Sequence (0008,9124)
   and Source Image Sequence (0008,2112).

Below is a more complex example.

-  Ophthalmic TomographyImage SOP Instance UID is "2.3.4.5" and contains
   3 frames.

-  Ophthalmic TomographyImage SOP Instance UID is "1.6.7.8.9" and
   contains 2 frames.

-  Ophthalmic Optical Coherence Tomography B-scan Volume Analysis SOP
   Instance encodes five frames (e.g., one frame for each Ophthalmic
   TomographyFrame from the two Ophthalmic Tomography Image SOP
   Instances).

.. _sect_UUU.3:

Ophthalmic Tomography Angiography Examples
------------------------------------------

OCT en face images are derived from images obtained using OCT technology
(i.e., structural OCT volume images plus angiographic flow volume
information). With special image acquisition sequences and post hoc
image processing algorithms, OCT-A detects the motion of the blood cells
in the vessels to produce images of retinal and choroidal blood flow
with capillary level resolution. En face images derived from these
motion contrast volumes are similar to images obtained in retinal
fluorescein angiography with contrast dye administered intravenously,
though differences are observed when comparing these two modalities.
This technology enables a high resolution visualization of the retinal
and choroidal capillary network to detect the growth of abnormal blood
vessels to provide additional insights in diagnosing and managing a
variety of retinal diseases including diabetic retinopathy, neovascular
age-related macular degeneration, retinal vein occlusion and others.

The following are examples of how the ophthalmic tomography angiography
DICOM objects may be used.

.. _sect_UUU.3.1:

Clinical Examples
~~~~~~~~~~~~~~~~~

.. _sect_UUU.3.1.1:

Diabetic Macular Ischemia
^^^^^^^^^^^^^^^^^^^^^^^^^

A 54 year old female patient with an 18 year history of DM2 presents
with unexplained painless decreased visual acuity in both eyes. The
patient was on hemodialysis (HD) for diabetes related renal failure. She
had a failed HD shunt in the right arm and a functioning shunt in the
left. SD-OCT testing showed no thickening of the macula. Because of her
renal failure and HD history IVFA was deferred and OCT angiography of
the maculae was performed. This showed significant widening of the
foveal avascular zone (FAZ) explaining her poor visual acuity and
excluding treatment opportunities.

.. _sect_UUU.3.1.2:

Age Related Macular Degeneration
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

A 71 Year Old Male Patient Presents With A 3 Month History of Decreased
Visual Acuity and Distorted Vision in The Right Eye. He Demonstrates A
Well-defined Elevation of The Deep Retina Adjacent to The Fovea Od by
Biomicroscopy That Correlates to A Small Pigment Epithelial Detachment
(ped) Shown by Sd-oct. OCT Angiography Demonstrated A Subretinal
Neovascular Network in The Same Area. This Was Treated With Intravitreal
Anti-vegf Injection Monthly For Three Months With Resolution of The Ped
and Incremental Regression of The Subretinal Neovascular Membrane by
Point to Point Registration OCT Angiography and Finally Non-perfusion of
The Previous Srn.

.. _sect_UUU.3.1.3:

Branch Retinal Vein Occlusion
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

A 59 y/o male patient with hypertension and long smoking history
presents with a six week history of painless decrease in vision in the
right eye. Ophthalmoscopy showed dilated and tortuous veins inferior
temporally in the right eye with a superior temporal distribution of
deep retinal hemorrhages that extended to the mid-periphery, but did not
include the macula. SD-OCT showed thickening of the macula and OCT
angiography showed rarefaction of the retinal capillaries consistent
with ischemic branch retinal vein occlusion and macular edema.

.. _sect_UUU.3.2:

Research Examples
~~~~~~~~~~~~~~~~~

.. _sect_UUU.3.2.1:

Proliferative Diabetic Retinopathy
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

A 38-year-old male patient with 26 year history of type 1 diabetes
examined for evaluation of 10-day history of scant vitreous hemorrhage
due to neovascularization of the optic disc.

