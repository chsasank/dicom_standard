.. _chapter_FFFF:

Advanced Blending Presentation State Storage Encoding Example (Informative)
===========================================================================

This section illustrates the usage of the Advanced Blending Presentation
State for a functional MRI study.

.. _sect_FFFF.1:

Introduction
------------

Quantitative imaging provides measurements of physical properties, in
vivo and non-invasively, for research and clinical practice. DICOM
support for parametric maps provides a structure for organizing these
results as an extension of the already widely-used imaging standard. The
addition of color LUT support for parametric maps bridges the gap
between data handling and visualization.

An example of quantitative imaging in clinical practice today is the use
of MRI, PET and other modalities in brain mapping for diagnostic
assessment in pre-treatment planning for tumor, epilepsy, arterio-venous
malformations (AVMs) and other conditions. MR Diffusion tensor imaging
(DTI) results in fractional anisotropy (FA) and other parametric maps
highlighting white matter structures. Task-based functional MRI (fMRI)
highlights specific areas of eloquent cortex (gray matter) as expressed
in statistical activation maps. Other parameters and modalities
including perfusion, MR spectroscopy, and PET are often employed to
locate and characterize lesions by means of their hyper- and
hypo-metabolism and -perfusion in parametric maps.

The visualization of multiple parametric maps and sources of anatomical
information in the same space requires the tools to highlight areas of
interest (and hide irrelevant areas) in parametric maps. Two important
tools provided in this supplement are thresholding of parametric maps by
their real-world values, and blending of multiple images in a single
view.

In this example the series 2 to 5 have a lower resolution and are
expected to be resampled to have the same resolution as series 1 as this
is identified as series to be used for target Geometry.

.. _sect_FFFF.2:

Example
-------

The example describes the blending of five series:

Series 1: the anatomical series which is stored as a single volume in an
Enhanced MR Image object having no Color LUT attached. The Image will be
displayed with a Relative Opacity of 0.7.

Series 2: the DTI series which is stored as an Enhanced MR Color Image
object means that no RGB transformation is needed. The Image will be
displayed with a Relative Opacity of 1 - 0.7.

Series 3: Reading task captured in a Parametric Map with Color LUT
Winter attached to it. The Image will be displayed with threshold range
6% to 50%. Opacity will be equal divided with the other two task maps.

Series 4: Listening task captured in a Parametric Map with Color LUT
Fall attached to it. The Image will be displayed with threshold range 9%
to 60%. Opacity will be equal divided with the other two task maps.

Series 5: Silent word generation task captured in a Parametric Map with
Color LUT Spring attached to it. The Image will be displayed with
threshold range 7% to 75%. Opacity will be equal divided with the other
two task maps.

The result of the first blending operation (FOREGROUND) will be blended
with the result of the second blending operation (EQUAL) through a
FOREGROUND blending operation with a Relative Opacity of 0.6.

`figure_title <#figure_FFFF.2-6>`__ shows the final result with
information of patient and different blended image layers. The overlay
of the patient and layer information is not described in the object but
would be application specific behavior.

.. _sect_FFFF.3:

Encoding Example
----------------

.. table:: Encoding Example

   +-------------+-------------+-------------+-------------+-------------+
   | **Nesting** | **Attribute | **Tag**     | **Value**   | **Comment** |
   |             | Name**      |             |             |             |
   +=============+=============+=============+=============+=============+
   |             | Advanced    | (0070,1B01) |             |             |
   |             | Blending    |             |             |             |
   |             | Sequence    |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   |             | %item 1     |             |             | Identifies  |
   |             |             |             |             | Anatomical  |
   |             |             |             |             | Series, no  |
   |             |             |             |             | subset of   |
   |             |             |             |             | series or   |
   |             |             |             |             | r           |
   |             |             |             |             | egistration |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | Blending    | (0070,1B02) | 1           |             |
   |             | Input       |             |             |             |
   |             | Number      |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | Study       | (0020,000D) | "1.3.46.6   |             |
   |             | Instance    |             | 70589.11.3" |             |
   |             | UID         |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | Series      | (0020,000E) | "           |             |
   |             | Instance    |             | 1.3.46.6705 |             |
   |             | UID         |             | 89.11.3.45" |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | Geometry    | (0070,1B08) | TRUE        | Series      |
   |             | for Display |             |             | geometry    |
   |             |             |             |             | shall be    |
   |             |             |             |             | used as     |
   |             |             |             |             | target      |
   |             |             |             |             | geometry    |
   |             |             |             |             | for the     |
   |             |             |             |             | blending    |
   |             |             |             |             | operation   |
   +-------------+-------------+-------------+-------------+-------------+
   |             | %enditem 1  |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   |             | %item 2     |             |             | Identifies  |
   |             |             |             |             | DTI Series, |
   |             |             |             |             | no subset   |
   |             |             |             |             | of series   |
   |             |             |             |             | is used, no |
   |             |             |             |             | r           |
   |             |             |             |             | egistration |
   |             |             |             |             | present     |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | Blending    | (0070,1B02) | 2           |             |
   |             | Input       |             |             |             |
   |             | Number      |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | Study       | (0020,000D) | "1.3.46.6   |             |
   |             | Instance    |             | 70589.11.3" |             |
   |             | UID         |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | Series      | (0020,000E) | "           |             |
   |             | Instance    |             | 1.3.46.6705 |             |
   |             | UID         |             | 89.11.3.49" |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | Geometry    | (0070,1B08) | FALSE       | Series      |
   |             | for Display |             |             | geometry    |
   |             |             |             |             | shall not   |
   |             |             |             |             | be used as  |
   |             |             |             |             | target      |
   |             |             |             |             | geometry    |
   |             |             |             |             | for the     |
   |             |             |             |             | blending    |
   |             |             |             |             | operation   |
   +-------------+-------------+-------------+-------------+-------------+
   |             | %enditem 2  |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   |             | %item 3     |             |             | Identifies  |
   |             |             |             |             | first       |
   |             |             |             |             | Parametric  |
   |             |             |             |             | map, no     |
   |             |             |             |             | r           |
   |             |             |             |             | egistration |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | Blending    | (0070,1B02) | 3           |             |
   |             | Input       |             |             |             |
   |             | Number      |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | Study       | (0020,000D) | "1.3.46.6   |             |
   |             | Instance    |             | 70589.11.3" |             |
   |             | UID         |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | Series      | (0020,000E) | "           |             |
   |             | Instance    |             | 1.3.46.6705 |             |
   |             | UID         |             | 89.11.3.56" |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | Threshold   | (0070,1B11) |             |             |
   |             | Sequence    |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | %item 3-1   |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>          | Threshold   | (0070,1B12) |             |             |
   |             | Value       |             |             |             |
   |             | Sequence    |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>          | %item 3-1-1 |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>>         | Threshold   | (0070,1B14) | 6           | First       |
   |             | Value       |             |             | threshold   |
   |             |             |             |             | value       |
   +-------------+-------------+-------------+-------------+-------------+
   | >>          | %enditem    |             |             |             |
   |             | 3-1-1       |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>          | %item 3-1-2 |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>>         | Threshold   | (0070,1B14) | 50          | Second      |
   |             | Value       |             |             | threshold   |
   |             |             |             |             | value       |
   +-------------+-------------+-------------+-------------+-------------+
   | >>          | %enditem    |             |             |             |
   |             | 3-1-2       |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>          | Threshold   | (0070,1B13) | RANGE_INCL  |             |
   |             | Type        |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | %enditem    |             |             |             |
   |             | 3-1         |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   |             | %enditem 3  |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   |             | %item 4     |             |             | Identifies  |
   |             |             |             |             | second      |
   |             |             |             |             | Parametric  |
   |             |             |             |             | map, no     |
   |             |             |             |             | r           |
   |             |             |             |             | egistration |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | Blending    | (0070,1B02) | 3           |             |
   |             | Input       |             |             |             |
   |             | Number      |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | Study       | (0020,000D) | "1.3.46.6   |             |
   |             | Instance    |             | 70589.11.3" |             |
   |             | UID         |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | Series      | (0020,000E) | "           |             |
   |             | Instance    |             | 1.3.46.6705 |             |
   |             | UID         |             | 89.11.3.58" |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | Threshold   | (0070,1B11) |             |             |
   |             | Sequence    |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | %item 4-1   |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>          | Threshold   | (0070,1B12) |             |             |
   |             | Value       |             |             |             |
   |             | Sequence    |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>>         | %item 4-1-1 |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>>         | Threshold   | (0070,1B14) | 9           | First       |
   |             | Value       |             |             | threshold   |
   |             |             |             |             | value       |
   +-------------+-------------+-------------+-------------+-------------+
   | >>          | %enditem    |             |             |             |
   |             | 4-1-1       |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>          | %item 4-1-2 |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>>         | Threshold   | (0070,1B14) | 60          | Second      |
   |             | Value       |             |             | threshold   |
   |             |             |             |             | value       |
   +-------------+-------------+-------------+-------------+-------------+
   | >>          | %enditem    |             |             |             |
   |             | 4-1-2       |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>          | Threshold   | (0070,1B13) | RANGE_INCL  |             |
   |             | Type        |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | %enditem    |             |             |             |
   |             | 4-1         |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   |             | %enditem 4  |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   |             | %item 5     |             |             | Identifies  |
   |             |             |             |             | third       |
   |             |             |             |             | Parametric  |
   |             |             |             |             | map, no     |
   |             |             |             |             | r           |
   |             |             |             |             | egistration |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | Blending    | (0070,1B02) | 3           |             |
   |             | Input       |             |             |             |
   |             | Number      |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | Study       | (0020,000D) | "1.3.46.6   |             |
   |             | Instance    |             | 70589.11.3" |             |
   |             | UID         |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | Series      | (0020,000E) | "           |             |
   |             | Instance    |             | 1.3.46.6705 |             |
   |             | UID         |             | 89.11.3.59" |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | Threshold   | (0070,1B11) |             |             |
   |             | Sequence    |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | %item 5-1   |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>          | Threshold   | (0070,1B12) |             |             |
   |             | Value       |             |             |             |
   |             | Sequence    |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>          | %item 5-1-1 |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>>         | Threshold   | (0070,1B14) | 7           | First       |
   |             | Value       |             |             | threshold   |
   |             |             |             |             | value       |
   +-------------+-------------+-------------+-------------+-------------+
   | >>          | %enditem    |             |             |             |
   |             | 5-1-1       |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>          | %item 5-1-2 |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>>         | Threshold   | (0070,1B14) | 75          | Second      |
   |             | Value       |             |             | threshold   |
   |             |             |             |             | value       |
   +-------------+-------------+-------------+-------------+-------------+
   | >>          | %enditem    |             |             |             |
   |             | 5-1-2       |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>          | Threshold   | (0070,1B13) | RANGE_INCL  |             |
   |             | Type        |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | %enditem    |             |             |             |
   |             | 5-1         |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   |             | %enditem 5  |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   |             | Pixel       | (0008,9205) | "           |             |
   |             | P           |             | TRUE_COLOR" |             |
   |             | resentation |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   |             | Blending    | (0070,1B04) |             |             |
   |             | Display     |             |             |             |
   |             | Sequence    |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   |             | %item 1     |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | Blending    | (0070,1B03) |             |             |
   |             | Display     |             |             |             |
   |             | Input       |             |             |             |
   |             | Sequence    |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | %item 1-1   |             |             | Anatomical  |
   |             |             |             |             | series, no  |
   |             |             |             |             | threshold   |
   +-------------+-------------+-------------+-------------+-------------+
   | >>          | Blending    | (0070,1B02) | 1           |             |
   |             | Input       |             |             |             |
   |             | Number      |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | %enditem    |             |             |             |
   |             | 1-1         |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | %item 1-2   |             |             | DTI series, |
   |             |             |             |             | no          |
   |             |             |             |             | threshold   |
   +-------------+-------------+-------------+-------------+-------------+
   | >>          | Blending    | (0070,1B02) | 2           |             |
   |             | Input       |             |             |             |
   |             | Number      |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | %enditem    |             |             |             |
   |             | 1-2         |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | Relative    | (0070,0403) | 0.7         |             |
   |             | Opacity     |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | Blending    | (0070,1B06) | FOREGROUND  |             |
   |             | Mode        |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | Blending    | (0070,1B02) | 6           | Output is   |
   |             | Input       |             |             | used for    |
   |             | Number      |             |             | later       |
   |             |             |             |             | Blending    |
   +-------------+-------------+-------------+-------------+-------------+
   |             | %enditem 1  |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   |             | %item 2     |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | Blending    | (0070,1B03) |             |             |
   |             | Display     |             |             |             |
   |             | Input       |             |             |             |
   |             | Sequence    |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | %item 2-1   |             |             | Parametric  |
   |             |             |             |             | series 1    |
   +-------------+-------------+-------------+-------------+-------------+
   | >>          | Blending    | (0070,1B02) | 3           |             |
   |             | Input       |             |             |             |
   |             | Number      |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | %enditem    |             |             |             |
   |             | 2-1         |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | %item 2-2   |             |             | Parametric  |
   |             |             |             |             | series 2    |
   +-------------+-------------+-------------+-------------+-------------+
   | >>          | Blending    | (0070,1B02) | 4           |             |
   |             | Input       |             |             |             |
   |             | Number      |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | %enditem    |             |             |             |
   |             | 2-2         |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | %item 2-3   |             |             | Parametric  |
   |             |             |             |             | series 3    |
   +-------------+-------------+-------------+-------------+-------------+
   | >>          | Blending    | (0070,1B02) | 5           |             |
   |             | Input       |             |             |             |
   |             | Number      |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | End         |             |             |             |
   |             | Sequence    |             |             |             |
   |             | Item 2-3    |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | Blending    | (0070,1B06) | EQUAL       |             |
   |             | Mode        |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | Blending    | (0070,1B02) | 7           | Output is   |
   |             | Input       |             |             | used for    |
   |             | Number      |             |             | later       |
   |             |             |             |             | Blending    |
   +-------------+-------------+-------------+-------------+-------------+
   |             | %enditem 2  |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   |             | %item 3     |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | Blending    | (0070,1B03) |             |             |
   |             | Display     |             |             |             |
   |             | Input       |             |             |             |
   |             | Sequence    |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | %item 3-1   |             |             | Output      |
   |             |             |             |             | first       |
   |             |             |             |             | blending    |
   |             |             |             |             | operation,  |
   |             |             |             |             | no          |
   |             |             |             |             | threshold   |
   +-------------+-------------+-------------+-------------+-------------+
   | >>          | Blending    | (0070,1B02) | 6           |             |
   |             | Input       |             |             |             |
   |             | Number      |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | %enditem    |             |             |             |
   |             | 3-1         |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | %item 3-2   |             |             | Output      |
   |             |             |             |             | second      |
   |             |             |             |             | blending    |
   |             |             |             |             | operation,  |
   |             |             |             |             | no          |
   |             |             |             |             | threshold   |
   +-------------+-------------+-------------+-------------+-------------+
   | >>          | Blending    | (0070,1B02) | 7           |             |
   |             | Input       |             |             |             |
   |             | Number      |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | %enditem    |             |             |             |
   |             | 3-2         |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | Relative    | (0070,0403) | 0.6         |             |
   |             | Opacity     |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | Blending    | (0070,1B06) | FOREGROUND  |             |
   |             | Mode        |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   |             | %enditem 3  |             |             | No          |
   |             |             |             |             | Parametric  |
   |             |             |             |             | Blending    |
   |             |             |             |             | Input       |
   |             |             |             |             | Number is   |
   |             |             |             |             | present as  |
   |             |             |             |             | this step   |
   |             |             |             |             | defines the |
   |             |             |             |             | output to   |
   |             |             |             |             | be          |
   |             |             |             |             | displayed.  |
   +-------------+-------------+-------------+-------------+-------------+

