.. _chapter_7:

DICOM File Format
=================

The DICOM File Format provides a means to encapsulate in a file the Data
Set representing a SOP Instance related to a DICOM IOD. As shown in
`figure_title <#figure_7-1>`__, the byte stream of the Data Set is
placed into the file after the DICOM File Meta Information. Each file
contains a single SOP Instance.

.. _sect_7.1:

DICOM File Meta Information
---------------------------

The File Meta Information includes identifying information on the
encapsulated Data Set. This header consists of a 128 byte File Preamble,
followed by a 4 byte DICOM prefix, followed by the File Meta Elements
shown in `table_title <#table_7.1-1>`__. This header shall be present in
every DICOM file.

The File Preamble is available for use as defined by Application
Profiles or specific implementations. This Part of the DICOM Standard
does not require any structure for this fixed size Preamble. It is not
required to be structured as a DICOM Data Element with a Tag and a
Length. It is intended to facilitate access to the images and other data
in the DICOM file by providing compatibility with a number of commonly
used computer image file formats. Whether or not the File Preamble
contains information, the DICOM File content shall conform to the
requirements of this Part and the Data Set shall conform to the SOP
Class specified in the File Meta Information.

.. note::

   1. If the File Preamble is not used by an Application Profile or a
      specific implementation, all 128 bytes shall be set to 00H. This
      is intended to facilitate the recognition that the Preamble is
      used when all 128 bytes are not set as specified above.

   2. The File Preamble may for example contain information enabling a
      multi-media application to randomly access images stored in a
      DICOM Data Set. The same file can be accessed in two ways: by a
      multi-media application using the preamble and by a DICOM
      Application that ignores the preamble.

The four byte DICOM Prefix shall contain the character string "DICM"
encoded as uppercase characters of the ISO 8859 G0 Character Repertoire.
This four byte prefix is not structured as a DICOM Data Element with a
Tag and a Length.

The Preamble and Prefix are followed by a set of DICOM Meta Elements
with Tags and Lengths as defined in `table_title <#table_7.1-1>`__.

.. table:: DICOM File Meta Information

   +-------------------+-------------------+------+-------------------+
   | Attribute Name    | Tag               | Type | Attribute         |
   |                   |                   |      | Description       |
   +===================+===================+======+===================+
   | File Preamble     | *No Tag or Length | 1    | A fixed 128 byte  |
   |                   | Fields*           |      | field available   |
   |                   |                   |      | for Application   |
   |                   |                   |      | Profile or        |
   |                   |                   |      | implementation    |
   |                   |                   |      | specified use. If |
   |                   |                   |      | not used by an    |
   |                   |                   |      | Application       |
   |                   |                   |      | Profile or a      |
   |                   |                   |      | specific          |
   |                   |                   |      | implementation    |
   |                   |                   |      | all bytes shall   |
   |                   |                   |      | be set to 00H.    |
   |                   |                   |      |                   |
   |                   |                   |      | File-set Readers  |
   |                   |                   |      | or Updaters shall |
   |                   |                   |      | not rely on the   |
   |                   |                   |      | content of this   |
   |                   |                   |      | Preamble to       |
   |                   |                   |      | determine that    |
   |                   |                   |      | this File is or   |
   |                   |                   |      | is not a DICOM    |
   |                   |                   |      | File.             |
   +-------------------+-------------------+------+-------------------+
   | DICOM Prefix      | *No Tag or Length | 1    | Four bytes        |
   |                   | Fields*           |      | containing the    |
   |                   |                   |      | character string  |
   |                   |                   |      | "DICM". This      |
   |                   |                   |      | Prefix is         |
   |                   |                   |      | intended to be    |
   |                   |                   |      | used to recognize |
   |                   |                   |      | that this File is |
   |                   |                   |      | or is not a DICOM |
   |                   |                   |      | File.             |
   +-------------------+-------------------+------+-------------------+
   | File Meta         | (0002,0000)       | 1    | Number of bytes   |
   | Information Group |                   |      | following this    |
   | Length            |                   |      | File Meta Element |
   |                   |                   |      | (end of the Value |
   |                   |                   |      | field) up to and  |
   |                   |                   |      | including the     |
   |                   |                   |      | last File Meta    |
   |                   |                   |      | Element of the    |
   |                   |                   |      | Group 2 File Meta |
   |                   |                   |      | Information       |
   +-------------------+-------------------+------+-------------------+
   | File Meta         | (0002,0001)       | 1    | This is a two     |
   | Information       |                   |      | byte field where  |
   | Version           |                   |      | each bit          |
   |                   |                   |      | identifies a      |
   |                   |                   |      | version of this   |
   |                   |                   |      | File Meta         |
   |                   |                   |      | Information       |
   |                   |                   |      | header. In        |
   |                   |                   |      | version 1 the     |
   |                   |                   |      | first byte value  |
   |                   |                   |      | is 00H and the    |
   |                   |                   |      | second value byte |
   |                   |                   |      | value is 01H.     |
   |                   |                   |      |                   |
   |                   |                   |      | Implementations   |
   |                   |                   |      | reading Files     |
   |                   |                   |      | with Meta         |
   |                   |                   |      | Information where |
   |                   |                   |      | this attribute    |
   |                   |                   |      | has bit 0 (lsb)   |
   |                   |                   |      | of the second     |
   |                   |                   |      | byte set to 1 may |
   |                   |                   |      | interpret the     |
   |                   |                   |      | File Meta         |
   |                   |                   |      | Information as    |
   |                   |                   |      | specified in this |
   |                   |                   |      | version of        |
   |                   |                   |      | PS3.10. All other |
   |                   |                   |      | bits shall not be |
   |                   |                   |      | checked.          |
   |                   |                   |      |                   |
   |                   |                   |      | .. note::         |
   |                   |                   |      |                   |
   |                   |                   |      |    A bit field    |
   |                   |                   |      |    where each bit |
   |                   |                   |      |    identifies a   |
   |                   |                   |      |    version,       |
   |                   |                   |      |    allows         |
   |                   |                   |      |    explicit       |
   |                   |                   |      |    indication of  |
   |                   |                   |      |    the support of |
   |                   |                   |      |    multiple       |
   |                   |                   |      |    previous       |
   |                   |                   |      |    versions.      |
   |                   |                   |      |    Future         |
   |                   |                   |      |    versions of    |
   |                   |                   |      |    the File Meta  |
   |                   |                   |      |    Information    |
   |                   |                   |      |    that can be    |
   |                   |                   |      |    read by        |
   |                   |                   |      |    version 1      |
   |                   |                   |      |    readers will   |
   |                   |                   |      |    have bit 0 of  |
   |                   |                   |      |    the second     |
   |                   |                   |      |    byte set to 1  |
   +-------------------+-------------------+------+-------------------+
   | Media Storage SOP | (0002,0002)       | 1    | Uniquely          |
   | Class UID         |                   |      | identifies the    |
   |                   |                   |      | SOP Class         |
   |                   |                   |      | associated with   |
   |                   |                   |      | the Data Set. SOP |
   |                   |                   |      | Class UIDs        |
   |                   |                   |      | allowed for media |
   |                   |                   |      | storage are       |
   |                   |                   |      | specified in -    |
   |                   |                   |      | Media Storage     |
   |                   |                   |      | Application       |
   |                   |                   |      | Profiles.         |
   +-------------------+-------------------+------+-------------------+
   | Media Storage SOP | (0002,0003)       | 1    | Uniquely          |
   | Instance UID      |                   |      | identifies the    |
   |                   |                   |      | SOP Instance      |
   |                   |                   |      | associated with   |
   |                   |                   |      | the Data Set      |
   |                   |                   |      | placed in the     |
   |                   |                   |      | file and          |
   |                   |                   |      | following the     |
   |                   |                   |      | File Meta         |
   |                   |                   |      | Information.      |
   +-------------------+-------------------+------+-------------------+
   | Transfer Syntax   | (0002,0010)       | 1    | Uniquely          |
   | UID               |                   |      | identifies the    |
   |                   |                   |      | Transfer Syntax   |
   |                   |                   |      | used to encode    |
   |                   |                   |      | the following     |
   |                   |                   |      | Data Set. This    |
   |                   |                   |      | Transfer Syntax   |
   |                   |                   |      | does not apply to |
   |                   |                   |      | the File Meta     |
   |                   |                   |      | Information.      |
   |                   |                   |      |                   |
   |                   |                   |      | .. note::         |
   |                   |                   |      |                   |
   |                   |                   |      |    It is          |
   |                   |                   |      |    recommended to |
   |                   |                   |      |    use one of the |
   |                   |                   |      |    DICOM Transfer |
   |                   |                   |      |    Syntaxes       |
   |                   |                   |      |    supporting     |
   |                   |                   |      |    explicit Value |
   |                   |                   |      |    Representation |
   |                   |                   |      |    encoding to    |
   |                   |                   |      |    facilitate     |
   |                   |                   |      |    interpretation |
   |                   |                   |      |    of File Meta   |
   |                   |                   |      |    Element        |
   |                   |                   |      |    Values. JPIP   |
   |                   |                   |      |    Referenced     |
   |                   |                   |      |    Pixel Data     |
   |                   |                   |      |    Transfer       |
   |                   |                   |      |    Syntaxes are   |
   |                   |                   |      |    not used (see  |
   |                   |                   |      |    ).             |
   +-------------------+-------------------+------+-------------------+
   | Implementation    | (0002,0012)       | 1    | Uniquely          |
   | Class UID         |                   |      | identifies the    |
   |                   |                   |      | implementation    |
   |                   |                   |      | that wrote this   |
   |                   |                   |      | file and its      |
   |                   |                   |      | content. It       |
   |                   |                   |      | provides an       |
   |                   |                   |      | unambiguous       |
   |                   |                   |      | identification of |
   |                   |                   |      | the type of       |
   |                   |                   |      | implementation    |
   |                   |                   |      | that last wrote   |
   |                   |                   |      | the file in the   |
   |                   |                   |      | event of          |
   |                   |                   |      | interchange       |
   |                   |                   |      | problems. It      |
   |                   |                   |      | follows the same  |
   |                   |                   |      | policies as       |
   |                   |                   |      | defined by        |
   |                   |                   |      | (association      |
   |                   |                   |      | negotiation).     |
   +-------------------+-------------------+------+-------------------+
   | Implementation    | (0002,0013)       | 3    | Identifies a      |
   | Version Name      |                   |      | version for an    |
   |                   |                   |      | Implementation    |
   |                   |                   |      | Class UID         |
   |                   |                   |      | (0002,0012) using |
   |                   |                   |      | up to 16          |
   |                   |                   |      | characters of the |
   |                   |                   |      | repertoire        |
   |                   |                   |      | identified in     |
   |                   |                   |      | `Character        |
   |                   |                   |      | Se                |
   |                   |                   |      | t <#sect_8.5>`__. |
   |                   |                   |      | It follows the    |
   |                   |                   |      | same policies as  |
   |                   |                   |      | defined by        |
   |                   |                   |      | (association      |
   |                   |                   |      | negotiation).     |
   +-------------------+-------------------+------+-------------------+
   | Source            | (0002,0016)       | 3    | The DICOM         |
   | Application       |                   |      | Application       |
   | Entity Title      |                   |      | Entity (AE) Title |
   |                   |                   |      | of the AE that    |
   |                   |                   |      | wrote this file's |
   |                   |                   |      | content (or last  |
   |                   |                   |      | updated it). If   |
   |                   |                   |      | used, it allows   |
   |                   |                   |      | the tracing of    |
   |                   |                   |      | the source of     |
   |                   |                   |      | errors in the     |
   |                   |                   |      | event of media    |
   |                   |                   |      | interchange       |
   |                   |                   |      | problems. The     |
   |                   |                   |      | policies          |
   |                   |                   |      | associated with   |
   |                   |                   |      | AE Titles are the |
   |                   |                   |      | same as those     |
   |                   |                   |      | defined in .      |
   |                   |                   |      |                   |
   |                   |                   |      | .. note::         |
   |                   |                   |      |                   |
   |                   |                   |      |    If the Data    |
   |                   |                   |      |    Set was        |
   |                   |                   |      |    created de     |
   |                   |                   |      |    novo by the    |
   |                   |                   |      |    application    |
   |                   |                   |      |    writing the    |
   |                   |                   |      |    file, its AE   |
   |                   |                   |      |    Title, if it   |
   |                   |                   |      |    has one, may   |
   |                   |                   |      |    be used. If    |
   |                   |                   |      |    the Data Set   |
   |                   |                   |      |    was received   |
   |                   |                   |      |    over the       |
   |                   |                   |      |    network, there |
   |                   |                   |      |    is potential   |
   |                   |                   |      |    ambiguity as   |
   |                   |                   |      |    to whether the |
   |                   |                   |      |    value is the   |
   |                   |                   |      |    same as        |
   |                   |                   |      |    Sending        |
   |                   |                   |      |    Application    |
   |                   |                   |      |    Entity Title   |
   |                   |                   |      |    (0002,0017) or |
   |                   |                   |      |    Receiving      |
   |                   |                   |      |    Application    |
   |                   |                   |      |    Entity Title   |
   |                   |                   |      |    (0002,0018) or |
   |                   |                   |      |    some other     |
   |                   |                   |      |    value.         |
   +-------------------+-------------------+------+-------------------+
   | Sending           | (0002,0017)       | 3    | The DICOM         |
   | Application       |                   |      | Application       |
   | Entity Title      |                   |      | Entity (AE) Title |
   |                   |                   |      | of the AE that    |
   |                   |                   |      | sent this file's  |
   |                   |                   |      | content over a    |
   |                   |                   |      | network.          |
   |                   |                   |      |                   |
   |                   |                   |      | .. note::         |
   |                   |                   |      |                   |
   |                   |                   |      |    This is the AE |
   |                   |                   |      |    that was the   |
   |                   |                   |      |    sender         |
   |                   |                   |      |    (source) of    |
   |                   |                   |      |    the content    |
   |                   |                   |      |    (the Data      |
   |                   |                   |      |    Set), in the   |
   |                   |                   |      |    case of a Data |
   |                   |                   |      |    Set sent over  |
   |                   |                   |      |    the network    |
   |                   |                   |      |    (i.e., the     |
   |                   |                   |      |    Calling AET of |
   |                   |                   |      |    the SCU for a  |
   |                   |                   |      |    C-STORE        |
   |                   |                   |      |    operation). If |
   |                   |                   |      |    the Data Set   |
   |                   |                   |      |    was instead    |
   |                   |                   |      |    created de     |
   |                   |                   |      |    novo by the    |
   |                   |                   |      |    application    |
   |                   |                   |      |    writing the    |
   |                   |                   |      |    file, it       |
   |                   |                   |      |    should not be  |
   |                   |                   |      |    present.       |
   +-------------------+-------------------+------+-------------------+
   | Receiving         | (0002,0018)       | 3    | The DICOM         |
   | Application       |                   |      | Application       |
   | Entity Title      |                   |      | Entity (AE) Title |
   |                   |                   |      | of the AE that    |
   |                   |                   |      | received this     |
   |                   |                   |      | file's content    |
   |                   |                   |      | over a network.   |
   |                   |                   |      |                   |
   |                   |                   |      | .. note::         |
   |                   |                   |      |                   |
   |                   |                   |      |    This is the AE |
   |                   |                   |      |    that was the   |
   |                   |                   |      |    recipient      |
   |                   |                   |      |    (destination)  |
   |                   |                   |      |    of the content |
   |                   |                   |      |    (the Data      |
   |                   |                   |      |    Set), in the   |
   |                   |                   |      |    case of a Data |
   |                   |                   |      |    Set received   |
   |                   |                   |      |    over the       |
   |                   |                   |      |    network (i.e., |
   |                   |                   |      |    the Called AET |
   |                   |                   |      |    of the SCP for |
   |                   |                   |      |    a C-STORE      |
   |                   |                   |      |    operation). If |
   |                   |                   |      |    the Data Set   |
   |                   |                   |      |    was instead    |
   |                   |                   |      |    created de     |
   |                   |                   |      |    novo by the    |
   |                   |                   |      |    application    |
   |                   |                   |      |    writing the    |
   |                   |                   |      |    file, it       |
   |                   |                   |      |    should not be  |
   |                   |                   |      |    present.       |
   +-------------------+-------------------+------+-------------------+
   | Source            | (0002,0026)       | 3    | The DICOM         |
   | Presentation      |                   |      | Presentation      |
   | Address           |                   |      | Address           |
   |                   |                   |      | corresponding to  |
   |                   |                   |      | the Source        |
   |                   |                   |      | Application       |
   |                   |                   |      | Entity Title      |
   |                   |                   |      | (0002,0016).      |
   |                   |                   |      |                   |
   |                   |                   |      | See `Presentation |
   |                   |                   |      | Address           |
   |                   |                   |      | Attributes <#     |
   |                   |                   |      | sect_7.1.1.1>`__. |
   +-------------------+-------------------+------+-------------------+
   | Sending           | (0002,0027)       | 3    | The DICOM         |
   | Presentation      |                   |      | Presentation      |
   | Address           |                   |      | Address           |
   |                   |                   |      | corresponding to  |
   |                   |                   |      | the Sending       |
   |                   |                   |      | Application       |
   |                   |                   |      | Entity Title      |
   |                   |                   |      | (0002,0017).      |
   |                   |                   |      |                   |
   |                   |                   |      | See `Presentation |
   |                   |                   |      | Address           |
   |                   |                   |      | Attributes <#     |
   |                   |                   |      | sect_7.1.1.1>`__. |
   +-------------------+-------------------+------+-------------------+
   | Receiving         | (0002,0028)       | 3    | The DICOM         |
   | Presentation      |                   |      | Presentation      |
   | Address           |                   |      | Address           |
   |                   |                   |      | corresponding to  |
   |                   |                   |      | the Receiving     |
   |                   |                   |      | Application       |
   |                   |                   |      | Entity Title      |
   |                   |                   |      | (0002,0018).      |
   |                   |                   |      |                   |
   |                   |                   |      | See `Presentation |
   |                   |                   |      | Address           |
   |                   |                   |      | Attributes <#     |
   |                   |                   |      | sect_7.1.1.1>`__. |
   +-------------------+-------------------+------+-------------------+
   | Private           | (0002,0100)       | 3    | The UID of the    |
   | Information       |                   |      | creator of the    |
   | Creator UID       |                   |      | private           |
   |                   |                   |      | information       |
   |                   |                   |      | (0002,0102).      |
   +-------------------+-------------------+------+-------------------+
   | Private           | (0002,0102)       | 1C   | Contains Private  |
   | Information       |                   |      | Information       |
   |                   |                   |      | placed in the     |
   |                   |                   |      | File Meta         |
   |                   |                   |      | Information. The  |
   |                   |                   |      | creator shall be  |
   |                   |                   |      | identified in     |
   |                   |                   |      | (0002,0100).      |
   |                   |                   |      | Required if       |
   |                   |                   |      | Private           |
   |                   |                   |      | Information       |
   |                   |                   |      | Creator UID       |
   |                   |                   |      | (0002,0100) is    |
   |                   |                   |      | present.          |
   +-------------------+-------------------+------+-------------------+

Except for the 128 byte preamble and the 4 byte prefix, the File Meta
Information shall be encoded using the Explicit VR Little Endian
Transfer Syntax (UID=1.2.840.10008.1.2.1) as defined in DICOM . Values
of each File Meta Element shall be padded when necessary to achieve an
even length, as specified in by their corresponding Value
Representation. The Unknown (UN) Value Representation shall not be used
in the File Meta Information. For compatibility with future versions of
this Standard, any Tag (0002,xxxx) not defined in
`table_title <#table_7.1-1>`__ shall be ignored.

Values of all Tags (0002,xxxx) are reserved for use by this Standard and
later versions of DICOM. Data Elements with a group of 0002 shall not be
used in Data Sets other than within the File Meta Information.

.. note::

   specifies that Elements with Tags (0001,xxxx), (0003,xxxx),
   (0005,xxxx), and (0007,xxxx) shall not be used.

.. _sect_7.1.1:

DICOM File Meta Information Attributes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. _sect_7.1.1.1:

Presentation Address Attributes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The encoding of the presentation address depends on the network
transport protocol.

For objects exchanged using the DICOM Upper Layer Protocol for TCP/IP,
the presentation address shall be encoded as a URI consisting of the
scheme "dicom" followed by a colon, then either the fully qualified host
name or IP address, followed by a colon and then the port number. E.g.,
"dicom:127.0.0.1:104", "dicom:myhost.mydomain.com:104".

For objects exchanged using the Web Services, the presentation address
shall be encoded as the absolute URL of the endpoint of the base of the
resource or service, sufficient to identify the system. E.g.,
"http://myhost.mydomain.com:80/wado-rs/". The presentation address is
not expected to be the complete address of the resource. The scheme
shall be "http", regardless of whether secure transport was actually
used or not.

.. note::

   For security reasons, care should be taken to assure that no access
   credentials such as usernames, passwords or authentication token
   parameters are encoded in the presentation address.

.. _sect_7.2:

Data Set Encapsulation
----------------------

Each File shall contain a single Data Set representing a single SOP
Instance related to a single SOP Class (and corresponding IOD).

.. note::

   A file may contain more than a single 2D image frame as specific IODs
   may be defined to include multiple frames.

The Transfer Syntax used to encode the Data Set shall be the one
identified by the Transfer Syntax UID of the DICOM File Meta
Information.

.. note::

   1. The Transfer Syntax used to encode the Data Set cannot be changed
      within the Data Set; i.e., the Transfer Syntax UID Data Element
      may not occur anywhere within the Data Set, e.g., nested within a
      Sequence Item.

   2. A DICOM Data Set does not include its total length. The end of the
      file indication provided by the DICOM File Service (see `File
      Content Access <#sect_8.4>`__) is the only indication of the end
      of the Data Set.

The last Data Element of a Data Set may be Data Element (FFFC,FFFC) if
padding of a Data Set is desired when a file is written. The Value of
this Data Set Trailing Padding Data Element (FFFC,FFFC) has no
significance and shall be ignored by all DICOM implementations reading
this Data Set. File-set Readers or Updaters shall be able to process
this Data Set Trailing Padding (FFFC,FFFC) either in the Data Set
following the Meta Information or in Data Sets nested in a Sequence (see
).

.. _sect_7.3:

Support of File Management Information
--------------------------------------

The DICOM File Format does not include file management information in
order to avoid duplication with functions related to the Media Format
Layer. If necessary for a given DICOM Application Profile, the following
information should be offered by the Media Format Layer:

a. File content owner identification;

b. File access statistics (e.g., date and time of creation);

c. Application file access control;

d. Physical media access control (e.g., write protect).

.. _sect_7.4:

Secure DICOM File Format
------------------------

A Secure DICOM File shall contain a single DICOM File encapsulated with
the Cryptographic Message Syntax as defined in RFC3369. Depending on the
cryptographic algorithms used for encapsulation, a Secure DICOM File can
provide one or more the following security properties:

-  Data Confidentiality (by means of encryption)

-  Data Origin Authentication (by means of certificates and digital
   signatures)

-  Data Integrity (by means of digital signatures)

In addition, a Secure DICOM File offers the possibility to communicate
encryption keys and certificates to the intended recipients by means of
key transport, key agreement or symmetric key-encryption key schemes.

.. _sect_7.5:

Security Considerations for DICOM File Format
---------------------------------------------

The DICOM File Format has a potential security vulnerability when the
128-byte File Preamble contains malicious executable content. Such
malicious executable content may also refer to other malicious content
in the file hidden within Data Elements of the File Meta Information or
the Data Set.

Depending upon the use and purpose of a particular application it may be
appropriate to:

-  Sanitize the preamble, such as by:

   -  Verifying that the preamble is:

      -  all zeroes, or

      -  begins with a valid magic number for recognized dual format
         content (e.g., TIFF or BigTIFF), or

      -  contains other known safe content.

   -  Clearing the preamble regardless of its content

      .. note::

         This will prevent use by applications that depend on the
         non-DICOM format, if the dual format capability has been used.

   -  Testing explicitly for executable preamble contents.

      .. note::

         The proper response to the presence of executable content
         depends upon the purpose of the application, but generally,
         legitimate executable content will not be found in a DICOM
         File. A hypothetical example of an exception would be if the
         file contained its own executable viewer; this is sufficiently
         unlikely as to be not worth considering.

-  Test explicitly for executable content anywhere within the DICOM
   File.

-  Validate that the DICOM values, structures and content comply with
   the standard encoding rules and the IOD of the specified SOP Class,
   including Private Data Elements.

   .. note::

      Validation that Data Element Values comply with their Value
      Representation may partially mitigate the risk of hidden malicious
      content, but it may be necessary to remove or analyze the contents
      of opaque binary data in OB or other binary numeric value Data
      Elements, whether they be Standard or Private Data Elements. The
      VR of Private Data Elements may not be known. Without an
      executable preamble, such hidden content may not be directly
      executable, but may still serve as a repository of malicious code
      to be activated by some other accompanying exploit.

-  Validate that the contents are of the appropriate SOP Classes.

-  Validate that DICOM File Format files created for HTTP requests and
   responses do not contain such malicious content.

   .. note::

      For example, it may be appropriate for an archive that stores and
      retrieves PS3.10 Files to verify and validate both input and
      output, rather than store and retrieve files without checking the
      content.

The proper response to a validation failure depends upon the purpose of
the application. Validation might be performed on input, output, or
both.

.. note::

   For example, an archive may choose to sanitize SOP Instances upon
   receipt, sanitize SOP Instances upon retrieval, validate the
   structure and fail storage requests for SOP Instances that fail
   validation, or other behavior based on the product purpose and the
   threat environment. This behavior is not specified by DICOM because
   the product purpose and the threat environment are highly dependent
   upon the application.

An implementation shall describe in its Conformance Statement its
behavior with respect to sanitization of the preamble and any other
validation performed.

