.. _chapter_A:

PC File System (Normative)
==========================

.. _sect_A.1:

PC File System Mapping to Media Formats
---------------------------------------

Several of the removable media utilize the PC file system. For any media
that use the PC file system, the following rules apply, except as
overridden in the applicable annex.

.. _sect_A.1.1:

File-set ID Mapping
~~~~~~~~~~~~~~~~~~~

The PC File System mapping does not provide a File-set ID.

.. note::

   On systems that permit user access to the media volume label, the
   volume label can be used to provide a File-set ID. Not all operating
   systems permit routine user access to this information.

.. _sect_A.1.2:

File ID Mapping
~~~~~~~~~~~~~~~

The PC File System provides a hierarchical structure for directories and
files within directories. Each structure has a root directory that may
contain references to both files and sub-directories. Sub-directories
may contain references to both files and other sub-directories. The
nomenclature for referring to files and directories in the PC File
System is:

a. \\ - For the root directory

b. \\filename - For a file in the root directory

c. \\subdir\filename - For a file in the sub-directory subdir

The PC File System name corresponding to a File ID shall be the DICOM
File ID prefixed with the character "\", with the "\" character
separating File ID components.

.. note::

   Example File ID mappings:

   =============== =======================
   **File ID**     **PC File system name**
   =============== =======================
   DICOMDIR        \\DICOMDIR
   FILENAME        \\FILENAME
   SUBDIR\FILENAME \\SUBDIR\FILENAME
   =============== =======================

The DICOMDIR file shall be in the root directory for media that do not
support multiple file-sets on a single medium. DICOMDIR location is
described for the multiple file-set situation in the annex for such
media.

.. note::

   It is recommended but not required that the File-set Descriptor File
   ID (0004,1141) be "README" (see ).

.. _sect_A.1.3:

File Management Information
~~~~~~~~~~~~~~~~~~~~~~~~~~~

The PC File System provides the following information for each file:

.. table:: PC File System File Information

   ========= =======================================
   Filename  1 to 8 characters
   Extension 0 to 3 characters
   Time      Time of last modification (or creation)
   Date      Date of last modification (or creation)
   Size      Size of file (in bytes)
   ========= =======================================

The PC File System Filename shall correspond to a DICOM File ID
Component. The PC File System Extension for a DICOM file shall not
contain any characters. The PC File System date and time shall be used
to provide the DICOM facilities for examining the modification or
creation date and time. Unused characters in Filename and Extension (see
`table_title <#table_A.1-1>`__) should be filled with null characters.

.. note::

   1. The PC File System does not specify or control the time base used
      for date and time. Coordination of reference time zones is outside
      the scope of this Standard.

   2. The typical written form of a filename is filename.extension
      (e.g., "FILE.EXT"). The period between filename and extension is a
      convention used in most programs for entering and displaying the
      filename and extension. The period is not actually recorded on
      disk and is not permitted as part of a filename. A file with no
      extension is recorded as a file with zero extension characters
      (i.e., all null filled) although it is often written and displayed
      without the period.

The PC File system does not provide ownership or access control
facilities. Write protection is addressed in the relevant physical media
specific annex. Protection mechanisms are not available for the generic
PC File System.

.. _sect_A.2:

Logical Format
--------------

The PC File System requires that the media be organized into sectors.
The media specific value for bytes/sector and the mechanism for doing
this is in each media annex.

The PC File System shall be organized as an "mtools" unpartitioned file
system (see Note), using either 12-bit or 16-bit File Allocation Table
(FAT). The layout of the boot sector shall be as shown in
`table_title <#table_A.2-1>`__. The FAT and related file structures are
compatible with the DOS 4.0 and later file systems, and are described in
detail in the Microsoft MS-DOS Programmer's Reference. Two byte integers
shall be encoded in little endian.

.. note::

   A PC File system may be either unpartitioned or partitioned.
   Traditionally, removable media such as floppy disks have been
   formatted as unpartitioned, and fixed media like hard disks have been
   formatted with a different form of Master Boot Record that specifies
   several partitions, each of which has the format of a complete
   unpartitioned system. When forms of removable media with larger
   capacity were introduced, some driver vendors chose to format them as
   unpartitioned, and others as partitioned. In order to facilitate
   interoperability with existing implementations this Part of the DICOM
   Standard currently specifies one format, the unpartitioned format.
   Some implementations of the PC DOS file system may experience
   difficulty reading or writing to large capacity unpartitioned
   removable media, and require special drivers.

The boot sector, sector 0 of track 0, shall be formatted as follows:

.. table:: Boot Sector

   +-------------+------------+-----------------------------------------+
   | **Byte(s)** | **Value**  | **Description**                         |
   +=============+============+=========================================+
   | 00 - 02     | varies     | Jump instruction to loader (NOPs) (see  |
   |             |            | note 1)                                 |
   +-------------+------------+-----------------------------------------+
   | 03 - 10     | "dddddddd" | The formatting DOS (vendor specific)    |
   |             |            | (see note 2)                            |
   +-------------+------------+-----------------------------------------+
   | 11 -12      | see note 5 | bytes/sector                            |
   +-------------+------------+-----------------------------------------+
   | 13          | see note 5 | sectors/cluster                         |
   +-------------+------------+-----------------------------------------+
   | 14 - 15     | 0001H      | 1 sector in boot record                 |
   +-------------+------------+-----------------------------------------+
   | 16          | 02H        | 2 File Allocation Tables (FAT) (see     |
   |             |            | note 3)                                 |
   +-------------+------------+-----------------------------------------+
   | 17 - 18     | 200H       | 512 root directory entries              |
   +-------------+------------+-----------------------------------------+
   | 19 - 20     | 0000H      | Flag for more than 65536 sector/disk.   |
   |             |            | Use offset 32 value                     |
   +-------------+------------+-----------------------------------------+
   | 21          | see note 5 | Flag for disk type; F0H if not          |
   |             |            | otherwise specified                     |
   +-------------+------------+-----------------------------------------+
   | 22 -23      | varies     | sectors/FAT                             |
   +-------------+------------+-----------------------------------------+
   | 24 - 25     | see note 6 | sectors/track                           |
   +-------------+------------+-----------------------------------------+
   | 26 - 27     | see note 6 | side (head) per disk                    |
   +-------------+------------+-----------------------------------------+
   | 28 - 31     | 00000000   | 0 reserved or hidden sectors            |
   +-------------+------------+-----------------------------------------+
   | 32 - 35     | varies     | Total sector/disk. Varies from disk to  |
   |             |            | disk                                    |
   +-------------+------------+-----------------------------------------+
   | 36 - 37     | 0000       | Physical Drive number = 0               |
   +-------------+------------+-----------------------------------------+
   | 38          | 29H        | Extended boot record signature = 41     |
   +-------------+------------+-----------------------------------------+
   | 39 - 42     | undefined  | Volume serial number (see note 4)       |
   +-------------+------------+-----------------------------------------+
   | 43 - 53     | varies     | The volume ID (vendor specific)         |
   +-------------+------------+-----------------------------------------+
   | 54 - 61     | varies     | The file system label                   |
   +-------------+------------+-----------------------------------------+
   | 62 - 509    | varies     | Don't care. Any contents acceptable     |
   +-------------+------------+-----------------------------------------+
   | 510         | 55H        | Signature flag - first byte             |
   +-------------+------------+-----------------------------------------+
   | 511         | AAH        | Signature flag - second byte            |
   +-------------+------------+-----------------------------------------+

.. note::

   1. These three bytes should either be EBH,00H,90H (indicating a
      relative jump) or 909090H indicating NOPs. The bytes are for
      booting off the optical drive, which DICOM does not standardize.
      Some programs use them to validate the disk. The use of EB0090H is
      known to be more commonly used and is the recommended choice.
      Readers of DICOM disks that use the PC File System should ignore
      this field.

   2. While eight characters appear to be valid in this field, the use
      of "MSDOS4.0" is known to be the preferred choice for this string.
      Some systems, upon finding this field not set to "MSDOS4.0" will
      ignore the sectors/FAT field and use their own calculation. This
      may cause an error due to the calculation resulting in a different
      value than the sectors/FAT field. (MS-DOS is a trademark of
      Microsoft)

   3. Two FATs are recommended. One FAT could also be used but again may
      cause some incompatibility.

   4. The serial number may be any four bytes. A random or sequential
      number is preferred but is not required.

   5. These values are specified in the annex for each particular type
      of media.

   6. These values are nominally specified in the Annex for each
      particular type of media, but vary considerably between
      implementations, and should not affect interoperability.

