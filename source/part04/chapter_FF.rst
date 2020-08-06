.. _chapter_FF:

Volumetric Presentation State Storage SOP Classes (Normative)
=============================================================

.. _sect_FF.1:

Overview
--------

.. _sect_FF.1.1:

Scope
~~~~~

The Volumetric Presentation State Storage SOP Classes extend the
functionality of the Storage Service class (defined in `Storage Service
Class (Normative) <#chapter_B>`__) to add the ability to convey an
intended Volumetric Presentation State or record an existing Volumetric
Presentation State. The SOP Classes specify the information and behavior
that may be used to present (display) images that are referenced from
within the SOP Classes.

They include capabilities for specifying:

-  spatial registration on the input datasets

-  cropping of the volume datasets by a bounding box, oblique planes and
   segmentation objects

-  the generation geometry of volumetric views

-  shading models

-  scalar to P-Value or RGB Value conversions

-  compositing of multiple MPR renderings

-  compositing of multiple volume streams and one volume stream with
   segmentation

-  clinical description of the specified view

-  volume and display relative annotations, including graphics, text and
   overlays plus optional references to structured content providing
   clinical context for annotations

-  membership to a collection of related Volumetric Presentation States
   intended to be processed or displayed together

-  the position within a set of sequentially related Volumetric
   Presentation States

-  animation of the view

-  reference to an image depicting the view described by the Volumetric
   Presentation State

Each Volumetric Presentation State corresponds to a single view
(equivalent to an Image Box in a Hanging Protocol or Structured
Display). If multiple Volumetric Presentation States are intended to be
displayed together (e.g., a set of orthogonal MPR views) these
Presentation States can be grouped by assigning them to a Display
Collection. However, any detailed information about how a set of views
should be presented can only be described by a Structured Display
instance or a Hanging Protocol.

The Planar MPR Volumetric Presentation State refers to the multi-planar
geometry and grayscale or color image transformations that are to be
applied in an explicitly defined manner to convert the stored image
pixel data values in a Composite Image Instance to presentation values
(P-Values) or Profile Connection Space values (PCS-Values) when an image
is displayed on a softcopy device.

The Volume Rendering Volumetric Presentation State specifies a volume
rendered view of volume data. Volume Rendering is a data visualization
method in which voxels (volume sample points) are assigned a color and
an opacity (alpha), and a 2D view is created by accumulating a set of
non-transparent samples along a ray through the volume behind each pixel
of the view. Ray samples are calculated by interpolating the voxel
values in the neighborhood of each sample.

Volume Rendering generally consists of a number of steps, many of which
are parametrically specified in the Volume Rendering SOP Classes. The
processing steps are:

-  Segmentation, or separating the volume data into groups that will
   share a particular color palette. Segmentation objects are specified
   as cropping inputs to the Volumetric Presentation State.

-  Gradient Computation, or finding edges or boundaries between
   different types of tissue in the volumetric data. The gradient
   computation method used is an implementation decision outside the
   scope of the Volumetric Presentation State.

-  Resampling of the volumetric data to create new samples along the
   imaginary ray behind each pixel in the output two-dimensional view,
   generally using some interpolation of the values of voxels in the
   neighborhood of the new sample. The interpolation method used is an
   implementation decision outside the scope of the Volumetric
   Presentation State.

-  Classification of samples to assign a color and opacity to each
   sample.

-  Shading or the application of a lighting model to samples indicating
   the effect of ambient, diffuse, and specular light on the sample.

-  Compositing or the accumulation of samples on each ray into the final
   value of the pixel corresponding to that ray. The specific algorithms
   used are outside the scope of the Volumetric Presentation State.

-  Conversion to presentation Profile Connection Space values
   (PCS-Values) when an image is displayed on a softcopy device.

The result of applying a Volumetric Presentation State is not expected
to be exactly reproducible on different systems. It is difficult to
describe the display and rendering algorithms in enough detail in an
interoperable manner such that a presentation produced at a later time
is indistinguishable from that of the original presentation. While
Volumetric Presentation States use established DICOM concepts of
grayscale and color matching (GSDF and ICC color profiles) and provide a
generic description of the different types of display algorithms
possible, variations in algorithm implementations within display devices
are inevitable and an exact match of volume presentation on multiple
devices cannot be guaranteed. Nevertheless, reasonable consistency is
provided by specification of inputs, geometric descriptions of spatial
views, type of processing to be used, color mapping and blending, input
fusion, and many generic rendering parameters, producing what is
expected to be a clinically acceptable result.

The P-Values are in a device independent perceptually linear space that
is formally defined in . The PCS-Values are in a device independent
space that is formally defined in the ICC Profiles as CIEXYZ or CIELab
values.

How an SCP of these SOP Classes chooses between multiple Presentation
State instances that may apply to an image is beyond the scope of this
Standard.

A claim of conformance as an SCP of the SOP Class implies that the SCP
shall make the Presentation State available to the user of the device,
and if selected by the user, shall apply all the transformations stored
in the state in the manner in which they are defined in the Standard.

How an SCP of these SOP Classes chooses to display multiple states that
are part of a Display Collection is beyond the scope of this Standard.

.. note::

   For example, if a user selects a state that is part of a four state
   Spatial Collection, an SCP may choose to display all four together,
   to display the single state selected by the user or to display two of
   the four states deemed appropriate by the SCP.

.. _sect_FF.2:

Volume Transformation Processes
-------------------------------

.. _sect_FF.2.1:

Volumetric Transformations
~~~~~~~~~~~~~~~~~~~~~~~~~~

The transformations defined in the Volumetric Presentation State Storage
SOP Classes replace those that may be defined in the Referenced Image
SOP Instances. If a particular transformation is absent in a Volume
Rendering Volumetric Presentation State Storage SOP Instance, then it
shall be assumed to be an identity transformation and any equivalent
transformation, if present, in the Referenced Image SOP Instances shall
not be used.

The presentation-related Attributes of the Volume Rendering Volumetric
Presentation State Storage SOP Classes are immutable. They shall never
be modified or updated; only a derived SOP Instance with a new SOP
Instance UID may be created to represent a different presentation.

.. _sect_FF.2.1.1:

Planar MPR Volumetric Transformations
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Planar MPR Volumetric Presentation State Storage SOP Classes support
a set of transformations to produce derived volumetric views of volume
input data.

The Grayscale Planar MPR Volumetric Presentation State Storage SOP Class
defines a grayscale volumetric view from a single volume input. The
sequence of transformations from volumetric inputs into P-Values is
explicitly defined in the reference pipeline described in
`figure_title <#figure_FF.2-1>`__.

The Compositing Planar MPR Volumetric Presentation State Storage SOP
Class defines a true color volumetric view from one or more volume
inputs. The sequence of transformations from volumetric inputs into
PCS-Values is explicitly defined in the reference pipeline described in
`figure_title <#figure_FF.2-2>`__. The actual sequence implemented may
differ (such as classifying and compositing prior to creating the MPR
view) but must result in similar appearance.

The planar MPR transformation requires a volume that is in the
Volumetric Presentation State Reference Coordinate System (VPS-RCS).

MPR generation is based on the attributes of the Multi-Planar
Reconstruction Geometry Module (see ). If the MPR Thickness Type
(0070,1502) is SLAB then the Rendering Method (0070,120D) is also used.

If Pixel Presentation (0008,9205) is MONOCHROME, then Presentation LUT
Shape (2050,0020) provides the transform to output P-Values.

If Pixel Presentation (0008,9205) is TRUE_COLOR, then Presentation State
Classification Component Sequence (0070,1801) describes the conversion
of each processed input into an RGB data stream, and Presentation State
Compositor Component Sequence (0070,1805) describes the compositing of
these separate RGBA data streams into a single RGB data stream. This
single RGB data stream is then processed as described by ICC Profile
(0028,2000) to produce output PCS-Values.

.. _sect_FF.2.1.2:

Volume Rendering Volumetric Transformations
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. _sect_FF.2.1.2.1:

Volume Rendering Pipelines
''''''''''''''''''''''''''

The Volume Rendering Volumetric Presentation State Storage SOP Classes
support a set of transformations to produce derived volumetric views of
volume input data. Attributes comprising the Volume Rendering Volumetric
Presentation States are defined in the context of the reference
pipelines described in this section. While the reference pipelines imply
a certain order of the volume rendering operations of classification,
resampling, shading, and compositing, the specific order in which these
operations are applied by any device claiming conformance to this
Standard are implementation-dependent and beyond the scope of this
Standard. It is the responsibility of the viewing application to
transform the Standard Attributes into parameters appropriate for the
particular order of operations implemented in the viewing application.

The Volume Rendering Volumetric Presentation State Storage SOP Class
defines a volumetric view from a single volume input to produce a volume
rendered view. The sequence of transformations from volumetric inputs
into PCS-Values is explicitly defined in the reference pipeline
described in `figure_title <#figure_FF.2.1.2.1-1>`__.

The Segmented Volume Rendering Volumetric Presentation State Storage SOP
Class defines a volumetric view from a single volume dataset with
optional segmentation croppings, each colored separately and blended
into the volume to be rendered. The sequence of transformations from
volumetric inputs into PCS-Values is explicitly defined in the reference
pipeline described in `figure_title <#figure_FF.2.1.2.1-2>`__.

There is a single item in the Volume Stream Sequence (0070,1A08) for
instances of this SOP Class.

The classified segmented volumes shall be blended in lowest to highest
priority order using B-over-A blending of the RGB data and the
corresponding opacity (alpha) data. The first item in the Presentation
State Classification Component Sequence (0070,1801) is the base upon
which subsequent items are cropped and B-over-A blended with it.

The Multiple Volume Rendering Volumetric Presentation State Storage SOP
Class defines a volumetric view from more than one volume input. The
sequence of transformations from volumetric inputs into PCS-Values is
explicitly defined in the reference pipeline described in
`figure_title <#figure_FF.2.1.2.1-3>`__. The specific algorithms for
volume rendering may differ, but must result in a similar appearance.

It is expected that all volume inputs are spatially registered to the
Volumetric Presentation State - Reference Coordinate System. The
specific step in the processing at which resampling is performed to
achieve this spatial registration is an implementation decision.

Each item in the Volume Stream Sequence (0070,1A08) produces one input
to a RGBA Compositor.

Transformation to PCS-Values is performed after Volume Rendering.

.. _sect_FF.2.1.2.2:

Volume Rendering Component
''''''''''''''''''''''''''

This component transforms an RGBA volume into a volume rendered view
according to the parameters in the Render Geometry Module. This
component is implementation dependent, but generally includes processing
steps such as gradient computation to find normals of use in the shading
operation, resampling of volume data, shading according to the
parameters in the Render Shading Module, and compositing of the
resampled data to produce the final volume rendered view.

.. _sect_FF.2.1.2.3:

Graphic Projection Component
''''''''''''''''''''''''''''

This component converts the volumetric annotation specified in the
Volumetric Graphic Annotation module into a graphic overlay for the 2D
volume rendered view. It is the role of this component to evaluate the
volumetric graphic annotations, determine which graphics are visible in
the volume rendered view, and provide graphics that are layered on the
view.

Inputs to the Graphic Projection component are:

-  Volumetric Graphic Annotation Module

-  RGBA volume input to the Volume Rendering component

-  Volume Render Geometry Module

-  Input-specific Cropping Specification Index (0070,1205) values

-  Volume Cropping Module Attributes

The Graphic Projection transform algorithm considers whether each
volumetric graphic annotation is visible in the current volume rendered
view, considering the volume data, Volume Render Geometry, and the value
of Annotation Clipping (0070,1907).

If Annotation Clipping (0070,1907) is YES, then the annotation shall be
visible only if it is present in the field of view and not obscured by
opaque structures that may lie between the annotation and the viewpoint.
In the case of the Volumetric Presentation Input Annotation Sequence
(0070,1905), annotation text shall be visible only if some part of the
specified segmentation is visible.

If Annotation Clipping (0070,1907) is NO, then the annotation shall
always be visible. A particular implementation may display annotations
that lie behind opaque structures in a different style (such as a softer
gray), but the decision to provide such display style is outside the
scope of this Standard.

The output of the Graphic Projection component is displayed on the 2D
presentation view in the graphic layers specified by the corresponding
values of Graphic Layer (0070,0002).

.. _sect_FF.2.2:

Volumetric Inputs, Registration and Cropping
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A Volumetric Presentation State can take multiple volumes as input. A
volume is defined in . The same source data can be referenced in more
than one input.

For each input volume, the Modality LUT or Rescale Slope and Rescale
Intercept transformation(s) as specified in the source image(s) is
applied first to the pixel data, otherwise an identity transformation
shall be assumed.

.. note::

   In enhanced multi-frame IODs this is specified in the Pixel Value
   Transformation Functional Group.

The VOI LUT encoded in the Volumetric Presentation State, if any, is
next applied to the input data, otherwise an identity transformation
shall be assumed.

The input volumes may or may not be in the Volumetric Presentation State
Reference Coordinate System (VPS-RCS). If they are not, they shall be
registered into the VPS-RCS.

Two methods of cropping the input volumes are provided:

-  All inputs to the Volumetric Presentation State may be cropped using
   the common cropping methods specified by Global Crop (0070,120B) and
   items in the Volume Cropping Sequence (0070,1301).

-  In addition, cropping may be specified independently for each input
   to the Volumetric Presentation State as specified by the value of
   Crop (0070,1204) and items in the Volume Cropping Sequence
   (0070,1301).

.. note::

   Combinations of cropping methods may be specified. For example, all
   inputs could be cropped using global bounding box cropping in
   addition to another cropping method applied to one of more individual
   inputs to the Volumetric Presentation State.

.. _sect_FF.2.3:

Volumetric Presentation State Display
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. _sect_FF.2.3.1:

Volumetric Presentation State Display Overview
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The MPR Volumetric Presentation State Display Module defines the
algorithms used to transform the result of the MultiPlanar
Reconstruction volumetric processing on the input data into an output of
P-Values or PCS-Values for display.

The Render Display Module defines the algorithms used to transform the
result of the Volume Rendering processing on the input data into output
RGBA values. Presentation State Classification Component Sequence
(0070,1801) describes the conversion of each cropped input into an RGBA
volumetric data stream. Volume Stream Sequence (0070,1209) describes
RGBA volumetric data streams which are overlayed using ordered "B over
A" blending into a volumetric data stream. Presentation State Compositor
Component Sequence (0070,1805) describes how the “B over A” blended
volumetric data streams are to be composited together into a single RGBA
volumetric data stream. This single RGBA data stream is an input to the
Volume Rendering component.

.. _sect_FF.2.3.2:

Description of Display Components
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. _sect_FF.2.3.2.1:

Classification Component Components
'''''''''''''''''''''''''''''''''''

There are two classification component types currently defined for
conversion from scalar input data to RGBA. The defined components are:

-  One Input -> RGBA: This component accepts reconstructed data from one
   input in the Volumetric Presentation State Input Sequence (0070,1201)
   and generates an RGB and an Alpha output. This classification
   component would be specified in an item of the Presentation State
   Classification Component Sequence (0070,1801):

-  Two Inputs -> RGBA: This component accepts reconstructed data from
   two inputs in the Volumetric Presentation State Input Sequence
   (0070,1201) and generates an RGB and an Alpha output. This component
   is used in the case where a two-dimensional color mapping needs to be
   performed. This classification component would be specified in an
   item of the Presentation State Classification Component Sequence
   (0070,1801):

   .. note::

      An example for the use of this component is to combine Ultrasound
      Flow Velocity and Ultrasound Flow Variance to produce a color
      range from red-blue based on flow velocity and adding a
      yellow-green tinge based on flow variance)

.. _sect_FF.2.3.2.2:

Compositor Components
'''''''''''''''''''''

There are two compositor component types defined for compositing of two
input RGBA (or one RGBA and one RGB) data sources. The defined
components are:

-  RGB Compositor: This component accepts two RGBA inputs (with one
   Alpha input optional) and composites the data into a single RGB
   output. Each item of Presentation State Compositor Component Sequence
   (0070,1805) specifies one RGB Compositor component:

-  RGBA Compositor: This component accepts two RGBA inputs and
   composites the data into a single RGB output and a single Alpha
   output.

.. _sect_FF.2.3.3:

Internal Structure of Components
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. _sect_FF.2.3.3.1:

Internal Structure of Classification Components
'''''''''''''''''''''''''''''''''''''''''''''''

Component Type (0070,1802) specifies the component defined in each item
of Presentation State Classification Component Sequence (0070,1801),
which in turn controls by conditions the rest of the content of the item
to provide the necessary specification of the component. The internal
structure of each component in block diagram form is as follows:

-  One Input -> RGBA: Specified by Component Type (0070,1802) =
   ONE_TO_RGBA:

-  Two Inputs -> RGBA: If Component Type (0070,1802) = TWO_TO_RGBA:

The number of most significant bits extracted from each input is
specified by the value of Bits Mapped to Color Lookup Table (0028,1403)
in the Component Input Sequence (0070,1803) item for that input.

If Component Type (0070,1802) = TWO_TO_RGBA, there shall be two items in
Component Input Sequence (0070,1803) with the first item defining the
source of the most significant bits of the Palette Color Lookup Table
input and the second item defining the source of the least significant
bits of the Palette Color Lookup Table input

.. _sect_FF.2.3.3.2:

Internal Structure of RGB and RGBA Compositor Components
''''''''''''''''''''''''''''''''''''''''''''''''''''''''

Weighting transfer functions that compute the weighting factors used by
the Compositor Function as a function of Alpha\ :sub:`1` and
Alpha\ :sub:`2` values are specified as weighting look-up tables (LUTs)
in the RGB and RGBA Compositor components. The RGB and RGBA Compositor
components are identical except for the compositing of the additional
Alpha component in the RGBA Compositor:

Because each Weighting LUT uses both Alpha values in determining a
weighting factor, they allow compositing functions that would not be
possible if each weighting factor were based only on that input's Alpha
value. See for typical usage of the Weighting LUTs.

The input bits to the Weighting LUTs are obtained by combining the two
Alpha inputs, with half the input bits obtained from each Alpha input:

-  In the case of the first compositor component corresponding to the
   first item in Presentation State Compositor Component Sequence
   (0070,1805), the Alpha from the classification component
   corresponding to the first item in the Presentation State
   Classification Component Sequence (0070,1805) provides the most
   significant bits of the Weighting LUT inputs, while the Alpha from
   the classification component corresponding to the second item in the
   Presentation State Classification Component Sequence (0070,1805)
   provides the least significant bits of the Weighting LUT inputs.

-  In the case of subsequent compositor components, the Alpha from the
   classification component corresponding to the next item in the
   Presentation State Classification Component Sequence (0070,1805)
   provides the least significant bits of the Weighting LUT inputs,
   while the most significant bits of the Weighting LUT inputs are
   computed as one minus the Alpha from the classification component
   corresponding to the next item in the Presentation State
   Classification Component Sequence (0070,1805).

The integer outputs of the Weighting LUTs are normalized to the range
0.0 to 1.0, and the Compositor Function combines the normalized R, G, B
and Alpha (each component called "Color" = C\ :sub:`x`) input values as
follows:

*C\ out = (C\ 1\ \*Weight\ 1) + (C\ 2\ \*Weight\ 2)*

The sum of the normalized Weight\ :sub:`1` and Weight\ :sub:`2` shall be
no greater than 1.0.

The color input values are normalized because the number of output bits
from the RGB Palette Color Lookup Tables and the Alpha Palette Color
Lookup Table may be different in each classification component.

The output of the compositor shall be range-limited ("clamped") to
ensure that the outputs are guaranteed to be within a valid range of
color values regardless of the validity of the weighting transfer
functions. This isolates subsequent compositor components and the
Profile Connection Space Transform from overflow errors.

.. _sect_FF.2.4:

Additional Volumetric Considerations
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. _sect_FF.2.4.1:

Annotations in Volumetric Presentations States
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Volumetric Presentation States provide two ways for annotating
views:

-  Annotations on the Volumetric Presentation View

-  Annotations described by coordinates in the Volumetric Presentation
   State Reference Coordinate System (VPS-RCS) with optional references
   to Structured Reports providing context.

Annotations on the view provide the application of free unformatted text
or vector graphics as described in the . Since the Graphic Annotation
Module allows only the addition of graphics to the 2D view defined by
the Presentation State without attached clinical meaning, Volumetric
Graphic Annotations provide a mechanism to create annotations in the
VPS-RCS with optional references to other objects which can have
structured context attached.

Volumetric Graphic Annotations can be specified in two variants: either
via Graphic Types with 3D coordinates, as defined in , or via a
reference to inputs of the Presentation State. The latter is intended to
be used to display annotation labels for segmentations of the volume
data; for example, when a lesion has been marked via a Segmentation IOD
and this segmentation is rendered together with the anatomical data.

Since annotations which are added via the Graphic Annotation Module are
defined within the display space, they should not be used to point to
clinical relevant structures which would be positioned on a different
anatomy after manipulation.

In contrast since Volumetric Graphic Annotations have coordinates in the
VPS-RCS, applications can still show them after a user has manipulated
the initial view which has been defined by the Presentation State.

The exact visual representation of the annotations is at the discretion
of the display application, as well as the mechanisms which may be
employed to ensure that Volumetric Graphic Annotations are sufficiently
visible, even if the location in the volume is not visible in the
current view. E.g. for a Graphic Type POINT a display application might
render a crosshair at the specified position in the volume or a sphere
with an arrow pointing to it instead of rendering Volumetric Graphic
Annotations directly within the volume a projection of the annotations
may be rendered as an overlay on top of the view.

However, annotations can be grouped into Graphic Layers and it is
suggested that applications provide mechanisms to define rendering
styles per Graphic Layer.

See and for examples of Volumetric Graphic Annotations.

.. _sect_FF.2.4.2:

Volumetric Animation
^^^^^^^^^^^^^^^^^^^^

Several different styles of animation are defined in Volumetric
Presentation States. In general, an animation style will vary either the
input, processing, or view geometry in order to produce a varying
presentation view. This section describes each of the animation styles
and how it produces an animated view.

.. _sect_FF.2.4.2.1:

Input Sequence Animation
''''''''''''''''''''''''

A Presentation Animation Style (0070,1A01) value of INPUT_SEQ indicates
that Input Sequence Animation is being specified. In this animation
style, a single Volumetric Presentation State is defined which includes
input items in the Volumetric Presentation State Input Sequence
(0070,1201) with different values of Input Sequence Position Index
(0070,1203). The animated presentation view is produced by sequencing
through values of Input Sequence Position Index (0070,1203) at a
specified animation rate Recommended Animation Rate (0070,1A03), where
each value of the index produces one 'frame' of the animated view from
inputs that have that value of Input Sequence Position Index
(0070,1203). See `figure_title <#figure_FF.3.2-1>`__.

.. note::

   For example, a set of inputs could be temporally related volumes of a
   moving anatomical structure like the heart.

There may be more than one input item in Volumetric Presentation State
Input Sequence (0070,1201) with the same value of Input Sequence
Position Index (0070,1203), in which case the inputs are processed
together to produce the frame of the animated view.

.. note::

   For example, pairs of input items could represent the same volume
   input at a point in time with two different segmentation croppings
   (representing different organ structures) that are blended together
   into a single view.

.. _sect_FF.2.4.2.2:

Presentation Sequence Animation
'''''''''''''''''''''''''''''''

A Presentation Animation Style (0070,1A01) value of PRESENTATION_SEQ
indicates that Presentation Sequence Animation is being specified. In
this animation style, a set of Volumetric Presentation States are
applied sequentially. See `figure_title <#figure_FF.3.2-2>`__.

.. note::

   One example of the use of presentation sequence animation is a view
   of a moving heart wherein a stent is at a stationary position at the
   center of the view. Because the geometry of each view frame is
   slightly different, separate Volumetric Presentation State instances
   are required for each view frame.

Each Volumetric Presentation State of the set is identified by having
the same value of Presentation Sequence Collection UID (0070,1102). The
order of application of these Presentation States is determined by the
value of Presentation Sequence Position Index (0070,1103) defined in the
Presentation State. The animated presentation view is produced by
sequencing through values of presentation sequence position index at a
specified animation rate Recommended Animation Rate (0070,1A03), where
each value of the index produces one 'frame' of the animated view
produced by that Volumetric Presentation State.

.. _sect_FF.2.4.2.3:

Crosscurve Animation
''''''''''''''''''''

A Presentation Animation Style (0070,1A01) value of CROSSCURVE indicates
that Crosscurve Animation is being specified. In this animation style, a
Presentation State defines a Planar MPR view at the beginning of a curve
defined in Animation Curve Sequence (0070,1A04). The Planar MPR view is
stepped a distance Animation Step Size (0070,1A05) along the curve
defined in Animation Curve Sequence (0070,1A04) at the rate specified by
Recommended Animation Rate (0070,1A03) in steps per second. See
`figure_title <#figure_FF.3.2-3>`__.

.. note::

   A typical application of this animation style is motion along a curve
   centered within the colon or a blood vessel.

.. _sect_FF.2.4.2.4:

Flythrough Animation
''''''''''''''''''''

A Presentation Animation Style (0070,1A01) value of FLYTHROUGH indicates
that Flythrough Animation is being specified. In this animation style,
the Volumetric Presentation State defines an initial volume rendered
view and a specified movement of the view along a path through the
volume. See `figure_title <#figure_FF.2.4.2.4-1>`__.

.. _sect_FF.2.4.2.5:

Swivel Animation
''''''''''''''''

A Presentation Animation Style (0070,1A01) value of SWIVEL indicates
that Swivel Animation is being specified. In this animation style, a
Presentation State defines an initial volume rendered using Viewpoint
Position (0070,1603), Viewpoint LookAt Point (0070,1604) and Viewpoint
Up Direction (0070,1605). When the animation begins, the view begins to
rotate back and forth about an axis parallel to the Viewpoint Up
Direction (0070,1605) that intersects the Viewpoint LookAt Point
(0070,1604). The extent of the arc of rotation is defined by Swivel
Range (0070,1A06) and the maximum rate of rotation is specified by
Recommended Animation Rate (0070,1A03) in degrees per second, although
it is recommended that the changes of direction at the ends of the
swivel range be smooth which implies a slowing of the rotation as the
endpoints are approached.

.. _sect_FF.2.5:

Display Layout
^^^^^^^^^^^^^^

The layout of multiple Volumetric Presentation States is not specified
by the Volumetric Transformation process. However, there are attributes
within Volumetric Presentation States that can influence the overall
display layout.

For instance:

-  Anatomic Region Sequence (0008,2218) specifies the anatomic region
   covered by the Volumetric Presentation State

-  View Code Sequence (0054,0220) describes the view of the anatomic
   region of interest (e.g., Coronal, Oblique transverse, etc.)

-  Presentation Display Collection UID (0070,1101) identifies the
   Presentation State as one of a set of views intended to be displayed
   together

-  SOP Class UID (0008,0016) identifies that the Presentation State
   describes the volumetric view

The use of these attributes allows a display application to create an
appropriate presentation of multiple Volumetric Presentation States,
whether through the application of a Hanging Protocol instance, a
Structured Display instance or by means of an application-specific
algorithm.

For an example of their use, see .

.. _sect_FF.3:

Behavior of An SCP
------------------

In addition to the behavior for the Storage Service Class specified in
`Behavior of an SCP <#sect_B.2.2>`__, the following additional
requirements are specified for the Volumetric Presentation State Storage
SOP Classes:

-  a display device acting as an SCP of these SOP Classes shall make all
   mandatory presentation attributes available for application to the
   referenced volumetric data at the discretion of the display device
   user, for all Image Storage SOP Classes defined in the Conformance
   Statement for which the Volumetric Presentation State Storage SOP
   Class is supported.

-  a display device acting as an SCP of the Volumetric Presentation
   State Storage SOP Classes shall support the Segmentation SOP Class
   for cropping and the Spatial Registration SOP Class for registration.

-  a display device acting as an SCP of a Volume Rendering Volumetric
   Presentation State Storage SOP Class shall perform an unshaded volume
   rendering if the Render Shading Module is absent from the SOP
   Instance.

-  a display device acting as an SCP of the Volumetric Presentation
   State Storage SOP Classes is not required to support the Presentation
   Animation Module.

-  a display device acting as an SCP of any of the Volumetric
   Presentation State Storage SOP Classes is not required to support
   Structured Reporting Storage SOP Classes.

.. _sect_FF.4:

Conformance
-----------

In addition to the Conformance Statement requirements for the Storage
Service Class specified in `Conformance Statement
Requirements <#sect_B.4.3>`__, the following additional requirements are
specified for the Volumetric Presentation State Storage SOP Classes:

.. _sect_FF.4.1:

Conformance Statement For An SCU
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The following behavior shall be documented in the Conformance Statement
of any implementation claiming conformance to a Volumetric Presentation
State Storage SOP Class as an SCU:

-  For an SCU of a Volumetric Presentation State Storage SOP Class that
   is creating a SOP Instance of the Class, the manner in which
   presentation related attributes are derived from a displayed image,
   operator intervention or defaults, and how they are included in the
   IOD.

-  For an SCU of a Volumetric Presentation State Storage SOP Class, the
   Image Storage SOP Classes that are also supported by the SCU and
   which may be referenced by instances of the Volumetric Presentation
   State Storage SOP Class.

.. _sect_FF.4.2:

Conformance Statement For An SCP
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The following behavior shall be documented in the Conformance Statement
of any implementation claiming conformance to a Volumetric Presentation
State Storage SOP Class as an SCP:

-  For an SCP of a Volumetric Presentation State Storage SOP Class that
   is displaying an image referred to by a SOP Instance of the Class,
   the manner in which presentation related attributes are used to
   influence the display of an image.

-  For an SCP of a Volumetric Presentation State Storage SOP Class, the
   Image Storage SOP Classes that are also supported by the SCP and
   which may be referenced by instances of the Volumetric Presentation
   State Storage SOP Class.

-  For an SCP of a Volumetric Presentation State Storage SOP Class,
   whether the Presentation Animation Module is supported, and if not
   supported, any notifications or lack of notifications to the user
   that the context information is not displayed.

-  For an SCP of a Volumetric Presentation State Storage SOP Class,
   whether references to Structured Report instances are supported, and
   if not supported, any notifications or lack of notifications to the
   user that the context information is not displayed.

