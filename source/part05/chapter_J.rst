.. _chapter_J:

Character Sets and Person Name Value Representation using Unicode UTF-8, GB18030 and GBK (Informative)
======================================================================================================

The Unicode UTF-8 character set and the GB18030 character set may be
used for multiple languages. Some of these languages may also be encoded
using other character sets that are defined elsewhere in the DICOM
Standard. As Unicode UTF-8 and GB18030 encodings do not allow ISO 2022
character set replacement, these must be used for all strings in a
single SOP Instance. This may have implications for the character set
selected for the encoding of the SOP Instance.

Since the GBK character set is fully code point compatible to the larger
character set of GB 18030, and the specific examples of GB 18030
encoding this in Annex (J.3 and J.4) include only the Chinese characters
falling in the common coding area between the two standards, these
examples are used to demonstrate the person name and text encoding in
both standards. Examples specific to GBK are not necessary.

.. _sect_J.1:

Example of Person Name Value Representation in the Chinese Language Using Unicode
---------------------------------------------------------------------------------

Person names in the Chinese language may be written in Hanzi
(ideographic characters), and/or Latin (alphabetic characters). The
Latin representation may be derived using pinyin or another Romanization
method, or may be a chosen "westernized" name. The two component groups
should be written in the order of alphabetic, then ideographic; the
phonetic component group is typically not used (see
`table_title <#table_6.2-1>`__). In this example the traditional script
is used.

.. note::

   1. Some healthcare information systems may encode a "westernized"
      name with other patient aliases in a separate attribute, e.g.,
      Other Patient Names (0010,1091).

   2. Some environments using Chinese language may use the third name
      component, e.g., for the Yi or Mongolian script, with or without
      the first name component. This would be similar to the Japanese
      and Korean name component usage.

In the example below, the Specific Character Set attribute (0008,0005)
would contain:

-  (0008,0005) ISO_IR 192

Text string:

-  *Wang^XiaoDong=王^小東=*

Character encoded representation is:

-  ``0x57 0x61 0x6e 0x67 0x5e 0x58 0x69 0x61 0x6f 0x44 0x6f 0x6e 0x67 0x3d``
   *``0xe7 0x8e 0x8b``* ``0x5e`` *``0xe5 0xb0 0x8f 0xe6 0x9d 0xb1``*
   ``0x3d``

.. note::

   The underlined bytes correspond to the Unicode code points for the
   Chinese characters:

   -  *王* (U+738B)

   -  *小* (U+5C0F)

   -  *東* (U+6771)

   and the corresponding UTF-8 encodings are:

   -  UTF-8 (U+738b) = 0xe7 0x8e 0x8b

   -  UTF-8 (U+5c0f U+6771) = 0xe5 0xb0 0x8f 0xe6 0x9d 0xb1

.. _sect_J.2:

Example of Long Text Value Representation in the Chinese Language Using Unicode
-------------------------------------------------------------------------------

The following is an example of a Long Text value representation that
includes ASCII and ISO 10646 character set.

Specific Character Set:

-  (0008,0005) ISO_IR 192

Text string:

-  The first line includes *中文*.

   The second line includes *中文*, too.

   The third line.

Character encoded representation is:

-  ``0x54 0x68 0x65 0x20 0x66 0x69 0x72 0x73 0x74 0x20 0x6c 0x69 0x6e 0x65 0x20 0x69 0x6e 0x63 0x6c 0x75 0x64 0x65 0x73``
   *``0xe4 0xb8 0xad 0xe6 0x96 0x87``*
   ``0x2e 0x0d 0x0a 0x54 0x68 0x65 0x20 0x73 0x65 0x63 0x6f 0x6e 0x64 0x20 0x6c 0x69 0x6e 0x65 0x20 0x69 0x6e 0x63 0x6c 0x75 0x64 0x65 0x73``
   *``0xe4 0xb8 0xad 0xe6 0x96 0x87``*
   ``0x2c 0x20 0x74 0x6f 0x6f 0x2e 0x0d 0x0a 0x54 0x68 0x65 0x20 0x74 0x68 0x69 0x72 0x64 0x20 0x6c 0x69 0x6e 0x65 0x2e 0x0d 0x0a``

.. note::

   The underlined byte codes correspond to the Unicode code points for
   the Chinese characters:

   -  *中* (U+4E2D) 0xe4 0xb8 0xad

   -  *文* (U+6587) 0xe6 0x96 0x87

.. _sect_J.3:

Example of Person Name Value Representation in the Chinese Language Using GB18030
---------------------------------------------------------------------------------

Person names in the Chinese language may be written in Hanzi
(ideographic characters), and/or Latin (alphabetic characters). The
Latin representation may be derived using pinyin or another Romanization
method, or may be a chosen "westernized" name. The two component groups
should be written in the order of alphabetic, then ideographic; the
phonetic component group is typically not used (see
`table_title <#table_6.2-1>`__). In this example the simplified script
is used.

.. note::

   See notes to `Example of Person Name Value Representation in the
   Chinese Language Using Unicode <#sect_J.1>`__.

In the example below, the Specific Character Set attribute (0008,0005)
would contain:

-  (0008,0005) GB18030

Text string:

-  *Wang^XiaoDong=王^小东=*

Character encoded representation is:

-  ``0x57 0x61 0x6e 0x67 0x5e 0x58 0x69 0x61 0x6f 0x44 0x6f 0x6e 0x67 0x3d 0xcd 0xf5 0x5e 0xd0 0xa1 0xb6 0xab 0x3d``

.. note::

   The GB18030 encodings for the Chinese characters used here are:

   -  *王* (CDF5 in GB18030)

   -  *小* (D0A1 in GB18030)

   -  *东* (B6AB in GB18030)

.. _sect_J.4:

Example of Long Text Value Representation in the Chinese Language Using GB18030
-------------------------------------------------------------------------------

The following is an example of a Long Text value representation that
includes ASCII and GB18030 character set.

Specific Character Set:

-  (0008,0005) GB18030

Text string:

-  The first line includes *中文*.

   The second line includes *中文*, too.

   The third line.

Character encoded representation is:

-  ``0x54 0x68 0x65 0x20 0x66 0x69 0x72 0x73 0x74 0x20 0x6c 0x69 0x6e 0x65 0x20 0x69 0x6e 0x63 0x6c 0x75 0x64 0x65 0x73``
   *``0xd6 0xd0 0xce 0xc4``*
   ``0x2e 0x0d 0x0a 0x54 0x68 0x65 0x20 0x73 0x65 0x63 0x6f 0x6e 0x64 0x20 0x6c 0x69 0x6e 0x65 0x20 0x69 0x6e 0x63 0x6c 0x75 0x64 0x65 0x73``
   *``0xd6 0xd0 0xce 0xc4``*
   ``0x2c 0x20 0x74 0x6f 0x6f 0x2e 0x0d 0x0a 0x54 0x68 0x65 0x20 0x74 0x68 0x69 0x72 0x64 0x20 0x6c 0x69 0x6e 0x65 0x2e 0x0d 0x0a``

.. note::

   The underlined byte codes correspond to the GB18030 encodings for the
   Chinese characters used:

   -  *中* (D6D0 in GB18030)

   -  *文* (CEC4 in GB18030)

.. _sect_J.5:

Person Name Value Representation in Other Languages Using Unicode
-----------------------------------------------------------------

Person names in many languages may be written in a local (non-Latin)
script, as well as in a transliteration to a Latin script
(Romanization). Healthcare information systems in those environments may
support one or both name formats. Local scripts may be encoded using
Unicode in UTF-8.

For the purpose of exchange in DICOM, there are three typical uses of
name component groups using Unicode in UTF-8:

1. Names in a Latin script may be encoded in the first (alphabetic)
   component group, and names in a local script (alphabet, abugida, or
   syllabary) in the third (phonetic) component group (see
   `table_title <#table_6.2-1>`__). The second (ideographic) component
   group is null. This is the preferred use for cross-enterprise or
   international communication.

2. Where the local script historically has a single byte character set
   defined for Specific Character Set (0008,0005), i.e., Cyrillic,
   Arabic, Greek, Hebrew, Thai, and the various versions of Latin, only
   the first name component group might be used. Encoding may be in
   Unicode in UTF-8, as described in this Annex, as an equivalent for
   use of that defined single byte character set in the first name
   component group (see note 1).

3. Names in the local script may be encoded in the first component
   group, and names in a Latin script in the third component group, both
   encoded in Unicode in UTF-8.

.. note::

   1. A previous edition of DICOM required the first name component
      group to use a single byte character set (see PS3.5-2008). Unicode
      in UTF-8 may now be used in that component group simply as a
      matter of a different character set encoding, but with the same
      application use of that component group.

   2. Healthcare information systems will use specific scripts in one,
      two, or three of the Person Name component groups in accordance
      with local policy. Conformant DICOM Application Entities that
      receive name attributes must accept multiple name component
      groups. An Application Entity that is configurable to allow the
      use of local script for names in either the first or the third
      component group, and a transliteration script in the other, would
      support all these typical representations.

   3. The transliteration (from a local script) may be a non-Latin
      script, e.g., Cyrillic. The same principles apply, and the
      Cyrillized name might be encoded in the first component group and
      the local script (which may in fact be a Latin-derived script) in
      the third component group.

