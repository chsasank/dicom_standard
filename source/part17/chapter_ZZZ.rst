.. _chapter_ZZZ:

Content Assessment (Informative)
================================

The following use cases exemplify the use of Content Assessment Results
IOD.

.. _sect_ZZZ.1:

RT Plan Treatment Assessment Use Case
-------------------------------------

A RT Plan SOP Instance is sent from a Treatment Planning System (TPS) to
a Quality Assurance (QA) Application and to the Treatment Management
System (TMS). The TMS de-composes the content for internal storage. At
the time of treatment the TMS re-composes the Instance and sends it to
the operator console of the linear accelerator. However, during
re-composition an error occurs and one jaw specification is omitted from
the recomposed Instance and the Beam Dose in the Fraction Scheme Module
is set to 0.0.

The operator console requests the QA Application to perform an
assessment to compare the copy of the Instance received from the
operator console with the copy of the Instance received earlier from the
TPS. The QA Application retrieves the Instance from the operator
console. The QA Application also performs an assessment by
re-calculation of the dosimetric parameters in the assessed plan.
Although the Beam Meterset in the assessed plan (from the operator
console) is the same as the Beam Meterset in the comparison plan (from
the TPS) , the Beam Meterset re-calculated by the QA Application is
different due to the missing jaw. Further on it is detected, that all
Beam Dose values have the value 0.0.

Beam Meterset for the current treatment device in this example is
expressed in Monitor Units.

.. table:: Content Assessment Results Module Example of a RT Plan
Treatment Assessment

   +----------+-----------------+---------------+----+-----------------+
   | Nesting  | Attribute Name  | Tag           | VR | Value           |
   +==========+=================+===============+====+=================+
   |          | Assessment      | (0082,0023)   | LO | Pre-Treatment   |
   |          | Label           |               |    | Assessment of   |
   |          |                 |               |    | Fraction 7      |
   +----------+-----------------+---------------+----+-----------------+
   |          | Assessment Type | (0082,0021)   | SQ |                 |
   |          | Code Sequence   |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   | %item    |                 |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   |          | >Code Value     | (0008,0100)   | SH | 121373          |
   +----------+-----------------+---------------+----+-----------------+
   |          | >Coding Scheme  | (0008,0102)   | SH | DCM             |
   |          | Designator      |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   |          | >Code Meaning   | (0008,0104)   | LO | RT              |
   |          |                 |               |    | Pre-Treatment   |
   |          |                 |               |    | Consistency     |
   |          |                 |               |    | Check           |
   +----------+-----------------+---------------+----+-----------------+
   | %enditem |                 |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   | %endsq   | (Assessment     |               |    |                 |
   |          | Type Code       |               |    |                 |
   |          | Sequence)       |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   |          | Assessment Set  | (0082,0016)   | LO | ID12345         |
   |          | ID              |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   |          | Assessment      | (0082,0017)   | SQ |                 |
   |          | Requester       |               |    |                 |
   |          | Sequence        |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   | %item    |                 |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   |          | >Observer Type  | (0040,A084)   | CS | DEV             |
   +----------+-----------------+---------------+----+-----------------+
   |          | >Station Name   | (0008,1010)   | SH | CONSOLE 1       |
   +----------+-----------------+---------------+----+-----------------+
   |          | >Device UID     | (0018,1002)   | UI | 1.2.3           |
   |          |                 |               |    | .4.5.6.7.8.9.10 |
   +----------+-----------------+---------------+----+-----------------+
   |          | >Manufacturer   | (0008,0070)   | LO | Fancy Linac     |
   |          |                 |               |    | Inc.            |
   +----------+-----------------+---------------+----+-----------------+
   |          | >Manufacturer's | (0008,1090)   | LO | Linear          |
   |          | Model Name      |               |    | Accelerator     |
   |          |                 |               |    | Console         |
   +----------+-----------------+---------------+----+-----------------+
   |          | >Institution    | (0008,0080)   | LO | RT Clinic 1     |
   |          | Name            |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   |          | >Institution    | (0008,0082)   | SQ |                 |
   |          | Code Sequence   |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   | %item    |                 |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   |          | >>Code Value    | (0080,0100)   | SH | Clinic1         |
   +----------+-----------------+---------------+----+-----------------+
   |          | >>Coding Scheme | (0008,0102)   | SH | 99MyCounty      |
   |          | Designator      |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   |          | >>Code Meaning  | (0008,0104)   | LO | RT Clinic 1     |
   +----------+-----------------+---------------+----+-----------------+
   | %enditem |                 |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   | %endsq   | (>Institution   |               |    |                 |
   |          | Code Sequence)  |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   | %enditem |                 |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   | %endsq   | (Assessment     |               |    |                 |
   |          | Requester       |               |    |                 |
   |          | Sequence)       |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   |          | Assessed SOP    | (0082,0004)   | SQ |                 |
   |          | Instance        |               |    |                 |
   |          | Sequence        |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   | %item    |                 |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   |          | >Referenced SOP | (0008,1150)   | UI | 1.2.840.10008.  |
   |          | Class UID       |               |    | 5.1.4.1.1.481.5 |
   |          |                 |               |    | (RT Plan        |
   |          |                 |               |    | Storage)        |
   +----------+-----------------+---------------+----+-----------------+
   |          | >Referenced SOP | (0008,1155)   | UI | 1.2.3.4.5.300   |
   |          | Instance UID    |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   | %enditem |                 |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   |          | >Referenced     | (0082,0005)   | SQ |                 |
   |          | Comparison SOP  |               |    |                 |
   |          | Instance        |               |    |                 |
   |          | Sequence        |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   | %item    |                 |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   |          | >>Referenced    | (0008,1150)   | UI | 1.2.840.10008.  |
   |          | SOP Class UID   |               |    | 5.1.4.1.1.481.5 |
   |          |                 |               |    | (RT Plan        |
   |          |                 |               |    | Storage)        |
   +----------+-----------------+---------------+----+-----------------+
   |          | >>Referenced    | (0008,1155)   | UI | 1.2.3.4.5.300   |
   |          | SOP Instance    |               |    |                 |
   |          | UID             |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   | %enditem |                 |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   | %endsq   | (>Referenced    |               |    |                 |
   |          | Comparison SOP  |               |    |                 |
   |          | Instance        |               |    |                 |
   |          | Sequence)       |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   | %enditem |                 |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   | %endsq   | (Assessed SOP   |               |    |                 |
   |          | Instance        |               |    |                 |
   |          | Sequence)       |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   |          | Assessment      | (0082,0001)   | CS | FAILED          |
   |          | Summary         |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   |          | Assessment      | (0082,0003)   | UT | Plan Checker    |
   |          | Summary         |               |    | result: Failed! |
   |          | Description     |               |    |                 |
   |          |                 |               |    | The assessed RT |
   |          |                 |               |    | Plan does not   |
   |          |                 |               |    | match the       |
   |          |                 |               |    | reference RT    |
   |          |                 |               |    | Plan it is      |
   |          |                 |               |    | compared to.    |
   |          |                 |               |    | One or more     |
   |          |                 |               |    | relevant        |
   |          |                 |               |    | Attributes are  |
   |          |                 |               |    | not equal.      |
   |          |                 |               |    | Monitor Unit    |
   |          |                 |               |    | values and Beam |
   |          |                 |               |    | Doses have      |
   |          |                 |               |    | unreasonable    |
   |          |                 |               |    | values.         |
   +----------+-----------------+---------------+----+-----------------+
   |          | Number of       | (0082,0006)   | UL | 3               |
   |          | Assessment      |               |    |                 |
   |          | Observations    |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   |          | Assessment      | (0082,0007)   | SQ |                 |
   |          | Observations    |               |    |                 |
   |          | Sequence        |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   | %item    |                 |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   |          | >Observation    | (0082,0008)   | CS | MAJOR           |
   |          | Significance    |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   |          | >Observation    | (0082,0022)   | SQ |                 |
   |          | Basis Code      |               |    |                 |
   |          | Sequence        |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   | %item    |                 |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   |          | >>Code Value    | (0008,0100)   | SH | 121375          |
   +----------+-----------------+---------------+----+-----------------+
   |          | >>Coding Scheme | (0008,0102)   | SH | DCM             |
   |          | Designator      |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   |          | >>Code Meaning  | (0008,0104)   | LO | Assessment By   |
   |          |                 |               |    | Comparison      |
   +----------+-----------------+---------------+----+-----------------+
   | %enditem |                 |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   | %endsq   | (>Assessment    |               |    |                 |
   |          | Basis Code      |               |    |                 |
   |          | Sequence)       |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   |          | >Observation    | (0082,000A)   | UT | Attribute value |
   |          | Description     |               |    | of Leaf/Jaw     |
   |          |                 |               |    | Positions is    |
   |          |                 |               |    | not equal.      |
   +----------+-----------------+---------------+----+-----------------+
   |          | >Structured     | (0082,000C)   | SQ |                 |
   |          | Constraint      |               |    |                 |
   |          | Observation     |               |    |                 |
   |          | Sequence        |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   | %item    |                 |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   |          | >>Selector      | (0082,0018)   | LO | Leaf/Jaw        |
   |          | Attribute Name  |               |    | Positions       |
   +----------+-----------------+---------------+----+-----------------+
   |          | >>Selector      | (0072,0050)   | CS | DS              |
   |          | Attribute VR    |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   |          | >>Selector      | (0072,0026)   | AT | 300A011C        |
   |          | Attribute       |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   |          | >>Selector      | (0072,0028) ) | US | 1               |
   |          | Value Number    |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   |          | >>Selector      | (0072,0052)   | AT | 300A00B0\30     |
   |          | Sequence        |               |    | 0A0111\300A011A |
   |          | Pointer         |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   |          | >>Selector      | (0074,1057)   | IS | 1\2\2           |
   |          | Sequence        |               |    |                 |
   |          | Pointer Items   |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   |          | >>Constraint    | (0082,0032)   | CS | EQUAL           |
   |          | Type            |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   |          | >>Constraint    | (0082,0036)   | CS | FAILURE         |
   |          | Violation       |               |    |                 |
   |          | Significance    |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   |          | >>Constraint    | (0082,0034)   | SQ |                 |
   |          | Value Sequence  |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   | %item    |                 |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   |          | >>>Selector DS  | (0072,0072)   | DS | -75.000\75.000  |
   |          | Value           |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   | %enditem |                 |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   | %endsq   | (>>Constraint   |               |    |                 |
   |          | Value Sequence) |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   |          | >>Assessed      | (0082,0010)   | SQ |                 |
   |          | Attribute Value |               |    |                 |
   |          | Sequence        |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   | %item    |                 |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   |          | >>>Selector DS  | (0072,0072)   | DS | -75.000         |
   |          | Value           |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   | %enditem |                 |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   | %endsq   | (>>Assessed     |               |    |                 |
   |          | Attribute Value |               |    |                 |
   |          | Sequence)       |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   | %enditem |                 |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   | %endsq   | (>Constraint    |               |    |                 |
   |          | Observation     |               |    |                 |
   |          | Sequence)       |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   | %enditem |                 |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   | %item    |                 |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   |          | >Observation    | (0082,0008)   | CS | MAJOR           |
   |          | Significance    |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   |          | >Observation    | (0082,0022)   | SQ |                 |
   |          | Basis Code      |               |    |                 |
   |          | Sequence        |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   | %item    |                 |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   |          | >>Code Value    | (0008,0100)   | SH | 121376          |
   +----------+-----------------+---------------+----+-----------------+
   |          | >>Coding Scheme | (0008,0102)   | SH | DCM             |
   |          | Designator      |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   |          | >>Code Meaning  | (0008,0104)   | LO | Assessment By   |
   |          |                 |               |    | Quality Rules   |
   +----------+-----------------+---------------+----+-----------------+
   | %enditem |                 |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   | %endsq   | (>Assessment    |               |    |                 |
   |          | Basis Code      |               |    |                 |
   |          | Sequence)       |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   |          | >Observation    | (0082,000A)   | UT | Monitor Units   |
   |          | Description     |               |    | re-calculation  |
   |          |                 |               |    | failed. The     |
   |          |                 |               |    | re-calculation  |
   |          |                 |               |    | of the beam     |
   |          |                 |               |    | meterset        |
   |          |                 |               |    | resulted in a   |
   |          |                 |               |    | different value |
   |          |                 |               |    | (76MU) than the |
   |          |                 |               |    | value in the    |
   |          |                 |               |    | assessed RT     |
   |          |                 |               |    | Plan. This      |
   |          |                 |               |    | value is        |
   |          |                 |               |    | outside the     |
   |          |                 |               |    | tolerance of    |
   |          |                 |               |    | reasonable      |
   |          |                 |               |    | differences     |
   |          |                 |               |    | acceptable on   |
   |          |                 |               |    | re-calculation. |
   +----------+-----------------+---------------+----+-----------------+
   |          | >Structured     | (0082,000C)   | SQ |                 |
   |          | Constraint      |               |    |                 |
   |          | Observation     |               |    |                 |
   |          | Sequence        |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   | %item    |                 |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   |          | >>Selector      | (0082,0018)   | LO | Beam Meterset   |
   |          | Attribute Name  |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   |          | >>Selector      | (0072,0050)   | CS | DS              |
   |          | Attribute VR    |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   |          | >>Selector      | (0072,0026)   | AT | 300A0086        |
   |          | Attribute       |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   |          | >>Selector      | (0072,0028) ) | US | 1               |
   |          | Value Number    |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   |          | >>Selector      | (0072,0052)   | AT | 30              |
   |          | Sequence        |               |    | 0A0070\300C0004 |
   |          | Pointer         |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   |          | >>Selector      | (0074,1057)   | IS | 1\1             |
   |          | Sequence        |               |    |                 |
   |          | Pointer Items   |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   |          | >>Constraint    | (0082,0032)   | CS | RANGE_INCL      |
   |          | Type            |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   |          | >>Constraint    | (0082,0036)   | CS | FAILURE         |
   |          | Violation       |               |    |                 |
   |          | Significance    |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   |          | >>Constraint    | (0082,0034)   | SQ |                 |
   |          | Value Sequence  |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   | %item    |                 |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   |          | >>>Selector DS  | (0072,0072)   | DS | 68              |
   |          | Value           |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   | %enditem |                 |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   | %item    |                 |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   |          | >>>Selector DS  | (0072,0072)   | DS | 84              |
   |          | Value           |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   | %enditem |                 |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   | %endsq   | (>>Constraint   |               |    |                 |
   |          | Value Sequence) |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   |          | >>Assessed      | (0082,0010)   | SQ |                 |
   |          | Attribute Value |               |    |                 |
   |          | Sequence        |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   | %item    |                 |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   |          | >>>Selector DS  | (0072,0072)   | DS | 108             |
   |          | Value           |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   | %enditem |                 |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   | %endsq   | (>>Assessed     |               |    |                 |
   |          | Attribute Value |               |    |                 |
   |          | Sequence)       |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   | %enditem |                 |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   | %endsq   | (>Constraint    |               |    |                 |
   |          | Observation     |               |    |                 |
   |          | Sequence)       |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   | %enditem |                 |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   | %item    |                 |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   |          | >Observation    | (0082,0008)   | CS | MODERATE        |
   |          | Significance    |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   |          | >Observation    | (0082,0022)   | SQ |                 |
   |          | Basis Code      |               |    |                 |
   |          | Sequence        |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   | %item    |                 |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   |          | >>Code Value    | (0008,0100)   | SH | 121376          |
   +----------+-----------------+---------------+----+-----------------+
   |          | >>Coding Scheme | (0008,0102)   | SH | DCM             |
   |          | Designator      |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   |          | >>Code Meaning  | (0008,0104)   | LO | Assessment By   |
   |          |                 |               |    | Quality Rules   |
   +----------+-----------------+---------------+----+-----------------+
   | %enditem |                 |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   | %endsq   | (>Observation   |               |    |                 |
   |          | Basis Code      |               |    |                 |
   |          | Sequence)       |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   |          | >Observation    | (0082,000A)   | UT | The Beam Dose   |
   |          | Description     |               |    | value of all    |
   |          |                 |               |    | Beams is zero,  |
   |          |                 |               |    | but Beam        |
   |          |                 |               |    | Meterset is     |
   |          |                 |               |    | non-zero.       |
   +----------+-----------------+---------------+----+-----------------+
   | %enditem |                 |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+
   | %endsq   | (Assessment     |               |    |                 |
   |          | Observations    |               |    |                 |
   |          | Sequence)       |               |    |                 |
   +----------+-----------------+---------------+----+-----------------+

