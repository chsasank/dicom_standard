.. _chapter_X:

120 mm BD Medium (Normative)
============================

This Annex defines the use of the UDF file systems with BD media in such
a manner as to require a reader to be capable of reading all of the
physical media types and UDF file system versions that are defined in
this Annex, and a creator to be able to create at least one of those
types of media and file system.

The media types supported are BD-RE and BD-R.

.. note::

   Capitalization in this annex may be inconsistent with other DICOM
   standards in order to be consistent with historical usage for terms
   in referenced documents.

Universal Disk Format (UDF) is a profile of the ECMA 167 3rd edition
file system.

.. note::

   The ECMA 167 3rd edition is more recent than ISO 13346:1995, which is
   equivalent to ECMA 167 2nd edition.

.. _sect_X.1:

DICOM Mapping to Media Format
-----------------------------

.. _sect_X.1.1:

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

.. _sect_X.1.2:

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

Only a single UDF Partition shall be present on each side of the media.

.. note::

   Both sides of a single piece of media may be used for storing DICOM
   data, when separate DICOM File-sets are created.

.. _sect_X.1.3:

DICOM File ID Mapping
~~~~~~~~~~~~~~~~~~~~~

The UDF Standard provides a hierarchical structure for directories and
files within directories. Each volume has a root directory that may
contain references to both files and sub-directories. Sub-directories
may contain reference to both files and other sub-directories.

.. _sect_X.1.3.1:

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

The maximum number of levels of a Resolved Path name in a UDF file-set
shall be at most 8 levels, to comply with the definition of a DICOM
File-set in .

The File Version Number is always equal to 1, as specified by UDF.

.. _sect_X.1.3.2:

DICOMDIR File
^^^^^^^^^^^^^

A DICOMDIR file in a DICOM File-set shall reside in the root directory
of the directory hierarchy, as specified in .

.. _sect_X.1.4:

DICOM File Management Information
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

No file management information beyond that specified in the UDF File
Entry is required. In particular no Extended Attributes or Named Streams
are required.

.. _sect_X.2:

File system
-----------

.. _sect_X.2.1:

UDF File System
~~~~~~~~~~~~~~~

The reader shall be able to read a logical format conforming to UDF 2.5
on BD-RE media and shall be able to read a logical format conforming to
UDF 2.6 on BD-R media.

The creator shall be able to create a logical format conforming to UDF
2.5 on BD-RE media and shall be able to create a logical format
conforming to UDF 2.6 on BD-R media.

The updater shall be able to update a logical format conforming to UDF
2.5 on BD-RE media and shall be able to update a logical format
conforming to UDF 2.6 on BD-R media, without updating the UDF revision
level of the file system already recorded on the media.

Options or extensions defined in UDF are required or restricted as
specified in the following sub-sections, and in the media specific
sub-sections.

.. note::

   1. Though the names of the files within the DICOM File-set are
      restricted by , other files on the media may have longer file
      names up to 255 characters, which is the maximum for UDF 2.5 and
      UDF 2.6.

   2. A Pseudo Overwrite Method is defined in the BD-R standard. It is
      used to make Write-Once media behave like rewritable media, hence
      sector format compatibility is ensured without multi-session or
      packet-written format. BD drives support Pseudo Overwrite
      management for BD-R. For Pseudo Overwrite Method the UDF version
      must be 2.6.

.. _sect_X.2.1.1:

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

.. _sect_X.2.1.2:

Virtual Partition Maps and Allocation Tables
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Creators and updaters shall not write UDF Virtual Partition Maps and
Virtual Allocation Tables on BD-RE and BD-R media, since pseudo
overwrite management is performed in the drive.

.. _sect_X.2.1.3:

Sparable Partition Maps and Sparing Tables
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Creators and updaters shall not write UDF Sparable Partition Maps and
Sparing Tables on BD-RE and BD-R media, since defect management is
performed in the drive.

.. _sect_X.2.1.4:

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

.. _sect_X.2.1.5:

Permissions and File Characteristics
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Creators and updaters shall always create permissions for files within
the DICOM File Set such that all users may create, read, write and
delete all files, and all users may access, create, modify and delete
all directories on all systems.

.. note::

   1. These requirements are equivalent to setting a Unix permission of
      644 for files and 755 for directories.

   2. The intent of these requirements is that for DICOM interchange
      media, implementation specific access control is not used or
      required.

The UDF File Identifier Descriptor for files within the DICOM File Set
shall not specify a File Characteristic of "hidden."

.. _sect_X.2.1.6:

File Types
^^^^^^^^^^

The UDF File Types within the DICOM File Set shall only be files (that
is a File Type of 0, meaning unspecified interpretation) or symbolic
links to files (that is a File Type of 12).

.. _sect_X.3:

Media Formats
-------------

.. _sect_X.3.1:

Blu-ray Disc™
~~~~~~~~~~~~~

.. _sect_X.3.1.1:

BD Physical Format
^^^^^^^^^^^^^^^^^^

The physical format of BD media shall comply with one of the following
applicable definitions:

-  Blu-ray Disc™ Association. White Paper Blu-ray Disc™ Format 1.A
   Physical Format Specifications for BD-RE (2nd Edition, February
   2006).

-  Blu-ray Disc™ Association. White Paper Blu-ray Disc™ Recordable
   Format Part 1 Physical Specifications (February 2006).

.. _sect_X.3.1.1.1:

BD Sector Format
''''''''''''''''

The sector format of BD media shall comply with one of the following
applicable definitions:

-  OSTA Universal Disk Format Specification (UDF) Version 2.5. April 30,
   2003.

-  OSTA Universal Disk Format Specification (UDF) Version 2.6. March 1,
   2005.

.. note::

   BD-RE is a truly random access medium, providing random access to
   fixed length sectors, hence no multi-session is applicable and
   packet-written format is not necessary.

.. _sect_X.3.1.2:

BD Logical Format
^^^^^^^^^^^^^^^^^

There are no requirements, restrictions, options or extensions to the
logical format that are specific to this media type, beyond those
specified in `File system <#sect_X.2>`__.

.. _sect_X.3.1.3:

BD Physical Media
^^^^^^^^^^^^^^^^^

The physical medium shall be the 120 mm BD medium as defined in one of
the following:

-  Blu-ray Disc™ Association. White Paper Blu-ray Disc™ Format 1.A
   Physical Format Specifications for BD-RE (2nd Edition, February
   2006).

-  Blu-ray Disc™ Association. White Paper Blu-ray Disc™ Recordable
   Format Part 1 Physical Specifications (February 2006).
