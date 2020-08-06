.. _chapter_O:

Registration (Informative)
==========================

.. _sect_O.1:

Spatial Registration and Spatial Fiducials SOP Classes
------------------------------------------------------

These SOP Classes allow describing spatial relationships between sets of
images. Each instance can describe any number of registrations as shown
in `figure_title <#figure_O.1-1>`__. It may also reference prior
registration instances that contribute to the creation of the
registrations in the instance.

A Reference Coordinate System (RCS) is a spatial Frame of Reference
described by the DICOM Frame of Reference Module. The chosen Frame of
Reference of the Registration SOP Instance may be the same as one or
more of the Referenced SOP Instances. In this case, the Frame of
Reference UID (0020,0052) is the same, as shown by the Registered RCS in
the figure. The registration information is a sequence of spatial
transformations, potentially including deformation information. The
composite of the specified spatial transformations defines the complete
transformation from one RCS to the other.

Image instances may have no DICOM Frame of Reference, in which case the
registration is to that single image (or frame, in the case of a
Multi-frame Image). The Spatial Registration IOD may also be used to
establish a coordinate system for an image that has no defined Frame of
Reference. To do this, the center of the top left pixel of the source
image is treated as being located at (0, 0, 0). Offsets from the first
pixel are computed using the resolution specified in the Source IOD.
Multiplying that coordinate by the Transformation matrix gives the
patient coordinate in the new Frame of Reference.

A special case is an atlas. DICOM has defined Well-Known Frame of
Reference UIDs for several common atlases. There is not necessarily
image data associated with an atlas.

When using the Spatial Registration or Deformable Registration SOP
Classes there are two types of coordinate systems. The coordinate system
of the referenced data is the *Source RCS*. The coordinate system
established by the SOP instance is the *Registered RCS*.

The sense of the direction of transformation differs between the Spatial
Registration SOP Class and the Deformable Spatial Registration SOP
Class. The Spatial Registration SOP Class specifies a transformation
that maps Source coordinates, in the Source RCS, to Registered
coordinates, in the Registered RCS. The Deformable Spatial Registration
SOP Class specifies transformations that map Registered coordinates, in
the Registered RCS, to coordinates in the Source RCS.

The Spatial Fiducials SOP Class stores spatial fiducials as implicit
registration information.

.. _sect_O.2:

Functional Use Cases
--------------------

**Multi-Modality Fusion:** A workstation or modality performs a
registration of images from independent acquisition modalities-PET, CT,
MR, NM, and US-from multiple series. The workstation stores the
registration data for subsequent visualization and image processing.
Such visualization may include side-by-side synchronized display, or
overlay (fusion) of one modality image on the display of another. The
processes for such fusion are beyond the scope of the Standard. The
workstation may also create and store a ready-for-display fused image,
which references both the source image instances and the registration
instance that describes their alignment.

**Prior Study Fusion:** Using post processing or a manual process, a
workstation creates a spatial object registration of the current Study's
Series from prior Studies for comparative evaluation.

**Atlas Mapping:** A workstation or a CAD device specifies fiducials of
anatomical features in the brain such as the anterior commissure,
posterior commissure, and points that define the hemispheric fissure
plane. The system stores this information in the Spatial Fiducials SOP
Instance. Subsequent retrieval of the fiducials enables a device or
workstation to register the patient images to a functional or anatomical
atlas, presenting the atlas information as overlays.

**CAD:** A CAD device creates fiducials of features during the course of
the analysis. It stores the locations of the fiducials for future
analysis in another imaging procedure. In the subsequent CAD procedure,
the CAD device performs a new analysis on the new data. As before, it
creates comparable fiducials, which it may store in a Spatial Fiducials
SOP Instance. The CAD device then performs additional analysis by
registering the images of the current exam to the prior exam. It does so
by correlating the fiducials of the prior and current exam. The CAD
device may store the registration in Registration SOP Instance.

**Adaptive Radiotherapy:** A CT Scan is taken to account for variations
in patient position prior to radiation therapy. A workstation performs
the registration of the most recent image data to the prior data,
corrects the plan, and stores the registration and revised plan.

**Image Stitching:** An acquisition device captures multiple images,
e.g., DX images down a limb. A user identifies fiducials on each of the
images. The system stores these in one or more Fiducial SOP Instances.
Then the images are "stitched" together algorithmically by means that
utilize the Fiducial SOP Instances as input. The result is a single
image and optionally a Registration SOP Instance that indicates how the
original images can be transformed to a location on the final image.

.. _sect_O.3:

System Interaction
------------------

`figure_title <#figure_O.3-1>`__ shows the system interaction of storage
operations for a registration of MR and CT using the Spatial
Registration SOP Class. The Image Plane Module Attributes of the CT
Series specify the spatial mapping to the RCS of its DICOM Frame of
Reference.

The receiver of the Registration SOP Instance may use the spatial
transformation to display or process the referenced image data in a
common coordinate system. This enables interactive display in 3D during
interpretation or planning, tissue classification, quantification, or
Computer Aided Detection. `figure_title <#figure_O.3-2>`__ shows a
typical interaction scenario.

In the case of coupled acquisition modalities, one acquisition device
may know the spatial relationship of its image data relative to the
other. The acquisition device may use the Registration SOP Class to
specify the relationship of modality B images to modality A images as
shown below in `figure_title <#figure_O.3-3>`__. In the most direct
case, the data of both modalities are in the same DICOM Frame of
Reference for each SOP Class Instance.

A Spatial Registration instance consists of one or more instances of a
Registration. Each Registration specifies a transformation from the RCS
of the Referenced Image Set, to the RCS of this Spatial Registration
instance (see ) identified by the Frame of Reference UID (0020,0052).

.. _sect_O.4:

Overview of Encoding
--------------------

`figure_title <#figure_O.4-1>`__ shows an information model of a Spatial
Registration to illustrate the relationship of the Attributes to the
objects of the model. The DICOM Attributes that describe each object are
adjacent to the object.

`figure_title <#figure_O.4-2>`__ shows an information model of a
Deformable Spatial Registration to illustrate the relationship of the
Attributes to the objects of the model. The DICOM Attributes that
describe each object are adjacent to the object.

`figure_title <#figure_O.4-3>`__ shows a Spatial Fiducials information
model to illustrate the relationship of the Attributes to the objects of
the model. The DICOM Attributes that describe each object are adjacent
to the object.

.. _sect_O.5:

Matrix Registration
-------------------

A 4x4 affine transformation matrix describes spatial rotation,
translation, scale changes and affine transformations that register
referenced images to the Registration IE's homogeneous RCS. These steps
are expressible in a single matrix, or as a sequence of multiple
independent rotations, translations, or scaling, each expressed in a
separate matrix. Normally, registrations are rigid body, involving only
rotation and translation. Changes in scale or affine transformations
occur in atlas registration or to correct minor mismatches.

.. _sect_O.6:

Spatial Fiducials
-----------------

Fiducials are image-derived reference markers of location, orientation,
or scale. These may be labeled points or collections of points in a data
volume that specify a shape. Most commonly, fiducials are individual
points.

Correlated fiducials of separate image sets may serve as inputs to a
registration process to estimate the spatial registration between
similar objects in the images. The correlation may, or may not, be
expressed in the fiducial identifiers. A fiducial identifier may be an
arbitrary number or text string to uniquely identify each fiducial from
others in the set. In this case, fiducial correlation relies on operator
recognition and control.

Alternatively, coded concepts may identify the acquired fiducials so
that systems can automatically correlate them. Examples of such coded
concepts are points of a stereotactic frame, prosthesis points, or
well-resolved anatomical landmarks such as bicuspid tips. Such codes
could be established and used locally by a department, over a wider area
by a society or research study coordinator, or from a standardized set.

The table below shows each case of identifier encoding. A and B
represent two independent registrations: one to some image set A, and
the other to image set B.

+--------------+--------------------------+--------------------------+
|              | **Fiducial Identifier    | **Fiducial Identifier    |
|              | (0070,0310)**            | Code Sequence            |
|              |                          | (0070,0311)**            |
+==============+==========================+==========================+
| Uncorrelated | A: 1, 2, 3               | A: (1, 99_A_CSD, *label  |
|              |                          | A1*) …                   |
|              | B: 4, 5, 6               |                          |
|              |                          | B: (4, 99_B_CSD, *label  |
|              |                          | B4*) …                   |
+--------------+--------------------------+--------------------------+
| Correlated   | A: 1, 2, 3 …             | A: (1, 99_MY_CSD, *label |
|              |                          | 1*) …                    |
|              | B: 1, 2, 3 …             |                          |
|              |                          | B: (1, 99_MY_CSD, *label |
|              |                          | 1*) …                    |
+--------------+--------------------------+--------------------------+

Fiducials may be a point or some other shape. For example, three or more
arbitrarily chosen points might designate the inter-hemispheric plane
for the registration of head images. Many arbitrarily chosen points may
identify a surface such as the inside of the skull.

A fiducial also has a Fiducial UID. This UID identifies the creation of
the fiducial and allows other SOP Instances to reference the fiducial
assignment.

