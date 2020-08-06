.. _chapter_N:

Softcopy Presentation State Storage SOP Classes (Normative)
===========================================================

.. _sect_N.1:

Overview
--------

.. _sect_N.1.1:

Scope
~~~~~

The Softcopy Presentation State Storage SOP Classes extend the
functionality of the Storage Service class (defined in `Storage Service
Class (Normative) <#chapter_B>`__) to add the ability to convey an
intended presentation state or record an existing presentation state.
The SOP Classes specify the information and behavior that may be used to
present (display) images that are referenced from within the SOP
Classes.

They include capabilities for specifying:

a. the output grayscale space in P-Values

b. the color output space as PCS-Values

c. grayscale contrast transformations including modality, VOI and
   presentation LUT

d. mask subtraction for multi-frame grayscale images

e. selection of the area of the image to display and whether to rotate
   or flip it

f. image and display relative annotations, including graphics, text and
   overlays

g. the blending of two image sets into a single presentation

The grayscale softcopy presentation state refers to the grayscale image
transformations that are to be applied in an explicitly defined manner
to convert the stored image pixel data values in a Composite Image
Instance to presentation values (P-Values) when an image is displayed on
a softcopy device. The P-Values are in a device independent perceptually
linear space that is formally defined in .

The color and pseudo-color softcopy presentation states refer to the
color image transformations that are to be applied in an explicitly
defined manner to convert the stored image pixel data values in a
Composite Image Instance to Profile Connection Space values (PCS-Values)
when an image is displayed on a softcopy device. The PCS-Values are in a
device independent space that is formally defined in the ICC Profiles as
CIEXYZ or CIELab values.

The blending presentation states specify two sets of images, an
underlying set, and a superimposed set, and the manner in which their
pixel values are blended. The underlying set is rendered as grayscale
and the superimposed set is rendered as color. The blending is not
defined in a pair wise image-by-image or frame-by-frame manner, but
rather the manner in which the two sets are combined is left to the
discretion of the implementation. Specifically, matters of spatial
registration, and any re-sampling and the mechanism of interpolation are
not specified.

The Softcopy Presentation State Storage SOP Classes may be used to store
a single state per image, or a common state to be shared by multiple
selected images. All images to which the Grayscale, Color and
Pseudo-Color Presentation States apply must be a part of the same study
that the stored state is a part of, and be of a single Composite Image
Storage SOP Class.

The two sets of images to which the Blended Presentation State applies
may be in separate Studies, Each set shall be within a single study.
Each set shall be of a single Composite Image Storage SOP Class.

How an SCU of this SOP Class records or generates this state is beyond
the scope of the Standard.

.. note::

   For example, an acquisition device may acquire, reconstruct and store
   to a workstation or archive images that are later examined by an
   operator for the purpose of quality assurance or printing. At that
   time a selected grayscale transformation (such as a window
   level/width operation) may be applied by the operator, and that
   activity captured and saved as a Grayscale Softcopy Presentation
   State Storage SOP Instance to the same workstation or archive, from
   which it is subsequently available for use by another user. Another
   workstation may retrieve the state for later use. Alternatively, an
   automated algorithm may derive a state from analysis of image
   statistics, body part examined, or other characteristics.

How an SCP of this SOP Class chooses between multiple states that may
apply to an image is beyond the scope of this Standard, other than to
state that a claim of conformance as an SCP of this SOP Class implies
that the SCP shall make the presentation state available to the user of
the device, and if selected by the user, shall apply all the
transformations stored in the state in the manner in which they are
defined in the Standard.

.. note::

   1. For example, an acquisition device may automatically store
      appropriate presentation states for series of images as they are
      reconstructed that represent adequate defaults. A user or
      algorithm may subsequently determine a more appropriate
      presentation state that more effectively displays the contents of
      an image, or record some annotation related directly to the image,
      and record that as another presentation state for an image. An
      application subsequently may display the image by automatically
      choosing to use the more recently saved or more specific
      presentation state, or may use the more general default
      presentation state for all images but notify the user that
      alternative presentation states are available.

   2. Choice of the same presentation state to display a grayscale image
      on two devices claiming conformance to these SOP Classes implies
      through the definition of the P-Value space that the displayed
      image on both devices will be perceptually similar within the
      limits defined in , regardless of the actual capabilities of the
      display systems.

   3. Choice of the same presentation state to display a color image on
      two devices claiming conformance to these SOP Classes implies
      through the definition of the PCS-Value space that the displayed
      image on both devices will appear similar in color regardless of
      the actual capabilities of the display systems.

   4. DICOM color images without an embedded optional ICC profile have
      no defined color space, regardless of their representation. The
      implementation creating a Color Softcopy Presentation State with
      an ICC profile is explicitly defining a color space in which to
      interpret that image, even if one was not known at the time that
      the image was created. Often a well-known color space such as sRGB
      will be used in the presentation state under such circumstances.

.. _sect_N.2:

Pixel Transformation Sequence
-----------------------------

The Softcopy Presentation State Storage SOP Classes support a sequence
of transformations that completely define the conversion of a stored
image into a displayed image.

The sequence of transformations from stored pixel values into P-Values
or PCS-Values is explicitly defined in a conceptual model. The actual
sequence implemented may differ but must result in the same appearance.
`figure_title <#figure_N.2-1>`__ describes this sequence of
transformations.

.. note::

   1. Even though a Composite Image Storage SOP Class may not include
      some Modules that are part of the described transformations, the
      Softcopy Presentation State Storage SOP Classes do include them.
      For example, the CT Image Storage SOP Class includes Rescale Slope
      and Intercept in the CT Image Module, but does not include the
      Modality LUT Module, and hence is restricted to the description of
      linear transformations. A saved presentation state that refers to
      a CT Image Storage SOP Instance may include a Modality LUT, and
      hence may apply a non-linear transformation.

   2. For the shutter, annotation and spatial transformations, the order
      in which they are applied relative to the other transformations
      should not result in a different appearance. The one exception is
      when a spatial transformation is applied that involves
      magnification implemented with interpolation. In this case,
      whether the interpolation is performed before or after the
      contrast transformations (such as VOI LUT) may result in a
      slightly different appearance. It is not considered necessary to
      constrain this sequence more precisely.

The transformations defined in the Softcopy Presentation State Storage
SOP Classes replace those that may be defined in the Referenced Image
SOP Instance. If a particular transformation is absent in the Softcopy
Presentation State Storage SOP Class, then it shall be assumed to be an
identity transformation, and any equivalent transformation, if present,
in the Referenced Image SOP Instance shall NOT be used instead.

Values of MONOCHROME1 and MONOCHROME2 for Photometric Interpretation
(0028,0004) in the Referenced Image SOP Instance shall be ignored, since
their effect is defined by the application of the grayscale presentation
state transformations.

.. note::

   These requirements are in order to achieve complete definition of the
   entire transformation in the Softcopy Presentation State Storage SOP
   Classes, and not to depend on the content of the Referenced Image SOP
   Instance, which may change.

The Referenced Image Storage SOP Instance may also contain bit-mapped
overlays. The Softcopy Presentation State Storage SOP Classes specify a
mechanism for turning these on or off (i.e., displaying them or not).

The presentation related Attributes of the Softcopy Presentation State
Storage SOP Classes are immutable. They shall never be modified or
updated; only a derived SOP Instance with a new SOP Instance UID may be
created to represent a different presentation.

When a Supplemental Palette Color LUT is present in a grayscale
Referenced Image Storage SOP Instance:

-  The grayscale pipeline in any applicable Grayscale Softcopy
   Presentation State Storage SOP Instance or Blended Softcopy
   Presentation State Storage SOP Instance shall be applied only to the
   range of grayscale stored pixel values, and the presentation state
   shall not affect the rendering of the indexed color values.

-  A Color Softcopy Presentation State Storage SOP Instance shall not be
   applied.

-  A Pseudo-color Softcopy Presentation State Storage SOP Instance may
   be applied, in which case the Supplemental Palette Color LUT
   information shall be ignored.

-  No mechanism for separately specifying color consistency of the
   colors in the Supplemental Palette Color LUT is presently defined,
   only the optional inclusion of an ICC profile in the image instance.

.. _sect_N.2.1:

Grayscale Transformations
~~~~~~~~~~~~~~~~~~~~~~~~~

.. _sect_N.2.1.1:

Modality LUT
^^^^^^^^^^^^

The Modality LUT operation applies only to grayscale values.

The Modality LUT transformation transforms the manufacturer dependent
pixel values into pixel values that are meaningful for the modality and
are manufacturer independent (e.g., Hounsfield number for CT modalities,
Optical Density for film digitizers). These may represent physical units
or be dimensionless. The Modality LUT in the Presentation State is
modality dependent and is analogous to the same Module in an Image.

.. note::

   1. In some cases, such as the CT Image Storage SOP Class, the same
      conceptual step as the Modality LUT is specified in another form,
      for example as Rescale Slope and Rescale Intercept Attributes in
      the CT Image Module, though the Modality LUT Module is not part of
      the CT Image IOD.

   2. Image pixel values with a value of Pixel Padding Value (0028,0120)
      in the referenced image, or within the range specified by Pixel
      Padding Value (0028,0120) and Pixel Padding Range Limit
      (0028,0121) (if present in the referenced image) shall be
      accounted for prior to entry to the Modality LUT stage. See the
      definition of Pixel Padding Value in . Neither Pixel Padding Value
      (0028,0120) nor Pixel Padding Range Limit (0028,0121) are encoded
      in the Presentation State Instance.

In the case of a linear transformation, the Modality LUT is described by
the Rescale Slope (0028,1053) and Rescale Intercept (0028,1052). In the
case of a non-linear transformation, the Modality LUT is described by
the Modality LUT Sequence. The rules for application of the Modality LUT
are defined in .

If the Modality LUT or equivalent Attributes are part of both the Image
and the Presentation State, then the Presentation State Modality LUT
shall be used instead of the Image Modality LUT or equivalent Attributes
in the Image. If the Modality LUT is not present in the Presentation
State it shall be assumed to be an identity transformation. Any Modality
LUT or equivalent Attributes in the Image shall not be used.

.. _sect_N.2.1.2:

Mask
^^^^

The Mask operation applies only to grayscale values.

The mask transformation may be applied in the case of multi-frame images
for which other frames at a fixed frame position or time interval
relative to the current frame may be subtracted from the current frame.
Multiple mask frames may be averaged, and sub-pixel shifted before
subtraction.

This transformation uses the Mask Module as used in the X-Ray
Angiography Image Storage SOP Class, though it may be applied to any
Image Storage SOP Instance that contains a multi-frame image.

In the case of X-Ray images, the subtraction is specified to take place
in a space logarithmic to X-Ray intensity. If the stored pixel values
are not already in such a space, an implementation defined
transformation to such a space must be performed prior to subtraction.
If a Modality LUT Module is present as well as a Mask Module, then the
Modality LUT shall specify a transformation into such a logarithmic
space, otherwise it shall not be present (even though a Modality LUT may
be present in the referenced image(s), which shall be ignored).

.. note::

   1. In the case of an XA or XRF image, if the Pixel Intensity
      Relationship (0028,1040) in the image is LOG, then even though a
      Modality LUT would be present in the image (to map pixel values
      back to linear to X-Ray intensity), no Modality LUT would be
      present in the presentation state (i.e., the Modality LUT would be
      an identity transformation) since log values are required for
      subtraction. See .

   2. In the case of an XA or XRF image, if the Pixel Intensity
      Relationship (0028,1040) is LIN, then no Modality LUT would be
      present in the image, but a Modality LUT would need to be present
      in the presentation state since log values are required for
      subtraction.

   3. In the case of an XA or XRF image, if the Pixel Intensity
      Relationship (0028,1040) in the image is DISP, then even though a
      Modality LUT may or may not be present in the image (to map pixel
      values back to linear to X-Ray intensity), a different Modality
      LUT would be present in the presentation state if the creator of
      the presentation state could create a transformation from DISP
      pixel values to a logarithmic space for subtraction, or the
      Modality LUT in the presentation state would be an identity
      transformation if the DISP pixel values were known to already be
      log values required for subtraction.

The result will be a signed value with a bit length one longer than the
source frames.

When there is no difference between corresponding pixel values, the
subtracted image pixel will have a value of 0.

If a pixel in the current frame has a greater value than in the mask
frame, then the resulting frame shall have a positive value. If it has a
lesser value, then the resulting frame shall have a negative value.

.. _sect_N.2.1.3:

VOI LUT
^^^^^^^

The VOI LUT operation applies only to grayscale values.

The value of interest (VOI) LUT transformation transforms the modality
pixel values into pixel values that are meaningful for the user or the
application.

.. note::

   Photometric Interpretation (0028,0004) is ignored, since its effect
   is defined by the application of the grayscale transformations.

The Softcopy VOI LUT Module in the Presentation State is analogous to
the VOI LUT Module in an Image.

In the case of a linear transformation, the VOI LUT is described by the
Window Center (0028,1050) and Window Width (0028,1051). In the case of a
non-linear transformation, the VOI LUT is described by the VOI LUT
Sequence. A VOI LUT Function (0028,1056) may be present to define a
potentially non-linear interpretation (e.g., SIGMOID) of the values of
Window Center (0028,1050) and Window Width (0028,1051). The rules for
application of the VOI LUT are defined in .

The VOI LUT may have sections with negative slope.

.. note::

   In the Basic Print Service Class a VOI LUT may not have negative
   slope.

If a VOI LUT is part of both the Image and the Presentation State then
the Presentation State VOI LUT shall be used instead of the Image VOI
LUT. If a VOI LUT (that applies to the Image) is not present in the
Presentation State, it shall be assumed to be an identity
transformation. Any VOI LUT or equivalent values in the Image shall not
be used.

.. _sect_N.2.1.4:

Presentation LUT
^^^^^^^^^^^^^^^^

The Presentation LUT operation applies only to grayscale values.

The Presentation LUT transformation transforms the pixel values into
P-Values, a device independent perceptually linear space as defined in .
It may be an identity function if the output of the VOI LUT
transformation is in P-Values.

.. note::

   If the Presentation LUT and VOI LUT step are identity
   transformations, and the Mask Module is absent, then the output of
   the Modality LUT must be, by definition, P-Values.

No output space other than P-Values is defined for the Grayscale
Softcopy Presentation State Storage SOP Classes.

In the case of a linear transformation, the Presentation LUT is
described by the Presentation LUT Shape (2050,0020). In the case of a
non-linear transformation, the Presentation LUT is described by the
Presentation LUT Sequence. The rules for application of the Presentation
LUT are defined in .

.. note::

   1. Since the grayscale transformation pipeline fully defines all
      transformations applied to the stored pixel values in the
      referenced image object, the value of Photometric Interpretation
      (0028,0004) in the referenced image object is ignored and
      overridden. This implies that either the creator of the
      presentation state chose a pipeline that reflects the Photometric
      Interpretation (0028,0004), or chose to ignore or override the
      Photometric Interpretation, and invert the image relative to what
      is specified by Photometric Interpretation. If the Modality LUT
      and VOI LUT do not have a negative slope, one can achieve the
      effect of inversion of the polarity of an image by choosing
      Presentation LUT Shape of IDENTITY or INVERSE that displays the
      minimum pixel value as white rather than black in the case of a
      Photometric Interpretation of MONOCHROME2, or black rather than
      white in the case of a Photometric Interpretation of MONOCHROME1.
      If Presentation LUT Data is sent, then one can invert the value of
      the entries in the LUT table to achieve inversion of polarity.

   2. The minimum P-Value (zero) always commands that the lowest
      intensity be displayed.

   3. No separate Polarity transformation is defined.

A Softcopy Presentation LUT Module is always present in a Presentation
State. If a Presentation LUT is present in the Image then the
Presentation State Presentation LUT shall be used instead of the Image
Presentation LUT.

.. _sect_N.2.2:

Color Transformations
~~~~~~~~~~~~~~~~~~~~~

.. _sect_N.2.2.1:

Profile Connection Space Transformation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Profile Connection Space Transformation operation applies only to
color images, including true color (e.g., RGB) and pseudo-color (e.g.,
PALETTE COLOR) images, grayscale images for which a Palette Color LUT
has been specified in the Presentation State, and the RGB output values
of a blending operation.

The ICC Profile is an Input Profile. That is, it describes the color
characteristics of a (possibly hypothetical) device that was used to
generate the input color values.

The intent is that a rendering device will use this information to
achieve color consistency. Typically this will be performed by
calibration of the output device to create an ICC Display or Output
Profile, the conversion of pixel values using the ICC Input Profile into
Profile Connection Space, followed by conversion using the ICC Display
or Output Profile into values suitable for rendering on the output
device. However, the exact mechanisms used are beyond the scope of the
Standard to define.

.. note::

   1. The means of achieving color consistency depends to a large extent
      on the nature of the material and the intent of the application.
      The process is more complicated than simply achieving colorimetric
      accuracy, which is trivial but does not produce satisfactory
      results. The transformations may take into account such matters as

      -  physical factors such as the ambient light of the viewing
         environment (viewing flare) and the nature of different
         illuminants

      -  psychovisual factors in the observer

      -  the preferences of the observer

      -  the consistency intent, whether it be to reproduce the colors
         perceived by an observer of

         -  the original scene,

         -  the media being reproduced, such as a print or transparency,
            as viewed under specified conditions.

   2. Implementations of color management schemes are typically provided
      in operating systems, libraries and tool kits, and the exact
      details are usually beyond the control of the DICOM application
      developer. Accordingly, it is normally sufficient to define a
      source of pixel values, and a corresponding ICC Input Profile for
      the device that captured or generated them.

   3. When a color image is rendered on grayscale display, the behavior
      is not defined. Since the L\* value of a CIELab representation of
      the PCS is not dissimilar to the Barten model used in the GSDF, a
      reasonable approach would be to interpret it as a P-Value.

An ICC Profile is always present in a Color, Pseudo-Color or Blended
Presentation State. If an ICC Profile is present in the Image then the
Presentation State ICC Profile shall be used instead of the Image ICC
Profile.

.. _sect_N.2.2.2:

White Point (Informative)
^^^^^^^^^^^^^^^^^^^^^^^^^

D50 means black body radiation of an object at 5000 degrees K, and
includes lots of red, which looks "natural". D65 is bluer, more like
"cloudy days", but human eyes are more sensitive to blue. While monitors
seem to be in the D50-D100 range, light boxes are about D110 (11000K).

The ICC PCS always uses a white point of D50.

In an ICC Input Profile, the chromaticAdaptationTag encodes a conversion
of an XYZ color from the actual illumination source to the PCS
illuminant (D50), and may be useful if the actual illumination source is
not D50. The actual illumination source may also be defined in the
mediaWhitePointTag. However, with a perceptual rendering intent, neither
of these tags are required to be used by the color management system,
nor do they have any specified rendering behavior (as opposed to their
use with absolute and relative colorimetric rendering intents).

It is beyond the scope of DICOM to define a required or suggested white
point for rendering, since an appropriate choice depends on a knowledge
of the display device or media characteristics and the viewing
environment.

.. _sect_N.2.3:

Common Spatial and Annotation Transformations
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The common spatial and annotation transformations apply to any
device-independent values, whether they be grayscale P-Values or color
PCS-Values, for any type of presentation state.

The values with which to render annotations are encoded as
device-independent values, either as grayscale P-Values or as color
PCS-Values. In the case of PCS-Values, CIELab values are encoded, and
defined by reference to a D50 illuminant.

Grayscale presentation states may specify annotations in color for
rendering on a color output device.

The mechanism for mapping grayscale P-Values and color PCS-values to the
same display is implementation-dependent and not defined by the
Standard.

.. _sect_N.2.3.1:

Shutter
^^^^^^^

The Shutter transformation provides the ability to exclude the perimeter
outside a region of an image. A gray level may be specified to replace
the area under the shutter.

One form of this transformation uses the Display Shutter Module as used
in the X-Ray Angiography Image Storage SOP Class, though it may be
applied to any Image Storage SOP Instance, including single frame
images.

Another form uses a bit-mapped overlay to indicate arbitrary areas of
the image that should be excluded from display by replacement with a
specified gray level, as described in the Bitmap Display Shutter Module.

.. note::

   1. Since annotations follow the shutter operation in the pipeline,
      annotations in shuttered regions are not obscured and are visible.

   2. Any shutter present in the referenced image object is ignored
      (i.e., not applied).

.. _sect_N.2.3.2:

Pre-Spatial Transformation Annotation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Pre-Spatial Transformation Annotation transformation includes the
application of bit-mapped overlays as defined in the Overlay Plane
Module, and free unformatted text or vector graphics as described in the
Graphic Annotation Module that are defined in the image pixel space (as
opposed to the displayed area space).

.. _sect_N.2.3.3:

Spatial Transformation
^^^^^^^^^^^^^^^^^^^^^^

Some modalities may not deliver the image in the desired rotation and
need to specify a rotation into the desired position for presentation.
This transformation, specified in the Spatial Transformation Module,
includes a rotation of 90, 180, 270 degrees clockwise followed by a
horizontal flip (L <--> R). Rotation by an arbitrary angle is not
supported.

In addition, selection of a region of the image pixel space to be
displayed is specified in the Displayed Area Module. This may have the
effect of magnifying (or minifying) that region depending on what
physical size the display is instructed to render the selected region.
If so, the method of interpolation (or sub-sampling) is implementation
dependent.

.. note::

   In particular the number of displayed pixels may be different from
   the number of image pixels as a result of:

   -  minification (e.g., 1 display pixel for 4 image pixels),

   -  magnification (4 display pixels for each image pixel),

   -  interpolation (display pixels derived from values other than those
      in the image pixels), and

   -  sub-sampling.

.. _sect_N.2.3.4:

Post-Spatial Transformation Annotation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Post-Spatial Transformation Annotation transformation includes the
application of free unformatted text or vector graphics as described in
the Graphic Annotation Module that are defined in the displayed area
space (as opposed to the image pixel space).

This implies that the displayed area space is defined as being the image
after all Spatial Transformations have been applied.

These annotations are rendered in the displayed space, though they may
be anchored to points in either the displayed area or image pixel space.

.. _sect_N.2.4:

Blending Transformations
~~~~~~~~~~~~~~~~~~~~~~~~

The grayscale to color blending transformation model applies only to a
pair of grayscale values, one of which is first mapped to color and then
superimposed upon the other. The resulting values are device independent
color PCS-Values. This process is illustrated in
`figure_title <#figure_N.2-3>`__.

For the purpose of this section, pixels are referred to as stored pixel
values and transformations are defined as point operations on these
values. However, it is likely that pixels from either or both the
superimposed and underlying image sets will have been spatially
resampled and hence interpolated or replicated. Such operations do not
affect the conceptual pipeline.

.. _sect_N.2.4.1:

Underlying Image Pixels
^^^^^^^^^^^^^^^^^^^^^^^

The Modality LUT and VOI LUT transformations are applied to the stored
pixel values of the underlying image.

The output range of the VOI LUT transformation depends either on the
width of the linear window or the range of output values of the LUT
defined by the LUT Descriptor. Conceptually, for the purpose of
describing the succeeding blending operation, the smallest pixel value
from the range is mapped to 0.0 and the largest pixel value is mapped to
1.0 and all intermediate values are linearly mapped to the [0.0..1.0]
interval.

.. _sect_N.2.4.2:

Superimposed Image Pixels
^^^^^^^^^^^^^^^^^^^^^^^^^

The Modality LUT and VOI LUT transformations are applied to the stored
pixel values of the superimposed image.

The full output range of the preceding VOI LUT transformation is
implicitly scaled to the entire input range of the Palette Color LUT
Transformation.

The output range of the RGB values in the Palette Color LUT
Transformation depends on the range of output values of the LUT defined
by the LUT Descriptors. Conceptually, for the purpose of describing the
succeeding blending operation, a LUT entry of 0 is mapped to 0.0 and the
largest LUT entry possible is mapped to 1.0 and all intermediate values
are linearly mapped to the [0.0..1.0] interval.

.. note::

   In practice, the Palette Color LUT output for the superimposed images
   is encoded in 8 or 16 bits and hence will have a range of 0 to 0xFF
   or 0xFFFF.

The Palette Color LUT used is that encoded in the Blending Presentation
State; any Palette Color LUTs or Supplemental Palette Color LUTs in the
image instances are ignored.

.. _sect_N.2.4.3:

Blending Operation
^^^^^^^^^^^^^^^^^^

The inputs to the blending operation are grayscale values from 0.0 to
1.0 from the underlying image (Y\ :sub:`u`) and RGB values from 0.0 to
1.0 from the superimposed image (RGB\ :sub:`s`), and an opacity value
from 0.0 to 1.0 (A).

The output is a single image containing RGB values (RGB\ :sub:`o`)
blended as:

R\ :sub:`o` = R\ :sub:`s` \* A + Y\ :sub:`u` \* (1-A)

G\ :sub:`o` = G\ :sub:`s` \* A + Y\ :sub:`u` \* (1-A)

B\ :sub:`o` = B\ :sub:`s` \* A + Y\ :sub:`u` \* (1-A)

.. _sect_N.2.4.4:

Conversion to Profile Connection Space
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The output of the blending operation is implicitly scaled to the gamut
of the hypothetical device described by the ICC Input Profile, resulting
in PCS-Values.

.. _sect_N.2.5:

Angiography Grayscale Transformations
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The XA/XRF Grayscale Softcopy Presentation State Storage SOP Class
supports a sequence of transformations that completely define the
conversion of a stored image into a displayed image.

The sequence of transformations from stored pixel values into P-Values
is explicitly defined in a conceptual model. The actual sequence
implemented may differ but must result in the same appearance.
`figure_title <#figure_N.2.5-1>`__ describes this sequence of
transformations.

.. _sect_N.2.5.1:

Mask
^^^^

The Mask transformation consists of mask subtraction operations as
specified by the Attributes of the XA/XRF Presentation State Mask Module
and the Attribute Mask Visibility Percentage of the XA/XRF Presentation
State Presentation Module.

The mask transformation may be applied in the case of multi-frame images
for which other frames at a fixed frame position or time interval
relative to the current frame may be subtracted from the current frame.
Multiple mask frames may be averaged, and sub-pixel shifted before
subtraction. Sub-pixel shift may be specified on a frame-by-frame base.
Different pixel-shifts may be applied to more than one region of a
contrast frame.

In the case of X-Ray images, the subtraction is specified to take place
in a space logarithmic to X-Ray intensity. If the stored pixel values
are not in a logarithmic space then a Pixel Intensity Relationship LUT
shall be present in the XA/XRF Presentation Mask Module specifying a
transformation into such a logarithmic space, otherwise it shall not be
present. If a Modality LUT or Pixel Intensity Relationship LUT is
present in the referenced image(s) it shall be ignored. The Pixel
Intensity Relationship LUT can be specified on a frame-by frame base
that can be different for mask and contrast frames.

.. note::

   1. For images of the X-Ray Angiographic Image Storage SOP Class or
      X-Ray RF Image Storage SOP Class the XA/XRF Grayscale Softcopy
      Presentation State allows a Pixel Intensity Relationship LUT to be
      specified on a frame-by-frame base. This is an enhancement of the
      image Modality LUT that is only applicable for all frames of an
      image.

   2. In the case of an XA or XRF image, if the Pixel Intensity
      Relationship (0028,1040) in the image is LOG, then even though a
      Modality LUT would be present in the image (to map pixel values
      back to linear X-Ray intensity), no Pixel Intensity Relationship
      LUT would be present in the presentation state for any frame since
      log values are required for subtraction. See .

      In the case of Enhanced XA or XRF image, if the Pixel Intensity
      Relationship (0028,1040) in the frame is LOG, then even though a
      Pixel Intensity Relationship LUT would be present in the frame (to
      map pixel values back to linear X-Ray intensity, LUT Function
      (0028,9474) equals TO_LINEAR), no Pixel Intensity Relationship LUT
      would be present in the presentation state for that frame since
      log values are required for subtraction. See .

   3. In the case of an XA or XRF image if the Pixel Intensity
      Relationship (0028,1040) in the image is LIN, then no Modality LUT
      would be present in the image, but a Pixel Intensity Relationship
      LUT would need to be present (to map pixel values to log values,
      LUT Function (0028,9474) equals TO_LOG) in the presentation state
      for all the frames since log values are required for subtraction.

      In the case of an Enhanced XA or XRF image, if the Pixel Intensity
      Relationship (0028,1040) in the frame is LIN, then no Pixel
      Intensity Relationship LUT for the purpose to map pixel values
      back to linear X-Ray intensity (LUT Function (0028,9474) equals
      TO_LINEAR) would be present in the image, but a Pixel Intensity
      Relationship LUT would need to be present (to map pixel values to
      log values) in the presentation state for that frame since log
      values are required for subtraction.

   4. In the case of an XA or XRF image, if the Pixel Intensity
      Relationship (0028,1040) in the image is DISP, then even though a
      Modality LUT may or may not be present in the image (to map pixel
      values back to linear to X-Ray intensity), a different Pixel
      Intensity Relationship LUT would be present in the presentation
      state if the creator of the presentation state could create a
      transformation from DISP pixel values to a logarithmic space for
      subtraction, or the Pixel Intensity Relationship LUT in the
      presentation state would be an identity transformation if the DISP
      pixel values were known to already be log values required for
      subtraction.

      In the case of an Enhanced XA or XRF image, if the Pixel Intensity
      Relationship (0028,1040) in the image is OTHER, then even though a
      Pixel Intensity Relationship LUT may or may not be present for
      that frame (to map pixel values back to linear to X-Ray
      intensity), a different Pixel Intensity Relationship LUT would be
      present in the presentation state for that frame if the creator of
      the presentation state could create a transformation from OTHER
      pixel values to a logarithmic space for subtraction, or the Pixel
      Intensity Relationship LUT in the presentation state would be an
      identity transformation if the OTHER pixel values were known to
      already be log values required for subtraction.

   5. Notes 2, 3 and 4 are summarized in
      `table_title <#table_N.2.5.1-1>`__

   .. table:: Summary of Providing a LUT Function for Subtraction

      +----------------------------------+----------------------------------+
      | Pixel Intensity Relationship     | The contents of Pixel Intensity  |
      | (0028,1040) Attribute of the     | Relationship LUT Sequence        |
      | referenced SOP Instance          | (0028,9422) in XA/XRF            |
      |                                  | Presentation State Mask Module   |
      +==================================+==================================+
      | LIN                              | TO_LOG LUT provided              |
      +----------------------------------+----------------------------------+
      | LOG                              | absent                           |
      +----------------------------------+----------------------------------+
      | DISP or OTHER                    | TO_LOG LUT provided, may be an   |
      |                                  | identity                         |
      +----------------------------------+----------------------------------+

.. _sect_N.2.5.2:

Edge Enhancement
^^^^^^^^^^^^^^^^

The Edge Enhancement transformation consists of filter operations to
enhance the display of the pixel data as specified by the Attribute
Display Filter Percentage of the XA/XRF Presentation State Presentation
Module.

.. _sect_N.2.6:

Advanced Blending Transformations
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The advanced blending transformation model applies to multiple color
inputs and uses foreground blending or equal blending.

Several transformations in this IOD affect the input prior to its use in
blending as depicted in `figure_title <#figure_N.2.6-1>`__.

Grayscale inputs that have no associated Color LUT information shall
have the normal grayscale processing and then be converted to a full
color image by setting R equals G equals B.

Padding pixels in an input are given an opacity value zero and shall be
set to 0 for Red, Green, and Blue.

The foreground method blends two inputs. The first input uses an opacity
of Relative Opacity (0070,0403) and the second input uses an opacity of
(1 - Relative Opacity (0070,0403) ).

If both the inputs are padding values then the result is padding value.

If one of the values is padding value then the result is the non-padding
value.

If both pixels have values then result is Relative Opacity \* first
value + (1 - Relative Opacity) \* second value.

The Equal blending mode blends two or more inputs where for each pixel
location the opacity is calculated as 1.0 divided by the number of
non-padding pixels. The result pixel blends all non-padding pixels using
the calculated opacity.

If an input pixel value is the padding-value then the Relative Opacity
for that input pixel is zero.

If an input pixel value is not the padding value then the Relative
Opacity for that pixel is 1 / (number of input pixels that are
non-padding pixels).

The result value is the sum for all input pixels of the input pixel
value \* Relative Opacity.

If all the inputs pixels are padding values then the result is padding
value.

.. _sect_N.3:

Behavior of an SCP
------------------

In addition to the behavior for the Storage Service Class specified in
`Behavior of an SCP <#sect_B.2.2>`__ Behavior of an SCP, the following
additional requirements are specified for the Softcopy Presentation
State Storage SOP Classes:

-  a display device acting as an SCP of these SOP Classes shall make all
   mandatory presentation Attributes available for application to the
   referenced images at the discretion of the display device user, for
   all Image Storage SOP Classes defined in the Conformance Statement
   for which the Softcopy Presentation State Storage SOP Class is
   supported.

-  a display device that is acting as an SCP of these SOP Classes and
   that supports compound graphics types shall display the graphics
   described in the Compound Graphic Sequence (0070,0209) and shall not
   display the Items in the Text Object Sequence (0070,0008) and Graphic
   Object Sequence (0070,0009) that have the same Compound Graphic
   Instance ID (0070,0226) value.

.. note::

   Though it is not required, a display device acting as an SCP of the
   Blending Softcopy Presentation State Storage SOP Class may support
   the Spatial Registration Storage SOP Class in order to transform one
   Frame of Reference into another or to explicitly identify the
   relationship between members of two sets of images, and may be able
   to resample underlying and superimposed sets of images that differ
   from each other in orientation and in-plane and between-plane spatial
   resolution.

.. _sect_N.4:

Conformance
-----------

In addition to the Conformance Statement requirements for the Storage
Service Class specified in `Conformance Statement
Requirements <#sect_B.4.3>`__, the following additional requirements are
specified for the Softcopy Presentation State Storage SOP Classes:

.. _sect_N.4.1:

Conformance Statement for an SCU
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The following issues shall be documented in the Conformance Statement of
any implementation claiming conformance to a Softcopy Presentation State
Storage SOP Class as an SCU:

-  For an SCU of a Softcopy Presentation State Storage SOP Class that is
   creating a SOP Instance of the Class, the manner in which
   presentation related Attributes are derived from a displayed image,
   operator intervention or defaults, and how they are included in the
   IOD.

-  For an SCU of a Softcopy Presentation State Storage SOP Class, the
   Image Storage SOP Classes that are also supported by the SCU and may
   be referenced by instances of the Softcopy Presentation State Storage
   SOP Class.

-  For an SCU of a Softcopy Presentation State Storage SOP Class whether
   it supports the Compound Graphic Sequence (0070,0209) and specifies
   which compound graphic types can be generated, including additional
   private defined compound graphic types.

.. _sect_N.4.2:

Conformance Statement for an SCP
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The following issues shall be documented in the Conformance Statement of
any implementation claiming conformance to a Softcopy Presentation State
Storage SOP Class as an SCP:

-  For an SCP of a Softcopy Presentation State Storage SOP Class that is
   displaying an image referred to by a SOP Instance of the Class, the
   manner in which presentation related Attributes are used to influence
   the display of an image.

-  For an SCP of a Softcopy Presentation State Storage SOP Class, the
   Image Storage SOP Classes that are also supported by the SCP and may
   be referenced by instances of the Softcopy Presentation State Storage
   SOP Class.

-  For an SCP of a Softcopy Presentation State Storage SOP Class whether
   it supports the Compound Graphic Sequence (0070,0209) and which
   compound graphic types can be rendered, including additional private
   defined compound graphic types.

