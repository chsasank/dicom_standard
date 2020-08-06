.. _chapter_IIII:

Encapsulated STL (Informative)
==============================

The goal of encapsulating a Stereolithography (STL) 3D manufacturing
model file inside a DICOM instance rather than transforming the data
into a different representation is to facilitate preservation of the STL
file in the exact form that it is used with extant manufacturing
devices, while at the same time unambiguously associating it with the
patient for whose care the model was created and the images from which
the model was derived.

.. _sect_IIII.1:

Example of CT Derived Encapsulated STL
--------------------------------------

In this example, the patient requires a replacement implant for a large
piece of skull on the left side of his head. A 3D manufacturing model
(encoded in binary STL) was created by mirroring the corresponding
section of the patient's right skull hemisphere, and then modified by
trimming to fit the specific implantation area.

The model was derived from a series of CT images (CT-01). The STL data
in this example is the first version, having no predecessor. The STL
data was created on November 22, 2017 at 7:10:14 AM and then stored in a
DICOM instance at 7:15:23 AM. The CT images were acquired weeks earlier.

The STL data was created in the coordinate system of CT-01; so they
share the same Frame of Reference UID value.

A preview image (optional) showing the rendered 3D object was created
and included with the encapsulated STL as an icon image.

No burned in annotation identifying the patient was included. The region
of the skull reconstructed in the model contains no distinguishing
facial features of the patient.

.. table:: CT Derived Encapsulated STL Example

   +-----------------+-------------+-----------------+-----------------+
   | Attribute Name  | Tag         | Example Value   | Comments        |
   +=================+=============+=================+=================+
   | *<Patient and   |             |                 |                 |
   | General Study   |             |                 |                 |
   | Modules not     |             |                 |                 |
   | shown for       |             |                 |                 |
   | brevity>*       |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Modality        | (0008,0060) | M3D             |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Series Instance | (0020,000E) | 2.999.89235.    |                 |
   | UID             |             | 5951.35894.0047 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Series Number   | (0020,0011) | 3               |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Series          | (0008,103E) | Skull plate     |                 |
   | Description     |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Instance Number | (0020,0013) | 1               |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Frame of        | (0020,0052) | 1.2             |                 |
   | Reference UID   |             | .3.4.5.6.7.8.99 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Manufacturer    | (0008,0070) | Acme Additive   |                 |
   |                 |             | Inc             |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Manufacturer's  | (0008,1090) | Implant Maker   |                 |
   | Model Name      |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Device Serial   | (0018,1000) | 00004367        |                 |
   | Number          |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Software        | (0018,1020) | 3.0.1           |                 |
   | Versions        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Content Date    | (0008,0023) | 20171122        |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Content Time    | (0008,0033) | 071014          |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Acquisition     | (0008,002A) | 20171122071014  |                 |
   | DateTime        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Image           | (0020,0062) | L               |                 |
   | Laterality      |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Burned In       | (0028,0301) | NO              |                 |
   | Annotation      |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Recognizable    | (0028,0302) | NO              |                 |
   | Visual Features |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Source Instance | (0042,0013) |                 | A sequence      |
   | Sequence        |             |                 | referencing the |
   |                 |             |                 | CT-01 source    |
   |                 |             |                 | images          |
   +-----------------+-------------+-----------------+-----------------+
   | %item           |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Referenced SOP | (0008,1150) | 1.2.840.1000    | Referenced      |
   | Class UID       |             | 8.5.1.4.1.1.2.1 | object is an    |
   |                 |             |                 | Enhanced CT     |
   |                 |             |                 | Image Storage   |
   |                 |             |                 | Instance        |
   +-----------------+-------------+-----------------+-----------------+
   | >Referenced SOP | (0008,1155) | 2.999.89235     | The multi-frame |
   | Instance UID    |             | .5951.35894.155 | CT instance     |
   |                 |             |                 | from study      |
   |                 |             |                 | CT-01           |
   +-----------------+-------------+-----------------+-----------------+
   | >Purpose of     | (0040,A170) | (121324, DCM,   |                 |
   | Reference Code  |             | "Source image") |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | %enditem        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Document Title  | (0042,0010) | CT 3D CAM model |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Concept Name    | (0040,A043) | `(85040-4, LN,  |                 |
   | Code Sequence   |             | "CT 3D CAM      |                 |
   |                 |             | model")         |                 |
   |                 |             | <http://loinc.o |                 |
   |                 |             | rg/24725-4/>`__ |                 |
   +-----------------+-------------+-----------------+-----------------+
   | MIME Type of    | (0040,0012) | model/stl       |                 |
   | Encapsulated    |             |                 |                 |
   | Document        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Encapsulated    | (0042,0011) | <Byte stream    | Note that ASCII |
   | Document        |             | representing    | STL files are   |
   |                 |             | the binary STL  | not supported.  |
   |                 |             | file>           |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Content         | (0070,0081) | Mirrored and    |                 |
   | Description     |             | trimmed skull   |                 |
   |                 |             | plate model     |                 |
   |                 |             | from CT         |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Measurement     | (0040,08EA) | (mm, UCUM,      |                 |
   | Units Code      |             | "mm")           |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Model           | (0068,7001) | YES             |                 |
   | Modification    |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Model Mirroring | (0068,7002) | YES             | In this         |
   |                 |             |                 | example,        |
   |                 |             |                 | mirroring (from |
   |                 |             |                 | the right side) |
   |                 |             |                 | was performed   |
   |                 |             |                 | to create the   |
   |                 |             |                 | object.         |
   +-----------------+-------------+-----------------+-----------------+
   | Model Usage     | (0068,7003) | (129016, DCM,   | In this         |
   | Code Sequence   |             | "Implant        | example, the    |
   |                 |             | Fabrication")   | goal is to      |
   |                 |             |                 | implant the     |
   |                 |             |                 | object in the   |
   |                 |             |                 | patient.        |
   +-----------------+-------------+-----------------+-----------------+
   | Icon Image      | (0088,0200) |                 | Sequence        |
   | Sequence        |             |                 | containing the  |
   |                 |             |                 | pre-rendered    |
   |                 |             |                 | preview image   |
   +-----------------+-------------+-----------------+-----------------+
   | %item           |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | *<Content of    |             |                 |                 |
   | Table C.7-11b   |             |                 |                 |
   | "Image Pixel    |             |                 |                 |
   | Macro           |             |                 |                 |
   | Attributes" not |             |                 |                 |
   | shown>*         |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | %enditem        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | SOP Class UID   | (0008,0016) | 1.2.840.10008.  |                 |
   |                 |             | 5.1.4.1.1.104.3 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | SOP Instance    | (0008,0018) | 1.2.3           |                 |
   | UID             |             | .4.5.6.7.88.901 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Instance        | (0008,0012) | 20171122        |                 |
   | Creation Date   |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Instance        | (0008,0013) | 071523          |                 |
   | Creation Time   |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+

.. _sect_IIII.2:

Example of Fused CT/MR Derived Encapsulated STL
-----------------------------------------------

In this example, the patient will shortly be undergoing a complex
cardiac surgery. A 3D manufacturing model (encoded in binary STL) was
created to manufacture a surgical planning aid representing the
patient's unique anatomy.

To begin, a series of CT images (CT-02) and a series of MR images
(MR-01) were registered using CT-02's frame of reference as the base
coordinate system and then fused. An initial version of the model was
derived and reviewed by the surgical team who requested that some of the
anatomy surrounding the heart be removed. A second version of the model
was created on July 16, 2017 at 1:04:34 PM then stored in a DICOM
instance at 1:33:01 PM. The CT and MR data were acquired at earlier
dates.

The Encapsulated STL file shown in this example is the second version..

Both versions of the STL were created in the coordinate system of CT-02;
so they all share the same Frame of Reference value.

Note: Mapping to other Frames of Reference of secondary source series
would be handled via registration objects.

A preview image (optional) showing the rendered 3D object was created
and included with the encapsulated STL as an icon image.

The creator of the model inscribed the patient's medical record number
on a side of the model to avoid the possibility of a wrong patient
error.

.. table:: Fused CT/MR Derived Encapsulated STL Example

   +-----------------+-------------+-----------------+-----------------+
   | Attribute Name  | Tag         | Example Value   | Comments        |
   +=================+=============+=================+=================+
   | *<Patient and   |             |                 |                 |
   | General Study   |             |                 |                 |
   | Modules not     |             |                 |                 |
   | shown for       |             |                 |                 |
   | brevity>*       |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Modality        | (0008,0060) | M3D             |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Series Instance | (0020,000E) | 2.999.89235.    |                 |
   | UID             |             | 5951.35894.0086 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Series Number   | (0020,0011) | 6               |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Series          | (0008,103E) | 3DP Models      |                 |
   | Description     |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Instance Number | (0020,0013) | 2               |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Frame of        | (0020,0052) | 1.2.            |                 |
   | Reference UID   |             | 3.4.5.6.777.0.1 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Manufacturer    | (0008,0070) | Acme Additive   |                 |
   |                 |             | Inc             |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Manufacturer's  | (0008,1090) | Cardioplan      |                 |
   | Model Name      |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Device Serial   | (0018,1000) | 10065789        |                 |
   | Number          |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Software        | (0018,1020) | 6.3             |                 |
   | Versions        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Content Date    | (0008,0023) | 20170716        |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Content Time    | (0008,0033) | 130034          |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Acquisition     | (0008,002A) | 20170716130034  |                 |
   | DateTime        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Image           | (0020,0062) | U               |                 |
   | Laterality      |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Burned In       | (0028,0301) | YES             |                 |
   | Annotation      |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Recognizable    | (0028,0302) | NO              |                 |
   | Visual Features |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Source Instance | (0042,0013) |                 | A sequence      |
   | Sequence        |             |                 | referencing     |
   |                 |             |                 | CT-02 and MR-01 |
   |                 |             |                 | source images   |
   |                 |             |                 | because both    |
   |                 |             |                 | were used.      |
   +-----------------+-------------+-----------------+-----------------+
   | %item           |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Referenced SOP | (0008,1150) | 1.2.840.1000    | Referenced      |
   | Class UID       |             | 8.5.1.4.1.1.2.1 | object is an    |
   |                 |             |                 | Enhanced CT     |
   |                 |             |                 | Image Storage   |
   |                 |             |                 | Instance        |
   +-----------------+-------------+-----------------+-----------------+
   | >Referenced SOP | (0008,1155) | 2.999.89235     | The multi-frame |
   | Instance UID    |             | .5951.35894.153 | CT instance     |
   |                 |             |                 | from study      |
   |                 |             |                 | CT-02           |
   +-----------------+-------------+-----------------+-----------------+
   | >Purpose of     | (0040,A170) | (121324, DCM,   |                 |
   | Reference Code  |             | "Source image") |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | %enditem        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | %item           |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Referenced SOP | (0008,1150) | 1.2.840.1000    | Referenced      |
   | Class UID       |             | 8.5.1.4.1.1.4.1 | object is an    |
   |                 |             |                 | Enhanced MR     |
   |                 |             |                 | Image Storage   |
   |                 |             |                 | Instance        |
   +-----------------+-------------+-----------------+-----------------+
   | >Referenced SOP | (0008,1155) | 2.999.89235     | The multi-frame |
   | Instance UID    |             | .5951.35894.154 | MR instance     |
   |                 |             |                 | from study      |
   |                 |             |                 | MR-01           |
   +-----------------+-------------+-----------------+-----------------+
   | >Purpose of     | (0040,A170) | (121324, DCM,   |                 |
   | Reference Code  |             | "Source image") |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | %enditem        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Document Title  | (0042,0010) | Mixed Modality  |                 |
   |                 |             | 3D CAM model    |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Concept Name    | (0040,A043) | (129019, DCM,   |                 |
   | Code Sequence   |             | "Mixed Modality |                 |
   |                 |             | 3D CAM model")  |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Predecessor     | (0040,A360) |                 | A reference to  |
   | Documents       |             |                 | the earlier     |
   | Sequence        |             |                 | encapsulated    |
   |                 |             |                 | STL             |
   +-----------------+-------------+-----------------+-----------------+
   | %item           |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Study Instance | (0020,000D) | 2.999.1241.15   |                 |
   | UID             |             | 15.15151.515.62 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Reference      | (0008,1115) |                 |                 |
   | Series Sequence |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | %item           |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Series        | (0020,000E) | 2.999.89235     |                 |
   | Instance UID    |             | .5951.35894.151 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Referenced    | (0008,1199) |                 |                 |
   | SOP Sequence    |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | %item           |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>Referenced   | (0008,1150) | 1.2.840.10008.5 | Encapsulated    |
   | SOP Class UID   |             | .1.4.1.1.104.3x | STL SOP Class   |
   +-----------------+-------------+-----------------+-----------------+
   | >>>Referenced   | (0008,1155) | 2.999.1241.15   |                 |
   | SOP Instance    |             | 15.15151.515.68 |                 |
   | UID             |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | %enditem        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Purpose of    | (0040,A170) | (129010, DCM,   |                 |
   | Reference Code  |             | "Edited Model") |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | %enditem        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | %enditem        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | MIME Type of    | (0040,0012) | model/stl       |                 |
   | Encapsulated    |             |                 |                 |
   | Document        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Encapsulated    | (0042,0011) | *<Byte stream   | Note that ASCII |
   | Document        |             | representing    | STL files are   |
   |                 |             | the binary STL  | not supported.  |
   |                 |             | file>*          |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Content         | (0070,0081) | Pre-surgery     |                 |
   | Description     |             | cardiac model   |                 |
   |                 |             | from CT and MR  |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Measurement     | (0040,08EA) | (mm, UCUM,      |                 |
   | Units Code      |             | "mm")           |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Model           | (0068,7001) | NO              |                 |
   | Modification    |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Model Mirroring | (0068,7002) | NO              |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Model Usage     | (0068,7003) | (129013, DCM,   | In this         |
   | Code Sequence   |             | "Planning       | example, the    |
   |                 |             | Intent")        | goal is to help |
   |                 |             |                 | plan the        |
   |                 |             |                 | surgery, so the |
   |                 |             |                 | value is        |
   |                 |             |                 | "Planning       |
   |                 |             |                 | Intent".        |
   +-----------------+-------------+-----------------+-----------------+
   | Icon Image      | (0088,0200) |                 | Sequence        |
   | Sequence        |             |                 | containing the  |
   |                 |             |                 | pre-rendered    |
   |                 |             |                 | preview image   |
   +-----------------+-------------+-----------------+-----------------+
   | %item           |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | *<Content of    |             |                 |                 |
   | Table C.7-11b   |             |                 |                 |
   | "Image Pixel    |             |                 |                 |
   | Macro           |             |                 |                 |
   | Attributes" not |             |                 |                 |
   | shown>*         |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | %enditem        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | SOP Class UID   | (0008,0016) | 1.2.840.10008.  |                 |
   |                 |             | 5.1.4.1.1.104.3 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | SOP Instance    | (0008,0018) | 2.999.1241.151  |                 |
   | UID             |             | 5.15151.515.987 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Instance        | (0008,0012) | 20170716        |                 |
   | Creation Date   |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Instance        | (0008,0013) | 133301          |                 |
   | Creation Time   |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+

