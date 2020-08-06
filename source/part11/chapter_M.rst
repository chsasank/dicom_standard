.. _chapter_M:

General Purpose BD With Compression Interchange Profiles (Normative)
====================================================================

.. _sect_M.1:

Profile Identification
----------------------

This Annex defines an Application Profile Class potentially inclusive of
all defined Media Storage SOP Classes. This class is intended to be used
for the interchange of Composite SOP Instances via BD media for
general-purpose applications. Objects from multiple modalities may be
included on the same media. Images may be compressed with or without
loss using either JPEG or JPEG 2000. And multi-frame images and video
may be compressed with MPEG2 Main Profile / Main Level or MPEG2 Main
Profile / High Level or MPEG-4 AVC/H.264 High Profile / Level 4.1 or
MPEG-4 AVC/H.264 BD-compatible High Profile / Level 4.1; all File Set
Readers are required to support decompression of all of the compressed
Transfer Syntaxes defined for each Profile.

A detailed list of the Media Storage SOP Classes that may be supported
is defined in .

.. table:: STD-GEN-BD and STD-GEN-SEC-BD Profiles

   +----------------------+----------------------+----------------------+
   | **Application        | **Identifier**       | **Description**      |
   | Profile**            |                      |                      |
   +======================+======================+======================+
   | General Purpose BD   | STD-GEN-BD-JPEG      | Handles interchange  |
   | Interchange with     |                      | of Composite SOP     |
   | JPEG                 |                      | Instances such as    |
   |                      |                      | Images (optionally   |
   |                      |                      | compressed with      |
   |                      |                      | either lossless or   |
   |                      |                      | lossy JPEG),         |
   |                      |                      | Structured Reports,  |
   |                      |                      | Presentation States  |
   |                      |                      | and Waveforms.       |
   +----------------------+----------------------+----------------------+
   | General Purpose BD   | STD-GEN-BD-J2K       | Handles interchange  |
   | Interchange with     |                      | of Composite SOP     |
   | JPEG 2000            |                      | Instances such as    |
   |                      |                      | Images (optionally   |
   |                      |                      | compressed with      |
   |                      |                      | either lossless or   |
   |                      |                      | lossy JPEG 2000),    |
   |                      |                      | Structured Reports,  |
   |                      |                      | Presentation States  |
   |                      |                      | and Waveforms.       |
   +----------------------+----------------------+----------------------+
   | General Purpose BD   | S                    | Handles interchange  |
   | Interchange with     | TD-GEN-BD-MPEG2-MPML | of multi-frame       |
   | MPEG2 MP@ML          |                      | images and video     |
   |                      |                      | using MPEG2 MP@ML    |
   |                      |                      | compression.         |
   +----------------------+----------------------+----------------------+
   | General Purpose BD   | S                    | Handles interchange  |
   | Interchange with     | TD-GEN-BD-MPEG2-MPHL | of multi-frame       |
   | MPEG2 MP@HL          |                      | images and video     |
   |                      |                      | using MPEG2 MP@HL    |
   |                      |                      | compression.         |
   +----------------------+----------------------+----------------------+
   | General Purpose BD   | STD                  | Handles interchange  |
   | Interchange with     | -GEN-BD-MPEG4-HPLV41 | of multi-frame       |
   | MPEG-4 AVC/H.264     |                      | images and video     |
   | HiP@Level4.1         |                      | using MPEG-4         |
   |                      |                      | AVC/H.264            |
   |                      |                      | HiP@Level4.1         |
   |                      |                      | compression.         |
   +----------------------+----------------------+----------------------+
   | General Purpose BD   | STD-G                | Handles interchange  |
   | Interchange with     | EN-BD-MPEG4-HPLV41BD | of multi-frame       |
   | MPEG-4 AVC/H.264     |                      | images and video     |
   | BD-Compatible        |                      | using MPEG-4         |
   | HiP@Level4.1         |                      | AVC/H.264            |
   |                      |                      | BD-compatible        |
   |                      |                      | HiP@Level4.1         |
   |                      |                      | compression.         |
   +----------------------+----------------------+----------------------+
   | General Purpose      | STD-GEN-SEC-BD-JPEG  | Handles interchange  |
   | Secure BD            |                      | of Composite SOP     |
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
   | General Purpose      | STD-GEN-SEC-BD-J2K   | Handles interchange  |
   | Secure BD            |                      | of Composite SOP     |
   | Interchange with     |                      | Instances such as    |
   | JPEG 2000            |                      | Images (optionally   |
   |                      |                      | compressed with      |
   |                      |                      | either lossless or   |
   |                      |                      | lossy JPEG 2000),    |
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
   | General Purpose      | STD-G                | Handles interchange  |
   | Secure BD            | EN-SEC-BD-MPEG2-MPML | of multi-frame       |
   | Interchange with     |                      | images and video     |
   | MPEG2 MP@ML          |                      | using MPEG2 MP@ML    |
   |                      |                      | compression. Offers  |
   |                      |                      | confidentiality,     |
   |                      |                      | integrity and,       |
   |                      |                      | depending on the     |
   |                      |                      | File-set creator's   |
   |                      |                      | choice, data origin  |
   |                      |                      | authentication.      |
   +----------------------+----------------------+----------------------+
   | General Purpose      | STD-G                | Handles interchange  |
   | Secure BD            | EN-SEC-BD-MPEG2-MPHL | of multi-frame       |
   | Interchange with     |                      | images and video     |
   | MPEG2 MP@HL          |                      | using MPEG2 MP@HL    |
   |                      |                      | compression. Offers  |
   |                      |                      | confidentiality,     |
   |                      |                      | integrity and,       |
   |                      |                      | depending on the     |
   |                      |                      | File-set creator's   |
   |                      |                      | choice, data origin  |
   |                      |                      | authentication.      |
   +----------------------+----------------------+----------------------+
   | General Purpose      | STD-GEN              | Handles interchange  |
   | Secure BD            | -SEC-BD-MPEG4-HPLV41 | of multi-frame       |
   | Interchange with     |                      | images and video     |
   | MPEG-4 AVC/H.264     |                      | using MPEG-4         |
   | HiP@Level4.1         |                      | AVC/H.264            |
   |                      |                      | HiP@Level4.1         |
   |                      |                      | compression. Offers  |
   |                      |                      | confidentiality,     |
   |                      |                      | integrity and,       |
   |                      |                      | depending on the     |
   |                      |                      | File-set creator's   |
   |                      |                      | choice, data origin  |
   |                      |                      | authentication.      |
   +----------------------+----------------------+----------------------+
   | General Purpose      | STD-GEN-S            | Handles interchange  |
   | Secure BD            | EC-BD-MPEG4-HPLV41BD | of multi-frame       |
   | Interchange with     |                      | images and video     |
   | MPEG-4 AVC/H.264     |                      | using MPEG-4         |
   | BD-compatible        |                      | AVC/H.264            |
   | HiP@Level4.1         |                      | BD-compatible        |
   |                      |                      | HiP@Level4.1         |
   |                      |                      | compression. Offers  |
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

.. _sect_M.2:

Clinical Context
----------------

This Application Profile Class facilitates the interchange of images and
related data on BD media. Typical interchange would be between
acquisition devices, archives and workstations.

This Application Profile Class facilitates the creation of a
multi-modality medium for image interchange, useful for clinical,
patient record, teaching and research applications, within and between
institutions.

This profile is intended only for general-purpose applications. It is
not intended as a replacement for specific Application Profiles that may
be defined for a particular clinical context.

.. note::

   1. The creation of a BD is considerably more complex than the reading
      thereof. Therefore the clinical context for this Application
      profile is likely to be asymmetric, with a sophisticated File Set
      Creator and relatively simple File Set Readers.

   2. Each BD Rewritable/Recordable contains a unique ID, which can be
      read by a BD drive. This ID can be used for referring to a BD, for
      example in a database.

.. _sect_M.2.1:

Roles and Service Class Options
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This Application Profile Class uses the Media Storage Service Class
defined in with the Interchange Option.

The Application Entity shall support one or more of the roles of File
Set Creator (FSC) or File Set Reader (FSR), or File Set Updater (FSU)
defined in .

.. _sect_M.2.1.1:

File Set Creator
^^^^^^^^^^^^^^^^

The role of File Set Creator shall be used by Application Entities that
generate a File Set under this Interchange Class of Application
Profiles.

File Set Creators shall be able to generate the Basic Directory SOP
Class in the DICOMDIR file with all the subsidiary Directory Records
related to the Image SOP Classes stored in the File Set. The Application
Entity acting as a File Set Creator generates a File Set under a
STD-GEN-BD or STD-GEN-SEC-BD Application Profile.

An FSC shall offer the ability to finalize the physical volume at the
completion of the most recent write session (no additional information
can be subsequently added to the volume), if supported by the media and
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

.. _sect_M.2.1.2:

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

.. note::

   All Transfer Syntaxes defined in the profile must be supported by the
   FSR. It is not permissible to only support one or other of the
   uncompressed or the compressed Transfer Syntaxes.

.. _sect_M.2.1.3:

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

An FSU shall offer the ability to finalize the physical volume at the
completion of the most recent write session (no additional information
can be subsequently added to the volume), if supported by the media and
file system specified in the profile.

.. note::

   If the volume has not been finalized, the File Set Updater will be
   able to update information assuming there is enough space on the
   volume to write a new DICOMDIR file, the information, and the
   fundamental volume control structures. Volume control structures are
   the structures that are inherent to the standards of the physical
   volume, see .

.. _sect_M.3:

STD-GEN-BD and STD-GEN-SEC-BD Profile Classes
---------------------------------------------

.. _sect_M.3.1:

SOP Classes and Transfer Syntaxes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This Application Profile is based on the Media Storage Service Class
with the Interchange Option (see ).

.. table:: STD-GEN-BD and STD-GEN-SEC-BD SOP Classes and Transfer
Syntaxes

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
   | Mul      | *See*    | MPEG2    | Defined  | M        | Defined  |
   | ti-frame |          | Main     | in       | andatory | in       |
   | C        |          | Profile  | Con      | for all  | Con      |
   | omposite |          | @ Main   | formance | SOP      | formance |
   | IODs for |          | Level    | S        | Classes  | S        |
   | which a  |          |          | tatement | defined  | tatement |
   | Media    |          | 1.2.840  |          | in       |          |
   | Storage  |          | .10008.1 |          | Con      |          |
   | SOP      |          | .2.4.100 |          | formance |          |
   | Class is |          |          |          | S        |          |
   | defined  |          |          |          | tatement |          |
   | in       |          |          |          |          |          |
   +----------+----------+----------+----------+----------+----------+
   | Mul      | *See*    | MPEG2    | Defined  | M        | Defined  |
   | ti-frame |          | Main     | in       | andatory | in       |
   | C        |          | Profile  | Con      | for all  | Con      |
   | omposite |          | @ High   | formance | SOP      | formance |
   | IODs for |          | Level    | S        | Classes  | S        |
   | which a  |          |          | tatement | defined  | tatement |
   | Media    |          | 1.2.840  |          | in       |          |
   | Storage  |          | .10008.1 |          | Con      |          |
   | SOP      |          | .2.4.101 |          | formance |          |
   | Class is |          |          |          | S        |          |
   | defined  |          |          |          | tatement |          |
   | in       |          |          |          |          |          |
   +----------+----------+----------+----------+----------+----------+
   | Mul      | *See*    | MPEG-4   | Defined  | M        | Defined  |
   | ti-frame |          | A        | in       | andatory | in       |
   | C        |          | VC/H.264 | Con      | for all  | Con      |
   | omposite |          | High     | formance | SOP      | formance |
   | IODs for |          | Profile  | S        | Classes  | S        |
   | which a  |          | / Level  | tatement | defined  | tatement |
   | Media    |          | 4.1      |          | in       |          |
   | Storage  |          |          |          | Con      |          |
   | SOP      |          | 1.2.840  |          | formance |          |
   | Class is |          | .10008.1 |          | S        |          |
   | defined  |          | .2.4.102 |          | tatement |          |
   | in       |          |          |          |          |          |
   +----------+----------+----------+----------+----------+----------+
   | Mul      | *See*    | MPEG-4   | Defined  | M        | Defined  |
   | ti-frame |          | A        | in       | andatory | in       |
   | C        |          | VC/H.264 | Con      | for all  | Con      |
   | omposite |          | BD-co    | formance | SOP      | formance |
   | IODs for |          | mpatible | S        | Classes  | S        |
   | which a  |          | High     | tatement | defined  | tatement |
   | Media    |          | Profile  |          | in       |          |
   | Storage  |          | / Level  |          | Con      |          |
   | SOP      |          | 4.1      |          | formance |          |
   | Class is |          |          |          | S        |          |
   | defined  |          | 1.2.840  |          | tatement |          |
   | in       |          | .10008.1 |          |          |          |
   |          |          | .2.4.103 |          |          |          |
   +----------+----------+----------+----------+----------+----------+

The SOP Classes and corresponding Transfer Syntax supported by this
Application Profile are specified in the `table_title <#table_M.3-1>`__.
The supported Storage SOP Class(es) shall be listed in the Conformance
Statement using a table of the same form.

.. _sect_M.3.2:

Physical Medium and Medium Format
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The STD-GEN-BD and STD-GEN-SEC-BD application profiles require any of
the 120 mm BD media, as defined in .

.. _sect_M.3.3:

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

.. _sect_M.3.3.1:

Additional Keys
^^^^^^^^^^^^^^^

File Set Creators and Updaters are required to generate the mandatory
elements specified in .

`table_title <#table_H.3-2>`__ specifies the additional associated keys
that shall also be applicable to the profiles defined in this Annex. At
each directory record level other additional data elements can be added,
but it is not required that File Set Readers be able to use them as
keys. Refer to the Basic Directory IOD in .

.. _sect_M.3.4:

Other Parameters
~~~~~~~~~~~~~~~~

.. _sect_M.3.4.1:

Multi-frame JPEG Format
^^^^^^^^^^^^^^^^^^^^^^^

The JPEG encoding of pixel data shall use Interchange Format (with table
specification) for all frames.

.. _sect_M.3.5:

Security Parameters
~~~~~~~~~~~~~~~~~~~

The STD-GEN-SEC-BD application profiles require that all DICOM Files in
the File-set including the DICOMDIR be Secure DICOM Files encapsulated
in accordance with the requirements of the Basic DICOM Media Security
Profile as defined in .

.. note::

   These Application Profiles do not place any consistency restrictions
   on the use of the Basic DICOM Media Security Profile with different
   DICOM Files of one File-set. For example, readers should not assume
   that all Files in the File-set can be decoded by the same set of
   recipients. Readers should also not assume that all secure Files use
   the same approach (hash key or digital signature) to ensure integrity
   or carry the same originators' signatures.

