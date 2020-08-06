.. _chapter_F:

120mm CD-R Medium (Normative)
=============================

The terms "CD-R" and "CD-WO" refer to the same medium and are used
interchangeably. Originally this medium was designated CD-WO, but the
most common vernacular today is CD-R. There are mixed references in this
annex to accommodate the common CD-R usage unless a specific reference
to CD-WO is required to reflect the historical documents accurately. The
term "CD-ROM," when used in reference to a disc, is a disc fabricated
with all the digital data already on it. "CD-R" media is a fabricated
blank, with the ability to have digital data written to it. The term
"CD-ROM" is also used to refer to a CD reader, e.g., "CD-ROM drive." A
CD-ROM drive can read either CD-R discs or CD-ROM discs.

.. note::

   Capitalization in this annex is inconsistent with other DICOM
   standards in order to be consistent with historical usage for terms.

.. _sect_F.1:

DICOM Mapping to Media Format
-----------------------------

Only one File-set shall be stored onto a single CD-R.

.. _sect_F.1.1:

DICOM File-set
~~~~~~~~~~~~~~

The ISO 9660 Standard provides a Volume Identifier in byte position 41
to 72 of the Primary Volume Descriptor. A DICOM File-Set is defined to
be one volume, and the File-Set ID shall be placed in the Volume
Identifier, starting with byte position 41. Extra bytes within the
Volume Identifier shall be spaces (20H).

The Volume Identifier for a File-Set ID consisting of zero characters
shall consist of all spaces (20H).

.. note::

   1. The character set for File IDs and File-set IDs (see ) is a subset
      of the ISO 9660 character set, therefore no further restrictions
      need to be imposed.

   2. Multiple ISO 9660 File-Sets on a single volume are achievable, but
      this profile does not support multiple file-sets.

.. _sect_F.1.2:

DICOM File ID Mapping
~~~~~~~~~~~~~~~~~~~~~

The ISO 9660 standard provides a hierarchical structure for directories
and files within directories. Each volume has a root directory that may
contain references to both files and sub-directories. Sub-directories
may contain reference to both files and other sub-directories.

.. _sect_F.1.2.1:

File ID
^^^^^^^

A volume may have at most 8 levels of directories, where the root
directory is defined as level 1. The nomenclature for referring to a
file in the ISO 9660 standard is dependent upon the receiving system.
For the purposes of this document, the following notation will be used:

a. / - For the root directory

b. /FILENAME.;1 - For a file in the root directory

c. /SUBDIR - For a sub-directory in the root directory

d. /SUBDIR/FILENAME.;1 - For a file in the sub-directory

Given a File ID consisting of N components, referred to as Comp1 through
CompN, then the corresponding ISO 9660 file shall be named
/Comp1/.../CompN.;1

The ISO 9660 File Name Extension shall not be used.

The ISO 9660 standard requires the two separators "." and ";" to
demarcate a "File Name Extension" and a "Version Number". To remain
compatible with the ISO standard, the version number shall be 1.

.. note::

   1. The above specified file ID mapping corresponds to ISO 9660 Level
      1 compliance. This ensures the greatest level of compatibility
      across receiving systems.

   2. The following is an example of the DICOM to ISO 9660 file mapping:

      ================= ======================
      **DICOM File ID** **ISO 9660 File Name**
      ================= ======================
      DICOMDIR          /DICOMDIR.;1
      SUBDIRA\IMAGE1    /SUBDIRA/IMAGE1.;1
      ================= ======================

   3. The ISO 9660 File Name written on the media as described above is
      not necessarily the name that an application will use in
      interacting with an operating system or CD-R writing utility. For
      example, the application will generally create a directory
      structure, and the OS or utility will create the correct full path
      file names with "/" characters. Similarly, the application
      generally will not need to append the dot character and ";1"
      version identifier to the name, as these will be added by the OS
      or utility to create an ISO 9660 compliant File Name. In fact, if
      the application appends ";1" to the name, and the OS or utility
      supports the Rock Ridge or Joliet extensions, those characters may
      be interpreted as part of the application specified file name
      rather than the file version identifier; a further file version
      identifier may be appended, resulting in an incorrect file name
      such as "/DICOMDIR.;1.;1".

.. _sect_F.1.2.2:

DICOMDIR File
^^^^^^^^^^^^^

A DICOMDIR file in a DICOM File-set shall reside in the root directory
of the directory hierarchy, and shall be named /DICOMDIR.;1.

Multiple DICOMDIR files shall not be stored on a single volume under
this annex.

.. _sect_F.1.3:

DICOM File Management Information
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A Directory record in ISO 9660 provides for a Recording Data and Time
field, which shall be set to the creation date of the file.

File modification data, file owner identification, and permissions are
part of the ISO 9660 - Extended Attribute Record. The Extended Attribute
Record is not required by this annex and shall be ignored at this time.
To ensure future backwards compatibility and file accessibility, the
Extended Attribute Record Length and File Flag of the Directory record
shall be set as follows for each file. The Extended Attribute Record
Length (byte position 2) shall be zero. The File Flags (byte position
26) shall have bit positions 3 and 4 set to zero.

.. _sect_F.2:

Media Formats
-------------

.. _sect_F.2.1:

Physical Format
~~~~~~~~~~~~~~~

The physical format of DICOM CD-R discs shall comply with the applicable
definitions within ISO/IEC 10149, Part II: CD-WO in Orange Book and
CD-ROM-XA (extended Architecture) (if Mode 1 sectors are not used), with
the additional modifications described in `Sector
Format <#sect_F.2.1.1>`__ and `Multi-session Format <#sect_F.2.1.2>`__.

.. _sect_F.2.1.1:

Sector Format
^^^^^^^^^^^^^

All DICOM files and all data that comprise the ISO 9660 file system of
the DICOM CD-R disc shall be stored either:

-  within Mode 1 sectors, or

-  within Mode 2, Form 1 sectors with CD-ROM-XA File Number = 0, Channel
   Number = 0 and Coding Information Byte = 0.

.. note::

   1. The physical storage capacity of a CD-R disc can be 74 minutes
      (630 MB) or 80 minutes (700 MB) when using the Mode 1 or Mode 2
      Form 1 format. The capacity is fixed by the pre-grooved spiral
      track present on a blank CD-R. Some older CD players will not be
      able to read the 80 min capacity CD-R discs.

   2. The DICOM Standard prohibits the use of Mode 2 Form 2 sectors.
      This format is used to record data on CD-Rs that exceed 74 minute
      capacity and can also be used for smaller capacity CD-Rs.
      CD-ROM-XA Mode 2 Form 2 sectors do not have sector level error
      correction. This significantly decreases the reliability of the
      media and significantly increases the likelihood of data
      corruption.

.. _sect_F.2.1.2:

Multi-session Format
^^^^^^^^^^^^^^^^^^^^

An area on the disc consisting of a Lead-In area, a Program area, and a
Lead-Out area, is called a "Session." If a disc contains or is able to
contain more than one session then this disc is called a "Multi-session"
disk. If the Lead-In area contains a pointer to the next session, then
the disc is appendable. The Lead-In and Lead-Out areas are written at
the conclusion of writing the program Area. The process of writing the
Lead-In and Lead-Out areas is commonly referred to as "Finalizing the
Session." The last recorded session contains all the information needed
to access the entire disc.

DICOM CD-R disc may contain multiple sessions. Data are added to a disc
by opening and writing a new session. A disc is non-appendable if the
last recorded session is designated as the "Final Session," as defined
in Part II: CD-WO version 2.0, Section 5.5.2.

CD-ROM readers shall support Multi-session CDs.

CD-R writers may choose to support Multi-session writing.

.. _sect_F.2.2:

Logical Format
~~~~~~~~~~~~~~

The logical format of CD-R shall conform to ISO 9660 level 1, with the
extensions described in `System Identifier Field <#sect_F.2.2.1>`__
through `System and Volume Descriptor Area <#sect_F.2.2.2>`__

.. _sect_F.2.2.1:

System Identifier Field
^^^^^^^^^^^^^^^^^^^^^^^

The ISO 9660 System Identifier Field of the PVD (Primary Volume
Descriptor) shall contain "CD-RTOS CD-BRIDGE" if a CD-I (Compact
Disc-Interactive) application is present. If a CD-I application is not
present, then this field shall be padded with space characters.

.. _sect_F.2.2.2:

System and Volume Descriptor Area
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The ISO 9660 System and Volume Descriptor Area (SVD) from the last
session points to the set of ISO 9660 Path Tables and Directory Records
that describes the file system of the DICOM CD-R disc. The SVD area
starts at the first logical sector of each session and continues through
to the first instance of the Volume Descriptor Set Terminator.

Adding, replacing or deleting files from the disc is accomplished by
opening a new session and writing within the new session new data (if
any), a new set of Path Tables, and Directory Records that reflect the
changes, and an SVD area that points to the new set of Path Tables and
Directory records.

.. _sect_F.3:

Physical Media
--------------

The physical medium shall be the 120 mm CD-R disc as defined in Part II:
CD-WO Version 2.0 in the Orange Book.

