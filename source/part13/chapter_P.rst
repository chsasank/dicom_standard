.. _chapter_P:

120 mm DVD Medium (Normative)
=============================

This Annex defines the use of the UDF and ISO 9660 file systems with DVD
media in such a manner as to require a reader to be capable of reading
all of the physical media types and UDF and ISO 9660 file system
versions that are defined in this Annex, and a creator to be able to
create at least one of those types of media and file system.

The media types supported are DVD-ROM, DVD-R authoring and general,
DVD-RW, DVD+R and DVD+RW.

.. note::

   1. Capitalization in this annex may be inconsistent with other DICOM
      standards in order to be consistent with historical usage for
      terms in referenced documents.

   2. Mandatory support for reading both UDF and ISO 9660 is included to
      facilitate migration from legacy CD-R implementations, which use
      ISO 9660, as well as to support the industry standard file system
      for DVD, UDF.

Universal Disk Format (UDF) is a profile of the ECMA 167 3rd edition
file system.

.. note::

   1. The ECMA 167 3rd edition is more recent than ISO 13346:1995, which
      is equivalent to ECMA 167 2nd edition.

   2. A reader of a UDF 2.01 file system can also read a 2.0, 1.5 or
      1.02 file system.

.. _sect_P.1:

DICOM Mapping to Media Format
-----------------------------

.. _sect_P.1.1Media:

Character Set
~~~~~~~~~~~~~

The character set used in UDF fields shall be the CS0 OSTA Compressed
Unicode character set, required by the UDF standard.

.. note::

   1. The CS0 OSTA Unicode character set is defined in UDF and is a
      subset of Unicode 2.0.

   2. UDF defines a specific form of compression of 8 and 16 bit Unicode
      characters that must be supported.

   3. The character set defined elsewhere in this section for DICOM
      File-set fields is a subset of this character set. However other
      fields in the UDF file system, and other files in the UDF file
      system not in the DICOM File-set, may use characters beyond those
      defined by DICOM for File ID Components, including those encoded
      in 16 bits.

   4. The character set for File IDs and File-set IDs (see ) is a subset
      of the ISO 9660 character set, therefore no further restrictions
      need to be imposed for ISO 9660 file systems.

.. _sect_P.1.2:

DICOM File-set
~~~~~~~~~~~~~~

One and only one DICOM File-set shall be stored on each side of a single
piece of media.

A DICOM File-set is defined to be completely contained within one UDF or
ISO 9660 File-set.

Only a single UDF or ISO 9660 File-set shall be present in the UDF
Volume.

Each side of the media will comprise a single self-contained UDF or ISO
9660 Volume. That is the UDF or ISO 9660 Volume Set shall not consist of
more than one UDF or ISO 9660 Volume.

Only a single UDF or ISO 9660 Partition shall be present on each side
the media.

.. note::

   Other partitions containing other file systems, possibly sharing the
   same data, may be present, such as an ISO-9660 bridge disk, a Mac HFS
   or Unix UFS hybrid disk, etc.

.. _sect_P.1.3:

DICOM File ID Mapping
~~~~~~~~~~~~~~~~~~~~~

The UDF and ISO 9660 Standards provide a hierarchical structure for
directories and files within directories. Each volume has a root
directory that may contain references to both files and sub-directories.
Sub-directories may contain reference to both files and other
sub-directories.

.. _sect_P.1.3.1:

File ID
^^^^^^^

defines a DICOM File ID Component as a string of 8 characters from a
subset of the G0 repertoire of ISO 8859. Each of these File ID
Components is mapped to a UDF File Identifier or Path Component in the
OSTA CS0 character set.

.. note::

   This mapping is a subset of the MS-DOS mapping specified in UDF.

Filename extensions are not used in DICOM File ID Components, hence an
UDF or ISO 9660 File Identifier shall not contain a File Extension or
the '.' that would precede such a File Extension.

The maximum number of levels of a Resolved Pathname in a UDF or ISO 9660
file-set shall be at most 8 levels, to comply with the definition of a
DICOM File-set in .

The File Version Number is always equal to 1, as specified by UDF or ISO
9660.

.. note::

   This file ID mapping is also compatible with ISO 9660 Level 1.

.. _sect_P.1.3.2:

DICOMDIR File
^^^^^^^^^^^^^

A DICOMDIR file in a DICOM File-set shall reside in the root directory
of the directory hierarchy, as specified in .

.. _sect_P.1.4:

DICOM File Management Information
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

No file management information beyond that specified in the UDF or ISO
9660 File Entry is required. In particular no Extended Attributes or
Named Streams are required.

.. note::

   Unlike the Annex of this Part specifying CD-R media, no restrictions
   or specifications with respect to ISO 9660 Recording Date and Time,
   file modification date, file owner identification and permissions, or
   other Extended Attribute Record values are specified, since these may
   be beyond the control of the DICOM application.

.. _sect_P.2:

File System
-----------

The reader shall be able to read a logical format conforming to UDF and
ISO 9660 file systems, as defined below.

The creator shall be able to create a logical format conforming to UDF
or ISO 9660 file systems or both, as defined below.

No requirements are defined for an updater.

.. note::

   The intent of these requirements is to insist that a reader be able
   to read media created by any creator, but not to require that media
   created by a particular creator can necessarily be updated by a
   different updater.

.. _sect_P.2.1:

UDF File System
~~~~~~~~~~~~~~~

The reader shall be able to read a logical format conforming to UDF 1.02
or 1.5 or 2.0 or 2.01, as required by the UDF 2.01 standard.

The creator shall be able to create a logical format conforming to any
one of UDF 1.02 or 1.5 or 2.0 or 2.01.

Options or extensions defined in UDF are required or restricted as
specified in the following sub-sections, and in the media specific
sub-sections.

.. note::

   Though the names of the files within the DICOM File set are
   restricted by , other files on the media may have longer file names.

.. _sect_P.2.1.1:

Interchange Levels
^^^^^^^^^^^^^^^^^^

For the UDF Primary Volume Descriptor, both the Interchange Level and
Maximum Interchange Level shall always be set to 2.

.. note::

   1. This means that the volume is not and will never be, part of a
      multi-volume set.

   2. The Interchange Level and Maximum Interchange Level in the File
      Set Descriptor are defined by UDF to always be 3. This is despite
      the fact that restrictions specified for the DICOM File-set may be
      very similar to lower Interchange Levels specified in ECMA 167.

.. _sect_P.2.1.2:

Virtual Partition Map and Allocation Tables
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Creators and updaters may or may not write UDF Virtual Partition Maps
and Virtual Allocation Tables depending on the appropriate choice for
physical media.

All readers are required to support UDF Virtual Partition Maps and
Virtual Allocation Tables.

.. _sect_P.2.1.3:

Sparable Partition Maps and Sparing Tables
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Creators and updaters may or may not write UDF Sparable Partition Maps
and Sparing Tables depending on the appropriate choice for physical
media, since defect management may or may not be performed in the drive.

All readers are required to support UDF Sparable Partition Maps and
Sparing Tables.

.. _sect_P.2.1.4:

System Dependent Requirements
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The reader shall not depend on any system dependent requirements as
specified in UDF to be able to read the DICOM File-set, and shall not
behave differently if they are present. Any unrecognized system
dependent requirements shall be gracefully ignored.

Creators and updaters writing to a version of UDF that supports Named
Streams shall use the default stream to write each file within the DICOM
File-set.

.. note::

   1. For example, a particular form of file permissions, particular
      extended attributes or particular named streams may not be
      required or affect application behavior.

   2. This does not mean that Extended Attributes or Named Streams may
      not be present and associated with files within the DICOM
      File-set.

.. _sect_P.2.1.5:

Permissions and File Characteristics
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Creators and updaters shall always create permissions for files within
the DICOM File Set such that all users may read, write and delete all
files, and all users may access and delete all directories on all
systems.

.. note::

   1. These requirements are equivalent to setting a Unix permission of
      644 for files and 755 for directories.

   2. The intent of these requirements is that for DICOM interchange
      media, implementation specific access control is not used or
      required.

The UDF File Identifier Descriptor for files within the DICOM File Set
shall not specify a File Characteristic of "hidden."

.. _sect_P.2.1.6:

File Types
^^^^^^^^^^

The UDF File Types within the DICOM File Set shall only be files (that
is a File Type of 0, meaning unspecified interpretation) or symbolic
links to files (that is a File Type of 12).

.. _sect_P.2.2:

ISO 9660 File System
~~~~~~~~~~~~~~~~~~~~

The reader shall be able to read a logical format conforming to ISO 9660
Level 1, 2 and 3, with or without Rockridge or Joliet Extensions, which
may or may not be present.

The creator shall be able to create a logical format conforming to ISO
9660 Level 1, 2 or 3, and may or may not add Rockridge or Joliet
Extensions.

.. note::

   Though the files within the DICOM File set are restricted to names
   that conform to a subset of ISO 9660 Level 1, other files on the
   media may have longer file names. Unlike the Annex of this Part
   specifying CD-R media, strict Level 1 conformance of the file system
   is not required, since this has proven difficult to constrain in
   practice.

.. _sect_P.2.2.1:

Extended Attributes, Permissions and File Characteristics
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

File modification data, file owner identification, and permissions are
part of the ISO 9660 - Extended Attribute Record. Support of the
Extended Attribute Record is not required.

If Extended Attribute Records are present, all files within the DICOM
File Set shall have permissions such that all users may read all files,
and all users may access all directories on all systems.

.. note::

   The intent of these requirements is that for DICOM interchange media,
   implementation specific access control is not used or required.

.. _sect_P.3:

Media Formats
-------------

.. _sect_P.3.1:

DVD
~~~

.. _sect_P.3.1.1:

DVD Physical Format
^^^^^^^^^^^^^^^^^^^

The physical format of DVD media shall comply with one of the following
applicable definitions:

-  DVD Specifications for Recordable Disc (DVD-R for General) : Part 1 -
   Physical Specifications Version 2.0

-  DVD Specifications for Recordable Disc (DVD-R for Authoring) : Part 1
   - Physical Specifications Version 2.0

-  DVD Specifications for Read-Only Disc (DVD-ROM) : Part 1 - Physical
   Specifications Version 1.13

-  DVD Specifications for Re-Recordable (DVD-RW) : Part 1 - Physical
   Specifications Version 1.1

-  DVD+RW Physical Specifications, Version 1.1

-  DVD+R Physical Specifications, Version 1.1

.. _sect_P.3.1.1.1:

DVD Sector Format
'''''''''''''''''

The sector format of DVD media shall comply with one of the following
applicable definitions:

-  DVD Specifications for Recordable Disc (DVD-R for General) : Part 2 -
   File System Specifications Version 2.0

-  DVD Specifications for Recordable Disc (DVD-R for Authoring) : Part 2
   - File System Specifications Version 2.0

-  DVD Specifications for Read-Only Disc (DVD-ROM) : Part 2 - File
   System Specifications Version 1.13

-  DVD Specifications for Re-Recordable Disc (DVD-RW) : Part 2 - File
   System Specifications Version 1.0

-  DVD+RW Defect Management & Physical Formatting Specification, Version
   1.0

No restrictions are placed on the use of disc-at-once, track-at-once,
multi-session or packet-written format if applicable to the physical
media type, other than that any session should be finalized at the
conclusion of writing the media in order to make it readable.

.. _sect_P.3.1.2:

DVD Logical Format
^^^^^^^^^^^^^^^^^^

There are no requirements, restrictions, options or extensions to the
logical format that are specific to this media type, beyond those
specified in `File System <#sect_P.2>`__.

.. _sect_P.3.1.3:

DVD Physical Media
^^^^^^^^^^^^^^^^^^

The physical medium shall be the 120 mm DVD-R medium as defined in one
of the following:

-  DVD Specifications for Recordable Disc (DVD-R for General) : Part 1 -
   Physical Specifications Version 2.0

-  DVD Specifications for Recordable Disc (DVD-R for Authoring) : Part 1
   - Physical Specifications Version 2.0

-  DVD Specifications for Read-Only Disc (DVD-ROM) : Part 1 - Physical
   Specifications Version 1.13

-  DVD Specifications for Re-Recordable (DVD-RW) : Part 1 - Physical
   Specifications Version 1.1

-  DVD+RW Physical Specifications, Version 1.1

-  DVD+R Physical Specifications, Version 1.1

