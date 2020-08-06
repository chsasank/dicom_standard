.. _chapter_Q:

90 mm 2.3 GB Magneto-Optical Disk (Normative)
=============================================

.. _sect_Q.1:

DICOM Mapping to Media Formats
------------------------------

Only one DICOM File-set shall be stored onto a single 90mm disk.

.. _sect_Q.2:

Media Formats
-------------

The media format comprises two distinct components:

a. The Recording format, which addresses magnetic recording, track
   definition, sector headers, etc.

b. The Logical format, which addresses the organization of the data
   portion of sectors to support semantics of the file system.

.. _sect_Q.2.1:

Recording Format
~~~~~~~~~~~~~~~~

The low level formatting shall be done using the GIGAMO standard. GIGAMO
is published as a Sony-Fujitsu document and is currently not an ISO/IEC
standard. The document specifying this formatting is the "GIGAMO 2.3GB
90mm Magneto-Optical Disk System in Cherry Book2 version 1.0". The
Secondary Defect List shall be used.

.. _sect_Q.2.2:

Logical Format
~~~~~~~~~~~~~~

The Logical Format for the 90mm 2.3GB disk shall be the PC File System
(`PC File System (Normative) <#chapter_A>`__).

The boot sector defined in `PC File System (Normative) <#chapter_A>`__
shall have the following values.

.. table:: Boot Parameter Values for 90mm 2.3 GB Magneto-Optical Disk

   +---------+-----------------------+----------------------------+
   | Byte(s) | Value                 | Description                |
   +=========+=======================+============================+
   | 11 - 12 | 0800H                 | 2048 Bytes/Sector          |
   +---------+-----------------------+----------------------------+
   | 13      | 08H, 10H, 20H, or 40H | Sectors / cluster, either  |
   |         |                       | 8, 16, 32, or 64           |
   +---------+-----------------------+----------------------------+
   | 21      | F8H                   | Flag for disk type F8H =   |
   |         |                       | Hard Disk                  |
   +---------+-----------------------+----------------------------+
   | 24-25   | 0019H (Nominal)       | Nominally 25               |
   |         |                       | sectors/track, but may     |
   |         |                       | vary, and any value should |
   |         |                       | not affect                 |
   |         |                       | interoperability           |
   +---------+-----------------------+----------------------------+
   | 26-27   | 0001 (Nominal)        | Nominally 1 head, but may  |
   |         |                       | vary, and any value should |
   |         |                       | not affect                 |
   |         |                       | interoperability.          |
   +---------+-----------------------+----------------------------+

.. note::

   When formatted the total formatted capacity of the disk is
   approximately 2.02GB.

.. _sect_Q.3:

Physical Media
--------------

The physical media shall be the 90mm Magneto-Optical Rewritable disk
with 2048 bytes per sector. It shall be compatible with the R/W Type
cartridge defined in the "GIGAMO 2.3GB 90mm Magneto-Optical Disk System
in Cherry Book2 version 1.0".

