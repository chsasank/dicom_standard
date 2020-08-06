.. _chapter_Y:

VOI LUT Functions (Informative)
===============================

Digital projection X-ray images typically have a very high dynamic range
due to the digital detector's performance. In order to display these
images, various Values Of Interest (VOI) transformations can be applied
to the images to facilitate diagnostic interpretation. The original
description of the DICOM grayscale pipeline assumed that either the
parameters of a linear LUT (window center and width) are used, or a
static non-linear LUT is applied (VOI LUT).

Normally, a display application interprets the window center and width
as parameters of a function following a linear law (see
`figure_title <#figure_Y-1>`__).

A VOI LUT sequence can be provided to describe a non-linear LUT as a
table of values, with the limitation that the parameters of this LUT
cannot be adjusted subsequently, unless the application provides the
ability to scale the output of the LUT (and there is no way in DICOM to
save such a change unless a new scaled LUT is built), or to fit a curve
to the LUT data, which may then be difficult to parametrize or adjust,
or be a poor fit.

Digital X-ray applications all have their counterpart in conventional
film/screen X-ray and a critical requirement for such applications is to
have an image "look" close to the film/screen applications. In the
film/screen world the image dynamics are mainly driven by the H-D curve
of the film that is the plot of the resulting optical density (OD) of
the film with respect to the logarithm of the exposure. The typical
appearance of an H-D curve is illustrated in
`figure_title <#figure_Y-2>`__.

In digital applications, a straightforward way to mock up a film-like
look would be to use a VOI LUT that has a similar shape to an H-D curve,
namely a toe, a linear part and a shoulder instead of a linear ramp.

While such a curve could be encoded as data within a VOI LUT, DICOM
defines an alternative for interpreting the existing window center and
width parameters, as the parameters of a non-linear function.

`figure_title <#figure_Y-3>`__ illustrates the shape of a typical
sigmoid as well as the graphical interpretation of the two LUT
parameters window center and window width. This figure corresponds to
the equation definition in for the VOI LUT Function (0028,1056) is
SIGMOID.

If a receiving display application does not support the SIGMOID VOI LUT
Function, then it can successfully apply the same window center and
window width parameters to a linear ramp and achieve acceptable results,
specifically a similar perceived contrast but without the roll-off at
the shoulder and toe.

A receiving display application that does support such a function is
then able to allow the user to adjust the window center and window width
with a more acceptable resulting appearance.

