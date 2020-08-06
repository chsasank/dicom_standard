.. _chapter_H:

Character Sets and Person Name Value Representation in the Japanese Language (Informative)
==========================================================================================

.. _sect_H.1:

Character Sets for the Japanese Language
----------------------------------------

The purpose of this section is to explain the character sets for the
Japanese language.

.. _sect_H.1.1:

JIS X 0201
~~~~~~~~~~

JIS X 0201 has the following code elements:

-  ISO-IR 13 Japanese katakana (phonetic) characters (94 characters)

-  ISO-IR 14 Japanese romaji (alphanumeric) characters (94 characters)

JIS X 0201 defines a 7-bit romaji code table (ISO-IR 14), a 7-bit
katakana code table (ISO-IR 13), and the combination of romaji and
katakana as an 8-bit code table (ISO-IR 14 as G0, ISO-IR 13 as G1).

The 7-bit romaji (ISO-IR 14) is identical to ASCII (ISO-IR 6) except
that bit combination 05/12 represents a yen sign and bit combination
07/14 represents an over-line. These are national Graphic Character
allocations in ISO 646.

The Escape Sequence for ISO/IEC 2022 is shown for reference in
`table_title <#table_H.1-1>`__ (for the Defined Terms, see ).

.. table:: ISO/IEC 2022 Escape Sequence for ISO-IR 13 and ISO-IR 14

   ====== =================== ===================
   \      **ISO-IR 14**       **ISO-IR 13**
   ====== =================== ===================
   G0 set **ESC 02/08 04/10** ESC 02/08 04/09
   G1 set ESC 02/09 04/10     **ESC 02/09 04/09**
   ====== =================== ===================

.. note::

   1. `table_title <#table_H.1-1>`__ does not include the G2 and G3 sets
      that are not used in DICOM. See `Assumed Initial
      States <#sect_6.1.2.5.1>`__.

   2. Defined Terms ISO_IR 13 and ISO 2022 IR 13 for the value of the
      Specific Character Set (0008,0005) support the G0 set for ISO-IR
      14 and G1 set for ISO-IR 13. See .

.. _sect_H.1.2:

JIS X 0208
~~~~~~~~~~

JIS X 0208 has the following code element:

-  ISO-IR 87: Japanese kanji (ideographic), hiragana (phonetic), and
   katakana (phonetic) characters (94\ :sup:`2` characters, 2-byte).

.. _sect_H.1.3:

JIS X 0212
~~~~~~~~~~

JIS X 0212 has the following code element:

-  ISO-IR 159: Supplementary Japanese kanji (ideographic) characters
   (94\ :sup:`2` characters, 2-byte)

The Escape Sequence for ISO/IEC 2022 is shown for reference in
`table_title <#table_H.1-2>`__ (for the Defined Terms, see )

.. table:: ISO/IEC 2022 Escape Sequence for ISO-IR 87 and ISO-IR 159

   ====== ===================== =========================
   \      **ISO-IR 87**         **ISO-IR 159**
   ====== ===================== =========================
   G0 set **ESC 02/04 04/02**   **ESC 02/04 02/08 04/04**
   G1 set ESC 02/04 02/09 04/02 ESC 02/04 02/09 04/04
   ====== ===================== =========================

.. note::

   1. The Escape Sequence for the designation function G0-DESIGNATE
      94-SET, has first I byte 02/04 and second I byte 02/08. There is
      an exception to this: The second I byte 02/08 is omitted if the
      Final Byte is 04/00, 04/01 or 04/02. See ISO/IEC 2022.

   2. The table does not include the G2 and G3 sets that are not used in
      DICOM. See `Assumed Initial States <#sect_6.1.2.5.1>`__.

   3. Defined Term ISO 2022 IR 87 for the value of the Specific
      Character Set (0008,0005) supports the G0 set for ISO-IR 87, and
      Defined Term ISO 2022 IR 159 supports the G0 set for ISO-IR 159.
      See .

.. _sect_H.2:

Internet Practice
-----------------

DICOM has adopted an encoding method for Japanese character sets that is
similar to the method for Internet practice.

The major protocols for the Internet such as SMTP, NNTP and HTTP adopt
the encoding method for Japanese characters called "ISO-2022-JP" as
described in RFC 1468, Japanese Character Encoding for Internet
Messages. There is also a less commonly used Internet practice called
"ISO-2022-JP-2" described in RFC 1554, which supports a larger
repertoire of character sets and additionally requires an escape to a
single-byte character set before encoding a SPACE (unlike DICOM and
ISO-2022-JP).

The character sets supported for the Japanese language in DICOM and
Internet practice are shown in `table_title <#table_H.2-1>`__.

.. table:: Character Sets for the Japanese language in DICOM and
Internet practice

   +----------------------+----------------------+----------------------+
   | **DICOM**            | **ISO-2022-JP**      | **ISO-2022-JP-2**    |
   +======================+======================+======================+
   | ASCII (ISO-IR 6)     | ASCII (ISO-IR 6)     | ASCII (ISO-IR 6)     |
   |                      |                      |                      |
   | JIS X 0201 Katakana  | JIS-X 0201 Romaji    | ISO8859-1 (ISO-IR    |
   | (ISO-IR 13)          | (ISO-IR 14)          | 100)                 |
   |                      |                      |                      |
   | JIS X 0201 Romaji    | JIS X 0208-1978      | ISO8859-7 Greek      |
   | (ISO-IR 14)          | Kanji (ISO-IR 42)    | (ISO-IR 126)         |
   |                      |                      |                      |
   | JIS X 0208 Kanji     | JIS-X 0208-1983      | JIS X 0201 Romaji    |
   | (ISO-IR 87)          | Kanji (ISO-IR 87)    | (ISO-IR 14)          |
   |                      |                      |                      |
   | JIS X 0212 Kanji     |                      | JIS X 0208-1978      |
   | (ISO-IR 159)         |                      | Kanji (ISO-IR 42)    |
   |                      |                      |                      |
   |                      |                      | JIS X 0208-1983      |
   |                      |                      | Kanji (ISO-IR 87)    |
   |                      |                      |                      |
   |                      |                      | JIS X 0212-1990      |
   |                      |                      | Kanji (ISO-IR 159)   |
   |                      |                      |                      |
   |                      |                      | GB2312-1980 (ISO-IR  |
   |                      |                      | 58)                  |
   |                      |                      |                      |
   |                      |                      | KSC5601-1987 (ISO-IR |
   |                      |                      | 149)                 |
   +----------------------+----------------------+----------------------+

The Control Characters supported in DICOM and Internet practice are
shown in `table_title <#table_H.2-2>`__.

.. table:: Control Characters Supported in DICOM and Internet practice

   =========== =================================
   **DICOM**   **ISO-2022-JP and ISO-2022-JP-2**
   =========== =================================
   LF (00/10)  LF (00/10)
               
   FF (00/12)  CR (00/13)
               
   CR (00/13)  SO (00/14)
               
   ESC (01/11) SI (00/15)
               
               ESC (01/11)
   =========== =================================

.. _sect_H.3:

Example of Person Name Value Representation in the Japanese Language
--------------------------------------------------------------------

Character strings representing person names are encoded using a
convention for PN value representations based on component groups with 5
components.

For languages that use ideographic characters, it is sometimes necessary
to write names both in ideographic characters and in phonetic
characters. Ideographic characters may be required for official
purposes, while phonetic characters may be needed for pronunciation and
data processing purposes.

For the purpose of writing names in ideographic characters and in
phonetic characters, up to 3 component groups may be used. The delimiter
of the component group shall be the equals character "=" (3DH). The
three component groups in their order of occurrence are: an alphabetic
representation, an ideographic representation, and a phonetic
representation.

.. _sect_H.3.1:

Value 1 of Attribute Specific Character Set (0008,0005) is Not Present.
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In this case, ISO-IR 6 is used by default in Specific Character Set:

-  (0008,0005) \\ISO 2022 IR 87

Character String:

-  *Yamada^Tarou=山田^太郎=やまだ^たろう*

-  *Yamada^Tarou= ESC 02/04 04/02 山田 ESC 02/08 04/02 ^ ESC 02/04 04/02
   太郎 ESC 02/08 04/02 = ESC 02/04 04/02 やまだ ESC 02/08 04/02 ^ ESC
   02/04 04/02 たろう ESC 02/08 04/02*

Encoded representation:

-  ``05/09 06/01 06/13 06/01 06/04 06/01 5/14 05/04 06/01 07/02 06/15 07/05 03/13 01/11 02/04 04/02 03/11 03/03 04/05 04/04 01/11 02/08 04/02 05/14 01/11 02/04 04/02 04/02 04/00 04/15 03/10 01/11 02/08 04/02 03/13 01/11 02/04 04/02 02/04 06/04 02/04 05/14 02/04 04/00 01/11 02/08 04/02 05/14 01/11 02/04 04/02 02/04 03/15 02/04 06/13 02/04 02/06 01/11 02/08 04/02``

An example of what might be displayed or printed by an ASCII based
machine that displays or prints the Control Character ESC (01/11) using
\\033:

-  *``Yamada^Tarou=\033$B;3ED\033(B^\033$BB@O:\033(B=\033$B$d$^$@\033(B^\033$B$?$m$&\033(B``*

.. table:: Character Sets and Escape Sequences Used in Example 1

   +-------+-------+-------+-------+-------+-------+-------+-------+
   | *     | *     | **    | **ISO | **Sta | **ESC | *     | *     |
   | *Char | *Comp | Value | Re    | ndard | Seque | *Code | *Char |
   | acter | onent | of    | gistr | for   | nce** | Elem  | acter |
   | Set   | Gr    | (     | ation | Code  |       | ent** | Set:  |
   | Des   | oup** | 0008, | Num   | E     |       |       | Pu    |
   | cript |       | 0005) | ber** | xtens |       |       | rpose |
   | ion** |       | De    |       | ion** |       |       | of    |
   |       |       | fined |       |       |       |       | Use** |
   |       |       | T     |       |       |       |       |       |
   |       |       | erm** |       |       |       |       |       |
   +=======+=======+=======+=======+=======+=======+=======+=======+
   | Jap   | F     | Value | I     |       |       | GL    | ISO   |
   | anese | irst: | 1:    | SO-IR |       |       |       | 646:  |
   |       |       |       | 6     |       |       |       |       |
   |       | S     | none  |       |       |       |       |       |
   |       | ingle |       |       |       |       |       |       |
   |       | -byte |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+
   |       | Se    | Value | I     | ISO   | ESC   | GL    | JIS X |
   |       | cond: | 2:    | SO-IR | 2022  | 02/04 |       | 0208: |
   |       |       |       | 87    |       | 04/02 |       |       |
   |       | I     | ISO   |       |       |       |       | Jap   |
   |       | deogr | 2022  |       |       |       |       | anese |
   |       | aphic | IR 87 |       |       |       |       | k     |
   |       |       |       |       |       |       |       | anji, |
   |       |       |       |       |       |       |       | hira  |
   |       |       |       |       |       |       |       | gana, |
   |       |       |       |       |       |       |       | kat   |
   |       |       |       |       |       |       |       | akana |
   +-------+-------+-------+-------+-------+-------+-------+-------+
   |       |       | Value | I     | ISO   | ESC   | GL    | ISO   |
   |       |       | 1:    | SO-IR | 2022  | 02/08 |       | 646:  |
   |       |       |       | 6     |       | 04/02 |       |       |
   |       |       | none  |       |       |       |       | for   |
   |       |       |       |       |       |       |       | delim |
   |       |       |       |       |       |       |       | iters |
   +-------+-------+-------+-------+-------+-------+-------+-------+
   |       | T     | Value | I     | ISO   | ESC   | GL    | JIS X |
   |       | hird: | 2:    | SO-IR | 2022  | 02/04 |       | 0208: |
   |       |       |       | 87    |       | 04/02 |       |       |
   |       | Pho   | ISO   |       |       |       |       | Jap   |
   |       | netic | 2022  |       |       |       |       | anese |
   |       |       | IR 87 |       |       |       |       | hira  |
   |       |       |       |       |       |       |       | gana, |
   |       |       |       |       |       |       |       | and   |
   |       |       |       |       |       |       |       | kat   |
   |       |       |       |       |       |       |       | akana |
   +-------+-------+-------+-------+-------+-------+-------+-------+
   |       |       | Value | I     | ISO   | ESC   | GL    | ISO   |
   |       |       | 1:    | SO-IR | 2022  | 02/08 |       | 646:  |
   |       |       |       | 6     |       | 04/02 |       |       |
   |       |       | none  |       |       |       |       | for   |
   |       |       |       |       |       |       |       | delim |
   |       |       |       |       |       |       |       | iters |
   +-------+-------+-------+-------+-------+-------+-------+-------+

.. _sect_H.3.2:

Value 1 of Attribute Specific Character Set (0008,0005) is ISO 2022 IR 13.
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Specific Character Set:

-  (0008,0005) ISO 2022 IR 13\ISO 2022 IR 87

Character String:

-  *ヤマダ^タロウ=山田^太郎=やまだ^たろう*

-  *ヤマダ^タロウ= ESC 02/04 04/02 山田 ESC 02/08 04/10 ^ ESC 02/04
   04/02 太郎 ESC 02/08 04/10 = ESC 02/04 04/02 やまだ ESC 02/08 04/10 ^
   ESC 02/04 04/02 たろう ESC 02/08 04/10*

Encoded representation:

-  ``13/04 12/15 12/00 13/14 05/14 12/00 13/11 11/03 03/13 01/11 02/04 04/02 03/11 03/03 04/05 04/04 01/11 02/08 04/10 05/14 01/11 02/04 04/02 04/02 04/00 04/15 03/10 01/11 02/08 04/10 03/13 01/11 02/04 04/02 02/04 06/04 02/04 05/14 02/04 04/00 01/11 02/08 04/10 05/14 01/11 02/04 04/02 02/04 03/15 02/04 06/13 02/04 02/06 01/11 02/08 04/10``

An example of what might be displayed or printed by an ASCII based
machine that displays or prints the Control Character ESC (01/11) using
\\033:

-  ``\324\3l7\300\336^\300\333\263=\033$B;3ED\033(J^\033$BB@O:\033(J=\033$B$d$^$@\033(J^\033$B$?$m$&\033(J``

.. table:: Character Sets and Escape Sequences Used in Example 2

   +-------+-------+-------+-------+-------+-------+-------+-------+
   | *     | *     | **    | **ISO | **Sta | **ESC | *     | *     |
   | *Char | *Comp | Value | Re    | ndard | Seque | *Code | *Char |
   | acter | onent | of    | gistr | for   | nce** | Elem  | acter |
   | Set   | Gr    | (     | ation | Code  |       | ent** | Set:  |
   | Des   | oup** | 0008, | Num   | E     |       |       | Pu    |
   | cript |       | 0005) | ber** | xtens |       |       | rpose |
   | ion** |       | De    |       | ion** |       |       | of    |
   |       |       | fined |       |       |       |       | Use** |
   |       |       | T     |       |       |       |       |       |
   |       |       | erm** |       |       |       |       |       |
   +=======+=======+=======+=======+=======+=======+=======+=======+
   | Jap   | F     | Value | I     | ISO   | ESC   | GR    | JIS X |
   | anese | irst: | 1:    | SO-IR | 2022  | 02/09 |       | 0201: |
   |       |       |       | 13    |       | 04/09 |       |       |
   |       | S     | ISO   |       |       |       |       | Jap   |
   |       | ingle | 2022  |       |       |       |       | anese |
   |       | -byte | IR 13 |       |       |       |       | kat   |
   |       |       |       |       |       |       |       | akana |
   +-------+-------+-------+-------+-------+-------+-------+-------+
   |       |       |       | I     | ISO   | ESC   | GL    | JIS X |
   |       |       |       | SO-IR | 2022  | 02/08 |       | 0201: |
   |       |       |       | 14    |       | 04/10 |       |       |
   |       |       |       |       |       |       |       | Jap   |
   |       |       |       |       |       |       |       | anese |
   |       |       |       |       |       |       |       | r     |
   |       |       |       |       |       |       |       | omaji |
   |       |       |       |       |       |       |       | for   |
   |       |       |       |       |       |       |       | delim |
   |       |       |       |       |       |       |       | iters |
   +-------+-------+-------+-------+-------+-------+-------+-------+
   |       | Se    | Value | I     | ISO   | ESC   | GL    | JIS X |
   |       | cond: | 2:    | SO-IR | 2022  | 02/04 |       | 0208: |
   |       |       |       | 87    |       | 04/02 |       |       |
   |       | I     | ISO   |       |       |       |       | Jap   |
   |       | deogr | 2022  |       |       |       |       | anese |
   |       | aphic | IR 87 |       |       |       |       | k     |
   |       |       |       |       |       |       |       | anji, |
   |       |       |       |       |       |       |       | hira  |
   |       |       |       |       |       |       |       | gana, |
   |       |       |       |       |       |       |       | kat   |
   |       |       |       |       |       |       |       | akana |
   +-------+-------+-------+-------+-------+-------+-------+-------+
   |       |       | Value | I     | ISO   | ESC   | GL    | JIS X |
   |       |       | 1:    | SO-IR | 2022  | 02/08 |       | 0201: |
   |       |       |       | 14    |       | 04/10 |       |       |
   |       |       | ISO   |       |       |       |       | Jap   |
   |       |       | 2022  |       |       |       |       | anese |
   |       |       | IR 13 |       |       |       |       | r     |
   |       |       |       |       |       |       |       | omaji |
   |       |       |       |       |       |       |       | for   |
   |       |       |       |       |       |       |       | delim |
   |       |       |       |       |       |       |       | iters |
   +-------+-------+-------+-------+-------+-------+-------+-------+
   |       | T     | Value | I     | ISO   | ESC   | GL    | JIS X |
   |       | hird: | 2:    | SO-IR | 2022  | 02/04 |       | 0208: |
   |       |       |       | 87    |       | 04/02 |       |       |
   |       | Pho   | ISO   |       |       |       |       | Jap   |
   |       | netic | 2022  |       |       |       |       | anese |
   |       |       | IR 87 |       |       |       |       | hira  |
   |       |       |       |       |       |       |       | gana, |
   |       |       |       |       |       |       |       | and   |
   |       |       |       |       |       |       |       | kat   |
   |       |       |       |       |       |       |       | akana |
   +-------+-------+-------+-------+-------+-------+-------+-------+
   |       |       | Value | I     | ISO   | ESC   | GL    | JIS X |
   |       |       | 1:    | SO-IR | 2022  | 02/08 |       | 0201: |
   |       |       |       | 14    |       | 04/10 |       |       |
   |       |       | ISO   |       |       |       |       | Jap   |
   |       |       | 2022  |       |       |       |       | anese |
   |       |       | IR 13 |       |       |       |       | r     |
   |       |       |       |       |       |       |       | omaji |
   |       |       |       |       |       |       |       | for   |
   |       |       |       |       |       |       |       | delim |
   |       |       |       |       |       |       |       | iters |
   +-------+-------+-------+-------+-------+-------+-------+-------+

