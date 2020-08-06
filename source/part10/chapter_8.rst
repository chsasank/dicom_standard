.. _chapter_8:

DICOM File Service
==================

The DICOM File Service specifies an abstract view of files from the
point of view of a service user in the Data Format Layer. Constraining
access to the content of files by Application Entities through such a
DICOM File Service ensures independence of the Data Format Layer
functions from specific Media Format and Physical Media selections.

.. note::

   This DICOM File Service definition is abstract in the sense that it
   is only the specification of a boundary. Its focus is limited to the
   aspects directly related to the access to the data structures of the
   Media Format Layer (not the specifications of the data structures
   themselves). Even though the DICOM File Service may be described by
   means of a number of abstract primitives such as read, write, delete,
   etc., it is not intended to be the definition of an Application
   Programming Interface (API).

The DICOM File Service specified for Media Storage offers a basic
service, simple enough to be supported by a wide range of commonly
available Media Format (or file systems), but rich enough to provide the
key functions to effectively manage files and access their content. The
following sections specify the minimum mandatory requirements that shall
be met by any physical media and associated media format to comply with
the DICOM Media Storage model.

.. note::

   It is acceptable that a specific Media Format offers more file
   services than those specified in the DICOM File Service. Such
   services may be internal to an implementation (i.e., not visible
   through the data structures on the Storage Media). Their usage is
   beyond the scope of the DICOM Standard. However, in cases where such
   services are reflected in the file structures of the Media format
   Layer or in the Data Set encoding an Information Object, the
   extension of such services in a manner that jeopardizes
   interoperability should not be done (e.g., File IDs longer than
   specified in the DICOM File Service).

.. _sect_8.1:

File-set
--------

The DICOM File Service offers the ability to create and access one or
more files in a File-set. A File-set is a collection of files that share
a common naming space within which File IDs (see `File
IDs <#sect_8.2>`__) are unique. No semantics is attached to the order of
Files within a File-set.

.. note::

   1. The DICOM File Service does not require that Files within a
      File-set be simultaneously accessible (e.g., sequentially accessed
      media such as tapes are supported).

   2. The DICOM File Service does not explicitly include the notion of
      distributing a File-set or a File across multiple
      "volumes/physical medium". However the transparent support by the
      Media Format Layer of such a feature is not precluded.

A File ID naming space (corresponding to a File-set) shall be associated
with an appropriate feature of a Media Format defined structure. This
mapping shall be specified in for each Media Format specification (this
is integral to the specification of the relationship between any
specific Media Format services and the DICOM File Services defined in
this Part).

.. note::

   An example of such a relationship is to map the File ID naming space
   to a volume in a personal computer Media Format or a partition in a
   workstation File System on a removable medium. Another example is to
   map the File ID naming space to a directory and its tree of
   sub-directories. In this case it could offer the possibility of
   supporting multiple File-sets (one per directory) on the same
   physical medium. Each File-set would have its own DICOMDIR File. To
   ensure interoperability, shall specify these specific mapping rules
   between the directories and the File ID naming space of a File-set
   (including the rules to unambiguously locate the DICOMDIR File).

A single File with the File ID DICOMDIR shall be included in each
File-set.

Each File-set shall be uniquely identified by a File-set UID that shall
be registered according to the UID registration rules specified in .
When Files are added or removed from a File-set, the File-set UID shall
not change.

A File-set may also be identified by a File-set ID, which provides a
simple (but possibly not globally unique) human readable reference. A
File-set ID is string of zero (0) to sixteen (16) characters from the
subset of the G0 repertoire of ISO 8859 (see `Character
Set <#sect_8.5>`__). A File-set ID may be associated or mapped to an
appropriate identifier at the Media Format Layer.

.. note::

   1. Continuing with the personal computer Media Format example used
      first in the previous note, a File-set ID may be defined to be
      identical to a volume label.

   2. Non-DICOM Files (Files with a content not formatted according to
      the requirements of this Part of the DICOM Standard) may be
      present in a File-set. Such files should not contain the DICOM
      File Meta Information specified in `table_title <#table_7.1-1>`__
      and may not be referenced by the DICOM Media Storage Directory
      (see `Reserved DICOMDIR File ID <#sect_8.6>`__).

A File-set Descriptor File (a "readme" file) may also be attached to a
File-set. See for a detailed specification of the Basic Directory IOD.

.. _sect_8.2:

File IDs
--------

Files are identified by a File ID that is unique within the context of a
File-set. A File ID is an ordered sequence of File ID Components. A File
ID may contain one to eight components. Each Component is a string of
one to eight characters from a subset of the G0 repertoire of ISO 8859
(see `Character Set <#sect_8.5>`__)

Such a structure for File IDs (a sequence of components) allows the
DICOM File Service to organize file selection in a hierarchical mode. No
conventions are defined by the DICOM Standard for the use of the
structure of File IDs components and their content (except for the
reserved File ID DICOMDIR, see `Reserved DICOMDIR File
ID <#sect_8.6>`__). Furthermore, no semantics shall be conveyed by the
structure and content of such File IDs. This implies that when a File ID
is assigned to any File in a File-set, the creating DICOM Application
Entity may choose to structure the File ID as it wishes. Any other AE
reading existing files or creating new files shall not be required to
know any semantics the original creator may have associated with such a
structure.

The File ID used to access a File through the abstract DICOM File
Service is not necessarily the sole file identifier. The interchange
Media Format (file system) may allow multiple file names to address the
same physical file. Any use of alternate file names is beyond the scope
of the DICOM Standard.

.. note::

   1. A DICOM File ID is equivalent to the commonly used concept of
      "path name" concatenated with a "file name". An example of a valid
      DICOM File ID with four components shown separated by backslashes
      is:SUBDIR1\SUBDIR2\SUBDIR3\ABCDEFGH

   2. As specified in the DICOM Storage Media Model, no semantics is
      attached to File ID content and structure as it relates to the
      DICOM Information Objects stored in these files. If used, the
      hierarchical structure simply provides a means to organize the
      Files of a File-set and facilitate their selection.

   3. The DICOM File Service does not specify any "separator" between
      the Components of the File ID. This is a Value Representation
      issue that may be addressed in a specific manner by each Media
      Format Layer. In DICOM IODs, File ID Components are generally
      handled as multiple Values and separated by "backslashes". There
      is no requirement that Media Format Layers use this separator.

   4. DICOM files stored on interchange media may have an alternate file
      name or link that uses less restricted file names, such as a
      filename extension (e.g., ".dcm" in accordance with RFC3240).

.. _sect_8.3:

File Management Roles and Services
----------------------------------

When DICOM Application Entities participate in the exchange of
information by the interchange of Storage Media, they perform through
the DICOM File Service a number of Media Storage Services:

a. M-WRITE, to create new files in a File-set and assign them a File ID;

b. M-READ to read existing files based on their File ID;

c. M-DELETE to delete existing files based on their File ID;

d. M-INQUIRE FILE-SET to inquire free space available for creating new
   files within the File-set;

e. M-INQUIRE FILE to inquire date and time of file creation (or last
   update if applicable) for any file within the File-set.

A DICOM Application Entity may take one or more of the following three
roles:

a. File-set Creator (FSC). Such an Application Entity, exercises this
   role by means of M-WRITE Operations to create the DICOMDIR File (see
   `Reserved DICOMDIR File ID <#sect_8.6>`__) and zero or more DICOM
   Files;

b. File-set Reader (FSR). Such an Application Entity, exercises this
   role by means of M-READ Operations to access one or more Files in a
   File-set. A File-set Reader shall not modify any of the files of the
   File-set (including the DICOMDIR File);

c. File-set Updater (FSU). Such an Application Entity, exercises this
   role by means of M-READ, M-WRITE, and M-DELETE Operations. It reads,
   but shall not modify, the content of any of the DICOM files in a
   File-set except for the DICOMDIR File. It may create additional Files
   by means of an M-WRITE or delete existing Files in a File-set by
   means of an M-DELETE.

.. note::

   Although a File-set Updater (FSU) may include the functions
   corresponding to a File-set Creator (FSC) and a File-set Reader
   (FSR), it is not required that implementations supporting an FSU role
   also support an FSC or an FSR role.

The use of the concept of roles in DICOM Conformance Statements will
result in a more precise expression of the capabilities of
implementations supporting DICOM Media Storage. Conforming
implementations shall support one of the following choices:

a. File-set Creator,

b. File-set Reader,

c. File-set Creator and File-set Reader,

d. File-set Updater,

e. File-set Updater and File-set Creator,

f. File-set Updater and File-set Reader,

g. File-set Updater, File-set Creator and File-set Reader.

Based on the roles supported by a DICOM Application Entity, the DICOM
File Service shall support the Media Operations defined in
`table_title <#table_8.3-1>`__.

.. table:: Media Operations and Roles

   +----------+----------+----------+----------+----------+----------+
   | Media    | M-WRITE  | M-READ   | M-DELETE | M        | M        |
   | Op       |          |          |          | -INQUIRE | -INQUIRE |
   | erations |          |          |          | FILE-SET | FILE     |
   | Roles    |          |          |          |          |          |
   +==========+==========+==========+==========+==========+==========+
   | FSC      | M        | *Not     | *Not     | M        | *Not     |
   |          | andatory | r        | r        | andatory | r        |
   |          |          | equired* | equired* |          | equired* |
   +----------+----------+----------+----------+----------+----------+
   | FSR      | *Not     | M        | *Not     | *Not     | M        |
   |          | r        | andatory | r        | r        | andatory |
   |          | equired* |          | equired* | equired* |          |
   +----------+----------+----------+----------+----------+----------+
   | FSC+FSR  | M        | M        | *Not     | M        | M        |
   |          | andatory | andatory | r        | andatory | andatory |
   |          |          |          | equired* |          |          |
   +----------+----------+----------+----------+----------+----------+
   | FSU      | M        | M        | M        | M        | M        |
   |          | andatory | andatory | andatory | andatory | andatory |
   +----------+----------+----------+----------+----------+----------+
   | FSU+FSC  | M        | M        | M        | M        | M        |
   |          | andatory | andatory | andatory | andatory | andatory |
   +----------+----------+----------+----------+----------+----------+
   | FSU+FSR  | M        | M        | M        | M        | M        |
   |          | andatory | andatory | andatory | andatory | andatory |
   +----------+----------+----------+----------+----------+----------+
   | FSU      | M        | M        | M        | M        | M        |
   | +FSC+FSR | andatory | andatory | andatory | andatory | andatory |
   +----------+----------+----------+----------+----------+----------+

.. note::

   1. Media Preparation is outside the scope of this Part of the DICOM
      Standard. However it is assumed to be performed by the FS Creator.

   2. The DICOM File Service does not require that file update
      capabilities (e.g., append) be supported by every Media Format
      Definition selected. The non-support of such file update
      capabilities to the DICOMDIR File may simply result in having to
      delete and create a new file in order to keep the directory
      information consistent.

   3. If the content of a file needs to be updated or changed by an FSU,
      it is considered by this Part of the DICOM Standard as an M-DELETE
      Operation followed by an M-WRITE Operation. The FSU is responsible
      for ensuring the internal consistency of the File and its
      conformance to PS3.10 and the specific SOP Class stored, exactly
      as if the FSU was creating a new File. In particular, if an FSU
      implementation needs to update the file content but is not able to
      recognize and fully process the content of the File Preamble (see
      `DICOM File Meta Information <#sect_7.1>`__), it may consider
      setting the first four bytes of the Preamble to "DICM" followed by
      124 bytes to 00H. This would avoid introducing inconsistencies
      between the content of the File Preamble and the remainder of the
      file content. An example of this situation may occur when a TIFF
      IFD 0 Offset in the File Preamble points at a further TIFF IFD
      embedded in the DICOM Data Set, and the update operation changes
      the location of this embedded TIFF IFD.

.. _sect_8.4:

File Content Access
-------------------

The DICOM File Service offers the ability to access the content of any
File of a File-set. The File content is an ordered string of zero or
more bytes, where the first byte is at the beginning of the file and the
last byte at the end of the File.

.. note::

   This File content definition as an ordered string of bytes is related
   to the view provided at the DICOM File Service level. It may not
   correspond to the physical ordering of bytes of data on a specific
   medium.

The DICOM File Service shall manage the delimitation of the end of the
File by ensuring the user of the File Service that read access beyond
the last byte will be detected and reported to the DICOM File Service
user. This delimitation function is performed by the Media Format Layer.

The DICOM File Service shall offer the ability:

a. for an FSR or FSU to perform an M-READ to read zero or more bytes of
   the content of a File;

b. for an FSC or FSU to perform an M-WRITE to write one or more bytes
   making the content of a File.

.. note::

   The DICOM File Service does not require any specific capability for
   the selective read access or write access of the content of a file
   (e.g., seek or append). However it does not restrict specific Media
   Format definitions to support such features.

.. _sect_8.5:

Character Set
-------------

File IDs and File-set IDs shall be character strings made of characters
from a subset of the G0 repertoire of ISO 8859. The following characters
form this subset:

A, B, C, D, E, F, G, H, I, J, K, L, M, N, O, P, Q, R, S, T, U, V, W, X,
Y, Z (uppercase)

1, 2, 3, 4, 5, 6, 7, 8, 9, 0 and \_ (underscore)

.. note::

   1. This is the character set defined for Control Strings (Value
      Representation CS - see ) except that SPACE is not included.

   2. This character set is selected to limit characters in File IDs and
      File-set IDs to those that do not conflict with reserved
      characters and delimiters in the file systems defined in .
      Component delimiters or other required demarcations defined in are
      not part of File IDs or File-set IDs

.. _sect_8.6:

Reserved DICOMDIR File ID
-------------------------

A single File with a File ID, DICOMDIR, shall exist as a member of every
File-set. This File ID is made of a single Component (see `File
IDs <#sect_8.2>`__ for the File ID structure). It contains the DICOM
Media Storage Directory (see for detailed specification of the Basic
Directory IOD), which includes general information about the whole
File-set. This general information is always present, but optionally the
directory content may be left empty in environments where it would not
be needed. If the DICOMDIR File does not exist in a File-set, the
File-set does not conform to PS3.10. The DICOMDIR shall not reference
Files outside of the File-set to which it belongs.

.. note::

   1. An example of the content of the DICOMDIR File may be found in
      `Example of DICOMDIR File Content (Informative) <#chapter_A>`__.

   2. If one chooses to map the origin of a File-set to a specific
      directory node in a specific Media Format, the File IDs, including
      the DICOMDIR File IDs, would be relative to this directory node
      path name.

The DICOMDIR File shall use the Explicit VR Little Endian Transfer
Syntax (UID=1.2.840.10008.1.2.1) to encode the Media Storage Directory
SOP Class. The DICOMDIR File shall comply with the DICOM File Format
specified in Section 7 of this Standard. In particular the:

a. SOP Class UID in the File Meta Information (header of the DICOMDIR
   File) shall have the Value specified in of this Standard for the
   Media Storage Directory SOP Class;

b. SOP Instance UID in the File Meta Information (header of the DICOMDIR
   File) shall contain the File-set UID Value. The File-set UID is
   assigned by the Application Entity that created the File-set (FSC
   role, see `File Management Roles and Services <#sect_8.3>`__) with
   zero or more DICOM Files. This File-set UID Value shall not be
   changed by any other Application Entities reading or updating the
   content of the File-set.

.. note::

   1. This policy reflects that a File-set is an abstraction of a
      "container" within which Files may be created or read. The
      File-set UID is related to the "container" not its content. A
      File-set in the DICOM File Service is intended to be mapped to a
      supporting feature of a selected Media Format (e.g., volume or
      partition).

   2. The Standard does not prevent the making of duplicate copies of a
      File-set (i.e., a File-set with the same File-set UID). However,
      within a managed domain of File-sets, a domain specific policy may
      be used to prevent the creation of such duplicate File-sets.

