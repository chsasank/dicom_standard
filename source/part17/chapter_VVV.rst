.. _chapter_VVV:

Segmentation of Images of Groups of Animals (Informative)
=========================================================

Imaging of small animals used for preclinical research may involve
acquiring images of multiple animals simultaneously (i.e., more than one
animal is present in the same image).

This Annex describes methods of cross-referencing image and other
composite SOP instances produced in the acquisition and segmentation
process and how the provenance of each may be recorded.

Only backward references are described, allowing for a sequential
workflow with processing performed by successive devices, without
modification of earlier instances.

.. _sect_VVV.1:

Use Case
--------

The relevant Attributes are described in and of the General Image
Module. The same principles apply if the General Image Module is not
used (e.g., for Enhanced Multi-frame Images, in which the same
Attributes are present, but nested in the appropriate Functional Group
Macros).

For the purpose of illustration, three successive steps are assumed:

1. acquisition of an image of several animals

2. processing of that image to detect (manually or automatically) the
   regions containing each animal, and storing the region as an
   appropriate composite instance

3. creation of derived images for each animal using as input the
   acquired image and the stored regions for each animal

Various DICOM composite objects could be used to encode the segmented
region. If the form of the segmented region is a

-  rasterized (bitmap), then the Segmentation Storage SOP Class is
   appropriate

   .. note::

      A bitmap overlay in a Grayscale or Color Softcopy Presentation
      State Storage SOP Class could also be used, though there are no
      defined semantics for this unintended use of bitmap overlays.

-  surface (mesh), then the Surface Storage SOP Class is appropriate

-  set of isocontours, then:

   -  for 3D patient-relative coordinates, the RT Structure Set Storage
      SOP Class is appropriate

   -  for 2D or 3D coordinates (and geometric shapes), a Structured
      Report Storage SOP Class may be appropriate, if a template with
      the appropriate semantics (what the contours "mean") is defined

   -  for 2D coordinates (and geometric shapes), a Grayscale or Color
      Softcopy Presentation State Storage SOP Class may be appropriate,
      though there are no defined semantics for recognizing what to do
      with which graphic objects

For illustrative purposes, the use of the Segmentation Storage SOP Class
is assumed, and a consistent Frame of Reference is assumed.

.. note::

   If images from different modalities are acquired, on separate
   devices, but with the same physical arrangement of animals, a more
   complex workflow might involve the use of one segmentation derived
   from one modality applied to images from a different modality with a
   different Frame of Reference, in which case use of the Spatial
   Registration Storage SOP Class or Deformable Spatial Registration
   Storage as persistent object might be appropriate, and appropriate
   references to it included. The same might apply if registration were
   necessary between images acquired on the same device, but given that
   research small animals are normally anesthetized, this is usually not
   required.

.. _sect_VVV.1.1:

Reference Attributes
~~~~~~~~~~~~~~~~~~~~

.. _sect_VVV.1.1.1:

Acquired Images of Multiple Animals
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

No references are present, since forward references are not used.

The Frame of Reference UID is present for cross-sectional modalities.

If the animals are not all aligned in the same direction, Patient
Position (0018,5100) for each animal is present within Group of Patients
Identification Sequence (0010,0027) and a nominal Patient Position
(0018,5100) is present in the General Series Module, and the coordinate
system dependent position and orientation Attributes of the Image Plane
Module Attributes (or corresponding Functional Groups) are relative to
the nominal Patient Position (0018,5100) present in the General Series
Module.

.. _sect_VVV.1.1.2:

Segmentation Instances
^^^^^^^^^^^^^^^^^^^^^^

Segmentations are Enhanced Multi-frame Images, so the Derivation Image
Functional Group () is used.

As required by the Segmentation IOD ():

-  the value of Purpose of Reference Sequence (0040,A170) within the
   Source Image Sequence (0008,2112) within Derivation Image Sequence
   (0008,9124) is (121322, DCM, "Source Image for Image Processing
   Operation")

-  the value of Derivation Code Sequence (0008,9215) within Derivation
   Image Sequence (0008,9124) is (113076, DCM, "Segmentation")

-  though not required, the value of Derivation Description (0008, 2111)
   may contain additional detail describing the image processing
   operation

The Frame of Reference UID is the same as that for the images from which
the segmentation was derived.

There is no requirement that application of the Segmentation be
restricted to the image referenced in the Derivation Image Functional
Group Macro, which describes the images that the segmentation was
derived from, not the images to which it is applicable (potentially all
of the images in the same Frame of Reference).

The Common Instance Reference Module is required to be present, which
provides Study and Series Instance UIDs for all referenced instances.

A segmentation instance may contain multiple segments, thus multiple
animals could be described in a single segmentation instance, or each
animal could be described in one of multiple segments within a single
segmentation instance. The manner in which each segment is numbered,
labeled and categorized is thus important. Each segment may be described
as follows:

-  Segment Number (0062,0004) from 1 to the number of animals (since the
   Attribute definition requires starting at 1, incrementing by 1)

-  Segment Label (0062,0005) using a human-readable label that
   appropriately identifies each animal in the context of the
   experiment, e.g., it may have the same value as the Patient ID
   (0010,0020) used for each separate animal.

-  Segmented Property Category Code Sequence (0062,0003) value of
   `(309825002, SCT, "Spatial and Relational
   Concept") <http://snomed.info/id/309825002>`__

-  Segmented Property Type Code Sequence (0062,000F) value of (113132,
   DCM, "Single subject selected from group")

.. note::

   The properties of `(309825002, SCT, "Spatial and Relational
   Concept") <http://snomed.info/id/309825002>`__ and (113132, DCM,
   "Single subject selected from group") are suggested instead of a more
   generic description, such as `(123037004, SCT, "Anatomical
   Structure") <http://snomed.info/id/123037004>`__ and `(38266002, SCT,
   "Entire Body") <http://snomed.info/id/38266002>`__, since though the
   latter would be accurate, it would not convey the additional
   implication of selection of one from many. Further, in some cases,
   the entire body may not actually be imaged (e.g., just the head of
   multiple subjects may be imaged simultaneously for brain studies).

.. _sect_VVV.1.1.3:

Derived Images of Single Animals
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

It is recommended that the source image(s) be referenced using Source
Image Sequence (0008,2112), either in the top level Data Set or within
the Derivation Image Functional Group () as appropriate for the IOD,
with:

-  the value of Purpose of Reference Sequence (0040,A170) within the
   Source Image Sequence (0008,2112) being (113130, DCM, "Predecessor
   containing group of imaging subjects")

-  the value of Derivation Code Sequence (0008,9215) being (113131, DCM,
   "Extraction of individual subject from group")

-  the value of Derivation Description (0008,2111) containing additional
   detail describing the image processing operation

It is recommended that the segmentation used be referenced using
Referenced Image Sequence (0008,1140), either in the top level Data Set
or within the Referenced Image Functional Group () as appropriate for
the IOD, with:

-  the value of Purpose of Reference Sequence (0040,A170) within
   Referenced Image Sequence (0008,1140) being (121321, DCM, "Mask image
   for image processing operation")

.. note::

   If instead of a segmentation (which is a form of image), a non-image
   object were used to encode the segmented regions, then use of
   Referenced Instance Sequence (0008,114A) instead of Referenced Image
   Sequence (0008,1140) would be appropriate.

The Frame of Reference UID is the same as the source images and the
segmentation.

If all the animals are not aligned in the same direction (i.e., do not
have the same value for Patient Position (0018,5100)), the coordinate
system dependent position and orientation Attributes of the Image Plane
Module Attributes (or corresponding Functional Groups) may have been
recomputed. If the animals are aligned in different directions, and
Patient Position (0018,5100) from within Group of Patients
Identification Sequence (0010,0027) in the source images is compared
against Patient Position (0018,5100) from the General Series Module in
the source images, the difference may be used to recompute (rotate, flip
and translate) new patient-relative vectors and offsets within the same
Frame of Reference. The value in the Patient Position (0018,5100) from
the General Series Module in the derived images are appropriate for the
selected animal.

It is recommended that the Common Instance Reference Module be present
even if it is not required by the IOD, to provide Study and Series
Instance UIDs for all referenced instances.

.. _sect_VVV.1.2:

Propagation of Composite Context
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Propagation and replacement of the appropriate patient-level and
study-level identifying and descriptive Attributes is also required.

The issues related to the identification of the "patient" in such cases
are addressed in .

New studies are required if the patient identifiers have changed.

New series are required for each of the derived (types) of objects,
since they are created by different equipment and have different values
for Modality.

.. _sect_VVV.1.3:

Propagation of History
~~~~~~~~~~~~~~~~~~~~~~

The history of operations applied to a composite instance and its
predecessors may be recorded in multiple items of Derivation Code
Sequence (0008,9215). It is preferable, when creating a new derived
object, to add to the end of the existing sequence of items, rather than
to completely replace them. It is also common to add to the plain text
that is contained in Derivation Description (0008, 2111), rather than
replacing it (maximum length permitting).

The history of which devices (and human operators) have operated on a
composite instance and its predecessors may be recorded in Contributing
Equipment Sequence (0018,A001). Again, it is preferable that the
existing sequence of items be extended rather than replaced, if
possible.

For both Derivation Code Sequence (0008,9215) and Contributing Equipment
Sequence (0018,A001), if multiple predecessors are applicable (e.g., the
source image and a segmentation mask), then the sequence of items of
both predecessors may be merged.

