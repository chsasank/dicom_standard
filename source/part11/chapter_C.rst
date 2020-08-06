.. _chapter_C:

Ultrasound Application Profile (Normative)
==========================================

.. _sect_C.1:

Class and Profile Identification
--------------------------------

This Annex defines Application Profiles for Ultrasound Media Storage
applications. Each Application Profile has a unique identifier used for
conformance claims. Due to the variety of clinical applications of
storage media in Ultrasound, a family of application profiles are
described in this section to best tailor an application choice to the
specific needs of the user. The identifier used to describe each profile
is broken down into three parts: a prefix, mid-section, and suffix. The
prefix describes the overall Application Profile Class and is common for
all ultrasound application profiles. The mid section describes the
specific clinical application of the profile. The suffix is used to
describe the actual media choice the profile will use.

The prefix for this class of application profiles is identified with the
STD-US identifier.

.. note::

   Conformance Statements may use the earlier prefix of APL that is
   equivalent to STD. This use is deprecated and may be retired in
   future editions of the Standard.

The midsection is broken down into three subclasses that describe the
clinical use of the data. These subclasses are: Image Display (ID
identifier), Spatial Calibration (SC identifier), and Combined
Calibration (CC identifier). All three subclasses can be applied to
either single frames (SF) images or single and multi-frames (MF) images.
The SC subclass enhances the ID class by adding the requirement for
region specific spatial calibration data with each IOD. The CC subclass
enhances the SC subclass by requiring region specific pixel component
calibration.

The suffix, xxxx, is used to describe the actual media choice used for
the conformance claim. Any of the above mentioned classes can be stored
onto one of eight pieces of media described in the
`table_title <#table_C.3-3>`__.

The specific Application Profiles are shown in the following table.

.. table:: Ultrasound Application Profile identifiers

   ======================= ================= ========================
   **Application Profile** **Single Frame**  **Single & Multi-Frame**
   ======================= ================= ========================
   Image Display           STD-US-ID-SF-xxxx STD-US-ID-MF-xxxx
   Spatial Calibration     STD-US-SC-SF-xxxx STD-US-SC-MF-xxxx
   Combined Calibration    STD-US-CC-SF-xxxx STD-US-CC-MF-xxxx
   ======================= ================= ========================

The ID Application Profile Classes are intended to be used for the
transfer of ultrasound images for display purposes.

The SC Application Profile Classes are intended to be used for the
transfer of ultrasound images with spatial calibration data for
quantitative purposes (see `Spatial Calibration (SC) Class
Requirements <#sect_C.4>`__).

The CC Application Profile Classes are intended to be used for the
transfer of ultrasound images with spatial and pixel component
calibration data for more advanced quantitative purposes (see `Combined
Calibration (CC) Class Requirements <#sect_C.5>`__).

.. _sect_C.2:

Clinical Context
----------------

These classes of Application Profiles facilitate the interchange of
ultrasound data on media. Typical interchanges would be between
ultrasound systems, between an ultrasound system and a display
workstation, between display workstations, or between an ultrasound
system and a data archive. This context is shown in
`figure_title <#figure_C.2-1>`__.

The operational use of the media transfer is potentially both
intra-institutional and inter-institutional.

.. _sect_C.2.1:

Roles
~~~~~

.. _sect_C.2.1.1:

File Set Creator
^^^^^^^^^^^^^^^^

The role of File Set Creator shall be used by Application Entities that
generate a File Set under the STD-US class of Application Profiles.
Typical entities using this role would include ultrasound imaging
equipment, workstations, and archive systems that generate a patient
record for transfer. File Set Creators shall be able to generate the
DICOMDIR directory file, single and/or multi frame Ultrasound
Information Object files, and depending on the subclass, region specific
calibration in the defined Transfer Syntaxes.

An FSC shall offer the ability to either finalize the disc at the
completion of the most recent write session (no additional information
can be subsequently added to the disc) or to allow multi-session
(additional information may be subsequently added to the disc) or to
allow packet-writing, if supported by the media and file system
specified in the profile.

.. _sect_C.2.1.2:

File Set Reader
^^^^^^^^^^^^^^^

The role of File Set Reader shall be used by Application Entities that
receive a transferred File Set. Typical entities using this role would
include ultrasound systems, display workstations, and archive systems
that receive a patient record from a piece of media. File Set Readers
shall be able to read the DICOMDIR directory file and all Information
Objects defined for the specific Application Profiles, using the defined
Transfer Syntaxes.

.. _sect_C.2.1.3:

File Set Updater
^^^^^^^^^^^^^^^^

The role of File Set Updater shall be used by Application Entities that
receive a transferred File Set and updates it by the addition or
deletion of objects to the media. Typical entities using this role would
include ultrasound systems adding new patient records to the media and
workstations that may add an information object containing a processed
or modified image.

An FSU shall offer the ability to either finalize the disc at the
completion of the most recent write session (no additional information
can be subsequently added to the disc) or to allow multi-session
(additional information may be subsequently added to the disc) or to
allow packet-writing, if supported by the media and file system
specified in the profile.

The FSU role is not defined for the STD-US-xx-xx-DVD profiles (i.e., for
DVD media that is not DVD-RAM).

.. _sect_C.3:

General Class Profile
---------------------

.. _sect_C.3.1:

Abstract and Transfer Syntaxes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Application Profiles in this class, STD-US, shall support the
appropriate Information Object Definitions (IOD) and Transfer Syntaxes
for the Media Storage SOP Class in the following table. In the role of
FS-Updater or FS-Creator the application can choose one of the three
possible transfer Syntaxes to create an IOD. In the role of FS-Reader an
application shall support all transfer Syntaxes defined for the STD-US
application profile.

.. table:: Ultrasound SOP Classes and Transfer Syntaxes

   +----------------+----------------+----------------+----------------+
   | **Information  | **SOP Class    | **Transfer     | **Transfer     |
   | Object         | UID**          | Syntax**       | Syntax UID**   |
   | Definition**   |                |                |                |
   +================+================+================+================+
   | DICOM Media    | 1.2.84         | Explicit VR    | 1.2.8          |
   | Storage        | 0.10008.1.3.10 | Little Endian  | 40.10008.1.2.1 |
   | Directory      |                | Uncompressed   | (see )         |
   +----------------+----------------+----------------+----------------+
   | Ultrasound     | 1.2.840.10008  | Explicit VR    | 1.2.8          |
   | Image Storage  | .5.1.4.1.1.6.1 | Little Endian  | 40.10008.1.2.1 |
   |                |                | Uncompressed   |                |
   +----------------+----------------+----------------+----------------+
   | Ultrasound     | 1.2.840.10008  | RLE Lossless   | 1.2.8          |
   | Image Storage  | .5.1.4.1.1.6.1 | Image          | 40.10008.1.2.5 |
   |                |                | Compression    |                |
   +----------------+----------------+----------------+----------------+
   | Ultrasound     | 1.2.840.10008  | JPEG Lossy,    | 1.2.840.       |
   | Image Storage  | .5.1.4.1.1.6.1 | Baseline       | 10008.1.2.4.50 |
   |                |                | Sequential     |                |
   |                |                | with Huffman   |                |
   |                |                | Coding         |                |
   |                |                | (Process 1)    |                |
   +----------------+----------------+----------------+----------------+
   | Ultrasound     | 1.2.840.10008  | Explicit VR    | 1.2.8          |
   | Multi-frame    | .5.1.4.1.1.3.1 | Little Endian  | 40.10008.1.2.1 |
   | Image Storage  |                | Uncompressed   |                |
   +----------------+----------------+----------------+----------------+
   | Ultrasound     | 1.2.840.10008  | RLE Lossless   | 1.2.8          |
   | Multi-frame    | .5.1.4.1.1.3.1 | Image          | 40.10008.1.2.5 |
   | Image Storage  |                | Compression    |                |
   +----------------+----------------+----------------+----------------+
   | Ultrasound     | 1.2.840.10008  | JPEG Lossy,    | 1.2.840.       |
   | Multi-frame    | .5.1.4.1.1.3.1 | Baseline       | 10008.1.2.4.50 |
   | Image Storage  |                | Sequential     |                |
   |                |                | with Huffman   |                |
   |                |                | Coding         |                |
   |                |                | (Process 1)    |                |
   +----------------+----------------+----------------+----------------+

.. _sect_C.3.1.1:

Ultrasound Single and Multi-frame Pixel Formats Supported
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The STD-US application profile requires that all ultrasound image
objects only be stored using the values described in US Image Module and
the specializations used for the Ultrasound Single and Multi-Frame IODs.

In the role of FS-Updater or FS-Creator the application can choose any
of the supported Photometric Interpretations described in US Image
Module to create an IOD. In the role of FS-Reader, an application shall
support all Photometric Interpretations described in US Image Module.

`table_title <#table_C.3-2>`__ describes restrictions on the use of
various Transfer Syntaxes with the supported Photometric Interpretations
for both single and multi-frame images.

.. table:: Defined Photometric Interpretation and Transfer Syntax Pairs

   +----------------------+----------------------+----------------------+
   | **Photometric        | **Transfer Syntax**  | **Transfer Syntax    |
   | Interpretation       |                      | UID**                |
   | Value**              |                      |                      |
   +======================+======================+======================+
   | MONOCHROME2          | Uncompressed         | 1.2.840.10008.1.2.1  |
   |                      |                      |                      |
   |                      | RLE Lossless Image   | 1.2.840.10008.1.2.5  |
   |                      | Compression          |                      |
   +----------------------+----------------------+----------------------+
   | RGB                  | Uncompressed         | 1.2.840.10008.1.2.1  |
   |                      |                      |                      |
   |                      | RLE Lossless Image   | 1.2.840.10008.1.2.5  |
   |                      | Compression          |                      |
   +----------------------+----------------------+----------------------+
   | PALETTE COLOR        | Uncompressed         | 1.2.840.10008.1.2.1  |
   |                      |                      |                      |
   |                      | RLE Lossless Image   | 1.2.840.10008.1.2.5  |
   |                      | Compression          |                      |
   +----------------------+----------------------+----------------------+
   | YBR_FULL             | RLE Lossless Image   | 1.2.840.10008.1.2.5  |
   |                      | Compression          |                      |
   +----------------------+----------------------+----------------------+
   | YBR_FULL_422         | Uncompressed         | 1.2.840.10008.1.2.1  |
   |                      |                      |                      |
   |                      | JPEG Lossy           | 1.                   |
   |                      |                      | 2.840.10008.1.2.4.50 |
   +----------------------+----------------------+----------------------+

.. _sect_C.3.2:

Physical Media and Media Formats
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

An ultrasound application profile class may be supported by any one of
the media described in `table_title <#table_C.3-3>`__.

.. table:: Media Classes

   ============== ================= ====================================
   **Media**      **Media Classes** **Media Format**                     
   ============== ================= ====================================
   2.3GB 90mm MOD MOD23-90          DOS, unpartitioned (removable media) 
   CD-R           CDR               ISO/IEC 9660                         
   DVD-RAM        DVD-RAM           UDF1.5                               
   120 mm DVD     DVD               UDF or ISO 9660                      
   ============== ================= ====================================

.. note::

   Media Classes FLOP, MOD128, MOD230, MOD540, MOD640, MOD650, MOD12 AND
   MOD23 were previously defined but have been retired. See PS3.11 2004.

.. _sect_C.3.3:

DICOMDIR
~~~~~~~~

The Directory shall include Directory Records of PATIENT, STUDY, SERIES,
IMAGE corresponding to the information object files in the File Set. All
DICOM files in the File Set incorporating SOP Instances (Information
Objects) defined for the specific Application Profile shall be
referenced by Directory Records. At the image level each file contains a
single ultrasound image object or a single ultrasound multi-frame image
object as defined in of the Standard.

.. note::

   For all media selected in this Application Profile Class, STD-US, the
   following applies as defined in .

All implementations should include the DICOM Media Storage Directory in
the DICOMDIR file. There should only be one DICOMDIR file on a single
media. The DICOMDIR file should be found in the root directory of the
media. For the case of double-sided MOD media, there shall be a DICOMDIR
on each side of the media.

On a single media the patient ID key at the patient level shall be
unique for each patient directory record.

.. _sect_C.3.3.1:

Additional Keys
^^^^^^^^^^^^^^^

File Set Creators and Updaters are only required to generate mandatory
elements specified in . At each directory record level any additional
data elements can be added as keys, but is not required by File Set
Readers to be able to use them as keys.

.. _sect_C.3.3.2:

File Component IDs
^^^^^^^^^^^^^^^^^^

.. note::

   File Component IDs should be created using a random number filename
   to minimize File Component ID collisions as described in . The
   FS-Updater should check the existence of a Component ID prior to
   creating that ID. Should an ID collision occur, the FS-Updater should
   try another ID.

.. _sect_C.4:

Spatial Calibration (SC) Class Requirements
-------------------------------------------

All implementations conforming to the Application Profile Class SC shall
include the US Region Calibration Module with the exception of pixel
component organization data element (0018,6044) and other data elements
that are conditional on that data element.

.. _sect_C.5:

Combined Calibration (CC) Class Requirements
--------------------------------------------

All implementations conforming to the Application Profile Class CC shall
include the US Region Calibration Module including the pixel component
organization data element (0018,6044) and other data elements that are
conditional on that data element.

