.. _chapter_K:

Character Sets and Person Name Value Representation in the Chinese Language with Code Extensions (Informative)
==============================================================================================================

.. _sect_K.1:

Character Sets for the Chinese Language in DICOM
------------------------------------------------

GB 2312 (registered as ISO-IR 58) is used as a Chinese character set in
DICOM. This character set is the one most broadly used for the
representation of Chinese characters. It can be encoded by ISO 2022 code
extension techniques.

The Escape Sequence is shown for reference in
`table_title <#table_K.1-1>`__ (see )

.. table:: ISO/IEC 2022 Escape Sequence for ISO-IR 58

   ============= =====================
   \             ISO-IR 58
   ============= =====================
   G0 set(ASCII) ESC 02/08 04/02
   G1 set        ESC 02/04 02/09 04/01
   ============= =====================

.. _sect_K.2:

Example of Person Name Value Representation in the Chinese Language
-------------------------------------------------------------------

Person names in the Chinese language may be written in Pinyin (phonetic
characters), Hanzi (ideographic characters), or English Name (alphabetic
characters). The three component groups should be written in the order
of alphabetic (English name), ideographic, and phonetic.

Specific Character Set:

-  (0008,0005) \\ISO 2022 IR 58

Character String:

-  *Zhang^XiaoDong=张^小东=*

Encoded String:

-  *Zhang^XiaoDong= ESC 02/04 02/09 04/01 张^ESC 02/04 02/09 04/01小东
   =*

Character encoded representation (GB2312) is:

-  ``0x5A 0x68 0x61 0x6E 0x67 0x5E 0x58 0x69 0x61 0x6F 0x44 0x6F 0x6E 0x67 0x3D``
   **``0x1B 0x24 0x29 0x41``** *``0xD5 0xC5``* ``0x5E``
   **``0x1B 0x24 0x29 0x41``** *``0xD0 0xA1 0xB6 0xAB``* ``0x3D 0x20``

.. note::

   1. The underlined byte codes correspond to double byte characters,
      the bold byte codes to escape sequences.

   2. The multi-byte character set (ISO-IR 58) and single-byte character
      set (ISO 646) can be used intermixed without any explicit escape
      sequence after the initial escape sequence, up to the next
      delimiter (^ or =) or the end of the value field. Once ISO 646 has
      been designated to G0 and ISO-IR 58 to G1, each character set has
      a different code area, thus can be used intermixed. The decoder
      will check the most significant bit of a character to know whether
      it is a two byte character in the G1 area (high bit one) or a one
      byte character in the G0 area (high bit zero). There does not need
      to be an explicit escape to invoke ISO 646 into G0 at the end of
      the string prior to a delimiter (^ or =) or the end of the value
      field. However, there does need to be a new invocation of ISO-IR
      58 in each name component in which it is used.

.. _sect_K.3:

Example of Long Text Value Representation in the Chinese Language with GB2312 G1
--------------------------------------------------------------------------------

Chinese (ISO 2022 IR 58) and ASCII (ISO 646) character sets can be used
intermingled without explicit escape sequences between them. The Chinese
character set ISO IR 58 is invoked to the G1 area, and the ASCII
character set is invoked to the G0 area. The following is an example of
a Long Text value representation that includes ASCII and Chinese
character set. Every line is presumed to start in the default character
set and requires an explicit invocation of GB 2312 into G1, but does not
require re-invocation of the default ASCII character set into G0.

Specific Character Set:

-  (0008,0005) \\ISO 2022 IR 58

Character String (with CR LF after each line):

-  1) *第一行文字。*

   2) *第二行文字。*

   3) *第三行文字。*

Encoded String:

-  1) ESC 02/04 02/09 04/01 *第一行文字。*

   2) ESC 02/04 02/09 04/01 *第二行文字。*

   3) ESC 02/04 02/09 04/01 *第三行文字。*

Character encoded representation (GB2312):

-  ``0x31 0x2e`` **``0x1B 0x24 0x29 0x41``**
   *``0xB5 0xDA 0xD2 0xBB 0xD0 0xD0 0xCE 0xC4 0xD7 0xD6 0xA1 0xA3``*
   ``0x0D 0x0A``

   ``0x32 0x2e`` **``0x1B 0x24 0x29 0x41``**
   *``0xB5 0xDA 0xB6 0xFE 0xD0 0xD0 0xCE 0xC4 0xD7 0xD6 0xA1 0xA3``*
   ``0x0D 0x0A``

   ``0x33 0x2e`` **``0x1B 0x24 0x29 0x41``**
   *``0xB5 0xDA 0xC8 0xFD 0xD0 0xD0 0xCE 0xC4 0xD7 0xD6 0xA1 0xA3``*
   ``0x0D 0x0A``

.. note::

   The underlined byte codes correspond to double byte characters, the
   bold byte codes to escape sequences.

.. table:: Character Sets and Escape Sequences used in the Examples of
Person Name

   +-------+-------+-------+-------+-------+-------+-------+-------+
   | *     | *     | **    | **ISO | **Sta | **ESC | *     | *     |
   | *Char | *Comp | Value | re    | ndard | Seque | *Code | *Char |
   | acter | onent | of    | gistr | for   | nce** | Elem  | acter |
   | Set   | Gr    | (     | ation | Code  |       | ent** | Set:  |
   | Des   | oup** | 0008, | num   | E     |       |       | Pu    |
   | cript |       | 0005) | ber** | xtens |       |       | rpose |
   | ion** |       | De    |       | ion** |       |       | of    |
   |       |       | fined |       |       |       |       | Use** |
   |       |       | T     |       |       |       |       |       |
   |       |       | erm** |       |       |       |       |       |
   +=======+=======+=======+=======+=======+=======+=======+=======+
   | Ch    | F     | Value | I     |       |       | G0    | ISO   |
   | inese | irst: | 1:    | SO-IR |       |       |       | 646:  |
   |       |       |       | 6     |       |       |       |       |
   |       | Alpha | none  |       |       |       |       |       |
   |       | betic |       |       |       |       |       |       |
   |       | (En   |       |       |       |       |       |       |
   |       | glish |       |       |       |       |       |       |
   |       | name) |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+
   | Se    | Value | ISO   | ISO   | ESC   | G1    | ISO   |       |
   | cond: | 1:    | -IR58 | 2022  | 02/04 |       | 2022  |       |
   |       |       |       |       | 02/09 |       | CN:   |       |
   | I     | ISO   |       |       | 04/01 |       |       |       |
   | deogr | 2022  |       |       |       |       | Ch    |       |
   | aphic | IR 58 |       |       |       |       | inese |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+
   | T     | Value | I     | ISO   | ESC   | G0    | ISO   |       |
   | hird: | 1:    | SO-IR | 2022  | 02/08 |       | 646:  |       |
   |       |       | 6     |       | 04/02 |       |       |       |
   | Pho   | none  |       |       |       |       | For   |       |
   | netic |       |       |       |       |       | delim |       |
   |       |       |       |       |       |       | iters |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+
