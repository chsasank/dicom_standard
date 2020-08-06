.. _chapter_EE:

Display System Management Service Class (Normative)
===================================================

.. _sect_EE.1:

Scope
-----

The Display System Service Class allows service users retrieve
parameters related to the Display Subsystem(s).

.. _sect_EE.2:

Display System SOP Class
------------------------

.. _sect_EE.2.1:

IOD Description
~~~~~~~~~~~~~~~

The Display System IOD is an abstraction of the soft-copy display system
and is the basic Information Entity to monitor the status of a Display
System. The Display System SOP Instance is created by the SCP during
start-up of the Display System and has a well-known SOP Instance UID.

.. _sect_EE.2.2:

DIMSE Service Group
~~~~~~~~~~~~~~~~~~~

The DIMSE Service shown in `table_title <#table_EE.2.2-1>`__ is
applicable to the Display System IOD under the Display System SOP Class.

.. table:: DIMSE Service Group Applicable to Display System

   ============================= =============
   DICOM Message Service Element Usage SCU/SCP
   ============================= =============
   N-GET                         M/M
   ============================= =============

This section describes the behavior of the DIMSE services that are
specific for this IOD. The general behavior of the DIMSE services is
specified in .

.. _sect_EE.2.2.1:

N-GET
^^^^^

N-GET is used to retrieve information from an instance of the Display
System SOP Class.

.. _sect_EE.2.2.1.1:

Attributes
''''''''''

.. _sect_EE.2.2.1.1.1:

Display Subsystem Macros
                        

To reduce the size and complexity of
`table_title <#table_EE.2.2.1-2>`__, a macro notation is used.

.. table:: Table Result Context Macro

   +--------------------------+-------------+--------------------------+
   | Attribute Name           | Tag         | Usage SCU/SCP            |
   +==========================+=============+==========================+
   | Performed Procedure Step | (0040,4050) | -/1                      |
   | Start DateTime           |             |                          |
   +--------------------------+-------------+--------------------------+
   | Performed Procedure Step | (0040,4051) | -/1                      |
   | End DateTime             |             |                          |
   +--------------------------+-------------+--------------------------+
   | Actual Human Performer   | (0040,4035) | 3/2                      |
   | Sequence                 |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Human Performer Code    | (0040,4009) | -/1C                     |
   | Sequence                 |             |                          |
   |                          |             | (Required if Human       |
   |                          |             | Performer's Name         |
   |                          |             | (0040,4037) is not       |
   |                          |             | present.)                |
   +--------------------------+-------------+--------------------------+
   | *>>Include*\ `table_tit  |             |                          |
   | le <#table_CC.2.5-2a>`__ |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Human Performer's Name  | (0040,4037) | -/1C                     |
   |                          |             |                          |
   |                          |             | (Required if Human       |
   |                          |             | Performer Code Sequence  |
   |                          |             | (0040,4009) is not       |
   |                          |             | present.)                |
   +--------------------------+-------------+--------------------------+
   | >Human Performer's       | (0040,4036) | -/2                      |
   | Organization             |             |                          |
   +--------------------------+-------------+--------------------------+
   | Measurement Equipment    | (0028,7012) | 3/2                      |
   | Sequence                 |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Measurement Functions   | (0028,7013) | -/1                      |
   +--------------------------+-------------+--------------------------+
   | >Measured                | (0028,7026) | -/1                      |
   | Characteristics          |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Measurement Equipment   | (0028,7014) | -/1                      |
   | Type                     |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Manufacturer            | (0008,0070) | -/1                      |
   +--------------------------+-------------+--------------------------+
   | >Manufacturer's Model    | (0008,1090) | -/1                      |
   | Name                     |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Device Serial Number    | (0018,1000) | -/2                      |
   +--------------------------+-------------+--------------------------+
   | >DateTime of Last        | (0018,1202) | -/2                      |
   | Calibration              |             |                          |
   +--------------------------+-------------+--------------------------+

.. _sect_EE.2.2.1.1.2:

Display System N-GET Attribute Requirements
                                           

The attributes that may be retrieved are shown in
`table_title <#table_EE.2.2.1-2>`__.

.. table:: Display System N-GET Attributes

   +--------------------------+-------------+--------------------------+
   | Attribute Name           | Tag         | Usage SCU/SCP            |
   +==========================+=============+==========================+
   | Specific Character Set   | (0008,0005) | -/1C                     |
   |                          |             |                          |
   |                          |             | (Required if an extended |
   |                          |             | or replacement character |
   |                          |             | set is used)             |
   +--------------------------+-------------+--------------------------+
   | **Display System         |             |                          |
   | Module**                 |             |                          |
   +--------------------------+-------------+--------------------------+
   | Manufacturer             | (0008,0070) | 3/1                      |
   +--------------------------+-------------+--------------------------+
   | Institution Name         | (0008,0080) | 3/1                      |
   +--------------------------+-------------+--------------------------+
   | Institution Address      | (0008,0081) | 3/1                      |
   +--------------------------+-------------+--------------------------+
   | Device Serial Number     | (0018,1000) | 3/1                      |
   +--------------------------+-------------+--------------------------+
   | Station Name             | (0008,1010) | 3/2                      |
   +--------------------------+-------------+--------------------------+
   | Institutional Department | (0008,1040) | 3/2                      |
   | Name                     |             |                          |
   +--------------------------+-------------+--------------------------+
   | Institutional Department | (0008,1041) | 3/3                      |
   | Type Code Sequence       |             |                          |
   +--------------------------+-------------+--------------------------+
   | Manufacturer's Model     | (0008,1090) | 3/1                      |
   | Name                     |             |                          |
   +--------------------------+-------------+--------------------------+
   | Equipment Administrator  | (0028,7000) | 3/2                      |
   | Sequence                 |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Person Name             | (0040,A123) | -/2                      |
   +--------------------------+-------------+--------------------------+
   | >Person Identification   | (0040,1101) | -/1                      |
   | Code Sequence            |             |                          |
   +--------------------------+-------------+--------------------------+
   | *>>Include*\ `table_tit  |             |                          |
   | le <#table_CC.2.5-2a>`__ |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Person's Address        | (0040,1102) | -/3                      |
   +--------------------------+-------------+--------------------------+
   | >Person's Telephone      | (0040,1103) | -/3                      |
   | Numbers                  |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Institution Name        | (0008,0080) | -/1C                     |
   |                          |             |                          |
   |                          |             | (Required if Institution |
   |                          |             | Code Sequence            |
   |                          |             | (0008,0082) is not       |
   |                          |             | present. May be present  |
   |                          |             | otherwise.)              |
   +--------------------------+-------------+--------------------------+
   | >Institution Address     | (0008,0081) | -/3                      |
   +--------------------------+-------------+--------------------------+
   | >Institution Code        | (0008,0082) | -/1C                     |
   | Sequence                 |             |                          |
   |                          |             | (Required if Institution |
   |                          |             | Name (0008,0080) is not  |
   |                          |             | present.May be present   |
   |                          |             | otherwise.)              |
   +--------------------------+-------------+--------------------------+
   | *>>Include*\ `table_tit  |             |                          |
   | le <#table_CC.2.5-2a>`__ |             |                          |
   +--------------------------+-------------+--------------------------+
   | Number of Display        | (0028,7001) | 3/1                      |
   | Subsystems               |             |                          |
   +--------------------------+-------------+--------------------------+
   | Display Subsystem        | (0028,7023) | 3/1                      |
   | Sequence                 |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Display Subsystem ID    | (0028,7003) | -/1                      |
   +--------------------------+-------------+--------------------------+
   | >Display Subsystem Name  | (0028,7004) | -/2                      |
   +--------------------------+-------------+--------------------------+
   | >Display Subsystem       | (0028,7005) | -/2                      |
   | Description              |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Display Device Type     | (0028,7022) | -/2                      |
   | Code Sequence            |             |                          |
   +--------------------------+-------------+--------------------------+
   | *>>Include*\ `table_tit  |             |                          |
   | le <#table_CC.2.5-2a>`__ |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Manufacturer            | (0008,0070) | -/2                      |
   +--------------------------+-------------+--------------------------+
   | >Device Serial Number    | (0018,1000) | -/2                      |
   +--------------------------+-------------+--------------------------+
   | >Manufacturer's Model    | (0008,1090) | -/2                      |
   | Name                     |             |                          |
   +--------------------------+-------------+--------------------------+
   | >System Status           | (0028,7006) | -/1                      |
   +--------------------------+-------------+--------------------------+
   | >System Status Comment   | (0028,7007) | -/2                      |
   +--------------------------+-------------+--------------------------+
   | >Display Subsystem       | (0028,700A) | -/2                      |
   | Configuration Sequence   |             |                          |
   +--------------------------+-------------+--------------------------+
   | >>Configuration ID       | (0028,700B) | -/1                      |
   +--------------------------+-------------+--------------------------+
   | >>Configuration Name     | (0028,700C) | -/2                      |
   +--------------------------+-------------+--------------------------+
   | >>Configuration          | (0028,700D) | -/2                      |
   | Description              |             |                          |
   +--------------------------+-------------+--------------------------+
   | >>Referenced Target      | (0028,700E) | -/2                      |
   | Luminance                |             |                          |
   | Characteristics ID       |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Current Configuration   | (0028,7002) | -/2                      |
   | ID                       |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Measurement Equipment   | (0028,7012) | -/2                      |
   | Sequence                 |             |                          |
   +--------------------------+-------------+--------------------------+
   | >>Measurement Functions  | (0028,7013) | -/1                      |
   +--------------------------+-------------+--------------------------+
   | >>Measured               | (0028,7026) | -/1                      |
   | Characteristics          |             |                          |
   +--------------------------+-------------+--------------------------+
   | >>Measurement Equipment  | (0028,7014) | -/1                      |
   | Type                     |             |                          |
   +--------------------------+-------------+--------------------------+
   | >>Manufacturer           | (0008,0070) | -/1                      |
   +--------------------------+-------------+--------------------------+
   | >>Manufacturer's Model   | (0008,1090) | -/1                      |
   | Name                     |             |                          |
   +--------------------------+-------------+--------------------------+
   | >>Device Serial Number   | (0018,1000) | -/1                      |
   +--------------------------+-------------+--------------------------+
   | >>DateTime of Last       | (0018,1202) | -/2                      |
   | Calibration              |             |                          |
   +--------------------------+-------------+--------------------------+
   | **Target Luminance       |             |                          |
   | Characteristics Module** |             |                          |
   +--------------------------+-------------+--------------------------+
   | Target Luminance         | (0028,7008) | 2/1                      |
   | Characteristics Sequence |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Luminance               | (0028,7009) | -/1                      |
   | Characteristics ID       |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Display Function Type   | (0028,7019) | -/1                      |
   +--------------------------+-------------+--------------------------+
   | >Target Minimum          | (0028,701D) | -/1                      |
   | Luminance                |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Target Maximum          | (0028,701E) | -/1                      |
   | Luminance                |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Gamma Value             | (0028,701A) | -/1C                     |
   |                          |             |                          |
   |                          |             | (Required if the value   |
   |                          |             | of Display Function Type |
   |                          |             | (0028,7019) is GAMMA)    |
   +--------------------------+-------------+--------------------------+
   | >Number of Luminance     | (0028,701B) | -/1C                     |
   | Points                   |             |                          |
   |                          |             | (Required if the value   |
   |                          |             | of Display Function Type |
   |                          |             | (0028,7019) is           |
   |                          |             | USER_DEFINED)            |
   +--------------------------+-------------+--------------------------+
   | >Luminance Response      | (0028,701C) | -/1C                     |
   | Sequence                 |             |                          |
   |                          |             | (Required if the value   |
   |                          |             | of Display Function Type |
   |                          |             | (0028,7019) is           |
   |                          |             | USER_DEFINED)            |
   +--------------------------+-------------+--------------------------+
   | >>DDL Value              | (0028,7017) | -/1                      |
   +--------------------------+-------------+--------------------------+
   | >>Luminance Value        | (0028,701F) | -/1                      |
   +--------------------------+-------------+--------------------------+
   | >Luminance Response      | (0028,7020) | -/1C                     |
   | Description              |             |                          |
   |                          |             | (Required if the value   |
   |                          |             | of Display Function Type |
   |                          |             | (0028,7019) is           |
   |                          |             | USER_DEFINED. May be     |
   |                          |             | present otherwise.)      |
   +--------------------------+-------------+--------------------------+
   | >CIExy White Point       | (0028,7018) | -/3                      |
   +--------------------------+-------------+--------------------------+
   | >Reflected Ambient Light | (2010,0160) | -/3                      |
   +--------------------------+-------------+--------------------------+
   | >Ambient Light Value     | (0028,7025) | -/1C                     |
   | Source                   |             |                          |
   |                          |             | (Required if Reflected   |
   |                          |             | Ambient Light            |
   |                          |             | (2010,0160) is present.) |
   +--------------------------+-------------+--------------------------+
   | **QA Results Module**    |             |                          |
   +--------------------------+-------------+--------------------------+
   | QA Results Sequence      | (0028,700F) | 3/1                      |
   +--------------------------+-------------+--------------------------+
   | >Display Subsystem ID    | (0028,7003) | -/1                      |
   +--------------------------+-------------+--------------------------+
   | >Display Subsystem QA    | (0028,7010) | -/2                      |
   | Results Sequence         |             |                          |
   +--------------------------+-------------+--------------------------+
   | >>Configuration ID       | (0028,700B) | -/1                      |
   +--------------------------+-------------+--------------------------+
   | >>Configuration QA       | (0028,7011) | -/2                      |
   | Results Sequence         |             |                          |
   +--------------------------+-------------+--------------------------+
   | >>>Display Calibration   | (0028,7016) | -/2                      |
   | Result Sequence          |             |                          |
   +--------------------------+-------------+--------------------------+
   | *>                       |             |                          |
   | >>>Include*\ `table_titl |             |                          |
   | e <#table_EE.2.2.1-1>`__ |             |                          |
   +--------------------------+-------------+--------------------------+
   | >>>>Luminance            | (0028,7009) | -/1                      |
   | Characteristics ID       |             |                          |
   +--------------------------+-------------+--------------------------+
   | >>>Visual Evaluation     | (0028,7015) | -/2                      |
   | Result Sequence          |             |                          |
   +--------------------------+-------------+--------------------------+
   | *>                       |             |                          |
   | >>>Include*\ `table_titl |             |                          |
   | e <#table_EE.2.2.1-1>`__ |             |                          |
   +--------------------------+-------------+--------------------------+
   | >>>>Visual Evaluation    | (0028,7028) | -/1                      |
   | Test Sequence            |             |                          |
   +--------------------------+-------------+--------------------------+
   | >>>>>Test Result         | (0028,7029) | -/1                      |
   +--------------------------+-------------+--------------------------+
   | >>>>>Test Result Comment | (0028,702A) | -/3                      |
   +--------------------------+-------------+--------------------------+
   | >>>>>Test Pattern Code   | (0028,702C) | -/3                      |
   | Sequence                 |             |                          |
   +--------------------------+-------------+--------------------------+
   | *>>                      |             |                          |
   | >>>>Include*\ `table_tit |             |                          |
   | le <#table_CC.2.5-2a>`__ |             |                          |
   +--------------------------+-------------+--------------------------+
   | >>>>>Referenced Image    | (0008,1140) | -/1C                     |
   | Sequence                 |             |                          |
   |                          |             | (Required if Test        |
   |                          |             | Pattern Code Sequence    |
   |                          |             | (0028,702C) is absent in |
   |                          |             | this item.May be present |
   |                          |             | otherwise.)              |
   +--------------------------+-------------+--------------------------+
   | >>>>>>Referenced SOP     | (0008,1150) | -/1                      |
   | Class UID                |             |                          |
   +--------------------------+-------------+--------------------------+
   | >>>>>>Referenced SOP     | (0008,1151) | -/1                      |
   | Instance UID             |             |                          |
   +--------------------------+-------------+--------------------------+
   | >>>>>>Referenced Frame   | (0008,1160) | -/1C                     |
   | Number                   |             |                          |
   |                          |             | (Required if the         |
   |                          |             | Referenced SOP Instance  |
   |                          |             | is a multi-frame image   |
   |                          |             | and the reference does   |
   |                          |             | not apply to all frames, |
   |                          |             | and Referenced Segment   |
   |                          |             | Number (0062,000B) is    |
   |                          |             | not present.)            |
   +--------------------------+-------------+--------------------------+
   | >>>>>>Referenced Segment | (0062,000B) | -/1C                     |
   | Number                   |             |                          |
   |                          |             | (Required if the         |
   |                          |             | Referenced SOP Instance  |
   |                          |             | is a Segmentation or     |
   |                          |             | Surface Segmentation and |
   |                          |             | the reference does not   |
   |                          |             | apply to all segments    |
   |                          |             | and Referenced Frame     |
   |                          |             | Number (0008,1160) is    |
   |                          |             | not present.)            |
   +--------------------------+-------------+--------------------------+
   | >>>>>>Test Image         | (0028,702B) | -/3                      |
   | Validation               |             |                          |
   +--------------------------+-------------+--------------------------+
   | >>>>Visual Evaluation    | (0028,702E) | -/1                      |
   | Method Code Sequence     |             |                          |
   +--------------------------+-------------+--------------------------+
   | *>                       |             |                          |
   | >>>>Include*\ `table_tit |             |                          |
   | le <#table_CC.2.5-2a>`__ |             |                          |
   +--------------------------+-------------+--------------------------+
   | >>>Luminance Uniformity  | (0028,7027) | -/2                      |
   | Result Sequence          |             |                          |
   +--------------------------+-------------+--------------------------+
   | *>                       |             |                          |
   | >>>Include*\ `table_titl |             |                          |
   | e <#table_EE.2.2.1-1>`__ |             |                          |
   +--------------------------+-------------+--------------------------+
   | >>>>Number of Luminance  | (0028,701B) | -/1                      |
   | Points                   |             |                          |
   +--------------------------+-------------+--------------------------+
   | >>>>Measurement Pattern  | (0028,702D) | -/1                      |
   | Code Sequence            |             |                          |
   +--------------------------+-------------+--------------------------+
   | *>                       |             |                          |
   | >>>>Include*\ `table_tit |             |                          |
   | le <#table_CC.2.5-2a>`__ |             |                          |
   +--------------------------+-------------+--------------------------+
   | >>>>DDL Value            | (0028,7017) | -/1                      |
   +--------------------------+-------------+--------------------------+
   | >>>>White Point Flag     | (0028,7021) | -/1                      |
   +--------------------------+-------------+--------------------------+
   | >>>>Luminance Response   | (0028,701C) | -/1                      |
   | Sequence                 |             |                          |
   +--------------------------+-------------+--------------------------+
   | >>>>>Luminance Value     | (0028,701F) | -/1                      |
   +--------------------------+-------------+--------------------------+
   | >>>>>CIExy White Point   | (0028,7018) | -/1C                     |
   |                          |             |                          |
   |                          |             | (Required if the value   |
   |                          |             | of White Point Flag      |
   |                          |             | (0028,7021) is YES.)     |
   +--------------------------+-------------+--------------------------+
   | >>>>Reflected Ambient    | (2010,0160) | -/3                      |
   | Light                    |             |                          |
   +--------------------------+-------------+--------------------------+
   | >>>>>Ambient Light Value | (0028,7025) | -/1C                     |
   | Source                   |             |                          |
   |                          |             | (Required if Reflected   |
   |                          |             | Ambient Light            |
   |                          |             | (2010,0160) is present.) |
   +--------------------------+-------------+--------------------------+
   | >>>Luminance Result      | (0028,7024) | -/2                      |
   | Sequence                 |             |                          |
   +--------------------------+-------------+--------------------------+
   | *>                       |             |                          |
   | >>>Include*\ `table_titl |             |                          |
   | e <#table_EE.2.2.1-1>`__ |             |                          |
   +--------------------------+-------------+--------------------------+
   | >>>>Number of Luminance  | (0028,701B) | -/1                      |
   | Points                   |             |                          |
   +--------------------------+-------------+--------------------------+
   | >>>>Luminance Response   | (0028,701C) | -/1                      |
   | Sequence                 |             |                          |
   +--------------------------+-------------+--------------------------+
   | >>>>>DDL Value           | (0028,7017) | -/1                      |
   +--------------------------+-------------+--------------------------+
   | >>>>>Luminance Value     | (0028,701F) | -/1                      |
   +--------------------------+-------------+--------------------------+
   | >>>>>CIExy White Point   | (0028,7018) | -/3                      |
   +--------------------------+-------------+--------------------------+
   | >>>>Reflected Ambient    | (2010,0160) | -/3                      |
   | Light                    |             |                          |
   +--------------------------+-------------+--------------------------+
   | >>>>Ambient Light Value  | (0028,7025) | -/1C                     |
   | Source                   |             |                          |
   |                          |             | (Required if Reflected   |
   |                          |             | Ambient Light            |
   |                          |             | (2010,0160) is present.) |
   +--------------------------+-------------+--------------------------+

.. _sect_EE.2.2.1.2:

SCU Behavior
''''''''''''

The SCU uses the N-GET to request the SCP to provide the contents of a
Display System SOP Instance. The SCU shall specify in the N-GET request
primitive the UID of the SOP Instance from which attributes are to be
returned.

The SCU shall specify the list of Display System Attributes for which
values are to be returned. The SCU shall not specify Attributes which
are defined within a Sequence, but rather specify the sequence itself to
be returned in its entirety.

The SCU shall specify in the N-GET request primitive the well-known UID
of the SOP Instance.

.. _sect_EE.2.2.1.3:

SCP Behavior
''''''''''''

The SCP shall return the values for the specified Attributes of the
Display System SOP Instance.

The SCP shall return the status code for the requested SOP Instance
retrieval. The meaning of success, warning, and failure status codes are
defined in .

.. _sect_EE.2.3:

SOP Class Definitions and UIDs
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The SOP Class UID of the Display System SOP Class shall have the value
of "1.2.840.10008.5.1.1.40".

.. _sect_EE.2.4:

Reserved Identifications
~~~~~~~~~~~~~~~~~~~~~~~~

The well-known UID of the Display System SOP Instance shall have the
value of "1.2.840.10008.5.1.1.40.1".

.. _sect_EE.3:

Conformance
-----------

.. _sect_EE.3.1:

Conformance Statement
~~~~~~~~~~~~~~~~~~~~~

The implementation conformance statement of this SOP Class shall follow
.

The SCU Conformance Statement shall specify the following items:

-  Maximum number of associations to be supported at the same time

-  List of SOP Classes supported

-  For each of the supported SOP Classes:

   -  List of supported SOP Class attributes and DICOM Message Service
      Elements

   -  For each supported attribute (mandatory and optional), a valid
      value range

The SCP Conformance Statement shall specify the following items:

-  Maximum number of associations to be supported at the same time

-  List of SOP Classes supported

-  For each of the supported SOP Classes:

   -  List of supported SOP Class attributes and DICOM Message Service
      Elements

   -  For each supported attribute (mandatory and optional)

      -  Valid value range

      -  Default value if no value is supplied by the SCU

      -  Status code (Failure or Warning) if the SCU supplies a value
         that is out of range

-  For each supported DIMSE service

   -  SCP behavior for all specific status codes

