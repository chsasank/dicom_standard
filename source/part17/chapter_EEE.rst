.. _chapter_EEE:

Intravascular OCT Image (Informative)
=====================================

.. _sect_EEE.1:

Purpose of This Annex
---------------------

The purpose of this annex is to explain key IVOCT FOR PROCESSING
parameters, describe the relationship between IVOCT FOR PROCESSING and
FOR PRESENTATION images. It also explains Intravascular Longitudinal
Reconstruction.

.. _sect_EEE.2:

IVOCT For Processing Parameters
-------------------------------

.. _sect_EEE.2.1:

Z Offset Correction
~~~~~~~~~~~~~~~~~~~

When an OCT image is acquired, the path length difference between the
reference and sample arms may vary, resulting in a shift along the axial
direction of the image, known as the Z Offset. With FOR PROCESSING
images, in order to convert the image in Cartesian coordinates and make
measurements, this Z Offset should be corrected, typically on a
per-frame or per-image basis. Z Offset is corrected by shifting Polar
data rows (A-lines) + OCT Z Offset Correction (0052,0030) pixels along
the axial dimension of the image.

Z Offset correction may be either a positive or negative value. Positive
values mean that the A-lines are shifted further away from the catheter
optics. Negative values mean that the A-lines are shifted closer to the
catheter optics. `figure_title <#figure_EEE.2-1>`__ illustrates a
negative Z Offset Correction.

.. _sect_EEE.2.2:

Refractive Index Correction
~~~~~~~~~~~~~~~~~~~~~~~~~~~

The axial distances in an OCT image are dependent on the refractive
index of the material that IVOCT light passes through. As a result, in
order to accurately make measurements in images derived from FOR
PROCESSING data, the axial dimension of the pixels should be globally
corrected by dividing the A-line Pixel Spacing (0052,0014) value (in
air) by the Effective Refractive Index (0052,0004) and setting the
Refractive Index Applied (0052,003A) to YES. Although not recommended,
if A-line Pixel Spacing (0052,0014) is reported in air (i.e., not
corrected by dividing by Effective Refractive Index) then the Refractive
Index Applied value shall be set to NO.

.. _sect_EEE.2.3:

Polar-Cartesian Conversion
~~~~~~~~~~~~~~~~~~~~~~~~~~

FOR PROCESSING Polar data is specified such that each column represents
a subsequent axial (z) location and each row an angular (q) coordinate.
Following Z Offset and Refractive Index Correction, Polar data can be
converted to Cartesian data by first orienting the seam line position so
that it is at the correct row location. This can be accomplished by
shifting the rows Seam Line Index (0052,0036) pixels so that its Seam
Line Location (0052,0033) is located at row "A-lines Per Frame \* Seam
Line Location / 360". Once the seam line is positioned correctly, the
Cartesian data can be obtained by remapping the Polar (z, q) data into
Cartesian (x, y) space, where the leftmost column of the Polar image
corresponds to the center of the Cartesian image.
`figure_title <#figure_EEE.2-2>`__ illustrates the Polar to Cartesian
conversion. The scan-converted frames are constructed using the Catheter
Direction of Rotation (0052,0031) Attribute to determine the order in
which the A-lines are acquired. Scan-converted frames are constructed
using A-lines that contain actual data (I.e., not padded A-lines).
Padded A-lines are added at the end of the frame and are contiguous.
`figure_title <#figure_EEE.2-2>`__ is an example of Polar to Cartesian
conversion.

.. _sect_EEE.3:

Intravascular Longitudinal Image
--------------------------------

An Intravascular Longitudinal Image (L-Mode) is a constrained
three-dimensional reconstruction of an IVUS or IVOCT Multi-frame Image.
The Longitudinal Image can be reconstructed from either FOR PROCESSING
or FOR PRESENTATION Images. `figure_title <#figure_EEE.3-1>`__ is an
example of an IVUS cross-sectional image (on the left) with a
reconstructed longitudinal view (on the right).

The Longitudinal reconstruction is comprised of a series of
perpendicular cut planes, typically consisting of up to 360 slices
spaced in degree increments. The cut planes are perpendicular to the
cross-sectional plane, and rotate around the catheter axis (I.e., center
of the catheter) to provide a full 360 degrees of rotation. A
longitudinal slice indicator is used to select the cut plane to display,
and is normally displayed in the associated cross-sectional image (e.g.,
blue arrow cursor in `figure_title <#figure_EEE.3-1>`__). A current
frame marker (e.g., yellow cursor located in the longitudinal view) is
used to indicate the position of the corresponding cross-sectional
image, within the longitudinal slice.

When pullback rate information is provided, distance measurements are
possible along the catheter axis. The Intravascular Longitudinal
Distance (0052,0028) or IVUS Pullback Rate (0018,3101) Attributes are
used along with the Frame Acquisition DateTime (0018,9074) Attribute to
facilitate measurement calculations. This allows for lesion, calcium,
stent and stent gap length measurements.
`figure_title <#figure_EEE.3-2>`__ is an example of an IVOCT
cross-sectional image (on the top), with a horizontal longitudinal view
on the bottom. The following example also illustrates how the tint
specified by the Palette Color LUT is applied to the OCT image.

`figure_title <#figure_EEE.3-3>`__ illustrates how the 2D
cross-sectional frames are stacked along the catheter longitudinal axis.
True geometric representation of the vessel morphology cannot be
rendered, since only the Z position information is known. Position (X
and Y) and rotation (X, Y and Z) information of the acquired
cross-sectional frames is unknown.

