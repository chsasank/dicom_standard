.. _chapter_8:

Encoding of Coded Entry Data
============================

The primary method of incorporating coded entry data in DICOM IODs is
the Code Sequence Attribute. Code Sequence Attributes are encoded as a
Sequence of Items using a Macro that is described in this section. These
Attributes typically include the string "Code Sequence" in the Attribute
Name. Their purpose is to encode terms by using codes from coding
schemes.

.. note::

   In this Standard, Code Sequence Attributes are defined for a variety
   of concepts, for example: Primary Anatomic Structure Sequence
   (0008,2228) and other Attributes to describe anatomy; and
   Intervention Drug Code Sequence (0018,0029), to document
   administration of drugs that have special significance in Imaging
   Procedures.

Each Item of a Code Sequence Attribute contains the triplet of Coding
Scheme Designator (0008,0102), the Code Value (0008,0100) (or Long Code
Value (0008,0119) or URN Code Value (0008,0120)), and Code Meaning
(0008,0104). Other optional and conditional Attributes may also be
present.

For any particular Code Sequence Attributes, the range of codes that may
be used for that Attribute (the Value Set) may be suggested or
constrained by specification of a Context Group. The Module or Template
in which the Attribute is used will specify whether or not the context
group is baseline or defined. A Baseline Context Group lists codes for
terms that are suggested and may be used, but are not required to be
used. A Defined Context Group lists codes for terms that shall be used
if the term is used.

Context Groups are defined in a Mapping Resource, such as the DICOM
Content Mapping Resource (DCMR) specified in . Context Groups consist of
lists of contextually related coded concepts, including Code Value
(0008,0100) (or Long Code Value (0008,0119) or URN Code Value
(0008,0120)) and Coding Scheme Designator (0008,0102). Each concept is
unique within the Context Group and identified by its Code Value
(0008,0100) (or Long Code Value (0008,0119) or URN Code Value
(0008,0120)) and Coding Scheme Designator (0008,0102). The Context Group
specification identifies whether it is extensible, i.e., whether it may
be modified in an Application to use additional terms (see ). Whether a
Context Group is used as a Baseline or Defined Context Group is defined
not in the mapping resource, but rather in the Template or Module in
which the Code Sequence Attribute is used.

Context Groups are identified by labels referred to as Context
Identifiers (CID). Formally, the Context Identifier specifies the
context of use, not the specific list of coded values selected for that
context of use in the Context Group. The set of values specified in the
Standard for a particular context may change over time, and set of
values used by an Application Entity for a particular context may
include a local or private extension beyond the Standard value set.

.. note::

   1. A specific set of coded values used by an Application Entity is
      therefore identified by the Mapping Resource Identifier, plus the
      Context Identifier, plus the Context Group Version, plus the
      identifiers for any private extension.

   2. The use by an Application Entity of coded terms not in the
      Standard specified Context Group does not require the explicit
      identification of a private extension. The Application Entity is
      then the implicit source of the extension.

   3. For the purpose of harmonization with HL7 vocabulary concepts,
      Context Groups are equivalent to HL7 Value Sets.

.. _sect_8.1:

Code Value
----------

Code Value (0008,0100) is an identifier that is unambiguous within the
Coding Scheme denoted by Coding Scheme Designator (0008,0102) and Coding
Scheme Version (0008,0103).

The Long Code Value (0008,0119) or URN Code Value (0008,0120) is only
used for codes that exceed the 16 character size limit of Code Value
(0008,0100). If the code value length exceeds 16, the Code Value
(0008,0100) shall not be present. If the code value length is 16
characters or less, the Code Value (0008,0100) shall contain the code
and neither Long Code Value (0008,0119) nor URN Code Value (0008,0120)
shall be present. The URN Code Value (0008,0120) shall be used for codes
that are represented using URN or URL notation. The Long Code Value
(0008,0119) shall be used for codes that are represented using other
notations and that exceed 16 characters in length.

.. note::

   The Code Value is typically not a natural language string, e.g.,
   "76752008".

.. _sect_8.2:

Coding Scheme Designator and Coding Scheme Version
--------------------------------------------------

The Attribute Coding Scheme Designator (0008,0102) identifies the coding
scheme in which the code for a term is defined. Standard coding scheme
designators used in DICOM information interchange are listed in . Other
coding scheme designators, for both private and public coding schemes,
may be used, in accordance with . Further identification of the coding
scheme designators used in a SOP Instance may be provided in the Coding
Scheme Identification Sequence (0008,0110) (see `SOP Common
Module <#sect_C.12.1>`__).

.. note::

   1. Typical coding schemes used in DICOM include "DCM" for DICOM
      defined codes, "SCT" for SNOMED CT, and "LN" for LOINC. See .

   2. Coding scheme designators beginning with "99" and the coding
      scheme designator "L" are defined in HL7 V2 to be private or local
      coding schemes.

   3. Most IODs that define the use of coded terms provide for the use
      of private codes and coding schemes through replacement of
      Baseline Context Groups or extension of Defined Context Groups.
      Systems supporting such private code use must provide a mechanism
      for the configuration of sets of Coding Scheme Designator
      (0008,0102), Code Value (0008,0100) (or Long Code Value
      (0008,0119) or URN Code Value (0008,0120)), and Code Meaning
      (0008,0104) to support interoperation of the private codes with
      other systems.

   4. It is highly recommended that local or non-standard coding schemes
      be identified in the Coding Scheme Identification Sequence
      (0008,0110). Documents or machine readable representations of the
      coding scheme (e.g., CSV or OWL files) can be linked to via a
      Coding Scheme URL (0008,010E). For appropriate values, see .

   5. URN and URL codes usually lack a Coding Scheme Designator
      (0008,0102).

The Attribute Coding Scheme Version (0008,0103) may be used to identify
the version of a coding scheme if necessary to resolve ambiguity in Code
Value (0008,0100), Long Code Value (0008,0119) or URN Code Value
(0008,0120). Coding Scheme Version (0008,0103) is not required for
backward-compatible revisions of a coding scheme, as the Coding Scheme
Designator (0008,0102) identifies the coding scheme as a whole as
currently published by the responsible organization.

.. note::

   1. See for a discussion of SNOMED Coding Scheme Designators 99SDM,
      SNM3, SRT and SCT.

   2. ICD-10, for example, is not a backward-compatible revision of
      ICD-9, and hence it has a different Coding Scheme Designator, not
      simply a different Coding Scheme Version.

.. _sect_8.3:

Code Meaning
------------

Code Meaning (0008,0104) is text that has meaning to a human and conveys
the meaning of the term defined by the combination of Code Value
(0008,0100) (or Long Code Value (0008,0119) or URN Code Value
(0008,0120)), and Coding Scheme Designator (0008,0102). Though such a
meaning can be "looked up" in the dictionary for the coding scheme, it
is encoded for the convenience of applications that do not have access
to such a dictionary.

It should be noted that for a particular Coding Scheme Designator
(0008,0102) and Code Value (0008,0100) or Long Code Value (0008,0119),
or URN Code Value (0008,0120), several alternative values for Code
Meaning (0008,0104) may be defined. These may be synonyms in the same
language or translations of the Coding Scheme into other languages.
Hence the value of Code Meaning (0008,0104) shall never be used as a
key, index or decision value, rather the combination of Coding Scheme
Designator (0008,0102) and Code Value (0008,0100), Long Code Value
(0008,0119), or URN Code Value (0008,0120) may be used. Code Meaning
(0008,0104) is a purely annotative, descriptive Attribute.

This does not imply that Code Meaning (0008,0104) can be filled with
arbitrary free text. Available values from the Coding Scheme or
translation in the chosen language shall be used.

.. _sect_8.4:

Mapping Resource
----------------

The value of Mapping Resource (0008,0105) denotes the
message/terminology Mapping Resource that specifies the Context Group
that specifies the Value Set. The Defined Terms for the value of Mapping
Resource (0008,0105) shall be:

DCMR
   DICOM Content Mapping Resource

SDM
   SNOMED DICOM Microglossary (Retired)

specifies the DICOM Content Mapping Resource (DCMR).

.. note::

   Unless otherwise specified, the DCMR is the source of all Context
   Groups and Templates specified in this Standard.

Mapping Resources may be uniquely identified by Mapping Resource UID
(0008,0118).

Private Mapping Resources (those not listed amongst the Defined Terms in
this section), may be identified by the prefix "99".

Mapping Resource Name (0008,0122) may contain the name of the Mapping
Resource. The value may e.g., denote the Institution or organization
that has specified the Value Set.

.. _sect_8.5:

Context Group Version
---------------------

Context Group Version (0008,0106) conveys the version of the Context
Group identified by Context Identifier (0008,010F). This Attribute uses
VR DT, but for Context Groups defined in the precision of Context Group
Version is limited to the day, and the time zone offset is not used.

.. _sect_8.6:

Context Identifier and Context UID
----------------------------------

The value of Context Identifier (0008,010F) identifies the Context Group
defined by Mapping Resource (0008,0105) from which the values of Code
Value (0008,0100) (or Long Code Value (0008,0119) or URN Code Value
(0008,0120)) and Code Meaning (0008,0104) were selected, or to which
Code Value (0008,0100) (or Long Code Value (0008,0119) or URN Code Value
(0008,0120)) and Code Meaning (0008,0104) have been added as a private
Context Group extension (see `Context Group Extensions <#sect_8.7>`__).
The Context Identifier Attribute uses VR CS, and for Context Groups
defined in the value shall be the Context Group Identifier as a string
of digits without leading zeros, and does not include the string "CID".

The value of Context UID (0008,0117) uniquely identifies the Context
Group. See .

.. note::

   Privately defined Context Groups may be identified by Context
   Identifier and Mapping Resource.

.. _sect_8.7:

Context Group Extensions
------------------------

Context Group Extension Flag (0008,010B) may be used to designate a pair
of Code Value (0008,0100) (or Long Code Value (0008,0119) or URN Code
Value (0008,0120)) and Code Meaning (0008,0104) as a selection from a
private extension of a Context Group. If the Context Group Extension
Flag is present, and has a value of "Y", Context Group Extension Creator
UID (0008,010D) shall be used to identify the person or organization who
created the extension to the Context Group. Context Group Local Version
(0008,0107) conveys an implementation-specific private version DateTime
of a Context Group that contains private extensions

.. note::

   1. These Attributes provide the means for implementations to extend
      code sets conveniently, while preserving referential integrity
      with respect to the original Context Group Version.

   2. The locally-defined (private) value of Context Group Local Version
      (0008,0107) typically would be a more recent date than the
      standard value of Context Group Version (0008,0106) specified in
      the standard message/terminology Mapping Resource that defines the
      Context Group.

.. _sect_8.8:

Standard Attribute Sets for Code Sequence Attributes
----------------------------------------------------

`table_title <#table_8.8-1>`__ specifies the default set of Attributes
encapsulated in the Items of Code Sequence Attributes. These Attributes
comprise the Code Sequence Macro.

.. note::

   The instruction "*Include*\ `table_title <#table_8.8-1>`__" may be
   used in an Information Object Definition as a concise way to indicate
   that the Attributes of `table_title <#table_8.8-1>`__ are included in
   the specification of the Attribute Set of a Sequence of Items.
   Additional constraints on the Code Sequence Data Element (such as a
   Context Group that defines the value set) may be appended to the
   "*Include*\ `table_title <#table_8.8-1>`__" instruction.

The default specifications of this Section are overridden within the
scope of a Sequence Item or Code Sequence Attribute or IOD by
corresponding specifications defined within the scope of that Sequence
Item or Code Sequence Attribute or IOD. Additional Attributes may also
be specified by the instantiation of the Macro.

The Basic Coded Entry Attributes fully define a Coded Entry. If it is
desired to convey the list from which a code has been chosen, then the
optional Enhanced Encoding Mode Attributes may also be present.

.. table:: Basic Code Sequence Macro Attributes

   +----------------------+-------------+------+----------------------+
   | Attribute Name       | Tag         | Type | Attribute            |
   |                      |             |      | Description          |
   +======================+=============+======+======================+
   | *BASIC CODED ENTRY   |             |      |                      |
   | ATTRIBUTES*          |             |      |                      |
   +----------------------+-------------+------+----------------------+
   | Code Value           | (0008,0100) | 1C   | The identifier of    |
   |                      |             |      | the Coded Entry.     |
   |                      |             |      |                      |
   |                      |             |      | See `Code            |
   |                      |             |      | V                    |
   |                      |             |      | alue <#sect_8.1>`__. |
   |                      |             |      |                      |
   |                      |             |      | Shall be present if  |
   |                      |             |      | the code value       |
   |                      |             |      | length is 16         |
   |                      |             |      | characters or less,  |
   |                      |             |      | and the code value   |
   |                      |             |      | is not a URN or URL. |
   +----------------------+-------------+------+----------------------+
   | Coding Scheme        | (0008,0102) | 1C   | The identifier of    |
   | Designator           |             |      | the coding scheme in |
   |                      |             |      | which the Coded      |
   |                      |             |      | Entry is defined.    |
   |                      |             |      |                      |
   |                      |             |      | See `Coding Scheme   |
   |                      |             |      | Designator and       |
   |                      |             |      | Coding Scheme        |
   |                      |             |      | Ver                  |
   |                      |             |      | sion <#sect_8.2>`__. |
   |                      |             |      |                      |
   |                      |             |      | Shall be present if  |
   |                      |             |      | Code Value           |
   |                      |             |      | (0008,0100) or Long  |
   |                      |             |      | Code Value           |
   |                      |             |      | (0008,0119) is       |
   |                      |             |      | present. May be      |
   |                      |             |      | present otherwise.   |
   +----------------------+-------------+------+----------------------+
   | Coding Scheme        | (0008,0103) | 1C   | An identifier of the |
   | Version              |             |      | version of the       |
   |                      |             |      | coding scheme if     |
   |                      |             |      | necessary to resolve |
   |                      |             |      | ambiguity.           |
   |                      |             |      |                      |
   |                      |             |      | See `Coding Scheme   |
   |                      |             |      | Designator and       |
   |                      |             |      | Coding Scheme        |
   |                      |             |      | Ver                  |
   |                      |             |      | sion <#sect_8.2>`__. |
   |                      |             |      | Required if the      |
   |                      |             |      | value of Coding      |
   |                      |             |      | Scheme Designator    |
   |                      |             |      | (0008,0102) is       |
   |                      |             |      | present and is not   |
   |                      |             |      | sufficient to        |
   |                      |             |      | identify the Code    |
   |                      |             |      | Value (0008,0100) or |
   |                      |             |      | Long Code Value      |
   |                      |             |      | (0008,0119)          |
   |                      |             |      | unambiguously. Shall |
   |                      |             |      | not be present if    |
   |                      |             |      | Coding Scheme        |
   |                      |             |      | Designator           |
   |                      |             |      | (0008,0102) is       |
   |                      |             |      | absent. May be       |
   |                      |             |      | present otherwise.   |
   +----------------------+-------------+------+----------------------+
   | Code Meaning         | (0008,0104) | 1    | Text that conveys    |
   |                      |             |      | the meaning of the   |
   |                      |             |      | Coded Entry.         |
   |                      |             |      |                      |
   |                      |             |      | See `Code            |
   |                      |             |      | Mea                  |
   |                      |             |      | ning <#sect_8.3>`__. |
   +----------------------+-------------+------+----------------------+
   | Long Code Value      | (0008,0119) | 1C   | The identifier of    |
   |                      |             |      | the Coded Entry.     |
   |                      |             |      |                      |
   |                      |             |      | See `Code            |
   |                      |             |      | V                    |
   |                      |             |      | alue <#sect_8.1>`__. |
   |                      |             |      |                      |
   |                      |             |      | Shall be present if  |
   |                      |             |      | Code Value           |
   |                      |             |      | (0008,0100) is not   |
   |                      |             |      | present and the Code |
   |                      |             |      | Value is not a URN   |
   |                      |             |      | or URL.              |
   +----------------------+-------------+------+----------------------+
   | URN Code Value       | (0008,0120) | 1C   | The identifier of    |
   |                      |             |      | the Coded Entry.     |
   |                      |             |      |                      |
   |                      |             |      | See `Code            |
   |                      |             |      | V                    |
   |                      |             |      | alue <#sect_8.1>`__. |
   |                      |             |      |                      |
   |                      |             |      | Shall be present if  |
   |                      |             |      | Code Value           |
   |                      |             |      | (0008,0100) is not   |
   |                      |             |      | present and the Code |
   |                      |             |      | Value is a URN or    |
   |                      |             |      | URL.                 |
   +----------------------+-------------+------+----------------------+

.. table:: Enhanced Code Sequence Macro Attributes

   +----------------------+-------------+------+----------------------+
   | Attribute Name       | Tag         | Type | Attribute            |
   |                      |             |      | Description          |
   +======================+=============+======+======================+
   | Context Identifier   | (0008,010F) | 3    | The identifier of    |
   |                      |             |      | the Context Group    |
   |                      |             |      | from which the Coded |
   |                      |             |      | Entry was selected.  |
   |                      |             |      |                      |
   |                      |             |      | See `Context         |
   |                      |             |      | Identifier and       |
   |                      |             |      | Context              |
   |                      |             |      | UID <#sect_8.6>`__.  |
   +----------------------+-------------+------+----------------------+
   | Context UID          | (0008,0117) | 3    | The unique           |
   |                      |             |      | identifier of the    |
   |                      |             |      | Context Group from   |
   |                      |             |      | which the Coded      |
   |                      |             |      | Entry was selected.  |
   |                      |             |      |                      |
   |                      |             |      | See `Context         |
   |                      |             |      | Identifier and       |
   |                      |             |      | Context              |
   |                      |             |      | UID <#sect_8.6>`__.  |
   +----------------------+-------------+------+----------------------+
   | Mapping Resource     | (0008,0105) | 1C   | The identifier of    |
   |                      |             |      | the Mapping Resource |
   |                      |             |      | that defines the     |
   |                      |             |      | Context Group from   |
   |                      |             |      | which Coded Entry    |
   |                      |             |      | was selected.        |
   |                      |             |      |                      |
   |                      |             |      | See `Mapping         |
   |                      |             |      | Reso                 |
   |                      |             |      | urce <#sect_8.4>`__. |
   |                      |             |      | Required if Context  |
   |                      |             |      | Identifier           |
   |                      |             |      | (0008,010F) is       |
   |                      |             |      | present.             |
   +----------------------+-------------+------+----------------------+
   | Mapping Resource UID | (0008,0118) | 3    | The unique           |
   |                      |             |      | identifier of the    |
   |                      |             |      | Mapping Resource     |
   |                      |             |      | that defines the     |
   |                      |             |      | Context Group from   |
   |                      |             |      | which Coded Entry    |
   |                      |             |      | was selected.        |
   |                      |             |      |                      |
   |                      |             |      | .. note::            |
   |                      |             |      |                      |
   |                      |             |      |    The unique        |
   |                      |             |      |    identifier for    |
   |                      |             |      |    the DICOM Content |
   |                      |             |      |    Mapping Resource  |
   |                      |             |      |    "DCMR" is defined |
   |                      |             |      |    in .              |
   +----------------------+-------------+------+----------------------+
   | Mapping Resource     | (0008,0122) | 3    | The name of the      |
   | Name                 |             |      | Mapping Resource     |
   |                      |             |      | that defines the     |
   |                      |             |      | Context Group from   |
   |                      |             |      | which Coded Entry    |
   |                      |             |      | was selected.        |
   |                      |             |      |                      |
   |                      |             |      | See `Mapping         |
   |                      |             |      | Reso                 |
   |                      |             |      | urce <#sect_8.4>`__. |
   +----------------------+-------------+------+----------------------+
   | Context Group        | (0008,0106) | 1C   | The identifier of    |
   | Version              |             |      | the version of the   |
   |                      |             |      | Context Group from   |
   |                      |             |      | which the Coded      |
   |                      |             |      | Entry was selected.  |
   |                      |             |      |                      |
   |                      |             |      | See `Context Group   |
   |                      |             |      | Ver                  |
   |                      |             |      | sion <#sect_8.5>`__. |
   |                      |             |      |                      |
   |                      |             |      | Required if Context  |
   |                      |             |      | Identifier           |
   |                      |             |      | (0008,010F) is       |
   |                      |             |      | present.             |
   +----------------------+-------------+------+----------------------+
   | Context Group        | (0008,010B) | 3    | Indicates whether    |
   | Extension Flag       |             |      | the triplet of Code  |
   |                      |             |      | Value (0008,0100)    |
   |                      |             |      | (or Long Code Value  |
   |                      |             |      | (0008,0119) or URN   |
   |                      |             |      | Code Value           |
   |                      |             |      | (0008,0120))/Coding  |
   |                      |             |      | Scheme Designator    |
   |                      |             |      | (0008,0102)/Code     |
   |                      |             |      | Meaning (0008,0104)  |
   |                      |             |      | is selected from a   |
   |                      |             |      | private extension of |
   |                      |             |      | the Context Group    |
   |                      |             |      | identified in        |
   |                      |             |      | Context Identifier   |
   |                      |             |      | (0008,010F). See     |
   |                      |             |      | `Context Group       |
   |                      |             |      | Extens               |
   |                      |             |      | ions <#sect_8.7>`__. |
   |                      |             |      |                      |
   |                      |             |      | Y                    |
   |                      |             |      | N                    |
   +----------------------+-------------+------+----------------------+
   | Context Group Local  | (0008,0107) | 1C   | An                   |
   | Version              |             |      | imp                  |
   |                      |             |      | lementation-specific |
   |                      |             |      | version of a Context |
   |                      |             |      | Group that contains  |
   |                      |             |      | private extensions.  |
   |                      |             |      |                      |
   |                      |             |      | See `Context Group   |
   |                      |             |      | Extens               |
   |                      |             |      | ions <#sect_8.7>`__. |
   |                      |             |      | Required if the      |
   |                      |             |      | value of Context     |
   |                      |             |      | Group Extension Flag |
   |                      |             |      | (0008,010B) is "Y".  |
   +----------------------+-------------+------+----------------------+
   | Context Group        | (0008,010D) | 1C   | Identifies the       |
   | Extension Creator    |             |      | person or            |
   | UID                  |             |      | organization who     |
   |                      |             |      | created an extension |
   |                      |             |      | to the Context       |
   |                      |             |      | Group. See `Context  |
   |                      |             |      | Group                |
   |                      |             |      | Extens               |
   |                      |             |      | ions <#sect_8.7>`__. |
   |                      |             |      |                      |
   |                      |             |      | Required if the      |
   |                      |             |      | value of Context     |
   |                      |             |      | Group Extension Flag |
   |                      |             |      | (0008,010B) is "Y".  |
   +----------------------+-------------+------+----------------------+

.. table:: Code Sequence Macro Attributes

   +----------------------+-------------+------+----------------------+
   | Attribute Name       | Tag         | Type | Attribute            |
   |                      |             |      | Description          |
   +======================+=============+======+======================+
   | *BASIC CODED ENTRY   |             |      |                      |
   | ATTRIBUTES*          |             |      |                      |
   +----------------------+-------------+------+----------------------+
   | *I                   |             |      |                      |
   | nclude*\ `table_titl |             |      |                      |
   | e <#table_8.8-1a>`__ |             |      |                      |
   +----------------------+-------------+------+----------------------+
   | Equivalent Code      | (0008,0121) | 3    | Codes that are       |
   | Sequence             |             |      | considered           |
   |                      |             |      | equivalent by the    |
   |                      |             |      | creating system.     |
   |                      |             |      |                      |
   |                      |             |      | One or more Items    |
   |                      |             |      | are permitted in     |
   |                      |             |      | this Sequence.       |
   |                      |             |      |                      |
   |                      |             |      | See `Equivalent Code |
   |                      |             |      | Sequ                 |
   |                      |             |      | ence <#sect_8.9>`__. |
   +----------------------+-------------+------+----------------------+
   | *>I                  |             |      |                      |
   | nclude*\ `table_titl |             |      |                      |
   | e <#table_8.8-1a>`__ |             |      |                      |
   +----------------------+-------------+------+----------------------+
   | *>I                  |             |      |                      |
   | nclude*\ `table_titl |             |      |                      |
   | e <#table_8.8-1b>`__ |             |      |                      |
   +----------------------+-------------+------+----------------------+
   | *ENHANCED ENCODING   |             |      |                      |
   | MODE*                |             |      |                      |
   +----------------------+-------------+------+----------------------+
   | *I                   |             |      |                      |
   | nclude*\ `table_titl |             |      |                      |
   | e <#table_8.8-1b>`__ |             |      |                      |
   +----------------------+-------------+------+----------------------+

.. _sect_8.9:

Equivalent Code Sequence
------------------------

The Equivalent Code Sequence (0008,0121) Attribute may optionally be
used to convey different codes for the same concept.

Equivalence is defined as having the same or similar meaning, and
requires that equivalent concepts do not include different aspects,
properties, features, characteristics, or parameters.

.. note::

   E.g., the SNOMED and FMA codes for a structure of the breast,
   `(76752008, SCT, "Breast") <http://snomed.info/id/76752008>`__ and
   `(57983, FMA,
   "Breast") <http://xiphoid.biostr.washington.edu/fma/fmabrowser-hierarchy.html?fmaid=57983>`__
   would be considered equivalent. Neither would be equivalent to
   concepts that pre-coordinated other aspects such as laterality, e.g.,
   `(80248007, SCT, "Left breast") <http://snomed.info/id/80248007>`__,
   or entire body organ, e.g., `(181131000, SCT, "Entire
   breast") <http://snomed.info/id/181131000>`__.

Some scenarios in which it is helpful for the creating system to send
equivalent codes include:

-  when different representations of the same concept are present in a
   standard coding scheme, such as the SNOMED-CT and SNOMED-RT and CTV3
   style identifiers,

-  when the same concept is present in different standard coding
   schemes, but considered by the creating system to be synonymous, such
   as anatomical concepts from SNOMED and FMA, and

-  when the same concept is present in a local as well as a standard
   coding scheme, but considered by the creating system to be
   synonymous, such as a local private procedure code and the same
   concept in LOINC or SNOMED or RADLEX.

The `table_title <#table_8.8-1b>`__ may be used to identify a Context
Group from which the codes were selected, such as for a particular
cross-institutional, cross-application context for trials, research and
knowledge-based applications.

.. _sect_8.10:

Coded Entry Data Examples
-------------------------

An example of a long SNOMED CT code encoding as an Item in a Sequence:

+----------+-----------------+-------------+----+-----------------+
| Nesting  | Attribute Name  | Tag         | VR | Value           |
+==========+=================+=============+====+=================+
| %item    |                 |             |    |                 |
+----------+-----------------+-------------+----+-----------------+
| >        | Coding Scheme   | (0008,0102) | SH | SCT             |
|          | Designator      |             |    |                 |
+----------+-----------------+-------------+----+-----------------+
| >        | Code Meaning    | (0008,0104) | LO | Invasive        |
|          |                 |             |    | diagnostic      |
|          |                 |             |    | procedure       |
+----------+-----------------+-------------+----+-----------------+
| >        | Long Code Value | (0008,0119) | UC | 621             |
|          |                 |             |    | 566751000087104 |
+----------+-----------------+-------------+----+-----------------+
| %enditem |                 |             |    |                 |
+----------+-----------------+-------------+----+-----------------+

.. note::

   SCT:621566751000087104 is not included in the SNOMED CT DICOM Subset
   and is not present in the SNOMED CT INT release. It is from the
   Canadian National Extension and is used here only as an example.

An example of a short SNOMED CT with equivalent SNOMED SRT and CTV3
(Read) codes as an Item in a Sequence:

+-----------+----------------+-------------+----+----------------+
| Nesting   | Attribute Name | Tag         | VR | Value          |
+===========+================+=============+====+================+
| %item     |                |             |    |                |
+-----------+----------------+-------------+----+----------------+
| >         | Code Value     | (0008,0100) | SH | `4064          |
|           |                |             |    | 00000 <http:// |
|           |                |             |    | snomed.info/id |
|           |                |             |    | /406400000>`__ |
+-----------+----------------+-------------+----+----------------+
| >         | Coding Scheme  | (0008,0102) | SH | SCT            |
|           | Designator     |             |    |                |
+-----------+----------------+-------------+----+----------------+
| >         | Code Meaning   | (0008,0104) | LO | Dimeglumine    |
|           |                |             |    | gadopentetate  |
|           |                |             |    | 469.01mg/mL    |
|           |                |             |    | inj soln 15mL  |
|           |                |             |    | pfld syr       |
+-----------+----------------+-------------+----+----------------+
| >         | Equivalent     | (0008,0121) | SQ |                |
|           | Code Sequence  |             |    |                |
+-----------+----------------+-------------+----+----------------+
| %sequence |                |             |    |                |
+-----------+----------------+-------------+----+----------------+
| %item     |                |             |    |                |
+-----------+----------------+-------------+----+----------------+
| >>        | Code Value     | (0008,0100) | SH | `C-            |
|           |                |             |    | B0478 <http:// |
|           |                |             |    | snomed.info/id |
|           |                |             |    | /406400000>`__ |
+-----------+----------------+-------------+----+----------------+
| >>        | Coding Scheme  | (0008,0102) | SH | SRT            |
|           | Designator     |             |    |                |
+-----------+----------------+-------------+----+----------------+
| >>        | Code Meaning   | (0008,0104) | LO | Dimeglumine    |
|           |                |             |    | gadopentetate  |
|           |                |             |    | 469.01mg/mL    |
|           |                |             |    | inj soln 15mL  |
|           |                |             |    | pfld syr       |
+-----------+----------------+-------------+----+----------------+
| %enditem  |                |             |    |                |
+-----------+----------------+-------------+----+----------------+
| %item     |                |             |    |                |
+-----------+----------------+-------------+----+----------------+
| >>        | Code Value     | (0008,0100) | SH | `              |
|           |                |             |    | XUaZB <http:// |
|           |                |             |    | snomed.info/id |
|           |                |             |    | /406400000>`__ |
+-----------+----------------+-------------+----+----------------+
| >>        | Coding Scheme  | (0008,0102) | SH | CTV3           |
|           | Designator     |             |    |                |
+-----------+----------------+-------------+----+----------------+
| >>        | Code Meaning   | (0008,0104) | LO | Dimeglumine    |
|           |                |             |    | gadopentetate  |
|           |                |             |    | 469.01mg/mL    |
|           |                |             |    | inj soln 15mL  |
|           |                |             |    | pfld syr       |
+-----------+----------------+-------------+----+----------------+
| %enditem  |                |             |    |                |
+-----------+----------------+-------------+----+----------------+
| %endseq   |                |             |    |                |
+-----------+----------------+-------------+----+----------------+
| %enditem  |                |             |    |                |
+-----------+----------------+-------------+----+----------------+

.. note::

   SCT:406400000 is not included in the SNOMED CT DICOM Subset and is
   used here only as an example.

An example of encoding a long URN as an Item in a Sequence.

+----------+----------------+-------------+----+-----------------+
| Nesting  | Attribute Name | Tag         | VR | Value           |
+==========+================+=============+====+=================+
| %item    |                |             |    |                 |
+----------+----------------+-------------+----+-----------------+
| >        | Code Meaning   | (0008,0104) | LO | HIPAA Privacy   |
|          |                |             |    | Rule            |
+----------+----------------+-------------+----+-----------------+
| >        | URN Code Value | (0008,0120) | UR | urn:lex:us:fe   |
|          |                |             |    | deral:codified. |
|          |                |             |    | regulation:2013 |
|          |                |             |    | -04-25;45CFR164 |
+----------+----------------+-------------+----+-----------------+
| %enditem |                |             |    |                 |
+----------+----------------+-------------+----+-----------------+

.. _sect_8.11:

Retired Codes and Expected Behavior
-----------------------------------

As this Standard and external coding schemes are maintained, the codes
specified as Values for Attributes and in Conditions may change. The
previous codes are considered Retired but implementations may continue
to send them and receivers will be expected to be able to continue to
recognize the Retired codes, including the Code Value and Coding Scheme
Designator, even if the current Standard does not publish them.

A notable example is the change throughout the Standard from using
"SNOMED-RT style" code values with a Coding Scheme Designator of "SRT",
"SNM3" or "99SDM", to the use of SNOMED CT numeric code values with a
Coding Scheme Designator of "SCT". Those retired codes may be found in
PS3.3 2019a. A mapping of retired to new SNOMED codes is found in .

