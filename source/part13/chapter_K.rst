.. _chapter_K:

DICOM MIME Media (Normative)
============================

.. _sect_K.1:

DICOM Mapping to MIME Formats
-----------------------------

.. _sect_K.1.1:

DICOM File Set
~~~~~~~~~~~~~~

One DICOM File set shall be contained in a MIME Multipart/mixed or
Multipart/related Media Type, called "DICOM File set" MIME Entity.

.. note::

   1. It may be necessary to fragment a message by using the
      Message/partial Media Type format.

   2. A "DICOM File set" MIME Entity may contain MIME Parts other than
      Application/dicom, which may be ignored by the DICOM application.

.. _sect_K.1.2:

DICOM File
~~~~~~~~~~

Each generic DICOM file shall be encoded as a MIME Application/dicom
Media Type, called "DICOM File" MIME Part, with the following
parameters:

-  "id" is constructed from the DICOM File ID. The total length is
   limited to 71 characters (to avoid that the e-mail application splits
   the id string). Each component is limited to 8 characters. The
   delimiter is a forward slash "/". There is never a leading delimiter
   (i.e., this is not a traditional path from a root directory).

For example:
"ROOTDIR/SUBDIR1/MRSCAN/A789FD07/19991024/ST00234/S00003/I00023"

-  "name" is constructed from the last DICOM File ID component (that
   means the "file name" without "path" information) and the extension
   ".dcm" (except for the DICOMDIR).

For example: "I00023.dcm"

.. note::

   1. Email clients typically use this parameter as the default name
      with which to save the file. If used for only one "DICOM File"
      Part (versus one DICOM File set), the length of this parameter is
      not restricted (unlike the "id" parameter).

   2. This name can not be the same as the name inside the DICOMDIR
      where the file extension is forbidden.

The other fields of the header of this "DICOM File" MIME Part are
respecting the general rules of MIME.

.. note::

   1. RFC3240 describes under the heading of additional information that
      a Macintosh File Type Code of "DICM" be used for DICOM files.

   2. Where Universal Type Identifiers (UTIs) are in use, it is
      recommended that a UTI of org.nema.dicom be used for DICOM files,
      which is defined here as conforming to public.data (not
      public.image, since not all DICOM files are images), and is
      defined to correspond to the tags 'DICM', .dcm and
      Application/dicom. The UTI property UTTypeIdentifier is "DICOM"
      and the UTI property UTTypeReferenceURL is http://dicom.nema.org/.

      See also
      "http://developer.apple.com/documentation/Carbon/Conceptual/understanding_utis/index.html".

.. _sect_K.1.2.1:

DICOMDIR
^^^^^^^^

One and only one DICOMDIR File may be present in any "DICOM File set"
MIME Entity. It is encoded as the generic "DICOM File" MIME Part, with a
DICOM File ID set to "DICOMDIR" and the "id" parameter set to
"DICOMDIR".

.. _sect_K.3:

Logical Format
--------------

The MIME logical format is used. The Content-Transfer-Encoding shall
allow the transfer of binary information (e.g., typically base64 if the
higher level does not allow transfer of binary information).

