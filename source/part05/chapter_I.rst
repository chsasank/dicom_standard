.. _chapter_I:

Character Sets and Person Name Value Representation in the Korean Language (Informative)
========================================================================================

.. _sect_I.1:

Character Sets For The Korean Language in DICOM
-----------------------------------------------

KS X 1001 (registered as ISO-IR 149) is used as a Korean character set
in DICOM. This character set is the one most broadly used for the
representation of Korean characters. It can be encoded by ISO 2022 code
extension techniques, and is registered in ISO 2375.

The Escape Sequence is shown for reference in
`table_title <#table_I.1-1>`__ (see )

.. table:: ISO/IEC 2022 Escape Sequence for ISO-IR 149

   ====== =========================
   \      ISO-IR 149
   ====== =========================
   G0 set ESC 02/04 02/08 04/03
   G1 set **ESC 02/04 02/09 04/03**
   ====== =========================

.. note::

   1. ISO-IR 149 is only used as a G1 set in DICOM.

   2. The Korean character set (ISO IR 149) is invoked to the G1 area.
      This is different from the Japanese multi-byte character sets (ISO
      2022 IR 87 and ISO 2022 IR 159), which use the G0 code area.
      Japan's choice of G0 is due to the adoption of an encoding method
      based on "ISO-2022-JP". ISO-2022-JP, the most familiar encoding
      method in Japan, and uses only the G0 code area. In Korea, most
      operating systems adopt an encoding method that invokes the Hangul
      character set (KS X 1001) in the G1 code area. So, the difference
      between code areas of Korean and Japanese character originates in
      convention, not a technical problem. Invocation of multi-byte
      character sets to the G1 area does not change the current DICOM
      normative requirements.

.. _sect_I.2:

Example of Person Name Value Representation in the Korean Language
------------------------------------------------------------------

Person names in the Korean language may be written in Hangul (phonetic
characters), Hanja (ideographic characters), or Latin (alphabetic
characters). The three component groups should be written in the order
of alphabetic, ideographic, and phonetic (see
`table_title <#table_6.2-1>`__).

Specific Character Set:

-  (0008,0005) \\ISO 2022 IR 149

Character String:

-  *Hong^Gildong=洪^吉洞=홍^길동*

-  *Hong^Gildong= ESC 02/04 02/09 04/03 洪 ^ ESC 02/04 02/09 04/03 吉洞
   = ESC 02/04 02/09 04/03 홍 ^ ESC 02/04 02/09 04/03 길동*

Encoded representation:

-  ``04/08 06/15 06/14 06/07 05/14 04/07 06/09 06/12 06/04 06/15 06/14 06/07 03/13 01/11 02/04 02/09 04/03 15/11 15/03 05/14 01/11 02/04 02/09 04/03 13/01 12/14 13/04 13/07 03/13 01/11 02/04 02/09 04/03 12/08 10/11 05/14 01/11 02/04 02/09 04/03 11/01 14/06 11/05 11/15``

An example of what might be displayed or printed by an ASCII based
machine that displays or prints the Control Character ESC (01/11) using
\\033:

-  *``Hong^Gildong=\033$) C\373\363^\033$)C\321\316\324\327=\033$)C\310\253^\033$)C\261\346\265\277``*

.. note::

   1. The multi-byte character set (ISO-IR 149) and single-byte
      character set (ISO 646) can be used intermixed without any
      explicit escape sequence after the initial escape sequence. Once
      ISO 646 has been designated to the GL area and ISO-IR 149 to the
      GR area, each character set has different code area, thus can be
      used intermixed. The decoder will check the most significant bit
      of a character to know whether it is a two byte character in the
      GR area (high bit one) or a one byte character in the GL area
      (high bit zero).

   2. In the above example of person name representation, explicit
      escape sequences precede each Hangul and Hanja string. These
      escape sequences are to meet the requirements of the code
      extension technique that specifies a switch to the Default
      Character Repertoire before delimiters. In the previous example,
      it is assumed that the Default Character Repertoire (ISO-646) is
      invoked to G0 code area and no character set to G1 area after
      delimiters ("^" and "=" signs). See
      `Requirements <#sect_6.1.2.5.3>`__.

.. _sect_I.3:

Example of Long Text Value Representation in the Korean Language Without Explicit Escape Sequences Between Character Sets
-------------------------------------------------------------------------------------------------------------------------

Hangul (ISO IR 149) and ASCII (ISO 646) character sets can be used
intermingled without explicit escape sequences between them. The Hangul
character set ISO IR 149 is invoked to the G1 area, so this invocation
doesn't affect the G0 area to which the ASCII character set has been
invoked. The following is an example of a Long Text value representation
that includes ASCII and Hangul character set.

Specific Character Set:

-  (0008,0005) \\ISO 2022 IR 149

Character String:

-  The first line includes *한글*.

   The second line includes *한글*, too.

   The third line

Encoded String:

-  ESC 02/04 02/09 04/03 The first line includes *한글*.

   ESC 02/04 02/09 04/03 The second line includes *한글*, too.

   The third line

Once having invoked the ISO IR 149 character set to G1 area by the
escape sequence in the head of line, one can use Hangul and ASCII
intermixed in that line.

.. table:: Character Sets and Escape Sequences Used in the Examples

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
   | K     | F     | Value | I     |       |       | GL    | ISO   |
   | orean | irst: | 1:    | SO-IR |       |       |       | 646:  |
   |       |       |       | 6     |       |       |       |       |
   |       | S     | none  |       |       |       |       |       |
   |       | ingle |       |       |       |       |       |       |
   |       | -byte |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+
   |       | Se    | Value | I     |       |       | GL    | ISO   |
   |       | cond: | 1:    | SO-IR |       |       |       | 646:  |
   |       |       |       | 6     |       |       |       |       |
   |       | I     | none  |       |       |       |       | For   |
   |       | deogr |       |       |       |       |       | delim |
   |       | aphic |       |       |       |       |       | iters |
   +-------+-------+-------+-------+-------+-------+-------+-------+
   |       |       | Value | I     | ISO   | ESC   | GR    | KS X  |
   |       |       | 2:    | SO-IR | 2022  | 02/04 |       | 1001: |
   |       |       |       | 149   |       | 02/09 |       |       |
   |       |       | ISO   |       |       | 04/03 |       | H     |
   |       |       | 2022  |       |       |       |       | angul |
   |       |       | IR    |       |       |       |       | and   |
   |       |       | 149   |       |       |       |       | Hanja |
   +-------+-------+-------+-------+-------+-------+-------+-------+
   |       | T     | Value | I     |       |       | GL    | ISO   |
   |       | hird: | 1:    | SO-IR |       |       |       | 646:  |
   |       |       |       | 6     |       |       |       |       |
   |       | Pho   | none  |       |       |       |       | For   |
   |       | netic |       |       |       |       |       | delim |
   |       |       |       |       |       |       |       | iters |
   +-------+-------+-------+-------+-------+-------+-------+-------+
   |       |       | Value | I     | ISO   | ESC   | GR    | KS X  |
   |       |       | 2:    | SO-IR | 2022  | 02/04 |       | 1001: |
   |       |       |       | 149   |       | 02/09 |       |       |
   |       |       | ISO   |       |       | 04/03 |       | H     |
   |       |       | 2022  |       |       |       |       | angul |
   |       |       | IR    |       |       |       |       | and   |
   |       |       | 149   |       |       |       |       | Hanja |
   +-------+-------+-------+-------+-------+-------+-------+-------+

