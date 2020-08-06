.. _chapter_6:

Value Encoding
==============

A Data Set is constructed by encoding the values of Attributes specified
in the Information Object Definition (IOD) of a Real-World Object. The
specific content and semantics of these Attributes are specified in
Information Object Definitions (see ). The range of possible data types
of these values and their encoding are specified in this section. The
structure of a Data Set, which is composed of Data Elements containing
these values, is specified in `The Data Set <#chapter_7>`__.

Throughout this Part, as well as other parts of the DICOM Standard, Tags
are used to identify both specific Attributes and their corresponding
Data Elements.

.. _sect_6.1:

Support of Character Repertoires
--------------------------------

Values that are text or character strings can be composed of Graphic and
Control Characters. The Graphic Character set, independent of its
encoding, is referred to as a Character Repertoire. Depending on the
native language context in which Application Entities wish to exchange
data using the DICOM Standard, different Character Repertoires will be
used. The Character Repertoires supported by DICOM are:

-  ISO 8859

-  JIS X 0201-1976 Code for Information Interchange

-  JIS X 0208-1990 Code for the Japanese Graphic Character set for
   information interchange

-  JIS X 0212-1990 Code of the supplementary Japanese Graphic Character
   set for information interchange

-  KS X 1001 (registered as ISO-IR 149) for Korean Language

-  TIS 620-2533 (1990) Thai Characters Code for Information Interchange

-  ISO 10646-1, 10646-2, and their associated supplements and extensions
   for Unicode character set

-  GB 18030

-  GB2312

-  GBK

.. note::

   1. The ISO 10646-1, 10646-2, and their associated supplements and
      extensions correspond to the Unicode version 3.2 character set.
      The ISO IR 192 corresponds to the use of the UTF-8 encoding for
      this character set.

   2. The GB 18030 character set is harmonized with the Unicode
      character set on a regular basis, to reflect updates from both the
      Chinese language and from Unicode extensions to support other
      languages.

   3. The issue of font selection is not addressed by the DICOM
      Standard. Issues such as proper display of words like "bone" in
      Chinese or Japanese usage are managed through font selection.
      Similarly, other user interface issues like bidirectional
      character display and text orientation are not addressed by the
      DICOM Standard. The Unicode documents provide extensive
      documentation on these issues.

   4. The GBK character set is an extension of the GB 2312-1980
      character set and supports the Chinese characters in GB 13000.1-93
      that is the Chinese adaptation of Unicode 1.1. The GBK is code
      point backward compatible to GB2312-1980. The GB 18030 character
      set is an extension of the GBK character set for support of
      Unicode 3.2, and provides backward code point compatibility.

.. _sect_6.1.1:

Representation of Encoded Character Values
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

As defined in the ISO Standards referenced in this section, byte values
used for encoded representations of characters are represented in this
section as two decimal numbers in the form column/row.

This means that the value can be calculated as (column \* 16) + row,
e.g., 01/11 corresponds to the value 27 (1BH).

.. note::

   Two digit hex notation will be used throughout the remainder of this
   Standard to represent character encoding. The column/row notation is
   used only within `Support of Character Repertoires <#sect_6.1>`__ to
   simplify any cross referencing with applicable ISO standards.

The byte encoding space is divided into four ranges of values:

-  CL bytes from 00/00 to 01/15

-  GL bytes from 02/00 to 07/15

-  CR bytes from 08/00 to 09/15

-  GR bytes from 10/00 to 15/15

.. note::

   ISO 8859 does not differentiate between a code element, e.g., G0, and
   the area in the code table, e.g., GL, where it is invoked. The term
   "G0" specifies the code element as well as the area in the code
   table. In ISO/IEC 2022 there is a clear distinction between the code
   elements (G0, G1, G2, and G3) and the areas in which the code
   elements are invoked (GL or GR). In this Standard the nomenclature of
   ISO/IEC 2022 is used.

The Control Character set C0 shall be invoked in CL and the Graphic
Character sets G0 and G1 in GL and GR respectively. Only some Control
Characters from the C0 set are used in DICOM (see `Control
Characters <#sect_6.1.3>`__), and characters from the C1 set shall not
be used.

.. _sect_6.1.2:

Graphic Characters
~~~~~~~~~~~~~~~~~~

A Character Repertoire, or character set, is a collection of Graphic
Characters specified independently of their encoding.

.. _sect_6.1.2.1:

Default Character Repertoire
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The default repertoire for character strings in DICOM shall be the Basic
G0 Set of the International Reference Version of ISO 646:1990 (ISO-IR
6). See `DICOM Default Character Repertoire (Normative) <#chapter_E>`__
for a table of the DICOM default repertoire and its encoding.

.. note::

   This Basic G0 Set is identical with the common character set of ISO
   8859.

.. _sect_6.1.2.2:

Extension or Replacement of the Default Character Repertoire
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

DICOM Application Entities (AEs) that extend or replace the default
repertoire convey this information in the Specific Character Set
(0008,0005) Attribute.

.. note::

   The Attribute Specific Character Set (0008,0005) is encoded using a
   subset of characters from ISO-IR 6. See the definition for the Value
   Representation (VR) of Code String (CS) in
   `table_title <#table_6.2-1>`__.

For Data Elements with Value Representations of SH (Short String), LO
(Long String), UC (Unlimited Characters), ST (Short Text), LT (Long
Text), UT (Unlimited Text) or PN (Person Name) the Default Character
Repertoire may be extended or replaced (these Value Representations are
described in more detail in `Value Representation (VR) <#sect_6.2>`__).
If such an extension or replacement is used, the relevant "Specific
Character Set" shall be defined as an attribute of the SOP Common Module
(0008,0005) (see ) and shall be stated in the Conformance Statement.
gives conformance guidelines.

.. note::

   1. Preferred repertoires as defined in ENV 41 503 and ENV 41 508 for
      the use in Western and Eastern Europe, respectively, are: ISO-IR
      100, ISO-IR 101, ISO-IR 144, ISO-IR 126. See `Encoding of
      Character Repertoires <#sect_6.1.2.3>`__.

   2. Information Object Definitions using different character sets
      cannot rely per se on lexical ordering or string comparison of
      data elements represented as character strings. These operations
      can only be carried out within a given character repertoire and
      not across repertoire boundaries.

.. _sect_6.1.2.3:

Encoding of Character Repertoires
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The 7-bit Default Character Repertoire can be replaced for use in Value
Representations SH, LO, ST, LT, PN, UC and UT with one of the
single-byte codes defined in .

.. note::

   This replacement character repertoire does not apply to other textual
   Value Representations (AE and CS).

The replacement character repertoire shall be specified in value 1 of
the Attribute Specific Character Set (0008,0005). Defined Terms for the
Attribute Specific Character Set are specified in .

.. note::

   1. The code table is split into the GL area, which supports a 94
      character set only (bit combinations 02/01 to 07/14) plus SPACE in
      02/00, and the GR area, which supports either a 94 or 96 character
      set (bit combinations 10/01 to 15/14 or 10/00 to 15/15). The
      default character set (ISO-IR 6) is always invoked in the GL area.

   2. All character sets specified in ISO 8859 include ISO-IR 6. This
      set will always be invoked in the GL area of the code table and is
      the equivalent of ASCII (ANSI X3.4:1986), whereas the various
      extension repertoires are mapped onto the GR area of the code
      table.

   3. The 8-bit code table of JIS X 0201 includes ISO-IR 14 (romaji
      alphanumeric characters) as the G0 code element and ISO-IR 13
      (katakana phonetic characters) as the G1 code element. ISO-IR 14
      is identical to ISO-IR 6, except that bit combination 05/12
      represents a "¥" (YEN SIGN) and bit combination 07/14 represents
      an over-line.

Two character codes of the single-byte character sets invoked in the GL
area of the code table, 02/00 and 05/12, have special significance in
the DICOM Standard. The character SPACE, represented by bit combination
02/00, shall be used for the padding of Data Element Values that are
character strings. The Graphic Character represented by the bit
combination 05/12, "\" (BACKSLASH) in the repertoire ISO-IR 6, shall
only be used in character strings with Value Representations of UT, ST
and LT (see `Value Representation (VR) <#sect_6.2>`__). Otherwise the
character code 05/12 is used as a separator for multi-valued Data
Elements (see `Value Multiplicity (VM) and Delimitation <#sect_6.4>`__).

.. note::

   When the value of the Attribute Specific Character Set (0008,0005) is
   either "ISO_IR 13" or "ISO 2022 IR 13", the graphic character
   represented by the bit combination 05/12 is a "¥" (YEN SIGN) in the
   character set of ISO-IR 14.

The character DELETE (bit combination 07/15) shall not be used in DICOM
character strings.

The replacement Character Repertoire specified in value 1 of the
Attribute Specific Character Set (0008,0005) (or the Default Character
Repertoire if value 1 is empty) may be further extended with additional
Coded Character Sets, if needed and permitted by the replacement
Character Repertoire. The additional Coded Character Sets and extension
mechanism shall be specified in additional values of the Attribute
Specific Character Set. If Attribute Specific Character Set (0008,0005)
has a single value, the DICOM SOP Instance supports only one code table
and no Code Extension techniques. If Attribute Specific Character Set
(0008,0005) has multiple values, the DICOM SOP Instance supports Code
Extension techniques as described in ISO/IEC 2022:1994.

The Character Repertoires that prohibit extension are identified in Part
3.

.. note::

   1. Considerations on the Handling of Unsupported Character Sets:

      In DICOM, character sets are not negotiated between Application
      Entities but are indicated by a conditional attribute of the SOP
      Common Module. Therefore, implementations may be confronted with
      character sets that are unknown to them.

      The Unicode Standard includes a substantial discussion of the
      recommended means for display and print for characters that lack
      font support. These same recommendations may apply to the
      mechanisms for unsupported character sets.

      The machine should print or display such characters by replacing
      all unknown characters with the four characters "\nnn", where
      "nnn" is the three digit octal representation of each byte.

      An example of this for an ASCII based machine would be as follows:

      Character String: *Günther*

      Encoded representation: 04/07 15/12 06/14 07/04 06/08 06/05 07/02

      ASCII based machine: G\374nther

      Implementations may also encounter Control Characters that they
      have no means to print or display. The machine may print or
      display such Control Characters by replacing the Control Character
      with the four characters "\nnn", where "nnn" is the three digit
      octal representation of each byte.

   2. Considerations for missing fonts

      The Unicode standard and the GB18030 standard define mechanisms
      for print and display of characters that are missing from the
      available fonts. If GBK is specified in Specific Character Set
      (0008,0005), the GB 18030 rules of print and display of characters
      shall apply. The DICOM Standard does not specify user interface
      behavior since it does not affect network or media data exchange.

   3. The Unicode and GB18030 standards have distinct Yen symbol,
      backslash, and several forms of reverse solidus. The separator for
      multi-valued data elements in DICOM is the character valued 05/12
      regardless of what glyph is used to enter or display this
      character. The other reverse solidus characters that have a very
      similar appearance are not separators. The choice of font can
      affect the appearance of 05/12 significantly. Multi-byte encoding
      systems, such as GB18030, GBK and ISO 2022, may generate encodings
      that contain a byte valued 05/12. Only the character that encodes
      as a single byte valued 05/12 is a delimiter.

      For multi-valued Data Elements, existing implementations that are
      expecting only single-byte replacement character sets may
      misinterpret the Value Multiplicity of the Data Element as a
      consequence of interpreting 05/12 bytes in multi-byte characters
      or ISO 2022 escape sequences as delimiters, and this may affect
      the integrity of store-and-forward operations. Applications that
      do not explicitly state support for GB18030, GBK or ISO 2022 in
      their conformance statement, might exhibit such behavior.

.. _sect_6.1.2.4:

Code Extension Techniques
^^^^^^^^^^^^^^^^^^^^^^^^^

For Data Elements with Value Representations of SH (Short String), LO
(Long String), UC (Unlimited Characters), ST (Short Text), LT (Long
Text), UT (Unlimited Text) or PN (Person Name), the Default Character
Repertoire or the character repertoire specified by value 1 of Attribute
Specific Character Set (0008,0005), may be extended using the Code
Extension techniques specified by ISO/IEC 2022:1994.

If such Code Extension techniques are used, the related Specific
Character Set or Sets shall be specified by value 2 to value n of the
Attribute Specific Character Set (0008,0005) of the SOP Common Module
(see ), and shall be stated in the Conformance Statement.

.. note::

   1. Defined Terms for Specific Character Set (0008,0005) are defined
      in .

   2. Support for Japanese kanji (ideographic), hiragana (phonetic),
      katakana (phonetic), Korean (Hangul phonetic and Hanja
      ideographic) and Chinese characters is defined in .

   3. The Chinese Character Set (GB18030) and Unicode (ISO 10646-1,
      10646-2) do not allow the use of Code Extension Techniques. If
      either of these character sets is used, no other character set may
      be specified in the Specific Character Set (0008,0005) attribute,
      that is, it may have only one value.

.. _sect_6.1.2.5:

Usage of Code Extension
^^^^^^^^^^^^^^^^^^^^^^^

DICOM supports Code Extension techniques if the Attribute Specific
Character Set (0008,0005) is multi-valued. The method employed for Code
Extension in DICOM is as described in ISO/IEC 2022:1994. The following
assumptions shall be made and the following restrictions shall apply:

.. _sect_6.1.2.5.1:

Assumed Initial States
''''''''''''''''''''''

-  Code element G0 and code element G1 (in 8-bit mode only) are always
   invoked in the GL and GR areas of the code table respectively.
   Designated character sets for these code elements are immediately in
   use. Code elements G2 and G3 are not used.

-  The primary set of Control Characters shall always be designated as
   the C0 code element and this shall be invoked in the CL area of the
   code table. The C1 code element shall not be used.

.. _sect_6.1.2.5.2:

Restrictions for Code Extension
'''''''''''''''''''''''''''''''

-  As code elements G0 and G1 always have shift status, Locking Shifts
   (SI, SO) are not required and shall not be used.

-  As code elements G2 and G3 are not used, Single Shifts (SS2 and SS3)
   cannot be used.

-  Only the ESC sequences specified in shall be used to activate Code
   Elements.

.. _sect_6.1.2.5.3:

Requirements
''''''''''''

The character set specified by value 1 of the Attribute Specific
Character Set (0008,0005), or the Default Character Repertoire if value
1 is missing, shall be active at the beginning of each textual Data
Element value, and at the beginning of each line (i.e., after a CR
and/or LF) or page (i.e., after an FF).

If within a textual value a character set other than the one specified
in value 1 of the Attribute Specific Character Set (0008,0005), or the
Default Character Repertoire if value 1 is missing, has been invoked,
the character set specified in the value 1, or the Default Character
Repertoire if value 1 is missing, shall be active in the following
instances:

-  before the end of line (i.e., before the CR and/or LF)

-  before the end of a page (i.e., before the FF)

-  before any other Control Character other than ESC (e.g., before any
   TAB)

-  before the end of a Data Element value (e.g., before the 05/12
   character code that separates multiple textual Data Element Values -
   05/12 corresponds to "\" (BACKSLASH) in the case of default
   repertoire IR-6 or "¥" (YEN SIGN) in the case of IR-14).

-  before the "^" and "=" delimiters separating name components and name
   component groups in Data Elements with a VR of PN.

If within a textual value a character set other than the one specified
in value 1 of the Attribute Specific Character Set (0008,0005), or the
Default Character Repertoire if value 1 is missing, is used, the Escape
Sequence of this character set must be inserted explicitly in the
following instances:

-  before the first use of the character set in the line

-  before the first use of the character set in the page

-  before the first use of the character set in the Data Element value

-  before the first use of the character set in the name component and
   name component group in Data Element with a VR of PN

.. note::

   These requirements allow an application to skip lines, values, or
   components in a textual data element and start the new line with a
   defined character set without the need to track the character set
   changes in the text skipped. A similar restriction appears in the
   RFCs describing the use of multi-byte character sets over the
   Internet. An Escape Sequence switching to the value 1 or default
   Specific Character Set is not needed within a line, value, or
   component if no Code Extensions are present. Nor is a switch needed
   to the value 1 or default Specific Character Set if this character
   set has only the G0 Code Element defined, and the G0 Code Element is
   still active.

.. _sect_6.1.2.5.4:

Levels of Implementation and Initial Designation
''''''''''''''''''''''''''''''''''''''''''''''''

a. Attribute Specific Character Set (0008,0005) not present:

   -  7-bit code

   -  Implementation level: ISO 2022 Level 1 - Elementary 7-bit code
      (code-level identifier 1)

   -  Initial designation: ISO-IR 6 (ASCII) as G0.

   -  Code Extension shall not be used.

b. Attribute Specific Character Set (0008,0005) single value other than
   "ISO_IR 192", "GB18030" or "GBK":

   -  8-bit code

   -  Implementation level: ISO 2022 Level 1 - Elementary 8-bit code
      (code-level identifier 11)

   -  Initial designation: One of the ISO 8859-defined character sets,
      or the 8-bit code table of JIS X 0201 specified by value 1 of the
      Attribute Specific Character Set (0008,0005), as G0 and G1.

   -  Code Extension shall not be used.

c. Attribute Specific Character Set (0008,0005) multi-valued:

   -  8-bit code

   -  Implementation level: ISO 2022 Level 4 - Redesignation of Graphic
      Character Sets within a Code (code-level identifier 14)

   -  Initial designation: One of the ISO 8859-defined character sets,
      or the 8-bit code table of JIS X 0201 specified by value 1 of the
      Attribute Specific Character Set (0008,0005), as G0 and G1. If
      value 1 of the Attribute Specific Character Set (0008,0005) is
      empty, ISO-IR 6 (ASCII) is assumed as G0, and G1 is undefined.

   -  All character sets specified in the various values of Attribute
      Specific Character Set (0008,0005), including value 1, may
      participate in Code Extension.

d. Attribute Specific Character Set (0008,0005) single value "ISO_IR
   192", "GB18030" or "GBK":

   -  variable length code

   -  Implementation level: not specified (not compatible with ISO 2022)

   -  Initial designation: as specified by value 1 of the Attribute
      Specific Character Set (0008,0005)

   -  Code Extension shall not be used.

.. _sect_6.1.3:

Control Characters
~~~~~~~~~~~~~~~~~~

Textual data that is interchanged may require some formatting
information. Control Characters are used to indicate formatting, but
their use in DICOM is kept to a minimum since some machines may handle
them inappropriately. ISO 646:1990 and ISO 6429:1990 define Control
Characters. As shown in `table_title <#table_6.1-1>`__ below, only a
subset of five Control Characters from the C0 set shall be used in DICOM
for the encoding of Control Characters in text strings.

.. table:: DICOM Control Characters and Their Encoding

   =========== =============== ===============
   **Acronym** **Name**        **Coded Value**
   =========== =============== ===============
   LF          Line Feed       00/10
   FF          Form Feed       00/12
   CR          Carriage Return 00/13
   ESC         Escape          01/11
   TAB         Horizontal Tab  00/09
   =========== =============== ===============

The ESC character shall be used only for ISO 2022 character set control
sequences, in accordance with `Usage of Code
Extension <#sect_6.1.2.5>`__.

In text strings (value representation ST, LT, or UT) a new line shall be
represented as CR LF.

.. note::

   1. Some machines (such as UNIX based machines) may interpret LF
      (00/10) as a new line. In such cases, it is expected that the
      DICOM format is converted to the correct internal representation
      for that machine.

   2. In previous editions of the Standard (see PS3.5 2015a), the TAB
      character was not listed as a Control Character.

.. _sect_6.2:

Value Representation (VR)
-------------------------

The Value Representation of a Data Element describes the data type and
format of that Data Element's Value(s). lists the VR of each Data
Element by Data Element Tag.

Values with VRs constructed of character strings, except in the case of
the VR UI, shall be padded with SPACE characters (20H, in the Default
Character Repertoire) when necessary to achieve even length. Values with
a VR of UI shall be padded with a single trailing NULL (00H) character
when necessary to achieve even length. Values with a VR of OB shall be
padded with a single trailing NULL byte value (00H) when necessary to
achieve even length.

All new VRs defined in future versions of DICOM shall be of the same
Data Element Structure as defined in `Data Element Structure with
Explicit VR <#sect_7.1.2>`__ with reserved bytes after the VR and a
32-bit unsigned integer VL (i.e., following the format for VRs such as
OB or UT), and may or may not permit undefined length.

.. note::

   1. Since all new VRs will be defined as specified in `Data Element
      Structure with Explicit VR <#sect_7.1.2>`__, an implementation may
      choose to ignore VRs not recognized by applying the rules stated
      in `Data Element Structure with Explicit VR <#sect_7.1.2>`__.

   2. When converting a Data Set from an Explicit VR Transfer Syntax to
      a different Transfer Syntax, an implementation may copy Data
      Elements with unrecognized VRs in the following manner:

      -  If the endianness of the Transfer Syntaxes is the same, the
         Value of the Data Element may be copied unchanged and if the
         target Transfer Syntax is Explicit VR, the VR bytes copied
         unchanged. In practice this only applies to Little Endian
         Transfer Syntaxes, since there was only one Big Endian Transfer
         Syntax defined.

      -  If the source Transfer Syntax is Little Endian and the target
         Transfer Syntax is the (retired) Big Endian Explicit VR
         Transfer Syntax, then the Value of the Data Element may be
         copied unchanged and the VR changed to UN, since being
         unrecognized, whether or not byte swapping is required is
         unknown. If the VR were copied unchanged, the byte order of the
         value might or might not be incorrect.

      -  If the source Transfer Syntax is the (retired) Big Endian
         Explicit VR Transfer Syntax, then the Data Element cannot be
         copied, because whether or not byte swapping is required is
         unknown, and there is no equivalent of the UN VR to use when
         the value is big endian rather than little endian.

      The issues of whether or not the element may be copied, and what
      VR to use if copying, do not arise when converting a Data Set from
      Implicit VR Little Endian Transfer Syntax, since the VR would not
      be present to be unrecognized, and if the data element VR is not
      known from a data dictionary, then UN would be used.

An individual Value, including padding, shall not exceed the Length of
Value, except in the case of the last Value of a multi-valued field as
specified in `Value Multiplicity (VM) and Delimitation <#sect_6.4>`__.

.. note::
   :name: note_6.1-2-1

   The lengths of Value Representations for which the Character
   Repertoire can be extended or replaced are expressly specified in
   characters rather than bytes in `table_title <#table_6.2-1>`__. This
   is because the mapping from a character to the number of bytes used
   for that character's encoding may be dependent on the character set
   used.

Escape Sequences used for Code Extension shall not be included in the
count of characters.

.. table:: DICOM Value Representations

   +----------------+----------------+----------------+----------------+
   | **VR Name**    | **Definition** | **Character    | **Length of    |
   |                |                | Repertoire**   | Value**        |
   +================+================+================+================+
   | AE             | A string of    | Default        | 16 bytes       |
   |                | characters     | Character      | maximum        |
   | Application    | that           | Repertoire     |                |
   | Entity         | identifies an  | excluding      |                |
   |                | Application    | character code |                |
   |                | Entity with    | 5CH (the       |                |
   |                | leading and    | BACKSLASH "\"  |                |
   |                | trailing       | in ISO-IR 6),  |                |
   |                | spaces (20H)   | and all        |                |
   |                | being          | control        |                |
   |                | no             | characters.    |                |
   |                | n-significant. |                |                |
   |                | A value        |                |                |
   |                | consisting     |                |                |
   |                | solely of      |                |                |
   |                | spaces shall   |                |                |
   |                | not be used.   |                |                |
   +----------------+----------------+----------------+----------------+
   | AS             | A string of    | "0"-"9", "D",  | 4 bytes fixed  |
   |                | characters     | "W", "M", "Y"  |                |
   | Age String     | with one of    | of Default     |                |
   |                | the following  | Character      |                |
   |                | formats --     | Repertoire     |                |
   |                | nnnD, nnnW,    |                |                |
   |                | nnnM, nnnY;    |                |                |
   |                | where nnn      |                |                |
   |                | shall contain  |                |                |
   |                | the number of  |                |                |
   |                | days for D,    |                |                |
   |                | weeks for W,   |                |                |
   |                | months for M,  |                |                |
   |                | or years for   |                |                |
   |                | Y.             |                |                |
   |                |                |                |                |
   |                | Example:       |                |                |
   |                | "018M" would   |                |                |
   |                | represent an   |                |                |
   |                | age of 18      |                |                |
   |                | months.        |                |                |
   +----------------+----------------+----------------+----------------+
   | AT             | Ordered pair   | not applicable | 4 bytes fixed  |
   |                | of 16-bit      |                |                |
   | Attribute Tag  | unsigned       |                |                |
   |                | integers that  |                |                |
   |                | is the value   |                |                |
   |                | of a Data      |                |                |
   |                | Element Tag.   |                |                |
   |                |                |                |                |
   |                | Example: A     |                |                |
   |                | Data Element   |                |                |
   |                | Tag of         |                |                |
   |                | (0018,00FF)    |                |                |
   |                | would be       |                |                |
   |                | encoded as a   |                |                |
   |                | series of 4    |                |                |
   |                | bytes in a     |                |                |
   |                | Little-Endian  |                |                |
   |                | Transfer       |                |                |
   |                | Syntax as      |                |                |
   |                | 18             |                |                |
   |                | H,00H,FFH,00H. |                |                |
   |                |                |                |                |
   |                | .. note::      |                |                |
   |                |                |                |                |
   |                |    The         |                |                |
   |                |    encoding of |                |                |
   |                |    an AT value |                |                |
   |                |    is exactly  |                |                |
   |                |    the same as |                |                |
   |                |    the         |                |                |
   |                |    encoding of |                |                |
   |                |    a Data      |                |                |
   |                |    Element Tag |                |                |
   |                |    as defined  |                |                |
   |                |    in `The     |                |                |
   |                |    Data        |                |                |
   |                |    Set <#      |                |                |
   |                | chapter_7>`__. |                |                |
   +----------------+----------------+----------------+----------------+
   | CS             | A string of    | Uppercase      | 16 bytes       |
   |                | characters     | characters,    | maximum        |
   | Code String    | identifying a  | "0"-"9", the   |                |
   |                | controlled     | SPACE          |                |
   |                | concept.       | character, and |                |
   |                | Leading or     | underscore     |                |
   |                | trailing       | "_", of the    |                |
   |                | spaces (20H)   | Default        |                |
   |                | are not        | Character      |                |
   |                | significant.   | Repertoire     |                |
   +----------------+----------------+----------------+----------------+
   | DA             | A string of    | "0"-"9" of     | 8 bytes fixed  |
   |                | characters of  | Default        |                |
   | Date           | the format     | Character      | In the context |
   |                | YYYYMMDD;      | Repertoire     | of a Query     |
   |                | where YYYY     |                | with range     |
   |                | shall contain  | In the context | matching (see  |
   |                | year, MM shall | of a Query     | ), the length  |
   |                | contain the    | with range     | is 18 bytes    |
   |                | month, and DD  | matching (see  | maximum.       |
   |                | shall contain  | ), the         |                |
   |                | the day,       | character "-"  |                |
   |                | interpreted as | is allowed,    |                |
   |                | a date of the  | and a trailing |                |
   |                | Gregorian      | SPACE          |                |
   |                | calendar       | character is   |                |
   |                | system.        | allowed for    |                |
   |                |                | padding.       |                |
   |                | Example:       |                |                |
   |                |                |                |                |
   |                | -  "19930822"  |                |                |
   |                |    would       |                |                |
   |                |    represent   |                |                |
   |                |    August 22,  |                |                |
   |                |    1993.       |                |                |
   |                |                |                |                |
   |                | .. note::      |                |                |
   |                |                |                |                |
   |                |    1. The      |                |                |
   |                |       ACR-NEMA |                |                |
   |                |       Standard |                |                |
   |                |       300      |                |                |
   |                |                |                |                |
   |                |   (predecessor |                |                |
   |                |       to       |                |                |
   |                |       DICOM)   |                |                |
   |                |                |                |                |
   |                |      supported |                |                |
   |                |       a string |                |                |
   |                |       of       |                |                |
   |                |                |                |                |
   |                |     characters |                |                |
   |                |       of the   |                |                |
   |                |       format   |                |                |
   |                |                |                |                |
   |                |     YYYY.MM.DD |                |                |
   |                |       for this |                |                |
   |                |       VR. Use  |                |                |
   |                |       of this  |                |                |
   |                |       format   |                |                |
   |                |       is not   |                |                |
   |                |                |                |                |
   |                |     compliant. |                |                |
   |                |                |                |                |
   |                |    2. See also |                |                |
   |                |       DT VR in |                |                |
   |                |       this     |                |                |
   |                |       table.   |                |                |
   |                |                |                |                |
   |                |    3. Dates    |                |                |
   |                |       before   |                |                |
   |                |       year     |                |                |
   |                |       1582,    |                |                |
   |                |       e.g.,    |                |                |
   |                |       used for |                |                |
   |                |       dating   |                |                |
   |                |                |                |                |
   |                |     historical |                |                |
   |                |       or       |                |                |
   |                |                |                |                |
   |                |  archeological |                |                |
   |                |       items,   |                |                |
   |                |       are      |                |                |
   |                |                |                |                |
   |                |    interpreted |                |                |
   |                |       as       |                |                |
   |                |                |                |                |
   |                |      proleptic |                |                |
   |                |                |                |                |
   |                |      Gregorian |                |                |
   |                |       calendar |                |                |
   |                |       dates,   |                |                |
   |                |       unless   |                |                |
   |                |                |                |                |
   |                |      otherwise |                |                |
   |                |                |                |                |
   |                |     specified. |                |                |
   +----------------+----------------+----------------+----------------+
   | DS             | A string of    | "0"-"9", "+",  | 16 bytes       |
   |                | characters     | "-", "E", "e", | maximum        |
   | Decimal String | representing   | "." and the    |                |
   |                | either a fixed | SPACE          |                |
   |                | point number   | character of   |                |
   |                | or a floating  | Default        |                |
   |                | point number.  | Character      |                |
   |                | A fixed point  | Repertoire     |                |
   |                | number shall   |                |                |
   |                | contain only   |                |                |
   |                | the characters |                |                |
   |                | 0-9 with an    |                |                |
   |                | optional       |                |                |
   |                | leading "+" or |                |                |
   |                | "-" and an     |                |                |
   |                | optional "."   |                |                |
   |                | to mark the    |                |                |
   |                | decimal point. |                |                |
   |                | A floating     |                |                |
   |                | point number   |                |                |
   |                | shall be       |                |                |
   |                | conveyed as    |                |                |
   |                | defined in     |                |                |
   |                | ANSI X3.9,     |                |                |
   |                | with an "E" or |                |                |
   |                | "e" to         |                |                |
   |                | indicate the   |                |                |
   |                | start of the   |                |                |
   |                | exponent.      |                |                |
   |                | Decimal        |                |                |
   |                | Strings may be |                |                |
   |                | padded with    |                |                |
   |                | leading or     |                |                |
   |                | trailing       |                |                |
   |                | spaces.        |                |                |
   |                | Embedded       |                |                |
   |                | spaces are not |                |                |
   |                | allowed.       |                |                |
   |                |                |                |                |
   |                | .. note::      |                |                |
   |                |                |                |                |
   |                |    Data        |                |                |
   |                |    Elements    |                |                |
   |                |    with        |                |                |
   |                |    multiple    |                |                |
   |                |    values      |                |                |
   |                |    using this  |                |                |
   |                |    VR may not  |                |                |
   |                |    be properly |                |                |
   |                |    encoded if  |                |                |
   |                |    Explicit-VR |                |                |
   |                |    Transfer    |                |                |
   |                |    Syntax is   |                |                |
   |                |    used and    |                |                |
   |                |    the VL of   |                |                |
   |                |    this        |                |                |
   |                |    attribute   |                |                |
   |                |    exceeds     |                |                |
   |                |    65534       |                |                |
   |                |    bytes.      |                |                |
   +----------------+----------------+----------------+----------------+
   | DT             | A concatenated | "0"-"9", "+",  | 26 bytes       |
   |                | date-time      | "-", "." and   | maximum        |
   | Date Time      | character      | the SPACE      |                |
   |                | string in the  | character of   | In the context |
   |                | format:        | Default        | of a Query     |
   |                |                | Character      | with range     |
   |                | YYYYMMDDHHMM   | Repertoire     | matching (see  |
   |                | SS.FFFFFF&ZZXX |                | ), the length  |
   |                |                |                | is 54 bytes    |
   |                | The components |                | maximum.       |
   |                | of this        |                |                |
   |                | string, from   |                |                |
   |                | left to right, |                |                |
   |                | are YYYY =     |                |                |
   |                | Year, MM =     |                |                |
   |                | Month, DD =    |                |                |
   |                | Day, HH = Hour |                |                |
   |                | (range "00" -  |                |                |
   |                | "23"), MM =    |                |                |
   |                | Minute (range  |                |                |
   |                | "00" - "59"),  |                |                |
   |                | SS = Second    |                |                |
   |                | (range "00" -  |                |                |
   |                | "60").         |                |                |
   |                |                |                |                |
   |                | FFFFFF =       |                |                |
   |                | Fractional     |                |                |
   |                | Second         |                |                |
   |                | contains a     |                |                |
   |                | fractional     |                |                |
   |                | part of a      |                |                |
   |                | second as      |                |                |
   |                | small as 1     |                |                |
   |                | millionth of a |                |                |
   |                | second (range  |                |                |
   |                | "000000" -     |                |                |
   |                | "999999").     |                |                |
   |                |                |                |                |
   |                | &ZZXX is an    |                |                |
   |                | optional       |                |                |
   |                | suffix for     |                |                |
   |                | offset from    |                |                |
   |                | Coordinated    |                |                |
   |                | Universal Time |                |                |
   |                | (UTC), where & |                |                |
   |                | = "+" or "-",  |                |                |
   |                | and ZZ = Hours |                |                |
   |                | and XX =       |                |                |
   |                | Minutes of     |                |                |
   |                | offset.        |                |                |
   |                |                |                |                |
   |                | The year,      |                |                |
   |                | month, and day |                |                |
   |                | shall be       |                |                |
   |                | interpreted as |                |                |
   |                | a date of the  |                |                |
   |                | Gregorian      |                |                |
   |                | calendar       |                |                |
   |                | system.        |                |                |
   |                |                |                |                |
   |                | A 24-hour      |                |                |
   |                | clock is used. |                |                |
   |                | Midnight shall |                |                |
   |                | be represented |                |                |
   |                | by only "0000" |                |                |
   |                | since "2400"   |                |                |
   |                | would violate  |                |                |
   |                | the hour       |                |                |
   |                | range.         |                |                |
   |                |                |                |                |
   |                | The Fractional |                |                |
   |                | Second         |                |                |
   |                | component, if  |                |                |
   |                | present, shall |                |                |
   |                | contain 1 to 6 |                |                |
   |                | digits. If     |                |                |
   |                | Fractional     |                |                |
   |                | Second is      |                |                |
   |                | unspecified    |                |                |
   |                | the preceding  |                |                |
   |                | "." shall not  |                |                |
   |                | be included.   |                |                |
   |                | The offset     |                |                |
   |                | suffix, if     |                |                |
   |                | present, shall |                |                |
   |                | contain 4      |                |                |
   |                | digits. The    |                |                |
   |                | string may be  |                |                |
   |                | padded with    |                |                |
   |                | trailing SPACE |                |                |
   |                | characters.    |                |                |
   |                | Leading and    |                |                |
   |                | embedded       |                |                |
   |                | spaces are not |                |                |
   |                | allowed.       |                |                |
   |                |                |                |                |
   |                | A component    |                |                |
   |                | that is        |                |                |
   |                | omitted from   |                |                |
   |                | the string is  |                |                |
   |                | termed a null  |                |                |
   |                | component.     |                |                |
   |                | Trailing null  |                |                |
   |                | components of  |                |                |
   |                | Date Time      |                |                |
   |                | indicate that  |                |                |
   |                | the value is   |                |                |
   |                | not precise to |                |                |
   |                | the precision  |                |                |
   |                | of those       |                |                |
   |                | components.    |                |                |
   |                | The YYYY       |                |                |
   |                | component      |                |                |
   |                | shall not be   |                |                |
   |                | null.          |                |                |
   |                | Non-trailing   |                |                |
   |                | null           |                |                |
   |                | components are |                |                |
   |                | prohibited.    |                |                |
   |                | The optional   |                |                |
   |                | suffix is not  |                |                |
   |                | considered as  |                |                |
   |                | a component.   |                |                |
   |                |                |                |                |
   |                | A Date Time    |                |                |
   |                | value without  |                |                |
   |                | the optional   |                |                |
   |                | suffix is      |                |                |
   |                | interpreted to |                |                |
   |                | be in the      |                |                |
   |                | local time     |                |                |
   |                | zone of the    |                |                |
   |                | application    |                |                |
   |                | creating the   |                |                |
   |                | Data Element,  |                |                |
   |                | unless         |                |                |
   |                | explicitly     |                |                |
   |                | specified by   |                |                |
   |                | the Timezone   |                |                |
   |                | Offset From    |                |                |
   |                | UTC            |                |                |
   |                | (0008,0201).   |                |                |
   |                |                |                |                |
   |                | UTC offsets    |                |                |
   |                | are calculated |                |                |
   |                | as "local time |                |                |
   |                | minus UTC".    |                |                |
   |                | The offset for |                |                |
   |                | a Date Time    |                |                |
   |                | value in UTC   |                |                |
   |                | shall be       |                |                |
   |                | +0000.         |                |                |
   |                |                |                |                |
   |                | .. note::      |                |                |
   |                |                |                |                |
   |                |    1. The      |                |                |
   |                |       range of |                |                |
   |                |       the      |                |                |
   |                |       offset   |                |                |
   |                |       is -1200 |                |                |
   |                |       to       |                |                |
   |                |       +1400.   |                |                |
   |                |       The      |                |                |
   |                |       offset   |                |                |
   |                |       for      |                |                |
   |                |       United   |                |                |
   |                |       States   |                |                |
   |                |       Eastern  |                |                |
   |                |       Standard |                |                |
   |                |       Time is  |                |                |
   |                |       -0500.   |                |                |
   |                |       The      |                |                |
   |                |       offset   |                |                |
   |                |       for      |                |                |
   |                |       Japan    |                |                |
   |                |       Standard |                |                |
   |                |       Time is  |                |                |
   |                |       +0900.   |                |                |
   |                |                |                |                |
   |                |    2. The RFC  |                |                |
   |                |       2822 use |                |                |
   |                |       of -0000 |                |                |
   |                |       as an    |                |                |
   |                |       offset   |                |                |
   |                |       to       |                |                |
   |                |       indicate |                |                |
   |                |       local    |                |                |
   |                |       time is  |                |                |
   |                |       not      |                |                |
   |                |       allowed. |                |                |
   |                |                |                |                |
   |                |    3. A Date   |                |                |
   |                |       Time     |                |                |
   |                |       value of |                |                |
   |                |       195308   |                |                |
   |                |       means    |                |                |
   |                |       August   |                |                |
   |                |       1953,    |                |                |
   |                |       not      |                |                |
   |                |       specific |                |                |
   |                |       to       |                |                |
   |                |                |                |                |
   |                |     particular |                |                |
   |                |       day. A   |                |                |
   |                |       Date     |                |                |
   |                |       Time     |                |                |
   |                |       value of |                |                |
   |                |       19       |                |                |
   |                | 530827111300.0 |                |                |
   |                |       means    |                |                |
   |                |       August   |                |                |
   |                |       27,      |                |                |
   |                |       1953,    |                |                |
   |                |       11;13    |                |                |
   |                |       a.m.     |                |                |
   |                |       accurate |                |                |
   |                |       to       |                |                |
   |                |       1/10th   |                |                |
   |                |       second.  |                |                |
   |                |                |                |                |
   |                |    4. The      |                |                |
   |                |       Second   |                |                |
   |                |                |                |                |
   |                |      component |                |                |
   |                |       may have |                |                |
   |                |       a value  |                |                |
   |                |       of 60    |                |                |
   |                |       only for |                |                |
   |                |       a leap   |                |                |
   |                |       second.  |                |                |
   |                |                |                |                |
   |                |    5. The      |                |                |
   |                |       offset   |                |                |
   |                |       may be   |                |                |
   |                |       included |                |                |
   |                |                |                |                |
   |                |     regardless |                |                |
   |                |       of null  |                |                |
   |                |                |                |                |
   |                |    components; |                |                |
   |                |       e.g.,    |                |                |
   |                |                |                |                |
   |                |      2007-0500 |                |                |
   |                |       is a     |                |                |
   |                |       legal    |                |                |
   |                |       value.   |                |                |
   +----------------+----------------+----------------+----------------+
   | FL             | Single         | not applicable | 4 bytes fixed  |
   |                | precision      |                |                |
   | Floating Point | binary         |                |                |
   | Single         | floating point |                |                |
   |                | number         |                |                |
   |                | represented in |                |                |
   |                | IEEE 754:1985  |                |                |
   |                | 32-bit         |                |                |
   |                | Floating Point |                |                |
   |                | Number Format. |                |                |
   +----------------+----------------+----------------+----------------+
   | FD             | Double         | not applicable | 8 bytes fixed  |
   |                | precision      |                |                |
   | Floating Point | binary         |                |                |
   | Double         | floating point |                |                |
   |                | number         |                |                |
   |                | represented in |                |                |
   |                | IEEE 754:1985  |                |                |
   |                | 64-bit         |                |                |
   |                | Floating Point |                |                |
   |                | Number Format. |                |                |
   +----------------+----------------+----------------+----------------+
   | IS             | A string of    | "0"-"9", "+",  | 12 bytes       |
   |                | characters     | "-" and the    | maximum        |
   | Integer String | representing   | SPACE          |                |
   |                | an Integer in  | character of   |                |
   |                | base-10        | Default        |                |
   |                | (decimal),     | Character      |                |
   |                | shall contain  | Repertoire     |                |
   |                | only the       |                |                |
   |                | characters 0 - |                |                |
   |                | 9, with an     |                |                |
   |                | optional       |                |                |
   |                | leading "+" or |                |                |
   |                | "-". It may be |                |                |
   |                | padded with    |                |                |
   |                | leading and/or |                |                |
   |                | trailing       |                |                |
   |                | spaces.        |                |                |
   |                | Embedded       |                |                |
   |                | spaces are not |                |                |
   |                | allowed.       |                |                |
   |                |                |                |                |
   |                | The integer,   |                |                |
   |                | n, represented |                |                |
   |                | shall be in    |                |                |
   |                | the range:     |                |                |
   |                |                |                |                |
   |                | -2\            |                |                |
   |                |  :sup:`31`\ <= |                |                |
   |                | n <=           |                |                |
   |                | (2\            |                |                |
   |                |  :sup:`31`-1). |                |                |
   +----------------+----------------+----------------+----------------+
   | LO             | A character    | Default        | 64 chars       |
   |                | string that    | Character      | maximum (see   |
   | Long String    | may be padded  | Repertoire     | `no            |
   |                | with leading   | and/or as      | te_title <#not |
   |                | and/or         | defined by     | e_6.1-2-1>`__) |
   |                | trailing       | (0008,0005)    |                |
   |                | spaces. The    | excluding      |                |
   |                | character code | character code |                |
   |                | 5CH (the       | 5CH (the       |                |
   |                | BACKSLASH "\"  | BACKSLASH "\"  |                |
   |                | in ISO-IR 6)   | in ISO-IR 6),  |                |
   |                | shall not be   | and all        |                |
   |                | present, as it | Control        |                |
   |                | is used as the | Characters     |                |
   |                | delimiter      | except ESC     |                |
   |                | between values | when used for  |                |
   |                | in             | ISO 2022       |                |
   |                | multi-valued   | escape         |                |
   |                | data elements. | sequences.     |                |
   |                | The string     |                |                |
   |                | shall not have |                |                |
   |                | Control        |                |                |
   |                | Characters     |                |                |
   |                | except for     |                |                |
   |                | ESC.           |                |                |
   +----------------+----------------+----------------+----------------+
   | LT             | A character    | Default        | 10240 chars    |
   |                | string that    | Character      | maximum (see   |
   | Long Text      | may contain    | Repertoire     | `no            |
   |                | one or more    | and/or as      | te_title <#not |
   |                | paragraphs. It | defined by     | e_6.1-2-1>`__) |
   |                | may contain    | (0008,0005)    |                |
   |                | the Graphic    | excluding      |                |
   |                | Character set  | Control        |                |
   |                | and the        | Characters     |                |
   |                | Control        | except TAB,    |                |
   |                | Characters,    | LF, FF, CR     |                |
   |                | CR, LF, FF,    | (and ESC when  |                |
   |                | and ESC. It    | used for ISO   |                |
   |                | may be padded  | 2022 escape    |                |
   |                | with trailing  | sequences).    |                |
   |                | spaces, which  |                |                |
   |                | may be         |                |                |
   |                | ignored, but   |                |                |
   |                | leading spaces |                |                |
   |                | are considered |                |                |
   |                | to be          |                |                |
   |                | significant.   |                |                |
   |                | Data Elements  |                |                |
   |                | with this VR   |                |                |
   |                | shall not be   |                |                |
   |                | multi-valued   |                |                |
   |                | and therefore  |                |                |
   |                | character code |                |                |
   |                | 5CH (the       |                |                |
   |                | BACKSLASH "\"  |                |                |
   |                | in ISO-IR 6)   |                |                |
   |                | may be used.   |                |                |
   +----------------+----------------+----------------+----------------+
   | OB             | An             | not applicable | see Transfer   |
   |                | octet-stream   |                | Syntax         |
   | Other Byte     | where the      |                | definition     |
   |                | encoding of    |                |                |
   |                | the contents   |                |                |
   |                | is specified   |                |                |
   |                | by the         |                |                |
   |                | negotiated     |                |                |
   |                | Transfer       |                |                |
   |                | Syntax. OB is  |                |                |
   |                | a VR that is   |                |                |
   |                | insensitive to |                |                |
   |                | byte ordering  |                |                |
   |                | (see `Little   |                |                |
   |                | Endian Byte    |                |                |
   |                | Ordering <#    |                |                |
   |                | sect_7.3>`__). |                |                |
   |                | The            |                |                |
   |                | octet-stream   |                |                |
   |                | shall be       |                |                |
   |                | padded with a  |                |                |
   |                | single         |                |                |
   |                | trailing NULL  |                |                |
   |                | byte value     |                |                |
   |                | (00H) when     |                |                |
   |                | necessary to   |                |                |
   |                | achieve even   |                |                |
   |                | length.        |                |                |
   +----------------+----------------+----------------+----------------+
   | OD             | A stream of    | not applicable | 2\ :sup:`32`-8 |
   |                | 64-bit IEEE    |                | bytes maximum  |
   | Other Double   | 754:1985       |                |                |
   |                | floating point |                |                |
   |                | words. OD is a |                |                |
   |                | VR that        |                |                |
   |                | requires byte  |                |                |
   |                | swapping       |                |                |
   |                | within each    |                |                |
   |                | 64-bit word    |                |                |
   |                | when changing  |                |                |
   |                | byte ordering  |                |                |
   |                | (see `Little   |                |                |
   |                | Endian Byte    |                |                |
   |                | Ordering <#    |                |                |
   |                | sect_7.3>`__). |                |                |
   +----------------+----------------+----------------+----------------+
   | OF             | A stream of    | not applicable | 2\ :sup:`32`-4 |
   |                | 32-bit IEEE    |                | bytes maximum  |
   | Other Float    | 754:1985       |                |                |
   |                | floating point |                |                |
   |                | words. OF is a |                |                |
   |                | VR that        |                |                |
   |                | requires byte  |                |                |
   |                | swapping       |                |                |
   |                | within each    |                |                |
   |                | 32-bit word    |                |                |
   |                | when changing  |                |                |
   |                | byte ordering  |                |                |
   |                | (see `Little   |                |                |
   |                | Endian Byte    |                |                |
   |                | Ordering <#    |                |                |
   |                | sect_7.3>`__). |                |                |
   +----------------+----------------+----------------+----------------+
   | OL             | A stream of    | not applicable | see Transfer   |
   |                | 32-bit words   |                | Syntax         |
   | Other Long     | where the      |                | definition     |
   |                | encoding of    |                |                |
   |                | the contents   |                |                |
   |                | is specified   |                |                |
   |                | by the         |                |                |
   |                | negotiated     |                |                |
   |                | Transfer       |                |                |
   |                | Syntax. OL is  |                |                |
   |                | a VR that      |                |                |
   |                | requires byte  |                |                |
   |                | swapping       |                |                |
   |                | within each    |                |                |
   |                | word when      |                |                |
   |                | changing byte  |                |                |
   |                | ordering (see  |                |                |
   |                | `Little Endian |                |                |
   |                | Byte           |                |                |
   |                | Ordering <#    |                |                |
   |                | sect_7.3>`__). |                |                |
   +----------------+----------------+----------------+----------------+
   | OV             | A stream of    | not applicable | see Transfer   |
   |                | 64-bit words   |                | Syntax         |
   | Other 64-bit   | where the      |                | definition     |
   | Very Long      | encoding of    |                |                |
   |                | the contents   |                |                |
   |                | is specified   |                |                |
   |                | by the         |                |                |
   |                | negotiated     |                |                |
   |                | Transfer       |                |                |
   |                | Syntax. OV is  |                |                |
   |                | a VR that      |                |                |
   |                | requires byte  |                |                |
   |                | swapping       |                |                |
   |                | within each    |                |                |
   |                | word when      |                |                |
   |                | changing byte  |                |                |
   |                | ordering (see  |                |                |
   |                | `Little Endian |                |                |
   |                | Byte           |                |                |
   |                | Ordering <#    |                |                |
   |                | sect_7.3>`__). |                |                |
   +----------------+----------------+----------------+----------------+
   | OW             | A stream of    | not applicable | see Transfer   |
   |                | 16-bit words   |                | Syntax         |
   | Other Word     | where the      |                | definition     |
   |                | encoding of    |                |                |
   |                | the contents   |                |                |
   |                | is specified   |                |                |
   |                | by the         |                |                |
   |                | negotiated     |                |                |
   |                | Transfer       |                |                |
   |                | Syntax. OW is  |                |                |
   |                | a VR that      |                |                |
   |                | requires byte  |                |                |
   |                | swapping       |                |                |
   |                | within each    |                |                |
   |                | word when      |                |                |
   |                | changing byte  |                |                |
   |                | ordering (see  |                |                |
   |                | `Little Endian |                |                |
   |                | Byte           |                |                |
   |                | Ordering <#    |                |                |
   |                | sect_7.3>`__). |                |                |
   +----------------+----------------+----------------+----------------+
   | PN             | A character    | Default        | 64 chars       |
   |                | string encoded | Character      | maximum per    |
   | Person Name    | using a 5      | Repertoire     | component      |
   |                | component      | and/or as      | group          |
   |                | convention.    | defined by     |                |
   |                | The character  | (0008,0005)    | (see           |
   |                | code 5CH (the  | excluding      | `no            |
   |                | BACKSLASH "\"  | character code | te_title <#not |
   |                | in ISO-IR 6)   | 5CH (the       | e_6.1-2-1>`__) |
   |                | shall not be   | BACKSLASH "\"  |                |
   |                | present, as it | in ISO-IR 6)   |                |
   |                | is used as the | and all        |                |
   |                | delimiter      | Control        |                |
   |                | between values | Characters     |                |
   |                | in             | except ESC     |                |
   |                | multi-valued   | when used for  |                |
   |                | data elements. | ISO 2022       |                |
   |                | The string may | escape         |                |
   |                | be padded with | sequences.     |                |
   |                | trailing       |                |                |
   |                | spaces. For    |                |                |
   |                | human use, the |                |                |
   |                | five           |                |                |
   |                | components in  |                |                |
   |                | their order of |                |                |
   |                | occurrence     |                |                |
   |                | are: family    |                |                |
   |                | name complex,  |                |                |
   |                | given name     |                |                |
   |                | complex,       |                |                |
   |                | middle name,   |                |                |
   |                | name prefix,   |                |                |
   |                | name suffix.   |                |                |
   |                |                |                |                |
   |                | .. note::      |                |                |
   |                |                |                |                |
   |                |    HL7         |                |                |
   |                |    prohibits   |                |                |
   |                |    leading     |                |                |
   |                |    spaces      |                |                |
   |                |    within a    |                |                |
   |                |    component;  |                |                |
   |                |    DICOM       |                |                |
   |                |    allows      |                |                |
   |                |    leading and |                |                |
   |                |    trailing    |                |                |
   |                |    spaces and  |                |                |
   |                |    considers   |                |                |
   |                |    them        |                |                |
   |                |                |                |                |
   |                | insignificant. |                |                |
   |                |                |                |                |
   |                | Any of the     |                |                |
   |                | five           |                |                |
   |                | components may |                |                |
   |                | be an empty    |                |                |
   |                | string. The    |                |                |
   |                | component      |                |                |
   |                | delimiter      |                |                |
   |                | shall be the   |                |                |
   |                | caret "^"      |                |                |
   |                | character      |                |                |
   |                | (5EH). There   |                |                |
   |                | shall be no    |                |                |
   |                | more than four |                |                |
   |                | component      |                |                |
   |                | delimiters,    |                |                |
   |                | i.e., none     |                |                |
   |                | after the last |                |                |
   |                | component if   |                |                |
   |                | all components |                |                |
   |                | are present.   |                |                |
   |                | Delimiters are |                |                |
   |                | required for   |                |                |
   |                | interior null  |                |                |
   |                | components.    |                |                |
   |                | Trailing null  |                |                |
   |                | components and |                |                |
   |                | their          |                |                |
   |                | delimiters may |                |                |
   |                | be omitted.    |                |                |
   |                | Multiple       |                |                |
   |                | entries are    |                |                |
   |                | permitted in   |                |                |
   |                | each component |                |                |
   |                | and are        |                |                |
   |                | encoded as     |                |                |
   |                | natural text   |                |                |
   |                | strings, in    |                |                |
   |                | the format     |                |                |
   |                | preferred by   |                |                |
   |                | the named      |                |                |
   |                | person.        |                |                |
   |                |                |                |                |
   |                | For veterinary |                |                |
   |                | use, the first |                |                |
   |                | two of the     |                |                |
   |                | five           |                |                |
   |                | components in  |                |                |
   |                | their order of |                |                |
   |                | occurrence     |                |                |
   |                | are:           |                |                |
   |                | responsible    |                |                |
   |                | party family   |                |                |
   |                | name or        |                |                |
   |                | responsible    |                |                |
   |                | organization   |                |                |
   |                | name, patient  |                |                |
   |                | name. The      |                |                |
   |                | remaining      |                |                |
   |                | components are |                |                |
   |                | not used and   |                |                |
   |                | shall not be   |                |                |
   |                | present.       |                |                |
   |                |                |                |                |
   |                | This group of  |                |                |
   |                | five           |                |                |
   |                | components is  |                |                |
   |                | referred to as |                |                |
   |                | a Person Name  |                |                |
   |                | component      |                |                |
   |                | group.         |                |                |
   |                |                |                |                |
   |                | For the        |                |                |
   |                | purpose of     |                |                |
   |                | writing names  |                |                |
   |                | in ideographic |                |                |
   |                | characters and |                |                |
   |                | in phonetic    |                |                |
   |                | characters, up |                |                |
   |                | to 3 groups of |                |                |
   |                | components     |                |                |
   |                | (see           |                |                |
   |                | `Character     |                |                |
   |                | Sets and       |                |                |
   |                | Person Name    |                |                |
   |                | Value          |                |                |
   |                | Representation |                |                |
   |                | in the         |                |                |
   |                | Japanese       |                |                |
   |                | Language       |                |                |
   |                | (I             |                |                |
   |                | nformative) <# |                |                |
   |                | chapter_H>`__, |                |                |
   |                | `Character     |                |                |
   |                | Sets and       |                |                |
   |                | Person Name    |                |                |
   |                | Value          |                |                |
   |                | Representation |                |                |
   |                | in the Korean  |                |                |
   |                | Language       |                |                |
   |                | (              |                |                |
   |                | Informative) < |                |                |
   |                | #chapter_I>`__ |                |                |
   |                | and `Character |                |                |
   |                | Sets and       |                |                |
   |                | Person Name    |                |                |
   |                | Value          |                |                |
   |                | Representation |                |                |
   |                | using Unicode  |                |                |
   |                | UTF-8, GB18030 |                |                |
   |                | and GBK        |                |                |
   |                | (I             |                |                |
   |                | nformative) <# |                |                |
   |                | chapter_J>`__) |                |                |
   |                | may be used.   |                |                |
   |                | The delimiter  |                |                |
   |                | for component  |                |                |
   |                | groups shall   |                |                |
   |                | be the equals  |                |                |
   |                | character "="  |                |                |
   |                | (3DH). There   |                |                |
   |                | shall be no    |                |                |
   |                | more than two  |                |                |
   |                | component      |                |                |
   |                | group          |                |                |
   |                | delimiters,    |                |                |
   |                | i.e., none     |                |                |
   |                | after the last |                |                |
   |                | component      |                |                |
   |                | group if all   |                |                |
   |                | component      |                |                |
   |                | groups are     |                |                |
   |                | present. The   |                |                |
   |                | three          |                |                |
   |                | component      |                |                |
   |                | groups of      |                |                |
   |                | components in  |                |                |
   |                | their order of |                |                |
   |                | occurrence     |                |                |
   |                | are: an        |                |                |
   |                | alphabetic     |                |                |
   |                | r              |                |                |
   |                | epresentation, |                |                |
   |                | an ideographic |                |                |
   |                | r              |                |                |
   |                | epresentation, |                |                |
   |                | and a phonetic |                |                |
   |                | r              |                |                |
   |                | epresentation. |                |                |
   |                |                |                |                |
   |                | Any component  |                |                |
   |                | group may be   |                |                |
   |                | absent,        |                |                |
   |                | including the  |                |                |
   |                | first          |                |                |
   |                | component      |                |                |
   |                | group. In this |                |                |
   |                | case, the      |                |                |
   |                | person name    |                |                |
   |                | may start with |                |                |
   |                | one or more    |                |                |
   |                | "="            |                |                |
   |                | delimiters.    |                |                |
   |                | Delimiters are |                |                |
   |                | required for   |                |                |
   |                | interior null  |                |                |
   |                | component      |                |                |
   |                | groups.        |                |                |
   |                | Trailing null  |                |                |
   |                | component      |                |                |
   |                | groups and     |                |                |
   |                | their          |                |                |
   |                | delimiters may |                |                |
   |                | be omitted.    |                |                |
   |                |                |                |                |
   |                | Precise        |                |                |
   |                | semantics are  |                |                |
   |                | defined for    |                |                |
   |                | each component |                |                |
   |                | group. See     |                |                |
   |                | `Ideographic   |                |                |
   |                | and Phonetic   |                |                |
   |                | Characters in  |                |                |
   |                | Data Elements  |                |                |
   |                | with VR of     |                |                |
   |                | PN <#sec       |                |                |
   |                | t_6.2.1.2>`__. |                |                |
   |                |                |                |                |
   |                | For examples   |                |                |
   |                | and notes, see |                |                |
   |                | `Examples of   |                |                |
   |                | PN VR and      |                |                |
   |                | Notes <#sec    |                |                |
   |                | t_6.2.1.1>`__. |                |                |
   +----------------+----------------+----------------+----------------+
   | SH             | A character    | Default        | 16 chars       |
   |                | string that    | Character      | maximum (see   |
   | Short String   | may be padded  | Repertoire     | `no            |
   |                | with leading   | and/or as      | te_title <#not |
   |                | and/or         | defined by     | e_6.1-2-1>`__) |
   |                | trailing       | (0008,0005)    |                |
   |                | spaces. The    | excluding      |                |
   |                | character code | character code |                |
   |                | 05CH (the      | 5CH (the       |                |
   |                | BACKSLASH "\"  | BACKSLASH "\"  |                |
   |                | in ISO-IR 6)   | in ISO-IR 6)   |                |
   |                | shall not be   | and all        |                |
   |                | present, as it | Control        |                |
   |                | is used as the | Characters     |                |
   |                | delimiter      | except ESC     |                |
   |                | between values | when used for  |                |
   |                | for multiple   | ISO 2022       |                |
   |                | data elements. | escape         |                |
   |                | The string     | sequences.     |                |
   |                | shall not have |                |                |
   |                | Control        |                |                |
   |                | Characters     |                |                |
   |                | except ESC.    |                |                |
   +----------------+----------------+----------------+----------------+
   | SL             | Signed binary  | not applicable | 4 bytes fixed  |
   |                | integer 32     |                |                |
   | Signed Long    | bits long in   |                |                |
   |                | 2's complement |                |                |
   |                | form.          |                |                |
   |                |                |                |                |
   |                | Represents an  |                |                |
   |                | integer, n, in |                |                |
   |                | the range:     |                |                |
   |                |                |                |                |
   |                | -              |                |                |
   |                | 2\             |                |                |
   |                |  :sup:`31`\ <= |                |                |
   |                | n <=           |                |                |
   |                | 2              |                |                |
   |                | \ :sup:`31`-1. |                |                |
   +----------------+----------------+----------------+----------------+
   | SQ             | Value is a     | not applicable | not applicable |
   |                | Sequence of    | (see `Nesting  | (see `Nesting  |
   | Sequence of    | zero or more   | of Data        | of Data        |
   | Items          | Items, as      | Sets <         | Sets <         |
   |                | defined in     | #sect_7.5>`__) | #sect_7.5>`__) |
   |                | `Nesting of    |                |                |
   |                | Data           |                |                |
   |                | Sets <         |                |                |
   |                | #sect_7.5>`__. |                |                |
   +----------------+----------------+----------------+----------------+
   | SS             | Signed binary  | not applicable | 2 bytes fixed  |
   |                | integer 16     |                |                |
   | Signed Short   | bits long in   |                |                |
   |                | 2's complement |                |                |
   |                | form.          |                |                |
   |                | Represents an  |                |                |
   |                | integer n in   |                |                |
   |                | the range:     |                |                |
   |                |                |                |                |
   |                | -2\            |                |                |
   |                |  :sup:`15`\ <= |                |                |
   |                | n <=           |                |                |
   |                | 2              |                |                |
   |                | \ :sup:`15`-1. |                |                |
   +----------------+----------------+----------------+----------------+
   | ST             | A character    | Default        | 1024 chars     |
   |                | string that    | Character      | maximum (see   |
   | Short Text     | may contain    | Repertoire     | `no            |
   |                | one or more    | and/or as      | te_title <#not |
   |                | paragraphs. It | defined by     | e_6.1-2-1>`__) |
   |                | may contain    | (0008,0005)    |                |
   |                | the Graphic    | excluding      |                |
   |                | Character set  | Control        |                |
   |                | and the        | Characters     |                |
   |                | Control        | except TAB,    |                |
   |                | Characters,    | LF, FF, CR     |                |
   |                | CR, LF, FF,    | (and ESC when  |                |
   |                | and ESC. It    | used for ISO   |                |
   |                | may be padded  | 2022 escape    |                |
   |                | with trailing  | sequences).    |                |
   |                | spaces, which  |                |                |
   |                | may be         |                |                |
   |                | ignored, but   |                |                |
   |                | leading spaces |                |                |
   |                | are considered |                |                |
   |                | to be          |                |                |
   |                | significant.   |                |                |
   |                | Data Elements  |                |                |
   |                | with this VR   |                |                |
   |                | shall not be   |                |                |
   |                | multi-valued   |                |                |
   |                | and therefore  |                |                |
   |                | character code |                |                |
   |                | 5CH (the       |                |                |
   |                | BACKSLASH "\"  |                |                |
   |                | in ISO-IR 6)   |                |                |
   |                | may be used.   |                |                |
   +----------------+----------------+----------------+----------------+
   | SV             | Signed binary  | not applicable | 8 bytes fixed  |
   |                | integer 64     |                |                |
   | Signed 64-bit  | bits long.     |                |                |
   | Very Long      | Represents an  |                |                |
   |                | integer n in   |                |                |
   |                | the range:     |                |                |
   |                |                |                |                |
   |                | -              |                |                |
   |                | 2\             |                |                |
   |                |  :sup:`63`\ <= |                |                |
   |                | n <=           |                |                |
   |                | 2              |                |                |
   |                | \ :sup:`63`-1. |                |                |
   +----------------+----------------+----------------+----------------+
   | TM             | A string of    | "0"-"9", "."   | 14 bytes       |
   |                | characters of  | and the SPACE  | maximum        |
   | Time           | the format     | character of   |                |
   |                | HHMMSS.FFFFFF; | Default        | In the context |
   |                | where HH       | Character      | of a Query     |
   |                | contains hours | Repertoire     | with range     |
   |                | (range "00" -  |                | matching (see  |
   |                | "23"), MM      | In the context | ), the length  |
   |                | contains       | of a Query     | is 28 bytes    |
   |                | minutes (range | with range     | maximum.       |
   |                | "00" - "59"),  | matching (see  |                |
   |                | SS contains    | ), the         |                |
   |                | seconds (range | character "-"  |                |
   |                | "00" - "60"),  | is allowed.    |                |
   |                | and FFFFFF     |                |                |
   |                | contains a     |                |                |
   |                | fractional     |                |                |
   |                | part of a      |                |                |
   |                | second as      |                |                |
   |                | small as 1     |                |                |
   |                | millionth of a |                |                |
   |                | second (range  |                |                |
   |                | "000000" -     |                |                |
   |                | "999999"). A   |                |                |
   |                | 24-hour clock  |                |                |
   |                | is used.       |                |                |
   |                | Midnight shall |                |                |
   |                | be represented |                |                |
   |                | by only "0000" |                |                |
   |                | since "2400"   |                |                |
   |                | would violate  |                |                |
   |                | the hour       |                |                |
   |                | range. The     |                |                |
   |                | string may be  |                |                |
   |                | padded with    |                |                |
   |                | trailing       |                |                |
   |                | spaces.        |                |                |
   |                | Leading and    |                |                |
   |                | embedded       |                |                |
   |                | spaces are not |                |                |
   |                | allowed.       |                |                |
   |                |                |                |                |
   |                | One or more of |                |                |
   |                | the components |                |                |
   |                | MM, SS, or     |                |                |
   |                | FFFFFF may be  |                |                |
   |                | unspecified as |                |                |
   |                | long as every  |                |                |
   |                | component to   |                |                |
   |                | the right of   |                |                |
   |                | an unspecified |                |                |
   |                | component is   |                |                |
   |                | also           |                |                |
   |                | unspecified,   |                |                |
   |                | which          |                |                |
   |                | indicates that |                |                |
   |                | the value is   |                |                |
   |                | not precise to |                |                |
   |                | the precision  |                |                |
   |                | of those       |                |                |
   |                | unspecified    |                |                |
   |                | components.    |                |                |
   |                |                |                |                |
   |                | The FFFFFF     |                |                |
   |                | component, if  |                |                |
   |                | present, shall |                |                |
   |                | contain 1 to 6 |                |                |
   |                | digits. If     |                |                |
   |                | FFFFFF is      |                |                |
   |                | unspecified    |                |                |
   |                | the preceding  |                |                |
   |                | "." shall not  |                |                |
   |                | be included.   |                |                |
   |                |                |                |                |
   |                | Examples:      |                |                |
   |                |                |                |                |
   |                | 1              |                |                |
   |                | . "070907.0705 |                |                |
   |                |    "           |                |                |
   |                |    represents  |                |                |
   |                |    a time of 7 |                |                |
   |                |    hours, 9    |                |                |
   |                |    minutes and |                |                |
   |                |    7.0705      |                |                |
   |                |    seconds.    |                |                |
   |                |                |                |                |
   |                | 2. "1010"      |                |                |
   |                |    represents  |                |                |
   |                |    a time of   |                |                |
   |                |    10 hours,   |                |                |
   |                |    and 10      |                |                |
   |                |    minutes.    |                |                |
   |                |                |                |                |
   |                | 3. "021 " is   |                |                |
   |                |    an invalid  |                |                |
   |                |    value.      |                |                |
   |                |                |                |                |
   |                | .. note::      |                |                |
   |                |                |                |                |
   |                |    1. The      |                |                |
   |                |       ACR-NEMA |                |                |
   |                |       Standard |                |                |
   |                |       300      |                |                |
   |                |                |                |                |
   |                |   (predecessor |                |                |
   |                |       to       |                |                |
   |                |       DICOM)   |                |                |
   |                |                |                |                |
   |                |      supported |                |                |
   |                |       a string |                |                |
   |                |       of       |                |                |
   |                |                |                |                |
   |                |     characters |                |                |
   |                |       of the   |                |                |
   |                |       format   |                |                |
   |                |                |                |                |
   |                |  HH:MM:SS.frac |                |                |
   |                |       for this |                |                |
   |                |       VR. Use  |                |                |
   |                |       of this  |                |                |
   |                |       format   |                |                |
   |                |       is not   |                |                |
   |                |                |                |                |
   |                |     compliant. |                |                |
   |                |                |                |                |
   |                |    2. See also |                |                |
   |                |       DT VR in |                |                |
   |                |       this     |                |                |
   |                |       table.   |                |                |
   |                |                |                |                |
   |                |    3. The SS   |                |                |
   |                |                |                |                |
   |                |      component |                |                |
   |                |       may have |                |                |
   |                |       a value  |                |                |
   |                |       of 60    |                |                |
   |                |       only for |                |                |
   |                |       a leap   |                |                |
   |                |       second.  |                |                |
   +----------------+----------------+----------------+----------------+
   | UC             | A character    | Default        | 2\ :sup:`32`-2 |
   |                | string that    | Character      | bytes maximum  |
   | Unlimited      | may be of      | Repertoire     |                |
   | Characters     | unlimited      | and/or as      | See            |
   |                | length that    | defined by     | `p             |
   |                | may be padded  | (0008,0005)    | ara_title <#no |
   |                | with trailing  | excluding      | te_6.2-3-2>`__ |
   |                | spaces. The    | character code |                |
   |                | character code | 5CH (the       |                |
   |                | 5CH (the       | BACKSLASH "\"  |                |
   |                | BACKSLASH "\"  | in ISO-IR 6),  |                |
   |                | in ISO-IR 6)   | and all        |                |
   |                | shall not be   | Control        |                |
   |                | present, as it | Characters     |                |
   |                | is used as the | except ESC     |                |
   |                | delimiter      | when used for  |                |
   |                | between values | ISO 2022       |                |
   |                | in             | escape         |                |
   |                | multi-valued   | sequences.     |                |
   |                | data elements. |                |                |
   |                | The string     |                |                |
   |                | shall not have |                |                |
   |                | Control        |                |                |
   |                | Characters     |                |                |
   |                | except for     |                |                |
   |                | ESC.           |                |                |
   +----------------+----------------+----------------+----------------+
   | UI             | A character    | "0"-"9", "."   | 64 bytes       |
   |                | string         | of Default     | maximum        |
   | Unique         | containing a   | Character      |                |
   | Identifier     | UID that is    | Repertoire     |                |
   | (UID)          | used to        |                |                |
   |                | uniquely       |                |                |
   |                | identify a     |                |                |
   |                | wide variety   |                |                |
   |                | of items. The  |                |                |
   |                | UID is a       |                |                |
   |                | series of      |                |                |
   |                | numeric        |                |                |
   |                | components     |                |                |
   |                | separated by   |                |                |
   |                | the period "." |                |                |
   |                | character. If  |                |                |
   |                | a Value Field  |                |                |
   |                | containing one |                |                |
   |                | or more UIDs   |                |                |
   |                | is an odd      |                |                |
   |                | number of      |                |                |
   |                | bytes in       |                |                |
   |                | length, the    |                |                |
   |                | Value Field    |                |                |
   |                | shall be       |                |                |
   |                | padded with a  |                |                |
   |                | single         |                |                |
   |                | trailing NULL  |                |                |
   |                | (00H)          |                |                |
   |                | character to   |                |                |
   |                | ensure that    |                |                |
   |                | the Value      |                |                |
   |                | Field is an    |                |                |
   |                | even number of |                |                |
   |                | bytes in       |                |                |
   |                | length. See    |                |                |
   |                | `Unique        |                |                |
   |                | Identifiers    |                |                |
   |                | (UIDs) <       |                |                |
   |                | #chapter_9>`__ |                |                |
   |                | and `Creating  |                |                |
   |                | a Privately    |                |                |
   |                | Defined Unique |                |                |
   |                | Identifier     |                |                |
   |                | (              |                |                |
   |                | Informative) < |                |                |
   |                | #chapter_B>`__ |                |                |
   |                | for a complete |                |                |
   |                | specification  |                |                |
   |                | and examples.  |                |                |
   +----------------+----------------+----------------+----------------+
   | UL             | Unsigned       | not applicable | 4 bytes fixed  |
   |                | binary integer |                |                |
   | Unsigned Long  | 32 bits long.  |                |                |
   |                | Represents an  |                |                |
   |                | integer n in   |                |                |
   |                | the range:     |                |                |
   |                |                |                |                |
   |                | 0 <= n <       |                |                |
   |                | 2\ :sup:`32`.  |                |                |
   +----------------+----------------+----------------+----------------+
   | UN             | An             | not applicable | Any length     |
   |                | octet-stream   |                | valid for any  |
   | Unknown        | where the      |                | of the other   |
   |                | encoding of    |                | DICOM Value    |
   |                | the contents   |                | R              |
   |                | is unknown     |                | epresentations |
   |                | (see `Unknown  |                |                |
   |                | (UN) Value     |                |                |
   |                | Repre          |                |                |
   |                | sentation <#se |                |                |
   |                | ct_6.2.2>`__). |                |                |
   +----------------+----------------+----------------+----------------+
   | UR             | A string of    | The subset of  | 2\ :sup:`32`-2 |
   |                | characters     | the Default    | bytes maximum. |
   | Universal      | that           | Character      |                |
   | Resource       | identifies a   | Repertoire     | See            |
   | Identifier or  | URI or a URL   | required for   | `p             |
   | Universal      | as defined in  | the URI as     | ara_title <#no |
   | Resource       | `biblioentry_  | defined in     | te_6.2-3-2>`__ |
   | Locator        | title <#biblio | IETF RFC3986   |                |
   | (URI/URL)      | _RFC_3986>`__. | Section 2,     |                |
   |                | Leading spaces | plus the space |                |
   |                | are not        | (20H)          |                |
   |                | allowed.       | character      |                |
   |                | Trailing       | permitted only |                |
   |                | spaces shall   | as trailing    |                |
   |                | be ignored.    | padding.       |                |
   |                | Data Elements  |                |                |
   |                | with this VR   | Characters     |                |
   |                | shall not be   | outside the    |                |
   |                | multi-valued.  | permitted      |                |
   |                |                | character set  |                |
   |                | .. note::      | must be        |                |
   |                |                | "percent       |                |
   |                |    Both        | encoded".      |                |
   |                |    absolute    |                |                |
   |                |    and         | .. note::      |                |
   |                |    relative    |                |                |
   |                |    URIs are    |    The         |                |
   |                |    permitted.  |    Backslash   |                |
   |                |    If the URI  |    (5CH)       |                |
   |                |    is          |    character   |                |
   |                |    relative,   |    is among    |                |
   |                |    then it is  |    those       |                |
   |                |    relative to |    disallowed  |                |
   |                |    the base    |    in URIs.    |                |
   |                |    URI of the  |                |                |
   |                |    object      |                |                |
   |                |    within      |                |                |
   |                |    which it is |                |                |
   |                |    contained.  |                |                |
   +----------------+----------------+----------------+----------------+
   | US             | Unsigned       | not applicable | 2 bytes fixed  |
   |                | binary integer |                |                |
   | Unsigned Short | 16 bits long.  |                |                |
   |                | Represents     |                |                |
   |                | integer n in   |                |                |
   |                | the range:     |                |                |
   |                |                |                |                |
   |                | 0 <= n <       |                |                |
   |                | 2\ :sup:`16`.  |                |                |
   +----------------+----------------+----------------+----------------+
   | UT             | A character    | Default        | 2\ :sup:`32`-2 |
   |                | string that    | Character      | bytes maximum  |
   | Unlimited Text | may contain    | Repertoire     |                |
   |                | one or more    | and/or as      | See            |
   |                | paragraphs. It | defined by     | `p             |
   |                | may contain    | (0008,0005)    | ara_title <#no |
   |                | the Graphic    | excluding      | te_6.2-3-2>`__ |
   |                | Character set  | Control        |                |
   |                | and the        | Characters     |                |
   |                | Control        | except TAB,    |                |
   |                | Characters,    | LF, FF, CR     |                |
   |                | CR, LF, FF,    | (and ESC when  |                |
   |                | and ESC. It    | used for ISO   |                |
   |                | may be padded  | 2022 escape    |                |
   |                | with trailing  | sequences).    |                |
   |                | spaces, which  |                |                |
   |                | may be         |                |                |
   |                | ignored, but   |                |                |
   |                | leading spaces |                |                |
   |                | are considered |                |                |
   |                | to be          |                |                |
   |                | significant.   |                |                |
   |                | Data Elements  |                |                |
   |                | with this VR   |                |                |
   |                | shall not be   |                |                |
   |                | multi-valued   |                |                |
   |                | and therefore  |                |                |
   |                | character code |                |                |
   |                | 5CH (the       |                |                |
   |                | BACKSLASH "\"  |                |                |
   |                | in ISO-IR 6)   |                |                |
   |                | may be used.   |                |                |
   +----------------+----------------+----------------+----------------+
   | UV             | Unsigned       | not applicable | 8 bytes fixed  |
   |                | binary integer |                |                |
   | Unsigned       | 64 bits long.  |                |                |
   | 64-bit Very    | Represents an  |                |                |
   | Long           | integer n in   |                |                |
   |                | the range:     |                |                |
   |                |                |                |                |
   |                | 0 <= n <       |                |                |
   |                | 2\ :sup:`64`.  |                |                |
   +----------------+----------------+----------------+----------------+

.. note::

   1. For attributes that were present in ACR-NEMA 1.0 and 2.0 and that
      have been retired, the specifications of Value Representation and
      Value Multiplicity provided are recommendations for the purpose of
      interpreting their values in objects created in accordance with
      earlier versions of this Standard. These recommendations are
      suggested as most appropriate for a particular attribute; however,
      there is no guarantee that historical objects will not violate
      some requirements or specified VR and/or VM.

   2. The length of the value of UC, UR and UT VRs is limited only by
      the size of the maximum unsigned integer representable in a 32 bit
      VL field minus two, since FFFFFFFFH is reserved and lengths are
      required to be even.

   3. In previous editions of the Standard (see PS3.5 2015a), the TAB
      character was not listed as permitted for the ST, LT and UT VRs.
      It has been added for the convenience of formatting and the
      encoding of XML text.

.. _sect_6.2.1:

Person Name (PN) Value Representation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. _sect_6.2.1.1:

Examples of PN VR and Notes
^^^^^^^^^^^^^^^^^^^^^^^^^^^

Examples:

-  Rev. John Robert Quincy Adams, B.A. M.Div.

   "Adams^John Robert Quincy^^Rev.^B.A. M.Div."

   [One family name; three given names; no middle name; one prefix; two
   suffixes.]

-  Susan Morrison-Jones, Ph.D., Chief Executive Officer

   "Morrison-Jones^Susan^^^Ph.D., Chief Executive Officer"

   [Two family names; one given name; no middle name; no prefix; two
   suffixes.]

-  John Doe

   "Doe^John"

   [One family name; one given name; no middle name, prefix, or suffix.
   Delimiters have been omitted for the three trailing null components.]

-  (for examples of the encoding of Person Names using multi-byte
   character sets see `Character Sets and Person Name Value
   Representation in the Japanese Language
   (Informative) <#chapter_H>`__)

-  "Smith^Fluffy"

   [A cat, rather than a human, whose responsible party family name is
   Smith, and whose own name is Fluffy]

-  "ABC Farms^Running on Water"

   [A horse whose responsible organization is named ABC Farms, and whose
   name is "Running On Water"]

.. note::

   1. A similar multiple component convention is also used by the HL7 v2
      XPN data type. However, the XPN data type places the suffix
      component before the prefix, and has a sixth component "degree"
      that DICOM subsumes in the name suffix. There are also differences
      in the manner in which name representation is identified.

   2. In typical American and European usage the first occurrence of
      "given name" would represent the "first name". The second and
      subsequent occurrences of the "given name" would typically be
      treated as a middle name(s). The "middle name" component is
      retained for the purpose of backward compatibility with existing
      standards.

   3. The implementer should remain mindful of earlier usage forms that
      represented "given names" as "first" and "middle" and that
      translations to and from this previous typical usage may be
      required.

   4. For reasons of backward compatibility with older versions of this
      Standard, person names might be considered a single family name
      complex (single component without "^" delimiters).

.. _sect_6.2.1.2:

Ideographic and Phonetic Characters in Data Elements with VR of PN
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Character strings representing person names are encoded using a
convention for PN value representations based on component groups with 5
components.

For the purpose of writing names in ideographic characters and in
phonetic characters, up to 3 component groups may be used. The delimiter
of the component group shall be the equals character "=" (3DH). The
three component groups in their order of occurrence are: an alphabetic
representation, an ideographic representation, and a phonetic
representation.

Any component group may be absent, including the first component group.
In this case, the person name may start with one or more "=" delimiters.
Delimiters are also required for interior null component groups.
Trailing null component groups and their delimiters may be omitted.

The first component group (identified by DICOM as "alphabetic") shall be
encoded using the character set specified by the Attribute Specific
Character Set (0008,0005), value 1. If Attribute Specific Character Set
(0008,0005) is not present, the Default Character Repertoire ISO-IR 6
shall be used. ISO 2022 escapes for Code Extension shall not be used in
this component group. When Specific Character Set (0008,0005) value 1
specifies a multi-byte character set without Code Extension (i.e.,
Unicode in UTF-8, GB18030 or GBK), the characters of this component
group may be encoded with multiple bytes, but shall be drawn from the
code points U+0020 through U+1FFF of ISO/IEC 10646, or the following
ISO/IEC 10646 code points:

-  U+3001, U+3002, U+300C, U+300D, U+3099 through U+309C, and U+30A0
   through U+30FF

The second group shall be used for ideographic characters. The character
sets used will usually be those from Attribute Specific Character Set
(0008,0005), value 2 through n, and may use ISO 2022 escapes.

The third group shall be used for phonetic characters. The character
sets used shall be those from Attribute Specific Character Set
(0008,0005), value 1 through n, and may use ISO 2022 escapes.

Delimiter characters "^" and "=" are taken from the character set
specified by value 1 of the Attribute Specific Character Set
(0008,0005). If Attribute Specific Character Set (0008,0005), value 1 is
not present, the Default Character Repertoire ISO-IR 6 shall be used.

At the beginning of the value of the Person Name data element, the
following initial condition is assumed: if Attribute Specific Character
Set (0008,0005), value 1 is not present, the Default Character
Repertoire ISO-IR 6 is invoked, and if the Attribute Specific Character
Set (0008,0005), value 1 is present, the character set specified by
value 1 of the Attribute is invoked.

At the end of the value of the Person Name data element, and before the
component delimiters "^" and "=", the character set shall be switched to
the Default Character Repertoire ISO-IR 6, if value 1 of the Attribute
Specific Character Set (0008,0005) is not present. If value 1 of the
Attribute Specific Character Set (0008,0005) is present, the character
set shall be switched to that specified by value 1 of the Attribute.

The value length of each component group is 64 characters maximum,
including the delimiter for the component group. Each combining
character (e.g., diacritics or vowel marks) shall be considered a
separate character for this maximum length, regardless of how an
application may display such combining characters (i.e., combined into
the glyph for the base character, or rendered separately).

.. _sect_6.2.2:

Unknown (UN) Value Representation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Unknown (UN) VR shall only be used for Private Attribute Data
Elements and Standard Data Elements previously encoded as some DICOM VR
other than UN using the DICOM Default Transfer Syntax (Implicit VR
Little Endian), and whose Value Representation is currently unknown, or
whose known Value Representation is none of OB, OD, OF, OL, OW, SQ, UC,
UR or UT and whose value length exceeds 65534 (2\ :sup:`16`-2) and
therefore cannot be encoded as a 16-bit unsigned integer in the Value
Length Field defined for the known Value Representation (see `Person
Name (PN) Value Representation <#sect_6.2.1>`__). As long as the VR is
unknown the Value Field is insensitive to byte ordering and shall not be
'byte-swapped' (see `Little Endian Byte Ordering <#sect_7.3>`__). In the
case of undefined length sequences, the value shall remain in implicit
VR form. See `Private Data Elements <#sect_7.8>`__ for a description of
Private Data Attribute Elements and section 10 and `Transfer Syntax
Specifications (Normative) <#chapter_A>`__ for a discussion of Transfer
Syntaxes.

The UN VR shall not be used for Private Creator Data Elements (i.e., the
VR is equal to LO, see `Private Data Element Tags <#sect_7.8.1>`__).

The UN VR shall not be used for File Meta Information Data Elements (any
Tag (0002,xxxx), see ).

.. note::

   1. All other (non-default) DICOM Transfer Syntaxes employ explicit VR
      in their encoding, and therefore any Private and/or Standard Data
      Element Value Field Attribute value encoded and decoded using any
      Transfer Syntax other than the default, and not having been
      translated to the DICOM Default Transfer Syntax default in the
      interim, will have a known VR.

   2. If at some point an application knows the actual VR for an
      Attribute of VR UN (e.g., has its own applicable data dictionary),
      it can assume that the Value Field of the Attribute is encoded in
      Little Endian byte ordering with implicit VR encoding,
      irrespective of the current Transfer Syntax.

   3. This VR of UN is needed when an explicit VR must be given to a
      Data Element whose Value Representation is unknown (e.g., store
      and forward).

   4. This VR of UN is also needed for the encoding of Data Elements
      with explicit VR whose value length exceeds 65534 (2\ :sup:`16`-2)
      (FFFEH, the largest even length unsigned 16 bit number) but which
      are defined to have a 16 bit explicit VR length field.

   5. The length field of the Value Representation of UN may contain the
      value of Undefined Length, in which case the contents can be
      assumed to be encoded with implicit VR. See `Item Encoding
      Rules <#sect_7.5.1>`__ to determine how to parse Data Elements
      with an Undefined Length.

   6. An example of a Standard Data Element using a UN VR is a Type 3 or
      Type U Standard Attribute added to an SOP Class definition. An
      existing application that does not support that new Attribute (and
      encounters it) could convert the VR to UN.

.. _sect_6.2.3:

URI/URL (UR) Value Representation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The URI/URL (UR) VR uses a subset of the Default Character Repertoire as
defined in `biblioentry_title <#biblio_RFC_3986>`__, and shall not use
any code extension or replacement techniques. URI/URL domain name
components that in their original form use characters outside the
permitted character set shall use the Internationalized Domain Names for
Applications encoding in accordance with IETF RFC5890 and RFC5891. Other
URI/URL content that uses characters outside the permitted character set
shall use the Internationalized Resource Identifiers encoding mechanism
of IETF RFC 3987, representing the content string in UTF-8 and percent
encoding characters as required.

.. note::

   For example, the use of a patient name in a URI/URL string may
   require use of the `biblioentry_title <#biblio_RFC_3987>`__
   technique.

.. _sect_6.3:

Enumerated Values and Defined Terms
-----------------------------------

The value of certain Data Elements may be chosen among a set of explicit
Values satisfying its VR. These explicit Values are either Enumerated
Values or Defined Terms and are specified in and .

Enumerated Values are used when the specified explicit Values are the
only Values allowed for a Data Element. A Data Element with Enumerated
Values that does not have a Value equivalent to one of the Values
specified in this Standard has an invalid value within the scope of a
specific Information Object/SOP Class definition.

.. note::

   1. Patient Sex (0010, 0040) is an example of a Data Element having
      Enumerated Values. It is defined to have a Value that is either
      "M", "F", or "O" (see ). No other Value shall be given to this
      Data Element.

   2. Future modifications of this Standard may add to the set of
      allowed values for Data Elements with Enumerated Values. Such
      additions by themselves may or may not require a change in SOP
      Class UIDs, depending on the semantics of the Data Element.

Defined Terms are used when the specified explicit Values may be
extended by implementers to include additional new Values. These new
Values shall be specified in the Conformance Statement (see ) and shall
not have the same meaning as currently defined Values in this Standard.
A Data Element with Defined Terms that does not contain a Value
equivalent to one of the Values currently specified in this Standard
shall not be considered to have an invalid value. An empty (zero length)
value is not a valid new Value for a Defined Term; empty values shall be
considered invalid unless the Standard specifically permits empty
values. New Values shall not have a meaning of unknown, since that
concept, if permitted by the Standard, shall be conveyed explicitly
either by allowing the Data Element to be zero length or by provision of
a standard Defined Term with such a meaning.

.. note::

   1. Reporting Priority (0040,1009) is an example of a Data Element
      having Defined Terms. It is defined to have a Value that may be
      one of the set of standard Values; HIGH, ROUTINE, MEDIUM, or LOW
      (see ). Because this Data Element has Defined Terms other
      reporting priorities may be defined by the implementer.

   2. The validity of empty values is usually specified by the attribute
      being defined as Type 2 (see `Type 2 Required Data
      Elements <#sect_7.4.3>`__). However, in the context of a required
      Type 1 attribute with multiple values, some (but not all) values
      may be allowed to be empty (see `Type 1 Required Data
      Elements <#sect_7.4.1>`__); in this case the Standard explicitly
      specifies the validity of empty values in the list of Defined
      Terms for each value. Specific Character Set (0008,0005) is an
      example of a Data Element for which the Standard specifically
      permits the first value to be empty when multiple values are
      present. Image Type (0008,0008) is an example of a Data Element
      that in some IODs defined in is required to be present with
      multiple values, but if an empty value is not explicitly listed in
      the Defined Terms for Value 3 by an IOD an empty value is invalid.

The Value Representation may affect the interpretation of Defined Terms
and Enumerated Values for numeric values. For binary Value
Representations, the textual representation of the Value in the Standard
does not affect the interpretation. For string Value Representations (IS
and DS), the meaning of the Value in the Standard shall be used, not the
literal string.

.. note::

   For example, an Enumerated Value of "1" expressed in the text of the
   Standard matches an IS or DS value encoded as "001", or a DS value
   encoded as "1.0" or "1." or "1.0000E+00" or any permitted encoding.
   Leading and trailing spaces are defined in
   `table_title <#table_6.2-1>`__ not to be significant and hence do not
   affect the interpretation.

.. _sect_6.4:

Value Multiplicity (VM) and Delimitation
----------------------------------------

The Value Multiplicity of a Data Element specifies the number of Values
that can be encoded in the Value Field of that Data Element. The VM of
each Data Element is specified explicitly in . If the number of Values
that may be encoded in an element is variable, it shall be represented
by two numbers separated by a dash; e.g., "1-10" means that there may be
1 to 10 Values in the element.

.. note::

   Elements having a multiplicity of "S", which represented "single", in
   older versions of this Standard, will have a multiplicity of "1" in
   this version of this Standard.

When a Data Element has multiple Values, those Values shall be delimited
as follows:

-  For character strings, the character 5CH (BACKSLASH "\" in the case
   of the repertoire ISO IR-6) shall be used as a delimiter between
   Values.

   .. note::

      BACKSLASH ("\") is used as a delimiter between character string
      Values that are of fixed length as well as variable length.

-  Multiple binary Values of fixed length shall be a series of
   concatenated Values without any delimiter.

Each string Value in a multi-valued character string may be of even or
odd length, but the length of the entire Value Field (including "\"
delimiters) shall be of even length. If padding is required to make the
Value Field of even length, a single padding character shall be applied
to the end of the Value Field (to the last Value), in which case the
length of the last Value may exceed the Length of Value by 1.

.. note::

   A padding character may need to be appended to a fixed length
   character string value in the above case.

Only the last UID Value in a multi-valued Data Element with a VR of UI
shall be padded with a single trailing NULL (00H) character when
necessary to ensure that the entire Value Field (including "\"
delimiters) is of even length.

Data Elements with a VR of LT, OB, OD, OF, OL, OW, SQ, ST, UN, UR or UT
shall always have a Value Multiplicity of one. See
`table_title <#table_6.2-1>`__.

