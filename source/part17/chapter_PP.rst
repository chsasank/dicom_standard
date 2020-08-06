.. _chapter_PP:

3D Ultrasound Volumes (Informative)
===================================

.. _sect_PP.1:

Purpose of This Annex
---------------------

The purpose of this annex is to identify the clinical use cases that
drove the development of Enhanced US Volume Object Definition for 3D
Ultrasound image storage. They represent the clinical needs that must be
addressed by interoperable Ultrasound medical devices and compatible
workstations exchanging 3D Ultrasound image data. The use cases listed
here are reviewed by representatives of the clinical community and are
believed to cover most common applications of 3D Ultrasound data.

.. _sect_PP.2:

3D Ultrasound Clinical Use Cases
--------------------------------

.. _sect_PP.2.1:

Use Cases
~~~~~~~~~

The following use cases consider the situations in which 3D Ultrasound
data is produced and used in the clinical setting:

1.  An ultrasound scanner generates a Volume Data set consisting of a
    set of parallel XY planes whose positions are specified relative to
    each other and/or a transducer frame-of-reference, with each plane
    containing one or more frames of data of different ultrasound data
    types. Ultrasound data types include, but are not limited to
    reflector intensity, Doppler velocity, Doppler power, Doppler
    variance, etc.

2.  An ultrasound scanner generates a set of temporally related Volume
    Data sets, each as described in Case1. Includes a set of volumes
    that are acquired sequentially, or acquired asynchronously and
    reassembled into temporal sequence (such as through the
    "Spatial-Temporal Image Correlation" (STIC) technique).

3.  Any Volume Data set may be operated upon by an application to create
    one or more Multi-Planar Reconstruction (MPR) views (as in Case7)

4.  Any Volume Data set may be operated upon by an application to create
    one or more Volume Rendered views (as in Case8)

5.  Make 3D size measurements on a volume in 3D-space

6.  An ultrasound scanner generates 3D image data consisting of one or
    more 2D frames that may be displayed, including

    a. A single 2D frame

    b. A temporal loop of 2D frames

    c. A loop of 2D frames at different spatial positions and/or
       orientations positions relative to one another

    d. A loop of 2D frames at different spatial positions, orientations,
       and/or times relative to one another

7.  An ultrasound scanner generates 3D image data consisting of one or
    more MPR Views that may be displayed as ordinary 2D frames,
    including

    a. An MPR View

    b. A temporal loop of MPR Views

    c. A loop of MPR Views representing different spatial positions
       and/or orientations relative to one another

    d. A loop of MPR Views representing different spatial positions,
       orientations, and/or times relative to one another

    e. A collection of MPR Views related to one another (example: 3
       mutually orthogonal MPR Views around the point of intersection)

8.  An ultrasound scanner generates 3D image data consisting of one or
    more Volume Rendered Views that may be displayed as ordinary 2D
    frames, including

    a. An Rendered View

    b. A temporal loop of Rendered Views

    c. A loop of Rendered Views with a varying observer point

    d. A temporal loop of Rendered Views with a varying observer point

    .. note::

       Images in this group are not normally measurable because each
       pixel in the 2D representation may be comprised of data from many
       pixels in depth along the viewing ray and does not correspond to
       any particular point in 3D-space.

9.  Allow successive display of frames in multi-frame objects in cases
    6, 7, and 8.

10. Make size measurements on 2D frames in cases 6, 7, and 8.

11. Separation of different data types allows for independent display
    and/or processing of image data (for example, color suppression to
    expose tissue boundaries, grayscale suppression for vascular flow
    trees, elastography, etc.)

12. Represent ECG and other physiological waveforms synchronized to
    acquired images.

13. Two-stage Retrieval: The clinician initially queries for and
    retrieves all the images in an exam that are directly viewable as
    sets of frames. Based on the review of these images (potentially on
    a legacy review application), the clinician may decide to perform
    advanced analysis of a subset of the exam images. Volume Data sets
    corresponding to those images are subsequently retrieved and
    examined.

14. An ultrasound scanner allows user to specify qualitative patient
    orientation (e.g., Left, Right, Medial, etc.) along with the image
    data.

15. An ultrasound scanner may maintain a patient-relative frame of
    reference (obtained such as through a gantry device) along with the
    image data.

16. Fiducial markers that tag anatomical references in the image data
    may be specified along with the image data.

17. Key Images of clinical interest are identified and either the entire
    image, or one or more frames or a volume segmentation within the
    image must be tagged for later reference.

.. _sect_PP.2.2:

Hierarchy of Use Cases
~~~~~~~~~~~~~~~~~~~~~~

This section organizes the list of use cases into a hierarchy. `3D
Ultrasound Solutions in DICOM <#sect_PP.3>`__ maps items in this
hierarchy to specific solutions in the DICOM Standard.

1. Data

   a. 3D Volume Data

      i.   Static and Dynamic volume data (Cases 1 and 2)

      ii.  Suitable for applications that create MPR and Render views
           (Cases 3 and 4)

      iii. 3D size measurements (Case 5)

   b. 2D representations of 3D volume data (Cases 6, 7, and 8)

      i.  Static and Dynamic varieties (Case 9)

      ii. 2D size measurements (Case 10)

   c. Separation of data types (Case 11)

   d. Integrate physiological waveforms with image acquisition (Case 12)

2. Workflow

   a. Permit Two-step review (Case 13)

      i.  Review 2D representations first (potentially on legacy viewer)

      ii. On-demand operations on 3D volume data

   b. Frame of Reference

      i.   Frame-relative

      ii.  Probe-relative

      iii. Patient-relative (Cases 14 and 15)

      iv.  Anatomical (Fiducials) (Case 16)

   c. Identify Key images (Case 17)

.. _sect_PP.3:

3D Ultrasound Solutions in DICOM
--------------------------------

This section maps the use case hierarchy in `Hierarchy of Use
Cases <#sect_PP.2.2>`__ to specific solutions in the DICOM Standard. As
described in items 1a and 1b, there are two different types of data
related to 3D image acquisition: the 3D volume data itself and 2D images
derived from the volume data. See `figure_title <#figure_PP.3-1>`__.

.. _sect_PP.3.1:

3D Volume Data sets
~~~~~~~~~~~~~~~~~~~

The 3D volume data is conveyed via the Enhanced US Volume SOP Class,
which represents individual 3D Volume Data sets or collections of
temporally-related 3D Volume Data sets using the 'enhanced' multi-frame
features used by Enhanced Storage SOP Classes for other modalities,
including shared and per-frame functional group sequences and
multi-frame dimensions. The 3D Volume Data sets represented by the
Enhanced Ultrasound IOD (the striped box in
`figure_title <#figure_PP.3-1>`__) are suitable for Multi-Planar
Reconstruction (MPR) and 3D rendering operations. Note that the
generation of the Cartesian volume, its relationship to
spatially-related 2D frames (whether the volume was created from
spatially-related frames, or spatially-related frames extracted from the
Cartesian volume), and the algorithms used for MPR or 3D rendering
operations are outside the scope of this Standard.

Functional Group Macros allow the storage of many parameters describing
the acquisition and positioning of the image planes relative to the
patient and external frame of references (such as a gantry or probe
locating device). These macros may apply to the entire instance (Shared
Functional Group) or may vary frame-to-frame (Per-Frame Functional
Group).

Multi-frame Dimensions are used to organize the data type, spatial, and
temporal variations among frames. Of particular interest is Data Type
used as a dimension to relate frames of different data types (like
tissue and flow) comprising each plane of an ultrasound image (item 1c
in the use case hierarchy). Refer to for the use of Dimensions with the
Enhanced US Volume SOP Class.

Sets of temporally-related volumes may have been acquired sequentially
or acquired asynchronously and reassembled into a temporal sequence,
such as through Spatial-Temporal Image Correlation (STIC). Regardless of
how the temporal volume sequence was acquired, frames in the resultant
volumes are marked with a temporal position value, such as Temporal
Position Time Offset (0020,930D) indicating the temporal position of the
resultant volumes independent of the time sequence of the acquisition
prior to reassembly into volumes.

.. _sect_PP.3.2:

2D Derived Images
~~~~~~~~~~~~~~~~~

The 2D image types represent collections of frames that are related to
or derived from the volume data, namely Render Views (projections),
separate Multi-Planar Reconstruction (MPR) views, or sets of
spatially-related source frames, either parallel or oblique (the
cross-hatched images in `figure_title <#figure_PP.3-1>`__). The
Ultrasound Image and Ultrasound Multi-frame Image IODs are used to
represent these related or derived 2D images. The US Image Module for
the Ultrasound Image Storage and Ultrasound Multi-frame Image Storage
SOP Classes have defined terms for "3D Rendering" (render or MPR views)
and "Spatially Related Frames" in value 4 of the Image Type (0008,0008)
Attribute to specify that the object contains these views while
maintaining backwards compatibility with Ultrasound review applications
for frame-by-frame display, which may be displayed sequentially
("fly-through" or temporal) loop display or as a side-by-side
("light-box") display of spatially-related slices. Also, the optional
Source Image Sequence (0008,2112) and Derivation Code Sequence
(0008,9215) Attributes may be included to more succinctly specify the
type of image contained in the instance and the 3D Volume Data set from
which it was derived.

2D Derived image instances should be linked to the source 3D Volume Data
set through established DICOM reference mechanisms. This is necessary to
support the "Two-Stage Review" use case. Consider the following
examples:

1. In the case of a 3D Volume Data set created from a set of
   spatially-related frames within the ultrasound scanner,

   -  the Enhanced US Volume instance should include

      a. Referenced Image Sequence (0008,1140) to the source Ultrasound
         Image and/or Multi-frame Image instances

      b. Referenced Image Purpose of Reference Code Sequence (0040,A170)
         using (121346, DCM, "Acquisition frames corresponding to
         volume")

   -  and the Ultrasound Image and/or Multi-frame Image instances should
      include:

      a. Referenced Image Sequence (0008,1140) to the 3D Volume Data set

      b. Referenced Image Purpose of Reference Code Sequence (0040,A170)
         using (121347, DCM, "Volume corresponding to spatially-related
         acquisition frames")

2. In the case of an Ultrasound Image or Ultrasound Multi-frame Image
   instance containing one or more of the spatially-related frames
   derived from a 3D volume data, the ultrasound image instance should
   include:

   a. Source Image Sequence (0008,2112) referencing the Enhanced US
      Volume instance

   b. Source Image Sequence Purpose of Reference Code Sequence
      (0040,A170) using (121322, DCM, "Source of Image Processing
      Operation")

   c. Derivation Code Sequence (0008,9215) using (113091, DCM,
      "Spatially-related frames extracted from the volume")

3. In the case of separate MPR or 3D rendered views derived from a 3D
   Volume Data set, the image instance(s) should include:

   a. Source Image Sequence (0008,2112) referencing the Enhanced US
      Volume instance

   b. Source Image Sequence Purpose of Reference Code Sequence
      (0040,A170) using (121322, DCM, "Source of Image Processing
      Operation")

   c. Derivation Code Sequence (0008,9215) using code(s) describing the
      specific derivation operation(s)

.. _sect_PP.3.3:

Physiological Waveforms Associated With 3D Volume Data sets
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

ECG or other physiological waveforms associated with an Enhanced US
Volume (item 1d in the use case hierarchy) are to be conveyed via a one
or more companion instances of Waveform IODs linked bidirectionally to
the Enhanced US Volume instance. Physiological waveforms associated with
Ultrasound image acquisition may be represented using any of the
Waveform IODs, and are linked with the Enhanced US Volume instance and
to other simultaneous waveforms through the Referenced Instance Sequence
in the image instance and each waveform instance. The Synchronization
module and the Acquisition DateTime Attribute (0018,1800) are used to
synchronize the waveforms with the image and each other.

.. _sect_PP.3.4:

Workflow Considerations
~~~~~~~~~~~~~~~~~~~~~~~

The use case of two-step review (item 2a in the use case hierarchy) is
addressed by the use of separate SOP Classes for 2D and 3D data
representations. A review may initially be performed on the Ultrasound
Image and Ultrasound Multi-frame Image instances created during the
study. If additional operations on the 3D volume data are desired, the
Enhanced US Volume instance referenced in the Source Image Sequence of
the derived object may be individually retrieved and operated upon by an
appropriate application.

The 3D volume data spatially relates individual frames of the image to
each other using the Transducer Frame of Reference defined in (items 2b
in the use case hierarchy). This permits alignment of frames with each
other in the common situation where a hand-held ultrasound transducer is
used without an external frame of reference. However, the Transducer
Frame of Reference may in turn be related to an external Frame of
Reference through the Transducer Gantry Position and Transducer Gantry
Orientation Attributes. This would permit the creation of optional Image
Position and Orientation values relative to the Patient when this
information is available. In addition to these frames of reference, the
spatial registration, fiducials, segmentation, and deformation objects
available for other Enhanced objects may also be used with the Enhanced
US Volume instances.

The Key Object Selection Document SOP Class may be used to identify
specific Enhanced US Volume instances of particular interest (item 2d in
the use case hierarchy).

