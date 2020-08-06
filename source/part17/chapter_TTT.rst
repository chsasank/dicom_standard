.. _chapter_TTT:

X-Ray 3D Angiographic Image Encoding Examples (Informative)
===========================================================

.. _sect_TTT.1:

General Concepts of X-Ray 3D Angiography
----------------------------------------

This chapter describes the general concepts of the X-Ray 3D Angiography:
the acquisition of the projection images, the 3D reconstruction, and the
encoding of the X-Ray 3D Angiographic Image SOP instances. They provide
better understanding of the different application cases in the rest of
this Annex.

.. _sect_TTT.1.1:

Process of Creating An X-Ray 3D Angiography
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Two main steps are involved in the process of creating an X-Ray 3D
Angiographic Instance: The acquisition of 2D projections and the 3D
reconstruction of the volume.

.. _sect_TTT.1.1.1:

Acquisition of 2D Projections
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The X-Ray equipment acquires 2D projections at different angles. The
Acquisition Context describes the technical parameters of a set of 2D
projection acquisitions that are used to perform a 3D reconstruction. In
the scope of the X-Ray 3D Angiographic SOP Class, all the projections of
an Acquisition Context share common parameter values, such as:

-  Detector settings, anti-scatter grid, field of view characteristics

-  Distances from the X-Ray source to the Isocenter and to the detector,
   table position and table angles

-  Focal spot, spectral filters

-  Contrast injection details

If one value of such common parameters changes during the acquisition of
the projections, then more than one Acquisition Context will be defined.

Typically the projections of an Acquisition Context are the result of a
rotational acquisition where the X-Ray positioner follows a circular
trajectory. However, it is possible to define an Acquisition Context as
the set of multiple projections at different X-Ray incidences without a
particular spatial trajectory.

An Acquisition Context is characterized by a period of time in which all
the projections are acquired. Some other parameters are used to describe
the Acquisition Context: start and end DateTime, average exposure
techniques (mA, kVp, exposure duration, etc.), positioner start, end and
increment angles.

Additionally, other technical parameters that change at each projection
can be documented in the X-Ray 3D Angiographic SOP Class on a
per-projection basis:

-  kVp, mA, exposure duration

-  Collimator shape and dimensions

-  X-Ray positioner angles

.. _sect_TTT.1.1.2:

3D Reconstruction
^^^^^^^^^^^^^^^^^

The 3D Reconstruction Application performing the 3D Reconstruction can
be located in the same X-Ray equipment or in another workstation.

A 3D Reconstruction in the scope of the X-Ray 3D Angiographic SOP Class
is the creation of one X-Ray 3D Angiographic volume from a set of
projections from one or more Acquisition Context(s). Therefore, one 3D
Reconstruction in this scope refers to the resulting volume, and not to
the application logic to process the projections. This application logic
is out of the scope of this SOP Class, the same encoding will result
whether several 3D Reconstructions are performed in a single or in
multiple application steps to create several volumes (e.g., low and high
resolution volumes) from the same set of projections.

One 3D Reconstruction is characterized by some parameters like name,
version, manufacturer, description and the type of algorithm used to
process the projections.

The 3D Reconstruction can use one or more Acquisition Contexts to
generate one single X-Ray 3D Angiographic Volume. Several 3D
Reconstructions can be encoded in one single X-Ray 3D Angiographic
Instance.

.. _sect_TTT.1.2:

X-Ray 3D Angiographic Real World Entities Relationships
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This section describes the relationships between the real world entities
involved in X-Ray 3D Angiography.

The X-Ray equipment creates one or more acquisition contexts (i.e., one
or more rotational acquisitions with different technical parameters).
The projections can be kept internal to the equipment (i.e., not
exported outside the equipment) or can be encoded as DICOM instances. In
the scope of the X-Ray 3D Angiographic SOP Class, the projections can be
encoded either as X-Ray Angiography SOP Class or Enhanced XA SOP Class.

If the projections are encoded as DICOM Instances, they can be
referenced in the X-Ray 3D Angiographic image as Contributing Sources.
Each Acquisition Context refers to all the DICOM instances involved in
that context. If the projections are kept internal to the equipment, the
X-Ray 3D Angiographic image can still describe the technical parameters
of each acquisition context without referencing any DICOM instance.

The 3D Reconstruction Application creates one or more 3D
Reconstructions, each 3D Reconstruction uses one or more Acquisition
Contexts. One or more 3D Reconstructions can be encoded in one single
X-Ray 3D Angiographic Instance.

.. _sect_TTT.1.3:

X-Ray 3D Angiographic Pixel Data Characterization
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Similarly to other 3D modalities like CT or MR, the X-Ray 3D
Angiographic image is generated from original source data (i.e.,
original projections) which can be kept internal to the equipment. In
this sense, the 3D data resulting from the reconstruction of the
original projections is considered as original (i.e., the Value 1 of the
Attributes Image Type (0008,0008) and Frame Type (0008,9007) equals
ORIGINAL).

Note that the original 2D projections can be stored as DICOM instances,
and the X-Ray 3D Angiographic image can be created from a later
reconstruction on a different equipment. In this case, since the source
data is the same original set of projections, the 3D data is still
considered as original.

.. _sect_TTT.2:

Application Cases
-----------------

This chapter describes different scenarios and application cases where
the 3D volume is reconstructed from rotational angiography. Each
application case is structured in four sections:

1. **User Scenario**: Describes the user needs in a specific clinical
   context, and/or a particular system configuration and equipment type.

2. **Encoding Outline**: Describes the X-Ray 3D Angiographic Image SOP
   Class related to this scenario, and highlights key aspects.

3. **Encoding Details**: Provides detailed recommendations of the key
   Attributes of the Image IOD(s) to address this particular scenario.
   The tables are similar to the IOD tables of the . Only Attributes
   with a specific recommendation in this particular scenario have been
   included.

4. **Example**: Presents a typical example of the scenario, with
   realistic sample values, and gives details of the encoding of the key
   Attributes of the Image IOD(s) to address this particular scenario.
   In the values of the Attributes, the text in bold face indicates
   specific Attribute values; the text in italic face gives an
   indication of the expected value content.

The first application case describes the most general reconstruction
scenario, and can be considered as a baseline. The further application
cases only describe the specificities of the new scenario vs. the
baseline.

.. _sect_TTT.2.1:

Case #1: One Rotation, One 2D Instance, One Reconstruction, One X-Ray 3D Instance
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This application case is related to the most general reconstruction of a
3D volume directly from all the frames of a rotational 2D projection
acquisition.

.. _sect_TTT.2.1.1:

User Scenario
^^^^^^^^^^^^^

The image acquisition system performs a rotational acquisition around
the patient and a volume is reconstructed from the acquired data (e.g.,
through "back-projection" algorithm). The reconstruction can either
occur on the same system (e.g., Acquisition Modality) or a secondary
processing system (e.g., Co-Workstation).

The reconstructed Volume needs to be encoded and kept saved for
interchange with 3D rendering application or further equipment involved
during an interventional procedure.

.. _sect_TTT.2.1.2:

Encoding Outline
^^^^^^^^^^^^^^^^

This is the basic use case of X-Ray 3D Angiographic image encoding.

The rotational acquisition can be encoded either as a multifamily XA
Image with limited frame-specific Attributes or as an Enhanced XA Image,
with frame-specific Attributes encoded that support the algorithms to
reconstruct volume data.

The volume data is encoded as an X-Ray 3D Angiographic instance. The
volume data typically spans the complete region of the projected matrix
size (in number of rows and columns).

All the projections of the original XA instance or Enhanced XA instance
are used to reconstruct the volume.

The X-Ray 3D Angiographic instance references the original XA instance
or Enhanced XA instance and uses Attributes to define the context on how
the original 2D image frames are used to create the volume.

.. _sect_TTT.2.1.3:

Encoding Details
^^^^^^^^^^^^^^^^

.. _sect_TTT.2.1.3.1:

X-Ray 3D Angiographic Image IOD
'''''''''''''''''''''''''''''''

.. _sect_TTT.2.1.3.1.1:

General and Enhanced Series Modules Recommendations
                                                   

These modules encode the Series relationship of the created volume.

.. table:: General and Enhanced Series Modules Recommendations

   +--------------------------+-------------+--------------------------+
   | Attribute Name           | Tag         | Recommendation           |
   +==========================+=============+==========================+
   | Series Instance UID      | (0020,000E) | Use a different Series   |
   |                          |             | than the original        |
   |                          |             | projections.             |
   +--------------------------+-------------+--------------------------+
   | Series Description       | (0008,103E) | Free text to describe    |
   |                          |             | the volume content,      |
   |                          |             | different from the       |
   |                          |             | description of the       |
   |                          |             | series of the projection |
   |                          |             | images.                  |
   +--------------------------+-------------+--------------------------+
   | Protocol Name            | (0018,1030) | Free text to describe    |
   |                          |             | technical aspects of the |
   |                          |             | reconstruction (focusing |
   |                          |             | on imaging protocol      |
   |                          |             | rather than clinical     |
   |                          |             | protocol). May be        |
   |                          |             | relevant for grouping,   |
   |                          |             | sorting or finding of    |
   |                          |             | the X-Ray 3D volume.     |
   +--------------------------+-------------+--------------------------+
   | Referenced Performed     | (0008,1111) | Reference to the image   |
   | Procedure Step Sequence  |             | acquisition procedure.   |
   |                          |             | May also reference a     |
   |                          |             | dedicated processing     |
   |                          |             | procedure step (e.g.,    |
   |                          |             | UPS).                    |
   +--------------------------+-------------+--------------------------+

.. _sect_TTT.2.1.3.1.2:

Frame of Reference Module Recommendations
                                         

This module encodes the identifier for the spatial relationship base of
this volume. If the originating 2D images do not deliver a value, it has
to be created for the reconstructed volume.

.. table:: Frame of Reference Module Recommendations

   +--------------------------+-------------+--------------------------+
   | Attribute Name           | Tag         | Recommendation           |
   +==========================+=============+==========================+
   | Frame of Reference UID   | (0020,0052) | Volumes with identical   |
   |                          |             | FoR UID share the same   |
   |                          |             | spatial relationship.    |
   |                          |             | Copy the FoR UID if the  |
   |                          |             | originating image is     |
   |                          |             | encoded as an Enhanced   |
   |                          |             | XA Image.                |
   +--------------------------+-------------+--------------------------+
   | Position Reference       | (0020,1040) | If the system is capable |
   | Indicator                |             | to derive such           |
   |                          |             | information from the     |
   |                          |             | anatomy-related          |
   |                          |             | information in the       |
   |                          |             | projection X-Ray image   |
   |                          |             | data, otherwise no       |
   |                          |             | recommendation to set a  |
   |                          |             | value.                   |
   +--------------------------+-------------+--------------------------+

.. _sect_TTT.2.1.3.1.3:

General and Enhanced General Equipment Modules Recommendations
                                                              

This module encodes the equipment identification information of the
system that reconstructed the volume data. Since the reconstruction is
not necessarily performed by the same system that acquired the
projections, the identification of the Equipment performing the
reconstruction is recommended. Furthermore the Contributing Equipment
Sequence (0018,A001) of the is recommended to be used to preserve the
identification of the system that created the projection image that was
base for the reconstruction.

.. _sect_TTT.2.1.3.1.4:

Image Pixel Module Recommendations
                                  

This module encodes the actual pixels of the volume slices. Each slice
is encoded as one frame of the X-Ray 3D Angiographic instance. The order
of the frames encoded in the pixel data is aligned with the Image
Position (Patient) Attribute. The order of frames is optimal for simple
2D viewing if the x-,y-,z-values steadily increase or decrease.

.. _sect_TTT.2.1.3.1.5:

Enhanced Contrast/Bolus Module Recommendations
                                              

This module encodes the contrast media applied. The minimum information
that needs to be provided is related to the contrast agent and the
administration route. In the reconstructed image, the contrast
information comes either from the acquisition system in case of direct
reconstruction without source DICOM instances, or from the projection
images in case of reconstruction from source DICOM instances.

.. table:: Enhanced Contrast/Bolus Module Recommendations

   +--------------------------+-------------+--------------------------+
   | Attribute Name           | Tag         | Recommendation           |
   +==========================+=============+==========================+
   | Contrast/Bolus Agent     | (0018,0012) |                          |
   | Sequence                 |             |                          |
   +--------------------------+-------------+--------------------------+
   | *>Include Baseline .*    |             | See `Differences between |
   |                          |             | XA and Enhanced          |
   |                          |             | XA <#                    |
   |                          |             | sect_TTT.2.1.3.1.5.1>`__ |
   +--------------------------+-------------+--------------------------+
   | >Contrast/Bolus          | (0018,0014) |                          |
   | Administration Route     |             |                          |
   | Sequence                 |             |                          |
   +--------------------------+-------------+--------------------------+
   | *>>Include Baseline .*   |             | See `Differences between |
   |                          |             | XA and Enhanced          |
   |                          |             | XA <#s                   |
   |                          |             | ect_TTT.2.1.3.1.5.1>`__. |
   +--------------------------+-------------+--------------------------+

.. _sect_TTT.2.1.3.1.5.1:

Differences between XA and Enhanced XA
                                      

If the source instance is encoded as an Enhanced XA instance, the
Enhanced Contrast/Bolus Module is specified in that IOD, then those
values are copied from the source instance.

If the source instance is encoded as an XA Image, only the
Contrast/Bolus Module is specified in that IOD. Although acquisition
devices are encouraged to provide details of the contrast, most of the
relevant Attributes are type 3, so it is possible that if contrast was
applied, the only indication will be the presence of Contrast/Bolus
Agent (0018,0010) since that Attribute is type 2. In that case, if the
application is unable to get more specific information from the
operator, it may populate the contrast details with the generic
`(7140000, SCT, "Contrast agent") <http://snomed.info/id/7140000>`__
code for contrast agent and the `(261665006, SCT,
"Unknown") <http://snomed.info/id/261665006>`__ code for the
administration route.

.. _sect_TTT.2.1.3.1.6:

Multi-frame Dimensions Module Recommendations
                                             

This module encodes a (default) presentation order of the image frames.

.. table:: Multi-frame Dimensions Module Recommendations

   +--------------------------+-------------+--------------------------+
   | Attribute Name           | Tag         | Recommendation           |
   +==========================+=============+==========================+
   | Dimension Organization   | (0020,9221) | This will be an initial  |
   | Sequence                 |             | single dimension and     |
   |                          |             | therefore a single       |
   |                          |             | Dimension UID is         |
   |                          |             | sufficient.              |
   +--------------------------+-------------+--------------------------+
   | Dimension Organization   | (0020,9311) | The value will be "3D".  |
   | Type                     |             |                          |
   +--------------------------+-------------+--------------------------+
   | Dimension Index Sequence | (0020,9222) | Specifies a Dimension    |
   |                          |             | Index that refers to the |
   |                          |             | Image Position (Patient) |
   |                          |             | as dimension for frame   |
   |                          |             | order during 2D          |
   |                          |             | presentation of an X-Ray |
   |                          |             | 3D volume.               |
   +--------------------------+-------------+--------------------------+

.. _sect_TTT.2.1.3.1.7:

Patient Orientation Module Recommendations
                                          

This module encodes the orientation of the Patient for later use with
same or other equipment. The related coded terms can be derived from the
Patient Position (0018,5100) according to the following table, where:

-  PO denotes the Patient Orientation Code Sequence (0054,0410);

-  POM denotes the Patient Orientation Modifier Code Sequence
   (0054,0412);

-  PGR denotes the Patient Gantry Relationship Code Sequence
   (0054,0414).

.. table:: Patient Position to Orientation Conversion Recommendations

   +------------------+--------------------------------------------------+
   | Patient Position | Patient Orientation Coding                       |
   +==================+==================================================+
   | HFS              | PO: `(102538003, SCT,                            |
   |                  | "                                                |
   |                  | recumbent") <http://snomed.info/id/102538003>`__ |
   |                  |                                                  |
   |                  | POM: `(40199007, SCT,                            |
   |                  | "supine") <http://snomed.info/id/40199007>`__    |
   |                  |                                                  |
   |                  | PGR: `(102540008, SCT,                           |
   |                  | "                                                |
   |                  | headfirst") <http://snomed.info/id/102540008>`__ |
   +------------------+--------------------------------------------------+
   | HFP              | PO: `(102538003, SCT,                            |
   |                  | "                                                |
   |                  | recumbent") <http://snomed.info/id/102538003>`__ |
   |                  |                                                  |
   |                  | POM: `(1240000, SCT,                             |
   |                  | "prone") <http://snomed.info/id/1240000>`__      |
   |                  |                                                  |
   |                  | PGR: `(102540008, SCT,                           |
   |                  | "                                                |
   |                  | headfirst") <http://snomed.info/id/102540008>`__ |
   +------------------+--------------------------------------------------+
   | FFS              | PO: `(102538003, SCT,                            |
   |                  | "                                                |
   |                  | recumbent") <http://snomed.info/id/102538003>`__ |
   |                  |                                                  |
   |                  | POM: `(40199007, SCT,                            |
   |                  | "supine") <http://snomed.info/id/40199007>`__    |
   |                  |                                                  |
   |                  | PGR: `(102541007, SCT,                           |
   |                  | "f                                               |
   |                  | eet-first") <http://snomed.info/id/102541007>`__ |
   +------------------+--------------------------------------------------+
   | FFP              | PO: `(102538003, SCT,                            |
   |                  | "                                                |
   |                  | recumbent") <http://snomed.info/id/102538003>`__ |
   |                  |                                                  |
   |                  | POM: `(1240000, SCT,                             |
   |                  | "prone") <http://snomed.info/id/1240000>`__      |
   |                  |                                                  |
   |                  | PGR: `(102541007, SCT,                           |
   |                  | "f                                               |
   |                  | eet-first") <http://snomed.info/id/102541007>`__ |
   +------------------+--------------------------------------------------+
   | HFDR             | PO: `(102538003, SCT,                            |
   |                  | "                                                |
   |                  | recumbent") <http://snomed.info/id/102538003>`__ |
   |                  |                                                  |
   |                  | POM: `(102535000, SCT, "right lateral            |
   |                  | decubitus") <http://snomed.info/id/102535000>`__ |
   |                  |                                                  |
   |                  | PGR: `(102540008, SCT,                           |
   |                  | "                                                |
   |                  | headfirst") <http://snomed.info/id/102540008>`__ |
   +------------------+--------------------------------------------------+
   | HFDL             | PO: `(102538003, SCT,                            |
   |                  | "                                                |
   |                  | recumbent") <http://snomed.info/id/102538003>`__ |
   |                  |                                                  |
   |                  | POM: `(102536004, SCT, "left lateral             |
   |                  | decubitus") <http://snomed.info/id/102536004>`__ |
   |                  |                                                  |
   |                  | PGR: `(102540008, SCT,                           |
   |                  | "                                                |
   |                  | headfirst") <http://snomed.info/id/102540008>`__ |
   +------------------+--------------------------------------------------+
   | FFDR             | PO: `(102538003, SCT,                            |
   |                  | "                                                |
   |                  | recumbent") <http://snomed.info/id/102538003>`__ |
   |                  |                                                  |
   |                  | POM: `(102535000, SCT, "right lateral            |
   |                  | decubitus") <http://snomed.info/id/102535000>`__ |
   |                  |                                                  |
   |                  | PGR: `(102541007, SCT,                           |
   |                  | "f                                               |
   |                  | eet-first") <http://snomed.info/id/102541007>`__ |
   +------------------+--------------------------------------------------+
   | FFDL             | PO: `(102538003, SCT,                            |
   |                  | "                                                |
   |                  | recumbent") <http://snomed.info/id/102538003>`__ |
   |                  |                                                  |
   |                  | POM: `(102536004, SCT, "left lateral             |
   |                  | decubitus") <http://snomed.info/id/102536004>`__ |
   |                  |                                                  |
   |                  | PGR: `(102541007, SCT,                           |
   |                  | "f                                               |
   |                  | eet-first") <http://snomed.info/id/102541007>`__ |
   +------------------+--------------------------------------------------+

.. _sect_TTT.2.1.3.1.8:

X-Ray 3D Image Module Recommendations
                                     

This module encodes the specific content of the reconstructed volume.

.. table:: X-Ray 3D Image Module Recommendations

   +---------------------+-------------+--------------------------------+
   | Attribute Name      | Tag         | Recommendation                 |
   +=====================+=============+================================+
   | Image Type          | (0008,0008) | Use "ORIGINAL" value 1 (Pixel  |
   |                     |             | Data Characteristics) to       |
   |                     |             | indicate a reconstruction from |
   |                     |             | original projections.          |
   |                     |             |                                |
   |                     |             | Use "VOLUME" in value 3 (Image |
   |                     |             | Flavor) to indicate regularly  |
   |                     |             | sampled.                       |
   +---------------------+-------------+--------------------------------+
   | Icon Image Sequence | (0088,0200) | Include if the reconstruction  |
   |                     |             | application may be able to     |
   |                     |             | generate a rendered            |
   |                     |             | representative icon image.     |
   +---------------------+-------------+--------------------------------+

.. _sect_TTT.2.1.3.1.9:

X-Ray 3D Angiographic Image Contributing Sources Module Recommendations
                                                                       

This module encodes the source SOP instances used to create the X-Ray 3D
Angiographic instance.

.. table:: X-Ray 3D Angiographic Image Contributing Sources Module
Recommendations

   +--------------------------+-------------+--------------------------+
   | Attribute Name           | Tag         | Recommendation           |
   +==========================+=============+==========================+
   | Contributing Sources     | (0018,9506) | One item since there is  |
   | Sequence                 |             | only one originating     |
   |                          |             | image that contributed   |
   |                          |             | to the creation of the   |
   |                          |             | X-Ray 3D Angiographic    |
   |                          |             | image.                   |
   +--------------------------+-------------+--------------------------+

.. _sect_TTT.2.1.3.1.10:

X-Ray 3D Angiographic Acquisition Module Recommendations
                                                        

This module encodes the important technical and physical parameters of
the source SOP instances used to create the X-Ray 3D Angiographic Image
instance.

The contents of the Enhanced XA Image IOD and XA Image IOD are
significantly different. Therefore the contents of the X-Ray 3D
Acquisition Sequence will vary depending on availability of encoded data
in the source instance.

The content of the X-Ray 3D General Positioner Movement Macro provides a
general overview on the Positioner data. In case a system does not
support the Isocenter Reference System, it may still be of advantage to
provide the patient-based Positioner Primary and Secondary Angles in the
Per Projection Acquisition Sequence (0018,9538).

The contents of the Per Projection Acquisition Sequence (0018,9538) need
to be carefully aligned with the list of frame numbers in the Referenced
Frame Numbers (0008,1160) Attribute in the Source Image Sequence
(0008,2112).

.. table:: X-Ray 3D Angiographic Acquisition Module Recommendations

   +--------------------------+-------------+--------------------------+
   | Attribute Name           | Tag         | Recommendation           |
   +==========================+=============+==========================+
   | X-Ray 3D Acquisition     | (0018,9507) | One item since there is  |
   | Sequence                 |             | only one acquisition     |
   |                          |             | context that contributed |
   |                          |             | to the reconstruction of |
   |                          |             | the X-Ray 3D             |
   |                          |             | Angiographic image pixel |
   |                          |             | data contents.           |
   +--------------------------+-------------+--------------------------+

.. _sect_TTT.2.1.3.1.11:

Pixel Measures Macro Recommendations
                                    

This module encodes the detailed size of the volume element (Pixel
Spacing for row/column dimension of each slice, and Slice Thickness for
the distance between slices). It depends on the reconstruction algorithm
and is not necessarily identical to the related sizes in the projection
images.

For a single volume this macro is encoded "shared" as all the slices
will have the same Pixel Spacing and Slice Thickness.

.. _sect_TTT.2.1.3.1.12:

Frame Content Macro Recommendations
                                   

This module encodes the timing information of the frames, as well as
dimension and stack index values.

In the reconstruction from rotational projections the figure C.7.6.16-2
of should be interpreted carefully. All the frames forming one X-Ray 3D
Angiographic volume have been reconstructed simultaneously, therefore
all of them have a same time reference and the same acquisition
duration.

The projections have been acquired over a period of time, all of them
contributing to each 3D frame. Therefore, it's recommended to encode the
3D frame acquisition duration as the elapsed time from the first to the
last projection frame time that contributed to that volume.

.. table:: Frame Content Macro Recommendations

   +--------------------------+-------------+--------------------------+
   | Attribute Name           | Tag         | Recommendation           |
   +==========================+=============+==========================+
   | Frame Content Sequence   | (0020,9111) | Provides details for     |
   |                          |             | each frame. The Date and |
   |                          |             | Time Attributes are      |
   |                          |             | identical for all frames |
   |                          |             | and are set to the       |
   |                          |             | date/time of the first   |
   |                          |             | projection frame due to  |
   |                          |             | the nature of the volume |
   |                          |             | creation. The Stack      |
   |                          |             | information can be used  |
   |                          |             | to group frames into     |
   |                          |             | sub-volumes, if needed.  |
   +--------------------------+-------------+--------------------------+
   | >Frame Reference         | (0018,9151) | Use the date and time of |
   | DateTime                 |             | the first 2D frame used  |
   |                          |             | for the reconstruction   |
   |                          |             | of this 3D frame. Same   |
   |                          |             | value for all the frames |
   |                          |             | of the same              |
   |                          |             | reconstruction.          |
   +--------------------------+-------------+--------------------------+
   | >Frame Acquisition       | (0018,9074) | Use the same value as    |
   | DateTime                 |             | the Frame Reference      |
   |                          |             | DateTime (0018,9151).    |
   +--------------------------+-------------+--------------------------+
   | >Frame Acquisition       | (0018,9220) | Use the duration of the  |
   | Duration                 |             | rotational acquisition.  |
   |                          |             | Same value for all the   |
   |                          |             | frames of the same       |
   |                          |             | reconstruction.          |
   +--------------------------+-------------+--------------------------+
   | >Dimension Index Values  | (0020,9157) | From 1 to M or M to 1    |
   |                          |             | depending whether the    |
   |                          |             | frames are to be         |
   |                          |             | displayed in the storage |
   |                          |             | order or reverse, M      |
   |                          |             | being the number of      |
   |                          |             | frames of the            |
   |                          |             | reconstructed volume.    |
   +--------------------------+-------------+--------------------------+
   | >Stack ID                | (0020,9056) | Use the value "1" for    |
   |                          |             | all the frames, since    |
   |                          |             | they belong to the same  |
   |                          |             | reconstructed volume.    |
   +--------------------------+-------------+--------------------------+
   | >In-Stack Position       | (0020,9057) | From 1 to M, where M is  |
   | Number                   |             | the number of frames of  |
   |                          |             | the reconstructed        |
   |                          |             | volume.                  |
   +--------------------------+-------------+--------------------------+

.. _sect_TTT.2.1.3.1.13:

Derivation Image Macro Recommendations
                                      

The volume is directly reconstructed from the original set of
projections and therefore not "derived" in this sense. Thus this macro
is not applicable in this scenario as the contents of the Contributing
Sources Sequence (0018,9506) and the X-Ray 3D Acquisition Sequence
(0018,9507) are sufficient to describe the relationship to the
originating image.

.. _sect_TTT.2.1.3.1.14:

Frame Anatomy Macro Recommendations
                                   

This macro encodes the anatomical context. It can be important to
parameterize the presentation of the volumes. For a single volume this
macro is encoded "shared". Typically the anatomy of the volume is only
available if the information is already provided within the originating
projection image, either by detection algorithm or by user input.

.. _sect_TTT.2.1.3.1.15:

X-Ray 3D Frame Type Macro Recommendations
                                         

This macro encodes the general characteristics of the volume slices like
color information for presentation, volumetric properties for
geometrical manipulations etc. In case of a single volume, this macro is
encoded "shared" as each slice of the volume has identical
characteristics. If multiple volumes are encoded in a single instance,
this macro may be encoded "per frame".

.. _sect_TTT.2.1.4:

Example
^^^^^^^

.. _sect_TTT.2.1.4.1:

Reconstruction Using All Frames of An Enhanced XA Image
'''''''''''''''''''''''''''''''''''''''''''''''''''''''

This basic example is the reconstruction of a volume by a
back-projection from all frames of a rotational acquisition which have
been encoded as an Enhanced XA Instance. The rotational acquisition
takes 5 seconds to acquire all the projections.

.. note::

   The example would be very similar if the rotational acquisition was
   encoded as an XA Image.

The dimension organization is based on the spatial position of the 3D
frames. The frames are to be displayed in the same order as stored.

The UIDs of this example correspond to the diagram shown in
`figure_title <#figure_TTT.2.1-1>`__

.. _sect_TTT.2.2:

Case #2: Reconstruction From A Sub-set of Projection Frames
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This application case is related to a reconstruction from a sub-set of
projection frames.

.. _sect_TTT.2.2.1:

User Scenario
^^^^^^^^^^^^^

The image acquisition system performs one rotational acquisition. Not
all of the acquired frames, but every N\ :sup:`th` frame is used to
reconstruct the volume, e.g., to speed-up the reconstruction.

.. _sect_TTT.2.2.2:

Encoding Outline
^^^^^^^^^^^^^^^^

Only selected frames of the original XA instance or Enhanced XA instance
are used to reconstruct the volume.

The X-Ray 3D instance references the original XA instance or Enhanced XA
instance and uses Attributes to define the context on how and which of
the original image frames are used to create the volume.

.. _sect_TTT.2.2.3:

Encoding Details
^^^^^^^^^^^^^^^^

.. _sect_TTT.2.2.3.1:

X-Ray 3D Angiographic Image IOD
'''''''''''''''''''''''''''''''

.. _sect_TTT.2.2.3.1.1:

X-Ray 3D Angiographic Acquisition Module Recommendations
                                                        

This module encodes the important technical and physical parameters of
the source SOP instances and the frames used to create the X-Ray 3D
Angiographic instance.

.. table:: X-Ray 3D Angiographic Acquisition Module Recommendations

   +--------------------------+-------------+--------------------------+
   | Attribute Name           | Tag         | Recommendation           |
   +==========================+=============+==========================+
   | X-Ray 3D Acquisition     | (0018,9507) | One item since there is  |
   | Sequence                 |             | only one acquisition     |
   |                          |             | context that contributed |
   |                          |             | to the reconstruction of |
   |                          |             | the X-Ray 3D             |
   |                          |             | Angiographic image pixel |
   |                          |             | data contents.           |
   +--------------------------+-------------+--------------------------+
   | >Source Image Sequence   | (0008,2112) |                          |
   +--------------------------+-------------+--------------------------+
   | >>Referenced Frame       | (0008,1160) | Only include the frame   |
   | Number                   |             | numbers used for the     |
   |                          |             | reconstruction.          |
   +--------------------------+-------------+--------------------------+
   | >Per Projection          | (0018,9538) | The content of the X-Ray |
   | Acquisition Sequence     |             | 3D General Positioner    |
   |                          |             | Movement Macro only      |
   |                          |             | provides an overview of  |
   |                          |             | the Positioner data.     |
   |                          |             | When not all frames of   |
   |                          |             | the originating          |
   |                          |             | projection image are     |
   |                          |             | used, it is recommended  |
   |                          |             | to provide the           |
   |                          |             | patient-based Positioner |
   |                          |             | Primary and Secondary    |
   |                          |             | Angles in the Per        |
   |                          |             | Projection Acquisition   |
   |                          |             | Sequence (0018,9538).    |
   |                          |             |                          |
   |                          |             | The contents of the Per  |
   |                          |             | Projection Acquisition   |
   |                          |             | Sequence (0018,9538)     |
   |                          |             | need to be carefully     |
   |                          |             | aligned with the list of |
   |                          |             | frame numbers in the     |
   |                          |             | Referenced Frame Numbers |
   |                          |             | (0008,1160) Attribute in |
   |                          |             | the Source Image         |
   |                          |             | Sequence (0008,2112).    |
   +--------------------------+-------------+--------------------------+

.. _sect_TTT.2.2.3.1.2:

Frame Content Macro Recommendations
                                   

This module encodes the timing information of the frames, as well as
dimension and stack index values.

.. table:: Frame Content Macro Recommendations

   +--------------------------+-------------+--------------------------+
   | Attribute Name           | Tag         | Recommendation           |
   +==========================+=============+==========================+
   | Frame Content Sequence   | (0020,9111) | Provides details for     |
   |                          |             | each frame.              |
   +--------------------------+-------------+--------------------------+
   | >Frame Acquisition       | (0018,9220) | Use the elapsed time     |
   | Duration                 |             | from the first to the    |
   |                          |             | last projection frame    |
   |                          |             | time used for this       |
   |                          |             | reconstruction.          |
   +--------------------------+-------------+--------------------------+

.. _sect_TTT.2.2.4:

Example
^^^^^^^

This specific example is the reconstruction of a volume by a
back-projection from every 5\ :sup:`th` frame of a rotational
acquisition and encoded as an Enhanced XA Image.

.. note::

   The example would be very similar if the rotational acquisition was
   encoded as an XA Image.

.. _sect_TTT.2.3:

Case #3: Reconstruction From A Sub-region of All Image Frames
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This application case is related to a regular reconstruction of the full
field of view of a rotational acquisition followed by a specific
reconstruction of a sub-region that contains an object of interest
(e.g., interventional device implanted, stent, coils etc.).

.. _sect_TTT.2.3.1:

User Scenario
^^^^^^^^^^^^^

The image acquisition system performs one rotational acquisition after
the intervention, on the region of the patient where an implant has been
placed.

Two 3D volumes are reconstructed; one of the full field of view of the
projection images, another of a sub-region of each of the acquired
frames, e.g., to extract the object of interest into a smaller volume.
The second volume is likely performed at higher resolution and likely
applies different 3D reconstruction techniques, for instance to
highlight the material of the implant. The purpose is to overlap the two
volumes and enhance the visibility of the object of interest over the
full field volume.

.. _sect_TTT.2.3.2:

Encoding Outline
^^^^^^^^^^^^^^^^

The rotational acquisition can either be encoded as XA Image or as
Enhanced XA Image.

Each reconstruction is encoded in a different X-Ray 3D Angiographic
instance.

Not all parts of each frame of the original XA instance or Enhanced XA
instance are used to reconstruct the second volume.

The X-Ray 3D instance references the original XA instance or Enhanced XA
instance and uses Attributes to define the context on how and which part
of the original image frames are used to create the Volume.

.. _sect_TTT.2.3.3:

Encoding Details
^^^^^^^^^^^^^^^^

.. _sect_TTT.2.3.3.1:

X-Ray 3D Angiographic Image IOD
'''''''''''''''''''''''''''''''

.. _sect_TTT.2.3.3.1.1:

Frame of Reference Module Recommendations
                                         

Since the two volumes are reconstructed from the same projections, the
reconstruction application will use the same patient coordinate system
on both volumes so that the spatial location of the object of interest
in both volumes will be the same. Therefore the two X-Ray 3D Instances
will have the same Frame of Reference (FoR) UID. If the originating 2D
Instances do not deliver a value of FoR UID, a new FoR UID has to be
created for the reconstructed volumes.

.. table:: Frame of Reference Module Recommendations

   +------------------------+-------------+--------------------------+
   | Attribute Name         | Tag         | Recommendation           |
   +========================+=============+==========================+
   | Frame of Reference UID | (0020,0052) | Use the same value for   |
   |                        |             | the full field of view   |
   |                        |             | volume and the           |
   |                        |             | sub-region volume.       |
   +------------------------+-------------+--------------------------+

.. _sect_TTT.2.3.3.1.2:

Pixel Measures Macro Recommendations
                                    

The detailed size of the volume element (Pixel Spacing for x/y dimension
and Slice Thickness for z dimension) may be different between the full
field of view reconstruction and the sub-region reconstruction.

.. table:: Pixel Measures Macro Recommendations

   +-------------------------+-------------+--------------------------+
   | Attribute Name          | Tag         | Recommendation           |
   +=========================+=============+==========================+
   | Pixel Measures Sequence | (0028,9110) | The pixel sizes and/or   |
   |                         |             | slice thickness are not  |
   |                         |             | necessarily equal in the |
   |                         |             | two reconstructed        |
   |                         |             | volumes. Within each     |
   |                         |             | individual volume this   |
   |                         |             | sequence is encoded as   |
   |                         |             | "shared".                |
   +-------------------------+-------------+--------------------------+

.. _sect_TTT.2.3.3.1.3:

Plane Position (Patient) Macro Recommendations
                                              

The plane position of the first slice in the first volume may have a
different value than in the second volume, as the sub-region volume can
be smaller and shifted with respect to the full field of view volume.

.. _sect_TTT.2.3.3.1.4:

Plane Orientation (Patient) Macro Recommendations
                                                 

The plane orientation could be different in the second volume depending
on the application needs, e.g., to align the slices with the object of
interest.

.. _sect_TTT.2.3.3.1.5:

Frame Content Macro Recommendations
                                   

This module encodes the timing information of the frames, as well as
dimension and stack index values.

.. table:: Frame Content Macro Recommendations

   +--------------------------+-------------+--------------------------+
   | Attribute Name           | Tag         | Recommendation           |
   +==========================+=============+==========================+
   | Frame Content Sequence   | (0020,9111) | Provides details for     |
   |                          |             | each frame.              |
   +--------------------------+-------------+--------------------------+
   | >Frame Acquisition       | (0018,9220) | Use the duration of the  |
   | Duration                 |             | rotational acquisition   |
   |                          |             | in the two reconstructed |
   |                          |             | volumes.                 |
   +--------------------------+-------------+--------------------------+

.. _sect_TTT.2.3.3.1.6:

Frame Anatomy Macro Recommendations
                                   

The volume directly reconstructed from a sub-region of each of the
original projection X-Ray frames does not necessarily reflect the same
anatomy or laterality as the full field of view volume. Therefore the
Frame Anatomy macro may point to a different anatomic context than the
one documented for the originating frames.

.. _sect_TTT.2.3.4:

Example
^^^^^^^

In this example, the slices of the two volumes are reconstructed in the
axial plane of the patient; the row direction is aligned in the positive
x-direction of the patient (right-left) and the column direction is
aligned in the positive y-direction of the patient (anterior-posterior).

The full field of view reconstruction in encoded with the Instance UID
"Z1" and consists of a 512 cube volume of 0.2 mm of voxel size. The
sub-region reconstruction in encoded with the Instance UID "Z2" and
consists of a 256 cube volume of the voxel size of 0.1 mm.

Both volumes share the same Frame of Reference UID.

.. _sect_TTT.2.4:

Case #4: Multiple Rotations, One Or More 2D Instances, One Reconstruction, One X-Ray 3D Instance
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This application case is related to a high resolution reconstruction
from several rotations around the same anatomy.

.. _sect_TTT.2.4.1:

User Scenario
^^^^^^^^^^^^^

The image acquisition system performs multiple 2D rotational
acquisitions around the patient with movements in the same or opposite
directions in the patient's transverse plane. A single volume is
reconstructed from the acquired data (e.g., through "back-projection"
algorithm). The reconstruction can either occur on the same system
(e.g., Acquisition Modality) or a secondary processing system (e.g.,
Co-Workstation).

The reconstructed Volume needs to be encoded and saved for further use.

.. _sect_TTT.2.4.2:

Encoding Outline
^^^^^^^^^^^^^^^^

The rotational acquisitions can be encoded either as a single instance
(e.g., "C") containing several rotations or as several instances (e.g.,
"C1", "C2", etc.) containing one rotation per instance. The rotational
acquisitions can either be encoded as XA Image(s) with limited
frame-specific Attributes or as Enhanced XA Image(s), with
frame-specific Attributes encoded that inform the algorithms to
reconstruct a volume.

The reconstructed volume data is encoded as a single X-Ray 3D
Angiographic instance. The reconstructed region covers typically the
full field of view of the projected matrix size.

All frames of the original XA Images or Enhanced XA Images are used to
reconstruct the volume.

The X-Ray 3D instance references the original acquisition instances and
records Attributes of the projections describing the acquisition
context.

.. _sect_TTT.2.4.3:

Encoding Details
^^^^^^^^^^^^^^^^

.. _sect_TTT.2.4.3.1:

2D X-Ray Angiographic Image IOD
'''''''''''''''''''''''''''''''

This scenario is based on the encoding of the different rotations in one
or more 2D instance(s), which can be encoded either as X-Ray Angiography
or Enhanced XA Images.

.. _sect_TTT.2.4.3.1.1:

Frame of Reference Module Recommendations
                                         

In the case of multiple source 2D Instances, the acquisition equipment
assumes that the patient has not moved between the different rotations.
This module encodes the same FoR UID in all the rotations, identifying a
common spatial relationship between them, thus allowing the 3D
reconstruction to use the projections of all the rotations to perform a
single volume reconstruction.

If the source 2D Instances do not provide a value of FoR UID, it has to
be created for the reconstructed volume.

.. table:: Frame of Reference Module Recommendations

   +--------------------------+-------------+--------------------------+
   | Attribute Name           | Tag         | Recommendation           |
   +==========================+=============+==========================+
   | Frame of Reference UID   | (0020,0052) | All XA Images or         |
   |                          |             | Enhanced XA Images       |
   |                          |             | created from the         |
   |                          |             | rotational acquisitions  |
   |                          |             | share the same spatial   |
   |                          |             | relationship.            |
   +--------------------------+-------------+--------------------------+
   | Position Reference       | (0020,1040) | No recommendation to set |
   | Indicator                |             | a value, unless a system |
   |                          |             | is capable to derive     |
   |                          |             | such information from    |
   |                          |             | the anatomy or has a     |
   |                          |             | mandatory user interface |
   |                          |             | to enter such            |
   |                          |             | information.             |
   +--------------------------+-------------+--------------------------+

.. note::

   The case where all the source 2D Instances have the same FoR UID is
   the "lucky" case. If no FoR UID value is provided in the 2D
   Instances, or if the FoR UIDs are different, there should be an
   additional 2D registration step before performing the 3D
   reconstruction.

.. _sect_TTT.2.4.3.2:

X-Ray 3D Angiographic Image IOD
'''''''''''''''''''''''''''''''

.. _sect_TTT.2.4.3.2.1:

X-Ray 3D Angiographic Image Contributing Sources Module Recommendations
                                                                       

This module encodes the source SOP instance(s) used to create the X-Ray
3D Angiographic instance.

.. table:: X-Ray 3D Angiographic Image Contributing Sources Module
Recommendations

   +--------------------------+-------------+--------------------------+
   | Attribute Name           | Tag         | Recommendation           |
   +==========================+=============+==========================+
   | Contributing Sources     | (0018,9506) | One item for each of the |
   | Sequence                 |             | originating instances    |
   |                          |             | that was used for the    |
   |                          |             | reconstruction of the    |
   |                          |             | X-Ray 3D Angiographic    |
   |                          |             | image.                   |
   +--------------------------+-------------+--------------------------+

.. _sect_TTT.2.4.3.2.2:

X-Ray 3D Angiographic Acquisition Module Recommendations
                                                        

There are multiple acquisition contexts, one per rotation of the
equipment. This module encodes the frame numbers of the source SOP
instance that belong to each acquisition context, as well as the
important technical and physical parameters of the source SOP instances
used to create the X-Ray 3D Angiographic instance.

.. table:: X-Ray 3D Angiographic Acquisition Module Recommendations

   +--------------------------+-------------+--------------------------+
   | Attribute Name           | Tag         | Recommendation           |
   +==========================+=============+==========================+
   | X-Ray 3D Acquisition     | (0018,9507) | One item for each        |
   | Sequence                 |             | acquisition context      |
   |                          |             | (i.e., each rotation)    |
   |                          |             | that contributed to the  |
   |                          |             | reconstruction of the    |
   |                          |             | X-Ray 3D Angiographic    |
   |                          |             | image pixel data         |
   |                          |             | contents.                |
   +--------------------------+-------------+--------------------------+
   | …                        |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Source Image Sequence   | (0008,2112) | One item for each        |
   |                          |             | acquisition context.     |
   +--------------------------+-------------+--------------------------+
   | >>Referenced SOP Class   | (0008,1150) |                          |
   | UID                      |             |                          |
   +--------------------------+-------------+--------------------------+
   | >>Referenced SOP         | (0008,1155) | The source SOP instance  |
   | Instance UID             |             | where this rotation      |
   |                          |             | belongs.                 |
   +--------------------------+-------------+--------------------------+
   | >>Referenced Frame       | (0008,1160) | The frame numbers of the |
   | Number                   |             | projections              |
   |                          |             | corresponding to this    |
   |                          |             | rotation.                |
   +--------------------------+-------------+--------------------------+
   | …                        |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Per Projection          | (0018,9538) | The content of this      |
   | Acquisition Sequence     |             | sequence needs to be     |
   |                          |             | carefully aligned with   |
   |                          |             | the list of frame        |
   |                          |             | numbers in the           |
   |                          |             | Referenced Frame Numbers |
   |                          |             | (0008,1160) Attribute in |
   |                          |             | the Source Image         |
   |                          |             | Sequence (0008,2112).    |
   +--------------------------+-------------+--------------------------+

.. _sect_TTT.2.4.3.2.3:

Frame Content Macro Recommendations
                                   

This module encodes the timing information of the frames, as well as
dimension and stack index values.

.. table:: Frame Content Macro Recommendations

   +--------------------------+-------------+--------------------------+
   | Attribute Name           | Tag         | Recommendation           |
   +==========================+=============+==========================+
   | Frame Content Sequence   | (0020,9111) | Provides details for     |
   |                          |             | each frame.              |
   +--------------------------+-------------+--------------------------+
   | >Frame Acquisition       | (0018,9220) | Use the elapsed time     |
   | Duration                 |             | from the first           |
   |                          |             | projection frame time of |
   |                          |             | the first rotation to    |
   |                          |             | the last projection      |
   |                          |             | frame time of the last   |
   |                          |             | rotation used for this   |
   |                          |             | reconstruction.          |
   +--------------------------+-------------+--------------------------+

.. _sect_TTT.2.4.4:

Example
^^^^^^^

This example is the reconstruction of a volume by a back-projection from
all frames of a rotational acquisition with two rotations encoded as two
XA Images.

.. _sect_TTT.2.5:

Case #5: One Rotation, One 2D Instance, Multiple Reconstructions, One X-Ray 3D Instance
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This application case is related to a rotational acquisition of several
cardiac cycles with related ECG signal information.

.. _sect_TTT.2.5.1:

User Scenario
^^^^^^^^^^^^^

The image acquisition system performs one 2D rotational acquisition of
the heart in a cardiac procedure. The gantry is continuously rotating at
a constant speed. The ECG is recorded during the rotation, and the
cardiac trigger delay time is known for each frame of the rotational
acquisition allowing it to be assigned to a given cardiac phase.

Several 3D volumes are reconstructed, one for each cardiac phase.

.. _sect_TTT.2.5.2:

Encoding Outline
^^^^^^^^^^^^^^^^

The rotational acquisition can either be encoded as XA Image or as
Enhanced XA Image. The XA instance (let's call it "C") is encoded in the
Series "B" of the Study "A".

Each reconstruction is related to one cardiac phase corresponding to a
sub-set of frames of the rotational acquisition. Therefore, each cardiac
phase represents one acquisition context.

Each reconstruction leads to one volume, all volumes are encoded in one
single X-Ray 3D Angiographic instance ("Z"). Each volume is for a
different cardiac phase. All volumes share the same stack id.

.. note::

   1. This figure shows only the first three cardiac phases. An
      implementation may chose how many phases it will reconstruct.

   2. Projection frames are assigned to a phase based on their cardiac
      trigger delay time. The rotation speed and acquisition pulse rate
      will not necessarily align uniformly with the cardiac cycle
      (especially if the heartbeat is irregular). Thus different phases
      may end up with different number of projections assigned to them.
      The reconstructed volumes will have the same space.

.. _sect_TTT.2.5.3:

Encoding Details
^^^^^^^^^^^^^^^^

.. _sect_TTT.2.5.3.1:

2D X-Ray Angiographic Image IOD
'''''''''''''''''''''''''''''''

This scenario is based on the encoding of a single rotational
acquisition in one 2D instance, together with the information of the ECG
and/or the cardiac trigger delay times of each frame of the rotational
image.

.. _sect_TTT.2.5.3.2:

X-Ray 3D Angiographic Image IOD
'''''''''''''''''''''''''''''''

.. _sect_TTT.2.5.3.2.1:

Image Pixel Module Recommendations
                                  

This module encodes the description of the pixels of the slices of the
volumes, each slice being one frame of the X-Ray 3D Angiographic
instance. The pixel data encodes all the frames of the first cardiac
phase followed by all the frames of the second cardiac phase and so on.
Within one cardiac phase, the order of the frames is aligned with the
Image Position (Patient) Attribute.

.. _sect_TTT.2.5.3.2.2:

Multi-frame Dimension Module Recommendations
                                            

This module encodes the dimensions for the presentation order of the
image frames.

.. table:: Multi-frame Dimension Module Recommendations

   +--------------------------+-------------+--------------------------+
   | Attribute Name           | Tag         | Recommendation           |
   +==========================+=============+==========================+
   | Dimension Organization   | (0020,9221) | There will be a single   |
   | Sequence                 |             | Dimension UID.           |
   +--------------------------+-------------+--------------------------+
   | Dimension Organization   | (0020,9311) | The value will be "3D".  |
   | Type                     |             |                          |
   +--------------------------+-------------+--------------------------+
   | Dimension Index Sequence | (0020,9222) | Two items are defined:   |
   |                          |             | the first one related to |
   |                          |             | the cardiac phase, the   |
   |                          |             | second one related to    |
   |                          |             | the spatial position of  |
   |                          |             | the slices. All frames   |
   |                          |             | of the same              |
   |                          |             | reconstructed volume     |
   |                          |             | have the same cardiac    |
   |                          |             | phase.                   |
   +--------------------------+-------------+--------------------------+
   | >Dimension Index Pointer | (0020,9165) | In the first item, the   |
   |                          |             | Attribute Nominal        |
   |                          |             | Percentage of Cardiac    |
   |                          |             | Phase (0020,9241) is     |
   |                          |             | used. In the second      |
   |                          |             | item, the Attribute      |
   |                          |             | Image Position (Patient) |
   |                          |             | (0020,0032) is used.     |
   +--------------------------+-------------+--------------------------+
   | >Functional Group        | (0020,9167) | Contains the tags        |
   | Pointer                  |             | (0018,9118) Cardiac      |
   |                          |             | Synchronization Sequence |
   |                          |             | and (0020,9113) Plane    |
   |                          |             | Position Sequence        |
   |                          |             | respectively in the      |
   |                          |             | first and second item.   |
   +--------------------------+-------------+--------------------------+
   | >Dimension Organization  | (0020,9164) | Same value for both      |
   | UID                      |             | items.                   |
   +--------------------------+-------------+--------------------------+

.. _sect_TTT.2.5.3.2.3:

X-Ray 3D Angiographic Acquisition Module Recommendations
                                                        

There are multiple acquisition contexts, one per cardiac phase. This
module encodes the frame numbers of the source SOP instance that belong
to each acquisition context and have the same cardiac phase.

.. table:: X-Ray 3D Angiographic Acquisition Module Recommendations

   +--------------------------+-------------+--------------------------+
   | Attribute Name           | Tag         | Recommendation           |
   +==========================+=============+==========================+
   | X-Ray 3D Acquisition     | (0018,9507) | One item for each        |
   | Sequence                 |             | acquisition context      |
   |                          |             | (i.e., each cardiac      |
   |                          |             | phase).                  |
   +--------------------------+-------------+--------------------------+
   | >Source Image Sequence   | (0008,2112) |                          |
   +--------------------------+-------------+--------------------------+
   | >>Referenced Frame       | (0008,1160) | The frame numbers of the |
   | Number                   |             | source SOP instance that |
   |                          |             | belong to this           |
   |                          |             | acquisition context      |
   |                          |             | (i.e., that have the     |
   |                          |             | same cardiac phase).     |
   |                          |             |                          |
   |                          |             | .. note::                |
   |                          |             |                          |
   |                          |             |    The number of         |
   |                          |             |    projection frames may |
   |                          |             |    be different for each |
   |                          |             |    acquisition context.  |
   |                          |             |    See Note 2 of         |
   |                          |             |    `Encoding             |
   |                          |             |    Outli                 |
   |                          |             | ne <#sect_TTT.2.5.2>`__. |
   +--------------------------+-------------+--------------------------+

.. _sect_TTT.2.5.3.2.4:

X-Ray 3D Reconstruction Module Recommendations
                                              

This module encodes the identification of the reconstructions performed
to create the X-Ray 3D Angiographic Instance.

.. table:: X-Ray 3D Reconstruction Module Recommendations

   +--------------------------+-------------+--------------------------+
   | Attribute Name           | Tag         | Recommendation           |
   +==========================+=============+==========================+
   | X-Ray 3D Reconstruction  | (0018,9530) | One item for each single |
   | Sequence                 |             | reconstruction, i.e.,    |
   |                          |             | for each cardiac phase.  |
   +--------------------------+-------------+--------------------------+
   | >Acquisition Index       | (0020,9518) | Number of the            |
   |                          |             | acquisition context for  |
   |                          |             | this reconstruction. As  |
   |                          |             | there is one             |
   |                          |             | reconstruction for each  |
   |                          |             | cardiac phase, the       |
   |                          |             | acquisition index is     |
   |                          |             | equal to the             |
   |                          |             | reconstruction index.    |
   +--------------------------+-------------+--------------------------+
   | >Reconstruction          | (0018,9531) | Free text description of |
   | Description              |             | the purpose of the       |
   |                          |             | reconstruction. It's     |
   |                          |             | recommended to identify  |
   |                          |             | the cardiac phase.       |
   +--------------------------+-------------+--------------------------+

.. _sect_TTT.2.5.3.2.5:

Frame Content Macro Recommendations
                                   

This module encodes the timing information of the frames, as well as
dimension and stack index values. All frames forming a volume of one
cardiac phase have the same time reference, and a single dimension index
value for the first dimension. All volumes for all cardiac phases share
the same stack id because they span the same space.

.. table:: Frame Content Macro Recommendations

   +--------------------------+-------------+--------------------------+
   | Attribute Name           | Tag         | Recommendation           |
   +==========================+=============+==========================+
   | Frame Content Sequence   | (0020,9111) |                          |
   +--------------------------+-------------+--------------------------+
   | >Frame Reference         | (0018,9151) | Use the date and time of |
   | DateTime                 |             | the first 2D frame used  |
   |                          |             | for the reconstruction   |
   |                          |             | of this 3D frame. In     |
   |                          |             | practice it will be the  |
   |                          |             | time of the first        |
   |                          |             | projection of this       |
   |                          |             | cardiac phase.           |
   +--------------------------+-------------+--------------------------+
   | >Frame Acquisition       | (0018,9074) | Use the same value as    |
   | DateTime                 |             | the Frame Reference      |
   |                          |             | DateTime (0018,9151).    |
   +--------------------------+-------------+--------------------------+
   | >Frame Acquisition       | (0018,9220) | Use the elapsed time     |
   | Duration                 |             | from the first to the    |
   |                          |             | last projection frame    |
   |                          |             | time used for the        |
   |                          |             | reconstruction of this   |
   |                          |             | 3D frame.                |
   +--------------------------+-------------+--------------------------+
   | >Cardiac Cycle Position  | (0018,9236) | Use the most             |
   |                          |             | representative position  |
   |                          |             | in the cardiac cycle.    |
   +--------------------------+-------------+--------------------------+
   | >Dimension Index Values  | (0020,9157) | The first value of this  |
   |                          |             | Attribute contains the   |
   |                          |             | same index for all the   |
   |                          |             | frames of the same       |
   |                          |             | volume (i.e., same       |
   |                          |             | cardiac phase). The      |
   |                          |             | second value indexes the |
   |                          |             | spatial position of each |
   |                          |             | frame in the volume.     |
   +--------------------------+-------------+--------------------------+
   | >Stack ID                | (0020,9056) | Same ID for all the      |
   |                          |             | frames of all cardiac    |
   |                          |             | phases.                  |
   +--------------------------+-------------+--------------------------+
   | >In-Stack Position       | (0020,9057) | From 1 to M for each     |
   | Number                   |             | cardiac phase, where M   |
   |                          |             | is the number of frames  |
   |                          |             | in each reconstructed    |
   |                          |             | phase.                   |
   |                          |             |                          |
   |                          |             | The spatially            |
   |                          |             | corresponding frames in  |
   |                          |             | different cardiac phases |
   |                          |             | share the same In-Stack  |
   |                          |             | Position Number.         |
   +--------------------------+-------------+--------------------------+

.. _sect_TTT.2.5.3.2.6:

Cardiac Synchronization Macro Recommendations
                                             

This module encodes a value representing the cardiac phase of the 3D
frames (i.e., the time of the frame relative to the R-peak).

.. table:: Cardiac Synchronization Macro Recommendations

   +--------------------------+-------------+--------------------------+
   | Attribute Name           | Tag         | Recommendation           |
   +==========================+=============+==========================+
   | Cardiac Synchronization  | (0018,9118) |                          |
   | Sequence                 |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Nominal Percentage of   | (0020,9241) | All the frames belonging |
   | Cardiac Phase            |             | to the same              |
   |                          |             | reconstruction will have |
   |                          |             | the same value. This     |
   |                          |             | Attribute is used as a   |
   |                          |             | dimension index.         |
   +--------------------------+-------------+--------------------------+
   | >Nominal Cardiac Trigger | (0020,9153) | Use the average time in  |
   | Delay Time               |             | ms from the time of the  |
   |                          |             | previous R-peak to the   |
   |                          |             | value of the Frame       |
   |                          |             | Reference DateTime       |
   |                          |             | (0018,9151).             |
   +--------------------------+-------------+--------------------------+

.. _sect_TTT.2.5.3.2.7:

X-Ray 3D Frame Type Macro Recommendations
                                         

This macro encodes the context of the volume slices. In this scenario of
multi-volume encoding, it is encoded "per frame", since the slices
belong to different volumes depending on the cardiac phase.

.. _sect_TTT.2.5.4:

Example
^^^^^^^

In this example the gantry performs one single rotation around the heart
at 20 degrees per second, covering an arc of 200 degrees during 10
seconds. Approximately 10 cardiac cycles are acquired. The frame rate is
8 frames per second, resulting in 8 projections acquired at each cardiac
cycle corresponding to 8 different cardiac phases.

Overall there will be 80 projections; 10 projections for each of the 8
cardiac phases. Each cardiac phase represents one acquisition context.
The information of the cardiac trigger delay time is encoded for each
projection. The projections are encoded as an XA Image with the Instance
UID "C".

The reconstruction application creates 8 volumes, each volume is
reconstructed by a back-projection from the 10 frames having the same
cardiac trigger delay time, i.e., the frames acquired at the same
cardiac phase. Each volume contains 256 frames. The 8 reconstructed
volumes are encoded in one single X-Ray 3D Angiographic instance of
Instance UID "Z".

.. _sect_TTT.2.6:

Case #6: Two Rotations, Two 2D Instances, Two Reconstructions, Two X-Ray 3D Instances
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This application case is related to two rotational acquisitions on the
same anatomical region before and after the intervention, with table
movement between the two acquisitions. The two reconstructed volumes are
created and automatically registered on the same patient coordinate
system.

.. _sect_TTT.2.6.1:

User Scenario
^^^^^^^^^^^^^

The image acquisition system performs two different 2D rotational
acquisitions at two different times of the interventional procedure: the
first acquisition before the intervention (e.g., before placement of a
stent) and the second one after the intervention.

Between the two acquisitions the table position has changed with respect
to the Isocenter. The rotational acquisitions are performed with the
same spatial trajectory of the X-Ray Detector relative to the Isocenter;
therefore the second acquisition contains a slightly different region of
the patient.

Two 3D volumes are reconstructed, one for each rotational acquisition.
After the intervention, the two 3D volumes are displayed together on the
same patient coordinate system. The user can visually assess the
placement of the stent over the anatomy pre-intervention. The patient
position on the table does not change during the procedure.

.. _sect_TTT.2.6.2:

Encoding Outline
^^^^^^^^^^^^^^^^

The rotational acquisitions can either be encoded as XA Image or as
Enhanced XA Image. The two XA instances (let's call them "C1" and "C2")
are encoded in two different Series ("B1" and "B2") of the same Study
("A").

The volume data is encoded as two X-Ray 3D Angiographic instances ("Z1"
and "Z2"). The volumes are typically a full set (in number of rows,
columns and slices) of the projected matrix size (in number of rows and
columns).

Each reconstructed volume contains one acquisition context consisting of
all the frames of the corresponding source 2D XA Image. To display the
two volumes together, they share the same Frame of Reference UID.

.. _sect_TTT.2.6.3:

Encoding Details
^^^^^^^^^^^^^^^^

.. _sect_TTT.2.6.3.1:

X-Ray 3D Angiographic Image IOD
'''''''''''''''''''''''''''''''

.. _sect_TTT.2.6.3.1.1:

Frame of Reference Module Recommendations
                                         

Since the purpose of this scenario is to overlap the two volumes without
additional spatial registration, the spatial location of the anatomy of
interest in both volumes needs to be the same. To keep the two volumes
spatially registered, the reconstruction application will use the table
position of both rotations to correct the table movement with respect to
the Isocenter, thus creating both volumes with the same spatial origin
and axis, i.e., same patient coordinate system.

Therefore, it is recommended to encode both instances with the same FoR
UID, equal to the Frame of Reference UID of the XA projection images. If
the originating XA images do not contain a Frame of Reference UID, the
reconstruction application will create the FoR UID equal for the two
reconstructed volumes.

.. table:: Frame of Reference Module Recommendations

   +--------------------------+-------------+--------------------------+
   | Attribute Name           | Tag         | Recommendation           |
   +==========================+=============+==========================+
   | Frame of Reference UID   | (0020,0052) | Use the same FoR UID     |
   |                          |             | value for both volumes.  |
   +--------------------------+-------------+--------------------------+
   | Position Reference       | (0020,1040) | Use a value either       |
   | Indicator                |             | provided by the operator |
   |                          |             | of the acquisition       |
   |                          |             | modality or the          |
   |                          |             | reconstruction console,  |
   |                          |             | if supplied.             |
   +--------------------------+-------------+--------------------------+

.. _sect_TTT.2.6.3.1.2:

Patient Orientation Module Recommendations
                                          

This module encodes the patient orientation with respect to the table.
It is supposed to contain the same values in both 3D volumes, since the
patient does not move between the two rotational acquisitions.

.. _sect_TTT.2.6.3.1.3:

Pixel Measures Macro Recommendations
                                    

The detailed size of the volume element (Pixel Spacing for row/column
dimension of each slice and Slice Thickness for the distance of slices)
depends on the reconstruction algorithm and is not necessarily identical
to the related sizes in the source (projection) image(s).

.. table:: Pixel Measures Macro Recommendations

   +-------------------------+-------------+--------------------------+
   | Attribute Name          | Tag         | Recommendation           |
   +=========================+=============+==========================+
   | Pixel Measures Sequence | (0028,9110) | Provide it as a shared   |
   |                         |             | macro, i.e., each slice  |
   |                         |             | of a volume has the same |
   |                         |             | Pixel Spacing and Slice  |
   |                         |             | Thickness.               |
   +-------------------------+-------------+--------------------------+
   | >Pixel Spacing          | (0028,0030) | May be different between |
   |                         |             | the two volumes.         |
   +-------------------------+-------------+--------------------------+
   | >Slice Thickness        | (0018,0050) | May be different between |
   |                         |             | the two volumes.         |
   +-------------------------+-------------+--------------------------+

.. _sect_TTT.2.6.3.1.4:

Plane Position (Patient) Macro Recommendations
                                              

This macro encodes the position of the 3D slices relative to the
patient.

It is assumed that the patient does not move on the table between the
two rotational acquisitions, but the table moves with respect to the
Isocenter. Although the spatial trajectory of the X-Ray Detector
relative to the Isocenter of the two rotational acquisitions is the
same, the two volumes contain a different region of the patient.

To allow spatial registration between the two volumes, the position of
the slices of the two volumes need to be defined with respect to the
same point of the patient. As the patient does not move on the table,
the reconstruction application will define the patient origin as a fixed
point on the table, so that the 3D slices of the two volumes are all
related to the same fixed point on the table (i.e., same point of the
patient) by the Attribute Image Position (Patient) (0020,0032).

The volume is positioned in the spatial coordinates identified by the
frame of reference, which is common to the two volumes. Therefore, the
position of the slices of both volumes is defined with respect to the
same patient origin.

.. _sect_TTT.2.6.3.1.5:

Plane Orientation (Patient) Macro Recommendations
                                                 

The slices can be oriented in any relation wrt. the patient coordinate
system. The plane orientation is expected to be the same for the two
volumes; however it could be different without compromising the
registration.

.. _sect_TTT.2.6.4:

Example
^^^^^^^

In this example, two rotational images are acquired; the first one
before the intervention and the second one after the intervention. They
are encoded with the Instance UIDs "C1" and "C2" respectively.

In both rotational acquisitions, the patient position with respect to
the table is head-first prone, and the table is not rotated nor tilted
with respect to the Isocenter. The patient coordinates and the Isocenter
coordinates are then aligned on x, y and z.

The patient origin is defined by the application as a fixed point on the
table.

During the first rotational acquisition, the table position with respect
to the Isocenter in the lateral direction [x] is +20mm, in the vertical
direction [y] is +40mm, and in the longitudinal direction [z] is +60mm.

During the second rotational acquisition, the table position with
respect to the Isocenter in the lateral direction [x] is -10mm, in the
vertical direction [y] is +80mm, and in the longitudinal direction [z]
is +110mm.

The second acquisition is performed with a relative table movement of
(-30,40,50) mm vs. the first acquisition in the patient coordinates
system. Therefore, for a given 3D slice "i" of the two volumes, the
Image Position (Patient) (0020,0032) of the second volume is translated
of (+30,-40,-50) mm vs. the Image Position (Patient) (0020,0032) of the
first volume.

The two reconstructions are performed with the same number of rows,
columns and slices, and both at the same resolution of 0.2 mm/voxel.
Note that if the resolution was different, the Image Position (Patient)
(0020,0032) of the second volume would be additionally translated by the
shift of the TLHC pixels relative to the center of the volume, because
both volumes are centered at the Isocenter.

The reconstructions are encoded in two X-Ray 3D Angiographic instances
of Instance UIDs "Z1" and "Z2" respectively.

.. _sect_TTT.2.7:

Case #7: Spatial Registration of 3D X-Ray Angiography With Enhanced XA
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This application case is related to the spatial registration of the
X-Ray 3D volume with a static projection acquisition on the same
anatomical region during the procedure.

.. _sect_TTT.2.7.1:

User Scenario
^^^^^^^^^^^^^

The image acquisition system performs two different 2D acquisitions at
two different times of the interventional procedure: one rotational
acquisition with a 3D reconstruction, and one static acquisition.

Between the two acquisitions, the table position has changed with
respect to the Isocenter. As the acquisitions are performed with the
X-Ray Detector centered on the Isocenter, in the second static
acquisition the anatomical region of the 3D volume is not centered
anymore at the Isocenter due to the table movement. It's assumed that
there is still part of the anatomy of the 3D volume that is projected in
the static acquisition.

During the intervention the 3D volume is segmented to extract some
anatomy that is less or not visible in the static acquisition (e.g.,
injected vessels, heart chambers). The user will want to display such 3D
anatomy over the 2D static image to visually assess the placement of
interventional devices like guide wires, needles etc. The patient
position on the table does not change during the procedure.

.. _sect_TTT.2.7.2:

Encoding Outline
^^^^^^^^^^^^^^^^

The two 2D acquisitions are encoded as two Enhanced XA Images, and both
contain the Attributes of the X-Ray Isocenter Reference System Macro
(see ). The two XA instances (let's call them "C1" and "C2") are encoded
in two different Series ("B1" and "B2") of the same Study ("A"). They
share the same Frame of Reference UID.

The volume data is encoded as an X-Ray 3D Angiographic instance ("Z1").

The reconstructed volume contains one acquisition context consisting of
all the frames of the corresponding source 2D XA Image. To display the
volume over the projection image, both volume and projection image share
the same Frame of Reference UID.

.. _sect_TTT.2.7.3:

Encoding Details
^^^^^^^^^^^^^^^^

.. _sect_TTT.2.7.3.1:

Enhanced X-Ray Angiographic Image IOD
'''''''''''''''''''''''''''''''''''''

This scenario is based on the encoding of the 2D acquisition as an
Enhanced XA Image, containing the Attributes of the X-Ray Isocenter
Reference System Macro (see ).

.. _sect_TTT.2.7.3.2:

X-Ray 3D Angiographic Image IOD
'''''''''''''''''''''''''''''''

.. _sect_TTT.2.7.3.2.1:

Frame of Reference Module Recommendations
                                         

This module encodes the identifier for the spatial relationship, which
will be the same for the volume and the projection image. The
reconstruction application will assign the Frame of Reference UID to the
reconstruction equal to the Frame of Reference UID of the Enhanced XA
projection image.

.. _sect_TTT.2.7.3.2.2:

Patient Orientation Module
                          

This module encodes the patient position and orientation with respect to
the table. It is supposed to contain the same values in the 3D volume
and in the 2D static image.

.. _sect_TTT.2.7.3.2.3:

Image - Equipment Coordinate Relationship Module
                                                

This module encodes the coordinate transformation matrix to allow the
spatial registration of the volume with the Isocenter reference system
of the angiographic equipment.

The reconstruction application defines the patient origin as an
arbitrary point on the equipment. The 3D slices of the volume are all
related to the patient coordinate system by the Attributes Image
Position (Patient) (0020,0032) and Image Orientation (Patient)
(0020,0037).

The patient is related to the Isocenter by the Attribute Image to
Equipment Mapping Matrix (0028,9520) which indicates the spatial
transformation from the patient coordinates to the Isocenter
coordinates. A point in the Patient Coordinate System (Bx, By, Bz) can
be expressed in the Isocenter Coordinate System (Ax, Ay, Az) by applying
the Image to Equipment Mapping Matrix as follows.

The terms (T\ :sub:`x`,T\ :sub:`y`,T\ :sub:`z`) of this matrix indicate
the position of the patient origin (i.e., a fixed point on the table) in
the Isocenter coordinate system.

.. table:: Image-Equipment Coordinate Relationship Module
Recommendations

   +--------------------------+-------------+--------------------------+
   | Attribute Name           | Tag         | Recommendation           |
   +==========================+=============+==========================+
   | Equipment Coordinate     | (0028,9537) | The value will be        |
   | System Identification    |             | ISOCENTER.               |
   +--------------------------+-------------+--------------------------+

.. _sect_TTT.2.7.3.2.4:

X-Ray 3D Angiographic Acquisition Module Recommendations
                                                        

This module encodes the table position and angles used during the
rotational acquisition to allow the spatial transformation of the volume
points from the Isocenter coordinates to the table coordinates. See for
further explanation about the spatial transformation from the Isocenter
reference system to the table reference system.

As soon as the volume points are related to the table coordinate system,
and assuming that the patient does not move on the table between the 2D
acquisitions, the volume points can be projected on the image plane of
any further projection acquisition even if the table has moved between
the acquisitions. See for further explanation about the projection on
the image plane of a point defined in the table coordinate system.

.. _sect_TTT.2.7.4:

Example
^^^^^^^

In this example, one rotational image is acquired before the
intervention. It is encoded with the Instance UID "C1". Then a second
projection static image is acquired during the intervention. It is
encoded with the Instance UID "C2". Both acquisitions are encoded as
Enhanced XA SOP Class.

In both acquisitions, the patient position with respect to the table is
head-first prone, and the table is not rotated nor tilted with respect
to the Isocenter. Therefore, the axis of the patient coordinate system
and the Isocenter coordinate system are aligned, and the 3x3 matrix
M\ :sub:`ij` of the Image to Equipment Mapping Matrix (0028,9520) is the
identity.

In this example, the patient origin is defined by the application as a
fixed point on the table; when the table position is zero, the patient
origin is the point (0,0,200) in the Isocenter coordinates system (in
mm).

During the rotational acquisition, the table position with respect to
the Isocenter in the lateral direction [x] is +20mm, in the vertical
direction [y] is +40mm, and in the longitudinal direction [z] is +60mm.
Therefore, the terms (T\ :sub:`x`,T\ :sub:`y`,T\ :sub:`z`) of the Image
to Equipment Mapping Matrix (0028,9520) are (20,40,260).

During the second acquisition, the table position with respect to the
Isocenter in the lateral direction [x] is +40mm, in the vertical
direction [y] is +30mm, and in the longitudinal direction [z] is +20mm.

Consequently, the second acquisition is performed with a relative table
translation of (30,-10,-50) mm vs. the first acquisition in the
Isocenter coordinate system. The positioner primary angle is -30 deg.
(RAO) and the secondary angle is 20 deg. (CRA). The distances from the
source to the Isocenter and from the source to the detector are 780 mm
and 1200 mm respectively.

The reconstruction is encoded in an X-Ray 3D Angiographic instance of
Instance UID "Z1".

