.. _chapter_I:

DVD MPEG2 Interchange Profiles (Normative)
==========================================

.. _sect_I.1:

Profile Identification
----------------------

This Annex defines an Application Profile Class for all multi-frame
Media Image Storage SOP Classes compressed with MPEG2.

.. table:: STD-DVD-MPEG2-MPML and STD-DVD-SEC-MPEG2-MPML Profiles

   +----------------------+----------------------+----------------------+
   | **Application        | **Identifier**       | **Description**      |
   | Profile**            |                      |                      |
   +======================+======================+======================+
   | DVD Interchange with | STD-DVD-MPEG2-MPML   | Handles interchange  |
   | MPEG2 MP@ML          |                      | of multi-frame       |
   |                      |                      | images as MPEG2      |
   |                      |                      | MP@ML compressed     |
   |                      |                      | video sequences.     |
   +----------------------+----------------------+----------------------+
   | Secure DVD           | ST                   | Handles interchange  |
   | Interchange with     | D-DVD-SEC-MPEG2-MPML | of multi-frame       |
   | MPEG2 MP@ML          |                      | images as MPEG2      |
   |                      |                      | MP@ML compressed     |
   |                      |                      | video sequences.     |
   |                      |                      | Offers               |
   |                      |                      | confidentiality,     |
   |                      |                      | integrity and,       |
   |                      |                      | depending on the     |
   |                      |                      | File-set creator's   |
   |                      |                      | choice, data origin  |
   |                      |                      | authentication.      |
   +----------------------+----------------------+----------------------+

Equipment claiming conformance to this Application Profile shall list
the subset of Media Storage SOP Classes that it supports in its
Conformance Statement.

.. _sect_I.2:

Clinical Context
----------------

This Application Profile Class facilitates the interchange of images
data on DVD media. Typical interchange would be between acquisition
devices, archives and workstations.

.. _sect_I.2.1:

Roles and Service Class Options
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This Application Profile Class uses the Media Storage Service Class
defined in .

The Application Entity shall support one or more of the roles of File
Set Creator (FSC) or File Set Reader (FSR), defined in . The File Set
Updater (FSU) role is not defined.

.. _sect_I.2.1.1:

File Set Creator
^^^^^^^^^^^^^^^^

The role of File Set Creator shall be used by Application Entities that
generate a File Set under this Image Interchange Class of Application
Profiles.

File Set Creators shall be able to generate the Basic Directory SOP
Class in the DICOMDIR file with all the subsidiary Directory Records
related to the Image SOP Classes stored in the File Set. The Application
Entity acting as a File Set Creator generates a File Set under a
STD-DVD-MPEG2-MPML or STD-DVD-SEC-MPEG2-MPML Application Profile.

FSC shall offer the ability to either finalize the physical volume at
the completion of the most recent write session (no additional
information can be subsequently added to the volume) or to allow
multi-session (additional information may be subsequently added to the
volume). An FSC may allow packet-writing, if supported by the media and
file system specified in the profile.

.. note::

   A multiple volume (i.e., a logical volume that can cross multiple
   physical media) is not supported by this class of Application
   profile. If a set of Files, e.g., a Study, cannot be written entirely
   on one physical volume (side of one piece of media), the FSC will
   create multiple independent DICOM File Sets such that each File Set
   can reside on a single physical volume (side of a single piece of
   media) controlled by its individual DICOMDIR file. The user of the
   FSC can opt to use written labels on the physical volumes to indicate
   that there is more than one physical volume for this set of files
   (e.g., a study).

.. _sect_I.2.1.2:

File Set Reader
^^^^^^^^^^^^^^^

The role of File Set Reader shall be used by Application Entities that
receive a transferred File Set under the Image Interchange Class of
Application Profiles. Typical entities using this role would include
image generating systems, display workstations, and archive systems that
receive a patient record; e.g., transferred from another institution.

File Set Readers shall be able to read the DICOMDIR directory file and
all the SOP Instance files defined for this Application Profile, for
which a Conformance Statement is made, using all the defined Transfer
Syntaxes for the Profile.

.. _sect_I.2.1.3:

File Set Updater
^^^^^^^^^^^^^^^^

The FSU role is not defined for the STD-DVD-MPEG2-MPML and
STD-DVD-SEC-MPEG2-MPML profiles.

.. _sect_I.3:

STD-DVD-MPEG2-MPML and STD-DVD-SEC-MPEG2-MPML Profile Classes
-------------------------------------------------------------

.. _sect_I.3.1:

SOP Classes and Transfer Syntaxes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This Application Profile is based on the Media Storage Service Class
(see ).

.. table:: STD-DVD-MPEG2-MPML and STD-DVD-SEC-MPEG2-MPML SOP Classes and
Transfer Syntaxes

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
   | Multi-frame | *See*       | MPEG2 MP@ML | Defined in  | Mandatory   |
   | Composite   |             | Image       | Conformance | for all SOP |
   | IODs for    |             | Compression | Statement   | Classes     |
   | which a     |             |             |             | defined in  |
   | Media       |             | 1           |             | Conformance |
   | Storage SOP |             | .2.840.1000 |             | Statement   |
   | Class is    |             | 8.1.2.4.100 |             |             |
   | defined in  |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+

The SOP Classes and corresponding Transfer Syntax supported by this
Application Profile are specified in the `table_title <#table_I.3-1>`__.
The supported Storage SOP Class(es) shall be listed in the Conformance
Statement using a table of the same form.

.. _sect_I.3.2:

Physical Medium and Medium Format
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The STD-DVD-MPEG2-MPML and STD-DVD-SEC-MPEG2-MPML application profiles
require any of the 120 mm DVD media other than DVD-RAM, as defined in .

.. _sect_I.3.3:

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

.. _sect_I.3.3.1:

Additional Keys
^^^^^^^^^^^^^^^

File Set Creators and Updaters are required to generate the mandatory
elements specified in .

`table_title <#table_I.3-2>`__ specifies the additional associated keys.
At each directory record level other additional data elements can be
added, but it is not required that File Set Readers be able to use them
as keys. Refer to the Basic Directory IOD in .

.. table:: STD-DVD-MPEG2-MPML and STD-DVD-SEC-MPEG2-MPML Additional
DICOMDIR Keys

   +-------------+-------------+-------------+----------+-------------+
   | **Key       | **Tag**     | **Directory | **Type** | **Notes**   |
   | Attribute** |             | Record      |          |             |
   |             |             | Type**      |          |             |
   +=============+=============+=============+==========+=============+
   | Patient's   | (0010,0030) | PATIENT     | 1C       | Required if |
   | Birth Date  |             |             |          | present in  |
   |             |             |             |          | any objects |
   |             |             |             |          | referenced  |
   |             |             |             |          | by          |
   |             |             |             |          | subordinate |
   |             |             |             |          | records     |
   |             |             |             |          | with a      |
   |             |             |             |          | non-zero    |
   |             |             |             |          | length      |
   |             |             |             |          | value.      |
   +-------------+-------------+-------------+----------+-------------+
   | Patient's   | (0010,0040) | PATIENT     | 1C       | Required if |
   | Sex         |             |             |          | present in  |
   |             |             |             |          | any objects |
   |             |             |             |          | referenced  |
   |             |             |             |          | by          |
   |             |             |             |          | subordinate |
   |             |             |             |          | records     |
   |             |             |             |          | with a      |
   |             |             |             |          | non-zero    |
   |             |             |             |          | length      |
   |             |             |             |          | value.      |
   +-------------+-------------+-------------+----------+-------------+
   | Institution | (0008,0080) | SERIES      | 1C       | Required if |
   | Name        |             |             |          | present in  |
   |             |             |             |          | any objects |
   |             |             |             |          | referenced  |
   |             |             |             |          | by          |
   |             |             |             |          | subordinate |
   |             |             |             |          | records     |
   |             |             |             |          | with a      |
   |             |             |             |          | non-zero    |
   |             |             |             |          | length      |
   |             |             |             |          | value.      |
   +-------------+-------------+-------------+----------+-------------+
   | Institution | (0008,0081) | SERIES      | 1C       | Required if |
   | Address     |             |             |          | present in  |
   |             |             |             |          | any objects |
   |             |             |             |          | referenced  |
   |             |             |             |          | by          |
   |             |             |             |          | subordinate |
   |             |             |             |          | records     |
   |             |             |             |          | with a      |
   |             |             |             |          | non-zero    |
   |             |             |             |          | length      |
   |             |             |             |          | value.      |
   +-------------+-------------+-------------+----------+-------------+
   | Performing  | (0008,1050) | SERIES      | 1C       | Required if |
   | Physicians' |             |             |          | present in  |
   | Name        |             |             |          | any objects |
   |             |             |             |          | referenced  |
   |             |             |             |          | by          |
   |             |             |             |          | subordinate |
   |             |             |             |          | records     |
   |             |             |             |          | with a      |
   |             |             |             |          | non-zero    |
   |             |             |             |          | length      |
   |             |             |             |          | value.      |
   +-------------+-------------+-------------+----------+-------------+
   | Image Type  | (0008,0008) | IMAGE       | 1C       | Required if |
   |             |             |             |          | present in  |
   |             |             |             |          | image       |
   |             |             |             |          | object.     |
   +-------------+-------------+-------------+----------+-------------+
   | Lossy Image | (0028,2112) | IMAGE       | 1C       | Required if |
   | Compression |             |             |          | present in  |
   | Ratio       |             |             |          | image       |
   |             |             |             |          | object with |
   |             |             |             |          | a non-zero  |
   |             |             |             |          | length      |
   |             |             |             |          | value.      |
   +-------------+-------------+-------------+----------+-------------+
   | Rows        | (0028,0010) | IMAGE       | 1        |             |
   +-------------+-------------+-------------+----------+-------------+
   | Columns     | (0028,0011) | IMAGE       | 1        |             |
   +-------------+-------------+-------------+----------+-------------+

.. note::

   The requirements with respect to the mandatory DICOMDIR keys in imply
   that either these attributes are present in the Image IOD, or they
   are in some other way supplied by the File-set Creator. These
   attributes are (0010,0020) Patient ID, (0008,0020) Study Date,
   (0008,0030) Study Time, (0020,0010) Study ID, (0020,0011) Series
   Number, and (0020,0013) Instance Number.

.. _sect_I.3.4:

Security Parameters
~~~~~~~~~~~~~~~~~~~

The STD-DVD-SEC-MPEG2-MPML application profiles require that all DICOM
Files in the File-set including the DICOMDIR be Secure DICOM Files
encapsulated in accordance with the requirements of the Basic DICOM
Media Security Profile as defined in .

.. note::

   These Application Profiles do not place any consistency restrictions
   on the use of the Basic DICOM Media Security Profile with different
   DICOM Files of one File-set. For example, readers should not assume
   that all Files in the File-set can be decoded by the same set of
   recipients. Readers should also not assume that all secure Files use
   the same approach (hash key or digital signature) to ensure Integrity
   or carry the same originators' signatures.

.. _sect_I.3.5:

"dual-format" (informative)
~~~~~~~~~~~~~~~~~~~~~~~~~~~

It is desirable that consumer DVD players (and computer software for
playing conventional DVD movies) be able to play the video data that is
encoded on the DICOM DVD. The MPEG2 bit stream that is "encapsulated" by
the DICOM Transfer Syntax is potentially re-usable by such applications,
if the appropriate UDF structure is created to share the same extent
between the DICOM file and the file format and folder structure used by
the consumer DVD Video format. Alternatively, the bit stream could be
duplicated and both sets of files present on the same piece of media.

This profile does not require this, nor specify which approach to take.
Specifically, this profile does not require that a DVD Video file and
folder structure be present, though it is recommended.

