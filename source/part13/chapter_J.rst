.. _chapter_J:

UDF on 120 mm DVD-RAM Medium (Normative)
========================================

This Annex defines the use of the UDF 1.5 file system with DVD-RAM
media.

.. note::

   1. Capitalization in this Annex may be inconsistent with usage
      elsewhere in the DICOM Standard in order to be consistent with
      historical usage for terms in referenced documents.

   2. DVD-ROM is a pre-mastered medium, that is it is manufactured
      rather than written on a one-off basis by a medical device. While
      it is likely that a device conforming to this Annex will be able
      to read a UDF file system from DVD-ROM, it is not a requirement.

Universal Disk Format (UDF) version 1.5 is a profile of the ECMA 167 3rd
edition file system.

.. note::

   1. The ECMA 167 3rd edition is more recent than ISO 13346:1995, which
      is equivalent to ECMA 167 2nd edition.

   2. Though later revisions of UDF such as 2.0 are defined with
      additional features compared to 1.5, these features are not
      required to support recording of a DICOM file set.

   3. A reader of a UDF 2.0 file system can also read a 1.5 or 1.02 file
      system.

   4. A UDF 1.02 reader cannot read the Virtual Allocation Table (VAT)
      used to incrementally write a UDF 1.5 or later disk.

   5. A UDF 1.5 file system reader can theoretically read those
      structures of a UDF 2.0 file system that are common to both
      versions. However, a UDF 1.5 reader cannot read the Named Streams
      or extended file entries that may be recorded on a UDF 2.0 file
      system.

      Since a UDF 1.5 reader may completely reject a 2.0 disk based on
      the version number written on the media, without attempting to
      read compatible structures of the file system, it is not permitted
      to write DICOM media with a version greater than 1.5.

   6. A writer (FSC or FSU) is not permitted to add structures from a
      later version of UDF to a file system that has been created with
      an earlier version of the file system.

.. _sect_J.1:

DICOM Mapping to Media Format
-----------------------------

.. _sect_J.1.1:

Media Character Set
~~~~~~~~~~~~~~~~~~~

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

.. _sect_J.1.2:

DICOM File-set
~~~~~~~~~~~~~~

One and only one DICOM File-set shall be stored on each side of a single
piece of media.

A DICOM File-set is defined to be completely contained within one UDF
File-set.

Only a single UDF File-set shall be present in the UDF Volume.

Each side of the media will comprise a single self-contained UDF Volume.
That is the UDF Volume Set shall not consist of more than one UDF
Volume.

Only a single UDF Partition shall be present on each side the media.

.. note::

   Other partitions containing other file systems, possibly sharing the
   same data, may be present, such as an ISO-9660 bridge disk, a Mac HFS
   or Unix UFS hybrid disk, etc.

.. _sect_J.1.3:

DICOM File ID Mapping
~~~~~~~~~~~~~~~~~~~~~

The UDF Standard provides a hierarchical structure for directories and
files within directories. Each volume has a root directory that may
contain references to both files and sub-directories. Sub-directories
may contain reference to both files and other sub-directories.

.. _sect_J.1.3.1:

File ID
^^^^^^^

defines a DICOM File ID Component as a string of 8 characters from a
subset of the G0 repertoire of ISO 8859. Each of these File ID
Components is mapped to a UDF File Identifier or Path Component in the
OSTA CS0 character set.

.. note::

   This mapping is a subset of the MS-DOS mapping specified in UDF.

Filename extensions are not used in DICOM File ID Components, hence a
UDF File Identifier shall not contain a File Extension or the '.' that
would precede such a File Extension.

The maximum number of levels of a Resolved Pathname in a UDF file-set
shall be at most 8 levels, to comply with the definition of a DICOM
File-set in .

The File Version Number is always equal to 1, as specified by UDF.

.. note::

   This file ID mapping is also compatible with ISO 9660 Level 1.

.. _sect_J.1.3.2:

DICOMDIR File
^^^^^^^^^^^^^

A DICOMDIR file in a DICOM File-set shall reside in the root directory
of the directory hierarchy, as specified in .

.. _sect_J.1.4:

DICOM File Management Information
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

No file management information beyond that specified in the UDF File
Entry is required. In particular no Extended Attributes or Named Streams
are required.

.. _sect_J.2:

File System
-----------

.. _sect_J.2.1:

UDF File System
~~~~~~~~~~~~~~~

The reader shall be able to read a logical format conforming to UDF 1.02
or 1.5, as required by the UDF 1.5 standard.

The creator shall be able to create a logical format conforming to UDF
1.5.

The updater shall be able to update a logical format conforming to UDF
1.02 or 1.5, without updating the UDF revision level of the file system
already recorded on the media, as required by the UDF 1.5 standard.

Options or extensions defined in UDF are required or restricted as
specified in the following sub-sections, and in the media specific
sub-sections.

.. _sect_J.2.1.1:

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

.. _sect_J.2.1.2:

Virtual Partition Map and Allocation Tables
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Creators and updaters shall not write UDF Virtual Partition Maps and
Virtual Allocation Tables on DVD-RAM media.

.. _sect_J.2.1.3:

Sparable Partition Maps and Sparing Tables
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Creators and updaters shall not write UDF Sparable Partition Maps and
Sparing Tables on DVD-RAM media, since defect management is performed in
the drive.

.. _sect_J.2.1.4:

System Dependent Requirements
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The reader shall not depend on any system dependent requirements as
specified in UDF to be able to read the DICOM File-set, and shall not
behave differently if they are present. Any unrecognized system
dependent requirements shall be gracefully ignored.

.. note::

   1. For example, a particular form of file permissions, particular
      extended attributes or particular named streams may not be
      required or affect application behavior.

   2. This does not mean that Extended Attributes or Named Streams may
      not be present and associated with files within the DICOM
      File-set.

.. _sect_J.2.1.5:

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

.. _sect_J.2.1.6:

File Types
^^^^^^^^^^

The UDF File Types within the DICOM File Set shall only be files (that
is a File Type of 0, meaning unspecified interpretation) or symbolic
links to files (that is a File Type of 12).

.. _sect_J.3:

Media Formats
-------------

.. _sect_J.3.1:

DVD-RAM
~~~~~~~

.. _sect_J.3.1.1:

DVD-RAM Physical Format
^^^^^^^^^^^^^^^^^^^^^^^

The physical format of DVD-RAM media shall comply with the applicable
definitions within "DVD Specifications for Rewritable Disc (DVD-RAM
4.7GB) : Part 1 - Physical Specifications Version 2.0" with the
additional modifications described in the following sub-sections.

.. note::

   Two physical forms of DVD-RAM are available, a double-sided variety
   (Type 1), and a single-sided variety (Type 2). Only Type 2 media can
   be removed from its cartridge and inserted in a conventional DVD-ROM
   drive.

.. _sect_J.3.1.1.1:

DVD-RAM Sector Format
'''''''''''''''''''''

The sector format of DVD-RAM media shall comply with the applicable
definitions in "DVD Specifications for Rewritable Disc (DVD-RAM 4.7GB) :
Part 2 - File System Specifications Version 2.0".

DVD-RAM is a truly random access media, providing random access to fixed
length sectors, hence no multi-session or packet-written format is
applicable.

.. _sect_J.3.1.2:

DVD-RAM Logical Format
^^^^^^^^^^^^^^^^^^^^^^

There are no requirements, restrictions, options or extensions to the
logical format that are specific to this media type, beyond those
specified in `File System <#sect_J.2>`__.

.. _sect_J.3.1.3:

DVD-RAM Physical Media
^^^^^^^^^^^^^^^^^^^^^^

The physical medium shall be the 120 mm DVD-RAM medium as defined in
"DVD Specifications for Rewritable Disc (DVD-RAM 4.7GB) : Part 1 -
Physical Specifications Version 2.0".

