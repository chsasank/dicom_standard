.. _chapter_7:

DCMR Context Group Specifications
=================================

Context Groups specify Value Set restrictions for Code Value (0008,0100)
(or Long Code Value (0008,0119) or URN Code Value (0008,0120)) and Code
Meaning (0008,0104) of Code Sequence Attributes for given functional or
operational contexts. This Section specifies the semantics of DCMR
Context Group Tables.

.. _sect_7.1:

Context Group Table Field Definition
------------------------------------

Context Groups are described using tables of the following form
(optional columns are shown with italic column titles):

**Resources:**
   HTML \| FHIR JSON \| FHIR XML \| IHE SVS XML

**Type:**
   **(Non-) Extensible**

**Version:**
   **<yyyymmdd>**

**UID:**
   **1.2.840.10008.6.1.uuuu**

.. table:: <Context Group Name>

   +----------+----------+----------+----------+----------+-------+
   | Coding   | *Coding  | Code     | Code     | *<R      | Units |
   | Scheme   | Scheme   | Value    | Meaning  | eference |       |
   | De       | Version* |          |          | Term     |       |
   | signator |          |          |          | inology> |       |
   |          |          |          |          | Eq       |       |
   |          |          |          |          | uivalent |       |
   |          |          |          |          | Value*   |       |
   +==========+==========+==========+==========+==========+=======+
   | ...      | ...      | ...      | ...      | ...      | ...   |
   +----------+----------+----------+----------+----------+-------+
   | ...      | ...      | ...      | ...      | ...      | ...   |
   +----------+----------+----------+----------+----------+-------+

A row of a Context Group table specifies one coded concept. Each Context
Group table is named by a title and identified by a CID number and
version.

The columns of the tables consist of:

-  Coding Scheme Designator: the value of Coding Scheme Designator
   (0008,0102)

-  Code Value: the value of Code Value (0008,0100) or Long Code Value
   (0008,0119) or URN Code Value (0008,0120)

-  Coding Meaning: the value of Code Meaning (0008,0104)

In those cases where it is necessary, Coding Scheme Version (the value
of Coding Scheme Version (0008,0103)) may also be specified. This column
may be absent if Coding Scheme Version is not required for any of the
coded concepts in the Context Group.

The value specified in the Code Meaning field is an acceptable value for
the specified code value, but does not preclude the use of other
synonymous text in the same or other language.

.. note::

   1. Some coding schemes do not specify the equivalent of a Code
      Meaning.

   2. Capitalization in the Code Meaning is generally not significant,
      except for abbreviations used in units of measurement prefixes
      (e.g., “ml” milliliter vs. “Ml” megaliter, or “pV” picovolt vs.
      “PV” petavolt).

If further description of the concept represented by the code is
required in the DCMR (rather than referring to an external coding
scheme), it is included in a separate table.

Optional columns may provide an informative mapping from the coded
concepts of the Context Group to a reference terminology specified in
the column heading. Typical reference terminologies include SNOMED CT
and UMLS.

An optional column may provide a normative baseline or defined set of
units to use for numeric measurements using the concept, either as a
single term (e.g., DT ({ratio}, UCUM, "ratio")), a list of such terms,
or a reference to a Context Group (e.g., DCID 7277 "Units of Diffusion
Rate Area Over Time").

A Context Group may alternatively be defined by narrative reference to
an externally defined coding scheme.

.. note::

   See for instance `Units of Measurement <#sect_CID_82>`__.

.. _sect_7.2:

Special Conventions for Context Group Tables
--------------------------------------------

.. _sect_7.2.1:

Include Context Group
~~~~~~~~~~~~~~~~~~~~~

The 'Include Context Group' macro is a concise mechanism for including
(by-reference) all of the rows of a specified Context Group in the
invoking Context Group, effectively substituting the specified Context
Group for the row where the macro is invoked. If an 'Include Context
Group' is specified, it shall be specified in the Concept Name column of
a Context Group Table. Table 7.2.1-1 specifies the syntax of the
'Include Context Group macro. Inclusion may be nested, in that included
Context Groups may themselves include other Context Groups. This gives
rise to the possibility of circular inclusion and multiple inclusion, in
which case the Context Group shall consist of the transitive closure of
the set of all coded concepts within the included Context Groups.

.. note::

   For example, it is reasonable to have the following definitions for
   context groups:

   -  Context ID 1, includes Context IDs 2 and 3

   -  Context ID 2, includes Context IDs 4 and 5

   -  Context ID 3, includes Context IDs 5 and 6

   -  Context ID 4 contains a, b, c

   -  Context ID 5 contains e, f, g

   -  Context ID 6 contains a, h, i

   The contents of Context ID 1 will be a, b, c, e, f, g, h, i.

.. table:: Include Context Group Macro

   ======================== ========== ============
   Coding Scheme Designator Code Value Code Meaning
   ======================== ========== ============
   …                        …          …
   *Include CID nnn*                   
   …                        …          …
   ======================== ========== ============

.. _sect_7.2.2:

Units of Measurement
~~~~~~~~~~~~~~~~~~~~

Context Group 82 is defined to include all units of measurement relevant
to DICOM IODs. In the past it was envisaged that an extensible list of
pre-coordinated codes would be included in the mapping resource.

DICOM has now adopted the Unified Codes for Units of Measurement (UCUM)
standard for all units of measurement. This coding scheme allows for the
"construction" of pre-coordinated codes from atomic components.

The specialization of the UCUM standard as it is used in DICOM involves
the following rules:

-  the Coding Scheme Designator is specified as "UCUM"

-  the version of UCUM from which a code is constructed is not required,
   as it is not needed to resolve ambiguity in the Code Value or Code
   Meaning; however, there is no restriction on the version being
   specified in Coding Scheme Version

-  the Code Value will be constructed from UCUM and make use of the
   "case-sensitive" form of UCUM code (e.g., "ml/s")

-  the Code Meaning for other than UCUM unity may be one of the
   following:

   -  the "print" value specified in UCUM (e.g., "mmHg" for Code Value
      mm[Hg])

   -  the same string as sent in the Code Value (e.g., "ml/s")

   -  constructed from the "names" of individual components using the
      Americanized form of name (e.g., "milliliters/second")

   -  constructed from the "names" of individual components using the
      European form of name (e.g., "*millilitres*/second")

-  In the case of UCUM unity ("1", or curly braces expression) it is
   forbidden to use "1" as a Code Meaning. `English Code Meanings of
   Selected Codes (Normative) <#chapter_G>`__ provides Code Meanings for
   a Code Value (0008,0100) of 1. A Template or Context Group may
   constrain the Code Meaning according to the following rules:

   -  UCUM default unit 1 shall use one of the Code Meaning synonyms
      specified in `English Code Meanings of Selected Codes
      (Normative) <#chapter_G>`__

   -  ratios of identically dimensioned values may use ({ratio}, UCUM,
      "ratio")

   -  unitless numeric scores may use ({M:N}, UCUM, "range: M:N") to
      specify the minimum and maximum value, for example, ({0:10}, UCUM,
      "range: 0:10")

   -  counts using UCUM annotation shall always use the text within the
      curly braces as the Code Meaning, for example, ({masses}, UCUM,
      "masses")

   -  compositions of a curly braces expression with other UCUM values
      may use a conventional clinical representation, for example,
      ({H.B.}/min, UCUM, "BPM")

The UCUM standard states that the preferred display values for codes deg
(degrees of plane angle) and Cel (degrees Celsius) are "°" and "°C".
However, the character ° does not have a representation in the DICOM
default character set (ASCII, ISO-IR 6). The Code Meaning specified in
this Part therefore uses "deg" and "C". SOP Instances that specify a
Specific Character Set that allows the character ° may use Code Meanings
"°" and "°C".

.. note::

   1. Code Meaning "C" formally conflicts with the Code Meaning for
      Coulomb. In the context of DICOM use, the possibility of confusion
      to a user based on the display of the Code Meaning is considered
      remote, as there is little use of Coulomb in imaging, and the
      context of the displayed item Concept Name would resolve between
      temperature and electric charge. Automated processing based on the
      Code Values should not face an issue as the Code Values differ.

   2. The character ° has Unicode code point U+00B0, and is represented
      as 0xB0 in ISO-IR 100 (Latin-1), ISO-IR 101 (Latin-2), ISO-IR 109
      (Latin-3), ISO-IR 110 (Latin-4), ISO-IR 126 (Greek), ISO-IR 138
      (Hebrew), and ISO-IR 148 (Latin-5). It is not encodable in ISO-IR
      13 (Katakana), ISO-IR 144 (Cyrillic), ISO-IR 127 (Arabic), or
      ISO-IR 166 (Thai).

.. _sect_7.2.3:

Extension of Context Groups
~~~~~~~~~~~~~~~~~~~~~~~~~~~

An Application may extend an Extensible Context Group by adding terms
for new concepts. Applications may not substitute other terms of the
same concept in the Context Group. Applications may not add a term that
means "unspecified" or "missing" or "unknown" similar; if such a concept
is intended to be permitted then the Standard will include it in the
Context Group already. Such extension may be made without a change in
Context Group Identifier, but with the specification of Context Group
Extensions (see ).

Non-extensible Context Groups shall not be modified in an Application.

.. note::

   The set of concepts in either an Extensible or a Non-extensible
   Context Group may be changed in subsequent editions of the Standard,
   in accordance with the procedures of the DICOM Standards Committee.

