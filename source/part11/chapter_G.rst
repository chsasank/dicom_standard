.. _chapter_G:

General Purpose MIME Interchange Profile (Normative)
====================================================

.. _sect_G.1:

Profile Identification
----------------------

This Annex defines an Application Profile Class including all defined
Media Storage SOP Classes. This class is intended to be used for the
interchange of Composite SOP Instances via e-mail for general purpose
applications.

.. note::

   This Media Storage Application Profile Class is not intended to
   replace the more robust DICOM Storage Service Class.

Objects from multiple modalities may be included on the same e-mail. A
detailed list of the Media Storage SOP Classes that may be supported is
defined in .

.. table:: STD-GEN-MIME Profile

   +-------------------------+----------------+-------------------------+
   | **Application Profile** | **Identifier** | **Description**         |
   +=========================+================+=========================+
   | General Purpose MIME    | STD-GEN-MIME   | Handles interchange of  |
   | Interchange             |                | Composite SOP Instances |
   |                         |                | by e-mail.              |
   +-------------------------+----------------+-------------------------+

The identifier for this General Purpose MIME Interchange profile shall
be STD-GEN-MIME.

Equipment claiming conformance to this Application Profile shall list
the subset of Media Storage SOP Classes that it supports in its
Conformance Statement.

.. note::

   Since it is not required to support all Media Storage Classes the
   user should carefully consider the subset of supported Media Storage
   SOP Classes in the Conformance Statements of such equipment to
   establish effective object interchange.

.. _sect_G.2:

Clinical Context
----------------

This Application Profile facilitates the interchange of images and
related data through e-mail.

This profile is intended only for general purpose applications. It is
not intended as a replacement for specific Application Profiles that may
be defined for a particular clinical context.

.. note::

   The present Application Profile does not include any specific
   mechanism regarding privacy. However it is highly recommended to use
   secure mechanisms (e.g., S/MIME) when using STD-GEN-MIME Application
   Profile over networks that are not otherwise secured.

.. _sect_G.2.1:

Roles and Service Class Options
-------------------------------

This Application Profile uses the Media Storage Service Class defined in
.

The Application Entity shall support one or two of the roles of File Set
Creator (FSC) and File Set Reader (FSR), defined in . Because the
exchange of e-mail does not involve storage, the role of File Set
Updater (FSU) is not specified.

.. _sect_G.2.1.1:

File Set Creator
~~~~~~~~~~~~~~~~

The role of File Set Creator may be used by Application Entities that
generate a File Set under this Interchange Class of Application
Profiles.

File Set Creators may be able to generate the Basic Directory SOP Class
in the DICOMDIR file with all the subsidiary Directory Records related
to the Image SOP Classes included in the File Set.

The Application Entity acting as a File Set Creator generates a File Set
under the STD-GEN-MIME Application Profile.

.. note::

   A multiple volume (i.e., a logical volume that can cross multiple
   media) is not supported by this class of Application profile. Because
   MIME is a virtual medium and since e-mail mechanisms include some way
   of fragmenting MIME parts to be sent through limited size e-mail,
   there are no needs for multiple volume.

.. _sect_G.2.1.2:

File Set Reader
~~~~~~~~~~~~~~~

The role of File Set Reader shall be used by Application Entities that
receive an exchanged File Set under the Image Interchange Class of
Application Profiles.

File Set Readers may be able to read the DICOMDIR directory file and
shall be able to read all the SOP Instance files defined for this
Application Profile, using the Transfer Syntaxes specified in the
Conformance Statement.

.. _sect_G.3:

STD-GEN-MIME Profile
--------------------

.. _sect_G.3.1:

SOP Classes and Transfer Syntaxes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This Application Profile is based on the Media Storage Service Class
(see ).

.. table:: STD-GEN-MIME SOP Classes and Transfer Syntaxes

   +-------------+-------------+-------------+-------------+-------------+
   | **          | **SOP Class | **Transfer  | **FSC       | **FSR       |
   | Information | UID**       | Syntax and  | Re          | Re          |
   | Object      |             | UID**       | quirement** | quirement** |
   | D           |             |             |             |             |
   | efinition** |             |             |             |             |
   +=============+=============+=============+=============+=============+
   | Basic       | 1.2.840.1   | Explicit VR | Optional    | Optional    |
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

The SOP Classes and corresponding Transfer Syntax supported by this
Application Profile are specified in the `table_title <#table_G.3-1>`__.
The supported Storage SOP Class(es) and Transfers Syntax(es) shall be
listed in the Conformance Statement using a table of the same form.

.. _sect_G.3.2:

Physical Medium and Medium Format
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The STD-GEN-MIME application profile requires the DICOM MIME medium as
defined in .

.. _sect_G.3.3:

Directory Information in DICOMDIR
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If the DICOMDIR is included, conformant Application Entities shall
include in it the Basic Directory IOD containing Directory Records at
the Patient and the subsidiary Study and Series levels, appropriate to
the SOP Classes in the File Set.

All DICOM files in the File Set incorporating SOP Instances defined for
the specific Application Profile shall be referenced by Directory
Records.

.. note::

   1. DICOMDIRs with no directory information are not allowed by this
      Application Profile.

   2. In the DICOMDIR each object may be referenced by a referenced file
      ID (e.g., 000/000) that contains multiple values corresponding to
      a path for physical system, since the MIME organization is flat.
      There is no requirement that this path will be used by the
      receiving application to create file hierarchy.

There may only be one DICOMDIR file per File Set. The Patient ID at the
patient level shall be unique for each patient directory record in one
File Set.

.. _sect_G.3.3.1:

Additional Keys
^^^^^^^^^^^^^^^

No additional keys are specified.

