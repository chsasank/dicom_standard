.. _chapter_F:

Basic Directory Information Object Definition (Normative)
=========================================================

.. _sect_F.1:

Scope of the Basic Directory Information IOD
--------------------------------------------

The Basic Directory Information Object Definition may be used for DICOM
Media Storage (see ) and the Media Storage Service Class (see ). It is
an abstraction of the information to:

a. Identify a File-set

b. Provide a directory that facilitates access to the information stored
   in the files of a File-set based on key medical information. Such a
   directory facility relies on a hierarchical information model of
   medical summary information referencing the content of the Files
   stored in a File-set on a storage medium. Standardizing such a
   directory function is a key element to facilitate the interchange of
   medical imaging data and is intended to support the complete range of
   modality imaging information.

.. note::

   The directory information has been defined so that a future version
   may be extended to support the distribution of the directory
   information among a logical tree of several files (with the DICOMDIR
   file at its root). However in this version, the entire directory
   information is specified to be stored in a single File with a
   DICOMDIR File ID.

.. note::

   1. Whether a single File-set or multiple File-sets are allowed on a
      formatted Physical Media is defined by the Media Format
      specification (used for each specific Physical Media) in .

   2. The DICOMDIR File is identified by a single component File ID,
      DICOMDIR. Other files in the File-set may have File IDs made of a
      single component (e.g., "ABGT" in
      `figure_title <#figure_F.1-1>`__) or multiple components (e.g.,
      AB\12 or AB\CDE\FI) not to exceed 8 components (see ).

This Basic Directory Information Object:

a. is based on a structure of basic medical information. It is not a
   file system directory such as the one that may be used by the Media
   Format Layer;

b. is simple enough to meet the requirements of elementary Media
   Interchange applications;

c. is efficient in supporting update to the directory on rewritable
   media without a complete rewrite of the entire DICOMDIR File;

d. is extendible for specific applications with specialized selection
   keys in addition to the standard keys;

e. does not mandate any relationship between the hierarchy of the
   medical information in the DICOM Directory and the hierarchy of the
   File ID Components;

.. note::

   Such an independence between the structure of the file identifiers,
   from which no semantic information shall be inferred, and the DICOM
   Directory that conveys medical imaging information, ensures that the
   broadest interoperability is possible between conforming DICOM media
   storage implementations.

.. _sect_F.2:

Basic Directory IOD Overview
----------------------------

The general organization of the Basic Directory IOD is introduced in
this Section. A simple example is also provided to illustrate the
application of this organization.

.. _sect_F.2.1:

Basic Directory IOD Organization
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Basic Directory IOD organization is based on a hierarchy of
Directory Entities. At the origin of this inverted tree is a root
Directory Entity. Each Directory Entity includes one or more Directory
Records, which in turn may each reference a lower level Directory
Entity.

Directory Records serve to reference objects stored in the Files of the
File-set. The organization of the Directory is depicted by the Basic
Directory IOD entity/relationship model presented in
`figure_title <#figure_F.2-1>`__.

Each Directory Record, irrespective of the Directory Entity it is
included in, contains four types of information:

a. A reference to a lower level Directory Entity or Referenced Directory
   Entity. This reference may be absent if such a lower level Directory
   Entity does not exist for an instance of a directory record;

b. A reference to a File of the File-set in which is stored a
   "Referenced Object" (formally called in DICOM a Referenced SOP
   Instance). This reference may be absent if no File is referenced.
   Files may be referenced directly by their File ID;

c. A set of "selection keys", specific to a Referenced Object, which
   will allow its selection among all the records included in a given
   Directory Entity;

d. A mechanism to chain the various Directory Records that belong to the
   same Directory Entity.

This generic content of a Directory Record is further specialized based
on its specific type in the context the Basic Directory IOD Information
Model specified in `Basic Directory IOD Information Model <#sect_F.4>`__
(e.g., a Study Record, a Series Record, etc.). A Directory Entity may
include Directory Records of different Types. By standardizing a number
of specific Directory Records (see `Definition of Specific Directory
Records <#sect_F.5>`__) in the context of the Basic Directory IOD
Information Model, one allows the definition of a variety of directory
contents while maintaining a framework for interoperability.

To facilitate the management and update of the Directory Information a
number of rules are defined:

a. Any Lower-Level Directory Entity shall be referenced by at most one
   higher-level Directory Record. Not allowing multiple higher-level
   Directory Records to reference the same Lower-Level Directory Entity
   simplifies the management of the deletion (or inactivation) of
   Directory Records and Lower-Level Directory Entities and associated
   Directory Records

b. Any Directory Record shall belong to a single Directory Entity. This
   rule and the above rule, makes the Basic Directory IOD itself
   strictly hierarchical

c. All files referenced by a Directory shall be present in the same
   File-Set to which the directory belongs

d. Non-DICOM files that are not referenced by the Directory may be
   included in the File-set space. The means of access to such Files and
   the semantics associated with their absence from the Directory is
   beyond the scope of the DICOM Standard

e. If a DICOMDIR contains a `Directory Information
   Module <#sect_F.3.2.2>`__, all DICOM Files of the File-set shall be
   referenced by a Directory Record

f. Any File of the File-set shall be directly referenced by at most one
   Directory Record of the Directory.

.. note::

   Referenced Files may contain SOP Instances of SOP Classes that
   provide the means to reference by UIDs other SOP Instances that may
   not be stored in files of the same File-set.

.. _sect_F.2.2:

Example of A Directory
~~~~~~~~~~~~~~~~~~~~~~

The example provided in this Section is only one simple example of a
possible directory content and organization. This Section is not
normative in nature. Therefore, this example is not meant to specify a
conformant directory nor to restrict the range of possible directory
organizations supported by this Part of the DICOM Standard.

The overall organization is illustrated at a logical level in
`Illustration of the Overall Directory Organization <#sect_F.2.2.1>`__.
The actual structure of the content is discussed in `Example of a
DICOMDIR File Structure <#sect_F.2.2.2>`__. depicts further details of
the encoding of the file content.

.. _sect_F.2.2.1:

Illustration of the Overall Directory Organization
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

A simple directory content is used as an example of Directory
organization. It is depicted by `figure_title <#figure_F.2-2>`__. The
left hand side part of `figure_title <#figure_F.2-2>`__ depicts the
various Objects stored in Files of the File-set. The right hand side
presents an example of organization of the directory that facilitates
access to the Files of the File-set.

This example shows how stored Files are referenced by Directory Records
that are grouped into Directory Entities. The two Study Directory
Records (Study 1 and Study 2) are part of the Directory Entity relative
to the Patient A.

Thin curved lines depict the referencing mechanism based on File IDs
that allow reference to Files containing stored objects. Thick curved
lines depict the internal referencing mechanisms that support the
reference to a lower-level Directory Entity by a Directory Record.

Keys that are used to select a specific Directory Record from among the
Directory Records of a Directory Entity are not shown on
`figure_title <#figure_F.2-2>`__.

One may note in this example that certain Directory Records such as the
Series Directory Records do not reference Files containing stored
objects. Other Directory Records such as the Image Directory Records do
not reference lower level Directory Entities. However, a number of
Directory Records reference both one lower level Directory Entity and
one File containing a stored object. This flexibility allows the
definition of a variety of directories.

.. _sect_F.2.2.2:

Example of a DICOMDIR File Structure
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Based on the example discussed in `Illustration of the Overall Directory
Organization <#sect_F.2.2.1>`__, the internal data structure used by the
Basic Directory IOD is depicted in `figure_title <#figure_F.2-3>`__. It
shows a set of Directory Records where each Directory Record is linked
by three different types of "referencing" mechanisms:

a. The chaining of Directory Records to form a Directory Entity. In
   particular, this facilitates the addition of new Directory Records at
   the level of any Directory Entity by placing them at the end of the
   DICOMDIR File. On `figure_title <#figure_F.2-3>`__, this chaining is
   shown by yellow lines:

   1. #1 shows the chaining of the Directory Records forming the root
      Directory Entity

   2. #2 shows the chaining of the Directory Records for the Directory
      Entity related to Patient A

   3. #3 shows the chaining of the Directory Records for the Directory
      Entity related to Study 1

   4. #4 shows the chaining of the Directory Records for the Directory
      Entity related to Series 1

b. Green lines depict the reference by a Directory Record to a lower
   level Directory Entity

c. Blue lines depict the reference by a Directory Record to a stored
   file containing a SOP Class

This example of a DICOMDIR File structure shows one example of a
specific order of the Directory Records. Other orderings of Directory
Records could result in a functionally equivalent directory.

.. _sect_F.3:

Basic Directory IOD
-------------------

This IOD is based on the Directory Information organization introduced
in `Basic Directory IOD Overview <#sect_F.2>`__. The model for this
Basic Directory IOD is described `Basic Directory IOD
Organization <#sect_F.2.1>`__ by the Entity/Relationship model in
`figure_title <#figure_F.2-1>`__. The rules specified in `Basic
Directory IOD Organization <#sect_F.2.1>`__ apply to this Information
Object Definition.

.. _sect_F.3.1:

Module Table
~~~~~~~~~~~~

The Basic Directory IOD includes the Modules specified by
`table_title <#table_F.3-1>`__.

.. table:: Basic Directory IOD Modules

   +-------------------+-------------------+-------+-------------------+
   | Module            | Reference         | Usage | Module            |
   |                   |                   |       | Description       |
   +===================+===================+=======+===================+
   | File-set          | `File-set         | M     | File-set          |
   | Identification    | Identification    |       | identification    |
   |                   | Module <          |       | information       |
   |                   | #sect_F.3.2.1>`__ |       |                   |
   +-------------------+-------------------+-------+-------------------+
   | Directory         | `Directory        | U     | Directory         |
   | Information       | Information       |       | Information       |
   |                   | Module <          |       | followed by a     |
   |                   | #sect_F.3.2.2>`__ |       | Sequence of       |
   |                   |                   |       | Directory         |
   |                   |                   |       | Records.          |
   |                   |                   |       |                   |
   |                   |                   |       | .. note::         |
   |                   |                   |       |                   |
   |                   |                   |       |    The `Directory |
   |                   |                   |       |    Information    |
   |                   |                   |       |    Module <       |
   |                   |                   |       | #sect_F.3.2.2>`__ |
   |                   |                   |       |    is optional.   |
   |                   |                   |       |    This           |
   |                   |                   |       |    `Directory     |
   |                   |                   |       |    Information    |
   |                   |                   |       |    Module <       |
   |                   |                   |       | #sect_F.3.2.2>`__ |
   |                   |                   |       |    should be      |
   |                   |                   |       |    present in all |
   |                   |                   |       |    but primitive  |
   |                   |                   |       |    environments   |
   |                   |                   |       |    where a        |
   |                   |                   |       |    directory is   |
   |                   |                   |       |    not needed. In |
   |                   |                   |       |    this case,     |
   |                   |                   |       |    only the       |
   |                   |                   |       |    File-set       |
   |                   |                   |       |    Identification |
   |                   |                   |       |    Information is |
   |                   |                   |       |    present.       |
   +-------------------+-------------------+-------+-------------------+

.. _sect_F.3.2:

Modules of the Basic Directory Information Object
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Attributes of the Basic Directory IOD are defined with a Type
designation that indicates if a specific Attribute is required for all
Media Storage Operations (see `Conventions <#chapter_5>`__).

.. _sect_F.3.2.1:

File-set Identification Module
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. table:: File-Set Identification Module Attributes

   +----------------------+-------------+------+----------------------+
   | Attribute Name       | Tag         | Type | Attribute            |
   |                      |             |      | Description          |
   +======================+=============+======+======================+
   | File-set ID          | (0004,1130) | 2    | User or              |
   |                      |             |      | implementation       |
   |                      |             |      | specific Identifier  |
   |                      |             |      | (up to 16            |
   |                      |             |      | characters). For     |
   |                      |             |      | definition, see .    |
   |                      |             |      | The File-set ID is   |
   |                      |             |      | intended to be a     |
   |                      |             |      | short human readable |
   |                      |             |      | label to easily (but |
   |                      |             |      | not necessarily      |
   |                      |             |      | uniquely) identify a |
   |                      |             |      | specific File-set to |
   |                      |             |      | facilitate operator  |
   |                      |             |      | manipulation of the  |
   |                      |             |      | physical media on    |
   |                      |             |      | which the File-set   |
   |                      |             |      | is stored.           |
   |                      |             |      | Assignment of Value  |
   |                      |             |      | and semantics are    |
   |                      |             |      | environment          |
   |                      |             |      | specific.            |
   +----------------------+-------------+------+----------------------+
   | File-set Descriptor  | (0004,1141) | 3    | ID of a File (in the |
   | File ID              |             |      | same File-set) used  |
   |                      |             |      | for user comments    |
   |                      |             |      | related to the       |
   |                      |             |      | File-set (e.g., a    |
   |                      |             |      | README file). The    |
   |                      |             |      | Specific Character   |
   |                      |             |      | set used may be      |
   |                      |             |      | specified in the     |
   |                      |             |      | Specific Character   |
   |                      |             |      | Set of the File-set  |
   |                      |             |      | Descriptor File      |
   |                      |             |      | (0004,1142).         |
   |                      |             |      |                      |
   |                      |             |      | .. note::            |
   |                      |             |      |                      |
   |                      |             |      |    This File is not  |
   |                      |             |      |    DICOM formatted   |
   |                      |             |      |    (no Preamble, nor |
   |                      |             |      |    DICM Prefix and   |
   |                      |             |      |    Meta              |
   |                      |             |      |    Information).     |
   +----------------------+-------------+------+----------------------+
   | Specific Character   | (0004,1142) | 1C   | Character set used   |
   | Set of File-set      |             |      | in the File-set      |
   | Descriptor File      |             |      | Descriptor File with |
   |                      |             |      | a File ID as         |
   |                      |             |      | specified in         |
   |                      |             |      | File-set Descriptor  |
   |                      |             |      | File ID (0004,1141). |
   |                      |             |      | Required to specify  |
   |                      |             |      | the expanded or      |
   |                      |             |      | replacement          |
   |                      |             |      | character set. If    |
   |                      |             |      | absent, only the     |
   |                      |             |      | Basic Graphic set is |
   |                      |             |      | used. See `Specific  |
   |                      |             |      | Character            |
   |                      |             |      | Set <                |
   |                      |             |      | #sect_C.12.1.1.2>`__ |
   |                      |             |      | for Defined Terms.   |
   +----------------------+-------------+------+----------------------+

.. note::

   Every File-set is assigned a File-set UID when created. The File-set
   UID need not be duplicated as a Type 1 Attribute of the `File-set
   Identification Module <#sect_F.3.2.1>`__. It is conveyed as the SOP
   Instance UID of the Basic Directory IOD. It is included in the
   DICOMDIR File Meta Information (see )

.. _sect_F.3.2.2:

Directory Information Module
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This Module contains a Sequence of Directory Records forming one or more
Directory Entities. This Module defines at least one Directory Entity,
the Root Directory Entity (which may be empty). Each Directory Record is
composed of Directory Elements (marked by a ">"). They include:

a. an offset pointer to another Directory Record of the Same Directory
   Entity

b. an offset pointer to a lower level Directory Entity

c. a Referenced File pointed to by the Directory Record

d. a set of keys representative of the information contained in the
   Referenced File

.. table:: Directory Information Module Attributes

   +----------------+----------------+----------------+----------------+
   | Attribute Name | Tag            | Type           | Attribute      |
   |                |                |                | Description    |
   +================+================+================+================+
   | Offset of the  | (0004,1200)    | 1              | Offset of the  |
   | First          |                |                | first byte (of |
   | Directory      |                |                | the Item Data  |
   | Record of the  |                |                | Element) of    |
   | Root Directory |                |                | the first      |
   | Entity         |                |                | Directory      |
   |                |                |                | Record of the  |
   |                |                |                | Root Directory |
   |                |                |                | Entity. This   |
   |                |                |                | Offset is a    |
   |                |                |                | number of      |
   |                |                |                | bytes starting |
   |                |                |                | with the first |
   |                |                |                | byte of the    |
   |                |                |                | File Meta      |
   |                |                |                | Information.   |
   |                |                |                | When the Root  |
   |                |                |                | Directory      |
   |                |                |                | Entity         |
   |                |                |                | contains no    |
   |                |                |                | Directory      |
   |                |                |                | Record, this   |
   |                |                |                | offset shall   |
   |                |                |                | be set to      |
   |                |                |                | 00000000H.     |
   |                |                |                |                |
   |                |                |                | .. note::      |
   |                |                |                |                |
   |                |                |                |    This offset |
   |                |                |                |    includes    |
   |                |                |                |    the File    |
   |                |                |                |    Preamble    |
   |                |                |                |    and the     |
   |                |                |                |    DICM        |
   |                |                |                |    Prefix.     |
   +----------------+----------------+----------------+----------------+
   | Offset of the  | (0004,1202)    | 1              | Offset of the  |
   | Last Directory |                |                | first byte (of |
   | Record of the  |                |                | the Item Data  |
   | Root Directory |                |                | Element) of    |
   | Entity         |                |                | the last       |
   |                |                |                | Directory      |
   |                |                |                | Record of the  |
   |                |                |                | Root Directory |
   |                |                |                | Entity. This   |
   |                |                |                | Offset is a    |
   |                |                |                | number of      |
   |                |                |                | bytes starting |
   |                |                |                | with the first |
   |                |                |                | byte of the    |
   |                |                |                | File Meta      |
   |                |                |                | Information.   |
   |                |                |                | When the Root  |
   |                |                |                | Directory      |
   |                |                |                | Entity         |
   |                |                |                | contains no    |
   |                |                |                | Directory      |
   |                |                |                | Record, this   |
   |                |                |                | offset shall   |
   |                |                |                | be set to      |
   |                |                |                | 00000000H.     |
   |                |                |                |                |
   |                |                |                | .. note::      |
   |                |                |                |                |
   |                |                |                |    This offset |
   |                |                |                |    includes    |
   |                |                |                |    the File    |
   |                |                |                |    Preamble    |
   |                |                |                |    and the     |
   |                |                |                |    DICM        |
   |                |                |                |    Prefix.     |
   +----------------+----------------+----------------+----------------+
   | File-set       | (0004,1212)    | 1              | 0000H          |
   | Consistency    |                |                |    no known    |
   | Flag           |                |                |    i           |
   |                |                |                | nconsistencies |
   |                |                |                |                |
   |                |                |                | The value      |
   |                |                |                | FFFFH shall    |
   |                |                |                | never be       |
   |                |                |                | present.       |
   |                |                |                |                |
   |                |                |                | .. note::      |
   |                |                |                |                |
   |                |                |                |    Formerly,   |
   |                |                |                |    this        |
   |                |                |                |    Attribute   |
   |                |                |                |    was         |
   |                |                |                |    intended to |
   |                |                |                |    signal that |
   |                |                |                |    the         |
   |                |                |                |    directory   |
   |                |                |                |    was in an   |
   |                |                |                |                |
   |                |                |                |   inconsistent |
   |                |                |                |    state with  |
   |                |                |                |    a value of  |
   |                |                |                |    FFFFH. This |
   |                |                |                |    usage has   |
   |                |                |                |    been        |
   |                |                |                |    retired.    |
   |                |                |                |    See         |
   |                |                |                |    `           |
   |                |                |                | PS3.3-2008 <ft |
   |                |                |                | p://medical.ne |
   |                |                |                | ma.org/MEDICAL |
   |                |                |                | /Dicom/2008/08 |
   |                |                |                | _03pu.pdf>`__. |
   +----------------+----------------+----------------+----------------+
   | Directory      | (0004,1220)    | 2              | Sequence of    |
   | Record         |                |                | zero or more   |
   | Sequence       |                |                | Items where    |
   |                |                |                | each Item      |
   |                |                |                | contains a     |
   |                |                |                | Directory      |
   |                |                |                | Record by      |
   |                |                |                | including the  |
   |                |                |                | Directory      |
   |                |                |                | Elements from  |
   |                |                |                | (0004,1400) to |
   |                |                |                | (0004,1511)    |
   |                |                |                | and Record     |
   |                |                |                | selection Keys |
   |                |                |                | as defined     |
   |                |                |                | below (marked  |
   |                |                |                | with a >).     |
   |                |                |                |                |
   |                |                |                | A zero length  |
   |                |                |                | Value          |
   |                |                |                | indicates that |
   |                |                |                | no Directory   |
   |                |                |                | Records are    |
   |                |                |                | contained in   |
   |                |                |                | the Root       |
   |                |                |                | Directory      |
   |                |                |                | Entity.        |
   +----------------+----------------+----------------+----------------+
   | >Offset of the | (0004,1400)    | 1              | Offset of the  |
   | Next Directory |                |                | first byte (of |
   | Record         |                |                | the Item Data  |
   |                |                |                | Element) of    |
   |                |                |                | the next       |
   |                |                |                | Directory      |
   |                |                |                | Record of the  |
   |                |                |                | same Directory |
   |                |                |                | Entity. This   |
   |                |                |                | Offset is an   |
   |                |                |                | unsigned       |
   |                |                |                | integer        |
   |                |                |                | representing a |
   |                |                |                | number of      |
   |                |                |                | bytes starting |
   |                |                |                | with the first |
   |                |                |                | byte of the    |
   |                |                |                | File           |
   |                |                |                | Met            |
   |                |                |                | a-information. |
   |                |                |                | A zero offset  |
   |                |                |                | shall be used  |
   |                |                |                | to mean that   |
   |                |                |                | there is no    |
   |                |                |                | other          |
   |                |                |                | Directory      |
   |                |                |                | Record in this |
   |                |                |                | Directory      |
   |                |                |                | Entity.        |
   |                |                |                |                |
   |                |                |                | This Offset    |
   |                |                |                | may be used to |
   |                |                |                | keep an        |
   |                |                |                | inactive       |
   |                |                |                | Record         |
   |                |                |                | (0004,1410)    |
   |                |                |                | chained with   |
   |                |                |                | the next       |
   |                |                |                | Directory      |
   |                |                |                | Record of the  |
   |                |                |                | same Directory |
   |                |                |                | Entity.        |
   |                |                |                |                |
   |                |                |                | .. note::      |
   |                |                |                |                |
   |                |                |                |    This offset |
   |                |                |                |    includes    |
   |                |                |                |    the File    |
   |                |                |                |    Preamble    |
   |                |                |                |    and the     |
   |                |                |                |    DICM        |
   |                |                |                |    Prefix.     |
   +----------------+----------------+----------------+----------------+
   | >Record In-use | (0004,1410)    | 1              | FFFFH          |
   | Flag           |                |                |    record is   |
   |                |                |                |    in use.     |
   |                |                |                |                |
   |                |                |                | The value      |
   |                |                |                | 0000H shall    |
   |                |                |                | never be       |
   |                |                |                | present.       |
   |                |                |                |                |
   |                |                |                | .. note::      |
   |                |                |                |                |
   |                |                |                |    Formerly,   |
   |                |                |                |    this        |
   |                |                |                |    Attribute   |
   |                |                |                |    was         |
   |                |                |                |    intended to |
   |                |                |                |    facilitate  |
   |                |                |                |    the         |
   |                |                |                |    deletion of |
   |                |                |                |    files, with |
   |                |                |                |    a value     |
   |                |                |                |    0000H       |
   |                |                |                |    signally an |
   |                |                |                |    inactive    |
   |                |                |                |    record.     |
   |                |                |                |    This usage  |
   |                |                |                |    has been    |
   |                |                |                |    retired.    |
   |                |                |                |    See         |
   |                |                |                |    `           |
   |                |                |                | PS3.3-2008 <ft |
   |                |                |                | p://medical.ne |
   |                |                |                | ma.org/MEDICAL |
   |                |                |                | /Dicom/2008/08 |
   |                |                |                | _03pu.pdf>`__. |
   |                |                |                |                |
   |                |                |                | Other Values   |
   |                |                |                | are reserved   |
   |                |                |                | and shall not  |
   |                |                |                | be set by      |
   |                |                |                | File-set       |
   |                |                |                | Creators, but  |
   |                |                |                | if present     |
   |                |                |                | shall be       |
   |                |                |                | interpreted as |
   |                |                |                | FFFFH by       |
   |                |                |                | File-set       |
   |                |                |                | Readers or     |
   |                |                |                | Updaters.      |
   +----------------+----------------+----------------+----------------+
   | >Offset of     | (0004,1420)    | 1              | Offset of the  |
   | Referenced     |                |                | first byte (of |
   | Lower-Level    |                |                | the Item Data  |
   | Directory      |                |                | Element) of    |
   | Entity         |                |                | the first      |
   |                |                |                | Directory      |
   |                |                |                | Record of the  |
   |                |                |                | Referenced     |
   |                |                |                | Lower Level    |
   |                |                |                | Directory      |
   |                |                |                | Entity. This   |
   |                |                |                | Offset is a    |
   |                |                |                | number of      |
   |                |                |                | bytes starting |
   |                |                |                | with the first |
   |                |                |                | byte of the    |
   |                |                |                | File Meta      |
   |                |                |                | Information.   |
   |                |                |                |                |
   |                |                |                | When no        |
   |                |                |                | lower-level    |
   |                |                |                | Directory      |
   |                |                |                | Entity         |
   |                |                |                | (containing at |
   |                |                |                | least one      |
   |                |                |                | Directory      |
   |                |                |                | Record) is     |
   |                |                |                | referenced,    |
   |                |                |                | this Attribute |
   |                |                |                | shall have a   |
   |                |                |                | Value of       |
   |                |                |                | 00000000H.     |
   |                |                |                |                |
   |                |                |                | .. note::      |
   |                |                |                |                |
   |                |                |                |    This offset |
   |                |                |                |    includes    |
   |                |                |                |    the File    |
   |                |                |                |    Preamble    |
   |                |                |                |    and the     |
   |                |                |                |    DICM        |
   |                |                |                |    Prefix.     |
   +----------------+----------------+----------------+----------------+
   | >Directory     | (0004,1430)    | 1              | Defines a      |
   | Record Type    |                |                | specialized    |
   |                |                |                | type of        |
   |                |                |                | Directory      |
   |                |                |                | Record by      |
   |                |                |                | reference to   |
   |                |                |                | its position   |
   |                |                |                | in the Media   |
   |                |                |                | Storage        |
   |                |                |                | Directory      |
   |                |                |                | Information    |
   |                |                |                | Model (see     |
   |                |                |                | `Basic         |
   |                |                |                | Directory IOD  |
   |                |                |                | Information    |
   |                |                |                | Model <#       |
   |                |                |                | sect_F.4>`__). |
   |                |                |                |                |
   |                |                |                | PATIENT        |
   |                |                |                | STUDY          |
   |                |                |                | SERIES         |
   |                |                |                | IMAGE          |
   |                |                |                | RADIOTHERAPY   |
   |                |                |                | RT DOSE        |
   |                |                |                | RT             |
   |                |                |                |  STRUCTURE SET |
   |                |                |                | RT PLAN        |
   |                |                |                | R              |
   |                |                |                | T TREAT RECORD |
   |                |                |                | PRESENTATION   |
   |                |                |                | WAVEFORM       |
   |                |                |                | SR DOCUMENT    |
   |                |                |                | KEY OBJECT DOC |
   |                |                |                | SPECTROSCOPY   |
   |                |                |                | RAW DATA       |
   |                |                |                | REGISTRATION   |
   |                |                |                | FIDUCIAL       |
   |                |                |                | HA             |
   |                |                |                | NGING PROTOCOL |
   |                |                |                | ENCAP DOC      |
   |                |                |                | VALUE MAP      |
   |                |                |                | STEREOMETRIC   |
   |                |                |                | PALETTE        |
   |                |                |                | IMPLANT        |
   |                |                |                | IMPLANT GROUP  |
   |                |                |                | IMPLANT ASSY   |
   |                |                |                | MEASUREMENT    |
   |                |                |                | SURFACE        |
   |                |                |                | SURFACE SCAN   |
   |                |                |                | TRACT          |
   |                |                |                | ASSESSMENT     |
   |                |                |                | PRIVATE        |
   |                |                |                |    Privately   |
   |                |                |                |    defined     |
   |                |                |                |    record      |
   |                |                |                |    hierarchy   |
   |                |                |                |    position.   |
   |                |                |                |    Type shall  |
   |                |                |                |    be defined  |
   |                |                |                |    by Private  |
   |                |                |                |    Record UID  |
   |                |                |                |                |
   |                |                |                |   (0004,1432). |
   |                |                |                |                |
   |                |                |                | .. note::      |
   |                |                |                |                |
   |                |                |                |                |
   |                |                |                |  1. Enumerated |
   |                |                |                |       Values   |
   |                |                |                |       PRINT    |
   |                |                |                |       QUEUE,   |
   |                |                |                |       FILM     |
   |                |                |                |       SESSION, |
   |                |                |                |       FILM     |
   |                |                |                |       BOX, and |
   |                |                |                |       IMAGE    |
   |                |                |                |       BOX were |
   |                |                |                |                |
   |                |                |                |     previously |
   |                |                |                |       defined. |
   |                |                |                |       They are |
   |                |                |                |       now      |
   |                |                |                |       retired. |
   |                |                |                |       See      |
   |                |                |                |                |
   |                |                |                |    PS3.3-1998. |
   |                |                |                |                |
   |                |                |                |                |
   |                |                |                |  2. Enumerated |
   |                |                |                |       Values   |
   |                |                |                |       OVERLAY, |
   |                |                |                |       MODALITY |
   |                |                |                |       LUT, VOI |
   |                |                |                |       LUT,     |
   |                |                |                |       CURVE,   |
   |                |                |                |       TOPIC,   |
   |                |                |                |       VISIT,   |
   |                |                |                |       RESULTS, |
   |                |                |                |       I        |
   |                |                |                | NTERPRETATION, |
   |                |                |                |       STUDY    |
   |                |                |                |                |
   |                |                |                |      COMPONENT |
   |                |                |                |       and      |
   |                |                |                |       STORED   |
   |                |                |                |       PRINT    |
   |                |                |                |       were     |
   |                |                |                |                |
   |                |                |                |     previously |
   |                |                |                |       defined. |
   |                |                |                |       They are |
   |                |                |                |       now      |
   |                |                |                |       retired. |
   |                |                |                |       See      |
   |                |                |                |                |
   |                |                |                |     `PS3.3-200 |
   |                |                |                | 4 <ftp://medic |
   |                |                |                | al.nema.org/ME |
   |                |                |                | DICAL/Dicom/20 |
   |                |                |                | 04/printed/04_ |
   |                |                |                | 03pu3.pdf>`__. |
   |                |                |                |                |
   |                |                |                |                |
   |                |                |                |  3. Enumerated |
   |                |                |                |       Value    |
   |                |                |                |       MRDR was |
   |                |                |                |                |
   |                |                |                |     previously |
   |                |                |                |       defined, |
   |                |                |                |       to allow |
   |                |                |                |       indirect |
   |                |                |                |                |
   |                |                |                |      reference |
   |                |                |                |       to a     |
   |                |                |                |       File by  |
   |                |                |                |       multiple |
   |                |                |                |                |
   |                |                |                |      Directory |
   |                |                |                |       Records. |
   |                |                |                |       It is    |
   |                |                |                |       now      |
   |                |                |                |       retired. |
   |                |                |                |       FSUs and |
   |                |                |                |       FSRs are |
   |                |                |                |       unlikely |
   |                |                |                |       to be    |
   |                |                |                |       capable  |
   |                |                |                |       of       |
   |                |                |                |                |
   |                |                |                |     supporting |
   |                |                |                |       this     |
   |                |                |                |                |
   |                |                |                |     mechanism. |
   |                |                |                |       See      |
   |                |                |                |                |
   |                |                |                |    PS3.3-2004. |
   |                |                |                |                |
   |                |                |                |                |
   |                |                |                |  4. Enumerated |
   |                |                |                |       Value    |
   |                |                |                |       HL7      |
   |                |                |                |       STRUC    |
   |                |                |                |       DOC was  |
   |                |                |                |                |
   |                |                |                |     previously |
   |                |                |                |       defined. |
   |                |                |                |       It is    |
   |                |                |                |       now      |
   |                |                |                |       retired. |
   |                |                |                |       See      |
   |                |                |                |                |
   |                |                |                |   PS3.3-2018b. |
   +----------------+----------------+----------------+----------------+
   | >Private       | (0004,1432)    | 1C             | Required if    |
   | Record UID     |                |                | the Directory  |
   |                |                |                | Record Type    |
   |                |                |                | (0004,1430) is |
   |                |                |                | of Value       |
   |                |                |                | PRIVATE. This  |
   |                |                |                | UID is used to |
   |                |                |                | define a       |
   |                |                |                | non-standard   |
   |                |                |                | type of        |
   |                |                |                | Directory      |
   |                |                |                | Record by      |
   |                |                |                | reference to   |
   |                |                |                | its position   |
   |                |                |                | in a private   |
   |                |                |                | extension to   |
   |                |                |                | the Basic      |
   |                |                |                | Directory IOD  |
   |                |                |                | Information    |
   |                |                |                | Model (see     |
   |                |                |                | `Definition of |
   |                |                |                | Specific       |
   |                |                |                | Directory      |
   |                |                |                | Records <#     |
   |                |                |                | sect_F.5>`__). |
   |                |                |                | This UID shall |
   |                |                |                | be registered  |
   |                |                |                | according to   |
   |                |                |                | the procedures |
   |                |                |                | defined in .   |
   |                |                |                | Its meaning    |
   |                |                |                | may or may not |
   |                |                |                | be specified   |
   |                |                |                | in a           |
   |                |                |                | Conformance    |
   |                |                |                | Statement.     |
   +----------------+----------------+----------------+----------------+
   | >Referenced    | (0004,1500)    | 1C             | A Multiple     |
   | File ID        |                |                | Value (see )   |
   |                |                |                | that           |
   |                |                |                | represents the |
   |                |                |                | ordered        |
   |                |                |                | components of  |
   |                |                |                | the File ID    |
   |                |                |                | containing a   |
   |                |                |                | "referenced    |
   |                |                |                | object" or     |
   |                |                |                | Referenced SOP |
   |                |                |                | Instance. A    |
   |                |                |                | maximum of 8   |
   |                |                |                | components,    |
   |                |                |                | each from 1 to |
   |                |                |                | 8 characters   |
   |                |                |                | shall be used  |
   |                |                |                | (see `Coding   |
   |                |                |                | Scheme         |
   |                |                |                | Designator and |
   |                |                |                | Coding Scheme  |
   |                |                |                | Version <#     |
   |                |                |                | sect_8.2>`__). |
   |                |                |                |                |
   |                |                |                | .. note::      |
   |                |                |                |                |
   |                |                |                |    The         |
   |                |                |                |    Referenced  |
   |                |                |                |    File ID     |
   |                |                |                |    provides    |
   |                |                |                |    the means   |
   |                |                |                |    to "locate" |
   |                |                |                |    the File    |
   |                |                |                |    through the |
   |                |                |                |    DICOM File  |
   |                |                |                |    Service     |
   |                |                |                |    provided by |
   |                |                |                |    the Media   |
   |                |                |                |    Format      |
   |                |                |                |    Layer.      |
   |                |                |                |                |
   |                |                |                | All referenced |
   |                |                |                | Files shall be |
   |                |                |                | with the       |
   |                |                |                | File-set to    |
   |                |                |                | which the      |
   |                |                |                | Directory      |
   |                |                |                | belongs. Any   |
   |                |                |                | File within    |
   |                |                |                | the File-set   |
   |                |                |                | (to which the  |
   |                |                |                | Directory      |
   |                |                |                | belongs) shall |
   |                |                |                | be referenced  |
   |                |                |                | by at most one |
   |                |                |                | Directory      |
   |                |                |                | Record. When   |
   |                |                |                | the Directory  |
   |                |                |                | Record does    |
   |                |                |                | not reference  |
   |                |                |                | any SOP        |
   |                |                |                | Instance this  |
   |                |                |                | Attribute      |
   |                |                |                | shall not be   |
   |                |                |                | present.       |
   +----------------+----------------+----------------+----------------+
   | >Referenced    | (0004,1510)    | 1C             | Unique ID for  |
   | SOP Class UID  |                |                | the SOP Class  |
   | in File        |                |                | of the         |
   |                |                |                | Instance       |
   |                |                |                | stored in the  |
   |                |                |                | referenced     |
   |                |                |                | File.          |
   |                |                |                |                |
   |                |                |                | Required if    |
   |                |                |                | the Directory  |
   |                |                |                | Record         |
   |                |                |                | references a   |
   |                |                |                | SOP Instance.  |
   +----------------+----------------+----------------+----------------+
   | >Referenced    | (0004,1511)    | 1C             | Unique         |
   | SOP Instance   |                |                | Identifier for |
   | UID in File    |                |                | the SOP        |
   |                |                |                | Instance       |
   |                |                |                | stored in the  |
   |                |                |                | referenced     |
   |                |                |                | file.          |
   |                |                |                |                |
   |                |                |                | Required if    |
   |                |                |                | the Directory  |
   |                |                |                | Record         |
   |                |                |                | references a   |
   |                |                |                | SOP Instance.  |
   +----------------+----------------+----------------+----------------+
   | >Referenced    | (0004,1512)    | 1C             | Unique         |
   | Transfer       |                |                | Identifier for |
   | Syntax UID in  |                |                | the Transfer   |
   | File           |                |                | Syntax used to |
   |                |                |                | encode the     |
   |                |                |                | Instance       |
   |                |                |                | stored in the  |
   |                |                |                | referenced     |
   |                |                |                | file.          |
   |                |                |                |                |
   |                |                |                | Required if    |
   |                |                |                | the Directory  |
   |                |                |                | Record         |
   |                |                |                | references a   |
   |                |                |                | SOP Instance.  |
   +----------------+----------------+----------------+----------------+
   | >Referenced    | (0004,151A)    | 1C             | Unique ID for  |
   | Related        |                |                | the Related    |
   | General SOP    |                |                | General SOP    |
   | Class UID in   |                |                | Class(es)      |
   | File           |                |                | related to the |
   |                |                |                | SOP Class of   |
   |                |                |                | the Instance   |
   |                |                |                | stored in the  |
   |                |                |                | referenced     |
   |                |                |                | file.          |
   |                |                |                |                |
   |                |                |                | Required if    |
   |                |                |                | the Directory  |
   |                |                |                | Record         |
   |                |                |                | references a   |
   |                |                |                | SOP Instance   |
   |                |                |                | that encodes   |
   |                |                |                | the Related    |
   |                |                |                | General SOP    |
   |                |                |                | Class UID      |
   |                |                |                | (0008,001A).   |
   |                |                |                |                |
   |                |                |                | .. note::      |
   |                |                |                |                |
   |                |                |                |    This may be |
   |                |                |                |    useful to   |
   |                |                |                |    an FSR that |
   |                |                |                |    does not    |
   |                |                |                |    support the |
   |                |                |                |    SOP Class   |
   |                |                |                |    of the      |
   |                |                |                |    referenced  |
   |                |                |                |    Instance,   |
   |                |                |                |    but does    |
   |                |                |                |    support one |
   |                |                |                |    of the      |
   |                |                |                |    Related     |
   |                |                |                |    General SOP |
   |                |                |                |    Classes.    |
   +----------------+----------------+----------------+----------------+
   | >Record        | See            | See            | A number of    |
   | Selection Keys | `Definition of | `Definition of | DICOM Data     |
   |                | Specific       | Specific       | Elements that  |
   |                | Directory      | Directory      | contain        |
   |                | Records        | Records        | specific keys  |
   |                | <#sect_F.5>`__ | <#sect_F.5>`__ | defined for    |
   |                |                |                | each type of   |
   |                |                |                | Directory      |
   |                |                |                | Record         |
   |                |                |                | (0004,1430)    |
   |                |                |                | defined in     |
   |                |                |                | `Definition of |
   |                |                |                | Specific       |
   |                |                |                | Directory      |
   |                |                |                | Records <      |
   |                |                |                | #sect_F.5>`__. |
   +----------------+----------------+----------------+----------------+

.. _sect_F.4:

Basic Directory IOD Information Model
-------------------------------------

The Basic Directory IOD Information Model defines the relationship
between the various types of Directory Records that may be used in
constructing DICOM Directories. This model is based on the DICOM
Application Model defined in this part of the DICOM Standard. Entities
in this Model correspond to Directory Records (DR). These are shown as
rectangular boxes. Each Directory Record in this model is part of a
Directory Entity (not shown except for the Root Entity) that is
referenced by a Directory Record of a higher-level Directory Entity
(e.g., a Study Directory Record references a Directory Entity that
includes Directory Records describing the content of the Study).

Each Directory Record has a number of mandatory and optional keys that
are not shown on this model. They are defined in `Definition of Specific
Directory Records <#sect_F.5>`__. Conventions used are those used by
this part of the DICOM Standard. The model is depicted as an
entity/relationship model in `figure_title <#figure_F.4-1>`__. These
Directory Record relationships are fully specified in
`table_title <#table_F.4-1>`__.

.. table:: Relationship Between Directory Records

   +----------------------+----------------------+----------------------+
   | Directory Record     | Section              | Directory Record     |
   | Type                 |                      | Types that may be    |
   |                      |                      | included in the next |
   |                      |                      | lower-level          |
   |                      |                      | directory Entity     |
   +======================+======================+======================+
   | (Root Directory      |                      | PATIENT, HANGING     |
   | Entity)              |                      | PROTOCOL, PALETTE,   |
   |                      |                      | IMPLANT, IMPLANT     |
   |                      |                      | ASSY, IMPLANT GROUP, |
   |                      |                      | PRIVATE              |
   +----------------------+----------------------+----------------------+
   | PATIENT              | `Patient Directory   | STUDY, PRIVATE       |
   |                      | Record               |                      |
   |                      | Definit              |                      |
   |                      | ion <#sect_F.5.1>`__ |                      |
   +----------------------+----------------------+----------------------+
   | STUDY                | `Study Directory     | SERIES, PRIVATE      |
   |                      | Record               |                      |
   |                      | Definit              |                      |
   |                      | ion <#sect_F.5.2>`__ |                      |
   +----------------------+----------------------+----------------------+
   | SERIES               | `Series Directory    | IMAGE, RT DOSE, RT   |
   |                      | Record               | STRUCTURE SET, RT    |
   |                      | Definit              | PLAN, RT TREAT       |
   |                      | ion <#sect_F.5.3>`__ | RECORD,              |
   |                      |                      | PRESENTATION,        |
   |                      |                      | WAVEFORM, SR         |
   |                      |                      | DOCUMENT, KEY OBJECT |
   |                      |                      | DOC, SPECTROSCOPY,   |
   |                      |                      | RAW DATA,            |
   |                      |                      | REGISTRATION,        |
   |                      |                      | FIDUCIAL, ENCAP DOC, |
   |                      |                      | VALUE MAP,           |
   |                      |                      | STEREOMETRIC, PLAN,  |
   |                      |                      | MEASUREMENT,         |
   |                      |                      | SURFACE, TRACT,      |
   |                      |                      | ASSESSMENT,          |
   |                      |                      | RADIOTHERAPY,        |
   |                      |                      | PRIVATE              |
   +----------------------+----------------------+----------------------+
   | IMAGE                | `Image Directory     | PRIVATE              |
   |                      | Record               |                      |
   |                      | Definit              |                      |
   |                      | ion <#sect_F.5.4>`__ |                      |
   +----------------------+----------------------+----------------------+
   | RT DOSE              | `RT Dose Directory   | PRIVATE              |
   |                      | Record               |                      |
   |                      | Definiti             |                      |
   |                      | on <#sect_F.5.19>`__ |                      |
   +----------------------+----------------------+----------------------+
   | RT STRUCTURE SET     | `RT Structure Set    | PRIVATE              |
   |                      | Directory Record     |                      |
   |                      | Definiti             |                      |
   |                      | on <#sect_F.5.20>`__ |                      |
   +----------------------+----------------------+----------------------+
   | RT PLAN              | `RT Plan Directory   | PRIVATE              |
   |                      | Record               |                      |
   |                      | Definiti             |                      |
   |                      | on <#sect_F.5.21>`__ |                      |
   +----------------------+----------------------+----------------------+
   | RT TREAT RECORD      | `RT Treatment Record | PRIVATE              |
   |                      | Directory Record     |                      |
   |                      | Definiti             |                      |
   |                      | on <#sect_F.5.22>`__ |                      |
   +----------------------+----------------------+----------------------+
   | PRESENTATION         | `Presentation State  | PRIVATE              |
   |                      | Directory Record     |                      |
   |                      | Definiti             |                      |
   |                      | on <#sect_F.5.23>`__ |                      |
   +----------------------+----------------------+----------------------+
   | WAVEFORM             | `Waveform Directory  | PRIVATE              |
   |                      | Record               |                      |
   |                      | Definiti             |                      |
   |                      | on <#sect_F.5.24>`__ |                      |
   +----------------------+----------------------+----------------------+
   | SR DOCUMENT          | `SR Document         | PRIVATE              |
   |                      | Directory Record     |                      |
   |                      | Definiti             |                      |
   |                      | on <#sect_F.5.25>`__ |                      |
   +----------------------+----------------------+----------------------+
   | KEY OBJECT DOC       | `Key Object Document | PRIVATE              |
   |                      | Directory Record     |                      |
   |                      | Definiti             |                      |
   |                      | on <#sect_F.5.26>`__ |                      |
   +----------------------+----------------------+----------------------+
   | SPECTROSCOPY         | `Spectroscopy        | PRIVATE              |
   |                      | Directory Record     |                      |
   |                      | Definiti             |                      |
   |                      | on <#sect_F.5.27>`__ |                      |
   +----------------------+----------------------+----------------------+
   | RAW DATA             | `Raw Data Directory  | PRIVATE              |
   |                      | Record               |                      |
   |                      | Definiti             |                      |
   |                      | on <#sect_F.5.28>`__ |                      |
   +----------------------+----------------------+----------------------+
   | REGISTRATION         | `Registration        | PRIVATE              |
   |                      | Directory Record     |                      |
   |                      | Definiti             |                      |
   |                      | on <#sect_F.5.29>`__ |                      |
   +----------------------+----------------------+----------------------+
   | FIDUCIAL             | `Fiducial Directory  | PRIVATE              |
   |                      | Record               |                      |
   |                      | Definiti             |                      |
   |                      | on <#sect_F.5.30>`__ |                      |
   +----------------------+----------------------+----------------------+
   | HANGING PROTOCOL     | `Hanging Protocol    | PRIVATE              |
   |                      | Directory Record     |                      |
   |                      | Definiti             |                      |
   |                      | on <#sect_F.5.31>`__ |                      |
   +----------------------+----------------------+----------------------+
   | ENCAP DOC            | `Encapsulated        | PRIVATE              |
   |                      | Document Directory   |                      |
   |                      | Record               |                      |
   |                      | Definiti             |                      |
   |                      | on <#sect_F.5.32>`__ |                      |
   +----------------------+----------------------+----------------------+
   | VALUE MAP            | `Real World Value    | PRIVATE              |
   |                      | Mapping Directory    |                      |
   |                      | Record               |                      |
   |                      | Definiti             |                      |
   |                      | on <#sect_F.5.34>`__ |                      |
   +----------------------+----------------------+----------------------+
   | STEREOMETRIC         | `Stereometric        | PRIVATE              |
   |                      | Relationship         |                      |
   |                      | Directory Record     |                      |
   |                      | Definiti             |                      |
   |                      | on <#sect_F.5.35>`__ |                      |
   +----------------------+----------------------+----------------------+
   | PALETTE              | `Palette Directory   | PRIVATE              |
   |                      | Record               |                      |
   |                      | Definiti             |                      |
   |                      | on <#sect_F.5.36>`__ |                      |
   +----------------------+----------------------+----------------------+
   | IMPLANT              | `Implant Directory   | PRIVATE              |
   |                      | Record               |                      |
   |                      | Definiti             |                      |
   |                      | on <#sect_F.5.37>`__ |                      |
   +----------------------+----------------------+----------------------+
   | IMPLANT ASSY         | `Implant Assembly    | PRIVATE              |
   |                      | Directory Record     |                      |
   |                      | Definiti             |                      |
   |                      | on <#sect_F.5.38>`__ |                      |
   +----------------------+----------------------+----------------------+
   | IMPLANT GROUP        | `Implant Group       | PRIVATE              |
   |                      | Directory Record     |                      |
   |                      | Definiti             |                      |
   |                      | on <#sect_F.5.39>`__ |                      |
   +----------------------+----------------------+----------------------+
   | PLAN                 | `Plan Directory      | PRIVATE              |
   |                      | Record               |                      |
   |                      | Definiti             |                      |
   |                      | on <#sect_F.5.40>`__ |                      |
   +----------------------+----------------------+----------------------+
   | MEASUREMENT          | `Measurement         | PRIVATE              |
   |                      | Directory Record     |                      |
   |                      | Definiti             |                      |
   |                      | on <#sect_F.5.41>`__ |                      |
   +----------------------+----------------------+----------------------+
   | SURFACE              | `Surface Directory   | PRIVATE              |
   |                      | Record               |                      |
   |                      | Definiti             |                      |
   |                      | on <#sect_F.5.42>`__ |                      |
   +----------------------+----------------------+----------------------+
   | SURFACE SCAN         | `Surface Scan Mesh   | PRIVATE              |
   |                      | Directory Record     |                      |
   |                      | Definiti             |                      |
   |                      | on <#sect_F.5.43>`__ |                      |
   +----------------------+----------------------+----------------------+
   | TRACT                | `Tractography        | PRIVATE              |
   |                      | Results Directory    |                      |
   |                      | Record               |                      |
   |                      | Definiti             |                      |
   |                      | on <#sect_F.5.44>`__ |                      |
   +----------------------+----------------------+----------------------+
   | ASSESSMENT           | `Content Assessment  | PRIVATE              |
   |                      | Results Directory    |                      |
   |                      | Record               |                      |
   |                      | Definiti             |                      |
   |                      | on <#sect_F.5.45>`__ |                      |
   +----------------------+----------------------+----------------------+
   | RADIOTHERAPY         | `Radiotherapy        | PRIVATE              |
   |                      | Directory Record     |                      |
   |                      | Definiti             |                      |
   |                      | on <#sect_F.5.46>`__ |                      |
   +----------------------+----------------------+----------------------+
   | PRIVATE              | `Private Directory   | PRIVATE, (any of the |
   |                      | Record               | above as privately   |
   |                      | Definit              | defined)             |
   |                      | ion <#sect_F.6.1>`__ |                      |
   +----------------------+----------------------+----------------------+

.. note::

   1. Directory Record Types PRINT QUEUE, FILM SESSION, FILM BOX, and
      IMAGE BOX were previously defined. They have been retired. See
      PS3.3-1998.

   2. Directory Record Types OVERLAY, MODALITY LUT, VOI LUT, CURVE,
      TOPIC, VISIT, RESULTS, INTERPRETATION, STUDY COMPONENT, STORED
      PRINT and MRDR were previously defined. They have been retired.
      See
      `PS3.3-2004 <ftp://medical.nema.org/MEDICAL/Dicom/2004/printed/04_03pu3.pdf>`__.

   3. Directory Record Type HL7 STRUC DOC was previously defined. It has
      been retired. See PS3.3 2018b.

.. _sect_F.5:

Definition of Specific Directory Records
----------------------------------------

The following Sections specify a number of Directory Records that were
introduced by the Basic Directory IOD Information Model presented in
`Basic Directory IOD Information Model <#sect_F.4>`__. For each one, it
identifies the SOP Classes that may be referenced and the related
mandatory keys. Keys are assigned a Type designation that indicates if
it is required for all Media Storage Operations of the Directory (see
`Conventions <#chapter_5>`__).

Type 2 and Type 3 Keys may be changed to Type 1 and Type 2 or 3
respectively by Application Profiles defined in . Keys based on Private
Data Elements, or Private Keys may also be used in addition to Standard
defined Keys. However such Private keys may be ignored by any File-set
Reader or Updater.

.. note::

   Normalized Print media storage was previously defined in DICOM. It is
   now retired. See PS3.3-1998.

.. _sect_F.5.1:

Patient Directory Record Definition
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Directory Record is based on the specification of `Basic Directory
IOD <#sect_F.3>`__. It is identified by a Directory Record Type of Value
"PATIENT." `table_title <#table_F.5-1>`__ lists the set of keys with
their associated Types for such a Directory Record Type. The description
of these keys may be found in the Modules related to the Patient IOD or
the Patient IE of Image IODs. This Type of Directory Record may
reference a Lower-Level Directory Entity that includes one or more
Directory Records as defined in `table_title <#table_F.4-1>`__.

.. table:: Patient Keys

   +----------------------+-------------+------+----------------------+
   | Key                  | Tag         | Type | Attribute            |
   |                      |             |      | Description          |
   +======================+=============+======+======================+
   | Specific Character   | (0008,0005) | 1C   | Required if an       |
   | Set                  |             |      | extended or          |
   |                      |             |      | replacement          |
   |                      |             |      | character set is     |
   |                      |             |      | used in one of the   |
   |                      |             |      | keys                 |
   +----------------------+-------------+------+----------------------+
   | Patient's Name       | (0010,0010) | 2    |                      |
   +----------------------+-------------+------+----------------------+
   | Patient ID           | (0010,0020) | 1    |                      |
   +----------------------+-------------+------+----------------------+
   | *Any other Attribute | 3           |      |                      |
   | of the Patient IE    |             |      |                      |
   | Modules*             |             |      |                      |
   +----------------------+-------------+------+----------------------+

For a given File-set, the Patient ID shall be unique. This means that it
shall not appear in different Patient Directory Records.

.. _sect_F.5.2:

Study Directory Record Definition
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Directory Record is based on the specification of `Basic Directory
IOD <#sect_F.3>`__. It is identified by a Directory Record Type of Value
"STUDY." `table_title <#table_F.5-2>`__ lists the set of keys with their
associated Types for such a Directory Record Type. The description of
these keys may be found in the Modules related to the Study IE of
Composite IODs. This Type of Directory Record may reference a
Lower-Level Directory Entity that includes one or more Directory Records
as defined in `table_title <#table_F.4-1>`__. Only one Study Directory
Record per Study Instance UID shall be present in a Basic Directory
Instance; this implies that a Study belongs to a single patient and
shall be referenced only once for that patient.

.. table:: Study Keys

   +----------------------+-------------+------+----------------------+
   | Key                  | Tag         | Type | Attribute            |
   |                      |             |      | Description          |
   +======================+=============+======+======================+
   | Specific Character   | (0008,0005) | 1C   | Required if an       |
   | Set                  |             |      | extended or          |
   |                      |             |      | replacement          |
   |                      |             |      | character set is     |
   |                      |             |      | used in one of the   |
   |                      |             |      | keys                 |
   +----------------------+-------------+------+----------------------+
   | Study Date           | (0008,0020) | 1    |                      |
   +----------------------+-------------+------+----------------------+
   | Study Time           | (0008,0030) | 1    |                      |
   +----------------------+-------------+------+----------------------+
   | Study Description    | (0008,1030) | 2    |                      |
   +----------------------+-------------+------+----------------------+
   | Study Instance UID   | (0020,000D) | 1C   | Required only if     |
   |                      |             |      | (0004,1511) is       |
   |                      |             |      | absent (see Note).   |
   +----------------------+-------------+------+----------------------+
   | Study ID             | (0020,0010) | 1    |                      |
   +----------------------+-------------+------+----------------------+
   | Accession Number     | (0008,0050) | 2    |                      |
   +----------------------+-------------+------+----------------------+
   | *Any other Attribute | 3           |      |                      |
   | of the Study IE      |             |      |                      |
   | Modules*             |             |      |                      |
   +----------------------+-------------+------+----------------------+

.. note::

   The Study Instance UID shall be present as a mandatory key only if no
   file is referenced by this Directory Record. In the case where this
   Directory Record references a file, the Directory Record contains in
   the Referenced SOP Instance UID in File (0004,1511). In this case
   (0004,1511) may be used as a "pseudo" Directory Record Key (see
   `table_title <#table_F.3-3>`__) and need not be duplicated.

.. _sect_F.5.3:

Series Directory Record Definition
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Directory Record is based on the specification of `Basic Directory
IOD <#sect_F.3>`__. It is identified by a Directory Record Type of Value
"SERIES." `table_title <#table_F.5-3>`__ lists the set of keys with
their associated Types for such a Directory Record Type. The description
of these keys may be found in the Modules related to the Series IE and
Equipment IE of Composite IODs. This type of Directory Record may
reference a Lower-Level Directory Entity that includes one or more
Directory Records as defined in `table_title <#table_F.4-1>`__. Only one
Series Directory Record per Series Instance UID shall be present in a
Basic Directory Instance; this implies that a Series belongs to a single
Study and shall be referenced only once for that Study.

.. table:: Series Keys

   +-------------------+-------------------+------+-------------------+
   | Key               | Tag               | Type | Attribute         |
   |                   |                   |      | Description       |
   +===================+===================+======+===================+
   | Specific          | (0008,0005)       | 1C   | Required if an    |
   | Character Set     |                   |      | extended or       |
   |                   |                   |      | replacement       |
   |                   |                   |      | character set is  |
   |                   |                   |      | used in one of    |
   |                   |                   |      | the keys          |
   +-------------------+-------------------+------+-------------------+
   | Modality          | (0008,0060)       | 1    |                   |
   +-------------------+-------------------+------+-------------------+
   | Series Instance   | (0020,000E)       | 1    |                   |
   | UID               |                   |      |                   |
   +-------------------+-------------------+------+-------------------+
   | Series Number     | (0020,0011)       | 1    |                   |
   +-------------------+-------------------+------+-------------------+
   | Icon Image        | (0088,0200)       | 3    | This Icon Image   |
   | Sequence          |                   |      | is representative |
   |                   |                   |      | of the Series. It |
   |                   |                   |      | may or may not    |
   |                   |                   |      | correspond to one |
   |                   |                   |      | of the images of  |
   |                   |                   |      | the Series.       |
   |                   |                   |      |                   |
   |                   |                   |      | Only a single     |
   |                   |                   |      | Item is permitted |
   |                   |                   |      | in this Sequence. |
   +-------------------+-------------------+------+-------------------+
   | *>Include*        | *See*\ `Icon      |      |                   |
   | \ `table_title <# | Image Key         |      |                   |
   | table_C.7-11b>`__ | Definition <#     |      |                   |
   |                   | sect_F.7>`__\ *.* |      |                   |
   +-------------------+-------------------+------+-------------------+
   | *Any other        | 3                 |      |                   |
   | Attribute of the  |                   |      |                   |
   | Series IE         |                   |      |                   |
   | Modules*          |                   |      |                   |
   +-------------------+-------------------+------+-------------------+

.. _sect_F.5.4:

Image Directory Record Definition
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Directory Record is based on the specification of `Basic Directory
IOD <#sect_F.3>`__. It is identified by a Directory Record Type of Value
"IMAGE." `table_title <#table_F.5-4>`__ lists the set of keys with their
associated Types for such a Directory Record Type. The description of
these keys may be found in the Modules related to the Image IE of Image
IODs. This Directory Record shall be used to reference an Image SOP
Instance. This type of Directory Record may reference a Lower-Level
Directory Entity that includes one or more Directory Records as defined
in `table_title <#table_F.4-1>`__.

.. table:: Image Keys

   +-------------------+-------------------+------+-------------------+
   | Key               | Tag               | Type | Attribute         |
   |                   |                   |      | Description       |
   +===================+===================+======+===================+
   | Specific          | (0008,0005)       | 1C   | Required if an    |
   | Character Set     |                   |      | extended or       |
   |                   |                   |      | replacement       |
   |                   |                   |      | character set is  |
   |                   |                   |      | used in one of    |
   |                   |                   |      | the keys.         |
   +-------------------+-------------------+------+-------------------+
   | Instance Number   | (0020,0013)       | 1    |                   |
   +-------------------+-------------------+------+-------------------+
   | Icon Image        | (0088,0200)       | 3    | This Icon Image   |
   | Sequence          |                   |      | is representative |
   |                   |                   |      | of the Image.     |
   |                   |                   |      |                   |
   |                   |                   |      | Only a single     |
   |                   |                   |      | Item is permitted |
   |                   |                   |      | in this Sequence. |
   +-------------------+-------------------+------+-------------------+
   | *>Include*        | *See*\ `Icon      |      |                   |
   | \ `table_title <# | Image Key         |      |                   |
   | table_C.7-11b>`__ | Definition <#     |      |                   |
   |                   | sect_F.7>`__\ *.* |      |                   |
   +-------------------+-------------------+------+-------------------+
   | *Any other        | 3                 |      |                   |
   | Attribute of the  |                   |      |                   |
   | Image IE Modules* |                   |      |                   |
   +-------------------+-------------------+------+-------------------+

.. note::

   Because Referenced SOP Instance UID in File (0004,1511) may be used
   as a "pseudo" Directory Record Key (see
   `table_title <#table_F.3-3>`__), it is not duplicated in this list of
   keys.

.. _sect_F.5.5:

Standalone Overlay Directory Record Definition
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Retired. See
`PS3.3-2004 <ftp://medical.nema.org/MEDICAL/Dicom/2004/printed/04_03pu3.pdf>`__.

.. _sect_F.5.6:

Standalone Modality LUT Directory Record Definition
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Retired. See
`PS3.3-2004 <ftp://medical.nema.org/MEDICAL/Dicom/2004/printed/04_03pu3.pdf>`__.

.. _sect_F.5.7:

Standalone VOI LUT Directory Record Definition
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Retired. See
`PS3.3-2004 <ftp://medical.nema.org/MEDICAL/Dicom/2004/printed/04_03pu3.pdf>`__.

.. _sect_F.5.8:

Standalone Curve Directory Record Definition
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Retired. See
`PS3.3-2004 <ftp://medical.nema.org/MEDICAL/Dicom/2004/printed/04_03pu3.pdf>`__.

.. _sect_F.5.9:

Topic Directory Record Definition
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Retired. See
`PS3.3-2004 <ftp://medical.nema.org/MEDICAL/Dicom/2004/printed/04_03pu3.pdf>`__.

.. _sect_F.5.10:

Visit Directory Record Definition
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Retired. See
`PS3.3-2004 <ftp://medical.nema.org/MEDICAL/Dicom/2004/printed/04_03pu3.pdf>`__.

.. _sect_F.5.11:

Results Directory Record Definition
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Retired. See
`PS3.3-2004 <ftp://medical.nema.org/MEDICAL/Dicom/2004/printed/04_03pu3.pdf>`__.

.. _sect_F.5.12:

Interpretation Directory Record Definition
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Retired. See
`PS3.3-2004 <ftp://medical.nema.org/MEDICAL/Dicom/2004/printed/04_03pu3.pdf>`__.

.. _sect_F.5.13:

Study Component Directory Record Definition
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Retired. See
`PS3.3-2004 <ftp://medical.nema.org/MEDICAL/Dicom/2004/printed/04_03pu3.pdf>`__.

.. _sect_F.5.14:

Print Queue Directory Record Definition
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This section was previously defined in DICOM. It is now retired. See
PS3.3-1998.

.. _sect_F.5.15:

Film Session Directory Record Definition
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This section was previously defined in DICOM. It is now retired. See
PS3.3-1998.

.. _sect_F.5.16:

Film Box Directory Record Definition
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This section was previously defined in DICOM. It is now retired. See
PS3.3-1998.

.. _sect_F.5.17:

Basic Image Box Directory Record Definition
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This section was previously defined in DICOM. It is now retired. See
PS3.3-1998.

.. _sect_F.5.18:

Stored Print Directory Record Definition
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Retired. See
`PS3.3-2004 <ftp://medical.nema.org/MEDICAL/Dicom/2004/printed/04_03pu3.pdf>`__.

.. _sect_F.5.19:

RT Dose Directory Record Definition
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This Directory Record is based on the specification of `Basic Directory
IOD <#sect_F.3>`__. It is identified by a Directory Record Type of Value
"RT DOSE". `table_title <#table_F.5-19>`__ lists the set of keys with
their associated Types for such a Directory Record Type. The description
of these keys may be found in the Modules related to the Dose IE of the
`RT Dose IOD <#sect_A.18>`__. This Directory Record shall be used to
reference a RT Dose SOP Instance. This Type of Directory Record may
reference a Lower-Level Directory Entity that includes one or more
Directory Records as defined in `table_title <#table_F.4-1>`__.

.. table:: RT Dose Keys

   +-------------------+-------------------+------+-------------------+
   | Key               | Tag               | Type | Attribute         |
   |                   |                   |      | Description       |
   +===================+===================+======+===================+
   | Specific          | (0008,0005)       | 1C   | Required if an    |
   | Character Set     |                   |      | extended or       |
   |                   |                   |      | replacement       |
   |                   |                   |      | character set is  |
   |                   |                   |      | used in one of    |
   |                   |                   |      | the keys.         |
   +-------------------+-------------------+------+-------------------+
   | Instance Number   | (0020,0013)       | 1    |                   |
   +-------------------+-------------------+------+-------------------+
   | Dose Summation    | (3004,000A)       | 1    |                   |
   | Type              |                   |      |                   |
   +-------------------+-------------------+------+-------------------+
   | Dose Comment      | (3004,0006)       | 3    |                   |
   +-------------------+-------------------+------+-------------------+
   | Icon Image        | (0088,0200)       | 3    | This Icon Image   |
   | Sequence          |                   |      | is representative |
   |                   |                   |      | of the RT Dose.   |
   |                   |                   |      |                   |
   |                   |                   |      | Only a single     |
   |                   |                   |      | Item is permitted |
   |                   |                   |      | in this Sequence. |
   +-------------------+-------------------+------+-------------------+
   | *>Include*        | *See*\ `Icon      |      |                   |
   | \ `table_title <# | Image Key         |      |                   |
   | table_C.7-11b>`__ | Definition <#     |      |                   |
   |                   | sect_F.7>`__\ *.* |      |                   |
   +-------------------+-------------------+------+-------------------+
   | *Any other        | 3                 |      |                   |
   | Attribute of the  |                   |      |                   |
   | Dose IE Modules*  |                   |      |                   |
   +-------------------+-------------------+------+-------------------+

.. note::

   Because Referenced SOP Instance UID in File (0004,1511) may be used
   as a "pseudo" Directory Record Key (see
   `table_title <#table_F.3-3>`__), it is not duplicated in this list of
   keys.

.. _sect_F.5.20:

RT Structure Set Directory Record Definition
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This Directory Record is based on the specification of `Basic Directory
IOD <#sect_F.3>`__. It is identified by a Directory Record Type of Value
"RT STRUCTURE SET". `table_title <#table_F.5-20>`__ lists the set of
keys with their associated Types for such a Directory Record Type. The
description of these keys may be found in the Modules related to the
Structure Set IE of the `RT Structure Set IOD <#sect_A.19>`__. This
Directory Record shall be used to reference a RT Structure Set SOP
Instance. This Type of Directory Record may reference a Lower-Level
Directory Entity that includes one or more Directory Records as defined
in `table_title <#table_F.4-1>`__.

.. table:: RT Structure Set Keys

   +----------------------+-------------+------+----------------------+
   | Key                  | Tag         | Type | Attribute            |
   |                      |             |      | Description          |
   +======================+=============+======+======================+
   | Specific Character   | (0008,0005) | 1C   | Required if an       |
   | Set                  |             |      | extended or          |
   |                      |             |      | replacement          |
   |                      |             |      | character set is     |
   |                      |             |      | used in one of the   |
   |                      |             |      | keys.                |
   +----------------------+-------------+------+----------------------+
   | Instance Number      | (0020,0013) | 1    |                      |
   +----------------------+-------------+------+----------------------+
   | Structure Set Label  | (3006,0002) | 1    |                      |
   +----------------------+-------------+------+----------------------+
   | Structure Set Date   | (3006,0008) | 2    |                      |
   +----------------------+-------------+------+----------------------+
   | Structure Set Time   | (3006,0009) | 2    |                      |
   +----------------------+-------------+------+----------------------+
   | *Any other Attribute | 3           |      |                      |
   | of the Structure Set |             |      |                      |
   | IE Modules*          |             |      |                      |
   +----------------------+-------------+------+----------------------+

.. note::

   Because (0004,1511) Referenced SOP Instance UID in File may be used
   as a "pseudo" Directory Record Key (see
   `table_title <#table_F.3-3>`__), it is not duplicated in this list of
   keys.

.. _sect_F.5.21:

RT Plan Directory Record Definition
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This Directory Record is based on the specification of `Basic Directory
IOD <#sect_F.3>`__. It is identified by a Directory Record Type of Value
"RT PLAN". `table_title <#table_F.5-21>`__ lists the set of keys with
their associated Types for such a Directory Record Type. The description
of these keys may be found in the Modules related to the Plan IE of the
`RT Plan IOD <#sect_A.20>`__. This Directory Record shall be used to
reference a RT Plan SOP Instance. This Type of Directory Record may
reference a Lower-Level Directory Entity that includes one or more
Directory Records as defined in `table_title <#table_F.4-1>`__.

.. table:: RT Plan Keys

   +----------------------+-------------+------+----------------------+
   | Key                  | Tag         | Type | Attribute            |
   |                      |             |      | Description          |
   +======================+=============+======+======================+
   | Specific Character   | (0008,0005) | 1C   | Required if an       |
   | Set                  |             |      | extended or          |
   |                      |             |      | replacement          |
   |                      |             |      | character set is     |
   |                      |             |      | used in one of the   |
   |                      |             |      | keys                 |
   +----------------------+-------------+------+----------------------+
   | Instance Number      | (0020,0013) | 1    |                      |
   +----------------------+-------------+------+----------------------+
   | RT Plan Label        | (300A,0002) | 1    |                      |
   +----------------------+-------------+------+----------------------+
   | RT Plan Date         | (300A,0006) | 2    |                      |
   +----------------------+-------------+------+----------------------+
   | RT Plan Time         | (300A,0007) | 2    |                      |
   +----------------------+-------------+------+----------------------+
   | *Any other Attribute | 3           |      |                      |
   | of the Plan IE       |             |      |                      |
   | Modules*             |             |      |                      |
   +----------------------+-------------+------+----------------------+

.. note::

   Because Referenced SOP Instance UID in File (0004,1511) may be used
   as a "pseudo" Directory Record Key (see
   `table_title <#table_F.3-3>`__), it is not duplicated in this list of
   keys.

.. _sect_F.5.22:

RT Treatment Record Directory Record Definition
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This Directory Record is based on the specification of `Basic Directory
IOD <#sect_F.3>`__. It is identified by a Directory Record Type of Value
"RT TREAT RECORD". `table_title <#table_F.5-22>`__ lists the set of keys
with their associated Types for such a Directory Record Type. The
description of these keys may be found in the Modules related to the
Treatment Record IE of the RT Treatment Record IODs. This Directory
Record shall be used to reference an RT Beams Treatment Record SOP
Instance, RT Brachy Treatment Record SOP Instance, or RT Treatment
Summary Record SOP Instance. This Type of Directory Record may reference
a Lower-Level Directory Entity that includes one or more Directory
Records as defined in `table_title <#table_F.4-1>`__.

.. table:: RT Treatment Record Keys

   +----------------------+-------------+------+----------------------+
   | Key                  | Tag         | Type | Attribute            |
   |                      |             |      | Description          |
   +======================+=============+======+======================+
   | Specific Character   | (0008,0005) | 1C   | Required if an       |
   | Set                  |             |      | extended or          |
   |                      |             |      | replacement          |
   |                      |             |      | character set is     |
   |                      |             |      | used in one of the   |
   |                      |             |      | keys                 |
   +----------------------+-------------+------+----------------------+
   | Instance Number      | (0020,0013) | 1    |                      |
   +----------------------+-------------+------+----------------------+
   | Treatment Date       | (3008,0250) | 2    |                      |
   +----------------------+-------------+------+----------------------+
   | Treatment Time       | (3008,0251) | 2    |                      |
   +----------------------+-------------+------+----------------------+
   | *Any other Attribute | 3           |      |                      |
   | of the Treatment     |             |      |                      |
   | Record IE Modules*   |             |      |                      |
   +----------------------+-------------+------+----------------------+

.. note::

   Because Referenced SOP Instance UID in File (0004,1511) may be used
   as a "pseudo" Directory Record Key (see
   `table_title <#table_F.3-3>`__), it is not duplicated in this list of
   keys.

.. _sect_F.5.23:

Presentation State Directory Record Definition
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Directory Record is based on the specification of `Basic Directory
IOD <#sect_F.3>`__. It is identified by a Directory Record Type of Value
"PRESENTATION". `table_title <#table_F.5-23>`__ lists the set of keys
with their associated Types for such a Directory Record Type. The
description of these keys may be found in the Modules related to
Softcopy Presentation State Storage and Structured Display IODs. This
Directory Record shall be used to reference a Softcopy Presentation
State Storage SOP Instance or a Structured Display SOP Instance. This
Type of Directory Record may reference a Lower-Level Directory Entity
that includes one or more Directory Records as defined in
`table_title <#table_F.4-1>`__.

.. table:: Presentation Keys

   +----------------------+-------------+------+----------------------+
   | Key                  | Tag         | Type | Attribute            |
   |                      |             |      | Description          |
   +======================+=============+======+======================+
   | Specific Character   | (0008,0005) | 1C   | Required if an       |
   | Set                  |             |      | extended or          |
   |                      |             |      | replacement          |
   |                      |             |      | character set is     |
   |                      |             |      | used in one of the   |
   |                      |             |      | keys.                |
   +----------------------+-------------+------+----------------------+
   | Presentation         | (0070,0082) | 1    | Date on which this   |
   | Creation Date        |             |      | presentation was     |
   |                      |             |      | created.             |
   |                      |             |      |                      |
   |                      |             |      | .. note::            |
   |                      |             |      |                      |
   |                      |             |      |    This date may be  |
   |                      |             |      |    different from    |
   |                      |             |      |    the date that the |
   |                      |             |      |    DICOM SOP         |
   |                      |             |      |    Instance was      |
   |                      |             |      |    created, since    |
   |                      |             |      |    the presentation  |
   |                      |             |      |    information       |
   |                      |             |      |    contained may     |
   |                      |             |      |    have been         |
   |                      |             |      |    recorded earlier. |
   +----------------------+-------------+------+----------------------+
   | Presentation         | (0070,0083) | 1    | Time at which this   |
   | Creation Time        |             |      | presentation was     |
   |                      |             |      | created.             |
   |                      |             |      |                      |
   |                      |             |      | .. note::            |
   |                      |             |      |                      |
   |                      |             |      |    This time may be  |
   |                      |             |      |    different from    |
   |                      |             |      |    the time that the |
   |                      |             |      |    DICOM SOP         |
   |                      |             |      |    Instance was      |
   |                      |             |      |    created, since    |
   |                      |             |      |    the presentation  |
   |                      |             |      |    information       |
   |                      |             |      |    contained may     |
   |                      |             |      |    have been         |
   |                      |             |      |    recorded earlier. |
   +----------------------+-------------+------+----------------------+
   | *                    |             |      |                      |
   | Include*\ `table_tit |             |      |                      |
   | le <#table_10-12>`__ |             |      |                      |
   +----------------------+-------------+------+----------------------+
   | Referenced Series    | (0008,1115) | 1C   | Sequence of Items    |
   | Sequence             |             |      | where each Item      |
   |                      |             |      | includes the         |
   |                      |             |      | Attributes of one    |
   |                      |             |      | Series to which the  |
   |                      |             |      | Presentation         |
   |                      |             |      | applies.             |
   |                      |             |      |                      |
   |                      |             |      | One or more Items    |
   |                      |             |      | shall be included in |
   |                      |             |      | this Sequence.       |
   |                      |             |      |                      |
   |                      |             |      | Required if the IOD  |
   |                      |             |      | of the Presentation  |
   |                      |             |      | SOP Instance         |
   |                      |             |      | referenced by this   |
   |                      |             |      | directory record     |
   |                      |             |      | includes the         |
   |                      |             |      | `Presentation State  |
   |                      |             |      | Relationship         |
   |                      |             |      | Module               |
   |                      |             |      |  <#sect_C.11.11>`__. |
   +----------------------+-------------+------+----------------------+
   | >Series Instance UID | (0020,000E) | 1    | Unique identifier of |
   |                      |             |      | a Series that is     |
   |                      |             |      | part of this Study.  |
   +----------------------+-------------+------+----------------------+
   | >Referenced Image    | (0008,1140) | 1    | Sequence of Items    |
   | Sequence             |             |      | where each Item      |
   |                      |             |      | provides reference   |
   |                      |             |      | to an Image SOP      |
   |                      |             |      | Instance.            |
   |                      |             |      |                      |
   |                      |             |      | One or more Items    |
   |                      |             |      | shall be included in |
   |                      |             |      | this Sequence.       |
   +----------------------+-------------+------+----------------------+
   | *>>                  |             |      |                      |
   | Include*\ `table_tit |             |      |                      |
   | le <#table_10-11>`__ |             |      |                      |
   +----------------------+-------------+------+----------------------+
   | Blending Sequence    | (0070,0402) | 1C   | Sequence of Items    |
   |                      |             |      | where each Item      |
   |                      |             |      | includes the         |
   |                      |             |      | Attributes of a      |
   |                      |             |      | Study to which the   |
   |                      |             |      | Presentation         |
   |                      |             |      | applies.             |
   |                      |             |      |                      |
   |                      |             |      | Only two Items shall |
   |                      |             |      | be included in this  |
   |                      |             |      | Sequence.            |
   |                      |             |      |                      |
   |                      |             |      | Required if the SOP  |
   |                      |             |      | Instance referenced  |
   |                      |             |      | by this directory    |
   |                      |             |      | record includes      |
   |                      |             |      | Blending Sequence    |
   |                      |             |      | (0070,0402).         |
   +----------------------+-------------+------+----------------------+
   | >Study Instance UID  | (0020,000D) | 1    | Unique identifier    |
   |                      |             |      | for a Study that     |
   |                      |             |      | contains the images  |
   |                      |             |      | to which the         |
   |                      |             |      | Presentation         |
   |                      |             |      | applies.             |
   +----------------------+-------------+------+----------------------+
   | >Referenced Series   | (0008,1115) | 1    | Sequence of Items    |
   | Sequence             |             |      | where each Item      |
   |                      |             |      | includes the         |
   |                      |             |      | Attributes of one    |
   |                      |             |      | Series to which the  |
   |                      |             |      | Presentation         |
   |                      |             |      | applies.             |
   |                      |             |      |                      |
   |                      |             |      | Only a single Item   |
   |                      |             |      | shall be included in |
   |                      |             |      | this Sequence.       |
   +----------------------+-------------+------+----------------------+
   | >>Series Instance    | (0020,000E) | 1    | Unique identifier of |
   | UID                  |             |      | the Series           |
   +----------------------+-------------+------+----------------------+
   | >>Referenced Image   | (0008,1140) | 1    | Sequence of Items    |
   | Sequence             |             |      | where each Item      |
   |                      |             |      | provides reference   |
   |                      |             |      | to an Image SOP      |
   |                      |             |      | Instance to which    |
   |                      |             |      | the Presentation     |
   |                      |             |      | applies.             |
   |                      |             |      |                      |
   |                      |             |      | One or more Items    |
   |                      |             |      | shall be included in |
   |                      |             |      | this Sequence.       |
   +----------------------+-------------+------+----------------------+
   | *>>>                 |             |      |                      |
   | Include*\ `table_tit |             |      |                      |
   | le <#table_10-11>`__ |             |      |                      |
   +----------------------+-------------+------+----------------------+
   | *Any other Attribute | 3           |      |                      |
   | of the Presentation  |             |      |                      |
   | State IE Modules*    |             |      |                      |
   +----------------------+-------------+------+----------------------+

.. note::

   Because Referenced SOP Instance UID in File (0004,1511) may be used
   as a "pseudo" Directory Record Key (see
   `table_title <#table_F.3-3>`__), it is not duplicated in this list of
   keys.

.. _sect_F.5.24:

Waveform Directory Record Definition
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Directory Record is based on the specification of `Basic Directory
IOD <#sect_F.3>`__. It is identified by a Directory Record Type of Value
"WAVEFORM". `table_title <#table_F.5-24>`__ lists the set of keys with
their associated Types for such a Directory Record Type. The description
of these keys may be found in PS3.3 of the DICOM Standard in the Modules
related to the Waveform IE. This Directory Record shall be used to
reference a Waveform SOP Instance. This Type of Directory Record may
reference a Lower-Level Directory Entity that includes one or more
Directory Records as defined in `table_title <#table_F.4-1>`__.

.. table:: Waveform Keys

   +----------------------+-------------+------+----------------------+
   | Key                  | Tag         | Type | Attribute            |
   |                      |             |      | Description          |
   +======================+=============+======+======================+
   | Specific Character   | (0008,0005) | 1C   | Required if an       |
   | Set                  |             |      | extended or          |
   |                      |             |      | replacement          |
   |                      |             |      | character set is     |
   |                      |             |      | used in one of the   |
   |                      |             |      | keys.                |
   +----------------------+-------------+------+----------------------+
   | Instance Number      | (0020,0013) | 1    |                      |
   +----------------------+-------------+------+----------------------+
   | Content Date         | (0008,0023) | 1    |                      |
   +----------------------+-------------+------+----------------------+
   | Content Time         | (0008,0033) | 1    |                      |
   +----------------------+-------------+------+----------------------+
   | *Any other Attribute | 3           |      |                      |
   | of the Waveform IE   |             |      |                      |
   | Modules*             |             |      |                      |
   +----------------------+-------------+------+----------------------+

.. note::

   Because Referenced SOP Instance UID in File (0004,1511) may be used
   as a "pseudo" Directory Record Key (see
   `table_title <#table_F.3-3>`__), it is not duplicated in this list of
   keys.

.. _sect_F.5.25:

SR Document Directory Record Definition
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Directory Record is based on the specification of `Basic Directory
IOD <#sect_F.3>`__. It is identified by a Directory Record Type of Value
"SR DOCUMENT". `table_title <#table_F.5-25>`__ lists the set of keys
with their associated Types for such a Directory Record Type. The
description of these keys may be found in the Modules related to the
Observation IE of Structured Report IOD. This Directory Record shall be
used to reference an SR Document. This type of Directory Record may
reference a Lower-Level Directory Entity that includes one or more
Directory Records as defined in `table_title <#table_F.4-1>`__.

.. table:: SR Document Keys

   +----------------------+-------------+------+----------------------+
   | Key                  | Tag         | Type | Attribute            |
   |                      |             |      | Description          |
   +======================+=============+======+======================+
   | Specific Character   | (0008,0005) | 1C   | Required if an       |
   | Set                  |             |      | extended or          |
   |                      |             |      | replacement          |
   |                      |             |      | character set is     |
   |                      |             |      | used in one of the   |
   |                      |             |      | keys.                |
   +----------------------+-------------+------+----------------------+
   | Instance Number      | (0020,0013) | 1    |                      |
   +----------------------+-------------+------+----------------------+
   | Completion Flag      | (0040,A491) | 1    |                      |
   +----------------------+-------------+------+----------------------+
   | Verification Flag    | (0040,A493) | 1    |                      |
   +----------------------+-------------+------+----------------------+
   | Content Date         | (0008,0023) | 1    |                      |
   +----------------------+-------------+------+----------------------+
   | Content Time         | (0008,0033) | 1    |                      |
   +----------------------+-------------+------+----------------------+
   | Verification         | (0040,A030) | 1C   | Most recent Date and |
   | DateTime             |             |      | Time of verification |
   |                      |             |      | among those defined  |
   |                      |             |      | in the Verifying     |
   |                      |             |      | Observer Sequence    |
   |                      |             |      | (0040,A073).         |
   |                      |             |      |                      |
   |                      |             |      | Required if          |
   |                      |             |      | Verification Flag    |
   |                      |             |      | (0040,A493) is       |
   |                      |             |      | VERIFIED.            |
   +----------------------+-------------+------+----------------------+
   | Concept Name Code    | (0040,A043) | 1    | Code describing the  |
   | Sequence             |             |      | concept represented  |
   |                      |             |      | by the root Content  |
   |                      |             |      | Item (Document       |
   |                      |             |      | Title).              |
   |                      |             |      |                      |
   |                      |             |      | Only a single Item   |
   |                      |             |      | shall be included in |
   |                      |             |      | this Sequence.       |
   +----------------------+-------------+------+----------------------+
   | *>                   |             |      |                      |
   | Include*\ `table_tit |             |      |                      |
   | le <#table_8.8-1>`__ |             |      |                      |
   +----------------------+-------------+------+----------------------+
   | Content Sequence     | (0040,A730) | 1C   | Contains the Target  |
   |                      |             |      | Content Items that   |
   |                      |             |      | modify the Concept   |
   |                      |             |      | Name Code Sequence   |
   |                      |             |      | of the root Content  |
   |                      |             |      | Item (Document       |
   |                      |             |      | Title).              |
   |                      |             |      |                      |
   |                      |             |      | One or more Items    |
   |                      |             |      | shall be included in |
   |                      |             |      | this Sequence.       |
   |                      |             |      |                      |
   |                      |             |      | All, and only,       |
   |                      |             |      | Content Items with   |
   |                      |             |      | the HAS CONCEPT MOD  |
   |                      |             |      | relationship from    |
   |                      |             |      | the root Content     |
   |                      |             |      | Item shall be        |
   |                      |             |      | included in this     |
   |                      |             |      | Sequence.            |
   |                      |             |      |                      |
   |                      |             |      | Required if the root |
   |                      |             |      | Content Item is the  |
   |                      |             |      | Source Content Item  |
   |                      |             |      | of HAS CONCEPT MOD   |
   |                      |             |      | relationships.       |
   +----------------------+-------------+------+----------------------+
   | >Relationship Type   | (0040,A010) | 1    | HAS CONCEPT MOD      |
   +----------------------+-------------+------+----------------------+
   | *>I                  |             |      |                      |
   | nclude*\ `table_titl |             |      |                      |
   | e <#table_C.17-5>`__ |             |      |                      |
   +----------------------+-------------+------+----------------------+
   | Any Attribute of the | 3           |      |                      |
   | Document IE Modules  |             |      |                      |
   +----------------------+-------------+------+----------------------+

.. note::

   Because Referenced SOP Instance UID in File (0004,1511) may be used
   as a "pseudo" Directory Record Key (see
   `table_title <#table_F.3-3>`__), it is not duplicated in this list of
   keys.

.. _sect_F.5.26:

Key Object Document Directory Record Definition
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Directory Record is based on the specification of `Basic Directory
IOD <#sect_F.3>`__. It is identified by a Directory Record Type of Value
"KEY OBJECT DOC". `table_title <#table_F.5-25>`__ lists the set of keys
with their associated Types for such a Directory Record Type. The
description of these keys may be found in the Modules related to the
Document IE of the Key Object Selection IOD. This Directory Record shall
be used to reference a Key Object Selection Document. This type of
Directory Record may reference a Lower-Level Directory Entity that
includes one or more Directory Records as defined in
`table_title <#table_F.4-1>`__.

.. table:: Key Object Document Keys

   +----------------------+-------------+------+----------------------+
   | Key                  | Tag         | Type | Attribute            |
   |                      |             |      | Description          |
   +======================+=============+======+======================+
   | Specific Character   | (0008,0005) | 1C   | Required if an       |
   | Set                  |             |      | extended or          |
   |                      |             |      | replacement          |
   |                      |             |      | character set is     |
   |                      |             |      | used in one of the   |
   |                      |             |      | keys.                |
   +----------------------+-------------+------+----------------------+
   | Instance Number      | (0020,0013) | 1    |                      |
   +----------------------+-------------+------+----------------------+
   | Content Date         | (0008,0023) | 1    |                      |
   +----------------------+-------------+------+----------------------+
   | Content Time         | (0008,0033) | 1    |                      |
   +----------------------+-------------+------+----------------------+
   | Concept Name Code    | (0040,A043) | 1    | Code describing the  |
   | Sequence             |             |      | concept represented  |
   |                      |             |      | by the root Content  |
   |                      |             |      | Item (Document       |
   |                      |             |      | Title).              |
   |                      |             |      |                      |
   |                      |             |      | Only a single Item   |
   |                      |             |      | shall be included in |
   |                      |             |      | this Sequence.       |
   +----------------------+-------------+------+----------------------+
   | *>                   |             |      |                      |
   | Include*\ `table_tit |             |      |                      |
   | le <#table_8.8-1>`__ |             |      |                      |
   +----------------------+-------------+------+----------------------+
   | Content Sequence     | (0040,A730) | 1C   | Contains the Target  |
   |                      |             |      | Content Items that   |
   |                      |             |      | modify the Concept   |
   |                      |             |      | Name Code Sequence   |
   |                      |             |      | of the root Content  |
   |                      |             |      | Item (Document       |
   |                      |             |      | Title).              |
   |                      |             |      |                      |
   |                      |             |      | One or more Items    |
   |                      |             |      | shall be included in |
   |                      |             |      | this Sequence.       |
   |                      |             |      |                      |
   |                      |             |      | All, and only,       |
   |                      |             |      | Content Items with   |
   |                      |             |      | the HAS CONCEPT MOD  |
   |                      |             |      | relationship from    |
   |                      |             |      | the root Content     |
   |                      |             |      | Item shall be        |
   |                      |             |      | included in this     |
   |                      |             |      | Sequence.            |
   |                      |             |      |                      |
   |                      |             |      | Required if the root |
   |                      |             |      | Content Item is the  |
   |                      |             |      | Source Content Item  |
   |                      |             |      | of HAS CONCEPT MOD   |
   |                      |             |      | relationships.       |
   +----------------------+-------------+------+----------------------+
   | >Relationship Type   | (0040,A010) | 1    | HAS CONCEPT MOD      |
   +----------------------+-------------+------+----------------------+
   | *>I                  |             |      |                      |
   | nclude*\ `table_titl |             |      |                      |
   | e <#table_C.17-5>`__ |             |      |                      |
   +----------------------+-------------+------+----------------------+
   | Any Attribute of the | 3           |      |                      |
   | Document IE Modules  |             |      |                      |
   +----------------------+-------------+------+----------------------+

.. note::

   Because Referenced SOP Instance UID in File (0004,1511) may be used
   as a "pseudo" Directory Record Key (see
   `table_title <#table_F.3-3>`__), it is not duplicated in this list of
   keys.

.. _sect_F.5.27:

Spectroscopy Directory Record Definition
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Directory Record is based on the specification of `Basic Directory
IOD <#sect_F.3>`__. It is identified by a Directory Record Type of Value
"SPECTROSCOPY." `table_title <#table_F.5-27>`__ lists the set of keys
with their associated Types for such a Directory Record Type. The
description of these keys may be found in the Modules related to the MR
Spectroscopy IE of MR Spectroscopy IODs. This Directory Record shall be
used to reference a Spectroscopy SOP Instance. This type of Directory
Record may reference a Lower-Level Directory Entity that includes one or
more Directory Records as defined in `table_title <#table_F.4-1>`__.

.. table:: Spectroscopy Keys

   +-------------------+-------------------+------+-------------------+
   | Key               | Tag               | Type | Attribute         |
   |                   |                   |      | Description       |
   +===================+===================+======+===================+
   | Specific          | (0008,0005)       | 1C   | Required if an    |
   | Character Set     |                   |      | extended or       |
   |                   |                   |      | replacement       |
   |                   |                   |      | character set is  |
   |                   |                   |      | used in one of    |
   |                   |                   |      | the keys.         |
   +-------------------+-------------------+------+-------------------+
   | Image Type        | (0008,0008)       | 1    |                   |
   +-------------------+-------------------+------+-------------------+
   | Content Date      | (0008,0023)       | 1    |                   |
   +-------------------+-------------------+------+-------------------+
   | Content Time      | (0008,0033)       | 1    |                   |
   +-------------------+-------------------+------+-------------------+
   | Instance Number   | (0020,0013)       | 1    |                   |
   +-------------------+-------------------+------+-------------------+
   | Referenced Image  | (0008,9092)       | 1C   | Required if       |
   | Evidence Sequence |                   |      | present in the    |
   |                   |                   |      | spectroscopy      |
   |                   |                   |      | Instance.         |
   |                   |                   |      |                   |
   |                   |                   |      | One or more Items |
   |                   |                   |      | shall be included |
   |                   |                   |      | in this Sequence. |
   +-------------------+-------------------+------+-------------------+
   | *>Include         |                   |      |                   |
   | *\ `table_title < |                   |      |                   |
   | #table_C.17-3>`__ |                   |      |                   |
   +-------------------+-------------------+------+-------------------+
   | Number of Frames  | (0028,0008)       | 1    |                   |
   +-------------------+-------------------+------+-------------------+
   | Rows              | (0028,0010)       | 1    |                   |
   +-------------------+-------------------+------+-------------------+
   | Columns           | (0028,0011)       | 1    |                   |
   +-------------------+-------------------+------+-------------------+
   | Data Point Rows   | (0028,9001)       | 1    |                   |
   +-------------------+-------------------+------+-------------------+
   | Data Point        | (0028,9002)       | 1    |                   |
   | Columns           |                   |      |                   |
   +-------------------+-------------------+------+-------------------+
   | Icon Image        | (0088,0200)       | 3    | This Icon Image   |
   | Sequence          |                   |      | is representative |
   |                   |                   |      | of the            |
   |                   |                   |      | Spectroscopy      |
   |                   |                   |      | Instance.         |
   |                   |                   |      |                   |
   |                   |                   |      | Only a single     |
   |                   |                   |      | Item is permitted |
   |                   |                   |      | in this Sequence. |
   +-------------------+-------------------+------+-------------------+
   | *>Include*        | *See*\ `Icon      |      |                   |
   | \ `table_title <# | Image Key         |      |                   |
   | table_C.7-11b>`__ | Definition <#     |      |                   |
   |                   | sect_F.7>`__\ *.* |      |                   |
   +-------------------+-------------------+------+-------------------+
   | *Any other        | 3                 |      |                   |
   | Attribute of the  |                   |      |                   |
   | MR Spectroscopy   |                   |      |                   |
   | IE Modules*       |                   |      |                   |
   +-------------------+-------------------+------+-------------------+

.. note::

   Because Referenced SOP Instance UID in File (0004,1511) may be used
   as a "pseudo" Directory Record Key (see
   `table_title <#table_F.3-3>`__), it is not duplicated in this list of
   keys.

.. _sect_F.5.28:

Raw Data Directory Record Definition
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Directory Record is based on the specification of `Basic Directory
IOD <#sect_F.3>`__. It is identified by a Directory Record Type of Value
"RAW DATA." `table_title <#table_F.5-28>`__ lists the set of keys with
their associated Types for such a Directory Record Type. The description
of these keys may be found in the Modules related to the Raw Data IE of
Raw Data IODs. This Directory Record shall be used to reference a Raw
Data SOP Instance. This type of Directory Record may reference a
Lower-Level Directory Entity that includes one or more Directory Records
as defined in `table_title <#table_F.4-1>`__.

.. table:: Raw Data Keys

   +-------------------+-------------------+------+-------------------+
   | Key               | Tag               | Type | Attribute         |
   |                   |                   |      | Description       |
   +===================+===================+======+===================+
   | Specific          | (0008,0005)       | 1C   | Required if an    |
   | Character Set     |                   |      | extended or       |
   |                   |                   |      | replacement       |
   |                   |                   |      | character set is  |
   |                   |                   |      | used in one of    |
   |                   |                   |      | the keys.         |
   +-------------------+-------------------+------+-------------------+
   | Content Date      | (0008,0023)       | 1    |                   |
   +-------------------+-------------------+------+-------------------+
   | Content Time      | (0008,0033)       | 1    |                   |
   +-------------------+-------------------+------+-------------------+
   | Instance Number   | (0020,0013)       | 2    |                   |
   +-------------------+-------------------+------+-------------------+
   | Icon Image        | (0088,0200)       | 3    | This Icon Image   |
   | Sequence          |                   |      | is representative |
   |                   |                   |      | of the Raw Data   |
   |                   |                   |      | Instance.         |
   |                   |                   |      |                   |
   |                   |                   |      | Only a single     |
   |                   |                   |      | Item is permitted |
   |                   |                   |      | in this Sequence. |
   +-------------------+-------------------+------+-------------------+
   | *>Include*        | *See*\ `Icon      |      |                   |
   | \ `table_title <# | Image Key         |      |                   |
   | table_C.7-11b>`__ | Definition <#     |      |                   |
   |                   | sect_F.7>`__\ *.* |      |                   |
   +-------------------+-------------------+------+-------------------+
   | *Any other        | 3                 |      |                   |
   | Attribute of the  |                   |      |                   |
   | Raw Data IE       |                   |      |                   |
   | Modules*          |                   |      |                   |
   +-------------------+-------------------+------+-------------------+

.. note::

   Because Referenced SOP Instance UID in File (0004,1511) may be used
   as a "pseudo" Directory Record Key (see
   `table_title <#table_F.3-3>`__), it is not duplicated in this list of
   keys.

.. _sect_F.5.29:

Registration Directory Record Definition
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Directory Record is based on the specification of `Basic Directory
IOD <#sect_F.3>`__. It is identified by a Directory Record Type of Value
"REGISTRATION." `table_title <#table_F.5-29>`__ lists the set of keys
with their associated Types for such a Directory Record Type. The
description of these keys may be found in the Modules related to the
Spatial Registration IE of the Spatial Registration IOD. This Directory
Record shall be used to reference a Spatial Registration SOP Instance.
This type of Directory Record may reference a Lower-Level Directory
Entity that includes one or more Directory Records as defined in
`table_title <#table_F.4-1>`__.

.. table:: Registration Keys

   +----------------------+-------------+------+----------------------+
   | Key                  | Tag         | Type | Attribute            |
   |                      |             |      | Description          |
   +======================+=============+======+======================+
   | Specific Character   | (0008,0005) | 1C   | Required if an       |
   | Set                  |             |      | extended or          |
   |                      |             |      | replacement          |
   |                      |             |      | character set is     |
   |                      |             |      | used in one of the   |
   |                      |             |      | keys.                |
   +----------------------+-------------+------+----------------------+
   | Content Date         | (0008,0023) | 1    | The date the content |
   |                      |             |      | creation started.    |
   +----------------------+-------------+------+----------------------+
   | Content Time         | (0008,0033) | 1    | The time the content |
   |                      |             |      | creation started.    |
   +----------------------+-------------+------+----------------------+
   | *                    |             |      |                      |
   | Include*\ `table_tit |             |      |                      |
   | le <#table_10-12>`__ |             |      |                      |
   +----------------------+-------------+------+----------------------+
   | *Any other Attribute | 3           |      |                      |
   | of the Spatial       |             |      |                      |
   | Registration IE      |             |      |                      |
   | Modules*             |             |      |                      |
   +----------------------+-------------+------+----------------------+

.. note::

   Because Referenced SOP Instance UID in File (0004,1511) may be used
   as a "pseudo" Directory Record Key (see
   `table_title <#table_F.3-3>`__), it is not duplicated in this list of
   keys.

.. _sect_F.5.30:

Fiducial Directory Record Definition
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Directory Record is based on the specification of `Basic Directory
IOD <#sect_F.3>`__. It is identified by a Directory Record Type of Value
"FIDUCIAL." `table_title <#table_F.5-30>`__ lists the set of keys with
their associated Types for such a Directory Record Type. The description
of these keys may be found in the Modules related to the Spatial
Fiducials IE of Spatial Fiducials IOD. This Directory Record shall be
used to reference a Spatial Fiducials SOP Instance. This type of
Directory Record may reference a Lower-Level Directory Entity that
includes one or more Directory Records as defined in
`table_title <#table_F.4-1>`__.

.. table:: Fiducial Keys

   +----------------------+-------------+------+----------------------+
   | Key                  | Tag         | Type | Attribute            |
   |                      |             |      | Description          |
   +======================+=============+======+======================+
   | Specific Character   | (0008,0005) | 1C   | Required if an       |
   | Set                  |             |      | extended or          |
   |                      |             |      | replacement          |
   |                      |             |      | character set is     |
   |                      |             |      | used in one of the   |
   |                      |             |      | keys.                |
   +----------------------+-------------+------+----------------------+
   | Content Date         | (0008,0023) | 1    | The date the content |
   |                      |             |      | creation started.    |
   +----------------------+-------------+------+----------------------+
   | Content Time         | (0008,0033) | 1    | The time the content |
   |                      |             |      | creation started.    |
   +----------------------+-------------+------+----------------------+
   | *                    |             |      |                      |
   | Include*\ `table_tit |             |      |                      |
   | le <#table_10-12>`__ |             |      |                      |
   +----------------------+-------------+------+----------------------+
   | *Any other Attribute | 3           |      |                      |
   | of the Spatial       |             |      |                      |
   | Fiducials IE         |             |      |                      |
   | Modules*             |             |      |                      |
   +----------------------+-------------+------+----------------------+

.. note::

   Because Referenced SOP Instance UID in File (0004,1511) may be used
   as a "pseudo" Directory Record Key (see
   `table_title <#table_F.3-3>`__), it is not duplicated in this list of
   keys.

.. _sect_F.5.31:

Hanging Protocol Directory Record Definition
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Directory Record is based on the specification of `Basic Directory
IOD <#sect_F.3>`__. It is identified by a Directory Record Type of Value
"HANGING PROTOCOL". `table_title <#table_F.5-31>`__ lists the set of
keys with their associated Types for such a Directory Record Type. The
description of these keys may be found in the Modules related to the
Hanging Protocol IOD. This Directory Record shall be used to reference a
Hanging Protocol SOP Instance. This type of Directory Record may
reference a Lower-Level Directory Entity that includes one or more
Directory Records as defined in `table_title <#table_F.4-1>`__.

.. table:: Hanging Protocol Keys

   +----------------------+-------------+------+----------------------+
   | Attribute Name       | Tag         | Type | Attribute            |
   |                      |             |      | Description          |
   +======================+=============+======+======================+
   | Specific Character   | (0008,0005) | 1C   | Required if an       |
   | Set                  |             |      | extended or          |
   |                      |             |      | replacement          |
   |                      |             |      | character set is     |
   |                      |             |      | used in one of the   |
   |                      |             |      | keys                 |
   +----------------------+-------------+------+----------------------+
   | Hanging Protocol     | (0072,0002) | 1    |                      |
   | Name                 |             |      |                      |
   +----------------------+-------------+------+----------------------+
   | Hanging Protocol     | (0072,0004) | 1    |                      |
   | Description          |             |      |                      |
   +----------------------+-------------+------+----------------------+
   | Hanging Protocol     | (0072,0006) | 1    |                      |
   | Level                |             |      |                      |
   +----------------------+-------------+------+----------------------+
   | Hanging Protocol     | (0072,0008) | 1    |                      |
   | Creator              |             |      |                      |
   +----------------------+-------------+------+----------------------+
   | Hanging Protocol     | (0072,000A) | 1    |                      |
   | Creation DateTime    |             |      |                      |
   +----------------------+-------------+------+----------------------+
   | Hanging Protocol     | (0072,000C) | 1    | Sequence that        |
   | Definition Sequence  |             |      | defines the type of  |
   |                      |             |      | imaging Studies to   |
   |                      |             |      | which this Hanging   |
   |                      |             |      | Protocol applies.    |
   |                      |             |      |                      |
   |                      |             |      | One or more Items    |
   |                      |             |      | shall be included in |
   |                      |             |      | this Sequence.       |
   +----------------------+-------------+------+----------------------+
   | >Modality            | (0008,0060) | 1C   | Required if Anatomic |
   |                      |             |      | Region Sequence      |
   |                      |             |      | (0008,2218) is not   |
   |                      |             |      | present. May be      |
   |                      |             |      | present otherwise.   |
   +----------------------+-------------+------+----------------------+
   | >Anatomic Region     | (0008,2218) | 1C   | One or more Items    |
   | Sequence             |             |      | shall be included in |
   |                      |             |      | this Sequence.       |
   |                      |             |      |                      |
   |                      |             |      | Required if Modality |
   |                      |             |      | (0008,0060) is not   |
   |                      |             |      | present. May be      |
   |                      |             |      | present otherwise.   |
   +----------------------+-------------+------+----------------------+
   | *>>                  |             |      |                      |
   | Include*\ `table_tit |             |      |                      |
   | le <#table_8.8-1>`__ |             |      |                      |
   +----------------------+-------------+------+----------------------+
   | >Laterality          | (0020,0060) | 2C   | Required if Anatomic |
   |                      |             |      | Region Sequence      |
   |                      |             |      | (0008,2218) is       |
   |                      |             |      | present.             |
   +----------------------+-------------+------+----------------------+
   | >Procedure Code      | (0008,1032) | 2    | Zero or more Items   |
   | Sequence             |             |      | shall be included in |
   |                      |             |      | this Sequence.       |
   +----------------------+-------------+------+----------------------+
   | *>>                  |             |      |                      |
   | Include*\ `table_tit |             |      |                      |
   | le <#table_8.8-1>`__ |             |      |                      |
   +----------------------+-------------+------+----------------------+
   | >Reason for          | (0040,100A) | 2    | Zero or more Items   |
   | Requested Procedure  |             |      | shall be included in |
   | Code Sequence        |             |      | this Sequence.       |
   +----------------------+-------------+------+----------------------+
   | *>>                  |             |      |                      |
   | Include*\ `table_tit |             |      |                      |
   | le <#table_8.8-1>`__ |             |      |                      |
   +----------------------+-------------+------+----------------------+
   | Number of Priors     | (0072,0014) | 1    |                      |
   | Referenced           |             |      |                      |
   +----------------------+-------------+------+----------------------+
   | Hanging Protocol     | (0072,000E) | 2    | Sequence that        |
   | User Identification  |             |      | provides a coded     |
   | Code Sequence        |             |      | identifier for the   |
   |                      |             |      | person, group, or    |
   |                      |             |      | site for which this  |
   |                      |             |      | Hanging Protocol was |
   |                      |             |      | defined.             |
   |                      |             |      |                      |
   |                      |             |      | Zero or one Item     |
   |                      |             |      | shall be included in |
   |                      |             |      | this Sequence.       |
   +----------------------+-------------+------+----------------------+
   | *>                   |             |      |                      |
   | Include*\ `table_tit |             |      |                      |
   | le <#table_8.8-1>`__ |             |      |                      |
   +----------------------+-------------+------+----------------------+
   | *Any other Attribute | 3           |      |                      |
   | of the Hanging       |             |      |                      |
   | Protocol IOD*        |             |      |                      |
   +----------------------+-------------+------+----------------------+

.. note::

   Because Referenced SOP Instance UID in File (0004,1511) may be used
   as a "pseudo" Directory Record Key (see
   `table_title <#table_F.3-3>`__), it is not duplicated in this list of
   keys.

.. _sect_F.5.32:

Encapsulated Document Directory Record Definition
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Directory Record is based on the specification of `Basic Directory
IOD <#sect_F.3>`__. It is identified by a Directory Record Type of Value
"ENCAP DOC." `table_title <#table_F.5-32>`__ lists the set of keys with
their associated Types for such a Directory Record Type. The description
of these keys may be found in the Modules related to the Encapsulated
Document IE of Encapsulated IODs. This Directory Record shall be used to
reference an Encapsulated Document SOP Instance. This type of Directory
Record may reference a Lower-Level Directory Entity that includes one or
more Directory Records as defined in `table_title <#table_F.4-1>`__.

.. note::

   Other Encapsulated Document SOP Classes may be added to the Standard
   in the future and these will likely be referenced by this directory
   record. Therefore, the MIME Type should be checked rather than
   assuming that the referenced file contains PDF.

.. table:: Encapsulated Document Keys

   +----------------------+-------------+------+----------------------+
   | Key                  | Tag         | Type | Attribute            |
   |                      |             |      | Description          |
   +======================+=============+======+======================+
   | Specific Character   | (0008,0005) | 1C   | Required if an       |
   | Set                  |             |      | extended or          |
   |                      |             |      | replacement          |
   |                      |             |      | character set is     |
   |                      |             |      | used in one of the   |
   |                      |             |      | keys.                |
   +----------------------+-------------+------+----------------------+
   | Content Date         | (0008,0023) | 2    | The date the content |
   |                      |             |      | creation started.    |
   +----------------------+-------------+------+----------------------+
   | Content Time         | (0008,0033) | 2    | The time the content |
   |                      |             |      | creation started.    |
   +----------------------+-------------+------+----------------------+
   | Instance Number      | (0020,0013) | 1    | A number that        |
   |                      |             |      | identifies this      |
   |                      |             |      | Instance             |
   +----------------------+-------------+------+----------------------+
   | Document Title       | (0042,0010) | 2    | The title of the     |
   |                      |             |      | document.            |
   +----------------------+-------------+------+----------------------+
   | HL7 Instance         | (0040,E001) | 1C   | Instance Identifier  |
   | Identifier           |             |      | from the referenced  |
   |                      |             |      | HL7 Structured       |
   |                      |             |      | Document, encoded as |
   |                      |             |      | a UID (OID or UUID), |
   |                      |             |      | concatenated with a  |
   |                      |             |      | caret ("^") and      |
   |                      |             |      | Extension value (if  |
   |                      |             |      | Extension is present |
   |                      |             |      | in Instance          |
   |                      |             |      | Identifier).         |
   |                      |             |      |                      |
   |                      |             |      | Required if          |
   |                      |             |      | encapsulated         |
   |                      |             |      | document is an HL7   |
   |                      |             |      | Structured Document. |
   +----------------------+-------------+------+----------------------+
   | Concept Name Code    | (0040,A043) | 2    | A coded              |
   | Sequence             |             |      | representation of    |
   |                      |             |      | the document title.  |
   |                      |             |      |                      |
   |                      |             |      | Zero or one Item     |
   |                      |             |      | shall be included in |
   |                      |             |      | this Sequence.       |
   +----------------------+-------------+------+----------------------+
   | *>                   | *B.*        |      |                      |
   | Include*\ `table_tit |             |      |                      |
   | le <#table_8.8-1>`__ |             |      |                      |
   +----------------------+-------------+------+----------------------+
   | MIME Type of         | (0042,0012) | 1    | The type of the      |
   | Encapsulated         |             |      | encapsulated         |
   | Document             |             |      | document stream      |
   |                      |             |      | described using the  |
   |                      |             |      | MIME Media Type (see |
   |                      |             |      | RFC 2046).           |
   +----------------------+-------------+------+----------------------+
   | *Any other Attribute | 3           |      |                      |
   | of                   |             |      |                      |
   | the*\ `Encapsulated  |             |      |                      |
   | Document             |             |      |                      |
   | Module <#sect        |             |      |                      |
   | _C.24.2>`__\ *except |             |      |                      |
   | Encapsulated         |             |      |                      |
   | Document             |             |      |                      |
   | (0042,0011)*         |             |      |                      |
   +----------------------+-------------+------+----------------------+

.. _sect_F.5.33:

HL7 Structured Document Directory Record Definition
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Retired. See PS3.3 2018b.

.. _sect_F.5.34:

Real World Value Mapping Directory Record Definition
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Directory Record is based on the specification of `Basic Directory
IOD <#sect_F.3>`__. It is identified by a Directory Record Type of Value
"VALUE MAP." `table_title <#table_F.5-34>`__ lists the set of keys with
their associated Types for such a Directory Record Type. The description
of these keys may be found in the Modules related to the Real World
Value Mapping IE of Real World Value Mapping IOD. This Directory Record
shall be used to reference a Real World Value Mapping SOP Instance. This
type of Directory Record may reference a Lower-Level Directory Entity
that includes one or more Directory Records as defined in
`table_title <#table_F.4-1>`__.

.. table:: Real World Value Mapping Keys

   +----------------------+-------------+------+----------------------+
   | Key                  | Tag         | Type | Attribute            |
   |                      |             |      | Description          |
   +======================+=============+======+======================+
   | Specific Character   | (0008,0005) | 1C   | Required if an       |
   | Set                  |             |      | extended or          |
   |                      |             |      | replacement          |
   |                      |             |      | character set is     |
   |                      |             |      | used in one of the   |
   |                      |             |      | keys.                |
   +----------------------+-------------+------+----------------------+
   | Content Date         | (0008,0023) | 1    | The date the content |
   |                      |             |      | creation started.    |
   +----------------------+-------------+------+----------------------+
   | Content Time         | (0008,0033) | 1    | The time the content |
   |                      |             |      | creation started.    |
   +----------------------+-------------+------+----------------------+
   | *                    |             |      |                      |
   | Include*\ `table_tit |             |      |                      |
   | le <#table_10-12>`__ |             |      |                      |
   +----------------------+-------------+------+----------------------+
   | *Any other Attribute | 3           |      |                      |
   | of the Real World    |             |      |                      |
   | Value Mapping IE     |             |      |                      |
   | Modules*             |             |      |                      |
   +----------------------+-------------+------+----------------------+

.. note::

   Because Referenced SOP Instance UID in File (0004,1511) may be used
   as a "pseudo" Directory Record Key (see
   `table_title <#table_F.3-3>`__), it is not duplicated in this list of
   keys.

.. _sect_F.5.35:

Stereometric Relationship Directory Record Definition
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Directory Record is based on the specification of `Basic Directory
IOD <#sect_F.3>`__. It is identified by a Directory Record Type of Value
"STEREOMETRIC". `table_title <#table_F.5-35>`__ lists the set of keys
with their associated Types for such a Directory Record Type. The
description of these keys may be found in the Modules related to the
Stereometric Relationship IE of Stereometric Relationship IOD. This
Directory Record shall be used to reference a Stereometric Relationship
SOP Instance. This type of Directory Record may reference a Lower-Level
Directory Entity that includes one or more Directory Records as defined
in `table_title <#table_F.4-1>`__.

.. table:: Stereometric Relationship Keys

   +----------------------+-------------+------+----------------------+
   | Key                  | Tag         | Type | Attribute            |
   |                      |             |      | Description          |
   +======================+=============+======+======================+
   | Specific Character   | (0008,0005) | 1C   | Required if an       |
   | Set                  |             |      | extended or          |
   |                      |             |      | replacement          |
   |                      |             |      | character set is     |
   |                      |             |      | used in one of the   |
   |                      |             |      | keys.                |
   +----------------------+-------------+------+----------------------+
   | *Any other Attribute | 3           |      |                      |
   | of the Stereometric  |             |      |                      |
   | Relationship IE      |             |      |                      |
   | Modules*             |             |      |                      |
   +----------------------+-------------+------+----------------------+

.. note::

   Because Referenced SOP Instance UID in File (0004,1511) may be used
   as a "pseudo" Directory Record Key (see
   `table_title <#table_F.3-3>`__), it is not duplicated in this list of
   keys.

.. _sect_F.5.36:

Palette Directory Record Definition
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Directory Record is based on the specification of `Basic Directory
IOD <#sect_F.3>`__. It is identified by a Directory Record Type of Value
"PALETTE". `table_title <#table_F.5-36>`__ lists the set of keys with
their associated Types for such a Directory Record Type. The description
of these keys may be found in the Modules related to the Color Palette
IOD. This Directory Record shall be used to reference a Color Palette
SOP Instance. This type of Directory Record may reference a Lower-Level
Directory Entity that includes one or more Directory Records as defined
in `table_title <#table_F.4-1>`__.

.. table:: Palette Keys

   +----------------------+-------------+------+----------------------+
   | Attribute Name       | Tag         | Type | Attribute            |
   |                      |             |      | Description          |
   +======================+=============+======+======================+
   | Specific Character   | (0008,0005) | 1C   | Required if an       |
   | Set                  |             |      | extended or          |
   |                      |             |      | replacement          |
   |                      |             |      | character set is     |
   |                      |             |      | used in one of the   |
   |                      |             |      | keys                 |
   +----------------------+-------------+------+----------------------+
   | Content Label        | (0070,0080) | 1    | A label that is used |
   |                      |             |      | to identify the      |
   |                      |             |      | palette.             |
   +----------------------+-------------+------+----------------------+
   | Content Description  | (0070,0081) | 2    | A description of the |
   |                      |             |      | content of the       |
   |                      |             |      | palette.             |
   +----------------------+-------------+------+----------------------+
   | *Any other Attribute | 3           |      |                      |
   | of the Color Palette |             |      |                      |
   | IOD*                 |             |      |                      |
   +----------------------+-------------+------+----------------------+

.. note::

   Because Referenced SOP Instance UID in File (0004,1511) may be used
   as a "pseudo" Directory Record Key (see
   `table_title <#table_F.3-3>`__), it is not duplicated in this list of
   keys.

.. _sect_F.5.37:

Implant Directory Record Definition
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Directory Record is based on the specification of `Basic Directory
IOD <#sect_F.3>`__. It is identified by a Directory Record Type of Value
"IMPLANT". `table_title <#table_F.5-37>`__ lists the set of keys with
their associated Types for such a Directory Record Type. The description
of these keys may be found in the Generic Implant Template IOD. This
Directory Record shall be used to reference a Generic Implant Template
SOP Instance.

.. table:: Implant Keys

   +---------------------+-------------+------+----------------------+
   | Key                 | Tag         | Type | Attribute            |
   |                     |             |      | Description          |
   +=====================+=============+======+======================+
   | Manufacturer        | (0008,0070) | 1    | Name of the          |
   |                     |             |      | manufacturer that    |
   |                     |             |      | produces the         |
   |                     |             |      | implant.             |
   +---------------------+-------------+------+----------------------+
   | Implant Name        | (0022,1095) | 1    | The (product) name   |
   |                     |             |      | of the implant.      |
   +---------------------+-------------+------+----------------------+
   | Implant Size        | (0068,6210) | 1C   | The size descriptor  |
   |                     |             |      | of the component.    |
   |                     |             |      |                      |
   |                     |             |      | Required if present  |
   |                     |             |      | in the referenced    |
   |                     |             |      | Instance.            |
   +---------------------+-------------+------+----------------------+
   | Implant Part Number | (0022,1097) | 1    | The (product)        |
   |                     |             |      | identifier of the    |
   |                     |             |      | implant.             |
   +---------------------+-------------+------+----------------------+

.. note::

   Because (0004,1511) Referenced SOP Instance UID in File may be used
   as a "pseudo" Directory Record Key (see
   `table_title <#table_F.3-3>`__), it is not duplicated in this list of
   keys.

.. _sect_F.5.38:

Implant Assembly Directory Record Definition
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Directory Record is based on the specification of `Basic Directory
IOD <#sect_F.3>`__. It is identified by a Directory Record Type of Value
"IMPLANT ASSY". `table_title <#table_F.5-38>`__ lists the set of keys
with their associated Types for such a Directory Record Type. The
description of these keys may be found in the Implant Assembly Template
IOD. This Directory Record shall be used to reference an Implant
Assembly Template SOP Instance.

.. table:: Implant Assembly Keys

   +----------------------+-------------+------+----------------------+
   | Key                  | Tag         | Type | Attribute            |
   |                      |             |      | Description          |
   +======================+=============+======+======================+
   | Implant Assembly     | (0076,0001) | 1    | A name given to the  |
   | Template Name        |             |      | assembly described   |
   |                      |             |      | in this Instance.    |
   +----------------------+-------------+------+----------------------+
   | Manufacturer         | (0008,0070) | 1    | Name of the          |
   |                      |             |      | manufacturer that    |
   |                      |             |      | produces the         |
   |                      |             |      | implant.             |
   +----------------------+-------------+------+----------------------+
   | Procedure Type Code  | (0076,0020) | 1    | A code describing    |
   | Sequence             |             |      | the Intervention in  |
   |                      |             |      | which the implant is |
   |                      |             |      | used.                |
   |                      |             |      |                      |
   |                      |             |      | One or more Items    |
   |                      |             |      | shall be included in |
   |                      |             |      | this Sequence.       |
   +----------------------+-------------+------+----------------------+
   | *>                   |             |      |                      |
   | Include*\ `table_tit |             |      |                      |
   | le <#table_8.8-1>`__ |             |      |                      |
   +----------------------+-------------+------+----------------------+

.. note::

   Because (0004,1511) Referenced SOP Instance UID in File may be used
   as a "pseudo" Directory Record Key (see
   `table_title <#table_F.3-3>`__), it is not duplicated in this list of
   keys.

.. _sect_F.5.39:

Implant Group Directory Record Definition
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Directory Record is based on the specification of `Basic Directory
IOD <#sect_F.3>`__. It is identified by a Directory Record Type of Value
"IMPLANT GROUP". `table_title <#table_F.5-39>`__ lists the set of keys
with their associated Types for such a Directory Record Type. The
description of these keys may be found in the Implant Template Group
IOD. This Directory Record shall be used to reference an Implant
Template Group SOP Instance.

.. table:: Implant Group Keys

   +----------------------+-------------+------+----------------------+
   | Key                  | Tag         | Type | Attribute            |
   |                      |             |      | Description          |
   +======================+=============+======+======================+
   | Implant Template     | (0078,0001) | 1    | Name of this group   |
   | Group Name           |             |      |                      |
   +----------------------+-------------+------+----------------------+
   | Implant Template     | (0078,0010) | 3    | Purpose or intent of |
   | Group Description    |             |      | this group.          |
   +----------------------+-------------+------+----------------------+
   | Implant Template     | (0078,0020) | 1    | Person or            |
   | Group Issuer         |             |      | Organization that    |
   |                      |             |      | issued this group.   |
   +----------------------+-------------+------+----------------------+

.. note::

   Because (0004,1511) Referenced SOP Instance UID in File may be used
   as a "pseudo" Directory Record Key (see
   `table_title <#table_F.3-3>`__), it is not duplicated in this list of
   keys.

.. _sect_F.5.40:

Plan Directory Record Definition
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Directory Record is based on the specification of `Basic Directory
IOD <#sect_F.3>`__. It is identified by a Directory Record Type of Value
"PLAN". `table_title <#table_F.5-40>`__ lists the set of keys with their
associated Types for such a Directory Record Type. The description of
these keys may be found in the Modules related to the Plan IEs of `RT
Plan IOD <#sect_A.20>`__ and `RT Ion Plan IOD <#sect_A.49>`__. This
Directory Record shall be used to reference one of the class of Plan SOP
Instances having a Modality (0008,0060) of "PLAN", such as the RT Beams
Delivery Instruction IOD. This type of Directory Record may reference a
Lower-Level Directory Entity that includes one or more Directory Records
as defined in `table_title <#table_F.4-1>`__.

.. table:: Plan Keys

   +----------------------+-------------+------+----------------------+
   | Key                  | Tag         | Type | Attribute            |
   |                      |             |      | Description          |
   +======================+=============+======+======================+
   | Specific Character   | (0008,0005) | 1C   | Required if an       |
   | Set                  |             |      | extended or          |
   |                      |             |      | replacement          |
   |                      |             |      | character set is     |
   |                      |             |      | used in one of the   |
   |                      |             |      | keys.                |
   +----------------------+-------------+------+----------------------+
   | *Any other Attribute | 3           |      |                      |
   | of the Plan IE       |             |      |                      |
   | Modules*             |             |      |                      |
   +----------------------+-------------+------+----------------------+

.. note::

   Because Referenced SOP Instance UID in File (0004,1511) may be used
   as a "pseudo" Directory Record Key (see
   `table_title <#table_F.3-3>`__), it is not duplicated in this list of
   keys.

.. _sect_F.5.41:

Measurement Directory Record Definition
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Directory Record is based on the specification of `Basic Directory
IOD <#sect_F.3>`__. It is identified by a Directory Record Type of Value
"MEASUREMENT". `table_title <#table_F.5-41>`__ lists the set of keys
with their associated Types for such a Directory Record Type. The
description of these keys may be found in the Modules related to the
Measurements IE of the Measurement IODs. This Directory Record shall be
used to reference a Measurement SOP Instance. This type of Directory
Record may reference a Lower-Level Directory Entity that includes one or
more Directory Records as defined in `table_title <#table_F.4-1>`__.

.. table:: Measurement Keys

   +----------------------+-------------+------+----------------------+
   | Key                  | Tag         | Type | Attribute            |
   |                      |             |      | Description          |
   +======================+=============+======+======================+
   | Specific Character   | (0008,0005) | 1C   | Required if an       |
   | Set                  |             |      | extended or          |
   |                      |             |      | replacement          |
   |                      |             |      | character set is     |
   |                      |             |      | used in one of the   |
   |                      |             |      | keys.                |
   +----------------------+-------------+------+----------------------+
   | Content Date         | (0008,0023) | 1    | The date the content |
   |                      |             |      | creation started.    |
   +----------------------+-------------+------+----------------------+
   | Content Time         | (0008,0033) | 1    | The time the content |
   |                      |             |      | creation started.    |
   +----------------------+-------------+------+----------------------+
   | *                    |             |      |                      |
   | Include*\ `table_tit |             |      |                      |
   | le <#table_10-12>`__ |             |      |                      |
   +----------------------+-------------+------+----------------------+
   | *Any other Attribute | 3           |      |                      |
   | of the Measurements  |             |      |                      |
   | IE Modules*          |             |      |                      |
   +----------------------+-------------+------+----------------------+

.. note::

   Because (0004,1511) Referenced SOP Instance UID in File may be used
   as a "pseudo" Directory Record Key (see
   `table_title <#table_F.3-3>`__), it is not duplicated in this list of
   keys.

.. _sect_F.5.42:

Surface Directory Record Definition
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Directory Record is based on the specification of `Basic Directory
IOD <#sect_F.3>`__. It is identified by a Directory Record Type of Value
"SURFACE". `table_title <#table_F.5-42>`__ lists the set of keys with
their associated Types for such a Directory Record Type. The description
of these keys may be found in the Modules related to the Surface IE of
the Surface Segmentation IOD. This Directory Record shall be used to
reference a Surface Segmentation SOP Instance. This type of Directory
Record may reference a Lower-Level Directory Entity that includes one or
more Directory Records as defined in `table_title <#table_F.4-1>`__.

.. table:: Surface Keys

   +----------------------+-------------+------+----------------------+
   | Key                  | Tag         | Type | Attribute            |
   |                      |             |      | Description          |
   +======================+=============+======+======================+
   | Specific Character   | (0008,0005) | 1C   | Required if an       |
   | Set                  |             |      | extended or          |
   |                      |             |      | replacement          |
   |                      |             |      | character set is     |
   |                      |             |      | used in one of the   |
   |                      |             |      | keys.                |
   +----------------------+-------------+------+----------------------+
   | Content Date         | (0008,0023) | 1    | The date the content |
   |                      |             |      | creation started.    |
   +----------------------+-------------+------+----------------------+
   | Content Time         | (0008,0033) | 1    | The time the content |
   |                      |             |      | creation started.    |
   +----------------------+-------------+------+----------------------+
   | *                    |             |      |                      |
   | Include*\ `table_tit |             |      |                      |
   | le <#table_10-12>`__ |             |      |                      |
   +----------------------+-------------+------+----------------------+
   | *Any other Attribute | 3           |      |                      |
   | of the Surface IE    |             |      |                      |
   | Modules*             |             |      |                      |
   +----------------------+-------------+------+----------------------+

.. note::

   Because (0004,1511) Referenced SOP Instance UID in File may be used
   as a "pseudo" Directory Record Key (see
   `table_title <#table_F.3-3>`__), it is not duplicated in this list of
   keys.

.. _sect_F.5.43:

Surface Scan Mesh Directory Record Definition
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Directory Record is based on the specification of `Basic Directory
IOD <#sect_F.3>`__. It is identified by a Directory Record Type of Value
"SURFACE SCAN". `table_title <#table_F.5-43>`__ lists the set of keys
with their associated Types for such a Directory Record Type. The
description of these keys may be found in the Modules related to the
Surface IE of the Surface Scan Mesh and Surface Scan Point Cloud IODs.
This Directory Record shall be used to reference a Surface Scan Mesh SOP
Instance. This type of Directory Record may reference a Lower-Level
Directory Entity that includes one or more Directory Records as defined
in `table_title <#table_F.4-1>`__.

.. table:: Surface Scan Keys

   +----------------------+-------------+------+----------------------+
   | Key                  | Tag         | Type | Attribute            |
   |                      |             |      | Description          |
   +======================+=============+======+======================+
   | Specific Character   | (0008,0005) | 1C   | Required if an       |
   | Set                  |             |      | extended or          |
   |                      |             |      | replacement          |
   |                      |             |      | character set is     |
   |                      |             |      | used in one of the   |
   |                      |             |      | keys.                |
   +----------------------+-------------+------+----------------------+
   | Content Date         | (0008,0023) | 1    | The date the content |
   |                      |             |      | creation started.    |
   +----------------------+-------------+------+----------------------+
   | Content Time         | (0008,0033) | 1    | The time the content |
   |                      |             |      | creation started.    |
   +----------------------+-------------+------+----------------------+
   | *Any other Attribute | 3           |      |                      |
   | of the Surface IE    |             |      |                      |
   | Modules*             |             |      |                      |
   +----------------------+-------------+------+----------------------+

.. note::

   Because (0004,1511) Referenced SOP Instance UID in File may be used
   as a "pseudo" Directory Record Key (see
   `table_title <#table_F.3-3>`__), it is not duplicated in this list of
   keys.

.. _sect_F.5.44:

Tractography Results Directory Record Definition
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Directory Record is based on the specification of `Basic Directory
IOD <#sect_F.3>`__. It is identified by a Directory Record Type of Value
"TRACT". `table_title <#table_F.5-44>`__ lists the set of keys with
their associated Types for such a Directory Record Type. The description
of these keys may be found in the Modules related to the Tractography
Results IE of the Tractography Results IOD. This Directory Record shall
be used to reference a Tractography Results SOP Instance. This type of
Directory Record may reference a Lower-Level Directory Entity that
includes one or more Directory Records as defined in
`table_title <#table_F.4-1>`__.

.. table:: Tractography Results Keys

   +----------------------+-------------+------+----------------------+
   | Key                  | Tag         | Type | Attribute            |
   |                      |             |      | Description          |
   +======================+=============+======+======================+
   | Specific Character   | (0008,0005) | 1C   | Required if an       |
   | Set                  |             |      | extended or          |
   |                      |             |      | replacement          |
   |                      |             |      | character set is     |
   |                      |             |      | used in one of the   |
   |                      |             |      | keys.                |
   +----------------------+-------------+------+----------------------+
   | Content Date         | (0008,0023) | 1    | The date the content |
   |                      |             |      | creation started.    |
   +----------------------+-------------+------+----------------------+
   | Content Time         | (0008,0033) | 1    | The time the content |
   |                      |             |      | creation started.    |
   +----------------------+-------------+------+----------------------+
   | *                    |             |      |                      |
   | Include*\ `table_tit |             |      |                      |
   | le <#table_10-12>`__ |             |      |                      |
   +----------------------+-------------+------+----------------------+
   | *Any other Attribute | 3           |      |                      |
   | of the Tractography  |             |      |                      |
   | Results IE Modules*  |             |      |                      |
   +----------------------+-------------+------+----------------------+

.. note::

   Because (0004,1511) Referenced SOP Instance UID in File may be used
   as a "pseudo" Directory Record Key (see
   `table_title <#table_F.3-3>`__), it is not duplicated in this list of
   keys.

.. _sect_F.5.45:

Content Assessment Results Directory Record Definition
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Directory Record is based on the specification of `Basic Directory
IOD <#sect_F.3>`__. It is identified by a Directory Record Type of Value
"ASSESSMENT". `table_title <#table_F.5-45>`__ lists the set of keys with
their associated Types for such a Directory Record Type. The description
of these keys may be found in the Modules related to the Content
Assessment Results IOD. This Directory Record shall be used to reference
a Content Assessment Results SOP Instance. This type of Directory Record
may reference a Lower-Level Directory Entity that includes one or more
Directory Records as defined in `table_title <#table_F.4-1>`__.

.. table:: Content Assessment Results Directory Record Results Keys

   +----------------------+-------------+------+----------------------+
   | Key                  | Tag         | Type | Attribute            |
   |                      |             |      | Description          |
   +======================+=============+======+======================+
   | Specific Character   | (0008,0005) | 1C   | Required if an       |
   | Set                  |             |      | extended or          |
   |                      |             |      | replacement          |
   |                      |             |      | character set is     |
   |                      |             |      | used in one of the   |
   |                      |             |      | keys.                |
   +----------------------+-------------+------+----------------------+
   | Instance Number      | (0020,0013) | 1    |                      |
   +----------------------+-------------+------+----------------------+
   | Instance Creation    | (0008,0012) | 1    |                      |
   | Date                 |             |      |                      |
   +----------------------+-------------+------+----------------------+
   | Instance Creation    | (0008,0013) | 2    |                      |
   | Time                 |             |      |                      |
   +----------------------+-------------+------+----------------------+
   | Any other Attribute  | 3           |      |                      |
   | of the Content       |             |      |                      |
   | Assessment Results   |             |      |                      |
   | IE Modules           |             |      |                      |
   +----------------------+-------------+------+----------------------+

.. note::

   Because Referenced SOP Instance UID in File (0004,1511) may be used
   as a "pseudo" Directory Record Key (see
   `table_title <#table_F.3-3>`__), it is not duplicated in this list of
   keys.

.. _sect_F.5.46:

Radiotherapy Directory Record Definition
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Directory Record is based on the specification of `Basic Directory
IOD <#sect_F.3>`__. It is identified by a Directory Record Type of Value
"RADIOTHERAPY". `table_title <#table_F.5-46>`__ lists the set of keys
with their associated Types for such a Directory Record Type. The
description of these keys may be found in the Modules related to the
Instance-level IEs of the RT Second-Generation IODs. This Directory
Record shall be used to reference one of the classes of RT
Second-Generation SOP Instances having a Modality (0008,0060) as defined
in `RT Second Generation Objects <#sect_A.86.1>`__. This type of
Directory Record may reference a Lower-Level Directory Entity that
includes one or more Directory Records as defined in
`table_title <#table_F.4-1>`__.

.. table:: Radiotherapy Keys

   +----------------------+-------------+------+----------------------+
   | Key                  | Tag         | Type | Attribute            |
   |                      |             |      | Description          |
   +======================+=============+======+======================+
   | Specific Character   | (0008,0005) | 1C   | Required if an       |
   | Set                  |             |      | extended or          |
   |                      |             |      | replacement          |
   |                      |             |      | character set is     |
   |                      |             |      | used in one of the   |
   |                      |             |      | keys.                |
   +----------------------+-------------+------+----------------------+
   | Instance Number      | (0020,0013) | 1    |                      |
   +----------------------+-------------+------+----------------------+
   | User Content Label   | (3010,0033) | 1C   | Required if User     |
   |                      |             |      | Content Label        |
   |                      |             |      | (3010,0033) is       |
   |                      |             |      | present.             |
   +----------------------+-------------+------+----------------------+
   | User Content Long    | (3010,0034) | 1C   | Required if User     |
   | Label                |             |      | Content Long Label   |
   |                      |             |      | (3010,0034) is       |
   |                      |             |      | present.             |
   +----------------------+-------------+------+----------------------+
   | Content Description  | (0070,0081) | 2    |                      |
   +----------------------+-------------+------+----------------------+
   | Content Creator"s    | (0070,0084) | 2    |                      |
   | Name                 |             |      |                      |
   +----------------------+-------------+------+----------------------+
   | Any other Attribute  | 3           |      |                      |
   | of the RT            |             |      |                      |
   | Second-Generation IE |             |      |                      |
   | Modules              |             |      |                      |
   +----------------------+-------------+------+----------------------+

.. note::

   Because Referenced SOP Instance UID in File (0004,1511) may be used
   as a "pseudo" Directory Record Key (See
   `table_title <#table_F.3-3>`__), it is not duplicated in this list of
   keys.

.. _sect_F.6:

Special Directory Records
-------------------------

.. _sect_F.6.1:

Private Directory Record Definition
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Private Directory Records may also be used in addition to Standard
defined Directory Records. Such Private Records shall follow the
specification of `Basic Directory IOD Overview <#sect_F.2>`__ and `Basic
Directory IOD <#sect_F.3>`__. In addition, if created by File-set
Creators they shall be proper extensions to the DICOM Basic Directory
IOD Information Model specified in `Basic Directory IOD Information
Model <#sect_F.4>`__. By proper extensions it is meant that any File-set
Creator creating private Directory Records shall still meet the
conformance requirements. Thus a File-set Reader or File-set Updater
that chooses to ignore such privately defined Directory Records will
find a conformant Directory.

.. _sect_F.6.2:

Multi-referenced File Directory Record Definition
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Retired. See
`PS3.3-2004 <ftp://medical.nema.org/MEDICAL/Dicom/2004/printed/04_03pu3.pdf>`__.

.. _sect_F.7:

Icon Image Key Definition
-------------------------

An Icon Image may be used as a key representative of an Image, RT Dose,
Spectroscopy, Raw Data or Series in a corresponding Directory Record to
allow an application to display icons that enable a user to select one
or more from amongst several of them. It is based on the general purpose
Image Pixel Macro (see `Information Module Definitions
(Normative) <#chapter_C>`__).

The Icon Image Key corresponds to Data Element (0088,0200). It is
defined as a Sequence that contains a single Item encapsulating the Data
Set made of the Data Elements of the Icon Image. The Data Elements are
defined by the Image Pixel Macro (see `Image Pixel
Module <#sect_C.7.6.3>`__).

The Image Pixel Macro usage is restricted in a few areas to facilitate
general use in Directory Record across various modality environments.
These restrictions are:

a. Only monochrome and palette color images shall be used. Samples per
   Pixel (0028,0002) shall have a Value of 1, Photometric Interpretation
   (0028,0004) shall have a Value of either MONOCHROME 1, MONOCHROME 2
   or PALETTE COLOR, Planar Configuration (0028,0006) shall not be
   present.

   .. note::

      True color icon images are not supported. This is due to the fact
      that the reduced size of the Icon Image makes the quality of a
      palette color image (with 256 colors) sufficient in most cases.
      This simplifies the handling of Icon Images by File-set Readers
      and File-set Updaters.

b. If an FSR/FSU supports Icons (i.e., does not ignore them) then it
   shall support at least a maximum size of 64 by 64 Icons. An FSC may
   write Icons of any size. Icons larger than 64 by 64 may be ignored by
   FSRs and FSUs unless specialized by Application Profiles.

c. Pixel samples shall have a Value of either 1 or 8 for Bits Allocated
   (0028,0100) and Bits Stored (0028,0101). High Bit (0028,0102) shall
   have a Value of one less than the Value used in Bit Stored.

d. Pixel Representation (0028,0103) shall specify an unsigned integer
   representation (Value 0000H).

e. Pixel Aspect Ratio (0028,0034) shall have a Value of 1:1.

f. If a Palette Color lookup Table is used, Bits Allocated (0028,0100)
   shall have a Value of 8.

