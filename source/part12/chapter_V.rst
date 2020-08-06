.. _chapter_V:

ZIP File Media (Normative)
==========================

.. _sect_V.1:

DICOM Mapping to ZIP File
-------------------------

.. _sect_V.1.1:

DICOM File-set
~~~~~~~~~~~~~~

One and only one DICOM File-set shall be contained in a ZIP File
archive.

Each DICOM SOP Instance shall be encoded in accordance with the rules in
.

.. note::

   A ZIP File may contain files that are not referenced by the DICOMDIR,
   which may be ignored by the DICOM application.

.. _sect_V.1.2:

DICOM File ID Mapping
~~~~~~~~~~~~~~~~~~~~~

The ZIP encoding preserves the hierarchical structure for directories
and files within directories. Each volume has a root directory that may
contain references to both files and sub-directories. Sub-directories
may contain reference to both files and other sub-directories.

.. _sect_V.1.2.1:

File ID
^^^^^^^

defines a DICOM File ID Component as a string of 8 characters from a
subset of the G0 repertoire of ISO 8859.

.. note::

   The use of long file names is prohibited.

Filename extensions are not used in DICOM File ID Components, hence a
File Identifier shall not contain a File Extension or the '.' that would
precede such a File Extension.

The maximum number of levels of a path name in a ZIP file-set shall be
at most 8 levels, to comply with the definition of a DICOM File-set in .

.. _sect_V.1.2.2:

DICOMDIR
^^^^^^^^

One and only one DICOMDIR File shall be present. The DICOMDIR shall be
at the root directory of the File-set.

.. note::

   The reason for the DICOMDIR is to serve as a manifest so that the
   recipient knows the full list of instances intended to be sent.

.. _sect_V.2:

Logical Format
--------------

The Zip file format shall be as described in the ZIP File Format
Specification available from PKWARE. The following capabilities shall be
used:

-  The ZIP encoding shall preserve the directory structure.

.. note::

   This specification may be found at
   http://support.pkware.com/display/PKZIP/APPNOTE.

