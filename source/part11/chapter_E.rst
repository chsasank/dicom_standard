.. _chapter_E:

CT and MR Image Application Profiles (Normative)
================================================

.. _sect_E.1:

Profile Identification
----------------------

This Annex defines Application Profiles for Computed Tomography and
Magnetic Resonance Imaging interchange and storage on high capacity
rewritable magneto-optical disks (MOD) and CD-R and DVD-RAM and other
DVD media uncompressed and with lossless compression.

.. table:: STD-CTMR Profiles

   +------------------------+------------------+------------------------+
   | **Application          | **Identifier**   | **Description**        |
   | Profile**              |                  |                        |
   +========================+==================+========================+
   | CT/MR Studies on 4.1GB | STD-CTMR-MOD41   | Handles single frame   |
   | MOD                    |                  | 8, 12 or 16 bit        |
   |                        |                  | grayscale and 8 bit    |
   |                        |                  | palette color,         |
   |                        |                  | uncompressed and       |
   |                        |                  | lossless compressed    |
   |                        |                  | images.                |
   +------------------------+------------------+------------------------+
   | CT/MR Studies on CD-R  | STD-CTMR-CD      | Handles single frame   |
   |                        |                  | 8, 12 or 16 bit        |
   |                        |                  | grayscale and 8 bit    |
   |                        |                  | palette color,         |
   |                        |                  | uncompressed and       |
   |                        |                  | lossless compressed    |
   |                        |                  | images.                |
   +------------------------+------------------+------------------------+
   | CT/MR Studies on       | STD-CTMR-DVD-RAM | Handles single frame   |
   | DVD-RAM Media          |                  | 8, 12 or 16 bit        |
   |                        |                  | grayscale and 8 bit    |
   |                        |                  | palette color,         |
   |                        |                  | uncompressed and       |
   |                        |                  | lossless compressed    |
   |                        |                  | images.                |
   +------------------------+------------------+------------------------+
   | CT/MR Studies on DVD   | STD-CTMR-DVD     | Handles single frame   |
   | Media                  |                  | 8, 12 or 16 bit        |
   |                        |                  | grayscale and 8 bit    |
   |                        |                  | palette color,         |
   |                        |                  | uncompressed and       |
   |                        |                  | lossless compressed    |
   |                        |                  | images.                |
   +------------------------+------------------+------------------------+

.. note::

   Media Profiles STD-CTMR-MOD650, STD-CTMR-MOD12 and STD-CTMR-MOD23
   were previously defined but have been retired. See PS3.11 2004.

.. _sect_E.2:

Clinical Context
----------------

These Application Profiles facilitate the interchange and storage of
primary CT and MR images as well as related Secondary Capture Images
with certain defined attributes, including grayscale and palette color
images. CT, MR and SC images may co-exist within the same File-set.

Typical interchanges would be between acquisition devices, archives and
workstations, within and between institutions.

.. _sect_E.2.1:

Roles and Service Class Options
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

These Application Profiles uses the Media Storage Service Class defined
in .

The Application Entity shall support one or more of the roles of
File-set Creator, File-set Reader, and File-set Updater, defined in .

.. _sect_E.2.1.1:

File Set Creator
^^^^^^^^^^^^^^^^

The Application entity acting as a File-Set Creator generates a File Set
under a STD-CTMR Application Profile. Typical entities using this role
would include CT or MR equipment, and archive systems that generate a
patient record for transfer to another institution. File Set Creators
shall be able to generate the Basic Directory SOP Class in the DICOMDIR
File with all types of Directory Records related to the SOP Classes
stored in the File-set.

An FSC shall offer the ability to either finalize the disc at the
completion of the most recent write session (no additional information
can be subsequently added to the disc) or to allow multi-session
(additional information may be subsequently added to the disc) or to
allow packet-writing, if supported by the media and file system
specified in the profile.

.. note::

   A multiple volume (a logical volume that can cross multiple physical
   media) is not supported by this class of Application profile. If a
   set of Files, e.g., a Study, cannot be written entirely on one
   physical volume, the FSC will create multiple independent DICOM
   File-sets such that each File-set can reside on a single physical
   volume controlled by its individual DICOMDIR file. The user of the
   FSC can opt to use written labels on the physical volumes to indicate
   that there is more than one physical volume for this set of files
   (e.g., a study).

.. _sect_E.2.1.2:

File Set Reader
^^^^^^^^^^^^^^^

The role of File Set Reader is used by Application Entities that receive
a transferred File Set. Typical entities using this role would include
display workstations, and archive systems that receive a patient record
transferred from another institution. File Set Readers shall be able to
read all the SOP Classes defined for the specific Application Profile
for which a Conformance Statement is made, using all the defined
Transfer Syntaxes.

.. _sect_E.2.1.3:

File Set Updater
^^^^^^^^^^^^^^^^

The role of File Set Updater is used by Application Entities that
receive a transferred File Set and update it by the addition of
information. Typical entities using this role would include analytic
workstations, which, for instance, may add to the File-set an
information object containing a processed image. Stations that update
patient information objects would also use this role. File-set Updaters
do not have to read the images. File-set Updaters shall be able to
generate one or more of the SOP Instances defined for the specific
Application Profile for which a conformance statement is made, and to
read and update the DICOMDIR file.

An FSU shall offer the ability to either finalize the disc at the
completion of the most recent write session (no additional information
can be subsequently added to the disc) or to allow multi-session
(additional information may be subsequently added to the disc) or to
allow packet-writing if supported by the media and file system specified
in the profile.

.. note::

   If the volume has not been finalized, the File Set Updater will be
   able to update information assuming there is enough space on the
   volume to write a new DICOMDIR file, the information, and the
   fundamental volume control structures. Volume control structures are
   the structures that are inherent to the standards of the physical
   volume, see .

The FSU role is not defined for the STD-CTMR-DVD profile.

.. _sect_E.3:

STD-CTMR Profiles
-----------------

.. _sect_E.3.1:

SOP Classes and Transfer Syntaxes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

These Application Profiles are based on the Media Storage Service Class
(see ).

SOP Classes and corresponding Transfer Syntaxes supported by these
Application Profiles are specified in the
`table_title <#table_E.3-1>`__.

.. table:: STD-CTMR SOP Classes and Transfer Syntaxes

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
   | CT Image | 1        | JPEG     | Optional | M        | Optional |
   |          | .2.840.1 | Lossless |          | andatory |          |
   |          | 0008.5.1 | Process  |          |          |          |
   |          | .4.1.1.2 | 14       |          |          |          |
   |          |          | (s       |          |          |          |
   |          |          | election |          |          |          |
   |          |          | value 1) |          |          |          |
   |          |          |          |          |          |          |
   |          |          | 1.2.84   |          |          |          |
   |          |          | 0.10008. |          |          |          |
   |          |          | 1.2.4.70 |          |          |          |
   +----------+----------+----------+----------+----------+----------+
   | CT Image | 1        | Explicit | Optional | M        | Optional |
   |          | .2.840.1 | VR       |          | andatory |          |
   |          | 0008.5.1 | Little   |          |          |          |
   |          | .4.1.1.2 | Endian   |          |          |          |
   |          |          | Unco     |          |          |          |
   |          |          | mpressed |          |          |          |
   |          |          |          |          |          |          |
   |          |          | 1.2      |          |          |          |
   |          |          | .840.100 |          |          |          |
   |          |          | 08.1.2.1 |          |          |          |
   +----------+----------+----------+----------+----------+----------+
   | MR Image | 1        | JPEG     | Optional | M        | Optional |
   |          | .2.840.1 | Lossless |          | andatory |          |
   |          | 0008.5.1 | Process  |          |          |          |
   |          | .4.1.1.4 | 14       |          |          |          |
   |          |          | (s       |          |          |          |
   |          |          | election |          |          |          |
   |          |          | value 1) |          |          |          |
   |          |          |          |          |          |          |
   |          |          | 1.2.84   |          |          |          |
   |          |          | 0.10008. |          |          |          |
   |          |          | 1.2.4.70 |          |          |          |
   +----------+----------+----------+----------+----------+----------+
   | MR Image | 1        | Explicit | Optional | M        | Optional |
   |          | .2.840.1 | VR       |          | andatory |          |
   |          | 0008.5.1 | Little   |          |          |          |
   |          | .4.1.1.4 | Endian   |          |          |          |
   |          |          | Unco     |          |          |          |
   |          |          | mpressed |          |          |          |
   |          |          |          |          |          |          |
   |          |          | 1.2      |          |          |          |
   |          |          | .840.100 |          |          |          |
   |          |          | 08.1.2.1 |          |          |          |
   +----------+----------+----------+----------+----------+----------+
   | SC Image | 1        | JPEG     | Optional | M        | Optional |
   | (gr      | .2.840.1 | Lossless |          | andatory |          |
   | ayscale) | 0008.5.1 | Process  |          |          |          |
   |          | .4.1.1.7 | 14       |          |          |          |
   |          |          | (s       |          |          |          |
   |          |          | election |          |          |          |
   |          |          | value 1) |          |          |          |
   |          |          |          |          |          |          |
   |          |          | 1.2.84   |          |          |          |
   |          |          | 0.10008. |          |          |          |
   |          |          | 1.2.4.70 |          |          |          |
   +----------+----------+----------+----------+----------+----------+
   | SC Image | 1        | Explicit | Optional | M        | Optional |
   | (gr      | .2.840.1 | VR       |          | andatory |          |
   | ayscale) | 0008.5.1 | Little   |          |          |          |
   |          | .4.1.1.7 | Endian   |          |          |          |
   |          |          | Unco     |          |          |          |
   |          |          | mpressed |          |          |          |
   |          |          |          |          |          |          |
   |          |          | 1.2      |          |          |          |
   |          |          | .840.100 |          |          |          |
   |          |          | 08.1.2.1 |          |          |          |
   +----------+----------+----------+----------+----------+----------+
   | SC       | 1        | JPEG     | Optional | Optional | Optional |
   | Image    | .2.840.1 | Lossless |          |          |          |
   | (palette | 0008.5.1 | Process  |          |          |          |
   | color)   | .4.1.1.7 | 14       |          |          |          |
   |          |          | (s       |          |          |          |
   |          |          | election |          |          |          |
   |          |          | value 1) |          |          |          |
   |          |          |          |          |          |          |
   |          |          | 1.2.84   |          |          |          |
   |          |          | 0.10008. |          |          |          |
   |          |          | 1.2.4.70 |          |          |          |
   +----------+----------+----------+----------+----------+----------+
   | SC       | 1        | Explicit | Optional | Optional | Optional |
   | Image    | .2.840.1 | VR       |          |          |          |
   | (palette | 0008.5.1 | Little   |          |          |          |
   | color)   | .4.1.1.7 | Endian   |          |          |          |
   |          |          | Unco     |          |          |          |
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
   |          |          |          |          |          |          |
   |          |          | 1.2      |          |          |          |
   |          |          | .840.100 |          |          |          |
   |          |          | 08.1.2.1 |          |          |          |
   +----------+----------+----------+----------+----------+----------+
   | X-Ray    | 1.2.8    | Explicit | Optional | Optional | Optional |
   | R        | 40.10008 | VR       |          |          |          |
   | adiation | .5.1.4.1 | Little   |          |          |          |
   | Dose SR  | .1.88.67 | Endian   |          |          |          |
   |          |          | Unco     |          |          |          |
   |          |          | mpressed |          |          |          |
   |          |          |          |          |          |          |
   |          |          | 1.2      |          |          |          |
   |          |          | .840.100 |          |          |          |
   |          |          | 08.1.2.1 |          |          |          |
   +----------+----------+----------+----------+----------+----------+

.. note::

   1. The FSU requirement is not defined for STD-CTMR-DVD profile.

   2. The Detached Patient management SOP Class was formerly defined in
      these profiles, but has been retired.

.. _sect_E.3.2:

Physical Medium and Medium Format
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The STD-CTMR-MOD41 application profile requires the 130 mm 4.1GB R/W MOD
physical medium with the PCDOS Media Format, as defined in .

The STD-CTMR-CD application profile requires the 120 mm CD-R physical
medium with the ISO 9660 Media Format, as defined in .

The STD-CTMR-DVD-RAM application profile requires the 120 mm DVD-RAM
medium, as defined in .

The STD-CTMR-DVD application profile requires any of the 120 mm DVD
media other than DVD-RAM, as defined in .

.. _sect_E.3.3:

Directory Information in DICOMDIR
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Conformant Application Entities shall include in the DICOMDIR File a
Basic Directory IOD containing Directory Records at the Patient and
subsidiary levels appropriate to the SOP Classes in the File-set. All
DICOM files in the File-set incorporating SOP Instances defined for the
specific Application Profile shall be referenced by Directory Records.

.. note::

   DICOMDIRs with no directory information are not allowed by this
   Application Profile.

.. _sect_E.3.3.1:

Additional Keys
^^^^^^^^^^^^^^^

File Set Creators and Updaters are required to generate the mandatory
elements specified in .

.. _sect_E.3.3.2:

Localizer Related Attributes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Directory Records of type IMAGE shall include the mandatory attributes
from the Frame of Reference and Image Plane modules, if present in the
composite image object, as specified in and included in
`table_title <#table_E.3-2>`__, in order to allow the image to be
referenced to a localizer image or other orthogonal image. The Rows
(0028,0010) and Columns (0028,0011) attributes are required in order to
facilitate annotation of such a localizer.

.. note::

   The Frame of Reference module is specified in as mandatory for the CT
   and MR composite information objects, but not for Secondary Capture
   objects.

.. _sect_E.3.3.3:

Icon Images
^^^^^^^^^^^

Directory Records of type SERIES or IMAGE may include Icon Images. The
icon pixel data shall be as specified in Icon Image Key Definition, and
restricted such that Photometric Interpretation (0028,0004) shall be
MONOCHROME2 or PALETTE COLOR, Bits Allocated (0028,0100) and Bits Stored
(0028,0101) shall be equal to 8, and Rows (0028,0010) and Columns
(0028,0011) shall be equal to 64.

.. _sect_E.3.4:

Other Parameters
~~~~~~~~~~~~~~~~

This section defines other parameters in the STD-CTMR profiles that need
to be specified in order to ensure interoperable information
interchange.

.. table:: STD-CTMR Additional DICOMDIR Keys

   +-------------+-------------+-------------+----------+-------------+
   | **Key       | **Tag**     | **Directory | **Type** | **Notes**   |
   | Attribute** |             | Record      |          |             |
   |             |             | Type**      |          |             |
   +=============+=============+=============+==========+=============+
   | Referenced  | (0008,1140) | IMAGE       | 1C       | Required if |
   | Image       |             |             |          | present in  |
   | Sequence    |             |             |          | image       |
   |             |             |             |          | object.     |
   +-------------+-------------+-------------+----------+-------------+
   | >Referenced | (0008,1150) | IMAGE       | 1C       | Required if |
   | SOP Class   |             |             |          | Referenced  |
   | UID         |             |             |          | Image       |
   |             |             |             |          | Sequence    |
   |             |             |             |          | (0008,1140) |
   |             |             |             |          | is present. |
   +-------------+-------------+-------------+----------+-------------+
   | >Referenced | (0008,1155) | IMAGE       | 1C       | Required if |
   | SOP         |             |             |          | Referenced  |
   | Instance    |             |             |          | Image       |
   | UID         |             |             |          | Sequence    |
   |             |             |             |          | (0008,1140) |
   |             |             |             |          | is present. |
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
   | Image       | (0020,0032) | IMAGE       | 1C       | Required if |
   | Position    |             |             |          | present in  |
   | (Patient)   |             |             |          | image       |
   |             |             |             |          | object.     |
   +-------------+-------------+-------------+----------+-------------+
   | Image       | (0020,0037) | IMAGE       | 1C       | Required if |
   | Orientation |             |             |          | present in  |
   | (Patient)   |             |             |          | image       |
   |             |             |             |          | object.     |
   +-------------+-------------+-------------+----------+-------------+
   | Frame of    | (0020,0052) | IMAGE       | 1C       | Required if |
   | Reference   |             |             |          | present in  |
   | UID         |             |             |          | image       |
   |             |             |             |          | object.     |
   +-------------+-------------+-------------+----------+-------------+
   | Rows        | (0028,0010) | IMAGE       | 1        |             |
   +-------------+-------------+-------------+----------+-------------+
   | Columns     | (0028,0011) | IMAGE       | 1        |             |
   +-------------+-------------+-------------+----------+-------------+
   | Pixel       | (0028,0030) | IMAGE       | 1C       | Required if |
   | Spacing     |             |             |          | present in  |
   |             |             |             |          | image       |
   |             |             |             |          | object.     |
   +-------------+-------------+-------------+----------+-------------+

.. note::

   1. The Basic Directory Information Object definition in defines the
      following attributes as Type 1 or 2: for PATIENT directory
      records: (0010,0010) Patient's Name; for STUDY directory records:
      (0008,0050) Accession Number, (0008,0020) Study Date, (0008,1030)
      Study Description; for SERIES directory records: (0008,0060)
      Modality. Hence these are not redefined here.

   2. The Basic Directory Information Object definition in allows for
      the optional inclusion of Icon Images at the IMAGE or SERIES
      level. These remain optional for this profile, and the choice of
      whether or not to include Icon Images for every image or series,
      or in a more selective manner, is left up to the implementer.
      E.3.3.3 describes restrictions that apply to Icon Images that are
      included in this profile.

.. _sect_E.3.4.1:

Image Attribute Values
^^^^^^^^^^^^^^^^^^^^^^

The attributes listed in `table_title <#table_E.3-3>`__ used within CT
Image files, those listed in `table_title <#table_E.3-4>`__ used within
MR Image files, those listed in `table_title <#table_E.3-5>`__ used
within grayscale SC Image files, and those listed in
`table_title <#table_E.3-6>`__ used within color SC Image files, shall
take the values specified, which are more specific than, but must be
consistent with, those specified in the definition of the CT, MR and SC
Image Information Object Definitions in .

.. table:: STD-CTMR Required Image Attribute Values for CT Images

   ========================== =========== ===========
   **Attribute**              **Tag**     **Value**
   ========================== =========== ===========
   Modality                   (0008,0060) CT
   Photometric Interpretation (0028,0004) MONOCHROME2
   ========================== =========== ===========

.. table:: STD-CTMR Required Image Attribute Values for MR Images

   ========================== =========== ===========================
   **Attribute**              **Tag**     **Value**
   ========================== =========== ===========================
   Modality                   (0008,0060) MR
   Photometric Interpretation (0028,0004) MONOCHROME2
   Bits Stored                (0028,0101) 8, 12 to 16
   High Bit                   (0028,0102) Bits Stored (0028,0101) - 1
   ========================== =========== ===========================

.. note::

   The definition of the MR Composite Image Object in does not restrict
   (0028,0101) Bits Stored or (0028,0102) High Bit.

.. table:: STD-CTMR Required Image Attribute Values for Grayscale SC
Images

   ========================== =========== ===========================
   **Attribute**              **Tag**     **Value**
   ========================== =========== ===========================
   Samples Per Pixel          (0028,0002) 1
   Photometric Interpretation (0028,0004) MONOCHROME2
   Bits Allocated             (0028,0100) 8 or 16
   Bits Stored                (0028,0101) Bits Allocated (0028,0100)
   High Bit                   (0028,0102) Bits Stored (0028,0101) - 1
   ========================== =========== ===========================

.. table:: STD-CTMR Required Image Attribute Values for Color SC Images

   ========================== =========== =============
   **Attribute**              **Tag**     **Value**
   ========================== =========== =============
   Samples Per Pixel          (0028,0002) 1
   Photometric Interpretation (0028,0004) PALETTE COLOR
   Bits Allocated             (0028,0100) 8
   Bits Stored                (0028,0101) 8
   High Bit                   (0028,0102) 7
   ========================== =========== =============

.. _sect_E.3.4.1.1:

Attribute Value Precedence
''''''''''''''''''''''''''

Retired.

