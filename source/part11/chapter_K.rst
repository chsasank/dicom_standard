.. _chapter_K:

Dental Application Profile (Normative)
======================================

.. _sect_K.1:

Class and Profile Identification
--------------------------------

This Annex defines Application Profiles for Dental Media Storage
applications.

.. table:: Dental Application Profile identifiers

   +-------------------------+----------------+-------------------------+
   | **Application Profile** | **Identifier** | **Description**         |
   +=========================+================+=========================+
   | Dental Radiograph       | STD-DEN-CD     | Interchange of dental   |
   | Interchange             |                | radiographic images on  |
   |                         |                | CD                      |
   +-------------------------+----------------+-------------------------+

.. _sect_K.2:

Clinical Context
----------------

This Application Profile facilitates the interchange of dental data on
media. Typical interchanges would be between dental systems, between a
dental system and a display workstation, between display workstations,
or between a dental system and a data archive. This context is shown in
`figure_title <#figure_K.2-1>`__.

The operational use of the media transfer is potentially between private
practitioners and an institution, intra-institutional and
inter-institutional.

.. _sect_K.2.1:

Roles
~~~~~

.. _sect_K.2.1.1:

File Set Creator
^^^^^^^^^^^^^^^^

The role of File Set Creator shall be used by Application Entities that
generate a File Set under the STD-DEN-CD Application Profile. Typical
entities using this role would include dental imaging equipment,
workstations, and archive systems that generate a patient record for
transfer. File Set Creators shall be able to generate the Basic
Directory SOP Class Instance in the DICOMDIR file and Digital Intra-oral
X-Ray and Digital X-Ray Image Storage SOP Class Instances in the File
Set.

An FSC shall offer the ability to either finalize the disc at the
completion of the most recent write session (no additional information
can be subsequently added to the disc) or to allow multi-session
(additional information may be subsequently added to the disc).

.. note::

   A multiple volume (a logical volume that can cross multiple physical
   media) is not supported by this Application Profile Class. If a set
   of Files, e.g., a Study, cannot be written entirely on one CD-R, the
   FSC will create multiple independent DICOM File-sets such that each
   File-set can reside on a single CD-R media controlled by its
   individual DICOMDIR file. The user of the FSC can opt to use written
   labels on the discs to indicate that there is more than one disc for
   this set of files (e.g., a study).

.. _sect_K.2.1.2:

File Set Reader
^^^^^^^^^^^^^^^

The role of File Set Reader shall be used by Application Entities that
receive a transferred File Set. Typical entities using this role would
include dental systems, display workstations, and archive systems that
receive a patient record from a piece of media. File Set Readers shall
be able to read the DICOMDIR directory file and all SOP Class Instances
defined for this Application Profile, using the defined Transfer
Syntaxes.

.. _sect_K.2.1.3:

File Set Updater
^^^^^^^^^^^^^^^^

The role of File Set Updater is not supported by this profile.

.. _sect_K.3:

General Class Profile
---------------------

.. _sect_K.3.1:

SOP Classes and Transfer Syntaxes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Application Profile STD-DEN-CD shall support the SOP Classes and
Transfer Syntaxes in the following table.

.. table:: Dental Abstract and Transfer Syntaxes

   +-------------+-------------+-------------+-------------+-------------+
   | **          | **SOP Class | **Transfer  | **FSC       | **FSR       |
   | Information | UID**       | Syntax and  | Re          | Re          |
   | Object      |             | UID**       | quirement** | quirement** |
   | D           |             |             |             |             |
   | efinition** |             |             |             |             |
   +=============+=============+=============+=============+=============+
   | Basic       | 1.2.840.1   | Explicit VR | Mandatory   | Mandatory   |
   | Directory   | 0008.1.3.10 | Little      |             |             |
   |             |             | Endian      |             |             |
   |             |             | U           |             |             |
   |             |             | ncompressed |             |             |
   |             |             |             |             |             |
   |             |             | 1.2.840.    |             |             |
   |             |             | 10008.1.2.1 |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Digital     | 1.2.8       | Explicit VR | Optional    | Mandatory   |
   | Intra-oral  | 40.10008.5. | Little      |             |             |
   | X-Ray Image | 1.4.1.1.1.3 | Endian      |             |             |
   | Storage -   |             | U           |             |             |
   | For         |             | ncompressed |             |             |
   | P           |             |             |             |             |
   | resentation |             | 1.2.840.    |             |             |
   |             |             | 10008.1.2.1 |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Digital     | 1.2.8       | Explicit VR | Optional    | Mandatory   |
   | X-Ray Image | 40.10008.5. | Little      |             |             |
   | Storage -   | 1.4.1.1.1.1 | Endian      |             |             |
   | For         |             | U           |             |             |
   | P           |             | ncompressed |             |             |
   | resentation |             |             |             |             |
   |             |             | 1.2.840.    |             |             |
   |             |             | 10008.1.2.1 |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Basic       | 1.2.8       | Explicit VR | Optional    | Optional    |
   | Structured  | 40.10008.5. | Little      |             |             |
   | Display     | 1.4.1.1.131 | Endian      |             |             |
   | Storage     |             | U           |             |             |
   |             |             | ncompressed |             |             |
   |             |             |             |             |             |
   |             |             | 1.2.840.    |             |             |
   |             |             | 10008.1.2.1 |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Grayscale   | 1.2.84      | Explicit VR | Optional    | Optional    |
   | Softcopy    | 0.10008.5.1 | Little      |             |             |
   | P           | .4.1.1.11.1 | Endian      |             |             |
   | resentation |             | U           |             |             |
   | State       |             | ncompressed |             |             |
   |             |             |             |             |             |
   |             |             | 1.2.840.    |             |             |
   |             |             | 10008.1.2.1 |             |             |
   +-------------+-------------+-------------+-------------+-------------+

.. note::

   The Digital X-Ray Image Storage and Digital Intra-oral X-Ray Image
   Storage For Presentation SOP Classes can also be used for scanned
   film.

A File Set Creator (FSC) shall support at least one of the specified
image storage SOP Classes.

.. _sect_K.3.2:

Physical Media and Media Formats
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The STD-DEN-CD profile requires the 120 mm CD-R physical media with the
ISO/IEC 9660 Media Format, as defined in .

.. _sect_K.3.3:

Directory Information in DICOMDIR
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Conformant Application Entities shall include in the DICOMDIR File the
Basic Directory IOD containing Directory Records at the Patient and the
subsidiary Study and Series levels, appropriate to the SOP Classes in
the File Set.

All DICOM files in the File Set incorporating SOP Instances defined for
the specific Application Profile shall be referenced by Directory
Records.

.. note::

   DICOMDIRs with no directory information are not allowed by this
   Application Profile.

All implementations shall include the DICOM Media Storage Directory in
the DICOMDIR file. There shall only be one DICOMDIR file per File Set.
The DICOMDIR file shall be in the root directory of the medium. The
Patient ID at the patient level shall be unique for each patient
directory record in one File Set.

No additional DICOMDIR keys are specified for this profile.

.. _sect_K.3.4:

Other Parameters
~~~~~~~~~~~~~~~~

.. _sect_K.3.4.1:

Image Attribute Values
^^^^^^^^^^^^^^^^^^^^^^

The Attributes listed in `table_title <#table_K.3-3>`__ used within the
image files shall take the values specified.

.. table:: STD-DEN-CD - Required Image Attribute Values

   +----------------+-------------+-------------------------------------+
   | **Attribute**  | **Tag**     | **Value**                           |
   +================+=============+=====================================+
   | Bits Allocated | (0028,0100) | If Bits Stored (0028,0101) is 8,    |
   |                |             | then 8; otherwise 16.               |
   +----------------+-------------+-------------------------------------+
   | Bits Stored    | (0028,0101) | 8, 10, 12 or 16                     |
   +----------------+-------------+-------------------------------------+

.. _sect_K.3.4.2:

Image Attribute Specialization
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Attributes listed in `table_title <#table_K.3-4>`__ shall have their
Types specialized.

.. table:: STD-DEN-CD - Required Image Attribute Types

   ================================== =========== ========
   **Attribute**                      **Tag**     **Type**
   ================================== =========== ========
   Institution Name                   (0008,0080) 2
   Manufacturer's Model Name          (0008,1090) 2
   Detector ID                        (0018,700A) 2
   Detector Manufacturer Name         (0018,702A) 2
   Detector Manufacturer's Model Name (0018,702B) 2
   ================================== =========== ========

.. note::

   These Type 3 attributes of the General Equipment and DX Detector
   Module are specialized in order to encourage FSCs to include values
   for them, recognizing that there are situations in which values may
   be unknown.

