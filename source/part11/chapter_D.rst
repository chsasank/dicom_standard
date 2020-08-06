.. _chapter_D:

General Purpose CD-R, DVD and BD Interchange Profiles (Normative)
=================================================================

.. _sect_D.1:

Profile Identification
----------------------

This Annex defines an Application Profile Class potentially inclusive of
all defined Media Storage SOP Classes. This class is intended to be used
for the interchange of Composite SOP Instances via CD-R, DVD-RAM and BD
media for general purpose applications. Objects from multiple modalities
may be included on the same media.

A detailed list of the Media Storage SOP Classes that may be supported
is defined in .

.. table:: STD-GEN Profile

   +----------------------+---------------------+----------------------+
   | **Application        | **Identifier**      | **Description**      |
   | Profile**            |                     |                      |
   +======================+=====================+======================+
   | General Purpose CD-R | STD-GEN-CD          | Handles interchange  |
   | Interchange          |                     | of Composite SOP     |
   |                      |                     | Instances such as    |
   |                      |                     | Images, Structured   |
   |                      |                     | Reports,             |
   |                      |                     | Presentation States  |
   |                      |                     | and Waveforms.       |
   +----------------------+---------------------+----------------------+
   | General Purpose      | STD-GEN-DVD-RAM     | Handles interchange  |
   | Interchange on       |                     | of Composite SOP     |
   | DVD-RAM Media        |                     | Instances such as    |
   |                      |                     | Images, Structured   |
   |                      |                     | Reports,             |
   |                      |                     | Presentation States  |
   |                      |                     | and Waveforms.       |
   +----------------------+---------------------+----------------------+
   | General Purpose      | STD-GEN-SEC-CD      | Handles interchange  |
   | Secure CD-R          |                     | of Composite SOP     |
   | Interchange          |                     | Instances such as    |
   |                      |                     | Images, Structured   |
   |                      |                     | Reports,             |
   |                      |                     | Presentation States  |
   |                      |                     | and Waveforms.       |
   |                      |                     | Offers               |
   |                      |                     | confidentiality,     |
   |                      |                     | integrity and,       |
   |                      |                     | depending on the     |
   |                      |                     | File-set creator's   |
   |                      |                     | choice, data origin  |
   |                      |                     | authentication.      |
   +----------------------+---------------------+----------------------+
   | General Purpose      | STD-GEN-SEC-DVD-RAM | Handles interchange  |
   | Secure Interchange   |                     | of Composite SOP     |
   | on DVD-RAM Media     |                     | Instances such as    |
   |                      |                     | Images, Structured   |
   |                      |                     | Reports,             |
   |                      |                     | Presentation States  |
   |                      |                     | and Waveforms.       |
   |                      |                     | Offers               |
   |                      |                     | confidentiality,     |
   |                      |                     | integrity and,       |
   |                      |                     | depending on the     |
   |                      |                     | File-set creator's   |
   |                      |                     | choice, data origin  |
   |                      |                     | authentication.      |
   +----------------------+---------------------+----------------------+
   | General Purpose      | STD-GEN-BD          | Handles Interchange  |
   | Interchange on BD    |                     | of Composite SOP     |
   | Media                |                     | Instances such as    |
   |                      |                     | Images, Structured   |
   |                      |                     | Reports,             |
   |                      |                     | Presentation States  |
   |                      |                     | and Waveforms.       |
   +----------------------+---------------------+----------------------+
   | General Purpose      | STD-GEN-SEC-BD      | Handles Interchange  |
   | Secure Interchange   |                     | of Composite SOP     |
   | on BD Media          |                     | Instances such as    |
   |                      |                     | Images, Structured   |
   |                      |                     | Reports,             |
   |                      |                     | Presentation States  |
   |                      |                     | and Waveforms.       |
   |                      |                     | Offers               |
   |                      |                     | confidentiality,     |
   |                      |                     | integrity and,       |
   |                      |                     | depending on the     |
   |                      |                     | File-set creator's   |
   |                      |                     | choice, data origin  |
   |                      |                     | authentication.      |
   +----------------------+---------------------+----------------------+

The identifier for this General Purpose Image Exchange profile class
shall be STD-GEN.

Equipment claiming conformance to this Application Profile shall list
the subset of Media Storage SOP Classes that it supports in its
Conformance Statement.

.. note::

   Since it is not required to support all Media Storage Classes the
   user should carefully consider the subset of supported Media Storage
   SOP Classes in the Conformance Statements of such equipment to
   establish effective object interchange.

.. _sect_D.2:

Clinical Context
----------------

This Application Profile facilitates the interchange of images and
related data on CD-R, DVD-RAM and BD media. Typical interchange would be
between acquisition devices, archives and workstations.

This Application Profile facilitates the creation of a multi-modality
medium for image interchange, useful for clinical, patient record,
teaching and research applications, within and between institutions.

This profile is intended only for general purpose applications. It is
not intended as a replacement for specific Application Profiles that may
be defined for a particular clinical context. The latter may support
compression Transfer Syntaxes, limitations on the form and content of
SOP Class instances, and specific media choices that preclude the use of
the General Purpose Interchange Profile.

.. note::

   The creation of a CD, DVD-RAM or BD is considerably more complex than
   the reading thereof. Therefore the clinical context for this
   Application profile is likely to be asymmetric, with a sophisticated
   File Set Creator and relatively simple File Set Readers.

.. _sect_D.2.1:

Roles and Service Class Options
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This Application Profile uses the Media Storage Service Class defined in
.

The Application Entity shall support one or more of the roles of File
Set Creator (FSC), File Set Reader (FSR), and File Set Updater (FSU),
defined in .

.. _sect_D.2.1.1:

File Set Creator
^^^^^^^^^^^^^^^^

The role of File Set Creator shall be used by Application Entities that
generate a File Set under this Image Interchange Class of Application
Profiles.

File Set Creators shall be able to generate the Basic Directory SOP
Class in the DICOMDIR file with all the subsidiary Directory Records
related to the Image SOP Classes stored in the File Set. The Application
Entity acting as a File Set Creator generates a File Set under a STD-GEN
Application Profile.

FSC shall offer the ability to either finalize the physical volume at
the completion of the most recent write session (no additional
information can be subsequently added to the volume) or to allow
multi-session (additional information may be subsequently added to the
volume) or to allow packet-writing, if supported by the media and file
system specified in the profile.

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

.. _sect_D.2.1.2:

File Set Reader
^^^^^^^^^^^^^^^

The role of File Set Reader shall be used by Application Entities that
receive a transferred File Set under the Image Interchange Class of
Application Profiles. Typical entities using this role would include
image generating systems, display workstations, and archive systems that
receive a patient record; e.g., transferred from another institution.

File Set Readers shall be able to read the DICOMDIR directory file and
all the SOP Instance files defined for this Application Profile, for
which a Conformance Statement is made, using the defined Transfer
Syntax.

.. _sect_D.2.1.3:

File Set Updater
^^^^^^^^^^^^^^^^

The role of File Set Updater is used by Application Entities that
receive a transferred File Set under the Image Exchange Class of
Application Profiles and update it by the addition (or deletion) of
images or information to (or from) the medium. Typical entities using
this role would include image generating systems and workstations that
process or modify images.

File Set Updaters shall be able to generate one or more of the SOP
Instances defined for this Application Profile, for which a Conformance
Statement is made, and to read and update the DICOMDIR file.

FSU shall offer the ability to either finalize the physical volume at
the completion of the most recent write session (no additional
information can be subsequently added to the volume) or to allow
multi-session (additional information may be subsequently added to the
volume) or to allow packet-writing. if supported by the media and file
system specified in the profile.

.. note::

   If the volume has not been finalized, the File Set Updater will be
   able to update information assuming there is enough space on the
   volume to write a new DICOMDIR file, the information, and the
   fundamental volume control structures. Volume control structures are
   the structures that are inherent to the standards of the physical
   volume, see .

.. _sect_D.3:

STD-GEN Profile Class
---------------------

.. _sect_D.3.1:

SOP Classes and Transfer Syntaxes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This Application Profile is based on the Media Storage Service Class
(see ).

.. table:: STD-GEN SOP Classes and Transfer Syntaxes

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
   | C        | *See*    | Explicit | Defined  | Defined  | Optional |
   | omposite |          | VR       | in       | in       |          |
   | Image &  |          | Little   | Con      | Con      |          |
   | Sta      |          | Endian   | formance | formance |          |
   | nd-alone |          | Unco     | S        | S        |          |
   | Storage  |          | mpressed | tatement | tatement |          |
   |          |          |          |          |          |          |
   |          |          | 1.2      |          |          |          |
   |          |          | .840.100 |          |          |          |
   |          |          | 08.1.2.1 |          |          |          |
   +----------+----------+----------+----------+----------+----------+

The SOP Classes and corresponding Transfer Syntax supported by this
Application Profile are specified in the `table_title <#table_D.3-1>`__.
The supported Storage SOP Class(es) shall be listed in the Conformance
Statement using a table of the same form.

.. _sect_D.3.2:

Physical Medium and Medium Format
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The STD-GEN-CD and STD-GEN-SEC-CD application profiles require the 120
mm CD-R physical medium with the ISO/IEC 9660 Media Format, as defined
in .

The STD-GEN-DVD-RAM and STD-GEN-SEC-DVD-RAM application profiles require
the 120 mm DVD-RAM medium, as defined in .

The STD-GEN-BD and STD-GEN-SEC-BD application profiles require any of
the 120 mm BD media, as defined in .

.. _sect_D.3.3:

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

.. _sect_D.3.3.1:

Additional Keys
^^^^^^^^^^^^^^^

File Set Creators and Updaters are required to generate the mandatory
elements specified in .

`table_title <#table_D.3-2>`__ specifies the additional associated keys.
At each directory record level other additional data elements can be
added, but it is not required that File Set Readers be able to use them
as keys. Refer to the Basic Directory IOD in .

.. table:: STD-GEN Additional DICOMDIR Keys

   +-------------+-------------+-------------+----------+-------------+
   | **Key       | **Tag**     | **Directory | **Type** | **Notes**   |
   | Attribute** |             | Record      |          |             |
   |             |             | Type**      |          |             |
   +=============+=============+=============+==========+=============+
   | Image Type  | (0008,0008) | IMAGE       | 1C       | Required if |
   |             |             |             |          | present in  |
   |             |             |             |          | image       |
   |             |             |             |          | object.     |
   +-------------+-------------+-------------+----------+-------------+
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
   |             |             |             |          | is present  |
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

.. note::

   The requirements with respect to the mandatory DICOMDIR keys in imply
   that either these attributes are present in the Image IOD, or they
   are in some other way supplied by the File-set Creator. These
   attributes are (0010,0020) Patient ID, (0008,0020) Study Date,
   (0008,0030) Study Time, (0020,0010) Study ID, (0020,0011) Series
   Number, and (0020,0013) Instance Number.

.. _sect_D.3.3.2:

Attribute Value Precedence
^^^^^^^^^^^^^^^^^^^^^^^^^^

Retired. See PS3.11 2004.

.. note::

   The retired Detached Patient Management SOP Class was previously
   suggested to allow patient identification and demographic information
   to be updated without changing the composite Image IOD files. This
   usage is now retired.

.. _sect_D.3.4:

Other Parameters
~~~~~~~~~~~~~~~~

Not applicable.

.. _sect_D.3.5:

Security Parameters
~~~~~~~~~~~~~~~~~~~

The STD-GEN-SEC-CD, STD-GEN-SEC-DVD-RAM and STD-GEN-SEC-BD application
profiles require that all DICOM Files in the File-set including the
DICOMDIR be Secure DICOM Files encapsulated in accordance with the
requirements of the Basic DICOM Media Security Profile as defined in .

.. note::

   These Application Profiles do not place any consistency restrictions
   on the use of the Basic DICOM Media Security Profile with different
   DICOM Files of one File-set. For example, readers should not assume
   that all Files in the File-set can be decoded by the same set of
   recipients. Readers should also not assume that all secure Files use
   the same approach (hash key or digital signature) to ensure Integrity
   or carry the same originators' signatures.

