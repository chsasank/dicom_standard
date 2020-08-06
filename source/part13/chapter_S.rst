.. _chapter_S:

CompactFlash Removable Devices
==============================

.. _sect_S.1:

DICOM Mapping to Media Formats
------------------------------

Only one DICOM file set shall be stored in the first partition of a
partitioned device. If the device is not partitioned, only one DICOM
file set shall be stored on the device.

.. _sect_S.1.1:

File System
~~~~~~~~~~~

The file system employed on these media shall be either the FAT16 file
system or the FAT32 file system. The information in the boot sector of
this partition shall be utilized by the file system to determine proper
access to this media (see Microsoft Extensible Firmware Initiative FAT32
File System Specification).

File names shall be further restricted to be in compliance with the File
ID rules specified in . The File ID shall be the same as the filename.

.. note::

   These rules limit the character set to being a subset of the DICOM
   default G0 character set, limit the file names to be no more than 8
   characters, and limit the directory tree to be no more than 8 levels
   deep. All of these restrictions are needed to comply with the most
   limited of the removable media.

.. _sect_S.2:

Media Formats
-------------

.. _sect_S.2.1:

Partitioning
~~~~~~~~~~~~

These media may be partitioned or unpartitioned. The more common usage
is partitioned.

.. note::

   Operating system support for unpartitioned media varies. Most current
   operating systems expect partitioned media. Some restrict their
   support further and only support access unpartitioned media or to the
   first partition of partitioned media.

.. _sect_S.3:

Physical Media Interface
------------------------

The physical, electrical, signaling, and software interface shall comply
with the CF+ and CompactFlash Specification.

