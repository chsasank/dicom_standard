.. _chapter_R:

USB Connected Removable Devices
===============================

.. _sect_R.1:

DICOM Mapping to Media Formats
------------------------------

Only one DICOM file set shall be stored in the first partition of a
partitioned device. If the device is not partitioned, only one DICOM
file set shall be stored on the device.

.. _sect_R.1.1:

File System
~~~~~~~~~~~

The file system employed on these media shall be either the FAT16 file
system or the FAT32 file system. The information in the boot sector of
this partition shall be utilized by the file system to determine proper
access to this media (see Microsoft Extensible Firmware Initiative FAT32
File System Specification).

File names used for DICOM files shall be further restricted to be in
compliance with the File ID rules specified in . The File ID shall be
the same as the filename.

.. note::

   These rules limit the character set to being a subset of the DICOM
   default G0 character set, limit the file names to be no more than 8
   characters, and limit the directory tree to be no more than 8 levels
   deep. All of these restrictions are needed to comply with the most
   limited of the removable media.

.. _sect_R.2:

Media Formats
-------------

.. _sect_R.2.1:

Partitioning
~~~~~~~~~~~~

These media may be partitioned or unpartitioned. The more common usage
is partitioned.

.. note::

   Operating system support for unpartitioned media varies. Most current
   operating systems expect partitioned media. Some restrict their
   support further and only support access to the first partition of
   this media. These support decisions are being driven by the high
   volume consumer items that utilize these mechanisms, such as digital
   cameras.

.. _sect_R.3:

Physical Media Interface
------------------------

These devices may have a wide variety of overall physical
characteristics. They shall provide a connector that complies with the
USB 1.1 or 2.0 specifications for physical, electrical, signaling, and
communications protocol. The electrical signaling and lower level USB
protocol support shall comply with the USB 1.1 or 2.0 specifications.
The device shall act as a Mass Storage Device, in accordance with the
USB Mass Storage Class, as described in the Universal Serial Bus Mass
Storage Class, Specification Overview and its subordinate and referenced
documents.

.. note::

   1. The USB base standard and the USB mass storage device standard
      includes specification for management of device addition and
      removal, and for negotiation of device command protocol
      capabilities. Support for these is normally part of the functions
      provided by the USB Mass Storage driver in an operating system.

   2. The USB 2.0 specification specifies 3 speeds of operation,
      "low-speed", "full-speed" and "high-speed", which are fully
      interoperable, and this profile does not distinguish between the
      speeds.

   3. The intent is to allow removable 1.1 and 2.0 USB media to
      interoperate with 1.1 and 2.0 USB devices.

