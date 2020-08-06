.. _chapter_F:

DICOM UL Encoding Rules for Application Contexts, Abstract Syntaxes, Transfer Syntaxes (Normative)
==================================================================================================

.. _sect_F.1:

Encoding Rules
--------------

Application Context Names, Abstract Syntax Names, Transfer Syntax Names,
and Service Class UIDs are OSI Object Identifiers in a numeric form as
defined by ISO 8824. The encoding of these names in the DICOM UL
protocol is specified in this Annex.

Each component of a Name or UID is encoded as an ISO 646:1990-Basic G0
Set Numeric String of bytes (characters 0-9). Leading 0's of each
component are not significant and shall not be sent. Components shall
not be padded. Components shall be separated by the character "." (2EH).
"Null" components (no numeric value between two separators) shall not
exist. Components with the value zero (0) shall be encoded as
(nnn.0.ppp). No separator nor padding shall be present before the first
digit of the first component or after the last digit of the last
component.

.. note::

   1. The string "1.2.840.123456.0.21.4" encoded as an ISO
      646:1990-Basic G0 Set character string conveys the following UID
      or Name with the following sequence of Object Identifier
      components: { (1), (2), (840), (123456), (0), (21), (4) }.

   2. The above rules have been made to simplify performing the
      comparison of UIDs.

DICOM Application Context Names (root plus suffix) shall not exceed 64
total characters (digits and separators between components).

DICOM Abstract and Transfer Syntax Names (root plus suffix) shall not
exceed 64 total characters (digits and separators between components).

