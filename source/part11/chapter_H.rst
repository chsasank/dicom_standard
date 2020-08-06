.. _chapter_H:

General Purpose DVD With Compression Interchange Profiles (Normative)
=====================================================================

.. _sect_H.1:

Profile Identification
----------------------

This Annex defines an Application Profile Class potentially inclusive of
all defined Media Storage SOP Classes. This class is intended to be used
for the interchange of Composite SOP Instances via DVD media for general
purpose applications. Objects from multiple modalities may be included
on the same media. Images may be compressed with or without loss using
either JPEG or JPEG 2000; all File Set Readers are required to support
decompression of all of the compressed Transfer Syntaxes defined for
each Profile.

A detailed list of the Media Storage SOP Classes that may be supported
is defined in .

.. table:: STD-GEN-DVD and STD-GEN-SEC-DVD Profiles

   +----------------------+----------------------+----------------------+
   | **Application        | **Identifier**       | **Description**      |
   | Profile**            |                      |                      |
   +======================+======================+======================+
   | General Purpose DVD  | STD-GEN-DVD-JPEG     | Handles interchange  |
   | Interchange with     |                      | of Composite SOP     |
   | JPEG                 |                      | Instances such as    |
   |                      |                      | Images, Structured   |
   |                      |                      | Reports,             |
   |                      |                      | Presentation States  |
   |                      |                      | and Waveforms,       |
   |                      |                      | either uncompressed  |
   |                      |                      | or with lossless or  |
   |                      |                      | lossy JPEG.          |
   +----------------------+----------------------+----------------------+
   | General Purpose DVD  | STD-GEN-DVD-J2K      | Handles interchange  |
   | Interchange with     |                      | of Composite SOP     |
   | JPEG 2000            |                      | Instances such as    |
   |                      |                      | Images, Structured   |
   |                      |                      | Reports,             |
   |                      |                      | Presentation States  |
   |                      |                      | and Waveforms,       |
   |                      |                      | either uncompressed  |
   |                      |                      | or with lossless or  |
   |                      |                      | lossy JPEG 2000.     |
   +----------------------+----------------------+----------------------+
   | General Purpose      | STD-GEN-SEC-DVD-JPEG | Handles interchange  |
   | Secure DVD           |                      | of Composite SOP     |
   | Interchange with     |                      | Instances such as    |
   | JPEG                 |                      | Images, Structured   |
   |                      |                      | Reports,             |
   |                      |                      | Presentation States  |
   |                      |                      | and Waveforms,       |
   |                      |                      | either uncompressed  |
   |                      |                      | or with lossless or  |
   |                      |                      | lossy JPEG. Offers   |
   |                      |                      | confidentiality,     |
   |                      |                      | integrity and,       |
   |                      |                      | depending on the     |
   |                      |                      | File-set creator's   |
   |                      |                      | choice, data origin  |
   |                      |                      | authentication.      |
   +----------------------+----------------------+----------------------+
   | General Purpose      | STD-GEN-SEC-DVD-J2K  | Handles interchange  |
   | Secure DVD           |                      | of Composite SOP     |
   | Interchange with     |                      | Instances such as    |
   | JPEG 2000            |                      | Images, Structured   |
   |                      |                      | Reports,             |
   |                      |                      | Presentation States  |
   |                      |                      | and Waveforms,       |
   |                      |                      | either uncompressed  |
   |                      |                      | or with lossless or  |
   |                      |                      | lossy JPEG 2000.     |
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

.. _sect_H.2:

Clinical Context
----------------

This Application Profile Class facilitates the interchange of images and
related data on DVD media. Typical interchange would be between
acquisition devices, archives and workstations.

This Application Profile Class facilitates the creation of a
multi-modality medium for image interchange, useful for clinical,
patient record, teaching and research applications, within and between
institutions.

This profile is intended only for general purpose applications. It is
not intended as a replacement for specific Application Profiles that may
be defined for a particular clinical context.

.. note::

   The creation of a DVD is considerably more complex than the reading
   thereof. Therefore the clinical context for this Application profile
   is likely to be asymmetric, with a sophisticated File Set Creator and
   relatively simple File Set Readers.

.. _sect_H.2.1:

Roles and Service Class Options
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This Application Profile Class uses the Media Storage Service Class
defined in .

The Application Entity shall support one or more of the roles of File
Set Creator (FSC) or File Set Reader (FSR), defined in . The File Set
Updater (FSU) role is not defined.

.. _sect_H.2.1.1:

File Set Creator
^^^^^^^^^^^^^^^^

The role of File Set Creator shall be used by Application Entities that
generate a File Set under this Image Interchange Class of Application
Profiles.

File Set Creators shall be able to generate the Basic Directory SOP
Class in the DICOMDIR file with all the subsidiary Directory Records
related to the Image SOP Classes stored in the File Set. The Application
Entity acting as a File Set Creator generates a File Set under a
STD-GEN-DVD or STD-GEN-SEC-DVD Application Profile.

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

.. _sect_H.2.1.2:

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

.. _sect_H.2.1.3:

File Set Updater
^^^^^^^^^^^^^^^^

The FSU role is not defined for the STD-GEN-DVD and STD-GEN-SEC-DVD
profiles.

.. _sect_H.3:

STD-GEN-DVD and STD-GEN-SEC-DVD Profile Classes
-----------------------------------------------

.. _sect_H.3.1:

SOP Classes and Transfer Syntaxes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This Application Profile is based on the Media Storage Service Class
(see ).

.. table:: STD-GEN-DVD and STD-GEN-SEC-DVD SOP Classes and Transfer
Syntaxes

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
   | Composite   | *See*       | Explicit VR | Defined in  | Mandatory   |
   | IODs for    |             | Little      | Conformance | for all SOP |
   | which a     |             | Endian      | Statement   | Classes     |
   | Media       |             | U           |             | defined in  |
   | Storage SOP |             | ncompressed |             | Conformance |
   | Class is    |             |             |             | Statement   |
   | defined in  |             | 1.2.840.    |             |             |
   |             |             | 10008.1.2.1 |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Composite   | *See*       | JPEG        | Defined in  | Mandatory   |
   | IODs for    |             | Lossless    | Conformance | for -JPEG   |
   | which a     |             | Process 14  | Statement   | profiles    |
   | Media       |             | (selection  |             | for all SOP |
   | Storage SOP |             | value 1)    |             | Classes     |
   | Class is    |             |             |             | defined in  |
   | defined in  |             | 1.2.840.100 |             | Conformance |
   |             |             | 08.1.2.4.70 |             | Statement   |
   +-------------+-------------+-------------+-------------+-------------+
   | Composite   | *See*       | JPEG Lossy, | Defined in  | Mandatory   |
   | IODs for    |             | Baseline    | Conformance | for -JPEG   |
   | which a     |             | Sequential  | Statement   | profiles    |
   | Media       |             | with        |             | for all SOP |
   | Storage SOP |             | Huffman     |             | Classes     |
   | Class is    |             | Coding      |             | defined in  |
   | defined in  |             | (Process 1) |             | Conformance |
   |             |             |             |             | Statement   |
   |             |             | 1.2.840.100 |             |             |
   |             |             | 08.1.2.4.50 |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Composite   | *See*       | JPEG        | Defined in  | Mandatory   |
   | IODs for    |             | Extended    | Conformance | for -JPEG   |
   | which a     |             | (Process 2  | Statement   | profiles    |
   | Media       |             | & 4):       |             | for all SOP |
   | Storage SOP |             |             |             | Classes     |
   | Class is    |             | Default     |             | defined in  |
   | defined in  |             | Transfer    |             | Conformance |
   |             |             | Syntax for  |             | Statement   |
   |             |             | Lossy JPEG  |             |             |
   |             |             | 12 Bit      |             |             |
   |             |             | Image       |             |             |
   |             |             | Compression |             |             |
   |             |             | (Process 4  |             |             |
   |             |             | only)       |             |             |
   |             |             |             |             |             |
   |             |             | 1.2.840.100 |             |             |
   |             |             | 08.1.2.4.51 |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Composite   | *See*       | JPEG 2000   | Defined in  | Mandatory   |
   | IODs for    |             | Image       | Conformance | for -J2K    |
   | which a     |             | Compression | Statement   | profiles    |
   | Media       |             | (Lossless   |             | for all SOP |
   | Storage SOP |             | Only)       |             | Classes     |
   | Class is    |             |             |             | defined in  |
   | defined in  |             | 1.2.840.100 |             | Conformance |
   |             |             | 08.1.2.4.90 |             | Statement   |
   +-------------+-------------+-------------+-------------+-------------+
   | Composite   | *See*       | JPEG 2000   | Defined in  | Mandatory   |
   | IODs for    |             | Image       | Conformance | for -J2K    |
   | which a     |             | Compression | Statement   | profiles    |
   | Media       |             |             |             | for all SOP |
   | Storage SOP |             | 1.2.840.100 |             | Classes     |
   | Class is    |             | 08.1.2.4.91 |             | defined in  |
   | defined in  |             |             |             | Conformance |
   |             |             |             |             | Statement   |
   +-------------+-------------+-------------+-------------+-------------+

The SOP Classes and corresponding Transfer Syntax supported by this
Application Profile are specified in the `table_title <#table_H.3-1>`__.
The supported Storage SOP Class(es) shall be listed in the Conformance
Statement using a table of the same form.

.. _sect_H.3.2:

Physical Medium and Medium Format
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The STD-GEN-DVD and STD-GEN-SEC-DVD application profiles require any of
the 120 mm DVD media other than DVD-RAM, as defined in .

.. _sect_H.3.3:

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

.. _sect_H.3.3.1:

Additional Keys
^^^^^^^^^^^^^^^

File Set Creators and Updaters are required to generate the mandatory
elements specified in .

`table_title <#table_H.3-2>`__ specifies the additional associated keys.
At each directory record level other additional data elements can be
added, but it is not required that File Set Readers be able to use them
as keys. Refer to the Basic Directory IOD in .

.. table:: STD-GEN-DVD and STD-GEN-SEC-DVD Additional DICOMDIR Keys

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
   | Calibration | (0050,0004) | IMAGE       | 1C       | Required if |
   | Image       |             |             |          | present in  |
   |             |             |             |          | image       |
   |             |             |             |          | object with |
   |             |             |             |          | a non-zero  |
   |             |             |             |          | length      |
   |             |             |             |          | value.      |
   +-------------+-------------+-------------+----------+-------------+
   | Referenced  | (0008,1140) | IMAGE or    | 1C       | Required if |
   | Image       |             | S           |          | present in  |
   | Sequence    |             | PECTROSCOPY |          | image       |
   |             |             |             |          | object with |
   |             |             |             |          | one or more |
   |             |             |             |          | items,      |
   |             |             |             |          | either in   |
   |             |             |             |          | the top     |
   |             |             |             |          | level Data  |
   |             |             |             |          | Set or      |
   |             |             |             |          | nested      |
   |             |             |             |          | within a    |
   |             |             |             |          | functional  |
   |             |             |             |          | group       |
   |             |             |             |          | sequence of |
   |             |             |             |          | the Shared  |
   |             |             |             |          | Functional  |
   |             |             |             |          | Groups      |
   |             |             |             |          | Sequence    |
   |             |             |             |          | (           |
   |             |             |             |          | 5200,9229). |
   |             |             |             |          |             |
   |             |             |             |          | This        |
   |             |             |             |          | sequence    |
   |             |             |             |          | shall be    |
   |             |             |             |          | the entire  |
   |             |             |             |          | contents of |
   |             |             |             |          | the         |
   |             |             |             |          | sequence    |
   |             |             |             |          | present in  |
   |             |             |             |          | image       |
   |             |             |             |          | object (all |
   |             |             |             |          | items and   |
   |             |             |             |          | elements    |
   |             |             |             |          | shall be    |
   |             |             |             |          | copied in   |
   |             |             |             |          | the same    |
   |             |             |             |          | order and   |
   |             |             |             |          | no addition |
   |             |             |             |          | or removal  |
   |             |             |             |          | shall be    |
   |             |             |             |          | done). When |
   |             |             |             |          | more then   |
   |             |             |             |          | one         |
   |             |             |             |          | sequence is |
   |             |             |             |          | present in  |
   |             |             |             |          | the image   |
   |             |             |             |          | object, the |
   |             |             |             |          | top level   |
   |             |             |             |          | Data Set    |
   |             |             |             |          | sequence    |
   |             |             |             |          | shall be    |
   |             |             |             |          | copied.     |
   +-------------+-------------+-------------+----------+-------------+
   | Lossy Image | (0028,2112) | IMAGE       | 1C       | Required if |
   | Compression |             |             |          | present in  |
   | Ratio       |             |             |          | image       |
   |             |             |             |          | object with |
   |             |             |             |          | a non-zero  |
   |             |             |             |          | length      |
   |             |             |             |          | value.      |
   +-------------+-------------+-------------+----------+-------------+
   | Rows        | (0028,0010) | IMAGE or    | 1        |             |
   |             |             | S           |          |             |
   |             |             | PECTROSCOPY |          |             |
   +-------------+-------------+-------------+----------+-------------+
   | Columns     | (0028,0011) | IMAGE or    | 1        |             |
   |             |             | S           |          |             |
   |             |             | PECTROSCOPY |          |             |
   +-------------+-------------+-------------+----------+-------------+
   | Frame of    | (0020,0052) | IMAGE or    | 1C       | Required if |
   | Reference   |             | S           |          | present in  |
   | UID         |             | PECTROSCOPY |          | image or    |
   |             |             |             |          | s           |
   |             |             |             |          | pectroscopy |
   |             |             |             |          | object.     |
   +-------------+-------------+-------------+----------+-------------+
   | Sync        | (0020,0200) | IMAGE or    | 1C       | Required if |
   | hronization |             | S           |          | present in  |
   | Frame of    |             | PECTROSCOPY |          | image or    |
   | Reference   |             |             |          | s           |
   | UID         |             |             |          | pectroscopy |
   |             |             |             |          | object.     |
   +-------------+-------------+-------------+----------+-------------+
   | Number of   | (0028,0008) | IMAGE or    | 1C       | Required if |
   | Frames      |             | S           |          | present in  |
   |             |             | PECTROSCOPY |          | image or    |
   |             |             |             |          | s           |
   |             |             |             |          | pectroscopy |
   |             |             |             |          | object.     |
   +-------------+-------------+-------------+----------+-------------+
   | Acquisition | (0018,1800) | IMAGE or    | 1C       | Required if |
   | Time        |             | S           |          | present in  |
   | S           |             | PECTROSCOPY |          | image or    |
   | ynchronized |             |             |          | s           |
   |             |             |             |          | pectroscopy |
   |             |             |             |          | object.     |
   +-------------+-------------+-------------+----------+-------------+
   | Acquisition | (0008,002A) | IMAGE or    | 1C       | Required if |
   | DateTime    |             | S           |          | present in  |
   |             |             | PECTROSCOPY |          | image or    |
   |             |             |             |          | s           |
   |             |             |             |          | pectroscopy |
   |             |             |             |          | object.     |
   +-------------+-------------+-------------+----------+-------------+
   | Image       | (0020,0032) | IMAGE or    | 1C       | Required if |
   | Position    |             | S           |          | present in  |
   | (Patient)   |             | PECTROSCOPY |          | image or    |
   |             |             |             |          | s           |
   |             |             |             |          | pectroscopy |
   |             |             |             |          | object,     |
   |             |             |             |          | either in   |
   |             |             |             |          | the top     |
   |             |             |             |          | level Data  |
   |             |             |             |          | Set or      |
   |             |             |             |          | nested      |
   |             |             |             |          | within a    |
   |             |             |             |          | functional  |
   |             |             |             |          | group       |
   |             |             |             |          | sequence of |
   |             |             |             |          | the Shared  |
   |             |             |             |          | Functional  |
   |             |             |             |          | Groups      |
   |             |             |             |          | Sequence    |
   |             |             |             |          | (           |
   |             |             |             |          | 5200,9229). |
   +-------------+-------------+-------------+----------+-------------+
   | Image       | (0020,0037) | IMAGE or    | 1C       | Required if |
   | Orientation |             | S           |          | present in  |
   | (Patient)   |             | PECTROSCOPY |          | image or    |
   |             |             |             |          | s           |
   |             |             |             |          | pectroscopy |
   |             |             |             |          | object,     |
   |             |             |             |          | either in   |
   |             |             |             |          | the top     |
   |             |             |             |          | level Data  |
   |             |             |             |          | Set or      |
   |             |             |             |          | nested      |
   |             |             |             |          | within a    |
   |             |             |             |          | functional  |
   |             |             |             |          | group       |
   |             |             |             |          | sequence of |
   |             |             |             |          | the Shared  |
   |             |             |             |          | Functional  |
   |             |             |             |          | Groups      |
   |             |             |             |          | Sequence    |
   |             |             |             |          | (           |
   |             |             |             |          | 5200,9229). |
   +-------------+-------------+-------------+----------+-------------+
   | Pixel       | (0028,0030) | IMAGE or    | 1C       | Required if |
   | Spacing     |             | S           |          | present in  |
   |             |             | PECTROSCOPY |          | image or    |
   |             |             |             |          | s           |
   |             |             |             |          | pectroscopy |
   |             |             |             |          | object,     |
   |             |             |             |          | either in   |
   |             |             |             |          | the top     |
   |             |             |             |          | level Data  |
   |             |             |             |          | Set or      |
   |             |             |             |          | nested      |
   |             |             |             |          | within a    |
   |             |             |             |          | functional  |
   |             |             |             |          | group       |
   |             |             |             |          | sequence of |
   |             |             |             |          | the Shared  |
   |             |             |             |          | Functional  |
   |             |             |             |          | Groups      |
   |             |             |             |          | Sequence    |
   |             |             |             |          | (           |
   |             |             |             |          | 5200,9229). |
   +-------------+-------------+-------------+----------+-------------+

.. note::

   The requirements with respect to the mandatory DICOMDIR keys in imply
   that either these attributes are present in the Image IOD, or they
   are in some other way supplied by the File-set Creator. These
   attributes are (0010,0020) Patient ID, (0008,0020) Study Date,
   (0008,0030) Study Time, (0020,0010) Study ID, (0020,0011) Series
   Number, and (0020,0013) Instance Number.

.. _sect_H.3.4:

Other Parameters
~~~~~~~~~~~~~~~~

.. _sect_H.3.4.2:

Multi-frame JPEG Format
^^^^^^^^^^^^^^^^^^^^^^^

The JPEG encoding of pixel data shall use Interchange Format (with table
specification) for all frames.

.. _sect_H.3.5:

Security Parameters
~~~~~~~~~~~~~~~~~~~

The STD-GEN-SEC-DVD application profiles require that all DICOM Files in
the File-set including the DICOMDIR be Secure DICOM Files encapsulated
in accordance with the requirements of the Basic DICOM Media Security
Profile as defined in .

.. note::

   These Application Profiles do not place any consistency restrictions
   on the use of the Basic DICOM Media Security Profile with different
   DICOM Files of one File-set. For example, readers should not assume
   that all Files in the File-set can be decoded by the same set of
   recipients. Readers should also not assume that all secure Files use
   the same approach (hash key or digital signature) to ensure Integrity
   or carry the same originators' signatures.

