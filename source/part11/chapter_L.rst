.. _chapter_L:

ZIP File Over Email Interchange Profiles (Normative)
====================================================

.. _sect_L.1:

Profile Identification
----------------------

This Annex defines three Application Profiles for interchange of a DICOM
Data Set, encapsulated in a ZIP File, through email.

Two Application Profiles support all defined Media Storage SOP Classes.
These are intended to be used for the interchange of Composite SOP
Instances via email for general purpose applications. Objects from
multiple modalities may be included on the same email. The email may
also include non-DICOM objects. One of these general profiles supports
encryption of the email.

A detailed list of the Media Storage SOP Classes is defined in

The other application profile is specialized for dental applications and
adds mandatory requirements for dental images to the general secure
email profile.

The specific Application Profiles are shown in
`table_title <#table_L.1-1>`__:

.. table:: STD-x-ZIP-MAIL Application Profiles

   +----------------------+----------------------+----------------------+
   | **Application        | **Identifier**       | **Description**      |
   | Profile**            |                      |                      |
   +======================+======================+======================+
   | General Purpose ZIP  | STD-GEN-ZIP-MAIL     | Interchange of       |
   | Email                |                      | Composite SOP        |
   |                      |                      | Instances by email.  |
   +----------------------+----------------------+----------------------+
   | General Purpose      | STD-GEN-SEC-ZIP-MAIL | Interchange of       |
   | Secure ZIP Email     |                      | Composite SOP        |
   |                      |                      | Instances by         |
   |                      |                      | encrypted email.     |
   +----------------------+----------------------+----------------------+
   | Dental Radiograph    | STD-DTL-SEC-ZIP-MAIL | Interchange of       |
   | ZIP Email            |                      | dental radiographic  |
   |                      |                      | images by encrypted  |
   |                      |                      | email                |
   +----------------------+----------------------+----------------------+

.. _sect_L.2:

Clinical Context
----------------

These Application Profiles facilitate the interchange of images and
related data through email.

The STD-GEN-ZIP-MAIL and STD-GEN-SEC-ZIP-MAIL profiles are intended for
general purpose applications. They are not intended as a replacement for
specific Application Profiles that may be defined for a particular
clinical context. The STD-DTL-SEC-ZIP-MAIL profile is intended for the
clinical context of the exchange of dental radiographs.

.. note::

   It is possible to use email transport without using the encrypted
   secure profile. This would make sense for mailing DICOM objects that
   do not need protection.

.. _sect_L.2.1:

Roles
~~~~~

.. _sect_L.2.1.1:

File Set Creator
^^^^^^^^^^^^^^^^

The role of File Set Creators shall be used by Application Entities that
generate a File-set under any of the profiles listed in
`table_title <#table_L.1-1>`__. Typical entities that will use this role
would include systems assigned to send images by email attachment to
other systems. File Set Creators shall be able to generate the DICOMDIR
directory file, and any supported DICOM Storage SOP Class Information
Object files.

.. _sect_L.2.1.2:

File Set Reader
^^^^^^^^^^^^^^^

The role of File Set Reader shall be used by Application Entities that
receive a transferred File Set. File Set Readers shall be able to read
the DICOMDIR directory file and all Information Objects defined for the
specific Application Profiles, using the defined Transfer Syntaxes.

.. _sect_L.2.1.3:

File Set Updater
^^^^^^^^^^^^^^^^

The role of File Set Updater is not defined for these Application
Profiles.

.. _sect_L.3:

General Class Profile
---------------------

.. _sect_L.3.1:

STD-GEN-ZIP-MAIL and STD-GEN-SEC-ZIP-MAIL Abstract and Transfer Syntaxes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Applications interchanging data under the STD-GEN-ZIP-MAIL and
STD-GEN-SEC-ZIP-MAIL profiles shall support the Information Object
Definitions (IOD) and Transfer Syntaxes for the Media Storage SOP Class
specified in `table_title <#table_L.3-1>`__.

.. table:: STD-GEN-ZIP-MAIL and STD-GEN-SEC-ZIP-MAIL SOP Classes and
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
   | Composite   | *See*       | Defined in  | Defined in  | Defined in  |
   | Image &     |             | Conformance | Conformance | Conformance |
   | Stand-alone |             | Statement   | Statement   | Statement   |
   | Storage     |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+

Equipment claiming conformance to these Application Profiles shall list
the subset of Media Storage SOP Classes and Transfer Syntaxes that it
supports in its Conformance Statement.

.. _sect_L.3.2:

Medium Format
~~~~~~~~~~~~~

The STD-GEN-ZIP-MAIL and STD-GEN-SEC-ZIP-MAIL application profiles shall
use the ZIP File Media interchanged using the Email Media format as
defined in . This Email media shall comply with the following
requirements:

a. The content shall be identified as: Content-Type: application/zip

b. The attachment shall be identified as: id="DICOM.ZIP";
   name="DICOM.ZIP"

c. The disposition shall be: Content-Disposition: attachment;
   filename="DICOM.ZIP"

d. The email shall not be compressed.

e. The subject line shall contain the phrase:DICOM-ZIP

.. note::

   An additional content type, file extension and file name may be
   defined by the Standard in the future to accommodate a DICOM specific
   zip file.

.. _sect_L.3.3:

Directory Information in DICOMDIR
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Directory shall include Directory Records of PATIENT, STUDY, SERIES,
IMAGE corresponding to the information object files in the File Set. All
DICOM files in the File Set incorporating SOP Instances (Information
Objects) defined for the specific Application Profile shall be
referenced by Directory Records.

.. note::

   DICOMDIRs with no directory information are not allowed by these
   Application Profiles.

There may only be one DICOMDIR file per File Set. The Patient ID at the
patient level shall be unique for each patient directory record in one
File Set.

.. _sect_L.3.3.1:

Additional Keys
^^^^^^^^^^^^^^^

No additional keys are specified.

.. _sect_L.3.4:

Secure Transport
~~~~~~~~~~~~~~~~

The Email Media interchange under the STD-GEN-SEC-ZIP-MAIL profile shall
use the Secure Use of Email Transport profile specified in .

.. _sect_L.4:

Dental Class Profile
--------------------

.. _sect_L.4.1:

STD-DTL-SEC-ZIP-MAIL Abstract and Transfer Syntaxes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Applications interchanging data under the STD-DTL-SEC-ZIP-MAIL profile
shall support the Information Object Definitions (IOD) and Transfer
Syntaxes for the Media Storage SOP Class specified in
`table_title <#table_L.3-2>`__. File Set Creators for the
STD-FTL-SEC-ZIP-MAIL shall support at least one of the optional IODs.

.. table:: STD-DTL-SEC-ZIP-MAIL Abstract and Transfer Syntaxes

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

.. _sect_L.4.2:

Medium Format
~~~~~~~~~~~~~

The STD-DTL-SEC-ZIP-MAIL application profile shall use the ZIP File
Media interchanged using the Email Media format as defined in . This
Email media shall comply with the following requirements:

a. The content shall be identified as: Content-Type: application/zip

b. The attachment shall be identified as: id="DICOM.ZIP";
   name="DICOM.ZIP"

c. The disposition shall be: Content-Disposition: attachment;
   filename="DICOM.ZIP"

d. The email shall not be compressed.

e. The subject line shall contain the phrase:DICOM-ZIP

.. note::

   An additional content type, file extension and file name may be
   defined by the Standard in the future to accommodate a DICOM specific
   zip file.

.. _sect_L.4.3:

Directory Information in DICOMDIR
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Directory shall include Directory Records of PATIENT, STUDY, SERIES,
IMAGE corresponding to the information object files in the File Set. All
DICOM files in the File Set incorporating SOP Instances (Information
Objects) defined for the specific Application Profile shall be
referenced by Directory Records.

.. note::

   DICOMDIRs with no directory information are not allowed by these
   Application Profiles.

There may only be one DICOMDIR file per File Set. The Patient ID at the
patient level shall be unique for each patient directory record in one
File Set.

.. _sect_L.4.4.1:

Additional Keys
^^^^^^^^^^^^^^^

No additional keys are specified.

.. _sect_L.4.5:

Specific Image Requirements For STD-DTL-SEC-ZIP-MAIL
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

For Digital Intra-oral X-Ray Image and Digital X-Ray Image Instances
interchanged under the STD-DTL-SEC-ZIP-MAIL profile, the Attributes
listed in `table_title <#table_L.4-1>`__ used within the image instances
shall take the values specified.

.. table:: STD-DTL-ZIP-MAIL - Required Image Attribute Values

   +----------------+-------------+-------------------------------------+
   | **Attribute**  | **Tag**     | **Value**                           |
   +================+=============+=====================================+
   | Bits Allocated | (0028,0100) | If Bits Stored (0028,0101) is 8,    |
   |                |             | then 8; otherwise 16.               |
   +----------------+-------------+-------------------------------------+
   | Bits Stored    | (0028,0101) | 8, 10, 12 or 16                     |
   +----------------+-------------+-------------------------------------+

The Attributes listed in `table_title <#table_L.4-2>`__ shall have their
Types specialized.

.. table:: STD-DTL-ZIP-MAIL - Required Image Attribute Types

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

.. _sect_L.4.6:

Secure Transport
~~~~~~~~~~~~~~~~

The Email Media interchange under the STD-DTL-SEC-ZIP-MAIL profiles
shall use the Secure Use of Email Transport profile specified in .

