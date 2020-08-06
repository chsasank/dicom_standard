.. _chapter_B:

1024 X-Ray Angiographic Application Profile (Normative)
=======================================================

.. _sect_B.1:

Class and Profile Identification
--------------------------------

This Annex defines a class of Application Profiles for 1024 X-Ray
Angiographic clinical applications. The identifier for this class shall
be STD-XA1K. It is the intent of these profiles to be backward
compatible with the Basic Cardiac X-Ray Angiographic Application Profile
(STD-XABC-CD) in `Basic Cardiac X-Ray Angiographic Application Profile
(Normative) <#chapter_A>`__.

The specific Application Profiles in this class are shown in the
`table_title <#table_B.1-1>`__.

.. table:: 1024 X-Ray Angiographic Profiles

   +-------------------------+----------------+-------------------------+
   | **Application Profile** | **Identifier** | **Description**         |
   +=========================+================+=========================+
   | 1024 X-Ray Angiographic | STD-XA1K-CD    | It handles single frame |
   | Studies on CD-R Media   |                | or multi-frame X-Ray    |
   |                         |                | digital images up to    |
   |                         |                | 1024x1024x12 bits;      |
   |                         |                | biplane acquisitions    |
   |                         |                | are encoded as two      |
   |                         |                | single plane            |
   |                         |                | information objects.    |
   |                         |                | Secondary Capture       |
   |                         |                | images are supported.   |
   +-------------------------+----------------+-------------------------+
   | 1024 X-Ray Angiographic | STD-XA1K-DVD   | It handles single frame |
   | Studies on DVD Media    |                | or multi-frame X-Ray    |
   |                         |                | digital images up to    |
   |                         |                | 1024x1024x12 bits;      |
   |                         |                | biplane acquisitions    |
   |                         |                | are encoded as two      |
   |                         |                | single plane            |
   |                         |                | information objects.    |
   |                         |                | Secondary Capture       |
   |                         |                | images are supported.   |
   +-------------------------+----------------+-------------------------+

.. _sect_B.2:

Clinical Context
----------------

This class of Application Profiles facilitates the interchange of
primary digital X-Ray cine runs, typically acquired as part of
angiographic procedures. Typical media interchanges would be from in-lab
acquisition equipment to either a display workstation or to a data
archive system, or between a display workstation and a data archive
system (in both directions).

Additionally, images derived from or related to primary digital X-Ray
cine runs, such as quantitative analysis images, reference images,
multi-modality images and screen capture images, may be interchanged via
this Profile.

The operational use of the media interchange is potentially both
intra-institutional and inter-institutional.

.. note::

   An FSC conforming to the Basic 512 Cardiac Angiographic Profile and
   General Purpose CD-R Profile supporting the SC Image Media Storage
   SOP Class could, if the restrictions in this profile were observed,
   create images that were readable by an FSR supporting the profile.
   Conversely, SC Images written by an FSC conforming to this profile,
   would be readable by an FSR conforming to the Basic 512 Cardiac
   Angiographic Profile and the General Purpose CD-R Profile supporting
   the SC Image Media Storage SOP Class.

.. _sect_B.2.1:

Roles and Service Class Options
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This Application Profile Class uses the Media Storage Service Class
defined in .

The Application Entity shall support one or more of the roles of
File-set Creator, File-set Reader, and File-set Updater, defined in .

.. _sect_B.2.1.1:

File Set Creator
^^^^^^^^^^^^^^^^

The Application entity acting as a File-Set Creator generates a File Set
under the STD-XA1K Application Profile Class. Typical entities using
this role would include X-Ray angiographic lab equipment, and archive
systems that generate a patient record for transfer to another
institution. File Set Creators shall be able to generate the Basic
Directory SOP Class in the DICOMDIR File with all types of Directory
Records related to the SOP Classes stored in the File-set.

An FSC shall offer the ability to either finalize the disc at the
completion of the most recent write session (no additional information
can be subsequently added to the disc) or to allow multi-session
(additional information may be subsequently added to the disc). An FSC
may allow packet-writing if supported by the media and file system
specified in the profile.

.. note::

   A multiple volume (a logical volume that can cross multiple physical
   media) is not supported by this Application Profile Class. If a set
   of Files, e.g., a Study, cannot be written entirely on one piece of
   media, the FSC will create multiple independent DICOM File-sets such
   that each File-set can reside on a single piece of media controlled
   by its individual DICOMDIR file. The user of the FSC can opt to use
   written labels on the discs to reflect that there is more than one
   disc for this set of files (e.g., a Study).

.. _sect_B.2.1.2:

File Set Reader
^^^^^^^^^^^^^^^

The role of File Set Reader shall be used by Application Entities that
receive a transferred File Set. Typical entities using this role would
include display workstations, and archive systems that receive a patient
record transferred from another institution. File Set Readers shall be
able to read all the defined SOP Instances defined for the specific
Application Profiles to which a conformance claim is made, using all the
defined Transfer Syntaxes.

.. _sect_B.2.1.3:

File Set Updater
^^^^^^^^^^^^^^^^

The role of File Set Updater shall be used by Application Entities that
receive a transferred File Set and update it by the addition of
processed information. Typical entities using this role would include
analytic workstations, which for instance may add to the File Set an
information object containing a processed (e.g., edge-enhanced) image
frame. Stations that update patient information objects would also use
this role. File-set Updaters shall be able to read and update the
DICOMDIR file. File-set Updaters do not have to read the image
information object. File-set Updaters shall be able to generate one or
more of the SOP Instances defined for the specific Application Profiles
to which a conformance claim is made, and to read and update the
DICOMDIR file.

An FSU shall offer the ability to either finalize the disc at the
completion of the most recent write session (no additional information
can be subsequently added to the disc) or to allow multi-session
(additional information may be subsequently added to the disc).

.. note::

   If the disc has not been finalized, the File-set Updater will be able
   to update information assuming there is enough space on the disc to
   write a new DICOMDIR file, the information, and the fundamental
   volume control structures. Volume control structures are the
   structures that are inherent to the standards of the physical volume;
   see

The FSU role is not defined for the STD-XA1K-DVD profile.

.. _sect_B.3:

STD-XA1K Application Profile Class Requirements
-----------------------------------------------

.. _sect_B.3.1:

SOP Classes and Transfer Syntaxes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This Application Profile Class is based on the Media Storage Service
Class (see ).

SOP Classes and corresponding Transfer Syntaxes supported by this
Application Profile are specified in `table_title <#table_B.3-1>`__.

.. table:: STD-XA1K SOP Classes and Transfer Syntaxes

   +----------+----------+----------+----------+----------+----------+
   | **Inf    | **SOP    | **       | **FSC    | **FSR    | **FSU    |
   | ormation | Class    | Transfer | Requi    | Requi    | Req      |
   | Object   | UID**    | Syntax   | rement** | rement** | uirement |
   | Defi     |          | and      |          |          | (see     |
   | nition** |          | UID**    |          |          | Note     |
   |          |          |          |          |          | 1)**     |
   +==========+==========+==========+==========+==========+==========+
   | Basic    | 1.2.     | Explicit | M        | M        | M        |
   | D        | 840.1000 | VR       | andatory | andatory | andatory |
   | irectory | 8.1.3.10 | Little   |          |          |          |
   |          |          | Endian   |          |          |          |
   |          |          | Unco     |          |          |          |
   |          |          | mpressed |          |          |          |
   |          |          |          |          |          |          |
   |          |          | 1.2      |          |          |          |
   |          |          | .840.100 |          |          |          |
   |          |          | 08.1.2.1 |          |          |          |
   +----------+----------+----------+----------+----------+----------+
   | X-Ray    | 1.2.     | JPEG     | M        | M        | Optional |
   | Angi     | 840.1000 | Lossless | andatory | andatory |          |
   | ographic | 8.5.1.4. | Process  |          |          |          |
   | Image    | 1.1.12.1 | 14       |          |          |          |
   |          |          | (s       |          |          |          |
   |          |          | election |          |          |          |
   |          |          | value 1) |          |          |          |
   |          |          |          |          |          |          |
   |          |          | 1.2.84   |          |          |          |
   |          |          | 0.10008. |          |          |          |
   |          |          | 1.2.4.70 |          |          |          |
   +----------+----------+----------+----------+----------+----------+
   | X-Ray    | 1.2.     | JPEG     | Optional | M        | U        |
   | Angi     | 840.1000 | Lossy,   | for DVD; | andatory | ndefined |
   | ographic | 8.5.1.4. | Baseline | Di       | for DVD; | for DVD; |
   | Image    | 1.1.12.1 | Se       | sallowed | Di       | Di       |
   |          |          | quential | for CD   | sallowed | sallowed |
   |          |          | with     |          | for CD   | for CD   |
   |          |          | Huffman  |          |          |          |
   |          |          | Coding   |          |          |          |
   |          |          | (Process |          |          |          |
   |          |          | 1)       |          |          |          |
   |          |          |          |          |          |          |
   |          |          | 1.2.84   |          |          |          |
   |          |          | 0.10008. |          |          |          |
   |          |          | 1.2.4.50 |          |          |          |
   +----------+----------+----------+----------+----------+----------+
   | X-Ray    | 1.2.     | JPEG     | Optional | M        | U        |
   | Angi     | 840.1000 | Extended | for DVD; | andatory | ndefined |
   | ographic | 8.5.1.4. | (Process | Di       | for DVD; | for DVD; |
   | Image    | 1.1.12.1 | 2 & 4):  | sallowed | Di       | Di       |
   |          |          |          | for CD   | sallowed | sallowed |
   |          |          | Default  |          | for CD   | for CD   |
   |          |          | Transfer |          |          |          |
   |          |          | Syntax   |          |          |          |
   |          |          | for      |          |          |          |
   |          |          | Lossy    |          |          |          |
   |          |          | JPEG 12  |          |          |          |
   |          |          | Bit      |          |          |          |
   |          |          | Image    |          |          |          |
   |          |          | Com      |          |          |          |
   |          |          | pression |          |          |          |
   |          |          | (Process |          |          |          |
   |          |          | 4 only)  |          |          |          |
   |          |          |          |          |          |          |
   |          |          | 1.2.84   |          |          |          |
   |          |          | 0.10008. |          |          |          |
   |          |          | 1.2.4.51 |          |          |          |
   +----------+----------+----------+----------+----------+----------+
   | S        | 1        | Explicit | Optional | M        | Optional |
   | econdary | .2.840.1 | VR       |          | andatory |          |
   | Capture  | 0008.5.1 | Little   |          |          |          |
   | Image    | .4.1.1.7 | Endian   |          |          |          |
   | Storage  |          | Unco     |          |          |          |
   |          |          | mpressed |          |          |          |
   |          |          |          |          |          |          |
   |          |          | 1.2      |          |          |          |
   |          |          | .840.100 |          |          |          |
   |          |          | 08.1.2.1 |          |          |          |
   +----------+----------+----------+----------+----------+----------+
   | G        | 1.2.     | Explicit | Optional | Optional | Optional |
   | rayscale | 840.1000 | VR       |          |          |          |
   | Softcopy | 8.5.1.4. | Little   |          |          |          |
   | Pres     | 1.1.11.1 | Endian   |          |          |          |
   | entation |          | Unco     |          |          |          |
   | State    |          | mpressed |          |          |          |
   | Storage  |          |          |          |          |          |
   |          |          | 1.2      |          |          |          |
   |          |          | .840.100 |          |          |          |
   |          |          | 08.1.2.1 |          |          |          |
   +----------+----------+----------+----------+----------+----------+

.. note::

   1. The FSU requirement is not defined for STD-XA1K-DVD profile.

   2. The Standalone Overlay, Standalone Curve and Detached Patient
      management SOP Classes were formerly defined in these profiles,
      but have been retired. The Grayscale Softcopy Presentation State
      Storage SOP Class has been added as the preferred mechanism for
      conveying annotations.

.. _sect_B.3.2:

Physical Media and Media Formats
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The 1024 X-Ray Angiographic Application CD-R Profile STD-XA1K-CD
requires the 120mm CD-R physical media with the ISO/IEC 9660 Media
Format, as defined in .

The 1024 X-Ray Angiographic Application DVD profile STD-XA1K-DVD
requires any of the 120 mm DVD media other than DVD-RAM as defined in .

.. _sect_B.3.3:

Directory Information in DICOMDIR
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Conformant Application Entities shall include in the DICOMDIR File a
Basic Directory IOD containing Directory Records at the Patient and
subsidiary levels appropriate to the SOP Classes in the File-set.

.. note::

   DICOMDIRs with no directory information are not allowed by this
   Application Profile.

.. _sect_B.3.3.1:

Additional Keys
^^^^^^^^^^^^^^^

`table_title <#table_B.3-2>`__ specifies the type of Directory Records
that shall be supported and the additional associated keys. Refer to the
Basic Directory IOD in .

.. table:: STD-XA1K Additional DICOMDIR Keys

   +-------------+-------------+-------------+----------+-------------+
   | **Key       | **Tag**     | **Directory | **Type** | **Notes**   |
   | Attribute** |             | Record      |          |             |
   |             |             | Type**      |          |             |
   +=============+=============+=============+==========+=============+
   | Patient's   | (0010,0030) | PATIENT     | 2        |             |
   | Birth Date  |             |             |          |             |
   +-------------+-------------+-------------+----------+-------------+
   | Patient's   | (0010,0040) | PATIENT     | 2        |             |
   | Sex         |             |             |          |             |
   +-------------+-------------+-------------+----------+-------------+
   | Institution | (0008,0080) | SERIES      | 2        |             |
   | Name        |             |             |          |             |
   +-------------+-------------+-------------+----------+-------------+
   | Institution | (0008,0081) | SERIES      | 2        |             |
   | Address     |             |             |          |             |
   +-------------+-------------+-------------+----------+-------------+
   | Performing  | (0008,1050) | SERIES      | 2        |             |
   | Physicians' |             |             |          |             |
   | Name        |             |             |          |             |
   +-------------+-------------+-------------+----------+-------------+
   | Icon Image  | (0088,0200) | IMAGE       | 1        |             |
   | Sequence    |             |             |          |             |
   +-------------+-------------+-------------+----------+-------------+
   | Image Type  | (0008,0008) | IMAGE       | 1C       | Required if |
   |             |             |             |          | the SOP     |
   |             |             |             |          | Instance    |
   |             |             |             |          | referenced  |
   |             |             |             |          | by the      |
   |             |             |             |          | Directory   |
   |             |             |             |          | Record is   |
   |             |             |             |          | an XA       |
   |             |             |             |          | Image.      |
   +-------------+-------------+-------------+----------+-------------+
   | Calibration | (0050,0004) | IMAGE       | 2        |             |
   | Image       |             |             |          |             |
   +-------------+-------------+-------------+----------+-------------+
   | Referenced  | (0008,1140) | IMAGE       | 1C       | Required if |
   | Image       |             |             |          | the SOP     |
   | Sequence    |             |             |          | Instance    |
   |             |             |             |          | referenced  |
   |             |             |             |          | by the      |
   |             |             |             |          | Directory   |
   |             |             |             |          | Record is   |
   |             |             |             |          | an XA Image |
   |             |             |             |          | and has an  |
   |             |             |             |          | Image Type  |
   |             |             |             |          | (0008,0008) |
   |             |             |             |          | value 3 of  |
   |             |             |             |          | BIPLANE A   |
   |             |             |             |          | or BIPLANE  |
   |             |             |             |          | B. May be   |
   |             |             |             |          | present     |
   |             |             |             |          | otherwise.  |
   +-------------+-------------+-------------+----------+-------------+
   | >Referenced | (0008,1150) | IMAGE       | 1C       | Required if |
   | SOP Class   |             |             |          | Referenced  |
   | UID         |             |             |          | Image       |
   |             |             |             |          | Sequence    |
   |             |             |             |          | (0008,1140) |
   |             |             |             |          | is present  |
   +-------------+-------------+-------------+----------+-------------+
   | >Referenced | (0008,1155) | IMAGE       | 1C       | Required if |
   | SOP         |             |             |          | Referenced  |
   | Instance    |             |             |          | Image       |
   | UID         |             |             |          | Sequence    |
   |             |             |             |          | (0008,1140) |
   |             |             |             |          | is present  |
   +-------------+-------------+-------------+----------+-------------+
   | *>All other | IMAGE       | 3           |          |             |
   | elements    |             |             |          |             |
   | from        |             |             |          |             |
   | Referenced  |             |             |          |             |
   | Image       |             |             |          |             |
   | Sequence    |             |             |          |             |
   | (including  |             |             |          |             |
   | Purpose of  |             |             |          |             |
   | Reference   |             |             |          |             |
   | Code        |             |             |          |             |
   | Sequence    |             |             |          |             |
   | and its     |             |             |          |             |
   | content)*   |             |             |          |             |
   +-------------+-------------+-------------+----------+-------------+
   | Lossy image | (0028,2112) | IMAGE       | 1C       | Required if |
   | Compression |             |             |          | present in  |
   | Ratio       |             |             |          | image       |
   |             |             |             |          | object with |
   |             |             |             |          | a non-zero  |
   |             |             |             |          | length      |
   |             |             |             |          | value.      |
   +-------------+-------------+-------------+----------+-------------+

.. _sect_B.3.3.2:

Icon Images
^^^^^^^^^^^

Directory Records of type IMAGE shall include Icon Images. The icon
pixel data shall be Bits Allocated and Bits Stored (0028,0101) attribute
values of 8 with Row (0028,0010) and Column (0028,0011) attribute values
of 128 and Photometric Interpretation (0028,0004) attribute value of
MONOCHROME2.

.. note::

   1. It is recommended that the Icon Images be encoding using VR OB
      encoding. The use of OW, allowed by the STD-XABC-CD Basic Cardiac
      profile defined in `Basic Cardiac X-Ray Angiographic Application
      Profile (Normative) <#chapter_A>`__, is deprecated, and may be
      retired in future editions of the Standard.

   2. This icon size is larger than that recommended in because the
      64x64 icon would not be clinically useful for identifying and
      selecting X-Ray angiographic images.

   3. For multi-frame images, it is recommended that the icon image be
      derived from the frame identified in the Representative Frame
      Number attribute (0028,6010), if defined for the image SOP
      Instance. If the Representative Frame Number is not present, a
      frame approximately one-third of the way through the multi-frame
      image should be selected. The process to reduce any image to a
      128x128 image is beyond the scope of this Standard.

.. _sect_B.3.4:

Other Parameters
~~~~~~~~~~~~~~~~

This section defines other parameters common to all specific Application
Profiles in the STD-XA1K class that need to be specified in order to
ensure interoperable media interchange.

.. _sect_B.3.4.1:

Image Attribute Values
^^^^^^^^^^^^^^^^^^^^^^

The attributes listed in `table_title <#table_B.3-3>`__ used within the
X-Ray Angiographic Image files have the specified values.

.. table:: STD-XA1K Required XA Image Attribute Values

   ============= =========== =======================
   **Attribute** **Tag**     **Value**
   ============= =========== =======================
   Modality      (0008,0060) XA
   Rows          (0028,0010) up to 1024 (see below)
   Columns       (0028,0011) up to 1024 (see below)
   Bits Stored   (0028,0101) 8, 10, and 12 bits only
   ============= =========== =======================

.. note::

   1. An FSC or FSU, when creating or updating a File-set, Rows or
      Columns will not exceed a value of 1024. When reading a File-set,
      an FSR or FSU will accept all values of up to 1024 for Rows or
      Columns.

   2. Photometric Interpretation, Pixel Representation, High Bit, Bits
      Allocated and Samples per Pixel are defined in the XA IOD.

The attributes listed in `table_title <#table_B.3-4>`__ used within the
Secondary Capture Image files have the specified values.

.. table:: STD-XA1K Required SC Image Attribute Values

   ========================== =========== ======================
   **Attribute**              **Tag**     **Value**
   ========================== =========== ======================
   Rows                       (0028,0010) up to 1024 (see below)
   Columns                    (0028,0011) up to 1024 (see below)
   Samples per Pixel          (0028,0002) 1
   Photometric Interpretation (0028,0004) MONOCHROME2
   Bits Allocated             (0028,0100) 8 bits only
   Bits Stored                (0028,0101) 8 bits only
   High Bit                   (0028,0102) 7
   Pixel Representation       (0028,0103) 0000H (unsigned)
   ========================== =========== ======================

.. note::

   1. An FSC or FSU, when creating or updating a File-set, Rows or
      Columns will not exceed a value of 1024. When reading a File-set,
      an FSR or FSU will accept all values of up to 1024 for Rows or
      Columns.

   2. It is recommend that Referenced Image Sequence (0008,1140) be
      present if the SC Image is significantly related to XA images and
      frames stored on the same media, and if present, it should contain
      references to those images and frames.

Overlay Group 60XX shall not be present in Secondary Capture Images, and
Standalone Overlays shall not be referenced by or to Secondary Capture
Images used in this profile.

.. _sect_B.3.4.2:

Multi-frame JPEG Format
^^^^^^^^^^^^^^^^^^^^^^^

The JPEG encoding of pixel data shall use Interchange Format (with table
specification) for all frames.

.. _sect_B.3.4.3:

Attribute Value Precedence
^^^^^^^^^^^^^^^^^^^^^^^^^^

Retired.

