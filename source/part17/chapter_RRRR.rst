.. _chapter_RRRR:

Encapsulated OBJ, 3D Model Grouping, & Color (Informative)
==========================================================

.. _sect_RRRR.1:

Overview
--------

This section explains the encapsulation of a 3D manufacturing model file
of the OBJ type inside a DICOM instance. The goal of encapsulating a
model rather than transforming the data into a different representation
is to facilitate preservation of the 3D file in the exact form that it
is used with extant manufacturing devices. At the same time
encapsulation populates DICOM header elements that record clinical
information absent from the OBJ format, including unambiguously
associating it with the patient for whose care the model was created.
Encapsulation also makes it possible to link to the images from which
the model was derived, even if these came from different studies.

The OBJ encapsulation case is slightly more complicated than that of STL
(`Encapsulated STL (Informative) <#chapter_IIII>`__). The OBJ has
supporting files (material library and texture maps). The relationship
between the multiple original files and the corresponding DICOM
instances is shown in `figure_title <#figure_RRRR.1-1>`__.

.. _sect_RRRR.2:

Example Encoding of OBJ & MTL
-----------------------------

This Section contains example excerpts for encoding OBJ files and
associated preview icons (optional), materials library file (MTL)
(optional), and texture map images (optional).

.. _sect_RRRR.2.1:

Example A
~~~~~~~~~

A patient, Kevin Franz-Lopez, with Medical Record Number 547892459, will
shortly be undergoing a complex partial nephrectomy to remove lesions on
their left kidney. A 3D manufacturing model (encoded in OBJ) was created
to manufacture a surgical planning aid representing the patient's unique
anatomy.

A model was constructed from a CT dataset (CT1). The model was created
on July 16, 2017 at 1:04:34 PM. The model was expressed as a single OBJ
file (kidneymodel.obj) which makes use of two texture maps encoded using
PNG (ntissue.png and fluid.png) and one texture map encoded using JPEG
(distissue.jpg). The relationship between the OBJ and texture maps is
captured in the materials list file (matlist.mtl). This set of files
corresponds to the Encapsulated MTL and DICOM Images elements in
`figure_title <#figure_RRRR.1-1>`__.

A preview icon was created showing the rendered 3D object for inclusion
with the OBJ file when encapsulated.

`table_title <#table_RRRR.2-1>`__ shows the Encapsulated OBJ.

.. table:: Encapsulated OBJ Example A

   +-----------------+-------------+-----------------+-----------------+
   | Attribute Name  | Tag         | Example Value   | Comments        |
   +=================+=============+=================+=================+
   | Content Date    | (0008,0023) | 20170716        |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Acquisition     | (0008,002A) | 20170716        |                 |
   | DateTime        |             | 13:00:34        |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Content Time    | (0008,0033) | 13:00:34        |                 |
   +-----------------+-------------+-----------------+-----------------+
   | ...             |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Modality        | (0008,0060) | M3D             |                 |
   +-----------------+-------------+-----------------+-----------------+
   | ...             |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Series          | (0008,103E) | Nephrectomy     |                 |
   | Description     |             | Planning Models |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Referenced      | (0008,114A) |                 |                 |
   | Instance        |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | %item           |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Referenced SOP | (0008,1150) | 1.2.840.10008.  | Encapsulated    |
   | Class UID       |             | 5.1.4.1.1.104.5 | MTL file SOP    |
   |                 |             |                 | class           |
   +-----------------+-------------+-----------------+-----------------+
   | >Referenced SOP | (0008,1155) | 2.999.89235     | UID of the      |
   | Instance UID    |             | .5951.35894.751 | encapsulated    |
   |                 |             |                 | MTL file (see   |
   |                 |             |                 | below)          |
   |                 |             |                 | supporting this |
   |                 |             |                 | OBJ model       |
   +-----------------+-------------+-----------------+-----------------+
   | >Relative URI   | (0068,7005) | "matlist.mtl"   | Relative URI    |
   | Reference       |             |                 | that preserved  |
   | Within          |             |                 | the MTL file's  |
   | Encapsulated    |             |                 | original        |
   | Document        |             |                 | filename as     |
   |                 |             |                 | referenced from |
   |                 |             |                 | within the OBJ  |
   |                 |             |                 | file.           |
   +-----------------+-------------+-----------------+-----------------+
   | %enditem        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | ...             |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Patient Name    | (0010,0010) | Fr              |                 |
   |                 |             | anz-Lopez^Kevin |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Patient ID      | (0010,0020) | 547892459       |                 |
   +-----------------+-------------+-----------------+-----------------+
   | ...             |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Image           | (0020,0062) | L               |                 |
   | Laterality      |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Burned In       | (0028,0301) | YES             | In this         |
   | Annotation      |             |                 | example, the    |
   |                 |             |                 | creator of the  |
   |                 |             |                 | model inscribed |
   |                 |             |                 | the patient's   |
   |                 |             |                 | medical record  |
   |                 |             |                 | number on a     |
   |                 |             |                 | side of the     |
   |                 |             |                 | model, to avoid |
   |                 |             |                 | the possibility |
   |                 |             |                 | of a wrong      |
   |                 |             |                 | patient error.  |
   +-----------------+-------------+-----------------+-----------------+
   | Recognizable    | (0028,0302) | NO              |                 |
   | Visual Features |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | MIME Type of    | (0040,0012) | model/obj       |                 |
   | Encapsulated    |             |                 |                 |
   | Document        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | %item           |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Referenced SOP | (0008,1150) | 1.2.840.1000    | Referenced      |
   | Class UID       |             | 8.5.1.4.1.1.2.1 | object is an    |
   |                 |             |                 | Enhanced CT     |
   |                 |             |                 | Image Storage   |
   +-----------------+-------------+-----------------+-----------------+
   | >Referenced SOP | (0008,1155) | 2.999.89235     | The multi-frame |
   | Instance UID    |             | .5951.35894.153 | CT image from   |
   |                 |             |                 | study CT1       |
   +-----------------+-------------+-----------------+-----------------+
   | %enditem        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | ...             |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Measurement     | (0040,08EA) |                 |                 |
   | Units Code      |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | %item           |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   |                 |             | (mm, UCUM,      |                 |
   |                 |             | "mm")           |                 |
   +-----------------+-------------+-----------------+-----------------+
   | %enditem        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | ...             |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Document Title  | (0042,0010) | Kidney Model    |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Encapsulated    | (0042,0011) | Byte stream     |                 |
   | Document        |             | representing    |                 |
   |                 |             | the OBJ file.   |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Source Instance | (0042,0013) | A sequence      |                 |
   | Sequence        |             | referencing CT1 |                 |
   |                 |             | source images   |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Model           | (0068,7001) | NO              |                 |
   | Modification    |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Model Mirroring | (0068,7002) | NO              |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Model Usage     | (0068,7003) |                 |                 |
   | Code Sequence   |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | %item           |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   |                 |             | (129013, DCM,   |                 |
   |                 |             | "Planning       |                 |
   |                 |             | Intent")        |                 |
   +-----------------+-------------+-----------------+-----------------+
   | %enditem        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Icon Image      | (0088,0200) | Sequence        | A pre-rendered  |
   | Sequence        |             | containing an   | view of the     |
   |                 |             | image           | model           |
   +-----------------+-------------+-----------------+-----------------+

Since the above OBJ file contains a reference to a materials library
(MTL) file, the MTL's contents must likewise be encapsulated in DICOM,
as shown in `table_title <#table_RRRR.2-2>`__.

.. table:: Encapsulated MTL Example A

   +-----------------+-------------+-----------------+-----------------+
   | Attribute Name  | Tag         | Example Value   | Comments        |
   +=================+=============+=================+=================+
   | SOP Instance    | (0008,0018) | 2.999.89235     | UID referenced  |
   | UID             |             | .5951.35894.751 | in the          |
   |                 |             |                 | Referenced      |
   |                 |             |                 | Instance        |
   |                 |             |                 | Sequence of the |
   |                 |             |                 | Encapsulated    |
   |                 |             |                 | OBJ object in   |
   |                 |             |                 | the table above |
   +-----------------+-------------+-----------------+-----------------+
   | ...             |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Modality        | (0008,0060) | M3D             |                 |
   +-----------------+-------------+-----------------+-----------------+
   | ...             |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Series          | (0008,103E) | Nephrectomy     |                 |
   | Description     |             | Planning Models |                 |
   +-----------------+-------------+-----------------+-----------------+
   | ...             |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Content Date    | (0008,0023) | 20170716        |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Content Time    | (0008,0033) | 13:00:34        |                 |
   +-----------------+-------------+-----------------+-----------------+
   | ...             |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Referenced      | (0008,1140) |                 |                 |
   | Image Sequence  |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | %item           |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Referenced    | (0008,1150) | 1.2.840.1000    | Multi-frame     |
   | SOP Class UID   |             | 8.5.1.4.1.1.7.4 | True Color      |
   |                 |             |                 | Secondary       |
   |                 |             |                 | Capture SOP     |
   |                 |             |                 | class           |
   +-----------------+-------------+-----------------+-----------------+
   | >>Referenced    | (0008,1155) | 2.999.89235     | UID reference   |
   | SOP Instance    |             | .5951.35894.841 | to texture      |
   | UID             |             |                 | image used for  |
   |                 |             |                 | normal kidney   |
   |                 |             |                 | tissue          |
   |                 |             |                 | (Multi-frame    |
   |                 |             |                 | True Color      |
   |                 |             |                 | Secondary       |
   |                 |             |                 | Capture         |
   |                 |             |                 | Instance)       |
   +-----------------+-------------+-----------------+-----------------+
   | >>Referenced    | (0008,1150) | 1.2.840.1000    | Multi-frame     |
   | SOP Class UID   |             | 8.5.1.4.1.1.7.4 | True Color      |
   |                 |             |                 | Secondary       |
   |                 |             |                 | Capture SOP     |
   |                 |             |                 | class           |
   +-----------------+-------------+-----------------+-----------------+
   | >>Relative URI  | (0068,7005) | "ntissue.png"   | Relative URI    |
   | Reference       |             |                 | that preserved  |
   | Within          |             |                 | the first       |
   | Encapsulated    |             |                 | texture map's   |
   | Document        |             |                 | original        |
   |                 |             |                 | filename as     |
   |                 |             |                 | referenced from |
   |                 |             |                 | within the MTL  |
   |                 |             |                 | file.           |
   +-----------------+-------------+-----------------+-----------------+
   | >>Referenced    | (0008,1155) | 2.999.89235     | UID reference   |
   | SOP Instance    |             | .5951.35894.842 | to texture      |
   | UID             |             |                 | image used for  |
   |                 |             |                 | diseased kidney |
   |                 |             |                 | tissue (Multi-  |
   |                 |             |                 | frame True      |
   |                 |             |                 | Color Secondary |
   |                 |             |                 | Capture         |
   |                 |             |                 | Instance)       |
   +-----------------+-------------+-----------------+-----------------+
   | >>Relative URI  | (0068,7005) | "distissue.png" | Relative URI    |
   | Reference       |             |                 | that preserved  |
   | Within          |             |                 | the second      |
   | Encapsulated    |             |                 | texture map's   |
   | Document        |             |                 | original        |
   |                 |             |                 | filename as     |
   |                 |             |                 | referenced from |
   |                 |             |                 | within the MTL  |
   |                 |             |                 | file.           |
   +-----------------+-------------+-----------------+-----------------+
   | >>Referenced    | (0008,1150) | 1.2.840.1000    | Multi-frame     |
   | SOP Class UID   |             | 8.5.1.4.1.1.7.4 | True Color      |
   |                 |             |                 | Secondary       |
   |                 |             |                 | Capture SOP     |
   |                 |             |                 | class           |
   +-----------------+-------------+-----------------+-----------------+
   | >>Referenced    | (0008,1155) | 2.999.89235     | UID reference   |
   | SOP Instance    |             | .5951.35894.843 | to texture      |
   | UID             |             |                 | image used for  |
   |                 |             |                 | fluid (Multi-   |
   |                 |             |                 | frame True      |
   |                 |             |                 | Color Secondary |
   |                 |             |                 | Capture         |
   |                 |             |                 | Instance)       |
   +-----------------+-------------+-----------------+-----------------+
   | >>Relative URI  | (0068,7005) | "fluid.jpg"     | Relative URI    |
   | Reference       |             |                 | that preserved  |
   | Within          |             |                 | the third       |
   | Encapsulated    |             |                 | texture map's   |
   | Document        |             |                 | original        |
   |                 |             |                 | filename as     |
   |                 |             |                 | referenced from |
   |                 |             |                 | within the MTL  |
   |                 |             |                 | file.           |
   +-----------------+-------------+-----------------+-----------------+
   | %enditem        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | ...             |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Patient Name    | (0010,0010) | Fr              |                 |
   |                 |             | anz-Lopez^Kevin |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Patient ID      | (0010,0020) | 547892459       |                 |
   +-----------------+-------------+-----------------+-----------------+
   | ...             |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | MIME Type of    | (0040,0012) | model/mtl       |                 |
   | Encapsulated    |             |                 |                 |
   | Document        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Document Title  | (0042,0010) | Kidney Model    |                 |
   |                 |             | Materials       |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Encapsulated    | (0042,0011) | Byte stream     |                 |
   | Document        |             | representing    |                 |
   |                 |             | the MTL file.   |                 |
   +-----------------+-------------+-----------------+-----------------+
   | ...             |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+

The example MTL file contains references to three texture images (see
Referenced Image Sequence above) and these likewise need to be encoded
in DICOM (if they are not natively DICOM). The Multi-frame True Color
Secondary Capture Instance is used to represent such texture images in
DICOM, regardless of the original format in which the texture map image
was stored.

In our example, the pixel data is read from the PNG files "ntissue.png"
and "distissue.png", and the JPEG file "fluid.jpg". Corresponding DICOM
Multi-Frame True Color Secondary capture images are created for each of
these texture maps, as is shown in `figure_title <#figure_RRRR.2-1>`__.
The original filenames are preserved in the URI Within Encapsulated
Document values within the Encapsulated MTL's Referenced Image Sequence.

An abbreviated version of the first of these three object's DICOM
headers is shown in `table_title <#table_RRRR.2-3>`__, focusing on how
these relate to use with an MTL Instance.

.. table:: Multi-frame True Color Secondary Capture Texture Map Example
A

   +----------------+-------------+---------------+------------------+
   | Attribute Name | Tag         | Example Value | Comments         |
   +================+=============+===============+==================+
   | ...            |             |               |                  |
   +----------------+-------------+---------------+------------------+
   | Modality       | (0008,0060) | TEXTUREMAP    | Indicates that   |
   |                |             |               | the image is a   |
   |                |             |               | texture map, and |
   |                |             |               | not some other   |
   |                |             |               | image taken of   |
   |                |             |               | the patient      |
   +----------------+-------------+---------------+------------------+
   | ...            |             |               |                  |
   +----------------+-------------+---------------+------------------+

It is important to note that when de-encapsulating MTL file, the texture
map images must be restored to both their original file name and file
format (as indicated by the corresponding URI Within Encapsulated
Document attribute values contained in the Encapsulated MTL instance
that references the texture map images. This is done so that the file
name references inside the MTL, which will be read by downstream
OBJ-capable software, will still be valid. Thus, in our example, our
first texture map DICOM image must be converted back into a PNG (as
indicated by the file extension in Relative URI Reference Within
Encapsulated Document value) and saved to the file system as
"ntissue.png" in the same location as the OBJ and MTL files.

The two other texture map images would be encoded in a manner like the
one above.

.. _sect_RRRR.3:

Manufacturing Model Grouping, Color & Opacity
---------------------------------------------

This example explains how to group manufacturing models together to
indicate that they are intended to be assembled into a single unit
(either after production, or as part of production on a multi-material
printer). As shown in `figure_title <#figure_RRRR.3-1>`__, a group of
models can include a mix of both STL and OBJ encapsulations
(CardiacAnatomy.obj, ThoracicSkeleton.obj, and Thyroid.stl). All that is
required to indicate grouping is that the Model Group UID (0068,7004) be
set to the same UID value for all objects in the group. In this example
the optional material file was not needed by the OBJ.

It is possible to specify preferred color and opacity of Manufacturing
3D Models using Recommended Display CIELab Value (0062,000D) and
Recommended Presentation Opacity (0066,000C). One particular use of
these attributes is in combination with model grouping, as it allows the
use of non-opaque materials to allow viewing of interior parts of the
grouped assembly. An example of such use is shown in
`figure_title <#figure_RRRR.3-2>`__, where the AorticCalcifications.obj
model is intended to be assembled inside the Aorta.stl model. Therefore,
the DICOM Encapsulated STL of the aorta is designated as having a
recommended presentation of semi-transparent red, while DICOM
Encapsulated OBJ of the calcifications is fully opaque white.

