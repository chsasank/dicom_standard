.. _chapter_A:

Basic Cardiac X-Ray Angiographic Application Profile (Normative)
================================================================

.. _sect_A.1:

Class and Profile Identification
--------------------------------

This Annex defines an Application Profile Class for Basic Cardiac X-Ray
Angiographic clinical applications.

The identifier for this class shall be STD-XABC. This annex is concerned
only with cardiac angiography.

The specific Application Profile in this class is shown in the
`table_title <#table_A.1-1>`__.

.. note::

   This table contains only a single Application Profile. It is expected
   that additional Application Profiles may be added to PS3.11.

.. table:: Basic Cardiac XA Profile

   +-------------------------+----------------+-------------------------+
   | **Application Profile** | **Identifier** | **Description**         |
   +=========================+================+=========================+
   | Basic Cardiac X-Ray     | STD-XABC-CD    | It handles single frame |
   | Angiographic Studies on |                | or multi-frame digital  |
   | CD-R Media              |                | images up to 512x512x8  |
   |                         |                | bits; biplane           |
   |                         |                | acquisitions are        |
   |                         |                | encoded as two single   |
   |                         |                | plane information       |
   |                         |                | objects.                |
   +-------------------------+----------------+-------------------------+

.. _sect_A.2:

Clinical Context
----------------

This Application Profile Class facilitates the interchange of primary
digital X-Ray cine runs, typically acquired as part of cardiac
catheterization procedures. Typical media interchanges would be from
in-lab acquisition equipment to either a display workstation or to a
data archive system, or between a display workstation and a data archive
system (in both directions). This context is shown in
`figure_title <#figure_A.2-1>`__.

The operational use of media interchange is potentially both
intra-institutional and inter-institutional.

.. _sect_A.2.1:

Roles and Service Class Options
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This Application Profile Class uses the Media Storage Service Class
defined in .

The Application Entity shall support one or more of the roles of
File-set Creator, File-set Reader, and File-set Updater, defined in .

.. _sect_A.2.1.1:

File Set Creator
^^^^^^^^^^^^^^^^

The Application entity acting as a File-Set Creator generates a File Set
under the STD-XABC Application Profile Class. Typical entities using
this role would include X-Ray angiographic lab equipment, and archive
systems that generate a patient record for transfer to another
institution. File Set Creators shall be able to generate the Basic
Directory SOP Class in the DICOMDIR File with all types of Directory
Records related to the SOP Classes stored in the File-set.

FSC shall offer the ability to either finalize the disc at the
completion of the most recent write session (no additional information
can be subsequently added to the disc) or to allow multi-session
(additional information may be subsequently added to the disk).

.. note::

   A multiple volume (a logical volume that can cross multiple physical
   media) is not supported by this Application Profile Class. If a set
   of Files, e.g., a Study, cannot be written entirely on one CD-R, the
   FSC will create multiple independent DICOM File-sets such that each
   File-set can reside on a single CD-R media controlled by its
   individual DICOMDIR file. The user of the FSC can opt to use written
   labels on the discs to indicate that there is more than one disc for
   this set of files (e.g., a study).

.. _sect_A.2.1.2:

File Set Reader
^^^^^^^^^^^^^^^

The role of File Set Reader is used by Application Entities that receive
a transferred File Set. Typical entities using this role would include
display workstations, and archive systems that receive a patient record
transferred from another institution. File Set Readers shall be able to
read all the SOP Classes defined for the specific Application Profile
for which a Conformance Statement is made, using all the defined
Transfer Syntaxes.

.. _sect_A.2.1.3:

File Set Updater
^^^^^^^^^^^^^^^^

The role of File Set Updater is used by Application Entities that
receive a transferred File Set and update it by the addition of
information. Typical entities using this role would include analytic
workstations, which, for instance, may add to the File-set an
information object containing a processed (e.g., edge-enhanced) image.
Stations that update patient information objects would also use this
role. File-set Updaters do not have to read the images. File-set
Updaters shall be able to generate one or more of the SOP Instances
defined for the specific Application Profile for which a conformance
statement is made, and to read and update the DICOMDIR file.

FSU shall offer the ability to either finalize the disc at the
completion of the most recent write session (no additional information
can be subsequently added to the disc) or to allow multi-session
(additional information may be subsequently added to the disk).

.. note::

   If the disc has not been closed out, the File-set Updater shall be
   able to update information assuming there is enough space on the disc
   to write a new DICOMDIR file, the information, and the fundamental
   CD-R control structures. CD-R control structures are the structures
   that are inherent to the CD-R standards, see .

.. _sect_A.3:

STD-XABC-CD Basic Cardiac Profile
---------------------------------

.. _sect_A.3.1:

SOP Classes and Transfer Syntaxes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This Application Profile is based on the Media Storage Service Class
(see ).

SOP Classes and corresponding Transfer Syntaxes supported by this
Application Profile are specified in the `table_title <#table_A.3-1>`__.

.. table:: STD-XABC-CD SOP Classes and Transfer Syntaxes

   +----------+----------+----------+----------+----------+----------+
   | **Inf    | **SOP    | **       | **FSC    | **FSR    | **FSU    |
   | ormation | Class    | Transfer | Requi    | Requi    | Requi    |
   | Object   | UID**    | Syntax   | rement** | rement** | rement** |
   | Defi     |          | and      |          |          |          |
   | nition** |          | UID**    |          |          |          |
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

.. note::

   1. This application profile does not allow the use of the X-Ray
      Angiographic Bi-Plane Image Object. Biplane acquisitions must
      therefore be transferred as two single plane SOP instances. A
      future Application Profile that permits X-Ray Angiographic
      Bi-Plane Image Object transfer is under development.

   2. This Application Profile includes only the XA Image SOP Instances.
      It does not include Standalone Curve, Modality LUT, VOI LUT, or
      Overlay SOP Instances.

.. _sect_A.3.2:

Physical Media and Media Formats
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Basic Cardiac Application Profiles in the STD-XABC class require the 120
mm CD-R physical media with the ISO/IEC 9660 Media Format, as defined in
.

.. _sect_A.3.3:

Directory Information in DICOMDIR
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Conformant Application Entities shall include in the DICOMDIR File a
Basic Directory IOD containing Directory Records at the Patient and
subsidiary levels appropriate to the SOP Classes in the File-set.

.. note::

   DICOMDIRs with no directory information are not allowed by this
   Application Profile.

.. _sect_A.3.3.1:

Additional Keys
^^^^^^^^^^^^^^^

`table_title <#table_A.3-2>`__ specifies the type of Directory Records
that shall be supported and the additional associated keys. Refer to the
Basic Directory IOD in .

.. table:: STD-XABC-CD Additional DICOMDIR Keys

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
   |             |             |             |          |             |
   | Sequence    |             |             |          |             |
   +-------------+-------------+-------------+----------+-------------+
   | Image Type  | (0008,0008) | IMAGE       | 1        |             |
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
   |             |             |             |          | Record has  |
   |             |             |             |          | an Image    |
   |             |             |             |          | Type        |
   |             |             |             |          | (0008,0008) |
   |             |             |             |          | of BIPLANE  |
   |             |             |             |          | A or        |
   |             |             |             |          | BIPLANE B.  |
   |             |             |             |          | May be      |
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

.. _sect_A.3.3.2:

Icon Images
^^^^^^^^^^^

Directory Records of type IMAGE shall include Icon Images. The icon
pixel data shall be supported with Bits Allocated (0028,0100) equal to 8
and Row (0028,0010) and Column (0028,0011) attribute values of 128.

.. note::

   1. This icon size is larger than that recommended in because the
      64x64 icon would not be clinically useful for identifying and
      selecting X-Ray angiographic images.

   2. For multi-frame images, it is recommended that the icon image be
      derived from the frame identified in the Representative Frame
      Number attribute (0028,6010), if defined for the image SOP
      Instance. If the Representative Frame Number is not present, a
      frame approximately one-third of the way through the multi-frame
      image should be selected. The process to reduce a 512x512 image to
      a 128x128 image is beyond the scope of this Standard.

.. _sect_A.3.4:

Other Parameters
~~~~~~~~~~~~~~~~

This section defines other parameters common to all specific Application
Profiles in the STD-XABC class that need to be specified in order to
ensure interoperable media interchange.

.. _sect_A.3.4.1:

Image Attribute Values
^^^^^^^^^^^^^^^^^^^^^^

The attributes listed in `table_title <#table_A.3-3>`__ used within the
X-Ray Angiographic Image files shall take the values specified.

.. table:: STD-XABC-CD- Required Image Attribute Values

   ============== =========== ===============
   **Attribute**  **Tag**     **Value**
   ============== =========== ===============
   Modality       (0008,0060) XA
   Rows           (0028,0010) 512 (see below)
   Columns        (0028,0011) 512 (see below)
   Bits Allocated (0028,0100) 8
   Bits Stored    (0028,0101) 8
   ============== =========== ===============

When creating or updating a File-set, Rows or Columns shall not exceed a
value of 512. When reading a File-set, an FSR or FSU shall accept a
value of at least 512 for Rows or Columns.

Overlay data, if present, shall be encoded in Overlay Data (60XX,3000).

.. _sect_A.3.4.1.1:

Attribute Value Precedence
''''''''''''''''''''''''''

Retired. See PS3.11 2004.

.. note::

   The retired Detached Patient Management SOP Class was previously
   suggested to allow patient identification and demographic information
   to be updated without changing the composite Image IOD files. This
   usage is now retired.

