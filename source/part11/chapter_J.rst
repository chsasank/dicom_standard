.. _chapter_J:

General Purpose USB and Flash Memory With Compression Interchange Profiles (Normative)
======================================================================================

.. _sect_J.1:

Profile Identification
----------------------

This Annex defines an Application Profile Class potentially inclusive of
all defined Media Storage SOP Classes. This class is intended to be used
for the interchange of Composite SOP Instances via USB, CF, MMC or SD
media for general-purpose applications. Objects from multiple modalities
may be included on the same media. Images may be compressed with or
without loss using either JPEG or JPEG 2000; all File Set Readers are
required to support decompression of all of the compressed Transfer
Syntaxes defined for each Profile.

A detailed list of the Media Storage SOP Classes that may be supported
is defined in .

.. table:: STD-GEN-USB, STD-GEN-SEC-USB STD-GEN-MMC, STD-GEN-SEC-MMC,
STD-GEN-CF, STD-GEN-SEC-CF, STD-GEN-SD and STD-GEN-SEC-SD Profiles

   +----------------------+----------------------+----------------------+
   | **Application        | **Identifier**       | **Description**      |
   | Profile**            |                      |                      |
   +======================+======================+======================+
   | General Purpose USB  | STD-GEN-USB-JPEG     | Handles interchange  |
   | Media Interchange    |                      | of Composite SOP     |
   | with JPEG            |                      | Instances such as    |
   |                      |                      | Images (optionally   |
   |                      |                      | compressed with      |
   |                      |                      | either lossless or   |
   |                      |                      | lossy JPEG),         |
   |                      |                      | Structured Reports,  |
   |                      |                      | Presentation States  |
   |                      |                      | and Waveforms.       |
   +----------------------+----------------------+----------------------+
   | General Purpose USB  | STD-GEN-USB-J2K      | Handles interchange  |
   | Media Interchange    |                      | of Composite SOP     |
   | with JPEG-2000       |                      | Instances such as    |
   |                      |                      | Images (optionally   |
   |                      |                      | compressed with      |
   |                      |                      | either reversible or |
   |                      |                      | irreversible JPEG    |
   |                      |                      | 2000), Structured    |
   |                      |                      | Reports,             |
   |                      |                      | Presentation States  |
   |                      |                      | and Waveforms.       |
   +----------------------+----------------------+----------------------+
   | General Purpose      | STD-GEN-SEC-USB-JPEG | Handles interchange  |
   | Secure USB Media     |                      | of Composite SOP     |
   | Interchange with     |                      | Instances such as    |
   | JPEG                 |                      | Images (optionally   |
   |                      |                      | compressed with      |
   |                      |                      | either lossless or   |
   |                      |                      | lossy JPEG),         |
   |                      |                      | Structured Reports,  |
   |                      |                      | Presentation States  |
   |                      |                      | and Waveforms.       |
   |                      |                      | Offers               |
   |                      |                      | confidentiality,     |
   |                      |                      | integrity and,       |
   |                      |                      | depending on the     |
   |                      |                      | File-set creator's   |
   |                      |                      | choice, data origin  |
   |                      |                      | authentication.      |
   +----------------------+----------------------+----------------------+
   | General Purpose      | STD-GEN-SEC-USB-J2K  | Handles interchange  |
   | Secure USB Media     |                      | of Composite SOP     |
   | Interchange with     |                      | Instances such as    |
   | JPEG-2000            |                      | Images (optionally   |
   |                      |                      | compressed with      |
   |                      |                      | either reversible or |
   |                      |                      | irreversible JPEG    |
   |                      |                      | 2000), Structured    |
   |                      |                      | Reports,             |
   |                      |                      | Presentation States  |
   |                      |                      | and Waveforms.       |
   |                      |                      | Offers               |
   |                      |                      | confidentiality,     |
   |                      |                      | integrity and,       |
   |                      |                      | depending on the     |
   |                      |                      | File-set creator's   |
   |                      |                      | choice, data origin  |
   |                      |                      | authentication.      |
   +----------------------+----------------------+----------------------+
   | General Purpose      | STD-GEN-MMC-JPEG     | Handles interchange  |
   | Multimedia Card      |                      | of Composite SOP     |
   | Interchange with     |                      | Instances such as    |
   | JPEG                 |                      | Images (optionally   |
   |                      |                      | compressed with      |
   |                      |                      | either lossless or   |
   |                      |                      | lossy JPEG),         |
   |                      |                      | Structured Reports,  |
   |                      |                      | Presentation States  |
   |                      |                      | and Waveforms.       |
   +----------------------+----------------------+----------------------+
   | General Purpose      | STD-GEN-MMC-J2K      | Handles interchange  |
   | Multimedia Card      |                      | of Composite SOP     |
   | Interchange with     |                      | Instances such as    |
   | JPEG-2000            |                      | Images (optionally   |
   |                      |                      | compressed with      |
   |                      |                      | either reversible or |
   |                      |                      | irreversible JPEG    |
   |                      |                      | 2000), Structured    |
   |                      |                      | Reports,             |
   |                      |                      | Presentation States  |
   |                      |                      | and Waveforms.       |
   +----------------------+----------------------+----------------------+
   | General Purpose      | STD-GEN-SEC-MMC-JPEG | Handles interchange  |
   | Secure Multimedia    |                      | of Composite SOP     |
   | Card Interchange     |                      | Instances such as    |
   | with JPEG            |                      | Images (optionally   |
   |                      |                      | compressed with      |
   |                      |                      | either lossless or   |
   |                      |                      | lossy JPEG),         |
   |                      |                      | Structured Reports,  |
   |                      |                      | Presentation States  |
   |                      |                      | and Waveforms.       |
   |                      |                      | Offers               |
   |                      |                      | confidentiality,     |
   |                      |                      | integrity and,       |
   |                      |                      | depending on the     |
   |                      |                      | File-set creator's   |
   |                      |                      | choice, data origin  |
   |                      |                      | authentication.      |
   +----------------------+----------------------+----------------------+
   | General Purpose      | STD-GEN-SEC-MMC-J2K  | Handles interchange  |
   | Secure Multimedia    |                      | of Composite SOP     |
   | Card Interchange     |                      | Instances such as    |
   | with JPEG-2000       |                      | Images (optionally   |
   |                      |                      | compressed with      |
   |                      |                      | either reversible or |
   |                      |                      | irreversible JPEG    |
   |                      |                      | 2000), Structured    |
   |                      |                      | Reports,             |
   |                      |                      | Presentation States  |
   |                      |                      | and Waveforms.       |
   |                      |                      | Offers               |
   |                      |                      | confidentiality,     |
   |                      |                      | integrity and,       |
   |                      |                      | depending on the     |
   |                      |                      | File-set creator's   |
   |                      |                      | choice, data origin  |
   |                      |                      | authentication.      |
   +----------------------+----------------------+----------------------+
   | General Purpose      | STD-GEN-CF-JPEG      | Handles interchange  |
   | CompactFlash         |                      | of Composite SOP     |
   | Interchange with     |                      | Instances such as    |
   | JPEG                 |                      | Images (optionally   |
   |                      |                      | compressed with      |
   |                      |                      | either lossless or   |
   |                      |                      | lossy JPEG),         |
   |                      |                      | Structured Reports,  |
   |                      |                      | Presentation States  |
   |                      |                      | and Waveforms.       |
   +----------------------+----------------------+----------------------+
   | General Purpose      | STD-GEN-CF-J2K       | Handles interchange  |
   | CompactFlash         |                      | of Composite SOP     |
   | Interchange with     |                      | Instances such as    |
   | JPEG-2000            |                      | Images (optionally   |
   |                      |                      | compressed with      |
   |                      |                      | either reversible or |
   |                      |                      | irreversible JPEG    |
   |                      |                      | 2000), Structured    |
   |                      |                      | Reports,             |
   |                      |                      | Presentation States  |
   |                      |                      | and Waveforms.       |
   +----------------------+----------------------+----------------------+
   | General Purpose      | STD-GEN-SEC-CF-JPEG  | Handles interchange  |
   | Secure CompactFlash  |                      | of Composite SOP     |
   | Interchange with     |                      | Instances such as    |
   | JPEG                 |                      | Images (optionally   |
   |                      |                      | compressed with      |
   |                      |                      | either lossless or   |
   |                      |                      | lossy JPEG),         |
   |                      |                      | Structured Reports,  |
   |                      |                      | Presentation States  |
   |                      |                      | and Waveforms.       |
   |                      |                      | Offers               |
   |                      |                      | confidentiality,     |
   |                      |                      | integrity and,       |
   |                      |                      | depending on the     |
   |                      |                      | File-set creator's   |
   |                      |                      | choice, data origin  |
   |                      |                      | authentication.      |
   +----------------------+----------------------+----------------------+
   | General Purpose      | STD-GEN-SEC-CF-J2K   | Handles interchange  |
   | Secure CompactFlash  |                      | of Composite SOP     |
   | Interchange with     |                      | Instances such as    |
   | JPEG-2000            |                      | Images (optionally   |
   |                      |                      | compressed with      |
   |                      |                      | either reversible or |
   |                      |                      | irreversible JPEG    |
   |                      |                      | 2000), Structured    |
   |                      |                      | Reports,             |
   |                      |                      | Presentation States  |
   |                      |                      | and Waveforms.       |
   |                      |                      | Offers               |
   |                      |                      | confidentiality,     |
   |                      |                      | integrity and,       |
   |                      |                      | depending on the     |
   |                      |                      | File-set creator's   |
   |                      |                      | choice, data origin  |
   |                      |                      | authentication.      |
   +----------------------+----------------------+----------------------+
   | General Purpose      | STD-GEN-SD-JPEG      | Handles interchange  |
   | Digital Card         |                      | of Composite SOP     |
   | Interchange with     |                      | Instances such as    |
   | JPEG                 |                      | Images (optionally   |
   |                      |                      | compressed with      |
   |                      |                      | either lossless or   |
   |                      |                      | lossy JPEG),         |
   |                      |                      | Structured Reports,  |
   |                      |                      | Presentation States  |
   |                      |                      | and Waveforms.       |
   +----------------------+----------------------+----------------------+
   | General Purpose      | STD-GEN-SD-J2K       | Handles interchange  |
   | Digital Card         |                      | of Composite SOP     |
   | Interchange with     |                      | Instances such as    |
   | JPEG-2000            |                      | Images (optionally   |
   |                      |                      | compressed with      |
   |                      |                      | either reversible or |
   |                      |                      | irreversible JPEG    |
   |                      |                      | 2000), Structured    |
   |                      |                      | Reports,             |
   |                      |                      | Presentation States  |
   |                      |                      | and Waveforms.       |
   +----------------------+----------------------+----------------------+
   | General Purpose      | STD-GEN-SEC-SD-JPEG  | Handles interchange  |
   | Secure Digital Card  |                      | of Composite SOP     |
   | Interchange with     |                      | Instances such as    |
   | JPEG                 |                      | Images (optionally   |
   |                      |                      | compressed with      |
   |                      |                      | either lossless or   |
   |                      |                      | lossy JPEG),         |
   |                      |                      | Structured Reports,  |
   |                      |                      | Presentation States  |
   |                      |                      | and Waveforms.       |
   |                      |                      | Offers               |
   |                      |                      | confidentiality,     |
   |                      |                      | integrity and,       |
   |                      |                      | depending on the     |
   |                      |                      | File-set creator's   |
   |                      |                      | choice, data origin  |
   |                      |                      | authentication.      |
   +----------------------+----------------------+----------------------+
   | General Purpose      | STD-GEN-SEC-SD-J2K   | Handles interchange  |
   | Secure Digital Card  |                      | of Composite SOP     |
   | Interchange with     |                      | Instances such as    |
   | JPEG-2000            |                      | Images (optionally   |
   |                      |                      | compressed with      |
   |                      |                      | either reversible or |
   |                      |                      | irreversible JPEG    |
   |                      |                      | 2000), Structured    |
   |                      |                      | Reports,             |
   |                      |                      | Presentation States  |
   |                      |                      | and Waveforms.       |
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

.. note::

   Since it is not required to support all Media Storage Classes the
   user should carefully consider the subset of supported Media Storage
   SOP Classes in the Conformance Statements of such equipment to
   establish effective object interchange.

.. _sect_J.2:

Clinical Context
----------------

This Application Profile Class facilitates the interchange of images and
related data on USB, CF, MMC or SD media. Typical interchange would be
between acquisition devices, archives and workstations.

This Application Profile Class facilitates the creation of a
multi-modality medium for image interchange, useful for clinical,
patient record, teaching and research applications, within and between
institutions.

This profile is intended only for general-purpose applications. It is
not intended as a replacement for specific Application Profiles that may
be defined for a particular clinical context.

.. _sect_J.2.1:

Roles and Service Class Options
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This Application Profile Class uses the Media Storage Service Class
defined in .

The Application Entity shall support one or more of the roles of File
Set Creator (FSC) or File Set Reader (FSR), or File Set Updater (FSU)
defined in .

.. _sect_J.2.1.1:

File Set Creator
^^^^^^^^^^^^^^^^

The role of File Set Creator shall be used by Application Entities that
generate a File Set under this Interchange Class of Application
Profiles.

File Set Creators shall be able to generate the Basic Directory SOP
Class in the DICOMDIR file with all the subsidiary Directory Records
related to the Image SOP Classes stored in the File Set. The Application
Entity acting as a File Set Creator generates a File Set under a
STD-GEN-USB, STD-GEN-SEC-USB STD-GEN-MMC, STD-GEN-SEC-MMC, STD-GEN-CF,
STD-GEN-SEC-CF, STD-GEN-SD or STD-GEN-SEC-SD Application Profile.

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

.. _sect_J.2.1.2:

File Set Reader
^^^^^^^^^^^^^^^

The role of File Set Reader shall be used by Application Entities that
receive a transferred File Set under this Interchange Class of
Application Profiles. Typical entities using this role would include
image generating systems, display workstations, and archive systems that
receive a patient record; e.g., transferred from another institution.

File Set Readers shall be able to read the DICOMDIR directory file and
all the SOP Instance files defined for this Application Profile, for
which a Conformance Statement is made, using all the defined Transfer
Syntaxes for the Profile.

.. note::

   All Transfer Syntaxes defined in the profile must be supported by the
   FSR. It is not permissible to only support one or other of the
   uncompressed or the compressed Transfer Syntaxes.

.. _sect_J.2.1.3:

File Set Updater
^^^^^^^^^^^^^^^^

The role of File Set Updater is used by Application Entities that
receive a transferred File Set under this Interchange Class of
Application Profiles and update it by the addition (or deletion) of
images or information to (or from) the medium. Typical entities using
this role would include image generating systems and workstations that
process or modify images.

File Set Updaters shall be able to generate one or more of the SOP
Instances defined for this Application Profile, for which a Conformance
Statement is made, and to read and update the DICOMDIR file.

.. _sect_J.3:

STD-GEN-USB, STD-GEN-SEC-USB, STD-GEN-MMC, STD-GEN-SEC-MMC, STD-GEN-CF, STD-GEN-SEC-CF, STD-GEN-SD and STD-GEN-SEC-SD Profile Classes
-------------------------------------------------------------------------------------------------------------------------------------

.. _sect_J.3.1:

SOP Classes and Transfer Syntaxes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This Application Profile is based on the Media Storage Service Class
(see ).

.. table:: STD-GEN-USB, STD-GEN-SEC-USB, STD-GEN-MMC, STD-GEN-SEC-MMC,
STD-GEN-CF, STD-GEN-SEC-CF, STD-GEN-SD and STD-GEN-SEC-SD SOP Classes
and Transfer Syntaxes

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
   | C        | *See*    | Explicit | Defined  | M        | Defined  |
   | omposite |          | VR       | in       | andatory | in       |
   | IODs for |          | Little   | Con      | for all  | Con      |
   | which a  |          | Endian   | formance | SOP      | formance |
   | Media    |          | Unco     | S        | Classes  | S        |
   | Storage  |          | mpressed | tatement | defined  | tatement |
   | SOP      |          |          |          | in       |          |
   | Class is |          | 1.2      |          | Con      |          |
   | defined  |          | .840.100 |          | formance |          |
   | in       |          | 08.1.2.1 |          | S        |          |
   |          |          |          |          | tatement |          |
   +----------+----------+----------+----------+----------+----------+
   | C        | *See*    | JPEG     | Defined  | M        | Defined  |
   | omposite |          | Lossless | in       | andatory | in       |
   | IODs for |          | Process  | Con      | for JPEG | Con      |
   | which a  |          | 14       | formance | profiles | formance |
   | Media    |          | (s       | S        | for all  | S        |
   | Storage  |          | election | tatement | SOP      | tatement |
   | SOP      |          | value 1) |          | Classes  |          |
   | Class is |          |          |          | defined  |          |
   | defined  |          | 1.2.84   |          | in       |          |
   | in       |          | 0.10008. |          | Con      |          |
   |          |          | 1.2.4.70 |          | formance |          |
   |          |          |          |          | S        |          |
   |          |          |          |          | tatement |          |
   +----------+----------+----------+----------+----------+----------+
   | C        | *See*    | JPEG     | Defined  | M        | Defined  |
   | omposite |          | Lossy,   | in       | andatory | in       |
   | IODs for |          | Baseline | Con      | for JPEG | Con      |
   | which a  |          | Se       | formance | profiles | formance |
   | Media    |          | quential | S        | for all  | S        |
   | Storage  |          | with     | tatement | SOP      | tatement |
   | SOP      |          | Huffman  |          | Classes  |          |
   | Class is |          | Coding   |          | defined  |          |
   | defined  |          | (Process |          | in       |          |
   | in       |          | 1)       |          | Con      |          |
   |          |          |          |          | formance |          |
   |          |          | 1.2.84   |          | S        |          |
   |          |          | 0.10008. |          | tatement |          |
   |          |          | 1.2.4.50 |          |          |          |
   +----------+----------+----------+----------+----------+----------+
   | C        | *See*    | JPEG     | Defined  | M        | Defined  |
   | omposite |          | Extended | in       | andatory | in       |
   | IODs for |          | (Process | Con      | for JPEG | Con      |
   | which a  |          | 2 & 4):  | formance | profiles | formance |
   | Media    |          |          | S        | for all  | S        |
   | Storage  |          | Default  | tatement | SOP      | tatement |
   | SOP      |          | Transfer |          | Classes  |          |
   | Class is |          | Syntax   |          | defined  |          |
   | defined  |          | for      |          | in       |          |
   | in       |          | Lossy    |          | Con      |          |
   |          |          | JPEG 12  |          | formance |          |
   |          |          | Bit      |          | S        |          |
   |          |          | Image    |          | tatement |          |
   |          |          | Com      |          |          |          |
   |          |          | pression |          |          |          |
   |          |          | (Process |          |          |          |
   |          |          | 4 only)  |          |          |          |
   |          |          |          |          |          |          |
   |          |          | 1.2.84   |          |          |          |
   |          |          | 0.10008. |          |          |          |
   |          |          | 1.2.4.51 |          |          |          |
   +----------+----------+----------+----------+----------+----------+
   | C        | *See*    | JPEG     | Defined  | M        | Defined  |
   | omposite |          | 2000     | in       | andatory | in       |
   | IODs for |          | Image    | Con      | for J2K  | Con      |
   | which a  |          | Com      | formance | profiles | formance |
   | Media    |          | pression | S        | for all  | S        |
   | Storage  |          | (        | tatement | SOP      | tatement |
   | SOP      |          | Lossless |          | Classes  |          |
   | Class is |          | Only)    |          | defined  |          |
   | defined  |          |          |          | in       |          |
   | in       |          | 1.2.84   |          | Con      |          |
   |          |          | 0.10008. |          | formance |          |
   |          |          | 1.2.4.90 |          | S        |          |
   |          |          |          |          | tatement |          |
   +----------+----------+----------+----------+----------+----------+
   | C        | *See*    | JPEG     | Defined  | M        | Defined  |
   | omposite |          | 2000     | in       | andatory | in       |
   | IODs for |          | Image    | Con      | for J2K  | Con      |
   | which a  |          | Com      | formance | profiles | formance |
   | Media    |          | pression | S        | for all  | S        |
   | Storage  |          |          | tatement | SOP      | tatement |
   | SOP      |          | 1.2.84   |          | Classes  |          |
   | Class is |          | 0.10008. |          | defined  |          |
   | defined  |          | 1.2.4.91 |          | in       |          |
   | in       |          |          |          | Con      |          |
   |          |          |          |          | formance |          |
   |          |          |          |          | S        |          |
   |          |          |          |          | tatement |          |
   +----------+----------+----------+----------+----------+----------+

The SOP Classes and corresponding Transfer Syntax supported by this
Application Profile are specified in the `table_title <#table_J.3-1>`__.
The supported Storage SOP Class(es) shall be listed in the Conformance
Statement using a table of the same form.

.. _sect_J.3.2:

Physical Medium and Medium Format
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The STD-GEN-USB-JPEG, STD-GEN-SEC-USB-JPEG, STD-GEN-USB-J2K and
STD-GEN-SEC-USB-J2K application profiles require any of the USB
Connected Removable Devices, as defined in .

The STD-GEN-MMC-JPEG, STD-GEN-SEC-MMC-JPEG, STD-GEN-MMC-J2K and
STD-GEN-SEC-MMC-J2K application profiles require any of the Multimedia
Card Removable Devices, as defined in .

The STD-GEN-CF-JPEG, STD- GEN-SEC-CF-JPEG, STD-GEN-CF-J2K and
STD-GEN-SEC-CF-J2K application profiles require any of the CompactFlash
Removable Devices, as defined in .

The STD-GEN-SD-JPEG, STD-GEN-SEC-SD-JPEG, STD-GEN-SD-J2K and
STD-GEN-SEC-SD-J2K application profiles require any of the Secure
Digital Card Removable Devices, as defined in .

.. _sect_J.3.3:

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

.. _sect_J.3.3.1:

Additional Keys
^^^^^^^^^^^^^^^

File Set Creators and Updaters are required to generate the mandatory
elements specified in .

`table_title <#table_H.3-2>`__ specifies the additional associated keys
that shall also be applicable to the profiles defined in this Annex. At
each directory record level other additional data elements can be added,
but it is not required that File Set Readers be able to use them as
keys. Refer to the Basic Directory IOD in .

.. _sect_J.3.4:

Other Parameters
~~~~~~~~~~~~~~~~

.. _sect_J.3.4.2:

Multi-frame JPEG Format
^^^^^^^^^^^^^^^^^^^^^^^

The JPEG encoding of pixel data shall use Interchange Format (with table
specification) for all frames.

.. _sect_J.3.5:

Security Parameters
~~~~~~~~~~~~~~~~~~~

The STD-GEN-SEC-USB-JPEG, STD-GEN-SEC-MMC-JPEG, STD-GEN-SEC-CF-JPEG,
STD-GEN-SEC-SD-JPEG, STD-GEN-SEC-USB-J2K, STD-GEN-SEC-MMC-J2K,
STD-GEN-SEC-CF-J2K and STD-GEN-SEC-SD-J2K application profiles require
that all DICOM Files in the File-set including the DICOMDIR be Secure
DICOM Files encapsulated in accordance with the requirements of the
Basic DICOM Media Security Profile as defined in .

.. note::

   These Application Profiles do not place any consistency restrictions
   on the use of the Basic DICOM Media Security Profile with different
   DICOM Files of one File-set. For example, readers should not assume
   that all Files in the File-set can be decoded by the same set of
   recipients. Readers should also not assume that all secure Files use
   the same approach (hash key or digital signature) to ensure Integrity
   or carry the same originators' signatures.

