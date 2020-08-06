.. _chapter_10:

Miscellaneous Macros
====================

.. _sect_10.1:

Person Identification Macro
---------------------------

This Macro may be invoked to specify a coded representation of a person
such as a healthcare worker, and the organization to which they are
responsible.

.. note::

   1. This Macro is typically invoked within a Sequence Item used to
      identify an individual such as a physician or a device operator.

   2. The free-text name of the individual is not included in this Macro
      since there are already widely used specific Attributes to hold
      such values.

   3. No Baseline, Defined or Enumerated CIDs are defined nor is any
      particular coding scheme specified. In practice, workers are
      usually identified by using a locally or nationally specific
      coding scheme. For example, a local Coding Scheme Designator might
      be used and the individual's internal hospital ID number user in
      Code Value.

   4. The organization is specified by either a coded Sequence or a free
      text name but not both. A Baseline CID of standard organizations
      is provided for the purpose of identifying standard organizations
      responsible for creation of Well Known Instances.

.. table:: Person Identification Macro Attributes Description

   +-------------------+-------------------+------+-------------------+
   | Attribute Name    | Tag               | Type | Attribute         |
   |                   |                   |      | Description       |
   +===================+===================+======+===================+
   | Person            | (0040,1101)       | 1    | A coded entry     |
   | Identification    |                   |      | that identifies a |
   | Code Sequence     |                   |      | person.           |
   |                   |                   |      |                   |
   |                   |                   |      | The Code Meaning  |
   |                   |                   |      | Attribute, though |
   |                   |                   |      | it will be        |
   |                   |                   |      | encoded with a VR |
   |                   |                   |      | of LO, may be     |
   |                   |                   |      | encoded according |
   |                   |                   |      | to the rules of   |
   |                   |                   |      | the PN VR (e.g.,  |
   |                   |                   |      | caret '^'         |
   |                   |                   |      | delimiters shall  |
   |                   |                   |      | separate name     |
   |                   |                   |      | components),      |
   |                   |                   |      | except that a     |
   |                   |                   |      | single component  |
   |                   |                   |      | (i.e., the whole  |
   |                   |                   |      | name unseparated  |
   |                   |                   |      | by caret          |
   |                   |                   |      | delimiters) is    |
   |                   |                   |      | not permitted.    |
   |                   |                   |      | Name component    |
   |                   |                   |      | groups for use    |
   |                   |                   |      | with multi-byte   |
   |                   |                   |      | character sets    |
   |                   |                   |      | are permitted, as |
   |                   |                   |      | long as they fit  |
   |                   |                   |      | within the 64     |
   |                   |                   |      | characters (the   |
   |                   |                   |      | length of the LO  |
   |                   |                   |      | VR).              |
   |                   |                   |      |                   |
   |                   |                   |      | One or more Items |
   |                   |                   |      | shall be included |
   |                   |                   |      | in this Sequence. |
   +-------------------+-------------------+------+-------------------+
   | *>Includ          | *No Baseline CID  |      |                   |
   | e*\ `table_title  | is defined.*      |      |                   |
   | <#table_8.8-1>`__ |                   |      |                   |
   +-------------------+-------------------+------+-------------------+
   | Person's Address  | (0040,1102)       | 3    | Person's mailing  |
   |                   |                   |      | address           |
   +-------------------+-------------------+------+-------------------+
   | Person's          | (0040,1103)       | 3    | Person's          |
   | Telephone Numbers |                   |      | telephone         |
   |                   |                   |      | number(s)         |
   +-------------------+-------------------+------+-------------------+
   | Person's Telecom  | (0040,1104)       | 3    | The person's      |
   | Information       |                   |      | telecommunication |
   |                   |                   |      | contact           |
   |                   |                   |      | information,      |
   |                   |                   |      | including         |
   |                   |                   |      | telephone, email, |
   |                   |                   |      | or other telecom  |
   |                   |                   |      | addresses.        |
   |                   |                   |      |                   |
   |                   |                   |      | .. note::         |
   |                   |                   |      |                   |
   |                   |                   |      |    1. This        |
   |                   |                   |      |       Attribute   |
   |                   |                   |      |       may have    |
   |                   |                   |      |       internal    |
   |                   |                   |      |       format or   |
   |                   |                   |      |       structure   |
   |                   |                   |      |       in          |
   |                   |                   |      |       accordance  |
   |                   |                   |      |       with local  |
   |                   |                   |      |       agreement   |
   |                   |                   |      |       or profile. |
   |                   |                   |      |       In the      |
   |                   |                   |      |       absence of  |
   |                   |                   |      |       such        |
   |                   |                   |      |       agreement   |
   |                   |                   |      |       or prior    |
   |                   |                   |      |       formatting, |
   |                   |                   |      |       use of      |
   |                   |                   |      |       ITU-T E.123 |
   |                   |                   |      |       is          |
   |                   |                   |      |       suggested.  |
   |                   |                   |      |                   |
   |                   |                   |      |    2. It is       |
   |                   |                   |      |       recommended |
   |                   |                   |      |       that this   |
   |                   |                   |      |       Attribute   |
   |                   |                   |      |       be treated  |
   |                   |                   |      |       as          |
   |                   |                   |      |       equivalent  |
   |                   |                   |      |       to HL7v2    |
   |                   |                   |      |       (v2.5 or    |
   |                   |                   |      |       later)      |
   |                   |                   |      |       field       |
   |                   |                   |      |       ROL-12, and |
   |                   |                   |      |       be          |
   |                   |                   |      |       formatted   |
   |                   |                   |      |       in          |
   |                   |                   |      |       accordance  |
   |                   |                   |      |       with the    |
   |                   |                   |      |       HL7v2 XTN   |
   |                   |                   |      |       data type   |
   |                   |                   |      |       (without    |
   |                   |                   |      |       escapes for |
   |                   |                   |      |       HL7 message |
   |                   |                   |      |       structure   |
   |                   |                   |      |       reserved    |
   |                   |                   |      |                   |
   |                   |                   |      |      characters). |
   |                   |                   |      |       See         |
   |                   |                   |      |       additional  |
   |                   |                   |      |       notes in    |
   |                   |                   |      |       the Module  |
   |                   |                   |      |       invoking    |
   |                   |                   |      |       this Macro. |
   +-------------------+-------------------+------+-------------------+
   | Institution Name  | (0008,0080)       | 1C   | Institution or    |
   |                   |                   |      | organization to   |
   |                   |                   |      | which the         |
   |                   |                   |      | identified        |
   |                   |                   |      | individual is     |
   |                   |                   |      | responsible or    |
   |                   |                   |      | accountable.      |
   |                   |                   |      | Required if       |
   |                   |                   |      | Institution Code  |
   |                   |                   |      | Sequence          |
   |                   |                   |      | (0008,0082) is    |
   |                   |                   |      | not present.      |
   +-------------------+-------------------+------+-------------------+
   | Institution       | (0008,0081)       | 3    | Mailing address   |
   | Address           |                   |      | of the            |
   |                   |                   |      | institution or    |
   |                   |                   |      | organization to   |
   |                   |                   |      | which the         |
   |                   |                   |      | identified        |
   |                   |                   |      | individual is     |
   |                   |                   |      | responsible or    |
   |                   |                   |      | accountable.      |
   +-------------------+-------------------+------+-------------------+
   | Institution Code  | (0008,0082)       | 1C   | Institution or    |
   | Sequence          |                   |      | organization to   |
   |                   |                   |      | which the         |
   |                   |                   |      | identified        |
   |                   |                   |      | individual is     |
   |                   |                   |      | responsible or    |
   |                   |                   |      | accountable.      |
   |                   |                   |      | Required if       |
   |                   |                   |      | Institution Name  |
   |                   |                   |      | (0008,0080) is    |
   |                   |                   |      | not present.      |
   |                   |                   |      |                   |
   |                   |                   |      | Only a single     |
   |                   |                   |      | Item shall be     |
   |                   |                   |      | included in this  |
   |                   |                   |      | Sequence.         |
   +-------------------+-------------------+------+-------------------+
   | *>Includ          | *B.*              |      |                   |
   | e*\ `table_title  |                   |      |                   |
   | <#table_8.8-1>`__ |                   |      |                   |
   +-------------------+-------------------+------+-------------------+
   | Institutional     | (0008,1040)       | 3    | The Department,   |
   | Department Name   |                   |      | Unit or Service   |
   |                   |                   |      | within the        |
   |                   |                   |      | healthcare        |
   |                   |                   |      | facility.         |
   +-------------------+-------------------+------+-------------------+
   | Institutional     | (0008,1041)       | 3    | A coded           |
   | Department Type   |                   |      | description of    |
   | Code Sequence     |                   |      | the type of       |
   |                   |                   |      | Department or     |
   |                   |                   |      | Service within    |
   |                   |                   |      | the healthcare    |
   |                   |                   |      | facility.         |
   |                   |                   |      |                   |
   |                   |                   |      | .. note::         |
   |                   |                   |      |                   |
   |                   |                   |      |    This might be  |
   |                   |                   |      |    obtained from  |
   |                   |                   |      |    a              |
   |                   |                   |      |    corresponding  |
   |                   |                   |      |    HL7v2 message  |
   |                   |                   |      |    containing     |
   |                   |                   |      |    PV1:10         |
   |                   |                   |      |    Hospital       |
   |                   |                   |      |    Service.       |
   |                   |                   |      |                   |
   |                   |                   |      | Only a single     |
   |                   |                   |      | Item is permitted |
   |                   |                   |      | in this Sequence. |
   +-------------------+-------------------+------+-------------------+
   | *>Includ          | *B.*              |      |                   |
   | e*\ `table_title  |                   |      |                   |
   | <#table_8.8-1>`__ |                   |      |                   |
   +-------------------+-------------------+------+-------------------+

.. _sect_10.2:

Content Item Macro
------------------

A Content Item is a flexible means of encoding attribute identifiers and
attribute values using the Code Sequence Macro (see `Encoding of Coded
Entry Data <#chapter_8>`__) for coded terminology defined by a coding
scheme. The Content Item provides a name-value pair, i.e., a Concept
Name, encoded as a Code Sequence, and a Concept Value. The Concept Value
may be encoded by any of a set of generic Attributes, as specified by a
Value Type, including text, personal name, numeric, and coded concept
(Code Sequence) values.

.. note::

   1. Comparing a Content Item to a native DICOM Data Element, the
      Concept Name Code Sequence corresponds to the Data Element Tag and
      Attribute Name, the Value Type to the Value Representation, and
      the Concept Value to the Data Element Value Field. See .

   2. The IMAGE Value Type of this Macro does not include the Type 3
      Attributes of the IMAGE Value Type defined in `SR Document Content
      Module <#sect_C.17.3>`__, as they are not required for Acquisition
      Context or Protocol Context Content Items.

Specific uses of the Content Item may invoke the Content Item Macro
defined in this Section, the Document Content Macro of `SR Document
Content Module <#sect_C.17.3>`__, or another similar construct. An
invocation of the Content Item Macro may constrain the allowed values of
Value Type (0040,A040).

.. note::

   1. The NUMERIC Value Type of this Macro differs from the NUM Value
      Type defined in `SR Document Content Module <#sect_C.17.3>`__,
      since the encoding of the Concept Value is different.

   2. The Value Type uses Enumerated Values so as to assure that
      non-standard Value Types are not used, and to prevent the
      nefarious use, for example, of a CONTAINER Value Type in an
      SR-like manner to create nested content, which is not the intent.

   3. Some invocations of this Macro may use the Content Item Modifier
      Sequence (0040,0441) to achieve a single level of "nesting". That
      Attribute is not included in this Macro itself, to prevent
      recursive inclusion.

See `Attribute Macros <#sect_5.4>`__ for the meaning of the Type column
in this Macro when applied to Normalized IODs.

.. table:: Content Item Macro Attributes Description

   +-------------------+-------------------+------+-------------------+
   | Attribute Name    | Tag               | Type | Attribute         |
   |                   |                   |      | Description       |
   +===================+===================+======+===================+
   | Value Type        | (0040,A040)       | 1    | The type of the   |
   |                   |                   |      | value encoded in  |
   |                   |                   |      | this name-value   |
   |                   |                   |      | Item.             |
   |                   |                   |      |                   |
   |                   |                   |      | DATE              |
   |                   |                   |      | TIME              |
   |                   |                   |      | DATETIME          |
   |                   |                   |      | PNAME             |
   |                   |                   |      | UIDREF            |
   |                   |                   |      | TEXT              |
   |                   |                   |      | CODE              |
   |                   |                   |      | NUMERIC           |
   |                   |                   |      | COMPOSITE         |
   |                   |                   |      | IMAGE             |
   +-------------------+-------------------+------+-------------------+
   | Observation       | (0040,A032)       | 3    | The date and time |
   | DateTime          |                   |      | on which this     |
   |                   |                   |      | Item was          |
   |                   |                   |      | completed. For    |
   |                   |                   |      | the purpose of    |
   |                   |                   |      | recording         |
   |                   |                   |      | measurements or   |
   |                   |                   |      | logging events,   |
   |                   |                   |      | completion time   |
   |                   |                   |      | is defined as the |
   |                   |                   |      | ending time of    |
   |                   |                   |      | data acquisition  |
   |                   |                   |      | of the            |
   |                   |                   |      | measurement, or   |
   |                   |                   |      | the ending time   |
   |                   |                   |      | of occurrence of  |
   |                   |                   |      | the event.        |
   +-------------------+-------------------+------+-------------------+
   | Concept Name Code | (0040,A043)       | 1    | Coded concept     |
   | Sequence          |                   |      | name of this      |
   |                   |                   |      | name-value Item.  |
   |                   |                   |      |                   |
   |                   |                   |      | Only a single     |
   |                   |                   |      | Item shall be     |
   |                   |                   |      | included in this  |
   |                   |                   |      | Sequence.         |
   +-------------------+-------------------+------+-------------------+
   | *>Includ          | *No Baseline CID  |      |                   |
   | e*\ `table_title  | is defined.*      |      |                   |
   | <#table_8.8-1>`__ |                   |      |                   |
   +-------------------+-------------------+------+-------------------+
   | DateTime          | (0040,A120)       | 1C   | DateTime value    |
   |                   |                   |      | for this          |
   |                   |                   |      | name-value Item.  |
   |                   |                   |      |                   |
   |                   |                   |      | Required if Value |
   |                   |                   |      | Type (0040,A040)  |
   |                   |                   |      | is DATETIME.      |
   +-------------------+-------------------+------+-------------------+
   | Date              | (0040,A121)       | 1C   | Date value for    |
   |                   |                   |      | this name-value   |
   |                   |                   |      | Item.             |
   |                   |                   |      |                   |
   |                   |                   |      | Required if Value |
   |                   |                   |      | Type (0040,A040)  |
   |                   |                   |      | is DATE.          |
   +-------------------+-------------------+------+-------------------+
   | Time              | (0040,A122)       | 1C   | Time value for    |
   |                   |                   |      | this name-value   |
   |                   |                   |      | Item.             |
   |                   |                   |      |                   |
   |                   |                   |      | Required if Value |
   |                   |                   |      | Type (0040,A040)  |
   |                   |                   |      | is TIME.          |
   +-------------------+-------------------+------+-------------------+
   | Person Name       | (0040,A123)       | 1C   | Person name value |
   |                   |                   |      | for this          |
   |                   |                   |      | name-value Item.  |
   |                   |                   |      |                   |
   |                   |                   |      | Required if Value |
   |                   |                   |      | Type (0040,A040)  |
   |                   |                   |      | is PNAME.         |
   +-------------------+-------------------+------+-------------------+
   | UID               | (0040,A124)       | 1C   | UID value for     |
   |                   |                   |      | this name-value   |
   |                   |                   |      | Item.             |
   |                   |                   |      |                   |
   |                   |                   |      | Required if Value |
   |                   |                   |      | Type (0040,A040)  |
   |                   |                   |      | is UIDREF.        |
   +-------------------+-------------------+------+-------------------+
   | Text Value        | (0040,A160)       | 1C   | Text value for    |
   |                   |                   |      | this name-value   |
   |                   |                   |      | Item.             |
   |                   |                   |      |                   |
   |                   |                   |      | Required if Value |
   |                   |                   |      | Type (0040,A040)  |
   |                   |                   |      | is TEXT.          |
   +-------------------+-------------------+------+-------------------+
   | Concept Code      | (0040,A168)       | 1C   | Coded concept     |
   | Sequence          |                   |      | value of this     |
   |                   |                   |      | name-value Item.  |
   |                   |                   |      |                   |
   |                   |                   |      | Only a single     |
   |                   |                   |      | Item shall be     |
   |                   |                   |      | included in this  |
   |                   |                   |      | Sequence.         |
   |                   |                   |      |                   |
   |                   |                   |      | Required if Value |
   |                   |                   |      | Type (0040,A040)  |
   |                   |                   |      | is CODE.          |
   +-------------------+-------------------+------+-------------------+
   | *>Includ          | *No Baseline CID  |      |                   |
   | e*\ `table_title  | is defined.*      |      |                   |
   | <#table_8.8-1>`__ |                   |      |                   |
   +-------------------+-------------------+------+-------------------+
   | Numeric Value     | (0040,A30A)       | 1C   | Numeric value for |
   |                   |                   |      | this name-value   |
   |                   |                   |      | Item. Only a      |
   |                   |                   |      | single value      |
   |                   |                   |      | shall be present. |
   |                   |                   |      |                   |
   |                   |                   |      | Required if Value |
   |                   |                   |      | Type (0040,A040)  |
   |                   |                   |      | is NUMERIC.       |
   +-------------------+-------------------+------+-------------------+
   | Floating Point    | (0040,A161)       | 1C   | The floating      |
   | Value             |                   |      | point             |
   |                   |                   |      | representation of |
   |                   |                   |      | Numeric Value     |
   |                   |                   |      | (0040,A30A). The  |
   |                   |                   |      | same number of    |
   |                   |                   |      | values as Numeric |
   |                   |                   |      | Value (0040,A30A) |
   |                   |                   |      | shall be present. |
   |                   |                   |      |                   |
   |                   |                   |      | Required if       |
   |                   |                   |      | Numeric Value     |
   |                   |                   |      | (0040,A30A) has   |
   |                   |                   |      | insufficient      |
   |                   |                   |      | precision to      |
   |                   |                   |      | represent the     |
   |                   |                   |      | value as a        |
   |                   |                   |      | string. May be    |
   |                   |                   |      | present           |
   |                   |                   |      | otherwise.        |
   +-------------------+-------------------+------+-------------------+
   | Rational          | (0040,A162)       | 1C   | The integer       |
   | Numerator Value   |                   |      | numerator of a    |
   |                   |                   |      | rational          |
   |                   |                   |      | representation of |
   |                   |                   |      | Numeric Value     |
   |                   |                   |      | (0040,A30A).      |
   |                   |                   |      | Encoded as a      |
   |                   |                   |      | signed integer    |
   |                   |                   |      | value. The same   |
   |                   |                   |      | number of values  |
   |                   |                   |      | as Numeric Value  |
   |                   |                   |      | (0040,A30A) shall |
   |                   |                   |      | be present.       |
   |                   |                   |      |                   |
   |                   |                   |      | Required if       |
   |                   |                   |      | Numeric Value     |
   |                   |                   |      | (0040,A30A) has   |
   |                   |                   |      | insufficient      |
   |                   |                   |      | precision to      |
   |                   |                   |      | represent a       |
   |                   |                   |      | rational value as |
   |                   |                   |      | a string. May be  |
   |                   |                   |      | present           |
   |                   |                   |      | otherwise.        |
   +-------------------+-------------------+------+-------------------+
   | Rational          | (0040,A163)       | 1C   | The integer       |
   | Denominator Value |                   |      | denominator of a  |
   |                   |                   |      | rational          |
   |                   |                   |      | representation of |
   |                   |                   |      | Numeric Value     |
   |                   |                   |      | (0040,A30A).      |
   |                   |                   |      | Encoded as a      |
   |                   |                   |      | non-zero unsigned |
   |                   |                   |      | integer value.    |
   |                   |                   |      | The same number   |
   |                   |                   |      | of values as      |
   |                   |                   |      | Numeric Value     |
   |                   |                   |      | (0040,A30A) shall |
   |                   |                   |      | be present.       |
   |                   |                   |      |                   |
   |                   |                   |      | Required if       |
   |                   |                   |      | Rational          |
   |                   |                   |      | Numerator Value   |
   |                   |                   |      | (0040,A162) is    |
   |                   |                   |      | present.          |
   +-------------------+-------------------+------+-------------------+
   | Measurement Units | (0040,08EA)       | 1C   | Units of          |
   | Code Sequence     |                   |      | measurement for a |
   |                   |                   |      | numeric value in  |
   |                   |                   |      | this name-value   |
   |                   |                   |      | Item.             |
   |                   |                   |      |                   |
   |                   |                   |      | Only a single     |
   |                   |                   |      | Item shall be     |
   |                   |                   |      | included in this  |
   |                   |                   |      | Sequence.         |
   |                   |                   |      |                   |
   |                   |                   |      | Required if Value |
   |                   |                   |      | Type (0040,A040)  |
   |                   |                   |      | is NUMERIC.       |
   +-------------------+-------------------+------+-------------------+
   | *>Includ          | *B.*              |      |                   |
   | e*\ `table_title  |                   |      |                   |
   | <#table_8.8-1>`__ |                   |      |                   |
   +-------------------+-------------------+------+-------------------+
   | Referenced SOP    | (0008,1199)       | 1C   | Composite SOP     |
   | Sequence          |                   |      | Instance          |
   |                   |                   |      | Reference value   |
   |                   |                   |      | for this          |
   |                   |                   |      | name-value Item.  |
   |                   |                   |      |                   |
   |                   |                   |      | Only a single     |
   |                   |                   |      | Item shall be     |
   |                   |                   |      | included in this  |
   |                   |                   |      | Sequence.         |
   |                   |                   |      |                   |
   |                   |                   |      | Required if Value |
   |                   |                   |      | Type (0040,A040)  |
   |                   |                   |      | is COMPOSITE or   |
   |                   |                   |      | IMAGE.            |
   +-------------------+-------------------+------+-------------------+
   | *>Includ          |                   |      |                   |
   | e*\ `table_title  |                   |      |                   |
   | <#table_10-11>`__ |                   |      |                   |
   +-------------------+-------------------+------+-------------------+
   | >Referenced Frame | (0008,1160)       | 1C   | Identifies the    |
   | Number            |                   |      | frame numbers     |
   |                   |                   |      | within the        |
   |                   |                   |      | Referenced SOP    |
   |                   |                   |      | Instance to which |
   |                   |                   |      | the reference     |
   |                   |                   |      | applies. The      |
   |                   |                   |      | first frame shall |
   |                   |                   |      | be denoted as     |
   |                   |                   |      | frame number 1.   |
   |                   |                   |      |                   |
   |                   |                   |      | .. note::         |
   |                   |                   |      |                   |
   |                   |                   |      |    This Attribute |
   |                   |                   |      |    may be         |
   |                   |                   |      |    multi-valued.  |
   |                   |                   |      |                   |
   |                   |                   |      | Required if the   |
   |                   |                   |      | Referenced SOP    |
   |                   |                   |      | Instance is a     |
   |                   |                   |      | multi-frame image |
   |                   |                   |      | and the reference |
   |                   |                   |      | does not apply to |
   |                   |                   |      | all frames, and   |
   |                   |                   |      | Referenced        |
   |                   |                   |      | Segment Number    |
   |                   |                   |      | (0062,000B) is    |
   |                   |                   |      | not present.      |
   +-------------------+-------------------+------+-------------------+
   | >Referenced       | (0062,000B)       | 1C   | Identifies the    |
   | Segment Number    |                   |      | segments to which |
   |                   |                   |      | the reference     |
   |                   |                   |      | applies           |
   |                   |                   |      | identified by     |
   |                   |                   |      | Segment Number    |
   |                   |                   |      | (0062,0004).      |
   |                   |                   |      |                   |
   |                   |                   |      | Required if the   |
   |                   |                   |      | Referenced SOP    |
   |                   |                   |      | Instance is a     |
   |                   |                   |      | Segmentation or   |
   |                   |                   |      | Surface           |
   |                   |                   |      | Segmentation and  |
   |                   |                   |      | the reference     |
   |                   |                   |      | does not apply to |
   |                   |                   |      | all segments and  |
   |                   |                   |      | Referenced Frame  |
   |                   |                   |      | Number            |
   |                   |                   |      | (0008,1160) is    |
   |                   |                   |      | not present.      |
   +-------------------+-------------------+------+-------------------+

.. _sect_10.2.1:

Content Item With Modifiers Macro
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Content Item with Modifiers is a means of describing structured content
which needs a Content Item with single optional level of modifiers, i.e.
a two-level structure of Content Items. An invocation of the Content
Item with Modifiers Macro will usually specify the allowed values using
a Protocol Context Template in , which allows a single Nesting Level
(see in ). Constraints on the use of this Macro may be specified in ,
which may be invoked in IODs in .

.. table:: Content Item with Modifiers Macro Attributes

   +-------------------+-------------------+------+-------------------+
   | Attribute Name    | Tag               | Type | Attribute         |
   |                   |                   |      | Description       |
   +===================+===================+======+===================+
   | *Inclu            | *No Baseline TID  |      |                   |
   | de*\ `table_title | is defined.*      |      |                   |
   |  <#table_10-2>`__ |                   |      |                   |
   +-------------------+-------------------+------+-------------------+
   | Content Item      | (0040,0441)       | 3    | Specifies         |
   | Modifier Sequence |                   |      | modifiers for the |
   |                   |                   |      | Content Item.     |
   |                   |                   |      |                   |
   |                   |                   |      | One or more Items |
   |                   |                   |      | are permitted in  |
   |                   |                   |      | this Sequence.    |
   +-------------------+-------------------+------+-------------------+
   | *>Inclu           | *No Baseline TID  |      |                   |
   | de*\ `table_title | is defined.*      |      |                   |
   |  <#table_10-2>`__ |                   |      |                   |
   +-------------------+-------------------+------+-------------------+

.. _sect_10.3:

Image SOP Instance Reference Macro
----------------------------------

.. table:: Image SOP Instance Reference Macro Attributes

   +----------------------+-------------+------+----------------------+
   | Attribute Name       | Tag         | Type | Attribute            |
   |                      |             |      | Description          |
   +======================+=============+======+======================+
   | *                    |             |      |                      |
   | Include*\ `table_tit |             |      |                      |
   | le <#table_10-11>`__ |             |      |                      |
   +----------------------+-------------+------+----------------------+
   | Referenced Frame     | (0008,1160) | 1C   | Identifies the frame |
   | Number               |             |      | numbers within the   |
   |                      |             |      | Referenced SOP       |
   |                      |             |      | Instance to which    |
   |                      |             |      | the reference        |
   |                      |             |      | applies. The first   |
   |                      |             |      | frame shall be       |
   |                      |             |      | denoted as frame     |
   |                      |             |      | number 1.            |
   |                      |             |      |                      |
   |                      |             |      | .. note::            |
   |                      |             |      |                      |
   |                      |             |      |    This Attribute    |
   |                      |             |      |    may be            |
   |                      |             |      |    multi-valued.     |
   |                      |             |      |                      |
   |                      |             |      | Required if the      |
   |                      |             |      | Referenced SOP       |
   |                      |             |      | Instance is a        |
   |                      |             |      | multi-frame image    |
   |                      |             |      | and the reference    |
   |                      |             |      | does not apply to    |
   |                      |             |      | all frames, and      |
   |                      |             |      | Referenced Segment   |
   |                      |             |      | Number (0062,000B)   |
   |                      |             |      | is not present.      |
   +----------------------+-------------+------+----------------------+
   | Referenced Segment   | (0062,000B) | 1C   | Identifies the       |
   | Number               |             |      | Segment Number to    |
   |                      |             |      | which the reference  |
   |                      |             |      | applies.             |
   |                      |             |      |                      |
   |                      |             |      | Required if the      |
   |                      |             |      | Referenced SOP       |
   |                      |             |      | Instance is a        |
   |                      |             |      | Segmentation or      |
   |                      |             |      | Surface Segmentation |
   |                      |             |      | and the reference    |
   |                      |             |      | does not apply to    |
   |                      |             |      | all segments and     |
   |                      |             |      | Referenced Frame     |
   |                      |             |      | Number (0008,1160)   |
   |                      |             |      | is not present.      |
   +----------------------+-------------+------+----------------------+

`table_title <#table_10-3b>`__ contains identifiers and access details
for a collection of Instances. It is intended to provide sufficient
information to retrieve the referenced Instances.

.. table:: Referenced Instances and Access Macro Attributes

   +----------------------+-------------+------+----------------------+
   | Attribute Name       | Tag         | Type | Attribute            |
   |                      |             |      | Description          |
   +======================+=============+======+======================+
   | Type of Instances    | (0040,E020) | 1    | Type of object       |
   |                      |             |      | Instances            |
   |                      |             |      | referenced.          |
   |                      |             |      |                      |
   |                      |             |      | DICOM                |
   |                      |             |      | CDA                  |
   +----------------------+-------------+------+----------------------+
   | Study Instance UID   | (0020,000D) | 1C   | Unique identifier    |
   |                      |             |      | for the Study.       |
   |                      |             |      |                      |
   |                      |             |      | Required if Type of  |
   |                      |             |      | Instances            |
   |                      |             |      | (0040,E020) is DICOM |
   |                      |             |      | and the Information  |
   |                      |             |      | Model of the         |
   |                      |             |      | referenced Instance  |
   |                      |             |      | contains the Study   |
   |                      |             |      | IE                   |
   +----------------------+-------------+------+----------------------+
   | Series Instance UID  | (0020,000E) | 1C   | Unique identifier    |
   |                      |             |      | for the Series that  |
   |                      |             |      | is part of the Study |
   |                      |             |      | identified in Study  |
   |                      |             |      | Instance UID         |
   |                      |             |      | (0020,000D), if      |
   |                      |             |      | present, and         |
   |                      |             |      | contains the         |
   |                      |             |      | referenced object    |
   |                      |             |      | Instance(s).         |
   |                      |             |      |                      |
   |                      |             |      | Required if Type of  |
   |                      |             |      | Instances            |
   |                      |             |      | (0040,E020) is DICOM |
   |                      |             |      | and the Information  |
   |                      |             |      | Model of the         |
   |                      |             |      | referenced Instance  |
   |                      |             |      | contains the Series  |
   |                      |             |      | IE                   |
   +----------------------+-------------+------+----------------------+
   | Referenced SOP       | (0008,1199) | 1    | References to object |
   | Sequence             |             |      | Instances.           |
   |                      |             |      |                      |
   |                      |             |      | One or more Items    |
   |                      |             |      | shall be included in |
   |                      |             |      | this Sequence        |
   +----------------------+-------------+------+----------------------+
   | >Referenced SOP      | (0008,1150) | 1    | Uniquely identifies  |
   | Class UID            |             |      | the referenced SOP   |
   |                      |             |      | Class.               |
   +----------------------+-------------+------+----------------------+
   | >Referenced SOP      | (0008,1155) | 1    | Uniquely identifies  |
   | Instance UID         |             |      | the referenced SOP   |
   |                      |             |      | Instance.            |
   +----------------------+-------------+------+----------------------+
   | >HL7 Instance        | (0040,E001) | 1C   | Instance Identifier  |
   | Identifier           |             |      | of the encapsulated  |
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
   |                      |             |      | Required if Type of  |
   |                      |             |      | Instances            |
   |                      |             |      | (0040,E020) is CDA.  |
   +----------------------+-------------+------+----------------------+
   | >Referenced Frame    | (0008,1160) | 1C   | Identifies the frame |
   | Number               |             |      | numbers within the   |
   |                      |             |      | Referenced SOP       |
   |                      |             |      | Instance to which    |
   |                      |             |      | the reference        |
   |                      |             |      | applies. The first   |
   |                      |             |      | frame shall be       |
   |                      |             |      | denoted as frame     |
   |                      |             |      | number 1.            |
   |                      |             |      |                      |
   |                      |             |      | .. note::            |
   |                      |             |      |                      |
   |                      |             |      |    This Attribute    |
   |                      |             |      |    may be            |
   |                      |             |      |    multi-valued.     |
   |                      |             |      |                      |
   |                      |             |      | Required if the      |
   |                      |             |      | Referenced SOP       |
   |                      |             |      | Instance is a        |
   |                      |             |      | multi-frame image    |
   |                      |             |      | and the reference    |
   |                      |             |      | does not apply to    |
   |                      |             |      | all frames, and      |
   |                      |             |      | Referenced Segment   |
   |                      |             |      | Number (0062,000B)   |
   |                      |             |      | is not present.      |
   +----------------------+-------------+------+----------------------+
   | >Referenced Segment  | (0062,000B) | 1C   | Identifies the       |
   | Number               |             |      | Segment Number to    |
   |                      |             |      | which the reference  |
   |                      |             |      | applies. Required if |
   |                      |             |      | the Referenced SOP   |
   |                      |             |      | Instance is a        |
   |                      |             |      | Segmentation and the |
   |                      |             |      | reference does not   |
   |                      |             |      | apply to all         |
   |                      |             |      | segments and         |
   |                      |             |      | Referenced Frame     |
   |                      |             |      | Number (0008,1160)   |
   |                      |             |      | is not present.      |
   +----------------------+-------------+------+----------------------+
   | DICOM Retrieval      | (0040,E021) | 1C   | Details for          |
   | Sequence             |             |      | retrieving Instances |
   |                      |             |      | via the DICOM        |
   |                      |             |      | Retrieve Service.    |
   |                      |             |      |                      |
   |                      |             |      | Required if DICOM    |
   |                      |             |      | Media Retrieval      |
   |                      |             |      | Sequence             |
   |                      |             |      | (0040,E022), WADO    |
   |                      |             |      | Retrieval Sequence   |
   |                      |             |      | (0040,E023), WADO-RS |
   |                      |             |      | Retrieval Sequence   |
   |                      |             |      | (0040,E025) and XDS  |
   |                      |             |      | Retrieval Sequence   |
   |                      |             |      | (0040,E024) are not  |
   |                      |             |      | present. May be      |
   |                      |             |      | present otherwise.   |
   |                      |             |      |                      |
   |                      |             |      | This Sequence shall  |
   |                      |             |      | only identify        |
   |                      |             |      | sources known to     |
   |                      |             |      | have Instances       |
   |                      |             |      | referenced in        |
   |                      |             |      | Referenced SOP       |
   |                      |             |      | Sequence             |
   |                      |             |      | (0008,1199).         |
   |                      |             |      |                      |
   |                      |             |      | One or more Items    |
   |                      |             |      | shall be included in |
   |                      |             |      | this Sequence.       |
   +----------------------+-------------+------+----------------------+
   | >Retrieve AE Title   | (0008,0054) | 1    | Title of a DICOM     |
   |                      |             |      | Application Entity   |
   |                      |             |      | where the referenced |
   |                      |             |      | Instance(s) may be   |
   |                      |             |      | retrieved on the     |
   |                      |             |      | network.             |
   +----------------------+-------------+------+----------------------+
   | DICOM Media          | (0040,E022) | 1C   | Details for          |
   | Retrieval Sequence   |             |      | retrieving Instances |
   |                      |             |      | from Media.          |
   |                      |             |      |                      |
   |                      |             |      | Required if DICOM    |
   |                      |             |      | Retrieval Sequence   |
   |                      |             |      | (0040,E021), WADO    |
   |                      |             |      | Retrieval Sequence   |
   |                      |             |      | (0040,E023), and     |
   |                      |             |      | WADO-RS Retrieval    |
   |                      |             |      | Sequence (0040,E025) |
   |                      |             |      | and XDS Retrieval    |
   |                      |             |      | Sequence (0040,E024) |
   |                      |             |      | are not present. May |
   |                      |             |      | be present           |
   |                      |             |      | otherwise.           |
   |                      |             |      |                      |
   |                      |             |      | This Sequence shall  |
   |                      |             |      | only identify media  |
   |                      |             |      | known to have        |
   |                      |             |      | Instances referenced |
   |                      |             |      | in Referenced SOP    |
   |                      |             |      | Sequence             |
   |                      |             |      | (0008,1199).         |
   |                      |             |      |                      |
   |                      |             |      | One or more Items    |
   |                      |             |      | shall be included in |
   |                      |             |      | this Sequence.       |
   +----------------------+-------------+------+----------------------+
   | >Storage Media       | (0088,0130) | 2    | The user or          |
   | File-Set ID          |             |      | implementation       |
   |                      |             |      | specific human       |
   |                      |             |      | readable identifier  |
   |                      |             |      | that identifies the  |
   |                      |             |      | Storage Media on     |
   |                      |             |      | which the referenced |
   |                      |             |      | Instance(s) reside.  |
   +----------------------+-------------+------+----------------------+
   | >Storage Media       | (0088,0140) | 1    | Uniquely identifies  |
   | File-Set UID         |             |      | the Storage Media on |
   |                      |             |      | which the referenced |
   |                      |             |      | Instance(s) reside.  |
   +----------------------+-------------+------+----------------------+
   | WADO Retrieval       | (0040,E023) | 1C   | Details for          |
   | Sequence             |             |      | retrieving Instances |
   |                      |             |      | available via        |
   |                      |             |      | WADO-URI.            |
   |                      |             |      |                      |
   |                      |             |      | .. note::            |
   |                      |             |      |                      |
   |                      |             |      |    This Sequence     |
   |                      |             |      |    addresses use of  |
   |                      |             |      |    the URI-based Web |
   |                      |             |      |    Access to DICOM   |
   |                      |             |      |    Objects.          |
   |                      |             |      |    Retrieval via the |
   |                      |             |      |    IHE XDS-I.b       |
   |                      |             |      |    RAD-69            |
   |                      |             |      |    Transaction is    |
   |                      |             |      |    addressed in the  |
   |                      |             |      |    XDS Retrieval     |
   |                      |             |      |    Sequence          |
   |                      |             |      |    (0040,E024).      |
   |                      |             |      |                      |
   |                      |             |      | Required if DICOM    |
   |                      |             |      | Retrieval Sequence   |
   |                      |             |      | (0040,E021), DICOM   |
   |                      |             |      | Media Retrieval      |
   |                      |             |      | Sequence             |
   |                      |             |      | (0040,E022), WADO-RS |
   |                      |             |      | Retrieval Sequence   |
   |                      |             |      | (0040,E025) and XDS  |
   |                      |             |      | Retrieval Sequence   |
   |                      |             |      | (0040,E024) are not  |
   |                      |             |      | present. May be      |
   |                      |             |      | present otherwise.   |
   |                      |             |      |                      |
   |                      |             |      | One or more Items    |
   |                      |             |      | shall be included in |
   |                      |             |      | this Sequence.       |
   +----------------------+-------------+------+----------------------+
   | >Retrieve URI        | (0040,E010) | 1    | URI/URL specifying   |
   |                      |             |      | the location of the  |
   |                      |             |      | referenced           |
   |                      |             |      | Instance(s).         |
   |                      |             |      | Includes fully       |
   |                      |             |      | specified scheme,    |
   |                      |             |      | authority, path, and |
   |                      |             |      | query in accordance  |
   |                      |             |      | with                 |
   |                      |             |      | `                    |
   |                      |             |      | biblioentry_title <# |
   |                      |             |      | biblio_RFC_3986>`__. |
   |                      |             |      |                      |
   |                      |             |      | .. note::            |
   |                      |             |      |                      |
   |                      |             |      |    The VR of this    |
   |                      |             |      |    Data Element has  |
   |                      |             |      |    changed from UT   |
   |                      |             |      |    to UR.            |
   +----------------------+-------------+------+----------------------+
   | XDS Retrieval        | (0040,E024) | 1C   | Details for          |
   | Sequence             |             |      | retrieving Instances |
   |                      |             |      | using the IHE        |
   |                      |             |      | XDS-I.b RAD-69       |
   |                      |             |      | Transaction.         |
   |                      |             |      |                      |
   |                      |             |      | .. note::            |
   |                      |             |      |                      |
   |                      |             |      |    Retrieval via     |
   |                      |             |      |    WADO-URI is       |
   |                      |             |      |    addressed by the  |
   |                      |             |      |    WADO Retrieval    |
   |                      |             |      |    Sequence          |
   |                      |             |      |    (0040,E023).      |
   |                      |             |      |    Retrieval via     |
   |                      |             |      |    WADO-RS is        |
   |                      |             |      |    addressed by the  |
   |                      |             |      |    WADO-RS Retrieval |
   |                      |             |      |    Sequence          |
   |                      |             |      |    (0040,E025).      |
   |                      |             |      |                      |
   |                      |             |      | Required if DICOM    |
   |                      |             |      | Retrieval Sequence   |
   |                      |             |      | (0040,E021), DICOM   |
   |                      |             |      | Media Retrieval      |
   |                      |             |      | Sequence             |
   |                      |             |      | (0040,E022), WADO-RS |
   |                      |             |      | Retrieval Sequence   |
   |                      |             |      | (0040,E025) and WADO |
   |                      |             |      | Retrieval Sequence   |
   |                      |             |      | (0040,E023) are not  |
   |                      |             |      | present. May be      |
   |                      |             |      | present otherwise.   |
   |                      |             |      |                      |
   |                      |             |      | This Sequence shall  |
   |                      |             |      | only identify        |
   |                      |             |      | repositories known   |
   |                      |             |      | to have Instances    |
   |                      |             |      | referenced in        |
   |                      |             |      | Referenced SOP       |
   |                      |             |      | Sequence             |
   |                      |             |      | (0008,1199).         |
   |                      |             |      |                      |
   |                      |             |      | One or more Items    |
   |                      |             |      | shall be included in |
   |                      |             |      | this Sequence.       |
   +----------------------+-------------+------+----------------------+
   | >Repository Unique   | (0040,E030) | 1    | Uniquely identifies  |
   | ID                   |             |      | a Repository from    |
   |                      |             |      | which the referenced |
   |                      |             |      | Instances can be     |
   |                      |             |      | retrieved.           |
   +----------------------+-------------+------+----------------------+
   | >Home Community ID   | (0040,E031) | 3    | Uniquely identifies  |
   |                      |             |      | a Community to which |
   |                      |             |      | requests for the     |
   |                      |             |      | referenced Instances |
   |                      |             |      | can be directed.     |
   +----------------------+-------------+------+----------------------+
   | WADO-RS Retrieval    | (0040,E025) | 1C   | Details for          |
   | Sequence             |             |      | retrieving Instances |
   |                      |             |      | via WADO-RS.         |
   |                      |             |      |                      |
   |                      |             |      | .. note::            |
   |                      |             |      |                      |
   |                      |             |      |    Retrieval via     |
   |                      |             |      |    WADO-URI is       |
   |                      |             |      |    addressed in the  |
   |                      |             |      |    WADO Retrieval    |
   |                      |             |      |    Sequence          |
   |                      |             |      |    (0040,E023).      |
   |                      |             |      |    Retrieval via the |
   |                      |             |      |    IHE XDS-I.b       |
   |                      |             |      |    RAD-69            |
   |                      |             |      |    Transaction is    |
   |                      |             |      |    addressed in the  |
   |                      |             |      |    XDS Retrieval     |
   |                      |             |      |    Sequence          |
   |                      |             |      |    (0040,E024).      |
   |                      |             |      |                      |
   |                      |             |      | Required if DICOM    |
   |                      |             |      | Retrieval Sequence   |
   |                      |             |      | (0040,E021), DICOM   |
   |                      |             |      | Media Retrieval      |
   |                      |             |      | Sequence             |
   |                      |             |      | (0040,E022), WADO    |
   |                      |             |      | Retrieval Sequence   |
   |                      |             |      | (0040,E023) and XDS  |
   |                      |             |      | Retrieval Sequence   |
   |                      |             |      | (0040,E024) are not  |
   |                      |             |      | present. May be      |
   |                      |             |      | present otherwise.   |
   |                      |             |      |                      |
   |                      |             |      | One or more Items    |
   |                      |             |      | shall be included in |
   |                      |             |      | this Sequence.       |
   +----------------------+-------------+------+----------------------+
   | >Retrieve URL        | (0008,1190) | 1    | URL specifying the   |
   |                      |             |      | location of the      |
   |                      |             |      | referenced           |
   |                      |             |      | Instance(s).         |
   +----------------------+-------------+------+----------------------+

`table_title <#table_10-3c>`__ contains details for where and how to
store Instances. It is intended to provide sufficient information to
store Instances to the correct location.

This Macro mirrors `table_title <#table_10-3b>`__.

.. table:: Storage Macro Attributes

   +----------------------+-------------+------+----------------------+
   | Attribute Name       | Tag         | Type | Attribute            |
   |                      |             |      | Description          |
   +======================+=============+======+======================+
   | Referenced SOP Class | (0008,1150) | 1C   | Uniquely identifies  |
   | UID                  |             |      | the referenced SOP   |
   |                      |             |      | Class.               |
   |                      |             |      |                      |
   |                      |             |      | Required if the      |
   |                      |             |      | storage request only |
   |                      |             |      | applies to a         |
   |                      |             |      | specific SOP Class.  |
   +----------------------+-------------+------+----------------------+
   | DICOM Storage        | (0040,4071) | 1C   | Details for storing  |
   | Sequence             |             |      | Instances via the    |
   |                      |             |      | DICOM Storage        |
   |                      |             |      | Service.             |
   |                      |             |      |                      |
   |                      |             |      | Required if STOW-RS  |
   |                      |             |      | Storage Sequence     |
   |                      |             |      | (0040,4072) or XDS   |
   |                      |             |      | Storage Sequence     |
   |                      |             |      | (0040,4074) is not   |
   |                      |             |      | present. May be      |
   |                      |             |      | present otherwise.   |
   |                      |             |      |                      |
   |                      |             |      | One or more Items    |
   |                      |             |      | shall be included in |
   |                      |             |      | this Sequence.       |
   +----------------------+-------------+------+----------------------+
   | >Destination AE      | (2100,0140) | 1    | Title of a DICOM     |
   |                      |             |      | Application Entity   |
   |                      |             |      | to which Instances   |
   |                      |             |      | will be stored.      |
   +----------------------+-------------+------+----------------------+
   | STOW-RS Storage      | (0040,4072) | 1C   | Details for storing  |
   | Sequence             |             |      | Instances via        |
   |                      |             |      | STOW-RS.             |
   |                      |             |      |                      |
   |                      |             |      | Required if DICOM    |
   |                      |             |      | Storage Sequence     |
   |                      |             |      | (0040,4071) and XDS  |
   |                      |             |      | Storage Sequence     |
   |                      |             |      | (0040,4074) are not  |
   |                      |             |      | present. May be      |
   |                      |             |      | present otherwise.   |
   |                      |             |      |                      |
   |                      |             |      | One or more Items    |
   |                      |             |      | shall be included in |
   |                      |             |      | this Sequence.       |
   +----------------------+-------------+------+----------------------+
   | >Storage URL         | (0040,4073) | 1    | URI/URL specifying   |
   |                      |             |      | the location of the  |
   |                      |             |      | STOW-RS storage      |
   |                      |             |      | service to which     |
   |                      |             |      | Instances will be    |
   |                      |             |      | stored.              |
   |                      |             |      |                      |
   |                      |             |      | The value shall be a |
   |                      |             |      | fully specified URI  |
   |                      |             |      | with protocol,       |
   |                      |             |      | authority and path,  |
   |                      |             |      | in accordance with   |
   |                      |             |      | `biblioentry_title < |
   |                      |             |      | #biblio_RFC_3986>`__ |
   |                      |             |      | and .                |
   +----------------------+-------------+------+----------------------+
   | XDS Storage Sequence | (0040,4074) | 1C   | Details for storing  |
   |                      |             |      | Instances via the    |
   |                      |             |      | IHE Provide and      |
   |                      |             |      | Register Document    |
   |                      |             |      | Set-b (ITI-41)       |
   |                      |             |      | transaction [IHE     |
   |                      |             |      | ITI-TF 2.b].         |
   |                      |             |      |                      |
   |                      |             |      | Required if STOW-RS  |
   |                      |             |      | Storage Sequence     |
   |                      |             |      | (0040,4072) and      |
   |                      |             |      | DICOM Storage        |
   |                      |             |      | Sequence (0040,4071) |
   |                      |             |      | are not present. May |
   |                      |             |      | be present           |
   |                      |             |      | otherwise.           |
   |                      |             |      |                      |
   |                      |             |      | One or more Items    |
   |                      |             |      | shall be included in |
   |                      |             |      | this Sequence.       |
   +----------------------+-------------+------+----------------------+
   | >Repository Unique   | (0040,E030) | 1    | Uniquely identifies  |
   | ID                   |             |      | a Repository from    |
   |                      |             |      | which the referenced |
   |                      |             |      | Instances can be     |
   |                      |             |      | retrieved.           |
   +----------------------+-------------+------+----------------------+
   | >Home Community ID   | (0040,E031) | 3    | Uniquely identifies  |
   |                      |             |      | a Community to which |
   |                      |             |      | requests for the     |
   |                      |             |      | referenced Instances |
   |                      |             |      | can be directed.     |
   +----------------------+-------------+------+----------------------+

.. _sect_10.4:

Series and Instance Reference Macro
-----------------------------------

`table_title <#table_10-4>`__ defines the Attributes that list Series
and SOP Instances within those Series.

.. table:: Series and Instance Reference Macro Attributes

   +----------------------+-------------+------+----------------------+
   | Attribute Name       | Tag         | Type | Attribute            |
   |                      |             |      | Description          |
   +======================+=============+======+======================+
   | Referenced Series    | (0008,1115) | 1    | Sequence of Items    |
   | Sequence             |             |      | each of which        |
   |                      |             |      | includes the         |
   |                      |             |      | Attributes of one    |
   |                      |             |      | Series.              |
   |                      |             |      |                      |
   |                      |             |      | One or more Items    |
   |                      |             |      | shall be included in |
   |                      |             |      | this Sequence.       |
   +----------------------+-------------+------+----------------------+
   | >Series Instance UID | (0020,000E) | 1    | Unique identifier of |
   |                      |             |      | the Series           |
   |                      |             |      | containing the       |
   |                      |             |      | referenced           |
   |                      |             |      | Instances.           |
   +----------------------+-------------+------+----------------------+
   | >Referenced Instance | (0008,114A) | 1    | Sequence of Items    |
   | Sequence             |             |      | each providing a     |
   |                      |             |      | reference to an      |
   |                      |             |      | Instance that is     |
   |                      |             |      | part of the Series   |
   |                      |             |      | defined by Series    |
   |                      |             |      | Instance UID         |
   |                      |             |      | (0020,000E) in the   |
   |                      |             |      | enclosing Item.      |
   |                      |             |      |                      |
   |                      |             |      | One or more Items    |
   |                      |             |      | shall be included in |
   |                      |             |      | this Sequence.       |
   +----------------------+-------------+------+----------------------+
   | *>>                  |             |      |                      |
   | Include*\ `table_tit |             |      |                      |
   | le <#table_10-11>`__ |             |      |                      |
   +----------------------+-------------+------+----------------------+

.. _sect_10.5:

General Anatomy Macros
----------------------

`table_title <#table_10-5>`__, `table_title <#table_10-6>`__,
`table_title <#table_10-7>`__ and `table_title <#table_10-7b>`__
describe the Attributes for identifying the general region of the
Patient anatomy examined using coded terminology, as well as the
principal structure(s) within that region that is the target of the
current SOP Instance. The only differences between the Macros are the
Type and Number of Items of the Anatomic Region Sequence (0008,2218)
Attribute. `table_title <#table_10-8>`__ describe the Attributes for the
coding of the principal structure only.

The invocation of these Macros may specify Baseline or Defined CIDs for
the Anatomic Region Sequence (0008,2218), the Anatomic Region Modifier
Sequence (0008,2220), and/or the Primary Anatomic Structure Sequence
(0008,2228).

The general region of the body (e.g., the anatomic region, organ, or
body cavity being examined) is identified by the Anatomic Region
Sequence (0008,2218). Characteristics of the anatomic region being
examined, such as sub-region (e.g., medial, lateral, superior, inferior,
lobe, quadrant) and laterality (e.g., right, left, both), may be refined
by the Anatomic Region Modifier Sequence (0008,2220).

.. note::

   These Attributes allow the specification of the information encoded
   by the Body Part Examined (0018,0015) in the `General Series
   Module <#sect_C.7.3.1>`__ in a more robust, consistent way.

The specific anatomic structures of interest within the image (e.g., a
particular artery within the anatomic region) is identified by the
Primary Anatomic Structure Sequence (0008,2228). Characteristics of the
anatomic structure, such as its location (e.g., subcapsular, peripheral,
central), configuration (e.g., distended, contracted), and laterality
(e.g., right, left, both), and so on, may be refined by the Primary
Anatomic Structure Modifier Sequence (0008,2230).

.. note::

   1. Laterality is often encoded in a separate Attribute, Image
      Laterality (0020,0062) or Frame Laterality (0020,9072), rather
      than in Anatomic Region Modifier Sequence (0008,2220) or Primary
      Anatomic Structure Modifier Sequence (0008,2230). The
      correspondence between the values is as follows:

      +----------------------------------+----------------------------------+
      | Image Laterality (0020,0062) or  | Coded Modifier                   |
      | Frame Laterality (0020,9072)     |                                  |
      +==================================+==================================+
      | L                                | `(7771000, SCT,                  |
      |                                  | "Left") <h                       |
      |                                  | ttp://snomed.info/id/7771000>`__ |
      +----------------------------------+----------------------------------+
      | R                                | `(24028007, SCT,                 |
      |                                  | "Right") <ht                     |
      |                                  | tp://snomed.info/id/24028007>`__ |
      +----------------------------------+----------------------------------+
      | U                                | `(66459002, SCT,                 |
      |                                  | "Unilateral") <ht                |
      |                                  | tp://snomed.info/id/66459002>`__ |
      +----------------------------------+----------------------------------+
      | B                                | `(51440002, SCT,                 |
      |                                  | "Bilateral") <ht                 |
      |                                  | tp://snomed.info/id/51440002>`__ |
      +----------------------------------+----------------------------------+

      The codes illustrated are from .

   2. Whether or not various anatomical structures may be paired or
      unpaired (have laterality) is illustrated in .

.. table:: General Anatomy Mandatory Macro Attributes

   +-------------------+-------------------+------+-------------------+
   | Attribute Name    | Tag               | Type | Attribute         |
   |                   |                   |      | Description       |
   +===================+===================+======+===================+
   | Anatomic Region   | (0008,2218)       | 1    | Sequence that     |
   | Sequence          |                   |      | identifies the    |
   |                   |                   |      | anatomic region   |
   |                   |                   |      | of interest in    |
   |                   |                   |      | this Instance     |
   |                   |                   |      | (i.e., external   |
   |                   |                   |      | anatomy, surface  |
   |                   |                   |      | anatomy, or       |
   |                   |                   |      | general region of |
   |                   |                   |      | the body).        |
   |                   |                   |      |                   |
   |                   |                   |      | Only a single     |
   |                   |                   |      | Item shall be     |
   |                   |                   |      | included in this  |
   |                   |                   |      | Sequence.         |
   +-------------------+-------------------+------+-------------------+
   | *>Includ          | *CID may be       |      |                   |
   | e*\ `table_title  | defined in the    |      |                   |
   | <#table_8.8-1>`__ | Macro             |      |                   |
   |                   | invocation.*      |      |                   |
   +-------------------+-------------------+------+-------------------+
   | >Anatomic Region  | (0008,2220)       | 3    | Sequence of Items |
   | Modifier Sequence |                   |      | that modifies the |
   |                   |                   |      | anatomic region   |
   |                   |                   |      | of interest of    |
   |                   |                   |      | this Instance.    |
   |                   |                   |      |                   |
   |                   |                   |      | One or more Items |
   |                   |                   |      | are permitted in  |
   |                   |                   |      | this Sequence.    |
   +-------------------+-------------------+------+-------------------+
   | *>>Includ         | *D, unless        |      |                   |
   | e*\ `table_title  | otherwise defined |      |                   |
   | <#table_8.8-1>`__ | in the Macro      |      |                   |
   |                   | invocation.*      |      |                   |
   +-------------------+-------------------+------+-------------------+
   | *Inclu            | *CID may be       |      |                   |
   | de*\ `table_title | defined in the    |      |                   |
   |  <#table_10-8>`__ | Macro             |      |                   |
   |                   | invocation.*      |      |                   |
   +-------------------+-------------------+------+-------------------+

.. table:: General Anatomy Required Macro Attributes

   +-------------------+-------------------+------+-------------------+
   | Attribute Name    | Tag               | Type | Attribute         |
   |                   |                   |      | Description       |
   +===================+===================+======+===================+
   | Anatomic Region   | (0008,2218)       | 2    | Sequence that     |
   | Sequence          |                   |      | identifies the    |
   |                   |                   |      | anatomic region   |
   |                   |                   |      | of interest in    |
   |                   |                   |      | this Instance     |
   |                   |                   |      | (i.e., external   |
   |                   |                   |      | anatomy, surface  |
   |                   |                   |      | anatomy, or       |
   |                   |                   |      | general region of |
   |                   |                   |      | the body).        |
   |                   |                   |      |                   |
   |                   |                   |      | Zero or one Item  |
   |                   |                   |      | shall be included |
   |                   |                   |      | in this Sequence. |
   +-------------------+-------------------+------+-------------------+
   | *>Includ          | *CID may be       |      |                   |
   | e*\ `table_title  | defined in the    |      |                   |
   | <#table_8.8-1>`__ | Macro             |      |                   |
   |                   | invocation.*      |      |                   |
   +-------------------+-------------------+------+-------------------+
   | >Anatomic Region  | (0008,2220)       | 3    | Sequence of Items |
   | Modifier Sequence |                   |      | that modifies the |
   |                   |                   |      | anatomic region   |
   |                   |                   |      | of interest of    |
   |                   |                   |      | this Instance     |
   |                   |                   |      |                   |
   |                   |                   |      | One or more Items |
   |                   |                   |      | are permitted in  |
   |                   |                   |      | this Sequence.    |
   +-------------------+-------------------+------+-------------------+
   | *>>Includ         | *D, unless        |      |                   |
   | e*\ `table_title  | otherwise defined |      |                   |
   | <#table_8.8-1>`__ | in the Macro      |      |                   |
   |                   | invocation.*      |      |                   |
   +-------------------+-------------------+------+-------------------+
   | *Inclu            | *CID may be       |      |                   |
   | de*\ `table_title | defined in the    |      |                   |
   |  <#table_10-8>`__ | Macro             |      |                   |
   |                   | invocation.*      |      |                   |
   +-------------------+-------------------+------+-------------------+

.. table:: General Anatomy Optional Macro Attributes

   +-------------------+-------------------+------+-------------------+
   | Attribute Name    | Tag               | Type | Attribute         |
   |                   |                   |      | Description       |
   +===================+===================+======+===================+
   | Anatomic Region   | (0008,2218)       | 3    | Sequence that     |
   | Sequence          |                   |      | identifies the    |
   |                   |                   |      | anatomic region   |
   |                   |                   |      | of interest in    |
   |                   |                   |      | this Instance     |
   |                   |                   |      | (i.e., external   |
   |                   |                   |      | anatomy, surface  |
   |                   |                   |      | anatomy, or       |
   |                   |                   |      | general region of |
   |                   |                   |      | the body).        |
   |                   |                   |      |                   |
   |                   |                   |      | Only a single     |
   |                   |                   |      | Item is permitted |
   |                   |                   |      | in this Sequence. |
   +-------------------+-------------------+------+-------------------+
   | *>Includ          | *CID may be       |      |                   |
   | e*\ `table_title  | defined in the    |      |                   |
   | <#table_8.8-1>`__ | Macro             |      |                   |
   |                   | invocation.*      |      |                   |
   +-------------------+-------------------+------+-------------------+
   | >Anatomic Region  | (0008,2220)       | 3    | Sequence of Items |
   | Modifier Sequence |                   |      | that modifies the |
   |                   |                   |      | anatomic region   |
   |                   |                   |      | of interest of    |
   |                   |                   |      | this Instance     |
   |                   |                   |      |                   |
   |                   |                   |      | One or more Items |
   |                   |                   |      | are permitted in  |
   |                   |                   |      | this Sequence.    |
   +-------------------+-------------------+------+-------------------+
   | *>>Includ         | *D, unless        |      |                   |
   | e*\ `table_title  | otherwise defined |      |                   |
   | <#table_8.8-1>`__ | in the Macro      |      |                   |
   |                   | invocation.*      |      |                   |
   +-------------------+-------------------+------+-------------------+
   | *Inclu            | *CID may be       |      |                   |
   | de*\ `table_title | defined in the    |      |                   |
   |  <#table_10-8>`__ | Macro             |      |                   |
   |                   | invocation.*      |      |                   |
   +-------------------+-------------------+------+-------------------+

.. table:: Multiple Site General Anatomy Optional Macro Attributes

   +-------------------+-------------------+------+-------------------+
   | Attribute Name    | Tag               | Type | Attribute         |
   |                   |                   |      | Description       |
   +===================+===================+======+===================+
   | Anatomic Region   | (0008,2218)       | 3    | Sequence that     |
   | Sequence          |                   |      | identifies the    |
   |                   |                   |      | anatomic region   |
   |                   |                   |      | of interest in    |
   |                   |                   |      | this Instance     |
   |                   |                   |      | (i.e., external   |
   |                   |                   |      | anatomy, surface  |
   |                   |                   |      | anatomy, or       |
   |                   |                   |      | general region of |
   |                   |                   |      | the body).        |
   |                   |                   |      |                   |
   |                   |                   |      | One or more Items |
   |                   |                   |      | are permitted in  |
   |                   |                   |      | this Sequence.    |
   +-------------------+-------------------+------+-------------------+
   | *>Includ          | *CID may be       |      |                   |
   | e*\ `table_title  | defined in the    |      |                   |
   | <#table_8.8-1>`__ | Macro             |      |                   |
   |                   | invocation.*      |      |                   |
   +-------------------+-------------------+------+-------------------+
   | >Anatomic Region  | (0008,2220)       | 3    | Sequence of Items |
   | Modifier Sequence |                   |      | that modifies the |
   |                   |                   |      | anatomic region   |
   |                   |                   |      | of interest in    |
   |                   |                   |      | this Instance     |
   |                   |                   |      |                   |
   |                   |                   |      | One or more Items |
   |                   |                   |      | are permitted in  |
   |                   |                   |      | this Sequence.    |
   +-------------------+-------------------+------+-------------------+
   | *>>Includ         | *D, unless        |      |                   |
   | e*\ `table_title  | otherwise defined |      |                   |
   | <#table_8.8-1>`__ | in the Macro      |      |                   |
   |                   | invocation.*      |      |                   |
   +-------------------+-------------------+------+-------------------+
   | *Inclu            | *CID may be       |      |                   |
   | de*\ `table_title | defined in the    |      |                   |
   |  <#table_10-8>`__ | Macro             |      |                   |
   |                   | invocation.*      |      |                   |
   +-------------------+-------------------+------+-------------------+

.. table:: Primary Anatomic Structure Macro Attributes

   +-------------------+-------------------+------+-------------------+
   | Attribute Name    | Tag               | Type | Attribute         |
   |                   |                   |      | Description       |
   +===================+===================+======+===================+
   | Primary Anatomic  | (0008,2228)       | 3    | Sequence of Items |
   | Structure         |                   |      | that identifies   |
   | Sequence          |                   |      | the primary       |
   |                   |                   |      | anatomic          |
   |                   |                   |      | structure(s) of   |
   |                   |                   |      | interest in this  |
   |                   |                   |      | Instance.         |
   |                   |                   |      |                   |
   |                   |                   |      | One or more Items |
   |                   |                   |      | are permitted in  |
   |                   |                   |      | this Sequence.    |
   +-------------------+-------------------+------+-------------------+
   | *>Includ          | *CID may be       |      |                   |
   | e*\ `table_title  | defined in the    |      |                   |
   | <#table_8.8-1>`__ | Macro             |      |                   |
   |                   | invocation.*      |      |                   |
   +-------------------+-------------------+------+-------------------+
   | >Primary Anatomic | (0008,2230)       | 3    | Sequence of Items |
   | Structure         |                   |      | that modifies the |
   | Modifier Sequence |                   |      | primary anatomic  |
   |                   |                   |      | structure of      |
   |                   |                   |      | interest in this  |
   |                   |                   |      | Instance.         |
   |                   |                   |      |                   |
   |                   |                   |      | One or more Items |
   |                   |                   |      | are permitted in  |
   |                   |                   |      | this Sequence.    |
   +-------------------+-------------------+------+-------------------+
   | *>>Includ         | *D.*              |      |                   |
   | e*\ `table_title  |                   |      |                   |
   | <#table_8.8-1>`__ |                   |      |                   |
   +-------------------+-------------------+------+-------------------+

.. _sect_10.6:

Request Attributes Macro
------------------------

.. table:: Request Attributes Macro Attributes

   +-------------------+-------------------+------+-------------------+
   | Attribute Name    | Tag               | Type | Attribute         |
   |                   |                   |      | Description       |
   +===================+===================+======+===================+
   | Requested         | (0040,1001)       | 1C   | Identifier that   |
   | Procedure ID      |                   |      | identifies the    |
   |                   |                   |      | Requested         |
   |                   |                   |      | Procedure in the  |
   |                   |                   |      | Imaging Service   |
   |                   |                   |      | Request.          |
   |                   |                   |      |                   |
   |                   |                   |      | Required if       |
   |                   |                   |      | procedure was     |
   |                   |                   |      | scheduled. May be |
   |                   |                   |      | present           |
   |                   |                   |      | otherwise.        |
   |                   |                   |      |                   |
   |                   |                   |      | .. note::         |
   |                   |                   |      |                   |
   |                   |                   |      |    The condition  |
   |                   |                   |      |    is to allow    |
   |                   |                   |      |    the contents   |
   |                   |                   |      |    of this Macro  |
   |                   |                   |      |    to be present  |
   |                   |                   |      |    (e.g., to      |
   |                   |                   |      |    convey the     |
   |                   |                   |      |    reason for the |
   |                   |                   |      |    procedure,     |
   |                   |                   |      |    such as        |
   |                   |                   |      |    whether a      |
   |                   |                   |      |    mammogram is   |
   |                   |                   |      |    for screening  |
   |                   |                   |      |    or diagnostic  |
   |                   |                   |      |    purposes) even |
   |                   |                   |      |    when the       |
   |                   |                   |      |    procedure was  |
   |                   |                   |      |    not formally   |
   |                   |                   |      |    scheduled and  |
   |                   |                   |      |    a value for    |
   |                   |                   |      |    this           |
   |                   |                   |      |    identifier is  |
   |                   |                   |      |    unknown,       |
   |                   |                   |      |    rather than    |
   |                   |                   |      |    making up a    |
   |                   |                   |      |    dummy value.   |
   +-------------------+-------------------+------+-------------------+
   | Accession Number  | (0008,0050)       | 3    | An identifier of  |
   |                   |                   |      | the Imaging       |
   |                   |                   |      | Service Request   |
   |                   |                   |      | for this          |
   |                   |                   |      | Requested         |
   |                   |                   |      | Procedure.        |
   +-------------------+-------------------+------+-------------------+
   | Issuer of         | (0008,0051)       | 3    | Identifier of the |
   | Accession Number  |                   |      | Assigning         |
   | Sequence          |                   |      | Authority that    |
   |                   |                   |      | issued the        |
   |                   |                   |      | Accession Number. |
   |                   |                   |      |                   |
   |                   |                   |      | Only a single     |
   |                   |                   |      | Item is permitted |
   |                   |                   |      | in this Sequence. |
   +-------------------+-------------------+------+-------------------+
   | *>Includ          |                   |      |                   |
   | e*\ `table_title  |                   |      |                   |
   | <#table_10-17>`__ |                   |      |                   |
   +-------------------+-------------------+------+-------------------+
   | Study Instance    | (0020,000D)       | 3    | The unique        |
   | UID               |                   |      | identifier for    |
   |                   |                   |      | the Study         |
   |                   |                   |      | provided for this |
   |                   |                   |      | Requested         |
   |                   |                   |      | Procedure.        |
   +-------------------+-------------------+------+-------------------+
   | Referenced Study  | (0008,1110)       | 3    | Uniquely          |
   | Sequence          |                   |      | identifies the    |
   |                   |                   |      | Study SOP         |
   |                   |                   |      | Instances         |
   |                   |                   |      | associated with   |
   |                   |                   |      | this SOP          |
   |                   |                   |      | Instance.         |
   |                   |                   |      |                   |
   |                   |                   |      | One or more Items |
   |                   |                   |      | are permitted in  |
   |                   |                   |      | this Sequence.    |
   |                   |                   |      |                   |
   |                   |                   |      | See `SOP Class    |
   |                   |                   |      | UID in Referenced |
   |                   |                   |      | Study             |
   |                   |                   |      | Sequence <        |
   |                   |                   |      | #sect_10.6.1>`__. |
   +-------------------+-------------------+------+-------------------+
   | *>Includ          |                   |      |                   |
   | e*\ `table_title  |                   |      |                   |
   | <#table_10-11>`__ |                   |      |                   |
   +-------------------+-------------------+------+-------------------+
   | Requested         | (0032,1060)       | 3    | Inst              |
   | Procedure         |                   |      | itution-generated |
   | Description       |                   |      | administrative    |
   |                   |                   |      | description or    |
   |                   |                   |      | classification of |
   |                   |                   |      | Requested         |
   |                   |                   |      | Procedure.        |
   +-------------------+-------------------+------+-------------------+
   | Requested         | (0032,1064)       | 3    | A Sequence that   |
   | Procedure Code    |                   |      | conveys the       |
   | Sequence          |                   |      | Procedure Type of |
   |                   |                   |      | the requested     |
   |                   |                   |      | procedure.        |
   |                   |                   |      |                   |
   |                   |                   |      | Only a single     |
   |                   |                   |      | Item is permitted |
   |                   |                   |      | in this Sequence. |
   +-------------------+-------------------+------+-------------------+
   | *>Includ          | *No Baseline CID  |      |                   |
   | e*\ `table_title  | is defined.*      |      |                   |
   | <#table_8.8-1>`__ |                   |      |                   |
   +-------------------+-------------------+------+-------------------+
   | Reason for the    | (0040,1002)       | 3    | Reason for        |
   | Requested         |                   |      | requesting this   |
   | Procedure         |                   |      | procedure.        |
   +-------------------+-------------------+------+-------------------+
   | Reason for        | (0040,100A)       | 3    | Coded Reason for  |
   | Requested         |                   |      | requesting this   |
   | Procedure Code    |                   |      | procedure.        |
   | Sequence          |                   |      |                   |
   |                   |                   |      | One or more Items |
   |                   |                   |      | are permitted in  |
   |                   |                   |      | this Sequence.    |
   +-------------------+-------------------+------+-------------------+
   | *>Includ          | *CID may be       |      |                   |
   | e*\ `table_title  | defined in the    |      |                   |
   | <#table_8.8-1>`__ | Macro             |      |                   |
   |                   | invocation.*      |      |                   |
   +-------------------+-------------------+------+-------------------+
   | Scheduled         | (0040,0009)       | 1C   | Identifier that   |
   | Procedure Step ID |                   |      | identifies the    |
   |                   |                   |      | Scheduled         |
   |                   |                   |      | Procedure Step.   |
   |                   |                   |      |                   |
   |                   |                   |      | Required if       |
   |                   |                   |      | procedure was     |
   |                   |                   |      | scheduled.        |
   |                   |                   |      |                   |
   |                   |                   |      | .. note::         |
   |                   |                   |      |                   |
   |                   |                   |      |    The condition  |
   |                   |                   |      |    is to allow    |
   |                   |                   |      |    the contents   |
   |                   |                   |      |    of this Macro  |
   |                   |                   |      |    to be present  |
   |                   |                   |      |    (e.g., to      |
   |                   |                   |      |    convey the     |
   |                   |                   |      |    reason for the |
   |                   |                   |      |    procedure,     |
   |                   |                   |      |    such as        |
   |                   |                   |      |    whether a      |
   |                   |                   |      |    mammogram is   |
   |                   |                   |      |    for screening  |
   |                   |                   |      |    or diagnostic  |
   |                   |                   |      |    purposes) even |
   |                   |                   |      |    when the       |
   |                   |                   |      |    procedure step |
   |                   |                   |      |    was not        |
   |                   |                   |      |    formally       |
   |                   |                   |      |    scheduled and  |
   |                   |                   |      |    a value for    |
   |                   |                   |      |    this           |
   |                   |                   |      |    identifier is  |
   |                   |                   |      |    unknown,       |
   |                   |                   |      |    rather than    |
   |                   |                   |      |    making up a    |
   |                   |                   |      |    dummy value.   |
   +-------------------+-------------------+------+-------------------+
   | Scheduled         | (0040,0007)       | 3    | Inst              |
   | Procedure Step    |                   |      | itution-generated |
   | Description       |                   |      | description or    |
   |                   |                   |      | classification of |
   |                   |                   |      | the Scheduled     |
   |                   |                   |      | Procedure Step to |
   |                   |                   |      | be performed.     |
   +-------------------+-------------------+------+-------------------+
   | Scheduled         | (0040,0008)       | 3    | Sequence          |
   | Protocol Code     |                   |      | describing the    |
   | Sequence          |                   |      | Scheduled         |
   |                   |                   |      | Protocol          |
   |                   |                   |      | following a       |
   |                   |                   |      | specific coding   |
   |                   |                   |      | scheme. One or    |
   |                   |                   |      | more Items are    |
   |                   |                   |      | permitted in this |
   |                   |                   |      | Sequence.         |
   +-------------------+-------------------+------+-------------------+
   | *>Includ          | *CID may be       |      |                   |
   | e*\ `table_title  | defined in the    |      |                   |
   | <#table_8.8-1>`__ | Macro             |      |                   |
   |                   | invocation.*      |      |                   |
   +-------------------+-------------------+------+-------------------+
   | >Protocol Context | (0040,0440)       | 3    | Sequence that     |
   | Sequence          |                   |      | specifies the     |
   |                   |                   |      | context for the   |
   |                   |                   |      | Scheduled         |
   |                   |                   |      | Protocol Code     |
   |                   |                   |      | Sequence          |
   |                   |                   |      | (0040,0008) Item. |
   |                   |                   |      | One or more Items |
   |                   |                   |      | are permitted in  |
   |                   |                   |      | this Sequence.    |
   +-------------------+-------------------+------+-------------------+
   | *>>Inclu          | *CID may be       |      |                   |
   | de*\ `table_title | defined in the    |      |                   |
   |  <#table_10-2>`__ | Macro             |      |                   |
   |                   | invocation.*      |      |                   |
   +-------------------+-------------------+------+-------------------+
   | >>Content Item    | (0040,0441)       | 3    | Sequence that     |
   | Modifier Sequence |                   |      | specifies         |
   |                   |                   |      | modifiers for a   |
   |                   |                   |      | Protocol Context  |
   |                   |                   |      | Content Item.     |
   |                   |                   |      |                   |
   |                   |                   |      | One or more Items |
   |                   |                   |      | are permitted in  |
   |                   |                   |      | this Sequence.    |
   |                   |                   |      |                   |
   |                   |                   |      | See `Protocol     |
   |                   |                   |      | Context           |
   |                   |                   |      | Sequence <#s      |
   |                   |                   |      | ect_C.4.10.1>`__. |
   +-------------------+-------------------+------+-------------------+
   | *>>>Inclu         | *CID may be       |      |                   |
   | de*\ `table_title | defined in the    |      |                   |
   |  <#table_10-2>`__ | Macro             |      |                   |
   |                   | invocation.*      |      |                   |
   +-------------------+-------------------+------+-------------------+

.. _sect_10.6.1:

SOP Class UID in Referenced Study Sequence
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Since Referenced Study Sequence (0008,1110) is Type 2 or 3 in each
usage, the Attribute may be zero length or omitted, respectively.

If Referenced Study Sequence (0008,1110) is present with an Item, the
SOP Class UID of the Detached Study Management SOP Class (Retired) may
be used in Referenced SOP Class UID (0008,1150).

.. _sect_10.7:

Basic Pixel Spacing Calibration Macro
-------------------------------------

`table_title <#table_10-10>`__ defines the Attributes for the Basic
Pixel Spacing Calibration Macro.

.. table:: Basic Pixel Spacing Calibration Macro Attributes

   +----------------------+-------------+------+----------------------+
   | Attribute Name       | Tag         | Type | Attribute            |
   |                      |             |      | Description          |
   +======================+=============+======+======================+
   | Pixel Spacing        | (0028,0030) | 1C   | Physical distance in |
   |                      |             |      | the Patient between  |
   |                      |             |      | the center of each   |
   |                      |             |      | pixel, specified by  |
   |                      |             |      | a numeric pair -     |
   |                      |             |      | adjacent row spacing |
   |                      |             |      | (delimiter) adjacent |
   |                      |             |      | column spacing in    |
   |                      |             |      | mm. See `Pixel       |
   |                      |             |      | Spacing              |
   |                      |             |      |  <#sect_10.7.1.1>`__ |
   |                      |             |      | and `Pixel Spacing   |
   |                      |             |      | Value Order and      |
   |                      |             |      | Valid                |
   |                      |             |      | Values               |
   |                      |             |      | <#sect_10.7.1.3>`__. |
   |                      |             |      | Required if the      |
   |                      |             |      | image has been       |
   |                      |             |      | calibrated. May be   |
   |                      |             |      | present otherwise.   |
   +----------------------+-------------+------+----------------------+
   | Pixel Spacing        | (0028,0A02) | 3    | The type of          |
   | Calibration Type     |             |      | correction for the   |
   |                      |             |      | effect of geometric  |
   |                      |             |      | magnification or     |
   |                      |             |      | calibration against  |
   |                      |             |      | an object of known   |
   |                      |             |      | size, if any. See    |
   |                      |             |      | `Pixel Spacing       |
   |                      |             |      | Calibration          |
   |                      |             |      | Type                 |
   |                      |             |      | <#sect_10.7.1.2>`__. |
   +----------------------+-------------+------+----------------------+
   | Pixel Spacing        | (0028,0A04) | 1C   | A free text          |
   | Calibration          |             |      | description of the   |
   | Description          |             |      | type of correction   |
   |                      |             |      | or calibration       |
   |                      |             |      | performed.           |
   |                      |             |      |                      |
   |                      |             |      | .. note::            |
   |                      |             |      |                      |
   |                      |             |      |    1. In the case of |
   |                      |             |      |       correction,    |
   |                      |             |      |       the text might |
   |                      |             |      |       include        |
   |                      |             |      |       description of |
   |                      |             |      |       the            |
   |                      |             |      |       assumptions    |
   |                      |             |      |       made about the |
   |                      |             |      |       body part and  |
   |                      |             |      |       geometry and   |
   |                      |             |      |       depth within   |
   |                      |             |      |       the Patient.   |
   |                      |             |      |                      |
   |                      |             |      |    2. in the case of |
   |                      |             |      |       calibration,   |
   |                      |             |      |       the text might |
   |                      |             |      |       include a      |
   |                      |             |      |       description of |
   |                      |             |      |       the fiducial   |
   |                      |             |      |       and where it   |
   |                      |             |      |       is located     |
   |                      |             |      |       (e.g., "XYZ    |
   |                      |             |      |       device applied |
   |                      |             |      |       to the skin    |
   |                      |             |      |       over the       |
   |                      |             |      |       greater        |
   |                      |             |      |       trochanter").  |
   |                      |             |      |                      |
   |                      |             |      |    3. Though it is   |
   |                      |             |      |       not required,  |
   |                      |             |      |       the `Device    |
   |                      |             |      |       Module         |
   |                      |             |      |  <#sect_C.7.6.12>`__ |
   |                      |             |      |       may be used to |
   |                      |             |      |       describe the   |
   |                      |             |      |       specific       |
   |                      |             |      |                      |
   |                      |             |      |      characteristics |
   |                      |             |      |       and size of    |
   |                      |             |      |       the            |
   |                      |             |      |       calibration    |
   |                      |             |      |       device.        |
   |                      |             |      |                      |
   |                      |             |      | Required if Pixel    |
   |                      |             |      | Spacing Calibration  |
   |                      |             |      | Type (0028,0A02) is  |
   |                      |             |      | present.             |
   +----------------------+-------------+------+----------------------+

.. _sect_10.7.1:

Basic Pixel Spacing Calibration Macro Attribute Descriptions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. _sect_10.7.1.1:

Pixel Spacing
^^^^^^^^^^^^^

Pixel Spacing (0028,0030) specifies the physical distance in the Patient
between the center of each pixel.

If Pixel Spacing (0028,0030) is present and the image has not been
calibrated to correct for the effect of geometric magnification, the
values of this Attribute shall be the same as in Imager Pixel Spacing
(0018,1164) or Nominal Scanned Pixel Spacing (0018,2010), if either of
those Attributes are present.

If Pixel Spacing (0028,0030) is present and the values are different
from those in Imager Pixel Spacing (0018,1164) or Nominal Scanned Pixel
Spacing (0018,2010), then the image has been corrected for known or
assumed geometric magnification or calibrated with respect to some
object of known size at known depth within the Patient.

If Pixel Spacing Calibration Type (0028,0A02) and Imager Pixel Spacing
(0018,1164) and Nominal Scanned Pixel Spacing (0018,2010) are absent,
then it cannot be determined whether or not correction or calibration
have been performed.

.. note::

   1. Imager Pixel Spacing (0018,1164) is a required Attribute in DX
      family IODs.

   2. Nominal Scanned Pixel Spacing (0018,2010) is a required Attribute
      in Multi-frame SC family IODs

.. _sect_10.7.1.2:

Pixel Spacing Calibration Type
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Pixel Spacing Calibration Type (0028,0A02) Attribute specifies the
type of correction for the effect of geometric magnification or
calibration against an object of known size, if any.

GEOMETRY
   The Pixel Spacing (0028,0030) values account for assumed or known
   geometric magnification effects and correspond to some unspecified
   depth within the Patient; the Pixel Spacing (0028,0030) values may
   thus be used for measurements of objects located close to the central
   ray and at the same depth.

FIDUCIAL
   The Pixel Spacing (0028,0030) values have been calibrated by the
   operator or image processing software by measurement of an object
   (fiducial) that is visible in the pixel data and is of known size and
   is located close to the central ray; the Pixel Spacing (0028,0030)
   values may thus be used for measurements of objects located close to
   the central ray and located at the same depth within the Patient as
   the fiducial.

.. _sect_10.7.1.3:

Pixel Spacing Value Order and Valid Values
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

All pixel spacing related Attributes are encoded as the physical
distance between the centers of each two-dimensional pixel, specified by
two numeric values.

The first value is the row spacing in mm, that is the spacing between
the centers of adjacent rows, or vertical spacing.

The second value is the column spacing in mm, that is the spacing
between the centers of adjacent columns, or horizontal spacing.

To illustrate, consider the example shown in
`figure_title <#figure_10.7.1.3-1>`__.

Pixel Spacing = Row Spacing \\ Column Spacing = 0.30\0.25.

All pixel spacing related Attributes shall have positive non-zero
values, except when there is only a single row or column or pixel of
data present, in which case the corresponding value may be zero.

.. note::

   A single row or column or "pixel" may occur in MR Spectroscopy
   Instances.

This description applies to:

-  Pixel Spacing (0028,0030)

-  Imager Pixel Spacing (0018,1164)

-  Nominal Scanned Pixel Spacing (0018,2010)

-  Image Plane Pixel Spacing (3002,0011)

-  Compensator Pixel Spacing (300A,00E9)

-  Detector Element Spacing (0018,7022)

-  Presentation Pixel Spacing (0070,0101)

-  Printer Pixel Spacing (2010,0376)

-  Object Pixel Spacing in Center of Beam (0018,9404)

.. _sect_10.8:

SOP Instance Reference Macro
----------------------------

`table_title <#table_10-11>`__ specifies the Attributes that reference
an SOP Instance.

.. table:: SOP Instance Reference Macro Attributes

   +----------------------+-------------+------+----------------------+
   | Attribute Name       | Tag         | Type | Description          |
   +======================+=============+======+======================+
   | Referenced SOP Class | (0008,1150) | 1    | Uniquely identifies  |
   | UID                  |             |      | the referenced SOP   |
   |                      |             |      | Class.               |
   +----------------------+-------------+------+----------------------+
   | Referenced SOP       | (0008,1155) | 1    | Uniquely identifies  |
   | Instance UID         |             |      | the referenced SOP   |
   |                      |             |      | Instance.            |
   +----------------------+-------------+------+----------------------+

.. _sect_10.9:

Content Identification Macro
----------------------------

`table_title <#table_10-12>`__ describe the Attributes for identifying a
SOP Instance potentially created by a human user interacting with an
application.

.. table:: Content Identification Macro Attributes

   +-------------------+-------------------+------+-------------------+
   | Attribute Name    | Tag               | Type | Attribute         |
   |                   |                   |      | Description       |
   +===================+===================+======+===================+
   | Instance Number   | (0020,0013)       | 1    | A number that     |
   |                   |                   |      | identifies this   |
   |                   |                   |      | SOP Instance.     |
   +-------------------+-------------------+------+-------------------+
   | Content Label     | (0070,0080)       | 1    | A label that is   |
   |                   |                   |      | used to identify  |
   |                   |                   |      | this SOP          |
   |                   |                   |      | Instance.         |
   +-------------------+-------------------+------+-------------------+
   | Content           | (0070,0081)       | 2    | A description of  |
   | Description       |                   |      | the content of    |
   |                   |                   |      | the SOP Instance. |
   +-------------------+-------------------+------+-------------------+
   | Concept Name Code | (0040,A043)       | 3    | A coded           |
   | Sequence          |                   |      | description of    |
   |                   |                   |      | the content of    |
   |                   |                   |      | the SOP Instance. |
   |                   |                   |      |                   |
   |                   |                   |      | Only a single     |
   |                   |                   |      | Item is permitted |
   |                   |                   |      | in this Sequence. |
   +-------------------+-------------------+------+-------------------+
   | *>Includ          | *No Baseline CID  |      |                   |
   | e*\ `table_title  | is defined.*      |      |                   |
   | <#table_8.8-1>`__ |                   |      |                   |
   +-------------------+-------------------+------+-------------------+
   | Alternate Content | (0070,0087)       | 3    | A Sequence        |
   | Description       |                   |      | containing        |
   | Sequence          |                   |      | alternate         |
   |                   |                   |      | descriptions      |
   |                   |                   |      | suitable for      |
   |                   |                   |      | presentation to   |
   |                   |                   |      | the user, e.g.,   |
   |                   |                   |      | in different      |
   |                   |                   |      | languages. One or |
   |                   |                   |      | more Items are    |
   |                   |                   |      | permitted in this |
   |                   |                   |      | Sequence.         |
   |                   |                   |      |                   |
   |                   |                   |      | .. note::         |
   |                   |                   |      |                   |
   |                   |                   |      |    The values of  |
   |                   |                   |      |    Specific       |
   |                   |                   |      |    Character Set  |
   |                   |                   |      |    for the entire |
   |                   |                   |      |    Data Set need  |
   |                   |                   |      |    to be          |
   |                   |                   |      |    sufficient to  |
   |                   |                   |      |    encode all     |
   |                   |                   |      |    Items of this  |
   |                   |                   |      |    Sequence       |
   |                   |                   |      |    correctly,     |
   |                   |                   |      |    e.g., using a  |
   |                   |                   |      |    single value   |
   |                   |                   |      |    with broad     |
   |                   |                   |      |    support such   |
   |                   |                   |      |    as UTF-8, or   |
   |                   |                   |      |    multiple       |
   |                   |                   |      |    values with    |
   |                   |                   |      |    escape         |
   |                   |                   |      |    sequences.     |
   +-------------------+-------------------+------+-------------------+
   | >Content          | (0070,0081)       | 1    | An alternate      |
   | Description       |                   |      | description that  |
   |                   |                   |      | is used to        |
   |                   |                   |      | identify this SOP |
   |                   |                   |      | Instance.         |
   +-------------------+-------------------+------+-------------------+
   | >Language Code    | (0008,0006)       | 1    | The language in   |
   | Sequence          |                   |      | which Content     |
   |                   |                   |      | Description       |
   |                   |                   |      | (0070,0081)       |
   |                   |                   |      | within this Item  |
   |                   |                   |      | is written. A     |
   |                   |                   |      | single Item shall |
   |                   |                   |      | be present.       |
   +-------------------+-------------------+------+-------------------+
   | *>>Includ         | *D.*              |      |                   |
   | e*\ `table_title  |                   |      |                   |
   | <#table_8.8-1>`__ |                   |      |                   |
   +-------------------+-------------------+------+-------------------+
   | >Concept Name     | (0040,A043)       | 3    | An alternate      |
   | Code Sequence     |                   |      | coded description |
   |                   |                   |      | of the content of |
   |                   |                   |      | the SOP Instance. |
   |                   |                   |      |                   |
   |                   |                   |      | Only a single     |
   |                   |                   |      | Item is permitted |
   |                   |                   |      | in this Sequence. |
   +-------------------+-------------------+------+-------------------+
   | *>>Includ         | *No Baseline CID  |      |                   |
   | e*\ `table_title  | is defined.*      |      |                   |
   | <#table_8.8-1>`__ |                   |      |                   |
   +-------------------+-------------------+------+-------------------+
   | Content Creator's | (0070,0084)       | 2    | Name of operator  |
   | Name              |                   |      | (such as a        |
   |                   |                   |      | technologist or   |
   |                   |                   |      | physician)        |
   |                   |                   |      | creating the      |
   |                   |                   |      | content of the    |
   |                   |                   |      | SOP Instance.     |
   +-------------------+-------------------+------+-------------------+
   | Content Creator's | (0070,0086)       | 3    | Identification of |
   | Identification    |                   |      | the person who    |
   | Code Sequence     |                   |      | created the       |
   |                   |                   |      | content. Only a   |
   |                   |                   |      | single Item is    |
   |                   |                   |      | permitted in this |
   |                   |                   |      | Sequence.         |
   +-------------------+-------------------+------+-------------------+
   | *>Inclu           |                   |      |                   |
   | de*\ `table_title |                   |      |                   |
   |  <#table_10-1>`__ |                   |      |                   |
   +-------------------+-------------------+------+-------------------+

.. _sect_10.9.1:

Enhanced Content Identification Macro
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Enhanced Content Identification Macro identifies content using a
label supporting lower case characters and specified character sets. If
a Code String is required, see `Content Identification
Macro <#sect_10.9>`__.

.. table:: Enhanced Content Identification Macro Attributes

   +----------------------+-------------+------+----------------------+
   | Attribute Name       | Tag         | Type | Attribute            |
   |                      |             |      | Description          |
   +======================+=============+======+======================+
   | User Content Label   | (3010,0033) | 1    | User-defined label   |
   |                      |             |      | for this SOP         |
   |                      |             |      | Instance.            |
   |                      |             |      |                      |
   |                      |             |      | See `User Content    |
   |                      |             |      | Label and Content    |
   |                      |             |      | Description <#       |
   |                      |             |      | sect_10.9.1.1.1>`__. |
   +----------------------+-------------+------+----------------------+
   | Content Description  | (0070,0081) | 2    | User-defined         |
   |                      |             |      | description for the  |
   |                      |             |      | content of this SOP  |
   |                      |             |      | Instance.            |
   |                      |             |      |                      |
   |                      |             |      | See `User Content    |
   |                      |             |      | Label and Content    |
   |                      |             |      | Description <#       |
   |                      |             |      | sect_10.9.1.1.1>`__. |
   +----------------------+-------------+------+----------------------+
   | Content Creator"s    | (0070,0084) | 2    | Name of operator     |
   | Name                 |             |      | (such as a           |
   |                      |             |      | technologist or      |
   |                      |             |      | physician) creating  |
   |                      |             |      | the content of the   |
   |                      |             |      | SOP Instance.        |
   +----------------------+-------------+------+----------------------+
   | Content Creator"s    | (0070,0086) | 3    | Identification of    |
   | Identification Code  |             |      | the person who       |
   | Sequence             |             |      | created the content. |
   |                      |             |      |                      |
   |                      |             |      | Only a single Item   |
   |                      |             |      | is permitted in this |
   |                      |             |      | Sequence.            |
   +----------------------+-------------+------+----------------------+
   | *                    |             |      |                      |
   | >Include*\ `table_ti |             |      |                      |
   | tle <#table_10-1>`__ |             |      |                      |
   +----------------------+-------------+------+----------------------+

.. _sect_10.9.1.1:

Enhanced Content Identification Macro Attribute Descriptions
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. _sect_10.9.1.1.1:

User Content Label and Content Description
''''''''''''''''''''''''''''''''''''''''''

User Content Label (3010,0033) shall represent a user-defined short free
text providing the primary identification of this entity to other users.
Content Description (0070,0081) allows a longer string containing
additional descriptive identifying text.

This information is intended for display to human readers. Shall not be
used for structured processing.

.. _sect_10.9.2:

Extended Content Identification Macro
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Extended Content Identification Macro identifies content using a
label supporting lower case characters and specified character sets. If
a Code String is required, see `Content Identification
Macro <#sect_10.9>`__.

.. table:: Extended Content Identification Macro Attributes

   +----------------------+-------------+------+----------------------+
   | Attribute Name       | Tag         | Type | Attribute            |
   |                      |             |      | Description          |
   +======================+=============+======+======================+
   | User Content Long    | (3010,0034) | 1    | User-defined label   |
   | Label                |             |      | for the content of   |
   |                      |             |      | this SOP Instance.   |
   |                      |             |      |                      |
   |                      |             |      | See `User Content    |
   |                      |             |      | Long Label and       |
   |                      |             |      | Content              |
   |                      |             |      | Description <#       |
   |                      |             |      | sect_10.9.2.1.1>`__. |
   +----------------------+-------------+------+----------------------+
   | Content Description  | (0070,0081) | 2    | User-defined         |
   |                      |             |      | description for the  |
   |                      |             |      | content of this SOP  |
   |                      |             |      | Instance.            |
   |                      |             |      |                      |
   |                      |             |      | See `User Content    |
   |                      |             |      | Long Label and       |
   |                      |             |      | Content              |
   |                      |             |      | Description <#       |
   |                      |             |      | sect_10.9.2.1.1>`__. |
   +----------------------+-------------+------+----------------------+
   | Content Creator's    | (0070,0084) | 2    | Name of operator     |
   | Name                 |             |      | (such as a           |
   |                      |             |      | technologist or      |
   |                      |             |      | physician) creating  |
   |                      |             |      | the content of the   |
   |                      |             |      | SOP Instance.        |
   +----------------------+-------------+------+----------------------+
   | Content Creator's    | (0070,0086) | 3    | Identification of    |
   | Identification Code  |             |      | the person who       |
   | Sequence             |             |      | created the content. |
   |                      |             |      |                      |
   |                      |             |      | Only a single Item   |
   |                      |             |      | is permitted in this |
   |                      |             |      | Sequence.            |
   +----------------------+-------------+------+----------------------+
   | *                    |             |      |                      |
   | >Include*\ `table_ti |             |      |                      |
   | tle <#table_10-1>`__ |             |      |                      |
   +----------------------+-------------+------+----------------------+

.. _sect_10.9.2.1:

Extended Content Identification Macro Attribute Descriptions
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. _sect_10.9.2.1.1:

User Content Long Label and Content Description
'''''''''''''''''''''''''''''''''''''''''''''''

User Content Long Label (3010,0034) shall represent a user-defined free
text providing the primary identification of this entity to other users.
Content Description (0070,0081) allows a longer string containing
additional descriptive identifying text.

This information is intended for display to human readers. Shall not be
used for structured processing.

.. _sect_10.10:

General Contributing Sources Macro
----------------------------------

`table_title <#table_10-13>`__ contains IOD Attributes that describe the
general characteristics of the contributing sources used to create a new
SOP Instance.

.. table:: General Contributing Sources Macro Attributes

   +-------------------+-------------------+------+-------------------+
   | Attribute Name    | Tag               | Type | Attribute         |
   |                   |                   |      | Description       |
   +===================+===================+======+===================+
   | Contributing SOP  | (0020,9529)       | 1C   | A Sequence that   |
   | Instances         |                   |      | identifies the    |
   | Reference         |                   |      | contributing SOP  |
   | Sequence          |                   |      | Instances.        |
   |                   |                   |      |                   |
   |                   |                   |      | Required if this  |
   |                   |                   |      | SOP Instance is   |
   |                   |                   |      | created from      |
   |                   |                   |      | other DICOM SOP   |
   |                   |                   |      | Instances.        |
   |                   |                   |      |                   |
   |                   |                   |      | .. note::         |
   |                   |                   |      |                   |
   |                   |                   |      |    The Attribute  |
   |                   |                   |      |    is absent in   |
   |                   |                   |      |    the case where |
   |                   |                   |      |    the sources    |
   |                   |                   |      |    used to create |
   |                   |                   |      |    this SOP       |
   |                   |                   |      |    Instance are   |
   |                   |                   |      |    not SOP        |
   |                   |                   |      |    Instances,     |
   |                   |                   |      |    e.g., a volume |
   |                   |                   |      |    that was       |
   |                   |                   |      |    directly       |
   |                   |                   |      |    generated by   |
   |                   |                   |      |    an acquisition |
   |                   |                   |      |    system.        |
   |                   |                   |      |                   |
   |                   |                   |      | One or more Items |
   |                   |                   |      | shall be included |
   |                   |                   |      | in this Sequence. |
   +-------------------+-------------------+------+-------------------+
   | >Study Instance   | (0020,000D)       | 1    | Unique identifier |
   | UID               |                   |      | for the Study of  |
   |                   |                   |      | the Contributing  |
   |                   |                   |      | SOP Instances.    |
   +-------------------+-------------------+------+-------------------+
   | >Referenced       | (0008,1115)       | 1    | Sequence of Items |
   | Series Sequence   |                   |      | each of which     |
   |                   |                   |      | includes the      |
   |                   |                   |      | Attributes of one |
   |                   |                   |      | Series.           |
   |                   |                   |      |                   |
   |                   |                   |      | One or more Items |
   |                   |                   |      | shall be included |
   |                   |                   |      | in this Sequence. |
   +-------------------+-------------------+------+-------------------+
   | >>Series Instance | (0020,000E)       | 1    | Unique identifier |
   | UID               |                   |      | of the Series     |
   |                   |                   |      | containing the    |
   |                   |                   |      | referenced        |
   |                   |                   |      | Instances.        |
   +-------------------+-------------------+------+-------------------+
   | >>Series Number   | (0020,0011)       | 2    | A number that     |
   |                   |                   |      | identifies this   |
   |                   |                   |      | Series.           |
   +-------------------+-------------------+------+-------------------+
   | >>Referenced      | (0008,114A)       | 1    | Sequence of Items |
   | Instance Sequence |                   |      | each providing a  |
   |                   |                   |      | reference to an   |
   |                   |                   |      | Instance that is  |
   |                   |                   |      | part of the       |
   |                   |                   |      | Series defined by |
   |                   |                   |      | Series Instance   |
   |                   |                   |      | UID (0020,000E)   |
   |                   |                   |      | in the enclosing  |
   |                   |                   |      | Item.             |
   |                   |                   |      |                   |
   |                   |                   |      | One or more Items |
   |                   |                   |      | shall be included |
   |                   |                   |      | in this Sequence. |
   +-------------------+-------------------+------+-------------------+
   | *>>>Includ        |                   |      |                   |
   | e*\ `table_title  |                   |      |                   |
   | <#table_10-11>`__ |                   |      |                   |
   +-------------------+-------------------+------+-------------------+
   | >>>Instance       | (0020,0013)       | 2    | A number that     |
   | Number            |                   |      | identifies this   |
   |                   |                   |      | Instance.         |
   +-------------------+-------------------+------+-------------------+
   | Manufacturer      | (0008,0070)       | 2    | Manufacturer of   |
   |                   |                   |      | the equipment     |
   |                   |                   |      | that produced the |
   |                   |                   |      | sources.          |
   +-------------------+-------------------+------+-------------------+
   | Manufacturer's    | (0008,1090)       | 1C   | Manufacturer's    |
   | Model Name        |                   |      | model name of the |
   |                   |                   |      | equipment that    |
   |                   |                   |      | produced the      |
   |                   |                   |      | sources.          |
   |                   |                   |      |                   |
   |                   |                   |      | Required if       |
   |                   |                   |      | present and       |
   |                   |                   |      | consistent in the |
   |                   |                   |      | contributing SOP  |
   |                   |                   |      | Instances.        |
   +-------------------+-------------------+------+-------------------+
   | Device Serial     | (0018,1000)       | 1C   | Manufacturer's    |
   | Number            |                   |      | serial number of  |
   |                   |                   |      | the equipment     |
   |                   |                   |      | that produced the |
   |                   |                   |      | sources.          |
   |                   |                   |      |                   |
   |                   |                   |      | Required if       |
   |                   |                   |      | present and       |
   |                   |                   |      | consistent in the |
   |                   |                   |      | contributing SOP  |
   |                   |                   |      | Instances.        |
   +-------------------+-------------------+------+-------------------+
   | Software Versions | (0018,1020)       | 1C   | Manufacturer's    |
   |                   |                   |      | designation of    |
   |                   |                   |      | software version  |
   |                   |                   |      | of the equipment  |
   |                   |                   |      | that produced the |
   |                   |                   |      | sources. See      |
   |                   |                   |      | `Software         |
   |                   |                   |      | Versions <#sect   |
   |                   |                   |      | _C.7.5.1.1.3>`__. |
   |                   |                   |      |                   |
   |                   |                   |      | Required if       |
   |                   |                   |      | present and       |
   |                   |                   |      | consistent in the |
   |                   |                   |      | contributing SOP  |
   |                   |                   |      | Instances.        |
   +-------------------+-------------------+------+-------------------+
   | Acquisition       | (0008,002A)       | 1C   | The time the      |
   | DateTime          |                   |      | acquisition of    |
   |                   |                   |      | data that         |
   |                   |                   |      | resulted in       |
   |                   |                   |      | sources started.  |
   |                   |                   |      |                   |
   |                   |                   |      | The value shall   |
   |                   |                   |      | be the start date |
   |                   |                   |      | and time of the   |
   |                   |                   |      | first             |
   |                   |                   |      | contributing SOP  |
   |                   |                   |      | Instance of the   |
   |                   |                   |      | group specified   |
   |                   |                   |      | by the            |
   |                   |                   |      | Contributing SOP  |
   |                   |                   |      | Instances         |
   |                   |                   |      | Reference         |
   |                   |                   |      | Sequence          |
   |                   |                   |      | (0020,9529).      |
   |                   |                   |      |                   |
   |                   |                   |      | Required if       |
   |                   |                   |      | present and       |
   |                   |                   |      | consistent in the |
   |                   |                   |      | contributing SOP  |
   |                   |                   |      | Instances.        |
   |                   |                   |      |                   |
   |                   |                   |      | .. note::         |
   |                   |                   |      |                   |
   |                   |                   |      |    The            |
   |                   |                   |      |    Acquisition    |
   |                   |                   |      |    DateTime may   |
   |                   |                   |      |    be created by  |
   |                   |                   |      |    combining the  |
   |                   |                   |      |    values of      |
   |                   |                   |      |    Acquisition    |
   |                   |                   |      |    Date           |
   |                   |                   |      |    (0008,0022)    |
   |                   |                   |      |    and            |
   |                   |                   |      |    Acquisition    |
   |                   |                   |      |    Time           |
   |                   |                   |      |    (0008,0032)    |
   |                   |                   |      |    Attributes in  |
   |                   |                   |      |    the            |
   |                   |                   |      |    contributing   |
   |                   |                   |      |    SOP Instances. |
   +-------------------+-------------------+------+-------------------+
   | Station Name      | (0008,1010)       | 1C   | User defined name |
   |                   |                   |      | identifying the   |
   |                   |                   |      | machine that      |
   |                   |                   |      | produced the      |
   |                   |                   |      | sources.          |
   |                   |                   |      |                   |
   |                   |                   |      | Required if       |
   |                   |                   |      | present and       |
   |                   |                   |      | consistent in the |
   |                   |                   |      | contributing SOP  |
   |                   |                   |      | Instances.        |
   +-------------------+-------------------+------+-------------------+
   | Operators' Name   | (0008,1070)       | 1C   | Name(s) of the    |
   |                   |                   |      | operator(s)       |
   |                   |                   |      | supporting the    |
   |                   |                   |      | Series.           |
   |                   |                   |      |                   |
   |                   |                   |      | Required if       |
   |                   |                   |      | present and       |
   |                   |                   |      | consistent in the |
   |                   |                   |      | contributing SOP  |
   |                   |                   |      | Instances.        |
   +-------------------+-------------------+------+-------------------+
   | Operator          | (0008,1072)       | 1C   | Identification of |
   | Identification    |                   |      | the operator(s)   |
   | Sequence          |                   |      | supporting the    |
   |                   |                   |      | Series. One or    |
   |                   |                   |      | more Items shall  |
   |                   |                   |      | be included in    |
   |                   |                   |      | this Sequence. If |
   |                   |                   |      | more than one     |
   |                   |                   |      | Item, the number  |
   |                   |                   |      | and order shall   |
   |                   |                   |      | correspond to the |
   |                   |                   |      | value of          |
   |                   |                   |      | Operators' Name   |
   |                   |                   |      | (0008,1070), if   |
   |                   |                   |      | present.          |
   |                   |                   |      |                   |
   |                   |                   |      | Required if       |
   |                   |                   |      | present and       |
   |                   |                   |      | consistent in the |
   |                   |                   |      | contributing SOP  |
   |                   |                   |      | Instances.        |
   +-------------------+-------------------+------+-------------------+
   | *>Inclu           |                   |      |                   |
   | de*\ `table_title |                   |      |                   |
   |  <#table_10-1>`__ |                   |      |                   |
   +-------------------+-------------------+------+-------------------+
   | Protocol Name     | (0018,1030)       | 1C   | User-defined      |
   |                   |                   |      | description of    |
   |                   |                   |      | the conditions    |
   |                   |                   |      | under which the   |
   |                   |                   |      | Series was        |
   |                   |                   |      | performed.        |
   |                   |                   |      |                   |
   |                   |                   |      | Required if       |
   |                   |                   |      | present and       |
   |                   |                   |      | consistent in the |
   |                   |                   |      | contributing SOP  |
   |                   |                   |      | Instances.        |
   |                   |                   |      |                   |
   |                   |                   |      | .. note::         |
   |                   |                   |      |                   |
   |                   |                   |      |    This Attribute |
   |                   |                   |      |    conveys        |
   |                   |                   |      |                   |
   |                   |                   |      |   Series-specific |
   |                   |                   |      |    protocol       |
   |                   |                   |      |    identification |
   |                   |                   |      |    and may or may |
   |                   |                   |      |    not be         |
   |                   |                   |      |    identical to   |
   |                   |                   |      |    the one        |
   |                   |                   |      |    presented in   |
   |                   |                   |      |    the Performed  |
   |                   |                   |      |    Protocol Code  |
   |                   |                   |      |    Sequence       |
   |                   |                   |      |    (0040,0260).   |
   +-------------------+-------------------+------+-------------------+
   | Performed         | (0040,0260)       | 1C   | Sequence          |
   | Protocol Code     |                   |      | describing the    |
   | Sequence          |                   |      | Protocol          |
   |                   |                   |      | performed for the |
   |                   |                   |      | Procedure Step    |
   |                   |                   |      | creating the      |
   |                   |                   |      | sources. One or   |
   |                   |                   |      | more Items shall  |
   |                   |                   |      | be included in    |
   |                   |                   |      | this Sequence.    |
   |                   |                   |      |                   |
   |                   |                   |      | Required if       |
   |                   |                   |      | present and       |
   |                   |                   |      | consistent in the |
   |                   |                   |      | contributing SOP  |
   |                   |                   |      | Instances.        |
   +-------------------+-------------------+------+-------------------+
   | *>Includ          | *No Baseline CID  |      |                   |
   | e*\ `table_title  | is defined.*      |      |                   |
   | <#table_8.8-1>`__ |                   |      |                   |
   +-------------------+-------------------+------+-------------------+
   | Acquisition       | (0018,9423)       | 1C   | User defined name |
   | Protocol Name     |                   |      | of the protocol   |
   |                   |                   |      | used to acquire   |
   |                   |                   |      | this image.       |
   |                   |                   |      |                   |
   |                   |                   |      | Required if       |
   |                   |                   |      | present and       |
   |                   |                   |      | consistent in the |
   |                   |                   |      | contributing SOP  |
   |                   |                   |      | Instances.        |
   +-------------------+-------------------+------+-------------------+

.. note::

   The Attributes at the first level of the General Contributing Sources
   Macro contain information that is common to all the Referenced SOP
   Instances included in the Contributing SOP Instances Reference
   Sequence. This allows to not duplicate information when the
   contributing Instances are single-frame objects and/or when they are
   in different Series with the same protocol and manufacturer
   information.

Typically the General Contributing Sources Macro is invoked from inside
another Sequence. Therefore, if the "common" Attributes of the Macro are
different among the Referenced SOP Instances, like different acquisition
protocols, software versions etc., the invoking Sequence will contain
several Items.

.. _sect_10.11:

Contributing Image Sources Macro
--------------------------------

`table_title <#table_10-14>`__ contains IOD Attributes that describe the
image related characteristics of the contributing image sources used to
create a new SOP Instance (e.g., a volume SOP Instance).

.. table:: Contributing Image Sources Macro Attributes

   +----------------------+-------------+------+----------------------+
   | Attribute Name       | Tag         | Type | Attribute            |
   |                      |             |      | Description          |
   +======================+=============+======+======================+
   | Rows                 | (0028,0010) | 1    | Number of rows in    |
   |                      |             |      | the images.          |
   +----------------------+-------------+------+----------------------+
   | Columns              | (0028,0011) | 1    | Number of columns in |
   |                      |             |      | the images.          |
   +----------------------+-------------+------+----------------------+
   | Bits Stored          | (0028,0101) | 1    | Number of bits       |
   |                      |             |      | stored for each      |
   |                      |             |      | pixel sample. Each   |
   |                      |             |      | sample shall have    |
   |                      |             |      | the same number of   |
   |                      |             |      | bits stored. See for |
   |                      |             |      | further explanation. |
   +----------------------+-------------+------+----------------------+
   | Lossy Image          | (0028,2110) | 1C   | Specifies whether    |
   | Compression          |             |      | the Source Images    |
   |                      |             |      | have undergone lossy |
   |                      |             |      | compression (at a    |
   |                      |             |      | point in their       |
   |                      |             |      | lifetime).           |
   |                      |             |      |                      |
   |                      |             |      | 00                   |
   |                      |             |      |    Image has NOT     |
   |                      |             |      |    been subjected to |
   |                      |             |      |    lossy             |
   |                      |             |      |    compression.      |
   |                      |             |      |                      |
   |                      |             |      | 01                   |
   |                      |             |      |    Image has been    |
   |                      |             |      |    subjected to      |
   |                      |             |      |    lossy             |
   |                      |             |      |    compression.      |
   |                      |             |      |                      |
   |                      |             |      | See `Lossy Image     |
   |                      |             |      | Compression <#s      |
   |                      |             |      | ect_C.7.6.1.1.5>`__. |
   |                      |             |      |                      |
   |                      |             |      | Required if it is    |
   |                      |             |      | known whether or not |
   |                      |             |      | Lossy Compression    |
   |                      |             |      | has been performed   |
   |                      |             |      | on the Images.       |
   |                      |             |      |                      |
   |                      |             |      | .. note::            |
   |                      |             |      |                      |
   |                      |             |      |    In some SOP Class |
   |                      |             |      |    definitions the   |
   |                      |             |      |    Lossy Image       |
   |                      |             |      |    Compression       |
   |                      |             |      |    Attribute is      |
   |                      |             |      |    optional.         |
   +----------------------+-------------+------+----------------------+
   | Lossy Image          | (0028,2112) | 1C   | Describes the        |
   | Compression Ratio    |             |      | approximate lossy    |
   |                      |             |      | compression ratio(s) |
   |                      |             |      | that have been       |
   |                      |             |      | applied to this      |
   |                      |             |      | image.               |
   |                      |             |      |                      |
   |                      |             |      | See `Lossy Image     |
   |                      |             |      | Compression          |
   |                      |             |      | Ratio <#sec          |
   |                      |             |      | t_C.7.6.1.1.5.2>`__. |
   |                      |             |      |                      |
   |                      |             |      | Required if Lossy    |
   |                      |             |      | Image Compression    |
   |                      |             |      | (0028,2110) is "01". |
   +----------------------+-------------+------+----------------------+
   | Lossy Image          | (0028,2114) | 1C   | A label for the      |
   | Compression Method   |             |      | lossy compression    |
   |                      |             |      | method(s) that have  |
   |                      |             |      | been applied to the  |
   |                      |             |      | source images.       |
   |                      |             |      |                      |
   |                      |             |      | See `Lossy Image     |
   |                      |             |      | Compression          |
   |                      |             |      | Method <#sec         |
   |                      |             |      | t_C.7.6.1.1.5.1>`__. |
   |                      |             |      |                      |
   |                      |             |      | Required if Lossy    |
   |                      |             |      | Image Compression    |
   |                      |             |      | (0028,2110) is "01". |
   +----------------------+-------------+------+----------------------+

.. _sect_10.12:

Patient Orientation Macro
-------------------------

This section describes Attributes of the Patient Orientation Macro by
specifying the Patient orientation related to gravity and equipment.
`table_title <#table_10-15>`__ contains IOD Attributes that describe the
Patient Orientation related to gravity and equipment.

.. table:: Patient Orientation Macro Attributes

   +----------------------+-------------+------+----------------------+
   | Attribute Name       | Tag         | Type | Attribute            |
   |                      |             |      | Description          |
   +======================+=============+======+======================+
   | Patient Orientation  | (0054,0410) | 1    | Sequence that        |
   | Code Sequence        |             |      | describes the        |
   |                      |             |      | orientation of the   |
   |                      |             |      | Patient with respect |
   |                      |             |      | to gravity.          |
   |                      |             |      |                      |
   |                      |             |      | See `Patient         |
   |                      |             |      | Orientation Code     |
   |                      |             |      | Sequence <#s         |
   |                      |             |      | ect_C.8.11.5.1.2>`__ |
   |                      |             |      | for further          |
   |                      |             |      | explanation.         |
   |                      |             |      |                      |
   |                      |             |      | Only a single Item   |
   |                      |             |      | shall be included in |
   |                      |             |      | this Sequence.       |
   +----------------------+-------------+------+----------------------+
   | *>                   | *B.*        |      |                      |
   | Include*\ `table_tit |             |      |                      |
   | le <#table_8.8-1>`__ |             |      |                      |
   +----------------------+-------------+------+----------------------+
   | >Patient Orientation | (0054,0412) | 1C   | Patient orientation  |
   | Modifier Code        |             |      | modifier.            |
   | Sequence             |             |      |                      |
   |                      |             |      | Required if needed   |
   |                      |             |      | to fully specify the |
   |                      |             |      | orientation of the   |
   |                      |             |      | Patient with respect |
   |                      |             |      | to gravity.          |
   |                      |             |      |                      |
   |                      |             |      | Only a single Item   |
   |                      |             |      | shall be included in |
   |                      |             |      | this Sequence.       |
   +----------------------+-------------+------+----------------------+
   | *>>                  | *B.*        |      |                      |
   | Include*\ `table_tit |             |      |                      |
   | le <#table_8.8-1>`__ |             |      |                      |
   +----------------------+-------------+------+----------------------+
   | Patient Gantry       | (0054,0414) | 3    | Sequence that        |
   | Relationship Code    |             |      | describes the        |
   | Sequence             |             |      | orientation of the   |
   |                      |             |      | Patient with respect |
   |                      |             |      | to the head of the   |
   |                      |             |      | table. See `Patient  |
   |                      |             |      | Gantry Relationship  |
   |                      |             |      | Code                 |
   |                      |             |      | Sequence <#          |
   |                      |             |      | sect_C.8.4.6.1.3>`__ |
   |                      |             |      | for further          |
   |                      |             |      | explanation.         |
   |                      |             |      |                      |
   |                      |             |      | Only a single Item   |
   |                      |             |      | is permitted in this |
   |                      |             |      | Sequence.            |
   +----------------------+-------------+------+----------------------+
   | *>                   | *B.*        |      |                      |
   | Include*\ `table_tit |             |      |                      |
   | le <#table_8.8-1>`__ |             |      |                      |
   +----------------------+-------------+------+----------------------+

.. _sect_10.12.1:

Relation With Other Positioning Attributes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Attributes of this Macro may be used to correlate the Patient-Based
Coordinate System (see `Image Plane Module <#sect_C.7.6.2>`__) and the
equipment.

.. note::

   The Patient Orientation Code Sequence (0054,0410) allows a more
   precise and comprehensive positioning than Patient Position
   (0018,5100). If this Sequence is present Patient Position (0018,5100)
   is not used.

.. _sect_10.13:

Performed Procedure Step Summary Macro
--------------------------------------

.. table:: Performed Procedure Step Summary Macro Attributes

   +-------------------+-------------------+------+-------------------+
   | Attribute Name    | Tag               | Type | Attribute         |
   |                   |                   |      | Description       |
   +===================+===================+======+===================+
   | Performed         | (0040,0253)       | 3    | User or equipment |
   | Procedure Step ID |                   |      | generated         |
   |                   |                   |      | identifier of     |
   |                   |                   |      | that part of a    |
   |                   |                   |      | Procedure that    |
   |                   |                   |      | has been carried  |
   |                   |                   |      | out within this   |
   |                   |                   |      | step.             |
   +-------------------+-------------------+------+-------------------+
   | Performed         | (0040,0244)       | 3    | Date on which the |
   | Procedure Step    |                   |      | Performed         |
   | Start Date        |                   |      | Procedure Step    |
   |                   |                   |      | started.          |
   +-------------------+-------------------+------+-------------------+
   | Performed         | (0040,0245)       | 3    | Time on which the |
   | Procedure Step    |                   |      | Performed         |
   | Start Time        |                   |      | Procedure Step    |
   |                   |                   |      | started.          |
   +-------------------+-------------------+------+-------------------+
   | Performed         | (0040,0250)       | 3    | Date on which the |
   | Procedure Step    |                   |      | Performed         |
   | End Date          |                   |      | Procedure Step    |
   |                   |                   |      | ended.            |
   +-------------------+-------------------+------+-------------------+
   | Performed         | (0040,0251)       | 3    | Time at which the |
   | Procedure Step    |                   |      | Performed         |
   | End Time          |                   |      | Procedure Step    |
   |                   |                   |      | ended.            |
   +-------------------+-------------------+------+-------------------+
   | Performed         | (0040,0254)       | 3    | Inst              |
   | Procedure Step    |                   |      | itution-generated |
   | Description       |                   |      | description or    |
   |                   |                   |      | classification of |
   |                   |                   |      | the Procedure     |
   |                   |                   |      | Step that was     |
   |                   |                   |      | performed.        |
   +-------------------+-------------------+------+-------------------+
   | Performed         | (0040,0260)       | 3    | Sequence          |
   | Protocol Code     |                   |      | describing the    |
   | Sequence          |                   |      | Protocol          |
   |                   |                   |      | performed for     |
   |                   |                   |      | this Procedure    |
   |                   |                   |      | Step. One or more |
   |                   |                   |      | Items are         |
   |                   |                   |      | permitted in this |
   |                   |                   |      | Sequence.         |
   +-------------------+-------------------+------+-------------------+
   | *>Includ          | *CID may be       |      |                   |
   | e*\ `table_title  | defined in the    |      |                   |
   | <#table_8.8-1>`__ | Macro             |      |                   |
   |                   | invocation.*      |      |                   |
   +-------------------+-------------------+------+-------------------+
   | >Protocol Context | (0040,0440)       | 3    | Sequence that     |
   | Sequence          |                   |      | specifies the     |
   |                   |                   |      | context for the   |
   |                   |                   |      | Performed         |
   |                   |                   |      | Protocol Code     |
   |                   |                   |      | Sequence          |
   |                   |                   |      | (0040,0260) Item. |
   |                   |                   |      | One or more Items |
   |                   |                   |      | are permitted in  |
   |                   |                   |      | this Sequence.    |
   +-------------------+-------------------+------+-------------------+
   | *>>Inclu          | *CID may be       |      |                   |
   | de*\ `table_title | defined in the    |      |                   |
   |  <#table_10-2>`__ | Macro             |      |                   |
   |                   | invocation.*      |      |                   |
   +-------------------+-------------------+------+-------------------+
   | >>Content Item    | (0040,0441)       | 3    | Sequence that     |
   | Modifier Sequence |                   |      | specifies         |
   |                   |                   |      | modifiers for a   |
   |                   |                   |      | Protocol Context  |
   |                   |                   |      | Content Item.     |
   |                   |                   |      |                   |
   |                   |                   |      | One or more Items |
   |                   |                   |      | are permitted in  |
   |                   |                   |      | this Sequence.    |
   |                   |                   |      |                   |
   |                   |                   |      | See `Protocol     |
   |                   |                   |      | Context           |
   |                   |                   |      | Sequence <#s      |
   |                   |                   |      | ect_C.4.10.1>`__. |
   +-------------------+-------------------+------+-------------------+
   | *>>>Inclu         | *CID may be       |      |                   |
   | de*\ `table_title | defined in the    |      |                   |
   |  <#table_10-2>`__ | Macro             |      |                   |
   |                   | invocation.*      |      |                   |
   +-------------------+-------------------+------+-------------------+
   | Comments on the   | (0040,0280)       | 3    | User-defined      |
   | Performed         |                   |      | comments on the   |
   | Procedure Step    |                   |      | Performed         |
   |                   |                   |      | Procedure Step.   |
   +-------------------+-------------------+------+-------------------+

.. _sect_10.14:

HL7v2 Hierarchic Designator Macro
---------------------------------

`table_title <#table_10-17>`__ describes the Attributes for identifying
an entity (system, organization, agency, or department) that has
responsibility for managing or assigning a defined set of instance
identifiers (such as placer or filler number, Patient identifiers,
provider identifiers, etc.). This entity could be a particular health
care application such as a registration system that assigns Patient
identifiers, a governmental entity such as a licensing authority that
assigns professional identifiers or drivers' license numbers, or a
facility where such identifiers are assigned.

.. note::

   This definition is identical to HL7 v2.5, Section 2.A.33, with only
   minor changes for editorial style.

These Attributes are equivalent to the components of the HL7 v2
Hierarchic Designator (HD) and Entity Identifier (EI) data types (see
HL7 v2 Chapter 2.A).

If both Local Namespace Entity ID (0040,0031) and Universal Entity ID
(0040,0032) are present, they shall refer to the same entity.

.. table:: HL7v2 Hierarchic Designator Macro Attributes

   +----------------------+-------------+------+----------------------+
   | Attribute Name       | Tag         | Type | Attribute            |
   |                      |             |      | Description          |
   +======================+=============+======+======================+
   | Local Namespace      | (0040,0031) | 1C   | Identifies an entity |
   | Entity ID            |             |      | within the local     |
   |                      |             |      | namespace or domain. |
   |                      |             |      | Required if          |
   |                      |             |      | Universal Entity ID  |
   |                      |             |      | (0040,0032) is not   |
   |                      |             |      | present; may be      |
   |                      |             |      | present otherwise.   |
   +----------------------+-------------+------+----------------------+
   | Universal Entity ID  | (0040,0032) | 1C   | Universal or unique  |
   |                      |             |      | identifier for an    |
   |                      |             |      | entity. Required if  |
   |                      |             |      | Local Namespace      |
   |                      |             |      | Entity ID            |
   |                      |             |      | (0040,0031) is not   |
   |                      |             |      | present; may be      |
   |                      |             |      | present otherwise.   |
   +----------------------+-------------+------+----------------------+
   | Universal Entity ID  | (0040,0033) | 1C   | Standard defining    |
   | Type                 |             |      | the format of the    |
   |                      |             |      | Universal Entity ID. |
   |                      |             |      | Required if          |
   |                      |             |      | Universal Entity ID  |
   |                      |             |      | (0040,0032) is       |
   |                      |             |      | present.             |
   |                      |             |      |                      |
   |                      |             |      | DNS                  |
   |                      |             |      |    An Internet       |
   |                      |             |      |    dotted name.      |
   |                      |             |      |    Either in ASCII   |
   |                      |             |      |    or as integers    |
   |                      |             |      |                      |
   |                      |             |      | EUI64                |
   |                      |             |      |    An IEEE Extended  |
   |                      |             |      |    Unique Identifier |
   |                      |             |      |                      |
   |                      |             |      | ISO                  |
   |                      |             |      |    An International  |
   |                      |             |      |    Standards         |
   |                      |             |      |    Organization      |
   |                      |             |      |    Object Identifier |
   |                      |             |      |                      |
   |                      |             |      | URI                  |
   |                      |             |      |    Uniform Resource  |
   |                      |             |      |    Identifier        |
   |                      |             |      |                      |
   |                      |             |      | UUID                 |
   |                      |             |      |    The DCE Universal |
   |                      |             |      |    Unique Identifier |
   |                      |             |      |                      |
   |                      |             |      | X400                 |
   |                      |             |      |    An X.400 MHS      |
   |                      |             |      |    identifier        |
   |                      |             |      |                      |
   |                      |             |      | X500                 |
   |                      |             |      |    An X.500          |
   |                      |             |      |    directory name    |
   +----------------------+-------------+------+----------------------+

.. _sect_10.15:

Issuer of Patient ID Macro
--------------------------

`table_title <#table_10-18>`__ describes the Attributes for identifying
the source of Patient ID (0010,0020).

These Attributes are equivalent to components of the HL7 v2 Extended
Composite ID with Check Digit (CX) data type (see HL7 v2 Chapter
2.A.14), as used in the HL7 v2 PID-3 Patient Identifier List field.

.. table:: Issuer of Patient ID Macro Attributes

   +-------------------+-------------------+------+-------------------+
   | Attribute Name    | Tag               | Type | Attribute         |
   |                   |                   |      | Description       |
   +===================+===================+======+===================+
   | Issuer of Patient | (0010,0021)       | 3    | Identifier of the |
   | ID                |                   |      | Assigning         |
   |                   |                   |      | Authority         |
   |                   |                   |      | (system,          |
   |                   |                   |      | organization,     |
   |                   |                   |      | agency, or        |
   |                   |                   |      | department) that  |
   |                   |                   |      | issued the        |
   |                   |                   |      | Patient ID.       |
   |                   |                   |      |                   |
   |                   |                   |      | .. note::         |
   |                   |                   |      |                   |
   |                   |                   |      |    Equivalent to  |
   |                   |                   |      |    HL7 v2 CX      |
   |                   |                   |      |    component 4    |
   |                   |                   |      |    subcomponent   |
   |                   |                   |      |    1.             |
   +-------------------+-------------------+------+-------------------+
   | Issuer of Patient | (0010,0024)       | 3    | Attributes        |
   | ID Qualifiers     |                   |      | specifying or     |
   | Sequence          |                   |      | qualifying the    |
   |                   |                   |      | identity of the   |
   |                   |                   |      | issuer of the     |
   |                   |                   |      | Patient ID, or    |
   |                   |                   |      | scoping the       |
   |                   |                   |      | Patient ID.       |
   |                   |                   |      |                   |
   |                   |                   |      | Only a single     |
   |                   |                   |      | Item is permitted |
   |                   |                   |      | in this Sequence. |
   +-------------------+-------------------+------+-------------------+
   | >Universal Entity | (0040,0032)       | 3    | Universal or      |
   | ID                |                   |      | unique identifier |
   |                   |                   |      | for the Patient   |
   |                   |                   |      | ID Assigning      |
   |                   |                   |      | Authority. The    |
   |                   |                   |      | authority         |
   |                   |                   |      | identified by     |
   |                   |                   |      | this Attribute    |
   |                   |                   |      | shall be the same |
   |                   |                   |      | as that of Issuer |
   |                   |                   |      | of Patient ID     |
   |                   |                   |      | (0010,0021), if   |
   |                   |                   |      | present.          |
   |                   |                   |      |                   |
   |                   |                   |      | .. note::         |
   |                   |                   |      |                   |
   |                   |                   |      |    Equivalent to  |
   |                   |                   |      |    HL7 v2 CX      |
   |                   |                   |      |    component 4    |
   |                   |                   |      |    subcomponent 2 |
   |                   |                   |      |    (Universal     |
   |                   |                   |      |    ID).           |
   +-------------------+-------------------+------+-------------------+
   | >Universal Entity | (0040,0033)       | 1C   | Standard defining |
   | ID Type           |                   |      | the format of the |
   |                   |                   |      | Universal Entity  |
   |                   |                   |      | ID (0040,0032).   |
   |                   |                   |      | Required if       |
   |                   |                   |      | Universal Entity  |
   |                   |                   |      | ID (0040,0032) is |
   |                   |                   |      | present.          |
   |                   |                   |      |                   |
   |                   |                   |      | .. note::         |
   |                   |                   |      |                   |
   |                   |                   |      |    Equivalent to  |
   |                   |                   |      |    HL7 v2 CX      |
   |                   |                   |      |    component 4    |
   |                   |                   |      |    subcomponent 3 |
   |                   |                   |      |    (Universal ID  |
   |                   |                   |      |    Type).         |
   |                   |                   |      |                   |
   |                   |                   |      | See `HL7v2        |
   |                   |                   |      | Hierarchic        |
   |                   |                   |      | Designator        |
   |                   |                   |      | Macro             |
   |                   |                   |      |  <#sect_10.14>`__ |
   |                   |                   |      | for Defined       |
   |                   |                   |      | Terms.            |
   +-------------------+-------------------+------+-------------------+
   | >Identifier Type  | (0040,0035)       | 3    | Type of Patient   |
   | Code              |                   |      | ID. Refer to HL7  |
   |                   |                   |      | v2 Table 0203 for |
   |                   |                   |      | Defined Terms.    |
   |                   |                   |      |                   |
   |                   |                   |      | .. note::         |
   |                   |                   |      |                   |
   |                   |                   |      |    Equivalent to  |
   |                   |                   |      |    HL7 v2 CX      |
   |                   |                   |      |    component 5    |
   |                   |                   |      |    (Identifier    |
   |                   |                   |      |    Type Code).    |
   +-------------------+-------------------+------+-------------------+
   | >Assigning        | (0040,0036)       | 3    | The place or      |
   | Facility Sequence |                   |      | location          |
   |                   |                   |      | identifier where  |
   |                   |                   |      | the identifier    |
   |                   |                   |      | was first         |
   |                   |                   |      | assigned to the   |
   |                   |                   |      | Patient. This     |
   |                   |                   |      | component is not  |
   |                   |                   |      | an inherent part  |
   |                   |                   |      | of the identifier |
   |                   |                   |      | but rather part   |
   |                   |                   |      | of the history of |
   |                   |                   |      | the identifier.   |
   |                   |                   |      |                   |
   |                   |                   |      | Only a single     |
   |                   |                   |      | Item is permitted |
   |                   |                   |      | in this Sequence. |
   |                   |                   |      |                   |
   |                   |                   |      | .. note::         |
   |                   |                   |      |                   |
   |                   |                   |      |    Equivalent to  |
   |                   |                   |      |    HL7 v2 CX      |
   |                   |                   |      |    component 6    |
   |                   |                   |      |    (Assigning     |
   |                   |                   |      |    Facility).     |
   +-------------------+-------------------+------+-------------------+
   | *>>Includ         |                   |      |                   |
   | e*\ `table_title  |                   |      |                   |
   | <#table_10-17>`__ |                   |      |                   |
   +-------------------+-------------------+------+-------------------+
   | >Assigning        | (0040,0039)       | 3    | The geo-political |
   | Jurisdiction Code |                   |      | body that         |
   | Sequence          |                   |      | assigned the      |
   |                   |                   |      | Patient           |
   |                   |                   |      | identifier.       |
   |                   |                   |      | Typically a code  |
   |                   |                   |      | for a country or  |
   |                   |                   |      | a state/province. |
   |                   |                   |      | Only a single     |
   |                   |                   |      | Item is permitted |
   |                   |                   |      | in this Sequence. |
   |                   |                   |      |                   |
   |                   |                   |      | .. note::         |
   |                   |                   |      |                   |
   |                   |                   |      |    Equivalent to  |
   |                   |                   |      |    HL7 v2 CX      |
   |                   |                   |      |    component 9    |
   |                   |                   |      |    (Assigning     |
   |                   |                   |      |    Jurisdiction). |
   +-------------------+-------------------+------+-------------------+
   | *>>Includ         | *B for country    |      |                   |
   | e*\ `table_title  | codes.*           |      |                   |
   | <#table_8.8-1>`__ |                   |      |                   |
   +-------------------+-------------------+------+-------------------+
   | >Assigning Agency | (0040,003A)       | 3    | The agency or     |
   | or Department     |                   |      | department that   |
   | Code Sequence     |                   |      | assigned the      |
   |                   |                   |      | Patient           |
   |                   |                   |      | identifier. Only  |
   |                   |                   |      | a single Item is  |
   |                   |                   |      | permitted in this |
   |                   |                   |      | Sequence.         |
   |                   |                   |      |                   |
   |                   |                   |      | .. note::         |
   |                   |                   |      |                   |
   |                   |                   |      |    Equivalent to  |
   |                   |                   |      |    HL7 v2 CX      |
   |                   |                   |      |    component 10   |
   |                   |                   |      |    (Assigning     |
   |                   |                   |      |    Agency or      |
   |                   |                   |      |    Department).   |
   +-------------------+-------------------+------+-------------------+
   | *>>Includ         | *No Baseline CID  |      |                   |
   | e*\ `table_title  | is defined.*      |      |                   |
   | <#table_8.8-1>`__ |                   |      |                   |
   +-------------------+-------------------+------+-------------------+

.. _sect_10.16:

Algorithm Identification Macro
------------------------------

`table_title <#table_10-19>`__ describes the Attributes for encoding the
algorithm used to create or derive a SOP Instance contents. An algorithm
is described by the Algorithm Family, a specific Algorithm Name, and an
Algorithm Version. A character string containing parameters that were
used in the algorithm can be included.

.. table:: Algorithm Identification Macro Attributes

   +-------------------+-------------------+------+-------------------+
   | Attribute Name    | Tag               | Type | Attribute         |
   |                   |                   |      | Description       |
   +===================+===================+======+===================+
   | Algorithm Family  | (0066,002F)       | 1    | The family of     |
   | Code Sequence     |                   |      | algorithm(s) that |
   |                   |                   |      | best describes    |
   |                   |                   |      | the software      |
   |                   |                   |      | algorithm used.   |
   |                   |                   |      |                   |
   |                   |                   |      | Only a single     |
   |                   |                   |      | Item shall be     |
   |                   |                   |      | included in this  |
   |                   |                   |      | Sequence.         |
   +-------------------+-------------------+------+-------------------+
   | *>Includ          | *CID may be       |      |                   |
   | e*\ `table_title  | defined in the    |      |                   |
   | <#table_8.8-1>`__ | Macro             |      |                   |
   |                   | invocation.*      |      |                   |
   +-------------------+-------------------+------+-------------------+
   | Algorithm Name    | (0066,0030)       | 3    | The code assigned |
   | Code Sequence     |                   |      | by a manufacturer |
   |                   |                   |      | to a specific     |
   |                   |                   |      | software          |
   |                   |                   |      | algorithm.        |
   |                   |                   |      |                   |
   |                   |                   |      | Only a single     |
   |                   |                   |      | Item is permitted |
   |                   |                   |      | in this Sequence. |
   +-------------------+-------------------+------+-------------------+
   | *>Includ          | *No Baseline CID  |      |                   |
   | e*\ `table_title  | is defined.*      |      |                   |
   | <#table_8.8-1>`__ |                   |      |                   |
   +-------------------+-------------------+------+-------------------+
   | Algorithm Name    | (0066,0036)       | 1    | The name assigned |
   |                   |                   |      | by a manufacturer |
   |                   |                   |      | to a specific     |
   |                   |                   |      | software          |
   |                   |                   |      | algorithm.        |
   +-------------------+-------------------+------+-------------------+
   | Algorithm Version | (0066,0031)       | 1    | The software      |
   |                   |                   |      | version           |
   |                   |                   |      | identifier        |
   |                   |                   |      | assigned by a     |
   |                   |                   |      | manufacturer to a |
   |                   |                   |      | specific software |
   |                   |                   |      | algorithm.        |
   +-------------------+-------------------+------+-------------------+
   | Algorithm         | (0066,0032)       | 3    | The input         |
   | Parameters        |                   |      | parameters used   |
   |                   |                   |      | by a manufacturer |
   |                   |                   |      | to configure the  |
   |                   |                   |      | behavior of a     |
   |                   |                   |      | specific software |
   |                   |                   |      | algorithm.        |
   +-------------------+-------------------+------+-------------------+
   | Algorithm Source  | (0024,0202)       | 3    | Source of the     |
   |                   |                   |      | algorithm, e.g.,  |
   |                   |                   |      | the name of the   |
   |                   |                   |      | manufacturer,     |
   |                   |                   |      | researcher,       |
   |                   |                   |      | university, etc.  |
   +-------------------+-------------------+------+-------------------+

.. _sect_10.17:

Selector Attribute Macro
------------------------

`table_title <#table_10-20>`__ specifies the Attributes that identify
either a particular value of an Attribute, all values of an Attribute, a
specific Item in a Sequence, or all Items in a Sequence. The Attribute
or Item may be nested within one or more Sequences, and/or a Private
Attribute.

The invocation of the Selector Attribute Macro may define additional
semantics. E.g., if the Selector Attribute Macro is used to select "all"
values of an Attribute and then test that set of value against some
condition, then an invocation might define whether it is required that
at least one value in the set meet the condition or whether all values
in the set must meet the condition.

`table_title <#table_10-20a>`__ extends the Selector Attribute Macro
with additional Attribute descriptors.

.. table:: Selector Attribute Macro Attributes

   +----------------------+-------------+------+----------------------+
   | Attribute Name       | Tag         | Type | Attribute            |
   |                      |             |      | Description          |
   +======================+=============+======+======================+
   | Selector Attribute   | (0072,0026) | 1C   | Data Element Tag of  |
   |                      |             |      | the Attribute to be  |
   |                      |             |      | referenced.          |
   |                      |             |      |                      |
   |                      |             |      | Required if the      |
   |                      |             |      | selected content is  |
   |                      |             |      | not a Sequence Item. |
   +----------------------+-------------+------+----------------------+
   | Selector Value       | (0072,0028) | 1C   | Non-negative integer |
   | Number               |             |      | identifying which    |
   |                      |             |      | value of a           |
   |                      |             |      | multi-valued         |
   |                      |             |      | Attribute identified |
   |                      |             |      | by Selector          |
   |                      |             |      | Attribute            |
   |                      |             |      | (0072,0026) is to be |
   |                      |             |      | referenced. The      |
   |                      |             |      | value 1 identifies   |
   |                      |             |      | the first value. The |
   |                      |             |      | value 0 identifies   |
   |                      |             |      | all values.          |
   |                      |             |      |                      |
   |                      |             |      | When the Value       |
   |                      |             |      | Multiplicity of the  |
   |                      |             |      | Selector Attribute   |
   |                      |             |      | (0072,0026) is 1     |
   |                      |             |      | then the value of    |
   |                      |             |      | this Attribute shall |
   |                      |             |      | be 1.                |
   |                      |             |      |                      |
   |                      |             |      | Required if the      |
   |                      |             |      | selected content is  |
   |                      |             |      | a single Attribute   |
   |                      |             |      | of any VR other than |
   |                      |             |      | SQ.                  |
   +----------------------+-------------+------+----------------------+
   | Selector Sequence    | (0072,0052) | 1C   | Contains the Data    |
   | Pointer              |             |      | Element Tags of the  |
   |                      |             |      | path to the Sequence |
   |                      |             |      | that contains the    |
   |                      |             |      | Attribute that is    |
   |                      |             |      | identified by        |
   |                      |             |      | Selector Attribute   |
   |                      |             |      | (0072,0026) or to    |
   |                      |             |      | the Item(s) to be    |
   |                      |             |      | selected in Selector |
   |                      |             |      | Sequence Pointer     |
   |                      |             |      | Items (0074,1057).   |
   |                      |             |      |                      |
   |                      |             |      | This Attribute shall |
   |                      |             |      | have the same number |
   |                      |             |      | of values as the     |
   |                      |             |      | level of nesting of  |
   |                      |             |      | Selector Attribute   |
   |                      |             |      | (0072,0026) or the   |
   |                      |             |      | selected Item(s).    |
   |                      |             |      |                      |
   |                      |             |      | Required if Selector |
   |                      |             |      | Attribute            |
   |                      |             |      | (0072,0026) is       |
   |                      |             |      | nested in one or     |
   |                      |             |      | more Sequences or is |
   |                      |             |      | absent.              |
   |                      |             |      |                      |
   |                      |             |      | See `Referencing     |
   |                      |             |      | Nested               |
   |                      |             |      | Elements <           |
   |                      |             |      | #sect_10.17.1.1>`__. |
   +----------------------+-------------+------+----------------------+
   | Selector Sequence    | (0072,0054) | 1C   | Identification of    |
   | Pointer Private      |             |      | the creator of a     |
   | Creator              |             |      | group of Private     |
   |                      |             |      | Data Elements used   |
   |                      |             |      | to encode Attributes |
   |                      |             |      | in the Selector      |
   |                      |             |      | Sequence Pointer     |
   |                      |             |      | (0072,0052).         |
   |                      |             |      |                      |
   |                      |             |      | This Attribute shall |
   |                      |             |      | have the same number |
   |                      |             |      | of values as         |
   |                      |             |      | Selector Sequence    |
   |                      |             |      | Pointer (0072,0052). |
   |                      |             |      |                      |
   |                      |             |      | For values of the    |
   |                      |             |      | Selector Sequence    |
   |                      |             |      | Pointer (0072,0052)  |
   |                      |             |      | that are not the     |
   |                      |             |      | Data Element Tag of  |
   |                      |             |      | a Private Attribute, |
   |                      |             |      | the corresponding    |
   |                      |             |      | value in Selector    |
   |                      |             |      | Sequence Pointer     |
   |                      |             |      | Private Creator      |
   |                      |             |      | (0072,0054) shall be |
   |                      |             |      | empty.               |
   |                      |             |      |                      |
   |                      |             |      | Required if Selector |
   |                      |             |      | Sequence Pointer     |
   |                      |             |      | (0072,0052) is       |
   |                      |             |      | present and one or   |
   |                      |             |      | more of the values   |
   |                      |             |      | of Selector Sequence |
   |                      |             |      | Pointer (0072,0052)  |
   |                      |             |      | is the Data Element  |
   |                      |             |      | Tag of a Private     |
   |                      |             |      | Attribute.           |
   |                      |             |      |                      |
   |                      |             |      | See `Private         |
   |                      |             |      | Attribute            |
   |                      |             |      | References <         |
   |                      |             |      | #sect_10.17.1.2>`__. |
   +----------------------+-------------+------+----------------------+
   | Selector Sequence    | (0074,1057) | 1C   | Identification of    |
   | Pointer Items        |             |      | the Item indices in  |
   |                      |             |      | the Selector         |
   |                      |             |      | Sequence Pointer     |
   |                      |             |      | (0072,0052).         |
   |                      |             |      |                      |
   |                      |             |      | This Attribute shall |
   |                      |             |      | have the same number |
   |                      |             |      | of values as the     |
   |                      |             |      | Selector Sequence    |
   |                      |             |      | Pointer (0072,0052). |
   |                      |             |      |                      |
   |                      |             |      | The value 1          |
   |                      |             |      | identifies the first |
   |                      |             |      | Item of the          |
   |                      |             |      | corresponding        |
   |                      |             |      | Sequence. The value  |
   |                      |             |      | 0 identifies all     |
   |                      |             |      | Items of the         |
   |                      |             |      | corresponding        |
   |                      |             |      | Sequence.            |
   |                      |             |      |                      |
   |                      |             |      | Required if Selector |
   |                      |             |      | Sequence Pointer     |
   |                      |             |      | (0072,0052) is       |
   |                      |             |      | present.             |
   |                      |             |      |                      |
   |                      |             |      | See `Referencing     |
   |                      |             |      | Nested               |
   |                      |             |      | Elements <           |
   |                      |             |      | #sect_10.17.1.1>`__. |
   +----------------------+-------------+------+----------------------+
   | Selector Attribute   | (0072,0056) | 1C   | Identification of    |
   | Private Creator      |             |      | the creator of a     |
   |                      |             |      | group of Private     |
   |                      |             |      | Data Elements.       |
   |                      |             |      |                      |
   |                      |             |      | Required if the      |
   |                      |             |      | Selector Attribute   |
   |                      |             |      | (0072,0026) value is |
   |                      |             |      | the Data Element Tag |
   |                      |             |      | of a Private         |
   |                      |             |      | Attribute.           |
   |                      |             |      |                      |
   |                      |             |      | See `Private         |
   |                      |             |      | Attribute            |
   |                      |             |      | References <         |
   |                      |             |      | #sect_10.17.1.2>`__. |
   +----------------------+-------------+------+----------------------+

.. table:: Extended Selector Attribute Macro Attributes

   +----------------------+-------------+------+----------------------+
   | Attribute Name       | Tag         | Type | Attribute            |
   |                      |             |      | Description          |
   +======================+=============+======+======================+
   | Selector Attribute   | (0082,0018) | 1    | Name of the Selector |
   | Name                 |             |      | Attribute            |
   |                      |             |      | (0072,0026).         |
   |                      |             |      |                      |
   |                      |             |      | For Standard Data    |
   |                      |             |      | Elements, this shall |
   |                      |             |      | be the value in the  |
   |                      |             |      | Name column of .     |
   +----------------------+-------------+------+----------------------+
   | Selector Attribute   | (0082,0019) | 3    | Keyword of the       |
   | Keyword              |             |      | Selector Attribute   |
   |                      |             |      | (0072,0026).         |
   |                      |             |      |                      |
   |                      |             |      | For Standard Data    |
   |                      |             |      | Elements, this shall |
   |                      |             |      | be the value in the  |
   |                      |             |      | Keyword column of .  |
   +----------------------+-------------+------+----------------------+
   | Selector Attribute   | (0072,0050) | 1    | Value Representation |
   | VR                   |             |      | of the Selector      |
   |                      |             |      | Attribute            |
   |                      |             |      | (0072,0026).         |
   |                      |             |      |                      |
   |                      |             |      | For Standard Data    |
   |                      |             |      | Elements, this shall |
   |                      |             |      | be the value in the  |
   |                      |             |      | VR column of .       |
   +----------------------+-------------+------+----------------------+
   | *                    |             |      |                      |
   | Include*\ `table_tit |             |      |                      |
   | le <#table_10-20>`__ |             |      |                      |
   +----------------------+-------------+------+----------------------+

.. _sect_10.17.1:

Selector Attribute Macro Attribute Descriptions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. _sect_10.17.1.1:

Referencing Nested Elements
^^^^^^^^^^^^^^^^^^^^^^^^^^^

Examples of use are shown in `table_title <#table_10-21>`__.

The examples include the selection of a top level Attribute, a nested
Attribute, one Item in a top level Sequence, all Items in a nested
Sequence or a specific Item in all Items of a parent Sequence.

.. table:: Selector Attribute Macro Example

   +-------------+-------------+-------------+-------------+-------------+
   | Example     | Selector    | Selector    | Selector    | Selector    |
   |             | Attribute   | Value       | Sequence    | Sequence    |
   |             | (0072,0026) | Number      | Pointer     | Pointer     |
   |             |             | (0072,0028) | (0072,0052) | Items       |
   |             |             |             |             | (0074,1057) |
   +=============+=============+=============+=============+=============+
   | Patient's   | (0010,0010) | 1           | absent      | absent      |
   | Name        |             |             |             |             |
   | (0010,0010) |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Second      | (0008,0008) | 2           | absent      | absent      |
   | value       |             |             |             |             |
   | (e.g.,      |             |             |             |             |
   | PRIMARY or  |             |             |             |             |
   | SECONDARY)  |             |             |             |             |
   | in Image    |             |             |             |             |
   | Type        |             |             |             |             |
   | (0008,0008) |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | RT Beam     | (300A,00B8) | 1           | (           | 1\2         |
   | Limiting    |             |             | 300A,00B0)\ |             |
   | Device Type |             |             | (300A,00B6) |             |
   | (300A,00B8) |             |             |             |             |
   | for the     |             |             |             |             |
   | second jaw  |             |             |             |             |
   | in Beam     |             |             |             |             |
   | Limiting    |             |             |             |             |
   | Device      |             |             |             |             |
   | Sequence    |             |             |             |             |
   | (300A,00B6) |             |             |             |             |
   | specified   |             |             |             |             |
   | for the     |             |             |             |             |
   | first Beam  |             |             |             |             |
   | in the Beam |             |             |             |             |
   | Sequence    |             |             |             |             |
   | (300A,00B0) |             |             |             |             |
   | of an RT    |             |             |             |             |
   | Plan        |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Code Value  | (0008,0100) | 1           | (0054,0220) | 1           |
   | (0008,0100) |             |             |             |             |
   | for the     |             |             |             |             |
   | first Item  |             |             |             |             |
   | in View     |             |             |             |             |
   | Code        |             |             |             |             |
   | Sequence    |             |             |             |             |
   | (0054,0220) |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | The second  | absent      | absent      | (300A,0180) | 2           |
   | Item in the |             |             |             |             |
   | Patient     |             |             |             |             |
   | Setup       |             |             |             |             |
   | Sequence    |             |             |             |             |
   | (300A,0180) |             |             |             |             |
   | in the top  |             |             |             |             |
   | level Data  |             |             |             |             |
   | Set         |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | The second  | absent      | absent      | (           | 3\2         |
   | Item in the |             |             | 300A,00B0)\ |             |
   | Beam        |             |             | (300A,00B6) |             |
   | Limiting    |             |             |             |             |
   | Device      |             |             |             |             |
   | Sequence    |             |             |             |             |
   | (300A,00B6) |             |             |             |             |
   | in third    |             |             |             |             |
   | Item in the |             |             |             |             |
   | Beam        |             |             |             |             |
   | Sequence    |             |             |             |             |
   | (300A,00B0) |             |             |             |             |
   | of an RT    |             |             |             |             |
   | Plan        |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | All Items   | absent      | absent      | (           | 3\0         |
   | in the Beam |             |             | 300A,00B0)\ |             |
   | Limiting    |             |             | (300A,00B6) |             |
   | Device      |             |             |             |             |
   | Sequence    |             |             |             |             |
   | (300A,00B6) |             |             |             |             |
   | in third    |             |             |             |             |
   | Item in the |             |             |             |             |
   | Beam        |             |             |             |             |
   | Sequence    |             |             |             |             |
   | (300A,00B0) |             |             |             |             |
   | of an RT    |             |             |             |             |
   | Plan        |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | The second  | absent      | absent      | (           | 0\2         |
   | Item in the |             |             | 300A,00B0)\ |             |
   | Beam        |             |             | (300A,00B6) |             |
   | Limiting    |             |             |             |             |
   | Device      |             |             |             |             |
   | Sequence    |             |             |             |             |
   | (300A,00B6) |             |             |             |             |
   | in all      |             |             |             |             |
   | Items in    |             |             |             |             |
   | the Beam    |             |             |             |             |
   | Sequence    |             |             |             |             |
   | (300A,00B0) |             |             |             |             |
   | of an RT    |             |             |             |             |
   | Plan        |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+

.. _sect_10.17.1.2:

Private Attribute References
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Selector Sequence Pointer Private Creator (0072,0054) and the
Selector Attribute Private Creator (0072,0056) each have a value that
corresponds to the Private Creator Data Element numbers (gggg,00pp),
where gggg is odd and pp ranges from 10 to FF. These identify a block of
Private Data Elements within the block (gggg,ppxx). When Selector
Attribute (0072,0026) or Selector Sequence Pointer (0072,0052) points to
a Private Data Element (gggg,ppxx), it shall have the value (gggg,00xx).

.. _sect_10.18:

Externally-Sourced Data Set Identification Macro
------------------------------------------------

`table_title <#table_10-22>`__ describes the Attributes for the
identification of an Externally-Sourced Data Set.

.. table:: Externally-Sourced Data Set Identification Macro Attributes

   +----------------------+-------------+------+----------------------+
   | Attribute Name       | Tag         | Type | Attribute            |
   |                      |             |      | Description          |
   +======================+=============+======+======================+
   | Data Set Name        | (0024,0306) | 1    | The name assigned to |
   |                      |             |      | the                  |
   |                      |             |      | Externally-Sourced   |
   |                      |             |      | Data Set.            |
   +----------------------+-------------+------+----------------------+
   | Data Set Version     | (0024,0307) | 1    | The software version |
   |                      |             |      | identifier assigned  |
   |                      |             |      | to the               |
   |                      |             |      | Externally-Sourced   |
   |                      |             |      | Data Set.            |
   +----------------------+-------------+------+----------------------+
   | Data Set Source      | (0024,0308) | 1    | Source of the        |
   |                      |             |      | Externally-Sourced   |
   |                      |             |      | Data Set. E.g., the  |
   |                      |             |      | name of the          |
   |                      |             |      | manufacturer,        |
   |                      |             |      | researcher,          |
   |                      |             |      | university, etc.     |
   +----------------------+-------------+------+----------------------+
   | Data Set Description | (0024,0309) | 3    | Description of the   |
   |                      |             |      | Externally-Sourced   |
   |                      |             |      | Data Set.            |
   +----------------------+-------------+------+----------------------+

.. _sect_10.19:

Exposure Index Macro
--------------------

`table_title <#table_10-23>`__ describes the Attributes for describing
the Exposure Index for single projection X-Ray images, as described by
IEC 62494-1 and the report of AAPM Task Group 116.

.. table:: Exposure Index Macro Attributes

   +----------------------+-------------+------+----------------------+
   | Attribute Name       | Tag         | Type | Attribute            |
   |                      |             |      | Description          |
   +======================+=============+======+======================+
   | Exposure Index       | (0018,1411) | 3    | Measure of the       |
   |                      |             |      | detector response to |
   |                      |             |      | radiation in the     |
   |                      |             |      | relevant image       |
   |                      |             |      | region of an image   |
   |                      |             |      | acquired with a      |
   |                      |             |      | digital X-Ray        |
   |                      |             |      | imaging system as    |
   |                      |             |      | defined in IEC       |
   |                      |             |      | 62494-1.             |
   |                      |             |      |                      |
   |                      |             |      | .. note::            |
   |                      |             |      |                      |
   |                      |             |      |    1. A string       |
   |                      |             |      |       rather than    |
   |                      |             |      |       binary Value   |
   |                      |             |      |       Representation |
   |                      |             |      |       is used for    |
   |                      |             |      |       this           |
   |                      |             |      |       Attribute, in  |
   |                      |             |      |       order to allow |
   |                      |             |      |       the sender to  |
   |                      |             |      |       control the    |
   |                      |             |      |       precision of   |
   |                      |             |      |       the value as   |
   |                      |             |      |       suggested in   |
   |                      |             |      |       the report of  |
   |                      |             |      |       AAPM Task      |
   |                      |             |      |       Group 116.     |
   |                      |             |      |                      |
   |                      |             |      |    2. This index     |
   |                      |             |      |       value is       |
   |                      |             |      |       scaled as      |
   |                      |             |      |       defined by IEC |
   |                      |             |      |       62494-1.       |
   +----------------------+-------------+------+----------------------+
   | Target Exposure      | (0018,1412) | 3    | The target value     |
   | Index                |             |      | used to calculate    |
   |                      |             |      | Deviation Index      |
   |                      |             |      | (0018,1413) as       |
   |                      |             |      | defined in IEC       |
   |                      |             |      | 62494-1.             |
   +----------------------+-------------+------+----------------------+
   | Deviation Index      | (0018,1413) | 3    | A scaled             |
   |                      |             |      | representation of    |
   |                      |             |      | the difference of    |
   |                      |             |      | the Exposure Index   |
   |                      |             |      | compared to the      |
   |                      |             |      | Target Exposure      |
   |                      |             |      | Index as defined in  |
   |                      |             |      | IEC 62494-1 and the  |
   |                      |             |      | report of AAPM TG    |
   |                      |             |      | 116.                 |
   +----------------------+-------------+------+----------------------+

.. _sect_10.20:

Mandatory View and Slice Progression Direction Macro
----------------------------------------------------

`table_title <#table_10-24>`__ specifies the Attributes that describe
the view, and in the case of cardiac views, the direction of the slices
relative to the cardiac anatomy.

.. table:: Mandatory View and Slice Progression Direction Macro
Attributes

   +-------------------+-------------------+------+-------------------+
   | Attribute Name    | Tag               | Type | Attribute         |
   |                   |                   |      | Description       |
   +===================+===================+======+===================+
   | View Code         | (0054,0220)       | 1    | Sequence that     |
   | Sequence          |                   |      | describes the     |
   |                   |                   |      | projection of the |
   |                   |                   |      | anatomic region   |
   |                   |                   |      | of interest.      |
   |                   |                   |      |                   |
   |                   |                   |      | Only a single     |
   |                   |                   |      | Item shall be     |
   |                   |                   |      | included in this  |
   |                   |                   |      | Sequence.         |
   +-------------------+-------------------+------+-------------------+
   | *>Includ          | *B unless         |      |                   |
   | e*\ `table_title  | otherwise         |      |                   |
   | <#table_8.8-1>`__ | specified in      |      |                   |
   |                   | invocation.*      |      |                   |
   +-------------------+-------------------+------+-------------------+
   | >View Modifier    | (0054,0222)       | 2C   | View Modifier.    |
   | Code Sequence     |                   |      |                   |
   |                   |                   |      | Required if       |
   |                   |                   |      | needed to fully   |
   |                   |                   |      | specify the View. |
   |                   |                   |      |                   |
   |                   |                   |      | Zero or more      |
   |                   |                   |      | Items shall be    |
   |                   |                   |      | included in this  |
   |                   |                   |      | Sequence.         |
   +-------------------+-------------------+------+-------------------+
   | *>>Includ         | *B unless         |      |                   |
   | e*\ `table_title  | otherwise         |      |                   |
   | <#table_8.8-1>`__ | specified in      |      |                   |
   |                   | invocation.*      |      |                   |
   +-------------------+-------------------+------+-------------------+
   | Slice Progression | (0054,0500)       | 1C   | Describes the     |
   | Direction         |                   |      | anatomical        |
   |                   |                   |      | direction in      |
   |                   |                   |      | which a set of    |
   |                   |                   |      | slices is         |
   |                   |                   |      | progressing (see  |
   |                   |                   |      | `Slice            |
   |                   |                   |      | Progression       |
   |                   |                   |      | Direction <#sec   |
   |                   |                   |      | t_10.20.1.1>`__). |
   |                   |                   |      | Meaningful only   |
   |                   |                   |      | for cardiac       |
   |                   |                   |      | images.           |
   |                   |                   |      |                   |
   |                   |                   |      | Enumerated Values |
   |                   |                   |      | are defined in    |
   |                   |                   |      | `Slice            |
   |                   |                   |      | Progression       |
   |                   |                   |      | Direction <#se    |
   |                   |                   |      | ct_10.20.1.1>`__. |
   |                   |                   |      |                   |
   |                   |                   |      | Required if View  |
   |                   |                   |      | Code Sequence     |
   |                   |                   |      | (0054,0220)       |
   |                   |                   |      | equals            |
   |                   |                   |      | `(103340004, SCT, |
   |                   |                   |      | "Short            |
   |                   |                   |      | Axis") <h         |
   |                   |                   |      | ttp://snomed.info |
   |                   |                   |      | /id/103340004>`__ |
   |                   |                   |      | or `(131185001,   |
   |                   |                   |      | SCT, "Vertical    |
   |                   |                   |      | Long              |
   |                   |                   |      | Axis") <h         |
   |                   |                   |      | ttp://snomed.info |
   |                   |                   |      | /id/131185001>`__ |
   |                   |                   |      | or `(131186000,   |
   |                   |                   |      | SCT, "Horizontal  |
   |                   |                   |      | Long              |
   |                   |                   |      | Axis") <ht        |
   |                   |                   |      | tp://snomed.info/ |
   |                   |                   |      | id/131186000>`__. |
   |                   |                   |      | May be present    |
   |                   |                   |      | otherwise.        |
   +-------------------+-------------------+------+-------------------+

.. _sect_10.20.1:

Mandatory View and Slice Progression Direction Macro Attributes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. _sect_10.20.1.1:

Slice Progression Direction
^^^^^^^^^^^^^^^^^^^^^^^^^^^

The image or frame order to which the Slice Progression Direction
(0054,0500) applies depends on the IOD:

-  In the case of Enhanced Multi-frame IODs, in which a Stack ID
   (0020,9056) may be defined, Stack ID (0020,9056) shall be used, and
   the slices are considered in order by In Stack Position Number
   (0020,9057)

-  In the case of Multi-frame IODs that are not Enhanced, the slices are
   considered in encoded frame order

-  In the case of single-frame IODs, the order is defined by increasing
   values of Instance Number

The Enumerated Values depend on the view:

-  If View Code Sequence (0054,0220) indicates a short axis view, such
   as when it equals `(103340004, SCT, "Short
   Axis") <http://snomed.info/id/103340004>`__:

   APEX_TO_BASE
   BASE_TO_APEX

-  If View Code Sequence (0054,0220) indicates a vertical long axis
   view, such as when it equals `(131185001, SCT, "Vertical Long
   Axis") <http://snomed.info/id/131185001>`__:

   ANT_TO_INF
      Anterior to Inferior

   INF_TO_ANT
      Inferior to Anterior

-  If View Code Sequence (0054,0220) indicates a horizontal long axis
   view, such as when it equals `(131186000, SCT, "Horizontal Long
   Axis") <http://snomed.info/id/131186000>`__:

   SEPTUM_TO_WALL
      Septum to Lateral Wall

   WALL_TO_SEPTUM
      Lateral Wall to Septum

.. note::

   The conditions on the choice of Enumerated Values are relatively
   general, rather than specific to a single coded view, in order to
   accommodate the echocardiography views defined in , in addition to
   the views for CT, MR, NM and PET defined in .

.. _sect_10.21:

Optional View and Slice Progression Direction Macro
---------------------------------------------------

`table_title <#table_10-25>`__ specifies the Attributes that describe
the view, and in the case of cardiac views, the direction of the slices
relative to the cardiac anatomy.

.. table:: Optional View and Slice Progression Direction Macro
Attributes

   +-------------------+-------------------+------+-------------------+
   | Attribute Name    | Tag               | Type | Attribute         |
   |                   |                   |      | Description       |
   +===================+===================+======+===================+
   | View Code         | (0054,0220)       | 3    | Sequence that     |
   | Sequence          |                   |      | describes the     |
   |                   |                   |      | projection of the |
   |                   |                   |      | anatomic region   |
   |                   |                   |      | of interest.      |
   |                   |                   |      |                   |
   |                   |                   |      | Only a single     |
   |                   |                   |      | Item is permitted |
   |                   |                   |      | in this Sequence. |
   +-------------------+-------------------+------+-------------------+
   | *>Includ          | *B unless         |      |                   |
   | e*\ `table_title  | otherwise         |      |                   |
   | <#table_8.8-1>`__ | specified in      |      |                   |
   |                   | invocation.*      |      |                   |
   +-------------------+-------------------+------+-------------------+
   | >View Modifier    | (0054,0222)       | 3    | View Modifier.    |
   | Code Sequence     |                   |      |                   |
   |                   |                   |      | One or more Items |
   |                   |                   |      | are permitted in  |
   |                   |                   |      | this Sequence.    |
   +-------------------+-------------------+------+-------------------+
   | *>>Includ         | *B unless         |      |                   |
   | e*\ `table_title  | otherwise         |      |                   |
   | <#table_8.8-1>`__ | specified in      |      |                   |
   |                   | invocation.*      |      |                   |
   +-------------------+-------------------+------+-------------------+
   | Slice Progression | (0054,0500)       | 3    | Describes the     |
   | Direction         |                   |      | anatomical        |
   |                   |                   |      | direction in      |
   |                   |                   |      | which a set of    |
   |                   |                   |      | slices is         |
   |                   |                   |      | progressing (see  |
   |                   |                   |      | `Slice            |
   |                   |                   |      | Progression       |
   |                   |                   |      | Direction <#sec   |
   |                   |                   |      | t_10.20.1.1>`__). |
   |                   |                   |      | Meaningful only   |
   |                   |                   |      | for cardiac       |
   |                   |                   |      | images.           |
   |                   |                   |      |                   |
   |                   |                   |      | Enumerated Values |
   |                   |                   |      | are defined in    |
   |                   |                   |      | `Slice            |
   |                   |                   |      | Progression       |
   |                   |                   |      | Direction <#se    |
   |                   |                   |      | ct_10.20.1.1>`__. |
   +-------------------+-------------------+------+-------------------+

.. _sect_10.22:

Numeric Value Macro
-------------------

`table_title <#table_10-26>`__ describes the Attributes used to relate
and convey a numeric value to a coded concept.

.. table:: Numeric Value Macro Attributes

   +-------------------+-------------------+------+-------------------+
   | Attribute Name    | Tag               | Type | Attribute         |
   |                   |                   |      | Description       |
   +===================+===================+======+===================+
   | Concept Name Code | (0040,A043)       | 1    | Coded concept     |
   | Sequence          |                   |      | name of this      |
   |                   |                   |      | name-value Item.  |
   |                   |                   |      |                   |
   |                   |                   |      | Only a single     |
   |                   |                   |      | Item shall be     |
   |                   |                   |      | included in this  |
   |                   |                   |      | Sequence.         |
   +-------------------+-------------------+------+-------------------+
   | *>Includ          | *No Context ID is |      |                   |
   | e*\ `table_title  | defined.*         |      |                   |
   | <#table_8.8-1>`__ |                   |      |                   |
   +-------------------+-------------------+------+-------------------+
   | Numeric Value     | (0040,A30A)       | 1    | Numeric value for |
   |                   |                   |      | this name-value   |
   |                   |                   |      | Item.             |
   +-------------------+-------------------+------+-------------------+
   | Measurement Units | (0040,08EA)       | 1    | Units of Numeric  |
   | Code Sequence     |                   |      | Value (0040,A30A) |
   |                   |                   |      | in this           |
   |                   |                   |      | name-value Item.  |
   |                   |                   |      |                   |
   |                   |                   |      | Only a single     |
   |                   |                   |      | Item shall be     |
   |                   |                   |      | included in this  |
   |                   |                   |      | Sequence.         |
   +-------------------+-------------------+------+-------------------+
   | *>Includ          | *D.*              |      |                   |
   | e*\ `table_title  |                   |      |                   |
   | <#table_8.8-1>`__ |                   |      |                   |
   +-------------------+-------------------+------+-------------------+

.. _sect_10.23:

RT Equipment Correlation Macro
------------------------------

.. table:: RT Equipment Correlation Macro Attributes Description

   +----------------------+-------------+------+----------------------+
   | Attribute Name       | Tag         | Type | Attribute            |
   |                      |             |      | Description          |
   +======================+=============+======+======================+
   | Patient Support      | (300A,0122) | 3    | Patient Support      |
   | Angle                |             |      | angle, i.e.,         |
   |                      |             |      | orientation of IEC   |
   |                      |             |      | PATIENT SUPPORT      |
   |                      |             |      | coordinate system    |
   |                      |             |      | with respect to IEC  |
   |                      |             |      | FIXED REFERENCE      |
   |                      |             |      | coordinate system    |
   |                      |             |      | (degrees).           |
   +----------------------+-------------+------+----------------------+
   | Table Top Pitch      | (300A,0140) | 3    | Table Top Pitch      |
   | Angle                |             |      | Angle, i.e., the     |
   |                      |             |      | rotation of the IEC  |
   |                      |             |      | TABLE TOP coordinate |
   |                      |             |      | system about the     |
   |                      |             |      | X-axis of the IEC    |
   |                      |             |      | TABLE TOP coordinate |
   |                      |             |      | system (degrees).    |
   |                      |             |      | See `Table Top Pitch |
   |                      |             |      | and Table Top        |
   |                      |             |      | Roll <#se            |
   |                      |             |      | ct_C.8.8.25.6.2>`__. |
   +----------------------+-------------+------+----------------------+
   | Table Top Roll Angle | (300A,0144) | 3    | Table Top Roll       |
   |                      |             |      | Angle, i.e., the     |
   |                      |             |      | rotation of the IEC  |
   |                      |             |      | TABLE TOP coordinate |
   |                      |             |      | system about the     |
   |                      |             |      | Y-axis of the IEC    |
   |                      |             |      | TABLE TOP coordinate |
   |                      |             |      | system (degrees).    |
   |                      |             |      | See `Table Top Pitch |
   |                      |             |      | and Table Top        |
   |                      |             |      | Roll <#se            |
   |                      |             |      | ct_C.8.8.25.6.2>`__. |
   +----------------------+-------------+------+----------------------+
   | Table Top            | (300A,0129) | 3    | Table Top            |
   | Longitudinal         |             |      | Longitudinal         |
   | Position             |             |      | position in IEC      |
   |                      |             |      | TABLE TOP coordinate |
   |                      |             |      | system (mm).         |
   +----------------------+-------------+------+----------------------+
   | Table Top Lateral    | (300A,012A) | 3    | Table Top Lateral    |
   | Position             |             |      | position in IEC      |
   |                      |             |      | TABLE TOP coordinate |
   |                      |             |      | system (mm).         |
   +----------------------+-------------+------+----------------------+

.. _sect_10.24:

Device Motion Control Macro
---------------------------

`table_title <#table_10-28>`__ specifies the Attributes that describe
requirements on performing the movement of a device from an actual to a
desired position.

.. table:: Device Motion Control Macro Attributes Description

   +----------------------+-------------+------+----------------------+
   | Attribute Name       | Tag         | Type | Attribute            |
   |                      |             |      | Description          |
   +======================+=============+======+======================+
   | Device Motion        | (300A,0450) | 3    | Device Motion        |
   | Control Sequence     |             |      | Control Definitions  |
   |                      |             |      | for each degree of   |
   |                      |             |      | freedom.             |
   |                      |             |      |                      |
   |                      |             |      | One or more Items    |
   |                      |             |      | are permitted in     |
   |                      |             |      | this Sequence.       |
   +----------------------+-------------+------+----------------------+
   | >Device Motion       | (300A,0453) | 1    | The parameter for    |
   | Parameter Code       |             |      | which the Device     |
   | Sequence             |             |      | Motion Control shall |
   |                      |             |      | be applied.          |
   +----------------------+-------------+------+----------------------+
   | *>>                  | *D*         |      |                      |
   | Include*\ `table_tit |             |      |                      |
   | le <#table_8.8-1>`__ |             |      |                      |
   +----------------------+-------------+------+----------------------+
   | >Device Motion       | (300A,0451) | 1C   | Permitted Motion     |
   | Execution Mode       |             |      | Execution Mode for   |
   |                      |             |      | movement.            |
   |                      |             |      |                      |
   |                      |             |      | Required if Device   |
   |                      |             |      | Motion Observation   |
   |                      |             |      | Mode (300A,0452) is  |
   |                      |             |      | absent. May be       |
   |                      |             |      | present otherwise.   |
   |                      |             |      |                      |
   |                      |             |      | See `Device Motion   |
   |                      |             |      | Execution            |
   |                      |             |      | Mode <               |
   |                      |             |      | #sect_10.24.1.1>`__. |
   +----------------------+-------------+------+----------------------+
   | >Device Motion       | (300A,0452) | 1C   | Required Motion      |
   | Observation Mode     |             |      | Observation Mode for |
   |                      |             |      | movement.            |
   |                      |             |      |                      |
   |                      |             |      | Required if Device   |
   |                      |             |      | Motion Execution     |
   |                      |             |      | Mode (300A,0451) is  |
   |                      |             |      | absent. May be       |
   |                      |             |      | present otherwise.   |
   |                      |             |      |                      |
   |                      |             |      | See `Device Motion   |
   |                      |             |      | Observation          |
   |                      |             |      | Mode <               |
   |                      |             |      | #sect_10.24.1.2>`__. |
   +----------------------+-------------+------+----------------------+

.. _sect_10.24.1:

Device Motion Control Macro Attributes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. _sect_10.24.1.1:

Device Motion Execution Mode
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Device Motion Execution Mode (300A,0451) identifies how the operator
invokes and controls the motion.

CONTINUOUS
   The device must be moved while the operator is activating one or more
   switches on the machine during the whole period of movement to
   prevent any uncontrolled movement.

TRIGGERED
   The device can be moved automatically to the desired position,
   triggered by a one-time command of the operator, without the need to
   constantly activate any switch.

AUTOMATIC
   The device movement can be initiated and performed automatically by
   the device to the desired position.

.. _sect_10.24.1.2:

Device Motion Observation Mode
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Device Motion Observation Mode (300A,0452) describes the presence of the
operator in the room, observing the motion.

INROOM
   The movement of the device is only allowed when the operator is
   present in the treatment room.

REMOTE
   The device can be moved by a command of the operator not being
   present in the treatment room, that is, from a device outside the
   treatment room.

.. _sect_10.25:

Attribute Value Constraint Macro
--------------------------------

`table_title <#table_10.25-1>`__ allows an Attribute to be identified
and to have constraints placed on acceptable values for that Attribute.
An Attribute being constrained is refered to in the Macro as a Selector
Attribute.

.. note::

   1. This Macro does not handle mutual constraints between multiple
      Attributes. For example constraining the ratio between two
      Attributes to a specific value is not possible unless there is a
      third Attribute that encodes that ratio so the third Attribute
      could then be constrained.

   2. The SOP Instance containing this Macro defines the purpose of the
      constraints, which may include constraining Attribute values in
      other SOP Instances.

.. table:: Attribute Value Constraint Macro Attributes

   +-------------------+-------------------+------+-------------------+
   | Attribute Name    | Tag               | Type | Attribute         |
   |                   |                   |      | Description       |
   +===================+===================+======+===================+
   | *Include          |                   |      |                   |
   | *\ `table_title < |                   |      |                   |
   | #table_10-20a>`__ |                   |      |                   |
   +-------------------+-------------------+------+-------------------+
   | Constraint Type   | (0082,0032)       | 1    | Describes how the |
   |                   |                   |      | value(s)          |
   |                   |                   |      | specified in the  |
   |                   |                   |      | Constraint Value  |
   |                   |                   |      | Sequence          |
   |                   |                   |      | (0082,0034) shall |
   |                   |                   |      | be used to        |
   |                   |                   |      | determine the     |
   |                   |                   |      | acceptability of  |
   |                   |                   |      | a given value for |
   |                   |                   |      | the Attribute     |
   |                   |                   |      | identified by     |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute         |
   |                   |                   |      | (0072,0026)       |
   |                   |                   |      |                   |
   |                   |                   |      | See `Constraint   |
   |                   |                   |      | Type <#           |
   |                   |                   |      | sect_10.25.1>`__. |
   |                   |                   |      |                   |
   |                   |                   |      | RANGE_INCL        |
   |                   |                   |      | RANGE_EXCL        |
   |                   |                   |      | GREATER_OR_EQUAL  |
   |                   |                   |      | LESS_OR_EQUAL     |
   |                   |                   |      | GREATER_THAN      |
   |                   |                   |      | LESS_THAN         |
   |                   |                   |      | EQUAL             |
   |                   |                   |      | MEMBER_OF         |
   |                   |                   |      | NOT_MEMBER_OF     |
   |                   |                   |      | MEMBER_OF_CID     |
   |                   |                   |      | UNCONSTRAINED     |
   +-------------------+-------------------+------+-------------------+
   | Constraint        | (0082,0036)       | 3    | Level of          |
   | Violation         |                   |      | significance of a |
   | Significance      |                   |      | Selector          |
   |                   |                   |      | Attribute value   |
   |                   |                   |      | exceeding this    |
   |                   |                   |      | constraint.       |
   |                   |                   |      |                   |
   |                   |                   |      | See `Constraint   |
   |                   |                   |      | Violation         |
   |                   |                   |      | Significance <#   |
   |                   |                   |      | sect_10.25.2>`__. |
   |                   |                   |      |                   |
   |                   |                   |      | FAILURE           |
   |                   |                   |      | WARNING           |
   |                   |                   |      | INFORMATIVE       |
   +-------------------+-------------------+------+-------------------+
   | Constraint        | (0082,0037)       | 1C   | Conditionality of |
   | Violation         |                   |      | the constraint    |
   | Condition         |                   |      | violation         |
   |                   |                   |      | significance. If  |
   |                   |                   |      | the condition is  |
   |                   |                   |      | not met, the      |
   |                   |                   |      | violation has no  |
   |                   |                   |      | significance.     |
   |                   |                   |      |                   |
   |                   |                   |      | The condition may |
   |                   |                   |      | be expressed as a |
   |                   |                   |      | mathematical      |
   |                   |                   |      | expression, a     |
   |                   |                   |      | human readable    |
   |                   |                   |      | text or other     |
   |                   |                   |      | form.             |
   |                   |                   |      |                   |
   |                   |                   |      | Required if       |
   |                   |                   |      | Constraint        |
   |                   |                   |      | Violation         |
   |                   |                   |      | Significance      |
   |                   |                   |      | (0082,0036) is    |
   |                   |                   |      | only significant  |
   |                   |                   |      | under certain     |
   |                   |                   |      | conditions.       |
   +-------------------+-------------------+------+-------------------+
   | Constraint Value  | (0082,0034)       | 1C   | Value(s) used to  |
   | Sequence          |                   |      | constrain the     |
   |                   |                   |      | contents of the   |
   |                   |                   |      | Attribute         |
   |                   |                   |      | referenced by the |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute         |
   |                   |                   |      | (0072,0026).      |
   |                   |                   |      |                   |
   |                   |                   |      | Required if       |
   |                   |                   |      | Constraint Type   |
   |                   |                   |      | (0082,0032) is    |
   |                   |                   |      | not               |
   |                   |                   |      | UNCONSTRAINED.    |
   |                   |                   |      |                   |
   |                   |                   |      | If the Constraint |
   |                   |                   |      | Type (0082,0032)  |
   |                   |                   |      | is                |
   |                   |                   |      | GREATER_OR_EQUAL, |
   |                   |                   |      | LESS_OR_EQUAL,    |
   |                   |                   |      | GREATER_THAN,     |
   |                   |                   |      | LESS_THAN, EQUAL  |
   |                   |                   |      | or MEMBER_OF_CID  |
   |                   |                   |      | only a single     |
   |                   |                   |      | Item shall be     |
   |                   |                   |      | included in this  |
   |                   |                   |      | Sequence.         |
   |                   |                   |      |                   |
   |                   |                   |      | If the Constraint |
   |                   |                   |      | Type (0082,0032)  |
   |                   |                   |      | is RANGE_INCL or  |
   |                   |                   |      | RANGE_EXCL,       |
   |                   |                   |      | exactly two Items |
   |                   |                   |      | shall be included |
   |                   |                   |      | in this Sequence, |
   |                   |                   |      | the first of      |
   |                   |                   |      | which is less     |
   |                   |                   |      | than or equal to  |
   |                   |                   |      | the second.       |
   |                   |                   |      |                   |
   |                   |                   |      | If the Constraint |
   |                   |                   |      | Type (0082,0032)  |
   |                   |                   |      | is MEMBER_OF or   |
   |                   |                   |      | NOT_MEMBER_OF,    |
   |                   |                   |      | one or more Items |
   |                   |                   |      | shall be included |
   |                   |                   |      | in this Sequence. |
   +-------------------+-------------------+------+-------------------+
   | *>Include*        | Any sub-Sequences |      |                   |
   | \ `table_title <# | in the Constraint |      |                   |
   | table_10.26-1>`__ | Value Sequence    |      |                   |
   |                   | (0082,0034) shall |      |                   |
   |                   | only contain one  |      |                   |
   |                   | Item.             |      |                   |
   |                   |                   |      |                   |
   |                   | Any Attribute in  |      |                   |
   |                   | the Sequence      |      |                   |
   |                   | Item(s) shall     |      |                   |
   |                   | contain a single  |      |                   |
   |                   | value.            |      |                   |
   |                   |                   |      |                   |
   |                   | If Constraint     |      |                   |
   |                   | Type (0082,0032)  |      |                   |
   |                   | is MEMBER_OF_CID, |      |                   |
   |                   | this shall be a   |      |                   |
   |                   | Selector UI Value |      |                   |
   |                   | (0072,007F),      |      |                   |
   |                   | despite the       |      |                   |
   |                   | Selector          |      |                   |
   |                   | Attribute VR      |      |                   |
   |                   | (0072,0050) being |      |                   |
   |                   | SQ.               |      |                   |
   |                   |                   |      |                   |
   |                   | See `Multi-valued |      |                   |
   |                   | Attribute         |      |                   |
   |                   | Constraints <#s   |      |                   |
   |                   | ect_10.25.1.1>`__ |      |                   |
   +-------------------+-------------------+------+-------------------+
   | Recommended       | (0082,0035)       | 3    | Contains a        |
   | Default Value     |                   |      | default value for |
   | Sequence          |                   |      | the contents of   |
   |                   |                   |      | the Selector      |
   |                   |                   |      | Attribute         |
   |                   |                   |      | (0072,0026).      |
   |                   |                   |      |                   |
   |                   |                   |      | Only a single     |
   |                   |                   |      | Item is permitted |
   |                   |                   |      | in this Sequence. |
   +-------------------+-------------------+------+-------------------+
   | *>Include*        |                   |      |                   |
   | \ `table_title <# |                   |      |                   |
   | table_10.26-1>`__ |                   |      |                   |
   +-------------------+-------------------+------+-------------------+
   | Measurement Units | (0040,08EA)       | 3    | Units of          |
   | Code Sequence     |                   |      | measurement for   |
   |                   |                   |      | the values in the |
   |                   |                   |      | Item(s) in the    |
   |                   |                   |      | Constraint Value  |
   |                   |                   |      | Sequence          |
   |                   |                   |      | (0082,0034) and   |
   |                   |                   |      | the Recommended   |
   |                   |                   |      | Default Value     |
   |                   |                   |      | Sequence          |
   |                   |                   |      | (0082,0035).      |
   |                   |                   |      |                   |
   |                   |                   |      | Only a single     |
   |                   |                   |      | Item is permitted |
   |                   |                   |      | in this Sequence. |
   +-------------------+-------------------+------+-------------------+
   | *>Includ          | *B.*              |      |                   |
   | e*\ `table_title  |                   |      |                   |
   | <#table_8.8-1>`__ |                   |      |                   |
   +-------------------+-------------------+------+-------------------+
   | Specification     | (0082,0033)       | 3    | Brief guidance    |
   | Selection         |                   |      | that a human      |
   | Guidance          |                   |      | operator may      |
   |                   |                   |      | consider when     |
   |                   |                   |      | selecting an      |
   |                   |                   |      | appropriate value |
   |                   |                   |      | for the Selector  |
   |                   |                   |      | Attribute         |
   |                   |                   |      | (0072,0026)       |
   |                   |                   |      | within the        |
   |                   |                   |      | constraints       |
   |                   |                   |      | defined.          |
   +-------------------+-------------------+------+-------------------+

.. _sect_10.25.1:

Constraint Type
~~~~~~~~~~~~~~~

The use of the specified value(s) in the Constraint Value Sequence
(0082,0034) to constrain the value of the Attribute referenced by the
Selector Attribute (0072,0026) shall depend on the value of Constraint
Type (0082,0032) as follows:

RANGE_EXCL
   the value is constrained to lie outside (i.e., not between) the
   specified values

GREATER_OR_EQUAL
   the value is constrained to be greater than or equal to the specified
   value

LESS_OR_EQUAL
   the value is constrained to be less than or equal to the specified
   value

GREATER_THAN
   the value is constrained to be greater than the specified value

LESS_THAN
   the value is constrained to be less than the specified value

EQUAL
   the value is constrained to be equal to the specified value

MEMBER_OF
   the value is constrained to be equal to one of the specified values

NOT_MEMBER_OF
   the value is constrained to be not equal to any of the specified
   values

MEMBER_OF_CID
   the value is constrained to be equal to a member of the specified CID

UNCONSTRAINED
   the value of the Selector Attribute (0072,0026) is not constrained

For MEMBER_OF_CID, Constraint Value Sequence (0082,0034) shall contain a
single Selector UI Value (0072,007F) , containing a Context Group UID
(see PS 3.6, Table A-3. Context Group UID Values).

RANGE_INCL, RANGE_EXCL, GREATER_OR_EQUAL, LESS_OR_EQUAL, GREATER_THAN or
LESS_THAN shall only be specified if the Selector Attribute (0072,0026)
is AS, DA, DS, DT, FD, FL, IS, SL, SS, TM, UL or US.

See for further guidance on value comparison.

.. note::

   MEMBER_OF with a single Item in the Constraint Value Sequence
   (0082,0034) is valid and is equivalent to EQUAL.

.. _sect_10.25.1.1:

Multi-valued Attribute Constraints
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

If the Attribute referenced by the Selector Attribute (0072,0026) has a
value multiplicity of greater than 1 and the value of Selector Value
Number (0072,0028) is 0, all values in the selected Attribute shall be
compared to the single specified value. The constraint is violated if
any of the multiple values do not satisfy the comparison.

.. _sect_10.25.2:

Constraint Violation Significance
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The violation of some constraints may be more significant than others.
Constraint Violation Significance (0082,0036) differentiates three
levels of signficance.

Specific behaviors associated with each level may be defined by the SOP
Class or may be left to implementations. For example, violation of a
constraint with a significance of FAILURE might require operator
intervention, special auditing or rejection of the target Instance being
evaluated; violation of a constraint with a significance of WARNING
might require the operator be notified or a warning message be logged;
violation of a constraint with a significance of INFORMATIVE might
require an informational message be logged, or nothing at all if the
constraint represents a preference not a signficant concern.

.. note::

   Violation of a constraint does not imply that the Selector Attribute
   value is non-conformant to the Standard or is not clinically
   appropriate.

.. _sect_10.26:

Attribute Value Macro
---------------------

`table_title <#table_10.26-1>`__ includes an Attribute to store a value
of a specified VR.

.. table:: Attribute Value Macro Attributes

   +-------------------+-------------------+------+-------------------+
   | Attribute Name    | Tag               | Type | Attribute         |
   |                   |                   |      | Description       |
   +===================+===================+======+===================+
   | Selector AE Value | (0072,005E)       | 1C   | The value(s) of   |
   |                   |                   |      | the Attribute     |
   |                   |                   |      | identified by     |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute         |
   |                   |                   |      | (0072,0026).      |
   |                   |                   |      |                   |
   |                   |                   |      | Required if       |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute VR      |
   |                   |                   |      | (0072,0050) is    |
   |                   |                   |      | present and the   |
   |                   |                   |      | value is AE.      |
   +-------------------+-------------------+------+-------------------+
   | Selector AS Value | (0072,005F)       | 1C   | The value(s) of   |
   |                   |                   |      | the Attribute     |
   |                   |                   |      | identified by     |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute         |
   |                   |                   |      | (0072,0026).      |
   |                   |                   |      |                   |
   |                   |                   |      | Required if       |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute VR      |
   |                   |                   |      | (0072,0050) is    |
   |                   |                   |      | present and the   |
   |                   |                   |      | value is AS.      |
   +-------------------+-------------------+------+-------------------+
   | Selector AT Value | (0072,0060)       | 1C   | The value(s) of   |
   |                   |                   |      | the Attribute     |
   |                   |                   |      | identified by     |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute         |
   |                   |                   |      | (0072,0026).      |
   |                   |                   |      |                   |
   |                   |                   |      | Required if       |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute VR      |
   |                   |                   |      | (0072,0050) is    |
   |                   |                   |      | present and the   |
   |                   |                   |      | value is AT.      |
   +-------------------+-------------------+------+-------------------+
   | Selector CS Value | (0072,0062)       | 1C   | The value(s) of   |
   |                   |                   |      | the Attribute     |
   |                   |                   |      | identified by     |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute         |
   |                   |                   |      | (0072,0026).      |
   |                   |                   |      |                   |
   |                   |                   |      | Required if       |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute VR      |
   |                   |                   |      | (0072,0050) is    |
   |                   |                   |      | present and the   |
   |                   |                   |      | value is CS.      |
   +-------------------+-------------------+------+-------------------+
   | Selector DA Value | (0072,0061)       | 1C   | The value(s) of   |
   |                   |                   |      | the Attribute     |
   |                   |                   |      | identified by     |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute         |
   |                   |                   |      | (0072,0026).      |
   |                   |                   |      |                   |
   |                   |                   |      | Required if       |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute VR      |
   |                   |                   |      | (0072,0050) is    |
   |                   |                   |      | present and the   |
   |                   |                   |      | value is DA.      |
   |                   |                   |      |                   |
   |                   |                   |      | See Note 2.       |
   +-------------------+-------------------+------+-------------------+
   | Selector DS Value | (0072,0072)       | 1C   | The value(s) of   |
   |                   |                   |      | the Attribute     |
   |                   |                   |      | identified by     |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute         |
   |                   |                   |      | (0072,0026).      |
   |                   |                   |      |                   |
   |                   |                   |      | Required if       |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute VR      |
   |                   |                   |      | (0072,0050) is    |
   |                   |                   |      | present and the   |
   |                   |                   |      | value is DS. See  |
   |                   |                   |      | Note 1 and Note   |
   |                   |                   |      | 2.                |
   +-------------------+-------------------+------+-------------------+
   | Selector DT Value | (0072,0063)       | 1C   | The value(s) of   |
   |                   |                   |      | the Attribute     |
   |                   |                   |      | identified by     |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute         |
   |                   |                   |      | (0072,0026).      |
   |                   |                   |      |                   |
   |                   |                   |      | Required if       |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute VR      |
   |                   |                   |      | (0072,0050) is    |
   |                   |                   |      | present and the   |
   |                   |                   |      | value is DT.      |
   |                   |                   |      |                   |
   |                   |                   |      | See Note 1 and    |
   |                   |                   |      | Note 2.           |
   +-------------------+-------------------+------+-------------------+
   | Selector FD Value | (0072,0074)       | 1C   | The value(s) of   |
   |                   |                   |      | the Attribute     |
   |                   |                   |      | identified by     |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute         |
   |                   |                   |      | (0072,0026).      |
   |                   |                   |      |                   |
   |                   |                   |      | Required if       |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute VR      |
   |                   |                   |      | (0072,0050) is    |
   |                   |                   |      | present and the   |
   |                   |                   |      | value is FD.      |
   |                   |                   |      |                   |
   |                   |                   |      | See Note 2.       |
   +-------------------+-------------------+------+-------------------+
   | Selector FL Value | (0072,0076)       | 1C   | The value(s) of   |
   |                   |                   |      | the Attribute     |
   |                   |                   |      | identified by     |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute         |
   |                   |                   |      | (0072,0026).      |
   |                   |                   |      |                   |
   |                   |                   |      | Required if       |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute VR      |
   |                   |                   |      | (0072,0050) is    |
   |                   |                   |      | present and the   |
   |                   |                   |      | value is FL.      |
   |                   |                   |      |                   |
   |                   |                   |      | See Note 2.       |
   +-------------------+-------------------+------+-------------------+
   | Selector IS Value | (0072,0064)       | 1C   | The value(s) of   |
   |                   |                   |      | the Attribute     |
   |                   |                   |      | identified by     |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute         |
   |                   |                   |      | (0072,0026).      |
   |                   |                   |      |                   |
   |                   |                   |      | Required if       |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute VR      |
   |                   |                   |      | (0072,0050) is    |
   |                   |                   |      | present and the   |
   |                   |                   |      | value is IS.      |
   +-------------------+-------------------+------+-------------------+
   | Selector LO Value | (0072,0066)       | 1C   | The value(s) of   |
   |                   |                   |      | the Attribute     |
   |                   |                   |      | identified by     |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute         |
   |                   |                   |      | (0072,0026).      |
   |                   |                   |      |                   |
   |                   |                   |      | Required if       |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute VR      |
   |                   |                   |      | (0072,0050) is    |
   |                   |                   |      | present and the   |
   |                   |                   |      | value is LO.      |
   +-------------------+-------------------+------+-------------------+
   | Selector LT Value | (0072,0068)       | 1C   | The value of the  |
   |                   |                   |      | Attribute         |
   |                   |                   |      | identified by     |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute         |
   |                   |                   |      | (0072,0026).      |
   |                   |                   |      |                   |
   |                   |                   |      | Required if       |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute VR      |
   |                   |                   |      | (0072,0050) is    |
   |                   |                   |      | present and the   |
   |                   |                   |      | value is LT.      |
   +-------------------+-------------------+------+-------------------+
   | Selector OB Value | (0072,0065)       | 1C   | The value of the  |
   |                   |                   |      | Attribute         |
   |                   |                   |      | identified by     |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute         |
   |                   |                   |      | (0072,0026).      |
   |                   |                   |      |                   |
   |                   |                   |      | Required if       |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute VR      |
   |                   |                   |      | (0072,0050) is    |
   |                   |                   |      | present and the   |
   |                   |                   |      | value is OB.      |
   +-------------------+-------------------+------+-------------------+
   | Selector OD Value | (0072,0073)       | 1C   | The value of the  |
   |                   |                   |      | Attribute         |
   |                   |                   |      | identified by     |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute         |
   |                   |                   |      | (0072,0026).      |
   |                   |                   |      |                   |
   |                   |                   |      | Required if       |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute VR      |
   |                   |                   |      | (0072,0050) is    |
   |                   |                   |      | present and the   |
   |                   |                   |      | value is OD.      |
   +-------------------+-------------------+------+-------------------+
   | Selector OF Value | (0072,0067)       | 1C   | The value of the  |
   |                   |                   |      | Attribute         |
   |                   |                   |      | identified by     |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute         |
   |                   |                   |      | (0072,0026).      |
   |                   |                   |      |                   |
   |                   |                   |      | Required if       |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute VR      |
   |                   |                   |      | (0072,0050) is    |
   |                   |                   |      | present and the   |
   |                   |                   |      | value is OF.      |
   +-------------------+-------------------+------+-------------------+
   | Selector OL Value | (0072,0075)       | 1C   | The value of the  |
   |                   |                   |      | Attribute         |
   |                   |                   |      | identified by     |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute         |
   |                   |                   |      | (0072,0026).      |
   |                   |                   |      |                   |
   |                   |                   |      | Required if       |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute VR      |
   |                   |                   |      | (0072,0050) is    |
   |                   |                   |      | present and the   |
   |                   |                   |      | value is OL.      |
   +-------------------+-------------------+------+-------------------+
   | Selector OW Value | (0072,0069)       | 1C   | The value of the  |
   |                   |                   |      | Attribute         |
   |                   |                   |      | identified by     |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute         |
   |                   |                   |      | (0072,0026).      |
   |                   |                   |      |                   |
   |                   |                   |      | Required if       |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute VR      |
   |                   |                   |      | (0072,0050) is    |
   |                   |                   |      | present and the   |
   |                   |                   |      | value is OW.      |
   +-------------------+-------------------+------+-------------------+
   | Selector PN Value | (0072,006A)       | 1C   | The value(s) of   |
   |                   |                   |      | the Attribute     |
   |                   |                   |      | identified by     |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute         |
   |                   |                   |      | (0072,0026).      |
   |                   |                   |      |                   |
   |                   |                   |      | Required if       |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute VR      |
   |                   |                   |      | (0072,0050) is    |
   |                   |                   |      | present and the   |
   |                   |                   |      | value is PN.      |
   +-------------------+-------------------+------+-------------------+
   | Selector SH Value | (0072,006C)       | 1C   | The value(s) of   |
   |                   |                   |      | the Attribute     |
   |                   |                   |      | identified by     |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute         |
   |                   |                   |      | (0072,0026).      |
   |                   |                   |      |                   |
   |                   |                   |      | Required if       |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute VR      |
   |                   |                   |      | (0072,0050) is    |
   |                   |                   |      | present and the   |
   |                   |                   |      | value is SH.      |
   +-------------------+-------------------+------+-------------------+
   | Selector SL Value | (0072,007C)       | 1C   | The value(s) of   |
   |                   |                   |      | the Attribute     |
   |                   |                   |      | identified by     |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute         |
   |                   |                   |      | (0072,0026).      |
   |                   |                   |      |                   |
   |                   |                   |      | Required if       |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute VR      |
   |                   |                   |      | (0072,0050) is    |
   |                   |                   |      | present and the   |
   |                   |                   |      | value is SL.      |
   +-------------------+-------------------+------+-------------------+
   | Selector SS Value | (0072,007E)       | 1C   | The value(s) of   |
   |                   |                   |      | the Attribute     |
   |                   |                   |      | identified by     |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute         |
   |                   |                   |      | (0072,0026).      |
   |                   |                   |      |                   |
   |                   |                   |      | Required if       |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute VR      |
   |                   |                   |      | (0072,0050) is    |
   |                   |                   |      | present and the   |
   |                   |                   |      | value is SS.      |
   +-------------------+-------------------+------+-------------------+
   | Selector ST Value | (0072,006E)       | 1C   | The value of the  |
   |                   |                   |      | Attribute         |
   |                   |                   |      | identified by     |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute         |
   |                   |                   |      | (0072,0026).      |
   |                   |                   |      |                   |
   |                   |                   |      | Required if       |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute VR      |
   |                   |                   |      | (0072,0050) is    |
   |                   |                   |      | present and the   |
   |                   |                   |      | value is ST.      |
   +-------------------+-------------------+------+-------------------+
   | Selector TM Value | (0072,006B)       | 1C   | The value(s) of   |
   |                   |                   |      | the Attribute     |
   |                   |                   |      | identified by     |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute         |
   |                   |                   |      | (0072,0026).      |
   |                   |                   |      |                   |
   |                   |                   |      | Required if       |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute VR      |
   |                   |                   |      | (0072,0050) is    |
   |                   |                   |      | present and the   |
   |                   |                   |      | value is TM.      |
   |                   |                   |      |                   |
   |                   |                   |      | See Note 1 and    |
   |                   |                   |      | Note 2.           |
   +-------------------+-------------------+------+-------------------+
   | Selector UC Value | (0072,006F)       | 1C   | The value(s) of   |
   |                   |                   |      | the Attribute     |
   |                   |                   |      | identified by     |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute         |
   |                   |                   |      | (0072,0026).      |
   |                   |                   |      |                   |
   |                   |                   |      | Required if       |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute VR      |
   |                   |                   |      | (0072,0050) is    |
   |                   |                   |      | present and the   |
   |                   |                   |      | value is UC.      |
   +-------------------+-------------------+------+-------------------+
   | Selector UI Value | (0072,007F)       | 1C   | The value(s) of   |
   |                   |                   |      | the Attribute     |
   |                   |                   |      | identified by     |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute         |
   |                   |                   |      | (0072,0026).      |
   |                   |                   |      |                   |
   |                   |                   |      | Required if       |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute VR      |
   |                   |                   |      | (0072,0050) is    |
   |                   |                   |      | present and the   |
   |                   |                   |      | value is UI.      |
   +-------------------+-------------------+------+-------------------+
   | Selector UL Value | (0072,0078)       | 1C   | The value(s) of   |
   |                   |                   |      | the Attribute     |
   |                   |                   |      | identified by     |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute         |
   |                   |                   |      | (0072,0026).      |
   |                   |                   |      |                   |
   |                   |                   |      | Required if       |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute VR      |
   |                   |                   |      | (0072,0050) is    |
   |                   |                   |      | present and the   |
   |                   |                   |      | value is UL.      |
   +-------------------+-------------------+------+-------------------+
   | Selector UN Value | (0072,006D)       | 1C   | The value of the  |
   |                   |                   |      | Attribute         |
   |                   |                   |      | identified by     |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute         |
   |                   |                   |      | (0072,0026).      |
   |                   |                   |      |                   |
   |                   |                   |      | Required if       |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute VR      |
   |                   |                   |      | (0072,0050) is    |
   |                   |                   |      | present and the   |
   |                   |                   |      | value is UN.      |
   +-------------------+-------------------+------+-------------------+
   | Selector UR Value | (0072,0071)       | 1C   | The value of the  |
   |                   |                   |      | Attribute         |
   |                   |                   |      | identified by     |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute         |
   |                   |                   |      | (0072,0026).      |
   |                   |                   |      |                   |
   |                   |                   |      | Required if       |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute VR      |
   |                   |                   |      | (0072,0050) is    |
   |                   |                   |      | present and the   |
   |                   |                   |      | value is UR.      |
   +-------------------+-------------------+------+-------------------+
   | Selector US Value | (0072,007A)       | 1C   | The value(s) of   |
   |                   |                   |      | the Attribute     |
   |                   |                   |      | identified by     |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute         |
   |                   |                   |      | (0072,0026).      |
   |                   |                   |      |                   |
   |                   |                   |      | Required if       |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute VR      |
   |                   |                   |      | (0072,0050) is    |
   |                   |                   |      | present and the   |
   |                   |                   |      | value is US.      |
   +-------------------+-------------------+------+-------------------+
   | Selector UT Value | (0072,0070)       | 1C   | The value of the  |
   |                   |                   |      | Attribute         |
   |                   |                   |      | identified by     |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute         |
   |                   |                   |      | (0072,0026).      |
   |                   |                   |      |                   |
   |                   |                   |      | Required if       |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute VR      |
   |                   |                   |      | (0072,0050) is    |
   |                   |                   |      | present and the   |
   |                   |                   |      | value is UT.      |
   +-------------------+-------------------+------+-------------------+
   | Selector Code     | (0072,0080)       | 1C   | The value(s) of   |
   | Sequence Value    |                   |      | the Attribute     |
   |                   |                   |      | identified by     |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute         |
   |                   |                   |      | (0072,0026). One  |
   |                   |                   |      | or more Items     |
   |                   |                   |      | shall be included |
   |                   |                   |      | in this Sequence. |
   |                   |                   |      | See `Selector     |
   |                   |                   |      | Code Sequence     |
   |                   |                   |      | Value <#sect_     |
   |                   |                   |      | C.23.4.2.1.2>`__. |
   |                   |                   |      |                   |
   |                   |                   |      | Required if       |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute VR      |
   |                   |                   |      | (0072,0050) is    |
   |                   |                   |      | present and the   |
   |                   |                   |      | value is SQ and   |
   |                   |                   |      | the Attribute     |
   |                   |                   |      | referenced by the |
   |                   |                   |      | Selector          |
   |                   |                   |      | Attribute         |
   |                   |                   |      | (0072,0026) is a  |
   |                   |                   |      | Code Sequence.    |
   +-------------------+-------------------+------+-------------------+
   | *>Includ          | *No Baseline CID  |      |                   |
   | e*\ `table_title  | is defined.*      |      |                   |
   | <#table_8.8-1>`__ |                   |      |                   |
   +-------------------+-------------------+------+-------------------+

.. note::

   1. For string Value Representations, the meaning of the Value in the
      Standard shall be used, not the literal string. E.g. "1.0E+3"
      equals "1000" and "1000.0".

   2. Some leniency will be required by the application in precision
      when matching this selector value to an Attribute value.

.. _sect_10.27:

Reference Location Macro
------------------------

This Macro allows a reference location in the context of a Patient or
scan to be identified and described. E.g., the Macro may describe an
anatomically defined location along the axis of a CT scan to prescribe
the extent of a scan or reconstruction. The location might be internal
to the Patient (and appear on a localizer image) or might be an external
landmark (on which a laser is aligned).

.. table:: Reference Location Macro Attributes

   +-------------------+-------------------+------+-------------------+
   | Attribute Name    | Tag               | Type | Attribute         |
   |                   |                   |      | Description       |
   +===================+===================+======+===================+
   | Reference         | (0018,9900)       | 1    | Brief             |
   | Location Label    |                   |      | user-readable     |
   |                   |                   |      | label for the     |
   |                   |                   |      | location.         |
   +-------------------+-------------------+------+-------------------+
   | Reference         | (0018,9901)       | 3    | Further           |
   | Location          |                   |      | elaboration of    |
   | Description       |                   |      | the Reference     |
   |                   |                   |      | Location.         |
   |                   |                   |      |                   |
   |                   |                   |      | The value may     |
   |                   |                   |      | include a         |
   |                   |                   |      | description of    |
   |                   |                   |      | the relative      |
   |                   |                   |      | anatomical        |
   |                   |                   |      | location, the     |
   |                   |                   |      | appearance of the |
   |                   |                   |      | feature or        |
   |                   |                   |      | landmark, or how  |
   |                   |                   |      | it can be         |
   |                   |                   |      | identified.       |
   +-------------------+-------------------+------+-------------------+
   | Reference Basis   | (0018,9902)       | 1    | The anatomical    |
   | Code Sequence     |                   |      | feature or point  |
   |                   |                   |      | of reference on   |
   |                   |                   |      | which the         |
   |                   |                   |      | reference         |
   |                   |                   |      | location is       |
   |                   |                   |      | based.            |
   |                   |                   |      |                   |
   |                   |                   |      | Only a single     |
   |                   |                   |      | Item shall be     |
   |                   |                   |      | included in this  |
   |                   |                   |      | Sequence.         |
   +-------------------+-------------------+------+-------------------+
   | *>Includ          | *CID may be       |      |                   |
   | e*\ `table_title  | defined in the    |      |                   |
   | <#table_8.8-1>`__ | Macro             |      |                   |
   |                   | invocation.*      |      |                   |
   +-------------------+-------------------+------+-------------------+
   | Reference         | (0018,9903)       | 1    | Characterizes the |
   | Geometry Code     |                   |      | geometry of the   |
   | Sequence          |                   |      | reference         |
   |                   |                   |      | location (e.g., a |
   |                   |                   |      | plane or point).  |
   |                   |                   |      |                   |
   |                   |                   |      | Only a single     |
   |                   |                   |      | Item shall be     |
   |                   |                   |      | included in this  |
   |                   |                   |      | Sequence.         |
   +-------------------+-------------------+------+-------------------+
   | *>Includ          | *CID may be       |      |                   |
   | e*\ `table_title  | defined in the    |      |                   |
   | <#table_8.8-1>`__ | Macro             |      |                   |
   |                   | invocation.*      |      |                   |
   +-------------------+-------------------+------+-------------------+
   | Offset Distance   | (0018,9904)       | 3    | Positive offset   |
   |                   |                   |      | (in mm) from the  |
   |                   |                   |      | Reference Basis   |
   |                   |                   |      | to the actual     |
   |                   |                   |      | Reference         |
   |                   |                   |      | Location.         |
   |                   |                   |      |                   |
   |                   |                   |      | See `Offset       |
   |                   |                   |      | Distance and      |
   |                   |                   |      | Direction <#      |
   |                   |                   |      | sect_10.27.1>`__. |
   +-------------------+-------------------+------+-------------------+
   | Offset Direction  | (0018,9905)       | 1C   | Direction of the  |
   |                   |                   |      | offset (in terms  |
   |                   |                   |      | of patient        |
   |                   |                   |      | position) from    |
   |                   |                   |      | the Reference     |
   |                   |                   |      | Basis to the      |
   |                   |                   |      | Reference         |
   |                   |                   |      | Location.         |
   |                   |                   |      |                   |
   |                   |                   |      | SUPERIOR          |
   |                   |                   |      | INFERIOR          |
   |                   |                   |      | ANTERIOR          |
   |                   |                   |      | POSTERIOR         |
   |                   |                   |      | LEFT              |
   |                   |                   |      | RIGHT             |
   |                   |                   |      | PROXIMAL          |
   |                   |                   |      | DISTAL            |
   |                   |                   |      | MEDIAL            |
   |                   |                   |      | LATERAL           |
   |                   |                   |      |                   |
   |                   |                   |      | Required if       |
   |                   |                   |      | Offset Distance   |
   |                   |                   |      | (0018,9904) is    |
   |                   |                   |      | present.          |
   +-------------------+-------------------+------+-------------------+

.. _sect_10.27.1:

Offset Distance and Direction
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

An example of the use of offsets might be:

+--------------------------+-------------+--------------------------+
| Reference Location Label | (0018,9900) | "1cm above Liver"        |
+--------------------------+-------------+--------------------------+
| Reference Location       | (0018,9901) | "1cm above the uppermost |
| Description              |             | extent of the liver"     |
+--------------------------+-------------+--------------------------+
| Reference Basis Code     | (0018,9902) | `(10200004, SCT,         |
| Sequence                 |             | "Liver") <http://sno     |
|                          |             | med.info/id/10200004>`__ |
+--------------------------+-------------+--------------------------+
| Reference Geometry Code  | (0018,9903) | (128120, DCM, "Plane     |
| Sequence                 |             | through Superior         |
|                          |             | Extent")                 |
+--------------------------+-------------+--------------------------+
| Offset Distance          | (0018,9904) | 10                       |
+--------------------------+-------------+--------------------------+
| Offset Direction         | (0018,9905) | SUPERIOR                 |
+--------------------------+-------------+--------------------------+

.. _sect_10.28:

Protocol Element Identification Macro
-------------------------------------

This Macro identifies and describes an element in a protocol such as an
acquisition protocol, a reconstruction protocol or a storage protocol.

.. table:: Protocol Element Identification Macro Attributes

   +----------------------+-------------+------+----------------------+
   | Attribute Name       | Tag         | Type | Attribute            |
   |                      |             |      | Description          |
   +======================+=============+======+======================+
   | Protocol Element     | (0018,9921) | 1    | Identifies the       |
   | Number               |             |      | protocol element and |
   |                      |             |      | the order in which   |
   |                      |             |      | the elements are     |
   |                      |             |      | performed in the     |
   |                      |             |      | Protocol.            |
   |                      |             |      |                      |
   |                      |             |      | The value shall      |
   |                      |             |      | start at 1 and       |
   |                      |             |      | increase             |
   |                      |             |      | monotonically by 1.  |
   +----------------------+-------------+------+----------------------+
   | Protocol Element     | (0018,9922) | 2    | Name for this        |
   | Name                 |             |      | protocol element.    |
   +----------------------+-------------+------+----------------------+
   | Protocol Element     | (0018,9924) | 3    | Description of the   |
   | Purpose              |             |      | purpose this element |
   |                      |             |      | serves in the        |
   |                      |             |      | protocol.            |
   |                      |             |      |                      |
   |                      |             |      | .. note::            |
   |                      |             |      |                      |
   |                      |             |      |    1. This is        |
   |                      |             |      |       intended for   |
   |                      |             |      |       use by the     |
   |                      |             |      |       radiologist,   |
   |                      |             |      |       technologist   |
   |                      |             |      |       and/or         |
   |                      |             |      |       physicist      |
   |                      |             |      |       during         |
   |                      |             |      |       management of  |
   |                      |             |      |       the Protocol   |
   |                      |             |      |       to understand  |
   |                      |             |      |       the purpose    |
   |                      |             |      |       the Protocol   |
   |                      |             |      |       Element serves |
   |                      |             |      |       in the         |
   |                      |             |      |       Protocol.      |
   |                      |             |      |                      |
   |                      |             |      |    2. It is not      |
   |                      |             |      |       intended to be |
   |                      |             |      |       copied into    |
   |                      |             |      |       the Series     |
   |                      |             |      |       Description.   |
   |                      |             |      |       Rather there   |
   |                      |             |      |       is an          |
   |                      |             |      |       Attribute in   |
   |                      |             |      |       the Performed  |
   |                      |             |      |       Storage Module |
   |                      |             |      |       called         |
   |                      |             |      |       Requested      |
   |                      |             |      |       Series         |
   |                      |             |      |       Description    |
   |                      |             |      |       (0018,9937)    |
   |                      |             |      |       that is        |
   |                      |             |      |       intended to be |
   |                      |             |      |       copied into    |
   |                      |             |      |       the Series     |
   |                      |             |      |       Description of |
   |                      |             |      |       the stored     |
   |                      |             |      |       Instances.     |
   +----------------------+-------------+------+----------------------+
   | Protocol Element     | (0018,9923) | 3    | Summary description  |
   | Characteristics      |             |      | of characteristics   |
   | Summary              |             |      | of this element.     |
   |                      |             |      |                      |
   |                      |             |      | .. note::            |
   |                      |             |      |                      |
   |                      |             |      |    1. This is        |
   |                      |             |      |       intended for   |
   |                      |             |      |       use by the     |
   |                      |             |      |       radiologist,   |
   |                      |             |      |       technologist   |
   |                      |             |      |       and/or         |
   |                      |             |      |       physicist      |
   |                      |             |      |       during         |
   |                      |             |      |       management of  |
   |                      |             |      |       the Protocol   |
   |                      |             |      |       to understand  |
   |                      |             |      |       the            |
   |                      |             |      |                      |
   |                      |             |      |      characteristics |
   |                      |             |      |       of the         |
   |                      |             |      |       Protocol       |
   |                      |             |      |       Element.       |
   |                      |             |      |                      |
   |                      |             |      |    2. It is not      |
   |                      |             |      |       intended to be |
   |                      |             |      |       copied into    |
   |                      |             |      |       the Series     |
   |                      |             |      |       Description.   |
   |                      |             |      |       Rather there   |
   |                      |             |      |       is an          |
   |                      |             |      |       Attribute in   |
   |                      |             |      |       the Performed  |
   |                      |             |      |       Storage Module |
   |                      |             |      |       called         |
   |                      |             |      |       Requested      |
   |                      |             |      |       Series         |
   |                      |             |      |       Description    |
   |                      |             |      |       (0018,9937)    |
   |                      |             |      |       that is        |
   |                      |             |      |       intended to be |
   |                      |             |      |       copied into    |
   |                      |             |      |       the Series     |
   |                      |             |      |       Description of |
   |                      |             |      |       the stored     |
   |                      |             |      |       Instances.     |
   +----------------------+-------------+------+----------------------+

.. _sect_10.29:

UDI Macro
---------

This Macro records details associated with a Unique Device Identifier
(UDI).

.. table:: UDI Macro Attributes

   +----------------------+-------------+------+----------------------+
   | Attribute Name       | Tag         | Type | Attribute            |
   |                      |             |      | Description          |
   +======================+=============+======+======================+
   | Unique Device        | (0018,1009) | 1    | The entire Human     |
   | Identifier           |             |      | Readable Form of the |
   |                      |             |      | UDI as defined by    |
   |                      |             |      | the Issuing Agency.  |
   |                      |             |      |                      |
   |                      |             |      | See `Unique Device   |
   |                      |             |      | Identifier           |
   |                      |             |      |  <#sect_10.29.1>`__. |
   +----------------------+-------------+------+----------------------+
   | Device Description   | (0050,0020) | 3    | Further description  |
   |                      |             |      | in free form text    |
   |                      |             |      | describing the       |
   |                      |             |      | device.              |
   |                      |             |      |                      |
   |                      |             |      | This can be used to  |
   |                      |             |      | distinguish between  |
   |                      |             |      | Items when multiple  |
   |                      |             |      | UDIs are recorded in |
   |                      |             |      | a Sequence.          |
   +----------------------+-------------+------+----------------------+

.. _sect_10.29.1:

Unique Device Identifier
~~~~~~~~~~~~~~~~~~~~~~~~

The UDI is a combination of the Device Identifier and the Production
Identifier.

The format of the string is defined by a corresponding Issuing Agency,
such as:

-  GS1 - http://www.gs1.org

-  HIBCC - http://www.hibcc.org

-  ICCBBA - http://www.iccbba.org

Details for encoding a valid device identifier are managed by the
Issuing Agency. For full documentation, refer to issuer materials.

The United States FDA requires the Issuing Agency to use only characters
and numbers from the invariant character set of ISO/IEC 646 (ISO 7-bit
coded character set also known as ISO IR 6). DICOM puts no constraints
on the length of the string or the character sets beyond the UT Value
Representation. Implementations should be prepared to handle very large
strings and unusual characters.

.. _sect_10.30:

Assertion Macro
---------------

This Macro is used to record Assertions made by a person or device about
the content of a SOP Instance. The nature of the Assertion is defined by
the Assertion Code.

The scope of the Assertion (e.g., whether it applies to the whole
Instance, to a specific Item in a Sequence, etc.) is described at the
point where the Macro is included. It is also expected that when this
Macro is included, the Baseline CID for the Assertion Code Sequence
(0044,0101) will be constrained.

.. table:: Assertion Macro Attributes

   +-------------------+-------------------+------+-------------------+
   | Attribute Name    | Tag               | Type | Attribute         |
   |                   |                   |      | Description       |
   +===================+===================+======+===================+
   | Assertion Code    | (0044,0101)       | 1    | The Assertion     |
   | Sequence          |                   |      | being made.       |
   |                   |                   |      |                   |
   |                   |                   |      | Only a single     |
   |                   |                   |      | Item shall be     |
   |                   |                   |      | included in this  |
   |                   |                   |      | Sequence.         |
   +-------------------+-------------------+------+-------------------+
   | *>Includ          | *No Baseline CID  |      |                   |
   | e*\ `table_title  | defined*          |      |                   |
   | <#table_8.8-1>`__ |                   |      |                   |
   +-------------------+-------------------+------+-------------------+
   | Assertion UID     | (0044,0102)       | 1    | Unique            |
   |                   |                   |      | identification of |
   |                   |                   |      | this Assertion.   |
   +-------------------+-------------------+------+-------------------+
   | Asserter          | (0044,0103)       | 1    | The person or     |
   | Identification    |                   |      | device making the |
   | Sequence          |                   |      | Assertion.        |
   |                   |                   |      |                   |
   |                   |                   |      | Only a single     |
   |                   |                   |      | Item shall be     |
   |                   |                   |      | included in this  |
   |                   |                   |      | Sequence.         |
   |                   |                   |      |                   |
   |                   |                   |      | .. note::         |
   |                   |                   |      |                   |
   |                   |                   |      |    Multiple       |
   |                   |                   |      |    asserters      |
   |                   |                   |      |    wishing to     |
   |                   |                   |      |    make the same  |
   |                   |                   |      |    Assertion may  |
   |                   |                   |      |    be recorded as |
   |                   |                   |      |    multiple       |
   |                   |                   |      |    Assertions,    |
   |                   |                   |      |    each with a    |
   |                   |                   |      |    single         |
   |                   |                   |      |    asserter.      |
   +-------------------+-------------------+------+-------------------+
   | *>Include*        | *Organizational   |      |                   |
   | \ `table_title <# | Role B.*          |      |                   |
   | table_C.17-3b>`__ |                   |      |                   |
   +-------------------+-------------------+------+-------------------+
   | Assertion         | (0044,0104)       | 1    | Date and time at  |
   | DateTime          |                   |      | which the         |
   |                   |                   |      | Assertion was     |
   |                   |                   |      | made.             |
   +-------------------+-------------------+------+-------------------+
   | Assertion         | (0044,0105)       | 3    | Date and time at  |
   | Expiration        |                   |      | which the         |
   | DateTime          |                   |      | Assertion         |
   |                   |                   |      | expires.          |
   |                   |                   |      |                   |
   |                   |                   |      | If this Attribute |
   |                   |                   |      | is absent or      |
   |                   |                   |      | empty, it means   |
   |                   |                   |      | the Assertion     |
   |                   |                   |      | does not have a   |
   |                   |                   |      | pre-determined    |
   |                   |                   |      | date and time at  |
   |                   |                   |      | which it expires. |
   +-------------------+-------------------+------+-------------------+
   | Assertion         | (0044,0106)       | 3    | Comments on the   |
   | Comments          |                   |      | nature, extent or |
   |                   |                   |      | basis of the      |
   |                   |                   |      | Assertion.        |
   +-------------------+-------------------+------+-------------------+
   | Pertinent         | (0038,0100)       | 3    | Reference to      |
   | Documents         |                   |      | document(s) that  |
   | Sequence          |                   |      | describe the      |
   |                   |                   |      | Assertion         |
   |                   |                   |      | semantics, or     |
   |                   |                   |      | provide the basis |
   |                   |                   |      | for making the    |
   |                   |                   |      | Assertion.        |
   |                   |                   |      |                   |
   |                   |                   |      | Items shall not   |
   |                   |                   |      | be empty.         |
   |                   |                   |      |                   |
   |                   |                   |      | One or more Items |
   |                   |                   |      | are permitted in  |
   |                   |                   |      | this Sequence.    |
   +-------------------+-------------------+------+-------------------+
   | >Referenced SOP   | (0008,1150)       | 3    | Unique identifier |
   | Class UID         |                   |      | for the class of  |
   |                   |                   |      | the referenced    |
   |                   |                   |      | document.         |
   +-------------------+-------------------+------+-------------------+
   | >Referenced SOP   | (0008,1155)       | 3    | Unique identifier |
   | Instance UID      |                   |      | for the           |
   |                   |                   |      | referenced        |
   |                   |                   |      | document as used  |
   |                   |                   |      | in DICOM Instance |
   |                   |                   |      | references (see   |
   |                   |                   |      | `HL7 Structured   |
   |                   |                   |      | Document          |
   |                   |                   |      | Reference         |
   |                   |                   |      | Sequence <#sec    |
   |                   |                   |      | t_C.12.1.1.6>`__) |
   +-------------------+-------------------+------+-------------------+
   | >HL7 Instance     | (0040,E001)       | 3    | Instance          |
   | Identifier        |                   |      | Identifier of the |
   |                   |                   |      | referenced        |
   |                   |                   |      | document, encoded |
   |                   |                   |      | as a UID (OID or  |
   |                   |                   |      | UUID),            |
   |                   |                   |      | concatenated with |
   |                   |                   |      | a caret ("^") and |
   |                   |                   |      | Extension value   |
   |                   |                   |      | (if Extension is  |
   |                   |                   |      | present in        |
   |                   |                   |      | Instance          |
   |                   |                   |      | Identifier).      |
   +-------------------+-------------------+------+-------------------+
   | >Retrieve URI     | (0040,E010)       | 3    | Retrieval access  |
   |                   |                   |      | path to the       |
   |                   |                   |      | referenced        |
   |                   |                   |      | document.         |
   |                   |                   |      |                   |
   |                   |                   |      | Includes fully    |
   |                   |                   |      | specified scheme, |
   |                   |                   |      | authority, path,  |
   |                   |                   |      | and query in      |
   |                   |                   |      | accordance with   |
   |                   |                   |      | `biblio           |
   |                   |                   |      | entry_title <#bib |
   |                   |                   |      | lio_RFC_3986>`__. |
   +-------------------+-------------------+------+-------------------+
   | Related Assertion | (0044,0107)       | 3    | Other Assertions  |
   | Sequence          |                   |      | which may be of   |
   |                   |                   |      | interest to       |
   |                   |                   |      | systems examining |
   |                   |                   |      | this Assertion.   |
   |                   |                   |      |                   |
   |                   |                   |      | One or more Items |
   |                   |                   |      | are permitted in  |
   |                   |                   |      | this Sequence.    |
   |                   |                   |      |                   |
   |                   |                   |      | .. note::         |
   |                   |                   |      |                   |
   |                   |                   |      |    For example,   |
   |                   |                   |      |    an Assertion   |
   |                   |                   |      |    that overrides |
   |                   |                   |      |    a previous     |
   |                   |                   |      |    Assertion or   |
   |                   |                   |      |    disapproves a  |
   |                   |                   |      |    previously     |
   |                   |                   |      |    approved       |
   |                   |                   |      |    protocol,      |
   |                   |                   |      |    could          |
   |                   |                   |      |    reference the  |
   |                   |                   |      |    prior approval |
   |                   |                   |      |    Instance       |
   |                   |                   |      |    making it      |
   |                   |                   |      |    easier to      |
   |                   |                   |      |    find/c         |
   |                   |                   |      | orrelate/confirm. |
   +-------------------+-------------------+------+-------------------+
   | >Referenced       | (0044,0108)       | 1    | Uniquely          |
   | Assertion UID     |                   |      | identifies a      |
   |                   |                   |      | related           |
   |                   |                   |      | Assertion.        |
   +-------------------+-------------------+------+-------------------+

.. _sect_10.31:

Entity Labeling Macro
---------------------

The Entity Labeling Macro provides identification of an entity to a
user.

This information is intended for display to human readers. Shall not be
used for structured processing.

.. table:: Entity Labeling Macro Attributes

   +--------------------+-------------+------+----------------------+
   | Attribute Name     | Tag         | Type | Attribute            |
   |                    |             |      | Description          |
   +====================+=============+======+======================+
   | Entity Label       | (3010,0035) | 1    | User-defined label   |
   |                    |             |      | for this entity.     |
   |                    |             |      |                      |
   |                    |             |      | See `Entity          |
   |                    |             |      | Label <              |
   |                    |             |      | #sect_10.31.1.1>`__. |
   +--------------------+-------------+------+----------------------+
   | Entity Name        | (3010,0036) | 3    | User-defined name    |
   |                    |             |      | for this entity.     |
   |                    |             |      |                      |
   |                    |             |      | See `Entity Name and |
   |                    |             |      | Entity               |
   |                    |             |      | Description <        |
   |                    |             |      | #sect_10.31.1.2>`__. |
   +--------------------+-------------+------+----------------------+
   | Entity Description | (3010,0037) | 3    | User-defined         |
   |                    |             |      | description for this |
   |                    |             |      | entity.              |
   |                    |             |      |                      |
   |                    |             |      | See `Entity Name and |
   |                    |             |      | Entity               |
   |                    |             |      | Description <        |
   |                    |             |      | #sect_10.31.1.2>`__. |
   +--------------------+-------------+------+----------------------+

.. _sect_10.31.1:

Entity Labeling Macro Attribute Descriptions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. _sect_10.31.1.1:

Entity Label
^^^^^^^^^^^^

The Entity Label (3010,0035) Attribute represents a user-defined short
free text providing the primary identification of this entity to other
users.

.. _sect_10.31.1.2:

Entity Name and Entity Description
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The optional Attribute Entity Name (3010,0036) allows a longer string
containing additional descriptive identifying text. The optional
Attribute Entity Description (3010,0037) provides additional information
when needed.

.. _sect_10.32:

Entity Long Labeling Macro
--------------------------

The Entity Long Labeling Macro provides identification of an entity to a
user.

This information is intended for display to human readers. Shall not be
used for structured processing.

.. table:: Entity Long Labeling Macro Attributes

   +--------------------+-------------+------+----------------------+
   | Attribute Name     | Tag         | Type | Attribute            |
   |                    |             |      | Description          |
   +====================+=============+======+======================+
   | Entity Long Label  | (3010,0038) | 1    | User-defined label   |
   |                    |             |      | for this entity.     |
   |                    |             |      |                      |
   |                    |             |      | See `Entity Long     |
   |                    |             |      | Label <              |
   |                    |             |      | #sect_10.32.2.1>`__. |
   +--------------------+-------------+------+----------------------+
   | Entity Description | (3010,0037) | 3    | User-defined         |
   |                    |             |      | description for this |
   |                    |             |      | entity.              |
   |                    |             |      |                      |
   |                    |             |      | See `Entity Name and |
   |                    |             |      | Entity               |
   |                    |             |      | Description <        |
   |                    |             |      | #sect_10.31.1.2>`__. |
   +--------------------+-------------+------+----------------------+

.. _sect_10.32.2:

Entity Long Labeling Macro Attribute Descriptions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. _sect_10.32.2.1:

Entity Long Label
^^^^^^^^^^^^^^^^^

The Entity Long Label (3010,0038) Attribute represents a user-defined
free text providing the primary identification of this entity to other
users.

.. _sect_10.33:

Conceptual Volume Macro
-----------------------

A Conceptual Volume is an abstract entity used to identify an anatomic
region (such as a planning target volume or a combination of multiple
anatomic volumes) or non-anatomic volumes such as a bolus or a marker. A
Conceptual Volume can be established without necessarily defining its
spatial extent (for example a Conceptual Volume for a tumor can be
established prior to segmenting it). The spatial extent of a Conceptual
Volume may change over time (for example as treatment proceeds the tumor
volume corresponding to the Conceptual Volume will change).

The spatial extent of a Conceptual Volume may be defined by any
general-purpose entity that represents geometric information (such as
Segmentation, Surface Segmentation, RT Structure Set SOP Instance and
alike) or a combination thereof, although the Conceptual Volume does
exist independently of a specific definition of its spatial extent.

A Conceptual Volume may also be defined as a combination of other
Conceptual Volumes.

Examples for Conceptual Volumes:

1. A Conceptual Volume (with a Conceptual Volume UID (3010,0006) can be
   used to represent the treatment target in an RT Physician Intent SOP
   Instance based upon a diagnostic image set, although the actual
   delineation of a specific target volume has not yet taken place.
   Later, the target volume is contoured. The RT Segment Annotation SOP
   Instance references the volume contours and associates it with the
   Conceptual Volume via the Conceptual Volume UID (3010,0006).

2. In an adaptive workflow, the anatomic volume may change over time.
   The Conceptual Volume on the other hand does not change. Multiple RT
   Segment Annotation SOP Instances, each referencing different
   Segmentation Instances, can be associated with the same Conceptual
   Volume via the Conceptual Volume UID (3010,0006) , making it possible
   to track the volume over time.

3. A Conceptual Volume may represent targets and/or anatomic regions for
   which manually calculated doses are tracked (for example, in
   emergency treatments). In this case, Conceptual Volumes may be
   instantiated first in an RT Physician Intent SOP Instance and
   subsequently used in RT Radiation SOP Instances, or may be first
   instantiated in the Radiation SOP Instances. After treatment, these
   Conceptual Volumes will be used in RT Radiation Records to track the
   delivered dose. Such Conceptual Volumes may never reference a
   segmentation, but serve as a key for referencing the Conceptual
   Volume across these different SOP Instances.

.. table:: Conceptual Volume Macro Attributes

   +-------------------+-------------------+------+-------------------+
   | Attribute Name    | Tag               | Type | Attribute         |
   |                   |                   |      | Description       |
   +===================+===================+======+===================+
   | Conceptual Volume | (3010,0006)       | 1    | A UID identifying |
   | UID               |                   |      | the Conceptual    |
   |                   |                   |      | Volume.           |
   +-------------------+-------------------+------+-------------------+
   | Originating SOP   | (3010,0007)       | 1C   | Reference to the  |
   | Instance          |                   |      | SOP Instance that |
   | Reference         |                   |      | contains the      |
   | Sequence          |                   |      | original          |
   |                   |                   |      | definition of     |
   |                   |                   |      | this Conceptual   |
   |                   |                   |      | Volume identified |
   |                   |                   |      | by Conceptual     |
   |                   |                   |      | Volume UID        |
   |                   |                   |      | (3010,0006).      |
   |                   |                   |      |                   |
   |                   |                   |      | Required when     |
   |                   |                   |      | Conceptual Volume |
   |                   |                   |      | UID (3010,0006)   |
   |                   |                   |      | was not issued in |
   |                   |                   |      | the current SOP   |
   |                   |                   |      | Instance, but     |
   |                   |                   |      | read from another |
   |                   |                   |      | SOP Instance.     |
   |                   |                   |      |                   |
   |                   |                   |      | Only a single     |
   |                   |                   |      | Item shall be     |
   |                   |                   |      | included in this  |
   |                   |                   |      | Sequence.         |
   +-------------------+-------------------+------+-------------------+
   | *>Includ          |                   |      |                   |
   | e*\ `table_title  |                   |      |                   |
   | <#table_10-11>`__ |                   |      |                   |
   +-------------------+-------------------+------+-------------------+
   | Equivalent        | (3010,000A)       | 3    | References one or |
   | Conceptual        |                   |      | more existing     |
   | Volumes Sequence  |                   |      | Conceptual        |
   |                   |                   |      | Volumes that      |
   |                   |                   |      | represent the     |
   |                   |                   |      | same concept as   |
   |                   |                   |      | the current       |
   |                   |                   |      | Conceptual        |
   |                   |                   |      | Volume.           |
   |                   |                   |      |                   |
   |                   |                   |      | This Sequence     |
   |                   |                   |      | might be used     |
   |                   |                   |      | when Conceptual   |
   |                   |                   |      | Volume references |
   |                   |                   |      | of existing SOP   |
   |                   |                   |      | Instances are     |
   |                   |                   |      | retrospectively   |
   |                   |                   |      | identified as     |
   |                   |                   |      | representing the  |
   |                   |                   |      | same entity.      |
   |                   |                   |      |                   |
   |                   |                   |      | One or more Items |
   |                   |                   |      | are permitted in  |
   |                   |                   |      | this Sequence.    |
   |                   |                   |      |                   |
   |                   |                   |      | See `Equivalent   |
   |                   |                   |      | Conceptual        |
   |                   |                   |      | Volumes <#se      |
   |                   |                   |      | ct_10.33.1.1>`__. |
   +-------------------+-------------------+------+-------------------+
   | >Referenced       | (3010,000B)       | 1    | A UID identifying |
   | Conceptual Volume |                   |      | the Conceptual    |
   | UID               |                   |      | Volume.           |
   +-------------------+-------------------+------+-------------------+
   | >Equivalent       | (3010,0009)       | 1    | Reference to a    |
   | Conceptual Volume |                   |      | SOP Instance that |
   | Instance          |                   |      | contains the      |
   | Reference         |                   |      | Referenced        |
   | Sequence          |                   |      | Conceptual Volume |
   |                   |                   |      | UID (3010,000B)   |
   |                   |                   |      | of the Equivalent |
   |                   |                   |      | Conceptual        |
   |                   |                   |      | Volume.           |
   |                   |                   |      |                   |
   |                   |                   |      | Only a single     |
   |                   |                   |      | Item shall be     |
   |                   |                   |      | included in this  |
   |                   |                   |      | Sequence.         |
   +-------------------+-------------------+------+-------------------+
   | *>>Includ         |                   |      |                   |
   | e*\ `table_title  |                   |      |                   |
   | <#table_10-11>`__ |                   |      |                   |
   +-------------------+-------------------+------+-------------------+
   | Derivation        | (3010,0014)       | 3    | Description of a  |
   | Conceptual Volume |                   |      | Conceptual Volume |
   | Sequence          |                   |      | that was used to  |
   |                   |                   |      | derive this       |
   |                   |                   |      | Conceptual        |
   |                   |                   |      | Volume.           |
   |                   |                   |      |                   |
   |                   |                   |      | Only a single     |
   |                   |                   |      | Item is permitted |
   |                   |                   |      | in this Sequence. |
   +-------------------+-------------------+------+-------------------+
   | >Derivation       | (0008,2111)       | 3    | A user-readable   |
   | Description       |                   |      | text description  |
   |                   |                   |      | of how this       |
   |                   |                   |      | Conceptual Volume |
   |                   |                   |      | was derived.      |
   +-------------------+-------------------+------+-------------------+
   | >Source           | (3010,0018)       | 1    | The set of        |
   | Conceptual Volume |                   |      | Conceptual        |
   | Sequence          |                   |      | Volumes that were |
   |                   |                   |      | used to derive    |
   |                   |                   |      | this Conceptual   |
   |                   |                   |      | Volume.           |
   |                   |                   |      |                   |
   |                   |                   |      | One or more Items |
   |                   |                   |      | shall be included |
   |                   |                   |      | in this Sequence. |
   +-------------------+-------------------+------+-------------------+
   | >>Source          | (3010,0015)       | 1    | UID identifying   |
   | Conceptual Volume |                   |      | the Conceptual    |
   | UID               |                   |      | Volume that was   |
   |                   |                   |      | used to derive    |
   |                   |                   |      | this Conceptual   |
   |                   |                   |      | Volume.           |
   +-------------------+-------------------+------+-------------------+
   | >>Conceptual      | (3010,000D)       | 1    | Index of the      |
   | Volume            |                   |      | constituent in    |
   | Constituent Index |                   |      | the Source        |
   |                   |                   |      | Conceptual Volume |
   |                   |                   |      | Sequence.         |
   |                   |                   |      |                   |
   |                   |                   |      | The value shall   |
   |                   |                   |      | start at 1 and    |
   |                   |                   |      | increase          |
   |                   |                   |      | monotonically by  |
   |                   |                   |      | 1.                |
   +-------------------+-------------------+------+-------------------+
   | >>Conceptual      | (3010,0012)       | 2    | Contains the      |
   | Volume            |                   |      | reference to the  |
   | Constituent       |                   |      | constituents of   |
   | Segmentation      |                   |      | the RT Segment    |
   | Reference         |                   |      | Annotation        |
   | Sequence          |                   |      | Instance from     |
   |                   |                   |      | which Conceptual  |
   |                   |                   |      | Volume is         |
   |                   |                   |      | derived.          |
   |                   |                   |      |                   |
   |                   |                   |      | Zero or one Item  |
   |                   |                   |      | shall be included |
   |                   |                   |      | in this Sequence. |
   +-------------------+-------------------+------+-------------------+
   | >>>Referenced     | (3010,004A)       | 1    | Reference to the  |
   | Direct Segment    |                   |      | SOP Instance that |
   | Instance Sequence |                   |      | contains the      |
   |                   |                   |      | Direct Segment    |
   |                   |                   |      | Reference         |
   |                   |                   |      | Sequence          |
   |                   |                   |      | (3010,0023).      |
   |                   |                   |      |                   |
   |                   |                   |      | Only a single     |
   |                   |                   |      | Item shall be     |
   |                   |                   |      | included in this  |
   |                   |                   |      | Sequence.         |
   |                   |                   |      |                   |
   |                   |                   |      | See `Referenced   |
   |                   |                   |      | Direct Segment    |
   |                   |                   |      | Instance          |
   |                   |                   |      | Sequence <#se     |
   |                   |                   |      | ct_10.34.1.3>`__. |
   +-------------------+-------------------+------+-------------------+
   | *>>>>Includ       |                   |      |                   |
   | e*\ `table_title  |                   |      |                   |
   | <#table_10-11>`__ |                   |      |                   |
   +-------------------+-------------------+------+-------------------+
   | >>>Referenced     | (3010,0020)       | 1    | The Segment       |
   | Segment Reference |                   |      | Reference Index   |
   | Index             |                   |      | (3010,0022) in    |
   |                   |                   |      | the Segment       |
   |                   |                   |      | Reference         |
   |                   |                   |      | Sequence          |
   |                   |                   |      | (3010,0021)       |
   |                   |                   |      | corresponding to  |
   |                   |                   |      | the segment       |
   |                   |                   |      | representing this |
   |                   |                   |      | Conceptual        |
   |                   |                   |      | Volume.           |
   |                   |                   |      |                   |
   |                   |                   |      | Shall reference   |
   |                   |                   |      | only segment      |
   |                   |                   |      | Items that        |
   |                   |                   |      | contain the       |
   |                   |                   |      | Direct Segment    |
   |                   |                   |      | Reference         |
   |                   |                   |      | Sequence          |
   |                   |                   |      | (3010,0023).      |
   +-------------------+-------------------+------+-------------------+
   | >Conceptual       | (3010,0016)       | 3    | Algorithm used to |
   | Volume Derivation |                   |      | derive this       |
   | Algorithm         |                   |      | Conceptual        |
   | Sequence          |                   |      | Volume.           |
   |                   |                   |      |                   |
   |                   |                   |      | One or more Items |
   |                   |                   |      | are permitted in  |
   |                   |                   |      | this Sequence.    |
   +-------------------+-------------------+------+-------------------+
   | *>>Includ         | *No Baseline CID  |      |                   |
   | e*\ `table_title  | defined*          |      |                   |
   | <#table_10-19>`__ |                   |      |                   |
   +-------------------+-------------------+------+-------------------+

.. _sect_10.33.1:

Conceptual Volume Macro Attribute Descriptions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. _sect_10.33.1.1:

Equivalent Conceptual Volumes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Conceptual Volumes can be declared to be equivalent to other Conceptual
Volumes. In such cases, the Equivalent Conceptual Volumes Sequence
(3010,000A) is used in derived SOP Instances which are aware of other
SOP Instances defining a semantically equivalent volume, but using
different Conceptual Volume UIDs (3010,0006).

.. _sect_10.33.1.2:

Derivation Conceptual Volume Sequence
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Derivation Conceptual Volume Sequence (3010,0014) may be used to
describe how a Conceptual Volume is derived from one or more other
Conceptual Volumes in cases where it may not be possible to describe the
method of the derivation completely. Since the Conceptual Volume cannot
be mathematically constructed from a derivation description, it will be
defined explicitly by a segmentation.

The specification of derivation is different from combining Conceptual
Volumes as defined in `Conceptual Volume Segmentation Reference and
Combination Macro <#sect_10.34>`__.

.. _sect_10.34:

Conceptual Volume Segmentation Reference and Combination Macro
--------------------------------------------------------------

This Macro allows the combination of Conceptual Volumes as constituents
of a combined volume. A representative example is to have the Left Lung
and the Right Lung segmented, and then to declare the Lungs as a
combined Conceptual Volume, for which prescription constraints can be
defined.

The Macro also allows reference to RT Segment Annotation SOP Instances,
which contain a segmented representation of the Conceptual Volume. At
the invocation of this Macro it is declared, whether this segmented
representation is required or not.

`figure_title <#figure_10.34-1>`__ describes an RT Physician Intent
Instance where Conceptual Volumes "Lung, left" and "Lung, right" are
referenced, but not defined. In this example, the RT Segmentation
Annotation Instances then define the volumetric information of the
Conceptual Volumes by referencing a specific segment of a Segmentation
Instance and a specific ROI in an RT Structure Set Instance.

`figure_title <#figure_10.34-1>`__ describes an RT Physician Intent
Instance defining Conceptual Volumes "Lung, left" and "Lung, right" and
Conceptual Volume "Lung" as a combination of the first two without a
direct reference to a volume definition.

.. table:: Conceptual Volume Segmentation Reference And Combination
Macro Attributes

   +----------------------+-------------+------+----------------------+
   | Attribute Name       | Tag         | Type | Attribute            |
   |                      |             |      | Description          |
   +======================+=============+======+======================+
   | *In                  |             |      |                      |
   | clude*\ `table_title |             |      |                      |
   |  <#table_10.33-1>`__ |             |      |                      |
   +----------------------+-------------+------+----------------------+
   | Conceptual Volume    | (3010,000E) | 1    | Indication that this |
   | Combination Flag     |             |      | Conceptual Volume is |
   |                      |             |      | a combination of     |
   |                      |             |      | other Conceptual     |
   |                      |             |      | Volumes.             |
   |                      |             |      |                      |
   |                      |             |      | YES                  |
   |                      |             |      | NO                   |
   +----------------------+-------------+------+----------------------+
   | Conceptual Volume    | (3010,0008) | 1C   | References to        |
   | Constituent Sequence |             |      | Conceptual Volumes   |
   |                      |             |      | which are            |
   |                      |             |      | constituents of this |
   |                      |             |      | Conceptual Volume.   |
   |                      |             |      |                      |
   |                      |             |      | See `Conceptual      |
   |                      |             |      | Volume Combination   |
   |                      |             |      | Expression <         |
   |                      |             |      | #sect_10.34.1.1>`__. |
   |                      |             |      |                      |
   |                      |             |      | Required if          |
   |                      |             |      | Conceptual Volume    |
   |                      |             |      | Combination Flag     |
   |                      |             |      | (3010,000E) equals   |
   |                      |             |      | YES.                 |
   |                      |             |      |                      |
   |                      |             |      | One or more Items    |
   |                      |             |      | shall be included in |
   |                      |             |      | this Sequence.       |
   |                      |             |      |                      |
   |                      |             |      | The combined         |
   |                      |             |      | Conceptual Volume    |
   |                      |             |      | UID shall not be     |
   |                      |             |      | included in the      |
   |                      |             |      | Sequence.            |
   +----------------------+-------------+------+----------------------+
   | >Conceptual Volume   | (3010,000D) | 1    | An index referenced  |
   | Constituent Index    |             |      | in the Conceptual    |
   |                      |             |      | Volume Combination   |
   |                      |             |      | Expression           |
   |                      |             |      | (3010,000C)          |
   |                      |             |      | identifying the      |
   |                      |             |      | Conceptual Volume    |
   |                      |             |      | Constituent.         |
   |                      |             |      |                      |
   |                      |             |      | The value shall      |
   |                      |             |      | start at 1 and       |
   |                      |             |      | increase             |
   |                      |             |      | monotonically by 1.  |
   +----------------------+-------------+------+----------------------+
   | >Constituent         | (3010,0013) | 1    | UID identifying the  |
   | Conceptual Volume    |             |      | Conceptual Volume    |
   | UID                  |             |      | that is a            |
   |                      |             |      | constituent of the   |
   |                      |             |      | combined Conceptual  |
   |                      |             |      | Volume.              |
   +----------------------+-------------+------+----------------------+
   | >Originating SOP     | (3010,0007) | 1    | Reference to the SOP |
   | Instance Reference   |             |      | Instance that        |
   | Sequence             |             |      | contains the         |
   |                      |             |      | original definition  |
   |                      |             |      | of the Conceptual    |
   |                      |             |      | Volume constituent   |
   |                      |             |      | identified by        |
   |                      |             |      | Constituent          |
   |                      |             |      | Conceptual Volume    |
   |                      |             |      | UID (3010,0013) in   |
   |                      |             |      | this Sequence.       |
   |                      |             |      |                      |
   |                      |             |      | If this Conceptual   |
   |                      |             |      | Volume orginated in  |
   |                      |             |      | the current SOP      |
   |                      |             |      | Instance, then the   |
   |                      |             |      | referenced SOP       |
   |                      |             |      | Instance UID is the  |
   |                      |             |      | current SOP Instance |
   |                      |             |      | UID.                 |
   |                      |             |      |                      |
   |                      |             |      | Only a single Item   |
   |                      |             |      | shall be included in |
   |                      |             |      | this Sequence.       |
   +----------------------+-------------+------+----------------------+
   | *>>                  |             |      |                      |
   | Include*\ `table_tit |             |      |                      |
   | le <#table_10-11>`__ |             |      |                      |
   +----------------------+-------------+------+----------------------+
   | >Conceptual Volume   | (3010,0012) | 1C   | Contains a segmented |
   | Constituent          |             |      | representation of    |
   | Segmentation         |             |      | the Conceptual       |
   | Reference Sequence   |             |      | Volume constituent.  |
   |                      |             |      |                      |
   |                      |             |      | Required if the      |
   |                      |             |      | Conceptual Volume    |
   |                      |             |      | Segmentation Defined |
   |                      |             |      | Flag (3010,0010)     |
   |                      |             |      | equals YES and the   |
   |                      |             |      | Conceptual Volume is |
   |                      |             |      | not a Combination of |
   |                      |             |      | other Conceptual     |
   |                      |             |      | Volumes.             |
   |                      |             |      |                      |
   |                      |             |      | Only a single Item   |
   |                      |             |      | shall be included in |
   |                      |             |      | this Sequence.       |
   |                      |             |      |                      |
   |                      |             |      | See `Conceptual      |
   |                      |             |      | Volume Segmentation  |
   |                      |             |      | Reference            |
   |                      |             |      | Sequence <           |
   |                      |             |      | #sect_10.34.1.2>`__. |
   +----------------------+-------------+------+----------------------+
   | >>Referenced Direct  | (3010,004A) | 1    | Reference to the SOP |
   | Segment Instance     |             |      | Instance that        |
   | Sequence             |             |      | contains the Direct  |
   |                      |             |      | Segment Reference    |
   |                      |             |      | Sequence             |
   |                      |             |      | (3010,0023).         |
   |                      |             |      |                      |
   |                      |             |      | Only a single Item   |
   |                      |             |      | shall be included in |
   |                      |             |      | this Sequence.       |
   |                      |             |      |                      |
   |                      |             |      | See `Referenced      |
   |                      |             |      | Direct Segment       |
   |                      |             |      | Instance             |
   |                      |             |      | Sequence <           |
   |                      |             |      | #sect_10.34.1.3>`__. |
   +----------------------+-------------+------+----------------------+
   | *>>>                 |             |      |                      |
   | Include*\ `table_tit |             |      |                      |
   | le <#table_10-11>`__ |             |      |                      |
   +----------------------+-------------+------+----------------------+
   | >>Referenced Segment | (3010,0020) | 1    | The Segment          |
   | Reference Index      |             |      | Reference Index      |
   |                      |             |      | (3010,0022) in the   |
   |                      |             |      | Segment Reference    |
   |                      |             |      | Sequence (3010,0021) |
   |                      |             |      | corresponding to the |
   |                      |             |      | segment representing |
   |                      |             |      | this Conceptual      |
   |                      |             |      | Volume.              |
   |                      |             |      |                      |
   |                      |             |      | Shall reference only |
   |                      |             |      | segment Items that   |
   |                      |             |      | contain the Direct   |
   |                      |             |      | Segment Reference    |
   |                      |             |      | Sequence             |
   |                      |             |      | (3010,0023).         |
   +----------------------+-------------+------+----------------------+
   | Conceptual Volume    | (3010,000C) | 1C   | Symbolic expression  |
   | Combination          |             |      | specifying the       |
   | Expression           |             |      | combination of       |
   |                      |             |      | Conceptual Volumes   |
   |                      |             |      | as a text string     |
   |                      |             |      | consisting of        |
   |                      |             |      | Conceptual Volume    |
   |                      |             |      | Constituent Index    |
   |                      |             |      | (3010,000D) values,  |
   |                      |             |      | combination          |
   |                      |             |      | operators and        |
   |                      |             |      | parentheses.         |
   |                      |             |      |                      |
   |                      |             |      | Required if          |
   |                      |             |      | Conceptual Volume    |
   |                      |             |      | Combination Flag     |
   |                      |             |      | (3010,000E) equals   |
   |                      |             |      | YES.                 |
   |                      |             |      |                      |
   |                      |             |      | See `Conceptual      |
   |                      |             |      | Volume Combination   |
   |                      |             |      | Expression <         |
   |                      |             |      | #sect_10.34.1.1>`__. |
   +----------------------+-------------+------+----------------------+
   | Conceptual Volume    | (3010,000F) | 2C   | Human-readable       |
   | Combination          |             |      | description of the   |
   | Description          |             |      | combination of       |
   |                      |             |      | Conceptual Volumes.  |
   |                      |             |      | This information is  |
   |                      |             |      | intended for         |
   |                      |             |      | displayand shall not |
   |                      |             |      | be used for          |
   |                      |             |      | structured           |
   |                      |             |      | processing.          |
   |                      |             |      |                      |
   |                      |             |      | Required if          |
   |                      |             |      | Conceptual Volume    |
   |                      |             |      | Combination Flag     |
   |                      |             |      | (3010,000E) equals   |
   |                      |             |      | YES.                 |
   +----------------------+-------------+------+----------------------+
   | Conceptual Volume    | (3010,0010) | 1    | Indication that      |
   | Segmentation Defined |             |      | there are defined    |
   | Flag                 |             |      | segmentations for    |
   |                      |             |      | this Conceptual      |
   |                      |             |      | Volume.              |
   |                      |             |      |                      |
   |                      |             |      | YES                  |
   |                      |             |      | NO                   |
   +----------------------+-------------+------+----------------------+
   | Conceptual Volume    | (3010,0011) | 1C   | Contains a segmented |
   | Segmentation         |             |      | representation of    |
   | Reference Sequence   |             |      | the Conceptual       |
   |                      |             |      | Volume.              |
   |                      |             |      |                      |
   |                      |             |      | Required when        |
   |                      |             |      | Conceptual Volume    |
   |                      |             |      | Segmentation Defined |
   |                      |             |      | Flag (3010,0010)     |
   |                      |             |      | equals YES and       |
   |                      |             |      | Conceptual Volume    |
   |                      |             |      | Combination Flag     |
   |                      |             |      | Indicator            |
   |                      |             |      | (3010,000E) equals   |
   |                      |             |      | NO.                  |
   |                      |             |      |                      |
   |                      |             |      | Only a single Item   |
   |                      |             |      | shall be included in |
   |                      |             |      | this Sequence.       |
   |                      |             |      |                      |
   |                      |             |      | See `Conceptual      |
   |                      |             |      | Volume Segmentation  |
   |                      |             |      | Reference            |
   |                      |             |      | Sequence <           |
   |                      |             |      | #sect_10.34.1.4>`__. |
   +----------------------+-------------+------+----------------------+
   | >Referenced Direct   | (3010,004A) | 1    | Reference to the SOP |
   | Segment Instance     |             |      | Instance that        |
   | Sequence             |             |      | contains the Segment |
   |                      |             |      | Reference Sequence   |
   |                      |             |      | (3010,0021) in which |
   |                      |             |      | the segment is       |
   |                      |             |      | defined.             |
   |                      |             |      |                      |
   |                      |             |      | Only a single Item   |
   |                      |             |      | shall be included in |
   |                      |             |      | this Sequence.       |
   |                      |             |      |                      |
   |                      |             |      | See `Referenced      |
   |                      |             |      | Direct Segment       |
   |                      |             |      | Instance             |
   |                      |             |      | Sequence <           |
   |                      |             |      | #sect_10.34.1.3>`__. |
   +----------------------+-------------+------+----------------------+
   | *>>                  |             |      |                      |
   | Include*\ `table_tit |             |      |                      |
   | le <#table_10-11>`__ |             |      |                      |
   +----------------------+-------------+------+----------------------+
   | >Referenced Segment  | (3010,0020) | 1    | The Segment          |
   | Reference Index      |             |      | Reference Index      |
   |                      |             |      | (3010,0022) in the   |
   |                      |             |      | Segment Reference    |
   |                      |             |      | Sequence (3010,0021) |
   |                      |             |      | corresponding to the |
   |                      |             |      | segment representing |
   |                      |             |      | this Conceptual      |
   |                      |             |      | Volume.              |
   |                      |             |      |                      |
   |                      |             |      | In the segment Item  |
   |                      |             |      | referenced, the      |
   |                      |             |      | Direct Segment       |
   |                      |             |      | Reference Sequence   |
   |                      |             |      | (3010,0023) shall be |
   |                      |             |      | present.             |
   +----------------------+-------------+------+----------------------+

.. _sect_10.34.1:

Conceptual Volume Segmentation Reference and Combination Macro Attribute Description
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. _sect_10.34.1.1:

Conceptual Volume Combination Expression
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

For Conceptual Volumes specified as a combination of other Conceptual
Volumes, the combination logic is specified by the text string value of
the Conceptual Volume Combination Expression (3010,000C).

A nested list notation is used to apply geometric operators to a set of
Conceptual Volumes.

The first element of the list shall be one of the following geometric
operators:

UNION
   geometric union of two or more arguments

INTERSECTION
   geometric intersection of two or more arguments

NEGATION
   geometric inverse of a single argument

SUBTRACTION
   geometric subtraction of second argument from the first

XOR
   geometric exclusive disjunction of two arguments

.. note::

   The result of a NEGATION operation is well-defined only if used as an
   operand to an INTERSECTION. NEGATION without context to an
   INTERSECTION results in an infinite Volume.

Subsequent elements shall specify arguments of the geometric operator.
An argument is either a Conceptual Volume Constituent Index (3010,000D)
value (i.e., positive integer) or a parenthesized list of operations.

The grammar for the Conceptual Volume Combination Expression (<sexpr>)
is shown below in BNF (Backus Naur Form) :

::

   <sexpr>         :: <cv> | <list>
   <cv>            :: 1 | 2 | 3 | …
   <list>          :: ( <op1><sp><sexpr> ) |
                      ( <op2><sp><sexpr><sp><sexpr> ) |
                      ( <op3><sp><args> )
   <args>          :: <sexpr><sp><sexpr> | <args><sp><sexpr>
   <op1>           :: NEGATION
   <op2>           :: SUBTRACTION | XOR
   <op3>           :: UNION | INTERSECTION
   <sp>            :: 0x20

Examples:

1. Union of paired organs 1 and 2 (disjoint)

   Conceptual Volume Combination Expression (3010,000C):

   (UNION 1 2)

   Items in Conceptual Volume Constituent Sequence (3010,0008):

   .. table:: Conceptual Volume Example of Union of Disjoint Volumes

      =============================================== =================
      Conceptual Volume Constituent Index (3010,000D) Conceptual Volume
      =============================================== =================
      1                                               Right Lung
      2                                               Left Lung
      =============================================== =================

2. Union of paired organs 1 and 2 (non-disjoint)

   Conceptual Volume Combination Expression (3010,000C):

   (UNION 1 2)

   Items in Conceptual Volume Constituent Sequence (3010,0008) :

   .. table:: Conceptual Volume Example of Union of non-disjoint Volumes

      =============================================== =================
      Conceptual Volume Constituent Index (3010,000D) Conceptual Volume
      =============================================== =================
      1                                               Spinal Cord PRV
      2                                               Left Lung
      =============================================== =================

3. Union of two organs 1 and 2 with excluded volume 3 using NEGATION

   Conceptual Volume Combination Expression (3010,000C):

   (INTERSECTION (UNION 1 2) (NEGATION 3) )

   Items in Conceptual Volume Constituent Sequence (3010,0008):

   .. table:: Conceptual Volume Example of Intersection and Negation

      =============================================== =================
      Conceptual Volume Constituent Index (3010,000D) Conceptual Volume
      =============================================== =================
      1                                               Heart
      2                                               Left Lung
      3                                               CTV
      =============================================== =================

4. Union of paired organs 1 and 2, with exclusion of multiple volumes 3,
   4 and 5

   Conceptual Volume Combination Expression (3010,000C):

   (INTERSECTION (UNION 1 2) (NEGATION (UNION 3 4 5) ))

   .. note::

      This combination can be expressed alternatively as:

      (SUBTRACTION (UNION 1 2) (UNION 3 4 5) )

   Items in Conceptual Volume Constituent Sequence (3010,0008):

   .. table:: Conceptual Volume Example of Intersection and Union

      =============================================== =================
      Conceptual Volume Constituent Index (3010,000D) Conceptual Volume
      =============================================== =================
      1                                               R Lung
      2                                               L Lung
      3                                               Node 1
      4                                               Node 2
      5                                               CTV
      =============================================== =================

5. Intersection of overlapping volumes 1 and 2

   Conceptual Volume Combination Expression (3010,000C):

   (INTERSECTION 1 2)

   Items in Conceptual Volume Constituent Sequence (3010,0008):

   .. table:: Conceptual Volume Example of Intersection of non-disjunct
   Volumes

      =============================================== =================
      Conceptual Volume Constituent Index (3010,000D) Conceptual Volume
      =============================================== =================
      1                                               Rectum
      2                                               Prostate PTV
      =============================================== =================

6. Intersection of disjoint volumes 1 and 2

   Conceptual Volume Combination Expression (3010,000C):

   (INTERSECTION 1 2)

   Items in Conceptual Volume Constituent Sequence (3010,0008):

   .. table:: Conceptual Volume Example of Intersection of disjunct
   Volumes

      =============================================== =================
      Conceptual Volume Constituent Index (3010,000D) Conceptual Volume
      =============================================== =================
      1                                               Bladder
      2                                               Prostate
      =============================================== =================

.. _sect_10.34.1.2:

Conceptual Volume Segmentation Reference Sequence
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Conceptual Volume Constituent Segmentation Reference Sequence
(3010,0012) contains a reference to a segmentation which represents the
volume of this consituent geometrically. The referenced segmentations of
the constituents of a combined Conceptual Volume may be in one or more
Frames of References.

The Conceptual Volume constituents shall not include the combined
Conceptual Volume being defined. Applications that wish to combine
existing segmentations within the same Conceptual Volume must create a
new Segmentation Instance.

.. _sect_10.34.1.3:

Referenced Direct Segment Instance Sequence
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

A SOP Instance may only be referenced in this Sequence if it belongs to
a SOP Class that includes the `Segment Reference
Module <#sect_C.36.9>`__.

.. _sect_10.34.1.4:

Conceptual Volume Segmentation Reference Sequence
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Conceptual Volume Segmentation Reference Sequence (3010,0011)
contains a reference to a segmentation which represents this volume
geometrically.

.. _sect_10.35:

Device Model Macro
------------------

The Device Model Macro contains general Attributes needed to specify a
device model other than the device creating the SOP Instance.

.. table:: Device Model Macro Attributes

   +----------------------+-------------+------+----------------------+
   | Attribute Name       | Tag         | Type | Attribute            |
   |                      |             |      | Description          |
   +======================+=============+======+======================+
   | Manufacturer         | (0008,0070) | 2    | Manufacturer of the  |
   |                      |             |      | device.              |
   +----------------------+-------------+------+----------------------+
   | Manufacturer's Model | (0008,1090) | 2    | Manufacturer's model |
   | Name                 |             |      | name of the device.  |
   +----------------------+-------------+------+----------------------+
   | Manufacturer's Model | (3010,001A) | 2    | A version number of  |
   | Version              |             |      | the Manufacturer's   |
   |                      |             |      | model of the device. |
   +----------------------+-------------+------+----------------------+

.. _sect_10.36:

Device Identification Macro
---------------------------

The Device Identification Macro identifies a (physical or virtual)
device.

.. table:: Device Identification Macro Attributes

   +-------------------+-------------------+------+-------------------+
   | Attribute Name    | Tag               | Type | Attribute         |
   |                   |                   |      | Description       |
   +===================+===================+======+===================+
   | Device Type Code  | (3010,002E)       | 1    | The type of the   |
   | Sequence          |                   |      | device.           |
   |                   |                   |      |                   |
   |                   |                   |      | Only a single     |
   |                   |                   |      | Item shall be     |
   |                   |                   |      | included in this  |
   |                   |                   |      | Sequence.         |
   +-------------------+-------------------+------+-------------------+
   | *>Includ          | *CID may be       |      |                   |
   | e*\ `table_title  | defined in the    |      |                   |
   | <#table_8.8-1>`__ | Macro             |      |                   |
   |                   | invocation.*      |      |                   |
   +-------------------+-------------------+------+-------------------+
   | Device Label      | (3010,002D)       | 1    | User-defined      |
   |                   |                   |      | label for this    |
   |                   |                   |      | device.           |
   +-------------------+-------------------+------+-------------------+
   | Long Device       | (0050,0021)       | 3    | User-defined      |
   | Description       |                   |      | description for   |
   |                   |                   |      | this device.      |
   +-------------------+-------------------+------+-------------------+
   | Device Serial     | (0018,1000)       | 2    | Manufacturer"s    |
   | Number            |                   |      | serial number of  |
   |                   |                   |      | the device.       |
   +-------------------+-------------------+------+-------------------+
   | Software Versions | (0018,1020)       | 2    | Manufacturer's    |
   |                   |                   |      | designation of    |
   |                   |                   |      | software version  |
   |                   |                   |      | of the equipment. |
   +-------------------+-------------------+------+-------------------+
   | UDI Sequence      | (0018,100A)       | 3    | Unique Device     |
   |                   |                   |      | Identifier (UDI)  |
   |                   |                   |      | of the device.    |
   |                   |                   |      |                   |
   |                   |                   |      | One or more Items |
   |                   |                   |      | are permitted in  |
   |                   |                   |      | this Sequence.    |
   |                   |                   |      |                   |
   |                   |                   |      | .. note::         |
   |                   |                   |      |                   |
   |                   |                   |      |    Multiple Items |
   |                   |                   |      |    may be present |
   |                   |                   |      |    if the entire  |
   |                   |                   |      |    equipment has  |
   |                   |                   |      |    UDIs issued by |
   |                   |                   |      |    different      |
   |                   |                   |      |    Issuing        |
   |                   |                   |      |    Authorities.   |
   +-------------------+-------------------+------+-------------------+
   | *>Include*        |                   |      |                   |
   | \ `table_title <# |                   |      |                   |
   | table_10.29-1>`__ |                   |      |                   |
   +-------------------+-------------------+------+-------------------+
   | Manufacturer's    | (3010,0043)       | 2    | An identifier     |
   | Device Identifier |                   |      | issued by the     |
   |                   |                   |      | manufacturer.     |
   |                   |                   |      |                   |
   |                   |                   |      | See Note.         |
   +-------------------+-------------------+------+-------------------+
   | Device Alternate  | (3010,001B)       | 2    | An identifier     |
   | Identifier        |                   |      | intended to be    |
   |                   |                   |      | read by a device  |
   |                   |                   |      | such as a bar     |
   |                   |                   |      | code reader.      |
   +-------------------+-------------------+------+-------------------+
   | Device Alternate  | (3010,001C)       | 1C   | Defines the type  |
   | Identifier Type   |                   |      | of Device         |
   |                   |                   |      | Alternate         |
   |                   |                   |      | Identifier.       |
   |                   |                   |      |                   |
   |                   |                   |      | Required if       |
   |                   |                   |      | Device Alternate  |
   |                   |                   |      | Identifier        |
   |                   |                   |      | (3010,001B) is    |
   |                   |                   |      | present.          |
   |                   |                   |      |                   |
   |                   |                   |      | BARCODE           |
   |                   |                   |      | RFID              |
   +-------------------+-------------------+------+-------------------+
   | Device Alternate  | (3010,001D)       | 1C   | Description of    |
   | Identifier Format |                   |      | the format in     |
   |                   |                   |      | which the Device  |
   |                   |                   |      | Alternate         |
   |                   |                   |      | Identifier        |
   |                   |                   |      | (3010,001B) is    |
   |                   |                   |      | issued.           |
   |                   |                   |      |                   |
   |                   |                   |      | Required if       |
   |                   |                   |      | Device Alternate  |
   |                   |                   |      | Identifier        |
   |                   |                   |      | (3010,001B) is    |
   |                   |                   |      | present.          |
   |                   |                   |      |                   |
   |                   |                   |      | See `Device       |
   |                   |                   |      | Alternate         |
   |                   |                   |      | Identifier        |
   |                   |                   |      | Format <#se       |
   |                   |                   |      | ct_10.36.1.1>`__. |
   +-------------------+-------------------+------+-------------------+

.. note::

   Typically, the Device Identifier is a code which can be
   electronically read by the machine utilizing that device, e.g. to
   verify the presence of that device.

.. _sect_10.36.1:

Device Component Identification Macro Attribute Descriptions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. _sect_10.36.1.1:

Device Alternate Identifier Format
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Device Alternate Identifier Format (3010,001D) specifies the format
of the value of the Device Alternate Identifier (3010,001B).

If the value of Device Alternate Identifier Type (3010,001C) is RFID, a
big variety of RFID formats exists (some examples are DOD-96, DOD-64
UID, GID-96, sgtin-96). Supported format values shall be defined in the
Conformance Statement.

For Device Alternate Identifier Type (3010,001C) = BARCODE, see `Barcode
Symbology <#sect_C.22.1.1>`__.

.. _sect_10.37:

Related Information Entities Macro
----------------------------------

This Macro defines references to entities and their purpose of
reference. References can be made at the Study level, Series level,
Instance level or Frame Level.

The attributes Pertinent SOP Classes in Study (3010,0052) and Pertinent
SOP Classes in Series (3010,0053) allow the specification of the
relevant SOP Classes for the given purpose. These attributes support
filtering for certain SOP Classes, specification of corresponding query
keys, and allowing the receiving application to assess its capabilities
to handle the specified objects.

All referenced Studies, Series and Instances share the same single
Purpose of Reference.

.. table:: Related Information Entities Macro Attributes

   +-------------------+-------------------+------+-------------------+
   | Attribute Name    | Tag               | Type | Attribute         |
   |                   |                   |      | Description       |
   +===================+===================+======+===================+
   | Purpose of        | (0040,A170)       | 1    | Describes the     |
   | Reference Code    |                   |      | purpose for which |
   | Sequence          |                   |      | the references    |
   |                   |                   |      | are made.         |
   |                   |                   |      |                   |
   |                   |                   |      | Only a single     |
   |                   |                   |      | Item shall be     |
   |                   |                   |      | included in this  |
   |                   |                   |      | Sequence.         |
   +-------------------+-------------------+------+-------------------+
   | *>Includ          | *CID may be       |      |                   |
   | e*\ `table_title  | defined in the    |      |                   |
   | <#table_8.8-1>`__ | Macro             |      |                   |
   |                   | invocation.*      |      |                   |
   +-------------------+-------------------+------+-------------------+
   | Referenced Study  | (0008,1110)       | 1    | Studies which are |
   | Sequence          |                   |      | relevant for the  |
   |                   |                   |      | invocation        |
   |                   |                   |      | context.          |
   |                   |                   |      |                   |
   |                   |                   |      | One or more Items |
   |                   |                   |      | shall be included |
   |                   |                   |      | in this Sequence. |
   +-------------------+-------------------+------+-------------------+
   | >Study Instance   | (0020,000D)       | 1    | Uniquely          |
   | UID               |                   |      | identifies the    |
   |                   |                   |      | referenced Study. |
   +-------------------+-------------------+------+-------------------+
   | >Pertinent SOP    | (3010,0052)       | 3    | The SOP Classes   |
   | Classes in Study  |                   |      | in the Study      |
   |                   |                   |      | which are         |
   |                   |                   |      | relevant for the  |
   |                   |                   |      | invocation        |
   |                   |                   |      | context.          |
   |                   |                   |      |                   |
   |                   |                   |      | If not present,   |
   |                   |                   |      | all SOP Instances |
   |                   |                   |      | included in the   |
   |                   |                   |      | referenced Study  |
   |                   |                   |      | are considered    |
   |                   |                   |      | relevant.         |
   +-------------------+-------------------+------+-------------------+
   | >Referenced       | (0008,1115)       | 3    | Series which are  |
   | Series Sequence   |                   |      | relevant for the  |
   |                   |                   |      | invocation        |
   |                   |                   |      | context.          |
   |                   |                   |      |                   |
   |                   |                   |      | One or more Items |
   |                   |                   |      | are permitted in  |
   |                   |                   |      | this Sequence.    |
   +-------------------+-------------------+------+-------------------+
   | >>Series Instance | (0020,000E)       | 1    | Uniquely          |
   | UID               |                   |      | identifies the    |
   |                   |                   |      | referenced        |
   |                   |                   |      | Series.           |
   +-------------------+-------------------+------+-------------------+
   | >>Pertinent SOP   | (3010,0053)       | 3    | The SOP Classes   |
   | Classes in Series |                   |      | in the Series     |
   |                   |                   |      | which are         |
   |                   |                   |      | relevant for the  |
   |                   |                   |      | invocation        |
   |                   |                   |      | context.          |
   |                   |                   |      |                   |
   |                   |                   |      | If not present,   |
   |                   |                   |      | all SOP Instances |
   |                   |                   |      | included in the   |
   |                   |                   |      | referenced Series |
   |                   |                   |      | are considered    |
   |                   |                   |      | relevant.         |
   +-------------------+-------------------+------+-------------------+
   | >>Referenced      | (0008,1140)       | 3    | Image SOP         |
   | Image Sequence    |                   |      | Instances which   |
   |                   |                   |      | are relevant in   |
   |                   |                   |      | the invocation    |
   |                   |                   |      | context.          |
   |                   |                   |      |                   |
   |                   |                   |      | One or more Items |
   |                   |                   |      | are permitted for |
   |                   |                   |      | this Sequence.    |
   +-------------------+-------------------+------+-------------------+
   | *>>>Inclu         |                   |      |                   |
   | de*\ `table_title |                   |      |                   |
   |  <#table_10-3>`__ |                   |      |                   |
   +-------------------+-------------------+------+-------------------+
   | >>Referenced      | (0008,114A)       | 3    | Non-Image SOP     |
   | Instance Sequence |                   |      | Instances which   |
   |                   |                   |      | are relevant in   |
   |                   |                   |      | the invocation    |
   |                   |                   |      | context.          |
   |                   |                   |      |                   |
   |                   |                   |      | One or more Items |
   |                   |                   |      | are permitted for |
   |                   |                   |      | this Sequence.    |
   +-------------------+-------------------+------+-------------------+
   | *>>>Includ        |                   |      |                   |
   | e*\ `table_title  |                   |      |                   |
   | <#table_10-11>`__ |                   |      |                   |
   +-------------------+-------------------+------+-------------------+

.. _sect_10.38:

Outline Definition Macro
------------------------

The Outline Definition Macro describes a 2D outline in a given
coordinate system.

.. table:: Outline Definition Macro Attributes

   +----------------------+-------------+------+----------------------+
   | Attribute Name       | Tag         | Type | Attribute            |
   |                      |             |      | Description          |
   +======================+=============+======+======================+
   | Outline Shape Type   | (0018,1630) | 1    | Type of shape of the |
   |                      |             |      | outline.             |
   |                      |             |      |                      |
   |                      |             |      | RECTANGULAR          |
   |                      |             |      | CIRCULAR             |
   |                      |             |      | POLYGONAL            |
   |                      |             |      |                      |
   |                      |             |      | See `Outline Shape   |
   |                      |             |      | Type <               |
   |                      |             |      | #sect_10.38.1.1>`__. |
   +----------------------+-------------+------+----------------------+
   | Outline Left         | (0018,1631) | 1C   | X-coordinate in mm   |
   | Vertical Edge        |             |      | of the left edge of  |
   |                      |             |      | the rectangular      |
   |                      |             |      | outline (parallel to |
   |                      |             |      | the y-axis of the    |
   |                      |             |      | coordinate system).  |
   |                      |             |      |                      |
   |                      |             |      | Required if Outline  |
   |                      |             |      | Shape Type           |
   |                      |             |      | (0018,1630) is       |
   |                      |             |      | RECTANGULAR.         |
   |                      |             |      |                      |
   |                      |             |      | See `Coordinate      |
   |                      |             |      | Definitions <        |
   |                      |             |      | #sect_10.38.1.2>`__. |
   +----------------------+-------------+------+----------------------+
   | Outline Right        | (0018,1632) | 1C   | X-coordinate in mm   |
   | Vertical Edge        |             |      | of the right edge of |
   |                      |             |      | the rectangular      |
   |                      |             |      | outline (parallel to |
   |                      |             |      | the y-axis of the    |
   |                      |             |      | coordinate system).  |
   |                      |             |      |                      |
   |                      |             |      | Required if Outline  |
   |                      |             |      | Shape Type           |
   |                      |             |      | (0018,1630) is       |
   |                      |             |      | RECTANGULAR.         |
   |                      |             |      |                      |
   |                      |             |      | See `Coordinate      |
   |                      |             |      | Definitions <        |
   |                      |             |      | #sect_10.38.1.2>`__. |
   +----------------------+-------------+------+----------------------+
   | Outline Upper        | (0018,1633) | 1C   | Y-coordinate in mm   |
   | Horizontal Edge      |             |      | of the upper edge of |
   |                      |             |      | the rectangular      |
   |                      |             |      | outline (parallel to |
   |                      |             |      | the x-axis of the    |
   |                      |             |      | coordinate system).  |
   |                      |             |      |                      |
   |                      |             |      | Required if Outline  |
   |                      |             |      | Shape Type           |
   |                      |             |      | (0018,1630) is       |
   |                      |             |      | RECTANGULAR.         |
   |                      |             |      |                      |
   |                      |             |      | See `Coordinate      |
   |                      |             |      | Definitions <        |
   |                      |             |      | #sect_10.38.1.2>`__. |
   +----------------------+-------------+------+----------------------+
   | Outline Lower        | (0018,1634) | 1C   | Y-coordinate in mm   |
   | Horizontal Edge      |             |      | of the lower edge of |
   |                      |             |      | the rectangular      |
   |                      |             |      | outline (parallel to |
   |                      |             |      | the x-axis of the    |
   |                      |             |      | coordinate system).  |
   |                      |             |      |                      |
   |                      |             |      | Required if Outline  |
   |                      |             |      | Shape Type           |
   |                      |             |      | (0018,1630) is       |
   |                      |             |      | RECTANGULAR.         |
   |                      |             |      |                      |
   |                      |             |      | See `Coordinate      |
   |                      |             |      | Definitions <        |
   |                      |             |      | #sect_10.38.1.2>`__. |
   +----------------------+-------------+------+----------------------+
   | Center of Circular   | (0018,1635) | 1C   | Location (x,y) in mm |
   | Outline              |             |      | of the center of the |
   |                      |             |      | circular outline.    |
   |                      |             |      |                      |
   |                      |             |      | Required if Outline  |
   |                      |             |      | Shape Type           |
   |                      |             |      | (0018,1630) is       |
   |                      |             |      | CIRCULAR.            |
   |                      |             |      |                      |
   |                      |             |      | See `Coordinate      |
   |                      |             |      | Definitions <        |
   |                      |             |      | #sect_10.38.1.2>`__. |
   +----------------------+-------------+------+----------------------+
   | Diameter of Circular | (0018,1636) | 1C   | Diameter in mm of    |
   | Outline              |             |      | the circular         |
   |                      |             |      | outline.             |
   |                      |             |      |                      |
   |                      |             |      | Required if Outline  |
   |                      |             |      | Shape Type           |
   |                      |             |      | (0018,1630) is       |
   |                      |             |      | CIRCULAR.            |
   |                      |             |      |                      |
   |                      |             |      | See `Coordinate      |
   |                      |             |      | Definitions <        |
   |                      |             |      | #sect_10.38.1.2>`__. |
   +----------------------+-------------+------+----------------------+
   | Number of Polygonal  | (0018,1637) | 1C   | Number of Vertices   |
   | Vertices             |             |      | in Vertices of the   |
   |                      |             |      | Polygonal Outline    |
   |                      |             |      | (0018,1638).         |
   |                      |             |      |                      |
   |                      |             |      | Required if Outline  |
   |                      |             |      | Shape Type           |
   |                      |             |      | (0018,1630) is       |
   |                      |             |      | POLYGONAL.           |
   +----------------------+-------------+------+----------------------+
   | Vertices of the      | (0018,1638) | 1C   | A data stream of     |
   | Polygonal Outline    |             |      | pairs of x and y in  |
   |                      |             |      | mm. Polygonal        |
   |                      |             |      | outlines are         |
   |                      |             |      | implicitly closed    |
   |                      |             |      | from the last vertex |
   |                      |             |      | to the origin vertex |
   |                      |             |      | and all edges shall  |
   |                      |             |      | be non-intersecting  |
   |                      |             |      | except at the        |
   |                      |             |      | vertices. Any given  |
   |                      |             |      | vertex shall occur   |
   |                      |             |      | only once in the     |
   |                      |             |      | data stream.         |
   |                      |             |      |                      |
   |                      |             |      | Required if Outline  |
   |                      |             |      | Shape Type           |
   |                      |             |      | (0018,1630) is       |
   |                      |             |      | POLYGONAL.           |
   |                      |             |      |                      |
   |                      |             |      | The number of        |
   |                      |             |      | pairsin this data    |
   |                      |             |      | stream shall equal   |
   |                      |             |      | the value ofNumber   |
   |                      |             |      | of Polygonal         |
   |                      |             |      | Vertices             |
   |                      |             |      | (0018,1637).         |
   |                      |             |      |                      |
   |                      |             |      | See `Coordinate      |
   |                      |             |      | Definitions <        |
   |                      |             |      | #sect_10.38.1.2>`__. |
   +----------------------+-------------+------+----------------------+

.. _sect_10.38.1:

Outline Definition Macro Attribute Description
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. _sect_10.38.1.1:

Outline Shape Type
^^^^^^^^^^^^^^^^^^

When outline shape is a rectangle or a circle per design, the Outline
Shape Type (0018,1630) shall have the value RECTANGULAR or CIRCULAR
respectively and the outline shall not be represented as a polyline.

.. _sect_10.38.1.2:

Coordinate Definitions
^^^^^^^^^^^^^^^^^^^^^^

The values are defined in a plane that is declared in the invocation of
the Macro.

.. _sect_10.39:

Patient to Equipment Relationship Macro
---------------------------------------

The Patient to Equipment Relationship Macro describes a position of the
patient with respect to a device. The position is defined by means of a
transformation matrix between a Patient Frame of Reference and an
Equipment Frame of Reference.

.. table:: Patient to Equipment Relationship Macro Attributes

   +-------------------+-------------------+------+-------------------+
   | Attribute Name    | Tag               | Type | Attribute         |
   |                   |                   |      | Description       |
   +===================+===================+======+===================+
   | Image to          | (0028,9520)       | 1    | A rigid,          |
   | Equipment Mapping |                   |      | homogeneous 4x4   |
   | Matrix            |                   |      | transformation    |
   |                   |                   |      | matrix that maps  |
   |                   |                   |      | the patient       |
   |                   |                   |      | coordinate space  |
   |                   |                   |      | in the Frame of   |
   |                   |                   |      | Reference used    |
   |                   |                   |      | for the patient   |
   |                   |                   |      | model to the      |
   |                   |                   |      | coordinate system |
   |                   |                   |      | defined by the    |
   |                   |                   |      | equipment. Matrix |
   |                   |                   |      | elements shall be |
   |                   |                   |      | listed in         |
   |                   |                   |      | row-major order.  |
   |                   |                   |      |                   |
   |                   |                   |      | See `Equipment    |
   |                   |                   |      | Coordinate        |
   |                   |                   |      | System <#se       |
   |                   |                   |      | ct_10.39.1.1>`__, |
   |                   |                   |      | `Image to         |
   |                   |                   |      | Equipment Mapping |
   |                   |                   |      | Matrix and        |
   |                   |                   |      | Patient Support   |
   |                   |                   |      | Position          |
   |                   |                   |      | Macro <#s         |
   |                   |                   |      | ect_10.39.1.2>`__ |
   |                   |                   |      | and `Image to     |
   |                   |                   |      | Equipment Mapping |
   |                   |                   |      | Matrix <#sec      |
   |                   |                   |      | t_C.7.6.21.1>`__. |
   +-------------------+-------------------+------+-------------------+
   | Frame of          | (3006,00C8)       | 3    | Comments entered  |
   | Reference         |                   |      | by a human        |
   | Transformation    |                   |      | operator about    |
   | Comment           |                   |      | the relationship  |
   |                   |                   |      | between the       |
   |                   |                   |      | patient frame of  |
   |                   |                   |      | reference and the |
   |                   |                   |      | equipment. For    |
   |                   |                   |      | display purposes  |
   |                   |                   |      | only, shall not   |
   |                   |                   |      | be used for other |
   |                   |                   |      | purposes.         |
   +-------------------+-------------------+------+-------------------+
   | Patient Location  | (3006,00C9)       | 2    | Specific points   |
   | Coordinates       |                   |      | in the patient    |
   | Sequence          |                   |      | coordinate system |
   |                   |                   |      | which further     |
   |                   |                   |      | characterize the  |
   |                   |                   |      | position of the   |
   |                   |                   |      | patient with      |
   |                   |                   |      | respect to the    |
   |                   |                   |      | equipment.        |
   |                   |                   |      |                   |
   |                   |                   |      | Zero or more      |
   |                   |                   |      | Items shall be    |
   |                   |                   |      | included in this  |
   |                   |                   |      | Sequence.         |
   +-------------------+-------------------+------+-------------------+
   | >3D Point         | (0068,6590)       | 1    | Coordinate        |
   | Coordinate        |                   |      | (x,y,z) in mm     |
   |                   |                   |      | describing the    |
   |                   |                   |      | location in the   |
   |                   |                   |      | patient Frame of  |
   |                   |                   |      | Reference that    |
   |                   |                   |      | will be           |
   |                   |                   |      | transformed to    |
   |                   |                   |      | the Equipment     |
   |                   |                   |      | Frame of          |
   |                   |                   |      | Reference by      |
   |                   |                   |      | using the Image   |
   |                   |                   |      | to Equipment      |
   |                   |                   |      | Mapping Matrix    |
   |                   |                   |      | (0028,9520).      |
   +-------------------+-------------------+------+-------------------+
   | >Patient Location | (3006,00CA)       | 1    | Identifies the    |
   | Coordinates Code  |                   |      | type of Patient   |
   | Sequence          |                   |      | Location          |
   |                   |                   |      | Coordinate.       |
   |                   |                   |      |                   |
   |                   |                   |      | One or more Items |
   |                   |                   |      | shall be included |
   |                   |                   |      | in this Sequence. |
   +-------------------+-------------------+------+-------------------+
   | *>>Include*\ `    | *CID is specified |      |                   |
   | table_title <#tab | at invocation.*   |      |                   |
   | le_8.8-1>`__\ *.* |                   |      |                   |
   +-------------------+-------------------+------+-------------------+
   | Patient Support   | (3006,00CB)       | 2    | Actual Patient    |
   | Position Sequence |                   |      | Support Position  |
   |                   |                   |      | parameters. Shall |
   |                   |                   |      | be consistent     |
   |                   |                   |      | with the Image to |
   |                   |                   |      | Equipment Mapping |
   |                   |                   |      | Matrix            |
   |                   |                   |      | (0028,9520).      |
   |                   |                   |      |                   |
   |                   |                   |      | See `Image to     |
   |                   |                   |      | Equipment Mapping |
   |                   |                   |      | Matrix and        |
   |                   |                   |      | Patient Support   |
   |                   |                   |      | Position          |
   |                   |                   |      | Macro <#se        |
   |                   |                   |      | ct_10.39.1.2>`__. |
   |                   |                   |      |                   |
   |                   |                   |      | Zero or one Item  |
   |                   |                   |      | shall be included |
   |                   |                   |      | in this Sequence. |
   +-------------------+-------------------+------+-------------------+
   | *>Include*\ `ta   |                   |      |                   |
   | ble_title <#table |                   |      |                   |
   | _10.40-1>`__\ *.* |                   |      |                   |
   +-------------------+-------------------+------+-------------------+

.. _sect_10.39.1:

Patient to Equipment Relationship Macro Attributes Description
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. _sect_10.39.1.1:

Equipment Coordinate System
^^^^^^^^^^^^^^^^^^^^^^^^^^^

A piece of equipment has an Equipment Coordinate System which can be
used for expressing geometric concepts such as locations and
orientations.The coordinate system is characterized by the location of
the origin and the orientation of coordinate axes with respect to the
equipment. The Equipment Coordinate System is a right-handed coordinate
system.

Equipment Coordinate Systems are typically based on a standardized
definition of axes. The choice of origin is often device-specific or
device-type-specific. It may be any significant location on the machine
such as the manufacturer-dependent machine isocenter.

The Equipment Coordinate System can be used as the parent for derived
coordinate systems.

.. _sect_10.39.1.2:

Image to Equipment Mapping Matrix and Patient Support Position Macro
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Image to Equipment Mapping Matrix (0028,9520) describes the
relationship between the Patient-oriented coordinate system and an
Equipment Coordinate System. This matrix :sup:`A`\ M :sub:`B`\ describes
a rigid transformation of a point ( :sup:`B`\ x, :sup:`B`\ y,
:sup:`B`\ z) with respect to the Patient coordinate system into (
:sup:`A`\ x, :sup:`A`\ y, :sup:`A`\ z) with respect to the Equipment
Coordinate System as defined in `Image to Equipment Mapping
Matrix <#sect_C.7.6.21.1>`__.

The Equipment Coordinate System is identified by the Equipment Frame of
Reference UID (300A,0675). For further information on the definition of
the Equipment Frame of Reference, see `Equipment Coordinate
System <#sect_10.39.1.1>`__. The patient-oriented coordinate system is
identified by the Frame of Reference UID (0020,0052) of the SOP Instance
it is used within. Both coordinate systems are expressed in millimeters.

The Patient Support Position Macro invoked by Patient Support Position
Sequence (3006,00CB) allows the exchange of device-specific parameters
for the patient support device. Applications designed to guide a
specific patient support device will be able to de-compose the
transformation into device-specific parameters or derive a
transformation matrix out of these parameters. Applications that are
unable to know the decomposition of the transformation to those
parameters and vice versa will still be able to display the native
labels and numerical values of those parameters to human readers.

The Patient Support Position Sequence (3006,00CB) may be present to
annotate the matrix and display the decomposed matrix contents. The
content of the Patient Support Position Macro shall be used for display
purposes only. It shall not be used for other purposes. The content of
this Macro shall not be used as a substitute for the Image to Equipment
Mapping Matrix (0028,9520). In general, there is more than one way to
reach the point in space that is described by the Image to Equipment
Mapping Matrix (0028,9520). Hence it is explicitly not implied how this
position is reached.

In some cases (e.g., emergency treatments in Radiotherapy), the Patient
Frame of Reference is not defined by an image series. In this case an
arbitrary Frame of Reference is used for the patient coordinate system
in the Frame of Reference Module of the SOP Instance. The Image to
Equipment Mapping Matrix (0028,9520) has the same meaning as in the case
of image-based Patient Frame of Reference.

If the Image to Equipment Mapping Matrix (0028,9520) and the Patient
Support Position Sequence (3006,00CB) are both present, the information
in both locations shall be consistent.

.. _sect_10.40:

Patient Support Position Macro
------------------------------

This Macro provides the device-specific geometric settings for the
Patient Support device.

The information is intended for display to human readers and to support
non-image-based patient positioning; however, the definition of the
patient position with respect to the device is contained in the Image to
Equipment Mapping Matrix (0028,9520).

.. table:: Patient Support Position Macro Attributes

   +----------------------+-------------+------+----------------------+
   | Attribute Name       | Tag         | Type | Attribute            |
   |                      |             |      | Description          |
   +======================+=============+======+======================+
   | Patient Support      | (300A,065C) | 1    | Method of            |
   | Position             |             |      | specification for    |
   | Specification Method |             |      | patient support      |
   |                      |             |      | parameters.          |
   |                      |             |      |                      |
   |                      |             |      | ABSENT               |
   |                      |             |      |    lNo parameters    |
   |                      |             |      |    are specified.    |
   |                      |             |      |                      |
   |                      |             |      | GLOBAL               |
   |                      |             |      |    Parameters are    |
   |                      |             |      |    specified using a |
   |                      |             |      |    globally known    |
   |                      |             |      |    method,           |
   |                      |             |      |    irrespective of   |
   |                      |             |      |    the device in     |
   |                      |             |      |    use.              |
   |                      |             |      |                      |
   |                      |             |      | DEVICE_SPECIFIC      |
   |                      |             |      |    Parameters are    |
   |                      |             |      |    specified using a |
   |                      |             |      |    device-specific   |
   |                      |             |      |    method.           |
   +----------------------+-------------+------+----------------------+
   | Patient Support      | (300A,065D) | 1C   | Translational and    |
   | Position Device      |             |      | rotational           |
   | Parameter Sequence   |             |      | parameters for       |
   |                      |             |      | Patient Support      |
   |                      |             |      | devices.             |
   |                      |             |      |                      |
   |                      |             |      | Required if Patient  |
   |                      |             |      | Support Position     |
   |                      |             |      | Specification Method |
   |                      |             |      | (300A,065C) does not |
   |                      |             |      | equal ABSENT.        |
   |                      |             |      |                      |
   |                      |             |      | One or more Items    |
   |                      |             |      | shall be included in |
   |                      |             |      | this Sequence if     |
   |                      |             |      | Patient Support      |
   |                      |             |      | Position             |
   |                      |             |      | Specification Method |
   |                      |             |      | (300A,065C) equals   |
   |                      |             |      | DEVICE_SPECIFIC.     |
   |                      |             |      |                      |
   |                      |             |      | Only one Item shall  |
   |                      |             |      | be included in this  |
   |                      |             |      | Sequence if Patient  |
   |                      |             |      | Support Position     |
   |                      |             |      | Specification Method |
   |                      |             |      | (300A,065C) equals   |
   |                      |             |      | GLOBAL.              |
   +----------------------+-------------+------+----------------------+
   | >Referenced Device   | (300A,0607) | 1C   | The value of Device  |
   | Index                |             |      | Index (3010,0039) in |
   |                      |             |      | Patient Support      |
   |                      |             |      | Devices Sequence     |
   |                      |             |      | (300A,0686)          |
   |                      |             |      | corresponding to the |
   |                      |             |      | Patient Support      |
   |                      |             |      | Device in use.       |
   |                      |             |      |                      |
   |                      |             |      | Required if Patient  |
   |                      |             |      | Support Position     |
   |                      |             |      | Specification Method |
   |                      |             |      | (300A,065C) equals   |
   |                      |             |      | DEVICE_SPECIFIC.     |
   +----------------------+-------------+------+----------------------+
   | >Device Order Index  | (300A,065E) | 1C   | Index defining the   |
   |                      |             |      | order in which the   |
   |                      |             |      | Items in the Patient |
   |                      |             |      | Support Position     |
   |                      |             |      | Device Parameter     |
   |                      |             |      | Sequence (300A,065D) |
   |                      |             |      | are applied.         |
   |                      |             |      |                      |
   |                      |             |      | The value shall      |
   |                      |             |      | start at 1 and       |
   |                      |             |      | increase             |
   |                      |             |      | monotonically by 1.  |
   |                      |             |      |                      |
   |                      |             |      | Required if Patient  |
   |                      |             |      | Support Position     |
   |                      |             |      | Specification Method |
   |                      |             |      | (300A,065C) equals   |
   |                      |             |      | DEVICE_SPECIFIC.     |
   |                      |             |      |                      |
   |                      |             |      | See `Position        |
   |                      |             |      | Parameters and Order |
   |                      |             |      | Index                |
   |                      |             |      |  <#sect_10.40.1>`__. |
   +----------------------+-------------+------+----------------------+
   | >Patient Support     | (300A,065B) | 1    | Translational and    |
   | Position Parameter   |             |      | rotational           |
   | Sequence             |             |      | parameters for a     |
   |                      |             |      | particular Patient   |
   |                      |             |      | Support device.      |
   |                      |             |      |                      |
   |                      |             |      | One or more Items    |
   |                      |             |      | shall be included in |
   |                      |             |      | this Sequence.       |
   +----------------------+-------------+------+----------------------+
   | >>Patient Support    | (300A,065F) | 1C   | Index defining the   |
   | Position Parameter   |             |      | order in which the   |
   | Order Index          |             |      | Items in the Patient |
   |                      |             |      | Support Position     |
   |                      |             |      | Parameter Sequence   |
   |                      |             |      | (300A,065B) are      |
   |                      |             |      | applied.             |
   |                      |             |      |                      |
   |                      |             |      | The value shall      |
   |                      |             |      | start at 1 and       |
   |                      |             |      | increase             |
   |                      |             |      | monotonically by 1.  |
   |                      |             |      |                      |
   |                      |             |      | Required if Patient  |
   |                      |             |      | Support Position     |
   |                      |             |      | Specification Method |
   |                      |             |      | (300A,065C) equals   |
   |                      |             |      | DEVICE_SPECIFIC.     |
   |                      |             |      |                      |
   |                      |             |      | See `Position        |
   |                      |             |      | Parameters and Order |
   |                      |             |      | Index                |
   |                      |             |      |  <#sect_10.40.1>`__. |
   +----------------------+-------------+------+----------------------+
   | *>>Incl              | *D.*        |      |                      |
   | ude*\ `table_title < |             |      |                      |
   | #table_10-2>`__\ *.* |             |      |                      |
   +----------------------+-------------+------+----------------------+

.. _sect_10.40.1:

Position Parameters and Order Index
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Device Order Index (300A,065E) and thePatient Support Position
Parameter Order Index (300A,065F) are applied sequentially, meaning all
the Items in a Patient Support Position Parameter Sequence (300A,065B)
are applied before proceeding to the Item in the Patient Support
Position Device Parameter Sequence (300A,065D) specified by the next
Device Order Index (300A,065E) value.

A vendor may specify codes that are not included in TID 175001 and/or a
set of codes which is not identical with the set defined in `IEC 61217
Patient Support Device <#sect_10.40.1.1>`__ or `Isocentric Patient
Support Device <#sect_10.40.1.2>`__. The vendor shall document the codes
used in this Macro in the Conformance Statement, as well as the
corresponding parameters, their geometric interpretation, and the order
in which they will be applied. These parameters shall use UCUM units of
mm for lengths and degrees for angles.

.. _sect_10.40.1.1:

IEC 61217 Patient Support Device
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Devices using the IEC 61217 coordinate systems to define geometric
settings for the Patient Support device shall use the codes in
`table_title <#table_10.40-2>`__ in the order specified in column
Patient Support Position Parameter Order Index (300A,065F). Other codes
shall not be used.

.. table:: Isocentric Patient Support Position Parameter Order Index

   +----------------------+----------------------+----------------------+
   | Code Value           | Code Meaning         | Patient Support      |
   | (0008,0100)          | (0008,0104)          | Position Parameter   |
   |                      |                      | Order Index          |
   |                      |                      | (300A,065F)          |
   +======================+======================+======================+
   | 126801               | IEC61217 Patient     | 1                    |
   |                      | Support Continuous   |                      |
   |                      | Yaw Angle            |                      |
   +----------------------+----------------------+----------------------+
   | 126806               | IEC61217 Table Top   | 2                    |
   |                      | Lateral Position     |                      |
   +----------------------+----------------------+----------------------+
   | 126807               | IEC61217 Table Top   | 3                    |
   |                      | Longitudinal         |                      |
   |                      | Position             |                      |
   +----------------------+----------------------+----------------------+
   | 126808               | IEC61217 Table Top   | 4                    |
   |                      | Vertical Position    |                      |
   +----------------------+----------------------+----------------------+
   | 126802               | IEC61217 Table Top   | 5                    |
   |                      | Support Continuous   |                      |
   |                      | Pitch Angle          |                      |
   +----------------------+----------------------+----------------------+
   | 126803               | IEC61217 Table Top   | 6                    |
   |                      | Support Continuous   |                      |
   |                      | Roll Angle           |                      |
   +----------------------+----------------------+----------------------+

.. _sect_10.40.1.2:

Isocentric Patient Support Device
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Devices using an isocentric representation to define geometric settings
for the Patient Support device shall use the codes in
`table_title <#table_10.40-3>`__ in the order specified in column
Patient Support Position Parameter Order Index (300A,065F). Other codes
shall not be used.

.. table:: Isocentric Patient Support Position Parameter Order Index

   +----------------------+----------------------+----------------------+
   | Code Value           | Code Meaning         | Patient Support      |
   | (0008,0100)          | (0008,0104)          | Position Parameter   |
   |                      |                      | Order Index          |
   |                      |                      | (300A,065F)          |
   +======================+======================+======================+
   | 126814               | Isocentric Patient   | 1                    |
   |                      | Support Continuous   |                      |
   |                      | Yaw Angle            |                      |
   +----------------------+----------------------+----------------------+
   | 126812               | Isocentric Patient   | 2                    |
   |                      | Support Continuous   |                      |
   |                      | Pitch Angle          |                      |
   +----------------------+----------------------+----------------------+
   | 126813               | Isocentric Patient   | 3                    |
   |                      | Support Continuous   |                      |
   |                      | Roll Angle           |                      |
   +----------------------+----------------------+----------------------+
   | 126815               | Isocentric Patient   | 4                    |
   |                      | Support Lateral      |                      |
   |                      | Position             |                      |
   +----------------------+----------------------+----------------------+
   | 126816               | Isocentric Patient   | 5                    |
   |                      | Support Longitudinal |                      |
   |                      | Position             |                      |
   +----------------------+----------------------+----------------------+
   | 126817               | Isocentric Patient   | 6                    |
   |                      | Support Vertical     |                      |
   |                      | Position             |                      |
   +----------------------+----------------------+----------------------+

